# DESC

This project implements the [Shadowsocks](https://github.com/shadowsocks/shadowsocks) protocol using python3.5 and asyncio library
 since the original project source code is unreadble and frustrated to extend.

Shadowsocks is a proxy program, that the client is listening socks5 protocol on local(socks5 connect/UDP association), 
forward encrypt socks5 data to remote proxy, and then the proxy forward the socket data to target host. It hides the SOCKS5
 handshakes and traffic bytes from censor.

Shadowsocks is mainly used for bypassing Great Firewall of China, since the data is encrypt and sent over 
normal TCP/UDP, no handshake, no fingerprint, getting away from packet inspection, it's hard to block.

# FEATURE
* shadowsocks protocol implements TCP proxy without OTA feature, no UDP
* sock5ssl implements only SOCKS CONNECT, no BIND/UDP ASSOCIATE


# USAGE

## INSTALLATION
### For Ubuntu 14.04

```
$ sudo apt-get install openssl
$ sudo pip3 install -e git+https://github.com/FTwO-O/pyShadowsocks.git@master#egg=pyshadowsocks
```

### For Mac OS
Mac OS has a deprecated openssl and does not includes the header files, so you need to install openssl library manually.

* build openssl manually using the [script](https://github.com/FTwO-O/Build_Mac_Command_Line_Tools/blob/master/openssl.sh) 

```
$ sudo pip3 install -e git+https://github.com/FTwO-O/pyShadowsocks.git@master#egg=pyshadowsocks
```
    
* Use brew to install openssl

```
$ brew install openssl
$ sudo pip3 install -e git+https://github.com/FTwO-O/pyShadowsocks.git@master#egg=pyshadowsocks
```

### START THE SERVICE

* proxy server

    1. shadowsocks

    ```
    ss shadowsocks --cipher_method aes-256-cfb --password 123456 remote --listen_port 8099 &
    ```
    
    2. socks5ssl
    
    ```
    ss socks5ssl --user user --password 123456 remote --listen_port 9000
    ```
    
* local socks5 server:
    1. shadowsocks
    ```
    ss shadowsocks --cipher_method aes-256-cfb --password 123456 local --remote_host 110.110.110.110 --remote_port 8099 &
    ```
    2. socks5ssl
    ```
    ss socks5ssl --user user --password 123456 local --remote_host 10.110.110.110 --remote_port 9000 --socks_port 10012 &
    ```
   
## Mac Client
* Download [GoAgentX for Mac](https://goagentx.googlecode.com/files/GoAgentX-v2.2.9.dmg).

* Add a shell service config (to start local socks server) and then click the ON button
![GoAgentX setting for pyShadowsocks](screenshots/goagentx_shell_service_config.png)

        
# TODO

1. ~~SOCKS5 user/password authentication~~
2. ~~SOCKS5 over SSL~~
3. ~~Remove the cryptography library, use openssl with ctypes.~~
4. Use Apple's cryto library for Mac OS X instead of openssl
5. Filtering connections to local ip for security consideration
6. Flow control
7. Custom protocol, carry TCP/UPD/HTTP traffic
8. Multi threading/process for multiple user/port