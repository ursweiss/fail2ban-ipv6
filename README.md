# !!! IMPORTANT !!!
1. This will not work anymore with any 0.9x version of fail2ban
2. The current 0.10 branch seems to work pretty fine as it will support IPv6 out of the box and is much cleaner than my hack. No RPM available of course, but very easy to install following their instructions: https://github.com/fail2ban/fail2ban/tree/0.10
3. Have a look at their "IPv6 support master plan" too: https://github.com/fail2ban/fail2ban/issues/1123


-----

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
  cp iptables-46-multiport-log.conf /etc/fail2ban/action.d/  
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
