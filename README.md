#### pkpraclinuxsecucok
#####10
######viewing and managing log files (logcheck)
```
apt-get install logcheck -y
```
config file:
```
vim /etc/logcheck/logcheck.conf
```
edit:(uncomment)
```
DATE
RULEDIR
REPORTLEVEL
SENDMAILTO
ATTACKSUBJECT
SECURITYSUBJECT
EVENTSSUBJECT
```
logpath file:
```
vim /etc/logcheck/logcheck.logfiles
```
edit(monitor all paths you want to monitor)
```
/var/log/syslog
/var/log/auth.log
/var/log/boot.log
```
######monitoring a network (nmap)
```
apt-get install nmap -y
nmap -sP 192.168.1.0/24
nmap -O 192.168.1.1
```
######system monotoring (glances)
```
apt-get install glances
```
```
vim /etc/default/glances
```
edit
```
RUN="true"
```
indicators:  
green:ok blue: careful violet:warning red:critical  
run:
```
glances -t 5
glances -c -P 192.168.1.1
```
to edit conf
```
/etc/glances/glances.conf
```

######monitoring logs using (multitail)
```
apt-get install multitail
```

monitor two log files simultaneously
```
multitail /var/log/syslog /var/log/boot.log
```
b to choose between, q to exit
```
multitail -s 2 /var/log/syslog /var/log/boot.log  //two lines
```
customize color
```
multitail -ci yellow /var/log/syslog -ci blue /var/log/boot.log
```
######system tools (whowatch)
```
apt-get install whowatch
```
run:
```
whoswatch
```
press F9 to go menu bar.
######stat
```
stat a.txt
stat -f /dev/sda2
stat a.*
```
######list open files (lsof)
list files belong to user
```
lsof -u ubuntu
```
process running on paticular port
```
lsof -i TCP:22
```

###### strace
```
strace -o output.txt ls
```
######auditing log files on linux (lynis)
```
apt-get install lynis -y
```
start a scan
```
lynis -c
```
log is saved see
```
vim /var/log/lynis.log
```


