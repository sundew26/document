---
title: wechat-public
date: 2018/06/21
tags: javascript
---

## 如何判断用户是否已关注公众号

一、微信公众平台配置
---
### 1. 获取appid, appsecret，添加白名单

登录微信公众平台，进入基本配置。开发中需要用到两个参数，appId和appSecret（appSecret只展示一次，需保存下来，否则需要重置获取）。
获取access_token时需要添加IP白名单。
![clipboard.png](https://segmentfault.com/img/bVbcc8v)
点击查看
![clipboard.png](https://segmentfault.com/img/bVbcc7q)
点击修改
![clipboard.png](https://segmentfault.com/img/bVbcc7D)
### 2. 添加网页授权
进入公众号设置=》功能设置=》网页授权域名
![clipboard.png](https://segmentfault.com/img/bVbcdci)
点击设置，input框中输入授权回调页的域名参考第1点（只能填写一个），下载第3点中的txt文档，上传至服务器的根目录。
![clipboard.png](https://segmentfault.com/img/bVbcd5o)


二、php后端实现
---

微信开放接口全局返回码说明参考：https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1433747234

### 1. 获取全局token
此token有效期为2小时，可以暂存起来，过期后需要重新获取。
PS： 项目中必须走同一个接口，否则容易互刷导致过期。
```
public static function getToken($appid, $appsecret){
    $url = 'https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid='.$appid.'&secret='.$appsecret;
    return Curl::callWebServer($url);
}

正确返回结果：
    {
        "access_token": "ACCESS_TOKEN",
        "expires_in": 7200
    }
    返回结果参数说明：
    参数	          说明
    access_token	  获取到的全局token
    expires_in	    凭证有效时间，单位：秒
    
错误返回结果：
    {"errcode": 40013, "errmsg": "invalid appid"}
    返回结果参数说明：
    返回码	说明
    -1	   系统繁忙，此时请开发者稍候再试
    0	    请求成功
    40001	AppSecret错误或者AppSecret不属于这个公众号，请开发者确认        AppSecret的正确性
    40002	请确保grant_type字段值为client_credential
    40164	调用接口的IP地址不在白名单中，请在接口IP白名单中进行设置。（小程序及小游戏调用不要求IP地址在白名单内。）
```
### 2. 获取用户关联公众号的openid

分两步，先要获取到用户对公众号的授权码，然后拿这个码去获取临时access_token和openid。

获取用户授权码
```
public static function getCode($appId, $redirect_uri, $state=1, $scope='snsapi_base', $response_type='code'){
    $url = 'https://open.weixin.qq.com/connect/oauth2/authorize?appid='.$appId.'&redirect_uri='.$redirect_uri.'&response_type='.$response_type.'&scope='.$scope.'&state='.$state.'#wechat_redirect';
    header('Location: '.$url, true, 301);
}

正确返回结果：
    返回code码，并且跳转回调页面$redirect_uri
    
错误返回结果：
    {"errcode": 10003, "errmsg": "redirect_uri域名与后台配置不一致"}
    返回结果参数说明：
    返回码	说明
    10003	redirect_uri域名与后台配置不一致
    10004	此公众号被封禁
    10005	此公众号并没有这些scope的权限
    10006	必须关注此测试号
    10009	操作太频繁了，请稍后重试
    10010	scope不能为空
    10011	redirect_uri不能为空
    10012	appid不能为空
    10013	state不能为空
    10015	公众号未授权第三方平台，请检查授权状态
    10016	不支持微信开放平台的Appid，请使用公众号Appid
```
    
通过getCode获取到的code换取网页授权的access_token和openid
```
public static function getAccessToken($code, $appid, $appsecret, $grant_type='authorization_code'){
    $url = 'https://api.weixin.qq.com/sns/oauth2/access_token?appid='.$appid.'&secret='.$appsecret.'&code='.$code.'&grant_type='.$grant_type.'';
    return Curl::callWebServer($url);
}
   
正确返回结果：
    { 
        "access_token": "ACCESS_TOKEN",
        "expires_in": 7200,
        "refresh_token": "REFRESH_TOKEN",
        "openid": "OPENID",
        "scope": "SCOPE"
    }
    返回参数说明
    参数	        描述
    access_token	网页授权接口调用凭证,注意：此access_token与基础支持的access_token不同
    expires_in	access_token接口调用凭证超时时间，单位（秒）
    refresh_token	用户刷新access_token
    openid	用户唯一标识，请注意，在未关注公众号时，用户访问公众号的网页，也会产生一个用户和公众号唯一的OpenID
    scope	用户授权的作用域，使用逗号（,）分隔
    
错误返回结果：
    {"errcode":40029, "errmsg":"invalid code"}

    ```
### 3. 获取用户信息
使用第2步中获取的openId和第1步中获取的token去获取用户信息
```
public static function getUserInfo($openId, $token){
    $url = 'https://api.weixin.qq.com/cgi-bin/user/info?access_token='.$token.'&openid='.$openId.'&lang=zh_CN';
    return Curl::callWebServer($queryUrl, '', 'GET');
}
正确返回结果：
    {
        "subscribe": 1, 
        "openid": "o6_bmjrPTlm6_2sgVt7hMZOPfL2M", 
        "nickname": "Band", 
        "sex": 1, 
        "language": "zh_CN", 
        "city": "广州", 
        "province": "广东", 
        "country": "中国", 
        "headimgurl":"http://thirdwx.qlogo.cn/mmopen/g3MonUZtNHkdmzicIlibx6iaFqAc56vxLSUfpb6n5WKSYVY0ChQKkiaJSgQ1dZuTOgvLLrhJbERQQ4eMsv84eavHiaiceqxibJxCfHe/0",
        "subscribe_time": 1382694957,
        "unionid": " o6_bmasdasdsad6_2sgVt7hMZOPfL"
        "remark": "",
        "groupid": 0,
        "tagid_list":[128,2],
        "subscribe_scene": "ADD_SCENE_QR_CODE",
        "qr_scene": 98765,
        "qr_scene_str": ""
    }
    返回参数说明：
        参数	        说明
        subscribe	   用户是否订阅该公众号标识，值为0时，代表此用户没有关注该公众号，拉取不到其余信息。
        openid	      用户的标识，对当前公众号唯一
        nickname	    用户的昵称
        sex	         用户的性别，值为1时是男性，值为2时是女性，值为0时是未知
        city	        用户所在城市
        country	     用户所在国家
        province	    用户所在省份
        language	    用户的语言，简体中文为zh_CN
        headimgurl	  用户头像，最后一个数值代表正方形头像大小（有0、46、64、96、132数值可选，0代表640*640正方形头像），用户没有头像时该项为空。若用户更换头像，原有头像URL将失效。
        subscribe_time  用户关注时间，为时间戳。如果用户曾多次关注，则取最后关注时间
        unionid	     只有在用户将公众号绑定到微信开放平台帐号后，才会出现该字段。
        remark	      公众号运营者对粉丝的备注，公众号运营者可在微信公众平台用户管理界面对粉丝添加备注
        groupid	     用户所在的分组ID（兼容旧的用户分组接口）
        tagid_list	  用户被打上的标签ID列表
        subscribe_scene 返回用户关注的渠道来源，ADD_SCENE_SEARCH 公众号搜索，ADD_SCENE_ACCOUNT_MIGRATION 公众号迁移，ADD_SCENE_PROFILE_CARD 名片分享，ADD_SCENE_QR_CODE 扫描二维码，ADD_SCENEPROFILE LINK 图文页内名称点击，ADD_SCENE_PROFILE_ITEM 图文页右上角菜单，ADD_SCENE_PAID 支付后关注，ADD_SCENE_OTHERS 其他
        qr_scene	    二维码扫码场景（开发者自定义）
        qr_scene_str	二维码扫码场景描述（开发者自定义）

错误结果：
    {"errcode":40013,"errmsg":"invalid appid"}
```
三、使用
---

判断是否关注过，此处为入口：
```
public function isConcern($appId, $appSecret) {
    $param = ''; // 如果有参数
    $this->getCode($appId, U('callback', 'param='.$param), 1 ,'snsapi_base');
}
```
授权后回调
```
public function callback(){
    $isconcern = 0;
    $code = $this->_get('code');
    $param = $this->_get('param');
    $appId = C('appId'); // config中配置
    $appSecret = C('appSecret');
    $accessTokenInfo = $this->getAccessToken($code, $appId, $appSecret);
    $openId = $accessTokenInfo['openid'];
    $accessToken = $accessTokenInfo['access_token'];
    $token = $this->getToken($appId, $appSecret);
    $userInfo = $this->getUserInfo($openId, $token['access_token']);
    if($userInfo['subscribe'] == 1){
        $this->assign('userInfo', $userInfo);
        $isconcern = 1; // 已关注
    } else {
        $isconcern = 0; // 未关注
    }
    $this->assign('openid', $openId);
    $this->display('page');
}
```

此时页面上可以获取到userInfo和isconcern，isconcern为1时表示已关注公众号，否则未关注。

##### [转自] [如何判断用户是否已关注公众号](https://segmentfault.com/a/1190000015268145)