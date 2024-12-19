# Born2BeRoot



>1 set up / add partitions

>2 sudo / user / group

>3 ssh

>4 git / vim

>5 conncting via ssh

>6 enable ufw firewall / allow firewall

>7 sudo policies

>8 password policies

>9 SCRIPTS :

  
  >> uname -m : show the architecture of the os

  
  >> cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l ///// show the number of physical processors

  
  >> cat /proc/cpuinfo | grep "^processor" | wc -l ///// show the number of virtual processors

  
  >> free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2, ($3/$2)*100)}' ///// (free -m) : dispaly ram in mb || (awk) : mem / $2 ram / $3 used ram

  
  >> df -h --total | awk '/total/ {printf("#Disk Usage: %s/%s (%s)\n", $3, $2, $5)}'

  
  >> df -h --total | awk '/total/ {printf("#Disk Usage: %s/%s (%s)\n", $3, $2, $5)}' ///// df -h : diplay used stockage ||| -total : total storage || awk : grep ||||| display storage use in percentage


  >> vmstat 1 4 | tail -1 | awk '{print "cpu usage " $15 "%"}' ///// display used cpu


  >> who -b | awk '{print "Last boot : " $3 " " $4}' ///// display last reboot timestamp


  >> if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi //// if lvm available or not
  

  >> ss -ta | grep ESTAB | wc -l    /// wc -l only the number /// ss -ta display established connections
  

  >> users | wc -w // list users in the server and list only the number
  

  >> ip link | grep link/ether | awk '{print $2}' ///// list ipv4 mac address
  

  >>  journalctl _COMM=sudo | grep COMMAND | wc -l //// list how many command executed by sudo
  

  _________________________________________________________________________________________________________________________________________________________



    wall "	Architecture: $arch
    
    CPU physical: $cpuf
    
    vCPU: $cpuv
    
    Memory Usage: $ram_use/${ram_total}MB ($ram_percent%)
    
    Disk Usage: $disk_use/${disk_total} ($disk_percent%)
    
    CPU load: $cpu_fin%
    
    Last boot: $lb
    
    LVM use: $lvmu
    
    Connections TCP: $tcpc ESTABLISHED
    
    User log: $ulog
    
    Network: IP $ip ($mac)
    
    Sudo: $cmnd cmd"



________________________________________________________________________________________________________________________________________________________________




Last login: Thu Dec 19 10:09:56 on ttys000
 42 wizzard is up to date
➜  ~ ssh riel-fas@127.0.0.1 -p 4242
riel-fas@127.0.0.1's password:
Permission denied, please try again.
riel-fas@127.0.0.1's password:
Linux riel-fas42 6.1.0-28-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.119-1 (2024-11-22) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Thu Dec 19 03:59:14 2024

Broadcast message from root@riel-fas42 (somewhere) (Thu Dec 19 04:50:05 2024):

 Archotecture: x86_64
     CPU physical: 0
     vCPU: 0
     Memory Usage: #Memory Usage: 226/960MB (
     Disk Usage: Disk Usage: 1.6G/29G (6%)
     CPU load: cpu usage100%%
     Last boot: Last boot2024-12-19 03:59
     LVM use: no
     Connections TCP:  ESTABLISHED
     User log: 0
#! /bin/bash

#Arch
arch=$(uname -m)


#CPU Phy
cpuf=$(cat/proc/cpuinfo | grep "physical id" | sort -u | wc -l)


#CPU Vir
cpuv=$(cat/proc/cpuinfo | grep "processor" | wc -l)


#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')


#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')


#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')


#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [$(lsblk | grep "lvm" | wc -l) -gt 0]; then echo yes; else echo no; fi)


#User log
ulog=$(ss -ta | grap ESTAB | wc -l)


#Network
ip=$(users | wc -w)


#sudo
cmnd=$(journalctl_COMM=sudo | grep COMMAND | wc -l)




"monitoring.sh" 63L, 1060B                                                                                                                                                                                1,1           Top
#! /bin/bash

