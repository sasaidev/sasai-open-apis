# Sasai Open Apis

## What's New (February, 2021)

We have a new release [Sasai 2.9.20](https://www.sasai.global/)!

It comes with lots of bug fixes, optimizations and support for SasaiPay SDKs.

## Introduction

This repository contains examples and best practices for integrating with Sasai, provided as Jupyter notebooks.

- [Sasai Authorisation](#): authorise and obtain user's basic information 
- [SasaiPay](#): process payments using the Sasai Wallet.  

## 1. Authorisation

This is a three step process.

### 1.1 Get Authorisation Code

Add the javascript below on your web page to get the authorisation code

```bash
function authenticateWithSasai() {
    var jsonData = '{"type":"800", "appId": "ownai_client", "scope": "user_info"}';
    window.SasaiCall.openAuth(jsonData);  //for android
    window.webkit.messageHandlers.currentCookies.postMessage(jsonData); // for iOS
}
 
function returnAuth(callbackData) {
    var data = JSON.parse(callbackData);
    alert(data);
}
```

**NOTE** 
- The **appId** and **scope** will be provided. The test values are **"client"** and **"user_info"** respectively.
- The cookie **phoneNumber** contains the Sasai registered phone number.

##### callBackData object structure

```bash
{
    "ret": "0",
    "code": "XYTHSG",
    "scope": "user_info"
}
```
| Field | Description |
| --- | --- |
| ret | "0" = Sucess, "-1" = Failed |
| code | Authorisation code to be used in successive get toke operations |
| scope | Default is **user_info** |

### 1.2 Get Access Token

Use the code returned in the callBackData above, to obtain an access_token

```bash
curl --request POST \
  --url 'http://opentest.im.sasai.mobi/authorize/oauth2/access_token?code=2I73DV&amp;secret=dc1s9dullflmh2et&amp;appId=client'
```

| Field |  |
| --- | --- |
| appId | Will be provided |
| secret | Will be provided |
| code | The code returned from the GET AUTHORISATION CODE step above |

Response

```bash
{
    "code": 200,
    "data": {
        "openid": "10000058024",
        "scope": "user_info",
        "access_token": "TOKEN",
        "expires_in": 7200,
        "refresh_token": "REFRESH_TOKEN"
    },
    "codeMsg": "Success"
} 
```
### 1.3 Get User Information

```bash
{
    "code": 200,
    "data": {
        "userId": 0,
        "userNumber": null,
        "password": null,
        "mobile": null,
        "mobileCode": 0,
        "codeMobile": null,
        "image": 0,
        "qrCode": null,
        "autograph": null,
        "gender": 0,
        "region": null,
        "nickName": null,
        "regApp": 0,
        "email": null,
        "walletStatus": 0,
        "emailState": 0,
        "state": 0,
        "createTime": 0,
        "updateTime": 0
    },
    "codeMsg": "Success"
}
```

#### 1.3.1 Get Authorisation Code

```bash
curl --request POST \
  --url https://opentest.im.sasai.mobi:41880/authorize/oauth2/authorize \
  --header 'content-type: application/json' \
  --header 'h_open_uid: 10000058024' \
  --data '{
    "param": "28JzERz1XbAmXaV1PZ1QZVtdK0DPAO/jtsEjWlC6V5fd4bcL7rxWhXhAE4KZXO4cGgG/H/1CbDpelOM7NLgfQNUswEt8wRJoTK0XMoRhYx/iRuYIjxZ+fzw2YIECLhfsIcv8ZBnppjBBapjq8j9DBnKvpd8dB0CzV1MEKwLeLKE=",
    "sign": "92567293b278a8e5e387250edf692003"
}'
```
| Field |  |
| --- | --- |
| openId | The *openId* from 1.3 above |
| param | AES encrypted concatenated string: scope + responseType + appId + authToken + userId |
| sign | AES encrypted concatenated string: scope + responseType + appId + authToken + userId + securityOffset |
| scope | user_info |
| responseType | code |
| securityOffset | 2605222301669449 |

```bash
{
  "code": 200,
  "data": {
    "code": "ECB8YE",
    "state": null
  },
  "codeMsg": "Success"
}
```
