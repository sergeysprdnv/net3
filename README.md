# Домашнее задание к занятию "`Обзор систем IT-мониторинга`" - `Спиридонов Сергей`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1
┌──(root㉿kali)-[/home/kali]
└─# nmap -sA 192.168.0.183
Starting Nmap 7.94 ( https://nmap.org ) at 2023-11-28 03:20 EST
Nmap scan report for user-VirtualBox.Dlink (192.168.0.183)
Host is up (0.00044s latency).
All 1000 scanned ports on user-VirtualBox.Dlink (192.168.0.183) are in ignored states.
Not shown: 1000 unfiltered tcp ports (reset)
MAC Address: 08:00:27:1A:EF:56 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 0.24 seconds

┌──(root㉿kali)-[/home/kali]
└─# nmap -sT 192.168.0.183
Starting Nmap 7.94 ( https://nmap.org ) at 2023-11-28 03:20 EST
Nmap scan report for user-VirtualBox.Dlink (192.168.0.183)
Host is up (0.00078s latency).
Not shown: 999 closed tcp ports (conn-refused)
PORT   STATE SERVICE
22/tcp open  ssh
MAC Address: 08:00:27:1A:EF:56 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 0.30 seconds

┌──(root㉿kali)-[/home/kali]
└─# nmap -sS 192.168.0.183
Starting Nmap 7.94 ( https://nmap.org ) at 2023-11-28 03:20 EST
Nmap scan report for user-VirtualBox.Dlink (192.168.0.183)
Host is up (0.00021s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
MAC Address: 08:00:27:1A:EF:56 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 0.36 seconds

┌──(root㉿kali)-[/home/kali]
└─# nmap -sV 192.168.0.183
Starting Nmap 7.94 ( https://nmap.org ) at 2023-11-28 03:20 EST
Nmap scan report for user-VirtualBox.Dlink (192.168.0.183)
Host is up (0.00042s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.9 (Ubuntu Linux; protocol 2.0)
MAC Address: 08:00:27:1A:EF:56 (Oracle VirtualBox virtual NIC)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.62 seconds

nmap просканировал tcp порты и нашел открытый порт 22 (SSH)
root@user-VirtualBox:/home/user# tail -f /var/log/suricata/fast.log
^C
root@user-VirtualBox:/home/user#




### Заданиe 2
┌──(root㉿kali)-[/home/kali]
└─# hydra -L users.txt -P pass.txt 192.168.0.183 ssh
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-11-28 03:09:02
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 16 login tries (l:4/p:4), ~1 try per task
[DATA] attacking ssh://192.168.0.183:22/
[22][ssh] host: 192.168.0.183   login: user   password: 1111
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 2 final worker threads did not complete until end.
[ERROR] 2 targets did not resolve or could not be connected
[ERROR] 0 target did not complete
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2023-11-28 03:09:06


root@user-VirtualBox:/home/user# tail /var/log/auth.log
Nov 28 11:09:05 user-VirtualBox sshd[2032]: Failed password for invalid user admin from 192.168.0.168 port 35142 ssh2
Nov 28 11:09:05 user-VirtualBox sshd[2030]: Failed password for invalid user admin from 192.168.0.168 port 35134 ssh2
Nov 28 11:09:05 user-VirtualBox sshd[2043]: Failed password for root from 192.168.0.168 port 35238 ssh2
Nov 28 11:09:05 user-VirtualBox sshd[2041]: Failed password for root from 192.168.0.168 port 35226 ssh2
Nov 28 11:09:05 user-VirtualBox sshd[2039]: Failed password for user from 192.168.0.168 port 35198 ssh2
Nov 28 11:09:05 user-VirtualBox sshd[2042]: Failed password for root from 192.168.0.168 port 35232 ssh2
Nov 28 11:09:05 user-VirtualBox sshd[2038]: Failed password for user from 192.168.0.168 port 35182 ssh2
Nov 28 11:09:13 user-VirtualBox sudo:     root : TTY=pts/1 ; PWD=/home/user ; USER=root ; COMMAND=/usr/bin/tail -f /var/log/suricata/fast.log
Nov 28 11:09:13 user-VirtualBox sudo: pam_unix(sudo:session): session opened for user root by user(uid=0)
Nov 28 11:09:15 user-VirtualBox sudo: pam_unix(sudo:session): session closed for user root

root@user-VirtualBox:/home/user# cat /var/log/fail2ban.log
2023-11-28 09:21:38,909 fail2ban.server         [4248]: INFO    --------------------------------------------------
2023-11-28 09:21:38,913 fail2ban.server         [4248]: INFO    Starting Fail2ban v0.11.1
2023-11-28 09:21:38,913 fail2ban.observer       [4248]: INFO    Observer start...
2023-11-28 09:21:38,921 fail2ban.database       [4248]: INFO    Connected to fail2ban persistent database '/var/lib/fail2ban/fail2ban.sqlite3'
2023-11-28 09:21:38,923 fail2ban.database       [4248]: WARNING New database created. Version '4'
2023-11-28 09:21:38,923 fail2ban.jail           [4248]: INFO    Creating new jail 'sshd'
2023-11-28 09:21:38,985 fail2ban.jail           [4248]: INFO    Jail 'sshd' uses pyinotify {}
2023-11-28 09:21:39,003 fail2ban.jail           [4248]: INFO    Initiated 'pyinotify' backend
2023-11-28 09:21:39,009 fail2ban.filter         [4248]: INFO      maxLines: 1
2023-11-28 09:21:39,108 fail2ban.filter         [4248]: INFO      maxRetry: 5
2023-11-28 09:21:39,109 fail2ban.filter         [4248]: INFO      findtime: 600
2023-11-28 09:21:39,109 fail2ban.actions        [4248]: INFO      banTime: 600
2023-11-28 09:21:39,109 fail2ban.filter         [4248]: INFO      encoding: UTF-8
2023-11-28 09:21:39,109 fail2ban.filter         [4248]: INFO    Added logfile: '/var/log/auth.log' (pos = 0, hash = 3ade58f1d0f0a1ec29cb14b5c35942572a75a318)
2023-11-28 09:21:39,211 fail2ban.jail           [4248]: INFO    Jail 'sshd' started
2023-11-28 09:26:50,852 fail2ban.server         [600]: INFO    --------------------------------------------------
2023-11-28 09:26:50,852 fail2ban.server         [600]: INFO    Starting Fail2ban v0.11.1
2023-11-28 09:26:50,853 fail2ban.observer       [600]: INFO    Observer start...
2023-11-28 09:26:50,876 fail2ban.database       [600]: INFO    Connected to fail2ban persistent database '/var/lib/fail2ban/fail2ban.sqlite3'
2023-11-28 09:26:50,880 fail2ban.jail           [600]: INFO    Creating new jail 'sshd'
2023-11-28 09:26:50,954 fail2ban.jail           [600]: INFO    Jail 'sshd' uses pyinotify {}
2023-11-28 09:26:50,986 fail2ban.jail           [600]: INFO    Initiated 'pyinotify' backend
2023-11-28 09:26:50,997 fail2ban.filter         [600]: INFO      maxLines: 1
2023-11-28 09:26:51,139 fail2ban.filter         [600]: INFO      maxRetry: 5
2023-11-28 09:26:51,139 fail2ban.filter         [600]: INFO      findtime: 600
2023-11-28 09:26:51,140 fail2ban.actions        [600]: INFO      banTime: 600
2023-11-28 09:26:51,140 fail2ban.filter         [600]: INFO      encoding: UTF-8
2023-11-28 09:26:51,146 fail2ban.filter         [600]: INFO    Added logfile: '/var/log/auth.log' (pos = 2820, hash = 3ade58f1d0f0a1ec29cb14b5c35942572a75a318)
2023-11-28 09:26:51,173 fail2ban.jail           [600]: INFO    Jail 'sshd' started
2023-11-28 09:35:48,301 fail2ban.server         [592]: INFO    --------------------------------------------------
2023-11-28 09:35:48,305 fail2ban.server         [592]: INFO    Starting Fail2ban v0.11.1
2023-11-28 09:35:48,306 fail2ban.observer       [592]: INFO    Observer start...
2023-11-28 09:35:48,333 fail2ban.database       [592]: INFO    Connected to fail2ban persistent database '/var/lib/fail2ban/fail2ban.sqlite3'
2023-11-28 09:35:48,338 fail2ban.jail           [592]: INFO    Creating new jail 'sshd'
2023-11-28 09:35:48,458 fail2ban.jail           [592]: INFO    Jail 'sshd' uses pyinotify {}
2023-11-28 09:35:48,506 fail2ban.jail           [592]: INFO    Initiated 'pyinotify' backend
2023-11-28 09:35:48,522 fail2ban.filter         [592]: INFO      maxLines: 1
2023-11-28 09:35:48,709 fail2ban.filter         [592]: INFO      maxRetry: 5
2023-11-28 09:35:48,710 fail2ban.filter         [592]: INFO      findtime: 600
2023-11-28 09:35:48,710 fail2ban.actions        [592]: INFO      banTime: 600
2023-11-28 09:35:48,710 fail2ban.filter         [592]: INFO      encoding: UTF-8
2023-11-28 09:35:48,719 fail2ban.filter         [592]: INFO    Added logfile: '/var/log/auth.log' (pos = 10040, hash = 3ade58f1d0f0a1ec29cb14b5c35942572a75a318)
2023-11-28 09:35:48,770 fail2ban.jail           [592]: INFO    Jail 'sshd' started
2023-11-28 09:42:19,394 fail2ban.server         [605]: INFO    --------------------------------------------------
2023-11-28 09:42:19,397 fail2ban.server         [605]: INFO    Starting Fail2ban v0.11.1
2023-11-28 09:42:19,398 fail2ban.observer       [605]: INFO    Observer start...
2023-11-28 09:42:19,418 fail2ban.database       [605]: INFO    Connected to fail2ban persistent database '/var/lib/fail2ban/fail2ban.sqlite3'
2023-11-28 09:42:19,424 fail2ban.jail           [605]: INFO    Creating new jail 'sshd'
2023-11-28 09:42:19,501 fail2ban.jail           [605]: INFO    Jail 'sshd' uses pyinotify {}
2023-11-28 09:42:19,523 fail2ban.jail           [605]: INFO    Initiated 'pyinotify' backend
2023-11-28 09:42:19,536 fail2ban.filter         [605]: INFO      maxLines: 1
2023-11-28 09:42:19,657 fail2ban.filter         [605]: INFO      maxRetry: 5
2023-11-28 09:42:19,658 fail2ban.filter         [605]: INFO      findtime: 600
2023-11-28 09:42:19,658 fail2ban.actions        [605]: INFO      banTime: 600
2023-11-28 09:42:19,659 fail2ban.filter         [605]: INFO      encoding: UTF-8
2023-11-28 09:42:19,661 fail2ban.filter         [605]: INFO    Added logfile: '/var/log/auth.log' (pos = 13610, hash = 3ade58f1d0f0a1ec29cb14b5c35942572a75a318)
2023-11-28 09:42:19,678 fail2ban.jail           [605]: INFO    Jail 'sshd' started
2023-11-28 09:43:42,742 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.120 - 2023-11-28 09:43:42
2023-11-28 10:26:46,484 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:46
2023-11-28 10:26:46,909 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:46
2023-11-28 10:26:46,914 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:46
2023-11-28 10:26:46,919 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:46
2023-11-28 10:26:46,961 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:46
2023-11-28 10:26:47,311 fail2ban.actions        [605]: NOTICE  [sshd] Ban 192.168.0.168
2023-11-28 10:26:49,206 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,216 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,352 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,355 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,358 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,359 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,360 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,368 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,372 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,376 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,380 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,395 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,403 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,404 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 10:26:49
2023-11-28 10:26:49,414 fail2ban.actions        [605]: NOTICE  [sshd] 192.168.0.168 already banned
2023-11-28 10:26:49,414 fail2ban.actions        [605]: NOTICE  [sshd] 192.168.0.168 already banned
2023-11-28 10:31:33,562 fail2ban.server         [605]: INFO    --------------------------------------------------
2023-11-28 10:31:33,567 fail2ban.server         [605]: INFO    Starting Fail2ban v0.11.1
2023-11-28 10:31:33,567 fail2ban.observer       [605]: INFO    Observer start...
2023-11-28 10:31:33,619 fail2ban.database       [605]: INFO    Connected to fail2ban persistent database '/var/lib/fail2ban/fail2ban.sqlite3'
2023-11-28 10:31:33,622 fail2ban.jail           [605]: INFO    Creating new jail 'sshd'
2023-11-28 10:31:33,792 fail2ban.jail           [605]: INFO    Jail 'sshd' uses pyinotify {}
2023-11-28 10:31:33,847 fail2ban.jail           [605]: INFO    Initiated 'pyinotify' backend
2023-11-28 10:31:33,866 fail2ban.filter         [605]: INFO      maxLines: 1
2023-11-28 10:31:34,017 fail2ban.filter         [605]: INFO      maxRetry: 5
2023-11-28 10:31:34,036 fail2ban.filter         [605]: INFO      findtime: 600
2023-11-28 10:31:34,038 fail2ban.actions        [605]: INFO      banTime: 600
2023-11-28 10:31:34,041 fail2ban.filter         [605]: INFO      encoding: UTF-8
2023-11-28 10:31:34,049 fail2ban.filter         [605]: INFO    Added logfile: '/var/log/auth.log' (pos = 28617, hash = 3ade58f1d0f0a1ec29cb14b5c35942572a75a318)
2023-11-28 10:31:34,136 fail2ban.jail           [605]: INFO    Jail 'sshd' started
2023-11-28 10:31:34,259 fail2ban.actions        [605]: NOTICE  [sshd] Restore Ban 192.168.0.168
2023-11-28 10:32:58,022 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.120 - 2023-11-28 10:32:58
2023-11-28 10:33:01,276 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.120 - 2023-11-28 10:33:01
2023-11-28 10:36:47,572 fail2ban.actions        [605]: NOTICE  [sshd] Unban 192.168.0.168
2023-11-28 11:09:03,227 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:02
2023-11-28 11:09:03,436 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:03
2023-11-28 11:09:03,448 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:03
2023-11-28 11:09:03,450 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:03
2023-11-28 11:09:03,459 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:03
2023-11-28 11:09:03,493 fail2ban.actions        [605]: NOTICE  [sshd] Ban 192.168.0.168
2023-11-28 11:09:05,517 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,520 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,525 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,527 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,530 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,530 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,531 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,532 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,549 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,555 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,556 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,561 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05
2023-11-28 11:09:05,561 fail2ban.filter         [605]: INFO    [sshd] Found 192.168.0.168 - 2023-11-28 11:09:05


После включения защиты SSH
┌──(root㉿kali)-[/home/kali]
└─# hydra -L users.txt -P pass.txt 192.168.0.183 ssh
Hydra v9.5 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2023-11-28 03:10:20
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 16 login tries (l:4/p:4), ~1 try per task
[DATA] attacking ssh://192.168.0.183:22/
[ERROR] could not connect to ssh://192.168.0.183:22 - Connection refused
