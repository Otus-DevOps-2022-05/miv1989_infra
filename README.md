# miv1989_infra
miv1989 Infra repository


HW#3
Адреса ВМ: 
bastion_IP = 51.250.77.64
someinternalhost_IP = 10.128.0.24

!SSH Forwarding на локальной машине"

PS C:\Users\Маруська> Set-Service ssh-agent -StartupType Manual
PS C:\Users\Маруська> Start-Service ssh-agent
PS C:\Users\Маруська> Get-Service ssh-agent

Status   Name               DisplayName
------   ----               -----------
Running  ssh-agent          OpenSSH Authentication Agent

ssh-add "C:\Users\Маруська\.ssh\id_rsa"

PS C:\Users\Маруська> ssh-add "C:\Users\쪠\.ssh\id_rsa"
Identity added: C:\Users\Маруська\.ssh\id_rsa (Маруська@LAPTOP-BP3BJ2H8)

PS C:\Users\Маруська> ssh -A appuser@51.250.77.64
Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-121-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
New release '22.04.1 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

Last login: Sat Aug 13 05:45:17 2022 from 5.165.16.59
appuser@bastion:~$ ssh 10.128.0.24
Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-121-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

appuser@someinternalhost:~$ hostname
someinternalhost

appuser@someinternalhost:~$ ip a show eth0
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether d0:0d:14:b2:f7:2e brd ff:ff:ff:ff:ff:ff
    inet 10.128.0.24/24 brd 10.128.0.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::d20d:14ff:feb2:f72e/64 scope link
       valid_lft forever preferred_lft forever

appuser@bastion:~$ ls -la ~/.ssh/
total 16
drwx------ 2 appuser appuser 4096 Jul 17 06:02 .
drwxr-xr-x 4 appuser appuser 4096 Jul 17 06:04 ..
-rw------- 1 appuser appuser  414 Jul  3 06:00 authorized_keys
-rw-r--r-- 1 appuser appuser  222 Jul 17 06:02 known_hosts

!Самостоятельное задание. В одну комманду!

PS C:\Users\Маруська> ssh -J appuser@51.250.77.64 appuser@10.128.0.24

Подключение через бастион-хост с использованием алиаса
Создать (отредактировать) файл ~/.ssh/config в котором указать следующее:

Host someinternalhost
  Hostname 10.128.0.24
  User appuser
  ForwardAgent yes
  ProxyJump appuser@51.250.77.64

