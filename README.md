# dlink-wdk
Python API for D-Link WDK

Tested on D-Link DIR 100 D1

Python 2.7.x (not 3.x)

Installation
============
```sh
sudo python setup.py install
```

Usage
=====

Log in to device
----------------
```python
import wdk
dev = wdk.Device('192.168.0.1')
dev.Login()
```
Note, login will be automatically be performed if a request fails. Username and password can be specified when instantiating the Device class (default: admin:<blank>). If a login has been previously been performed against that Device, those credentials will be used. 

Dump CDB (Configuration DataBase)
---------------------------------
```python
import wdk
dev = wdk.Device('192.168.0.1')
dev.ExecuteGet('$')
```
Note, this will succeed on versions before B13_fam2 without using login, using $sys_lang-bypass, if the bypass-flag is set when instantiating the class (default False). Furthermore, this will only return the "public" parts of the CDB, some CDB variables are hidden from this view but can be returned when explicitly requested . 

Memory read
-----------
```python
import wdk
dev = wdk.Device('192.168.0.1')
dev.MemRead(0x80000000)
```
Note, this will use the $sys_lang-bypass if the bypass-flag is set. Also, be careful when reading memory, accessing the wrong regions might crash the device. 

Memory write
------------
```python
import wdk
dev = wdk.Device('192.168.0.1')
dev.MemWrite(0x80000000,[0]*8])
```
