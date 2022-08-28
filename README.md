## Fail2Ban 简单修复了在Python3及其以上无法使用的错误,编译安装即可.(这问题出现很久,官方都没修,比较不爽.本人Python版本3.10.6)
__      _ _ ___ _               
                        / _|__ _(_) |_  ) |__  __ _ _ _  
                       |  _/ _` | | |/ /| '_ \/ _` | ' \ 
                       |_| \__,_|_|_/___|_.__/\__,_|_||_|
                       v1.0.1.dev1            20??/??/??

## Fail2Ban: 禁止造成多次认证错误的主机

Fail2Ban扫描日志文件，如`/var/log/auth.log`，并禁止IP地址进行过多的失败登录尝试。它通过更新系统防火墙规则，拒绝来自这些IP地址的新连接，并在可配置的时间内完成这一工作。Fail2Ban开箱即用，可以读取许多标准的日志文件，如sshd和Apache的日志文件，也可以轻松配置为读取你选择的任何日志文件，以处理你希望的任何错误。
尽管Fail2Ban能够降低错误的认证尝试率，但它不能消除弱认证带来的风险。
如果你真的想保护服务，请将服务设置为只使用双因素，或公共/私人认证机制。
     
<img src="http://www.worldipv6launch.org/wp-content/themes/ipv6/downloads/World_IPv6_launch_logo.svg" height="52pt"/> | 从v0.10开始，fail2ban支持IPv6地址的匹配。
------|------

此README是对Fail2Ban的快速介绍。更多的文档、FAQ和HOWTOs
可在 fail2ban(1) manpage, [Wiki](https://github.com/fail2ban/fail2ban/wiki) 找到。
[开发人员文档](https://fail2ban.readthedocs.io/)
和网站：https://www.fail2ban.org

安装:
-------------

**有可能Fail2Ban已经为你的发行版打包了。 在这种情况下 这种情况下，你应该用它来代替。**

Required:
- [Python2 >= 2.7 or Python >= 3.2](https://www.python.org) or [PyPy](https://pypy.org)
- python-setuptools, python-distutils or python3-setuptools for installation from source

Optional:
- [pyinotify >= 0.8.3](https://github.com/seb-m/pyinotify), may require:
  * Linux >= 2.6.13
- [gamin >= 0.0.21](http://www.gnome.org/~veillard/gamin)
- [systemd >= 204](http://www.freedesktop.org/wiki/Software/systemd) and python bindings:
  * [python-systemd package](https://www.freedesktop.org/software/systemd/python-systemd/index.html)
- [dnspython](http://www.dnspython.org/)


To install:

    tar xvfj fail2ban-1.0.1.tar.bz2
    cd fail2ban-1.0.1
    sudo python setup.py install
   
Alternatively, you can clone the source from GitHub to a directory of Your choice, and do the install from there. Pick the correct branch, for example, master or 0.11

    git clone https://github.com/fail2ban/fail2ban.git
    cd fail2ban
    sudo python setup.py install 
    
This will install Fail2Ban into the python library directory. The executable
scripts are placed into `/usr/bin`, and configuration in `/etc/fail2ban`.

Fail2Ban should be correctly installed now. Just type:

    fail2ban-client -h

to see if everything is alright. You should always use fail2ban-client and
never call fail2ban-server directly.
You can verify that you have the correct version installed with 

    fail2ban-client version

Please note that the system init/service script is not automatically installed.
To enable fail2ban as an automatic service, simply copy the script for your
distro from the `files` directory to `/etc/init.d`. Example (on a Debian-based
system):

    cp files/debian-initd /etc/init.d/fail2ban
    update-rc.d fail2ban defaults
    service fail2ban start

Configuration:
--------------

You can configure Fail2Ban using the files in `/etc/fail2ban`. It is possible to
configure the server using commands sent to it by `fail2ban-client`. The
available commands are described in the fail2ban-client(1) manpage.  Also see
fail2ban(1) and jail.conf(5)  manpages for further references.

Code status:
------------

* travis-ci.org: [![tests status](https://secure.travis-ci.org/fail2ban/fail2ban.svg?branch=master)](https://travis-ci.org/fail2ban/fail2ban?branch=master) / [![tests status](https://secure.travis-ci.org/fail2ban/fail2ban.svg?branch=0.11)](https://travis-ci.org/fail2ban/fail2ban?branch=0.11) (0.11 branch) / [![tests status](https://secure.travis-ci.org/fail2ban/fail2ban.svg?branch=0.10)](https://travis-ci.org/fail2ban/fail2ban?branch=0.10) (0.10 branch) 

* coveralls.io: [![Coverage Status](https://coveralls.io/repos/fail2ban/fail2ban/badge.svg?branch=master)](https://coveralls.io/github/fail2ban/fail2ban?branch=master) / [![Coverage Status](https://coveralls.io/repos/fail2ban/fail2ban/badge.svg?branch=0.11)](https://coveralls.io/github/fail2ban/fail2ban?branch=0.11) (0.11 branch) / [![Coverage Status](https://coveralls.io/repos/fail2ban/fail2ban/badge.svg?branch=0.10)](https://coveralls.io/github/fail2ban/fail2ban?branch=0.10) / (0.10 branch)

* codecov.io: [![codecov.io](https://codecov.io/gh/fail2ban/fail2ban/coverage.svg?branch=master)](https://codecov.io/gh/fail2ban/fail2ban/branch/master) / [![codecov.io](https://codecov.io/gh/fail2ban/fail2ban/coverage.svg?branch=0.11)](https://codecov.io/gh/fail2ban/fail2ban/branch/0.11) (0.11 branch) / [![codecov.io](https://codecov.io/gh/fail2ban/fail2ban/coverage.svg?branch=0.10)](https://codecov.io/gh/fail2ban/fail2ban/branch/0.10) (0.10 branch)

Contact:
--------

### Bugs, feature requests, discussions?
See [CONTRIBUTING.md](https://github.com/fail2ban/fail2ban/blob/master/CONTRIBUTING.md)

### You just appreciate this program:
Send kudos to the original author ([Cyril Jaquier](mailto:cyril.jaquier@fail2ban.org))
or *better* to the [mailing list](https://lists.sourceforge.net/lists/listinfo/fail2ban-users)
since Fail2Ban is "community-driven" for years now.

Thanks:
-------

See [THANKS](https://github.com/fail2ban/fail2ban/blob/master/THANKS) file.

License:
--------

Fail2Ban is free software; you can redistribute it and/or modify it under the
terms of the GNU General Public License as published by the Free Software
Foundation; either version 2 of the License, or (at your option) any later
version.

Fail2Ban is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
Fail2Ban; if not, write to the Free Software Foundation, Inc., 51 Franklin
Street, Fifth Floor, Boston, MA 02110, USA
