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




  
  

