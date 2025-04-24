# Overview

- Manufacturer's website information：https://www.netgear.com/
- Firmware download address ：https://kb.netgear.com/23510/DGND3700v2-Firmware-Version-1-1-00-15-NA-Users

# Affected version

DGND3700v2 V1.1.00.15_1.00.15NA

# Vulnerability description

An information disclosure vulnerability exists in NETGEAR DGND3700v2 firmware V1.1.00.15_1.00.15NA, where the /BRS_top.html page is accessible without authentication. This allows unauthenticated users obtain sensitive device information such as the router model and firmware version.

# Poc

http://192.168.1.1/BRS_top.html

![图 0](img/839713471f9fa66436228a5d595a0bd972a948166068004f84ce75ef42786c5b.png)  

![图 1](img/69344aa43cbd1b8ea790dae7ef538b025c1e0eab81415d1de944db21762981c4.png)  