#Arch
arch=$(uname -m)


#CPU Phy
cpuf=$(cat/proc/cpuinfo | grep "physical id" | sort -u | wc -l)


#CPU Vir
cpuv=$(cat/proc/cpuinfo | grep "processor" | wc -l)


     Network: IP 2
#! /bin/bash

#Arch
arch=$(uname -m)


#CPU Phy
cpuf=$(cat/proc/cpuinfo | grep "physical id" | sort -u | wc -l)


#CPU Vir
cpuv=$(cat/proc/cpuinfo | grep "processor" | wc -l)


#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')


#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')


#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')


#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [$(lsblk | grep "lvm" | wc -l) -gt 0]; then echo yes; else echo no; fi)


#User log
ulog=$(ss -ta | grap ESTAB | wc -l)


#Network
ip=$(users | wc -w)


#sudo
cmnd=$(journalctl_COMM=sudo | grep COMMAND | wc -l)




"monitoring.sh" 63L, 1060B                                                                                                                                                                                9,0-1         Top
     Sudo: 0 cmd


Broadcast message from root@riel-fas42 (tty1) (Thu Dec 19 04:55:21 2024):

 Archotecture: x86_64
     CPU physical: 0
     vCPU: 0
     Memory Usage: #Memory Usage: 226/960MB (
#! /bin/bash

#Arch
arch=$(uname -m)


#CPU Phy
cpuf=$(cat/proc/cpuinfo | grep "physical id" | sort -u | wc -l)


#CPU Vir
cpuv=$(cat/proc/cpuinfo | grep "processor" | wc -l)


#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')


#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')


#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')


#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [$(lsblk | grep "lvm" | wc -l) -gt 0]; then echo yes; else echo no; fi)


#User log
ulog=$(ss -ta | grap ESTAB | wc -l)


#Network
ip=$(users | wc -w)


#sudo
cmnd=$(journalctl_COMM=sudo | grep COMMAND | wc -l)


"./monitoring.sh" 63L, 1060B                                                              8,17          Top
#! /bin/bash
     Disk Usage: Disk Usage: 1.6G/29G (6%)
     CPU load: cpu usage100%%
     Last boot: Last boot2024-12-19 03:59
     LVM use: no
     Connections TCP:  ESTABLISHED
     User log: 0
     Network: IP 2
     Sudo: 0 cmd

^C
riel-fas@riel-fas42:~$ ^C
riel-fas@riel-fas42:~$ ls
monitoring.sh
riel-fas@riel-fas42:~$ nano monitoring.sh
riel-fas@riel-fas42:~$ vi monitoring.sh
riel-fas@riel-fas42:~$ ./monitoring.sh
./monitoring.sh: line 8: cat/proc/cpuinfo: No such file or directory
./monitoring.sh: line 12: cat/proc/cpuinfo: No such file or directory
awk: run time error: not enough arguments passed to printf("#Memory Usage: %d/%dMB (%.2f%%)
")
	FILENAME="-" FNR=2 NR=2
./monitoring.sh: line 33: [7: command not found
./monitoring.sh: line 37: grap: command not found

Broadcast message from riel-fas@riel-fas42 (pts/0) (Thu Dec 19 05:01:14 2024):

 Archotecture: x86_64
     CPU physical: 0
     vCPU: 0
     Memory Usage: #Memory Usage: 221/960MB (
     Disk Usage: Disk Usage: 1.6G/29G (6%)
     CPU load: cpu usage100%%
     Last boot: Last boot2024-12-19 03:59
     LVM use: no
#! /bin/bash

#Arch
arch=$(uname -m)


#CPU Phy
cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)


#CPU Vir
cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)


#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')


#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')


#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')


#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [$(lsblk | grep "lvm" | wc -l) -gt 0]; then echo yes; else echo no; fi)


#User log
ulog=$(ss -ta | grap ESTAB | wc -l)


#Network
ip=$(users | wc -w)


