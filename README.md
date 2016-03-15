About:

sSocks是一个跨平台的socks代理工具套装，可用来开启socks代理服务，支持socks5验证，支持IPV6和UDP，并提供反向socks代理服务

*nsocks* 类似通过Socks5代理后的netcat，可用来测试socks server

*ssocksd* 用来开启Socks5代理服务

*ssocks* 本地启用Socks5服务，并反弹到另一IP地址

*rcsocks* 接收反弹过来的Socks5服务，并转向另一端口

原项目地址：[sSocks](https://github.com/tostercx/ssocks)

Visual Studio 暂时不支持c99标准，所以无法直接编译从gcc移植过来的代码。

笔者修改了源码，让其在vs下编译通过。

How to use？
```console
nmake -f Makefile.nmake
```

------------------------------------------------------------------------

Original README:

------------------------------------------------------------------------
Features:
  - Configuration file
  - Authentication file
  - Generate a connection log file
  - Daemon mode
  - Server support bind mode
  - Socks4 support (if authentication is enable socks4 is disable)
  - Support choose of interface to bind

------------------------------------------------------------------------
TODO:
  - IPV6 support
  - UDP support
  - Stock password with a hash ( md5 or sha256 )
  - GSSAPI auth support ( maybe )
  - Set number of client max ( actually 255 is in client.h MAXCLI var )
  - Add --pid-file option to server 
  - ssocks bind localhost, not all
  - SSL implements out of RFC

------------------------------------------------------------------------
Software:
  - nsocks is a netcat like through a socks5 (usefull to test socks server)
  - ssocksd is the socks5 server
  - ssocks is a socks5 relay, it run a socks server on your localhost interface,
 and relay all data to the server specified in parameter (works but under dev)
  - rssocks is a reverse socks5 server ( POC under dev )
  - rcsocks is a reverse socks5 client ( POC under dev )

File:
  - /etc/ssocksd.conf is server configuration file
  - /etc/ssocksd.auth is password file
  - /var/log/ssocksd.log is default log (specified in configuration file)
  - /var/run/ssocksd.pid is create in daemon mode and delete
 when it receive SIGTERM

-----------------------------------------------------------------------

 How to use rssocks and rcsocks in pentest mode
 http://www.vimeo.com/22515255

------------------------------------------------------------------------
More information see man page:

ssocksd (1), nsocks (1), ssocks (1), ssocksd.auth (5), ssocksd.conf (5)
rssocks (1), rcsocks (1)

------------------------------------------------------------------------
Ubuntu/debian install:

  dpkg -i ssocks_0.0.*-*_i386.deb

Warning: This package install the server with init script and start it
with no authentication in the config file, so everybody can connect on.

------------------------------------------------------------------------
Gentoo install:

I've a ebuild with init script contact me if you want it

------------------------------------------------------------------------
From source:

  ./configure && make

Warning: don't content init script

------------------------------------------------------------------------
Warning, if you import from git, you need to do:

  $ ./bootstrap.sh
 
PS for me: To avoid to wait when you debug the server and some 
socket don't close properly

  # echo 1 > /proc/sys/net/ipv4/tcp_tw_recycle
  
To compile with dynamic lib

  $ ./configure --disble-static
  
To enable SSL

  $ ./configure with-ssl
 
Just for remember (this by default actually)

  $ ./configure --enable-static --disable-shared
 
PS: for test and debug authentication

  $ curl -U admin:abcde --socks5 127.0.0.1:1080 www.perdu.com

------------------------------------------------------------------------
Copyright (C) 2011 by Hugo Caron

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
 THE SOFTWARE.

------------------------------------------------------------------------
