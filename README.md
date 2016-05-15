#### pkpraclinuxsecucok
#####10
######viewing and managing log files (logcheck)
```
apt-get install logcheck
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
apt-get install nmap
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

######monitoring logs using multitail
```
apt-get install multitail
```

monitor two log files simultaneously
```
/etc/glances/glances.conf