#sudo
cmnd=$(journalctl_COMM=sudo | grep COMMAND | wc -l)


"monitoring.sh" 63L, 1062B                                                                12,11         Top
     Connections TCP:  ESTABLISHED
#! /bin/bash

#Arch
arch=$(uname -m)


#CPU Phy
cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)


#CPU Vir
cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)


#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')


#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')


#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')


#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [$(lsblk | grep "lvm" | wc -l) -gt 0]; then echo yes; else echo no; fi)


#User log
ulog=$(ss -ta | grap ESTAB | wc -l)


#Network
ip=$(users | wc -w)


#sudo
cmnd=$(journalctl_COMM=sudo | grep COMMAND | wc -l)


"monitoring.sh" 63L, 1062B                                                                16,1          Top
  1 #! /bin/bash
  2
  3 #Arch
  4 arch=$(uname -m)
  5
  6
  7 #CPU Phy
  8 cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)
  9
 10
 11 #CPU Vir
 12 cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)
 13
 14
 15 #Memory Usage
     User log: 0
#! /bin/bash

#Arch
arch=$(uname -m)


#CPU Phy
cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)


#CPU Vir
cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)


#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')


#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')


#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')


#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)

#User log
ulog=$(ss -ta | grap ESTAB | wc -l)


#Network
ip=$(users | wc -w)


#sudo
cmnd=$(journalctl_COMM=sudo | grep COMMAND | wc -l)



"monitoring.sh" 62L, 1063B                                                                1,12          Top
#! /bin/bash

#Arch
#! /bin/bash
     Network: IP 2
#! /bin/bash


#Arch
arch=$(uname -m)



#CPU Phy
cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)



#CPU Vir
cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)



#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')



#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')



#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')



#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)



#User log
ulog=$(ss -ta | grap ESTAB | wc -l)


"monitoring.sh" 73L, 1074B                                                                41,0-1        Top
#! /bin/bash


#Arch
arch=$(uname -m)



#CPU Phy
     Sudo: 0 cmd
#! /bin/bash


#Arch
arch=$(uname -m)



#CPU Phy
cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)



#CPU Vir
cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)



#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')



#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')



#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')



#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)



#User log
ulog=$(ss -ta | grap ESTAB | wc -l)


"monitoring.sh" 73L, 1074B                                                                36,0-1        Top
  1 #! /bin/bash
  2
  3
  4 #Arch

#Arch
arch=$(uname -m)



#CPU Phy
cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)



#CPU Vir
cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)



#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')



#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')



#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')



#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)



#User log
ulog=$(ss -ta | grep ESTAB | wc -l)



#Network
ip=$(users | wc -w)
"monitoring.sh" 73L, 1074B                                                                45,19         11%
#Arch
arch=$(uname -m)



#CPU Phy
cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)



#CPU Vir
cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)



#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')



#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')



#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')
riel-fas@riel-fas42:~$ vi monitoring.sh
arch=$(uname -m)



#CPU Phy
cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)



#CPU Vir
cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)



#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')



#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')



#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')



#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)



#User log
ulog=$(ss -ta | grep ESTAB | wc -l)



#Network
ip=$(users | wc -w)

"monitoring.sh" 73L, 1074B                                                                46,0-1        15%
arch=$(uname -m)



#CPU Phy
#! /bin/bash


#Arch
arch=$(uname -m)



#CPU Phy
cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)



#CPU Vir
cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)



#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')



riel-fas@riel-fas42:~$ cpuinfo
-bash: cpuinfo: command not found
riel-fas@riel-fas42:~$ man cpuinfo
-bash: man: command not found
riel-fas@riel-fas42:~$ cpuinfo --help
-bash: cpuinfo: command not found
riel-fas@riel-fas42:~$ vim ./monitoring.sh

