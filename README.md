#### pkpraclinuxsecucok
use ubuntu 14.04
#####1
######conducting integrity checks
```
apt-get install gtkhash -y
```

######USING luks
```
telinit 1
umount /home
fuser -mvk /home
```
check to confirm that the /home partition is not mounted
```
grep home /proc/mounts
```


######scanning hosts with nmap
scan a range
```
nmap -vv -sP 1.2.3.4-100
```


#####3
######viewing file and directory
list by column
```
ls -FC
```
exclude all the files and display only their subdict
```
ls -d */
```
ls all subdict
```
ls -R
```
######changing the file permisstions using chmod
copy file1's permission to file2
```
chmod --reference=file1 file2
```
######implementing access control list
```
touch a
useradd a
passwd -d a
setfacl -m u:a:rwx a
setfacl -m other:--- a
getfacl a
getfacl -R /etc
```

save and restore
```
getfacl -R /etc > res.acl
cd /anotherfolder
setfact -- restore=res.acl
```
######filehandling using mv
```
mv file1 file2 file3 /home/
```
using regex
```
mv -v *.txt /home
```

######install ldap
```
apt-get install slapd -y
apt-get install ldap-utils
dpkg-reconfigure slapd->No->
```
then
```
apt-get install phpldapadmin
```
<end>

#####4
######user auth
check all incorrect login attempts for a particular user
```
lastb user
```
get auth log last 10
```
tail -n 10 /var/log/auth.log
```
And the last command.
```
last
```
######Limiting the login capa
```
passwd -l user1   // usermod -L user1
passwd -u user1   // usermod -U user1
passwd -S user1  //show status of user. L=locked P=not
```


#####5
######disabling or enabling SSH root
######Restricting remote access with key
```
ssh-keygen -t rsa
ssh-copy-id remote_ip
```
######copYing remotely
```
sftp
get file.txt /etc    //copy /etc/file.txt to local
```


#####6

######tcp ip
lshw  list all hardware
```
lshw -class network
```
```
service network-manager restart  //redhat?
```
######using iptables to configure a firewall
```
iptables -v  //version
```

```
iptables -S
```
```
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
insert a role at index
```
iptables -I INPUT 1 -i lo -j ACCEPT
```
block input chain
```
iptables -A INPUT -j DROP
```
but these changes are non persistent.Hence
```
apt-get install iptables-persistent
service iptables-persistent start
```
######blocking spoofed addresses
```
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```
create a new table call blocked
```
iptables -N blocked
```
insert `block`table into INPUT table.
```
iptables -I INPUT 2 -j blocked
```
add a ip address into blocked table
```
iptables -A blocked -s 192.168.1.222 -j DROP
```
then
```
vim /etc/host.conf
```
edit
```
nospoof on
```

######block incoming traffic
```
iptables -A INPUT -i lo -j ACCEPT
```





#####7
######Linux (sxid)
```
apt-get install sxid -y
```
```
vim /etc/sxid.conf
```
edit
```
EMAIL="rengokantai"
KEEP_LOGS="5"
ALWAYS_NOTIFY="yes"
SEARCH
EXCLUDE
```
run command
```
sxid -c /etc/scid.conf -k
```
######portsentry (base on nmap)
```
apt-get install portsentry
```
```
grep portsentry /var/log/syslog
```
config
```
vim /etc/portsentry/portsentry.conf
```
edit
```
# block scan
BLOCK_UDP="1"
BLOCK_TCP="1"
```
and
```
# iptables support for Linux
KILL_ROUTE="/sbin/iptables -I INPUT -s $TARGET$ -j DROP"
```
other file:
```
vim /etc/default/portsentry
```
edit
```
TCP_MODE="atcp"
UDP_MODE="audp"
```

######using squid proxy
```
apt-get update -y && apt-get upgrade && apt-get install squid
```

######openssl server
```
apt-get install openssl apache2 -y
a2enmod ssl
```

```
mkdir /etc/apache2/ssl
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/server.key -out /etc/apache2/ssl/server.crt
```

Edit in
```
vim /etc/apache2/sites-avilable/default
```

```
SSLEngine on
SSLCertificateFile  /etc/apache2/ssl/server.crt
SSLCertificateKeyFile /etc/apache2/ssl/server.key
```
######tripwire
######shorewall
```
apt-get install shorewall -y
```
must config before start
```
vim /etc/default/shorewall
```
edit
```
startup=1
```
then
```
vim /etc/shorewall/shorewall.conf
```
edit
```
IP_FORWARDING=On
```
eth0->external eth1->internal




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


