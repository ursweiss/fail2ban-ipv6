This repository contains files and patches to make fail2ban work with IPv6 on RHEL/CentOS 6(.5). It's not perfect, but works fine for me.

It only supports iptables (or better, i haven't tested anything else. It may works...).
You can adjust any other existing iptables config by simply replacing "iptables" with "/usr/local/sbin/iptables-wrapper" (Had to use the full path to make it work).

It was made for fail2ban version 0.8.11-2 which is available as part of the EPEL repository for RHEL/CentOS 6.
If you use this version on RHEL/CentOS 6, you simply can replace the files (see below). If you use another 0.8 version, the patches may work, or at least help you what to change.

### How to install:

1. Install fail2ban as usual

  \# yum install fail2ban

2. Copy files:

  cp filter.py /usr/share/fail2ban/server/
  
  cp failregex.py /usr/share/fail2ban/server/
  
  cp iptables-46-multiport-log.conf /etc/fail2ban/actions.d/
  
  cp iptables-wrapper /usr/local/sbin/
  
  chmod 750 /usr/local/sbin/iptables-wrapper

3. Edit jail.conf:

  Adjust the ignoreip option:

  ignoreip = 127.0.0.1/8 ::1/128

  Use "iptables-46-multiport-log" as action


Done. Happy banning.


### Credits:
These files are a mix of two sources and some hours of my own work.
- Pull request of Rainier Schoof: https://github.com/fail2ban/fail2ban/pull/469
- Files of Thanatos: http://thanatos.trollprod.org/sousites/fail2banv6/fail2ban-ipv6.tar.bz2