Broadcast message from root@riel-fas42 (pts/1) (Thu Dec 19 05:09:21 2024):

 Archotecture: x86_64
     CPU physical: 1
     vCPU: 1
     Memory Usage: #Memory Usage: 236/960MB (
     Disk Usage: Disk Usage: 1.6G/29G (6%)
     CPU load: cpu usage100%%
     Last boot: Last boot2024-12-19 03:59
     LVM use: no
     Connections TCP:  ESTABLISHED
     User log: 0
     Network: IP 3
     Sudo: 0 cmd


Broadcast message from root@riel-fas42 (somewhere) (Thu Dec 19 05:10:04 2024):

 Archotecture: x86_64
     CPU physical: 1
     vCPU: 1
     Memory Usage: #Memory Usage: 236/960MB (
     Disk Usage: Disk Usage: 1.6G/29G (6%)
     CPU load: cpu usage100%%
     Last boot: Last boot2024-12-19 03:59
     LVM use: no
     Connections TCP:  ESTABLISHED
     User log: 0
     Network: IP 3
     Sudo: 0 cmd

^C
riel-fas@riel-fas42:~$ vi monitoring.sh
riel-fas@riel-fas42:~$ vi monitoring.sh
riel-fas@riel-fas42:~$ vi monitoring.sh
riel-fas@riel-fas42:~$ vi monitoring.sh
riel-fas@riel-fas42:~$ vi monitoring.sh
riel-fas@riel-fas42:~$ vi monitoring.sh
riel-fas@riel-fas42:~$ vi monitoring.sh

Broadcast message from root@riel-fas42 (somewhere) (Thu Dec 19 05:30:04 2024):

 Architecture: x86_64
     CPU physical: 1
     vCPU: 1
     Memory Usage: #Memory Usage: 237/960MB (
     Disk Usage: Disk Usage: 1.6G/29G (6%)
     CPU load: cpu usage100%%
     Last boot: Last boot2024-12-19 03:59
     LVM use: yes
     Connections TCP:  ESTABLISHED
     User log: 1
     Network: IP 2
     Sudo: 0 cmd

^C
riel-fas@riel-fas42:~$ clear

#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')



#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')



#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')



#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)



#User log
ulog=$(ss -ta | grep ESTAB | wc -l)



#Network
ip=$(users | wc -w)



#sudo
cmnd=$(journalctl_COMM=sudo | grep COMMAND | wc -l)





wall " Architecture: $arch
     CPU physical: $cpuf
     vCPU: $cpuv
     Memory Usage: $ram_use
     Disk Usage: $disk_use
     CPU load: $cpu_fin%
"monitoring.sh" 73L, 1074B                                                                                                                                                                                61,12         70%

#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')



#Disk Usage
#! /bin/bash


#Arch
arch=$(uname -m)



#CPU Phy
cpuf=$(cat /proc/cpuinfo | grep "physical id" | sort -u | wc -l)



#CPU Vir
cpuv=$(cat /proc/cpuinfo | grep "processor" | wc -l)



#Memory Usage
ram_use=$(free -m | awk '/Mem:/ {printf("#Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2)}')



#Disk Usage
disk_use=$(df -h --total | awk '/total/{printf("Disk Usage: %s/%s (%s)\n", $3, $2, $5)}')



#CPU Load
cpu_fin=$(vmstat 1 4 | tail -1 | awk '{print "cpu usage" $15 "%"}')



#Last Boot
lb=$(who -b | awk '{print "Last boot" $3 " " $4}')



#LVM
lvmu=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)



#User log
ulog=$(ss -ta | grep ESTAB | wc -l)



#Network
ip=$(users | wc -w)



#sudo
cmnd=$(journalctl_COMM=sudo | grep COMMAND | wc -l)





wall " Architecture: $arch
     CPU physical: $cpuf
     vCPU: $cpuv
     Memory Usage: $ram_use
     Disk Usage: $disk_use
     CPU load: $cpu_fin%
     Last boot: $lb
     LVM use: $lvmu
     Connections TCP: $tcpc ESTABLISHED
     User log: $ulog
     Network: IP $ip
     Sudo: $cmnd cmd"

  
  

