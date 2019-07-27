---
title: UnityHub破解
date: 2019-07-27 19:51:39
categories: Unity
tags: [Unity,UnityHub]
---

# 准备
- 安装UnityHub
- 安装nodejs

[点击下载UnityHub](https://public-cdn.cloud.unity3d.com/hub/prod/UnityHubSetup.exe?_ga=2.156672187.1060825894.1557847055-1023445126.1553702403) 

[点击下载nodejs 10.15.3 长期支持版](https://nodejs.org/dist/v10.15.3/node-v10.15.3-x64.msi) 

# 修改
安装nodejs后执行以下命令  
> npm install -g asar

打开UnityHub安装目录，如C:\Program Files\Unity Hub\resources  
点击文件-->打开Windows PowerShell,执行以下命令解压app.asar

> asar extract .\app.asar app

<br/>
解压后删除app.asar

<br/>
<br/>
修改Unity Hub\resources\app\src\services\licenseService\licenseClient.js

```js
getLicenseInfo(callback) {
    // load license
    // get latest data from licenseCore
    //licenseInfo.activated = licenseCore.getLicenseToken().length > 0;//注释这行
    licenseInfo.activated = true;//新增这行
    licenseInfo.flow = licenseCore.getLicenseKind();
    licenseInfo.label = licenseCore.getLicenseKind(true);
    licenseInfo.offlineDisabled = licenseCore.offlineDisabled;
    licenseInfo.transactionId = licenseCore.getTransactionId();
}
```

Unity Hub\resources\app\src\services\licenseService\licenseCore.js

```js
verifyLicenseData(xml, newfile = false) {
    return new Promise((resolve, reject) => {
        resolve(true);//新增这行
        if (xml === '') {
            this.licenseStatus = LICENSE_STATUS.kLicenseErrorFlag_NoLicense;
            reject();
            return;
        }
    }
}
```