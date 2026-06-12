Complete Linux Commands Guide for Admin / DevOps
1. Basic System Information
Command	What it does	Why / Where used
uname	Shows system/kernel info	Check OS/kernel details
uname -r	Shows kernel version only	Driver/module compatibility
uname -a	Shows full system info	Troubleshooting
hostname	Shows system hostname	Server identification
hostnamectl	Shows/change hostname	Linux server admin
whoami	Shows current user	Check logged-in user
id	Shows user ID, group ID	Permission troubleshooting
uptime	Shows system running time/load	Server health check
date	Shows system date/time	Logs, cron verification
cal	Shows calendar	Date reference
Examples
uname -r
uname -a
hostnamectl
whoami
id
uptime
date
2. File and Directory Commands
Listing files
ls
ls -l
ls -a
ls -la
ls -lh
ls -ltr
Command	Meaning
ls	List files
ls -l	Long format
ls -a	Show hidden files
ls -la	Long + hidden
ls -lh	Human-readable size
ls -ltr	Oldest to newest modified files
Directory navigation
pwd
cd /path
cd ..
cd ~
cd -
Command	Meaning
pwd	Show current directory
cd /path	Go to path
cd ..	Go one directory back
cd ~	Go to home directory
cd -	Go to previous directory
Create files/directories
touch file.txt
mkdir myfolder
mkdir -p app/logs/errors
Command	Meaning
touch	Create empty file
mkdir	Create directory
mkdir -p	Create parent directories also
Copy, move, rename, delete
cp file1 file2
cp -r dir1 dir2
mv old.txt new.txt
mv file.txt /tmp/
rm file.txt
rm -r folder
rm -rf folder
Command	Meaning
cp	Copy file
cp -r	Copy directory
mv	Move or rename
rm	Delete file
rm -r	Delete directory
rm -rf	Force delete recursively

Careful:

rm -rf /

This can destroy the system.

3. Viewing File Content
cat file.txt
less file.txt
more file.txt
head file.txt
head -n 20 file.txt
tail file.txt
tail -n 50 file.txt
tail -f /var/log/syslog
Command	Use
cat	Show full file
less	View large file page by page
head	Show first lines
tail	Show last lines
tail -f	Live log monitoring

Example:

tail -f /var/log/nginx/access.log

Used to watch live web server logs.

4. Editing Files
Nano editor
nano file.txt

Save:

CTRL + O
ENTER
CTRL + X
Vim editor
vim file.txt

Basic Vim:

i       insert mode
ESC     command mode
:w      save
:q      quit
:wq     save and quit
:q!     quit without saving
dd      delete line
yy      copy line
p       paste
/string search text
5. Modify File Content Using Commands
Add content
echo "Hello Linux" > file.txt
echo "New line" >> file.txt
Symbol	Meaning
>	Overwrite file
>>	Append to file
Replace text
sed -i 's/old/new/g' file.txt

Example:

sed -i 's/localhost/127.0.0.1/g' config.txt
Search text inside files
grep "error" file.txt
grep -i "error" file.txt
grep -r "password" /etc/
grep -n "failed" app.log
Command	Meaning
grep	Search text
grep -i	Case-insensitive
grep -r	Recursive search
grep -n	Show line number
6. File Permissions

Linux permissions:

r = read
w = write
x = execute

Permission structure:

-rwxr-xr--

Meaning:

-     file
rwx   owner permissions
r-x   group permissions
r--   others permissions
Check permissions
ls -l
Change permissions
chmod 755 script.sh
chmod 644 file.txt
chmod +x script.sh
chmod u+x script.sh
chmod g+w file.txt
chmod o-r file.txt
Permission	Meaning
777	Everyone full access
755	Owner full, others read/execute
644	Owner read/write, others read
600	Only owner read/write
400	Only owner read
Common usage
chmod +x deploy.sh
./deploy.sh

Used to make shell scripts executable.

7. File Ownership
chown user file.txt
chown user:group file.txt
chown -R user:group /app
Command	Meaning
chown user file	Change owner
chown user:group file	Change owner and group
chown -R	Recursive ownership change

Example:

sudo chown -R ubuntu:ubuntu /var/www/html

Used when web application files need correct ownership.

8. User Management
Check users
cat /etc/passwd
cut -d: -f1 /etc/passwd
Add user
sudo adduser user2

or:

sudo useradd user2
sudo passwd user2
Delete user
sudo userdel user2
sudo userdel -r user2
Command	Meaning
userdel user2	Delete user
userdel -r user2	Delete user and home directory
Change password
sudo passwd user2
9. Switching Users
su - user2
sudo su -
sudo -i
exit
Command	Meaning
su - user2	Switch to user2
sudo su -	Become root
sudo -i	Login as root shell
exit	Return to previous user

Example:

su - devuser

Used to test permissions as another user.

10. Make User Admin / Sudo User

On Ubuntu/Debian:

sudo usermod -aG sudo user2

On RHEL/CentOS/Amazon Linux:

sudo usermod -aG wheel user2

Check:

groups user2

Important:

usermod -aG sudo user2
Option	Meaning
-a	Append to group
-G	Supplementary group

Do not use only -G without -a, because it may remove the user from other groups.

11. Group Management
groupadd devops
groupdel devops
usermod -aG devops user1
gpasswd -d user1 devops
groups user1
Command	Meaning
groupadd	Create group
groupdel	Delete group
usermod -aG	Add user to group
gpasswd -d	Remove user from group
groups	Show user groups
12. Process Management
View processes
ps
ps aux
top
htop
Command	Meaning
ps	Current shell processes
ps aux	All running processes
top	Live process monitor
htop	Better process monitor

Install htop:

sudo apt install htop -y
Find process
ps aux | grep nginx
pgrep nginx
pidof nginx
Kill process
kill PID
kill -9 PID
pkill nginx
killall nginx
Command	Meaning
kill PID	Stop process politely
kill -9 PID	Force kill
pkill name	Kill by process name
killall name	Kill all matching processes
13. Service Management

Modern Linux uses systemd.

systemctl status nginx
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
systemctl reload nginx
systemctl enable nginx
systemctl disable nginx
Command	Meaning
status	Check service
start	Start service
stop	Stop service
restart	Restart service
reload	Reload config
enable	Start on boot
disable	Do not start on boot

Example:

sudo systemctl restart docker
sudo systemctl status docker
14. Logs Checking
System logs
journalctl
journalctl -xe
journalctl -u nginx
journalctl -u docker
journalctl -f
Command	Meaning
journalctl	View systemd logs
journalctl -xe	Detailed recent errors
journalctl -u service	Logs of service
journalctl -f	Live logs
Common log files
/var/log/syslog          Ubuntu system logs
/var/log/messages        RHEL/CentOS logs
/var/log/auth.log        Login/auth logs
/var/log/secure          RHEL auth logs
/var/log/dmesg           Kernel boot logs
/var/log/nginx/access.log
/var/log/nginx/error.log
/var/log/apache2/access.log
/var/log/apache2/error.log

Examples:

sudo tail -f /var/log/syslog
sudo tail -f /var/log/auth.log
sudo journalctl -u ssh -f
15. Disk Management
Check disk usage
df -h
du -sh *
du -sh /var/log
lsblk
blkid
Command	Meaning
df -h	Disk space
du -sh	Directory size
lsblk	Block devices
blkid	Disk UUID
Find large files
find / -type f -size +500M 2>/dev/null
Mount/unmount
mount /dev/sdb1 /mnt
umount /mnt
16. Memory and CPU Monitoring
free -h
top
htop
vmstat
uptime
lscpu
Command	Meaning
free -h	RAM usage
top	CPU/process usage
vmstat	System performance
lscpu	CPU info

Example:

free -h
top
17. Networking Commands
IP address
ip addr
ip a
ifconfig
hostname -I

ifconfig may not be installed by default.

Install:

sudo apt install net-tools -y
Routing
ip route
route -n
DNS check
cat /etc/resolv.conf
nslookup google.com
dig google.com
host google.com

Install DNS tools:

sudo apt install dnsutils -y
Connectivity check
ping google.com
ping 8.8.8.8
traceroute google.com
curl google.com
wget google.com

Install traceroute:

sudo apt install traceroute -y
Check open ports
ss -tuln
netstat -tuln
lsof -i
Command	Meaning
ss -tuln	Show listening TCP/UDP ports
netstat -tuln	Older alternative
lsof -i	Show network connections

Example:

sudo ss -tuln | grep 80

Used to check if Nginx is listening on port 80.

Test port connection
telnet IP PORT
nc -zv IP PORT

Example:

nc -zv 10.0.1.10 22
nc -zv google.com 443
18. SSH Commands
Connect to server
ssh user@server-ip
ssh -i key.pem ubuntu@public-ip
Copy files using SCP
scp file.txt user@server:/home/user/
scp -i key.pem file.txt ubuntu@ip:/home/ubuntu/
scp -r folder user@server:/tmp/
Sync files using rsync
rsync -av file.txt user@server:/path/
rsync -avz folder/ user@server:/backup/
19. Firewall Commands
Ubuntu UFW
sudo ufw status
sudo ufw enable
sudo ufw disable
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
sudo ufw deny 3306
sudo ufw delete allow 80
Firewalld
sudo firewall-cmd --state
sudo firewall-cmd --list-all
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload

Used mostly in RHEL/CentOS systems.

20. Package Management
Ubuntu/Debian
sudo apt update
sudo apt upgrade -y
sudo apt install nginx -y
sudo apt remove nginx -y
sudo apt purge nginx -y
sudo apt autoremove -y
RHEL/CentOS/Amazon Linux
sudo yum update -y
sudo yum install nginx -y
sudo yum remove nginx -y

Newer systems:

sudo dnf install nginx -y
21. Cron Jobs

Cron is used to schedule repeated tasks.

Edit cron
crontab -e
List cron jobs
crontab -l
Remove all cron jobs
crontab -r
Cron format
* * * * * command
| | | | |
| | | | day of week
| | | month
| | day of month
| hour
minute
Examples

Run every minute:

* * * * * /home/ubuntu/script.sh

Run every day at 2 AM:

0 2 * * * /home/ubuntu/backup.sh

Run every Sunday at 5 AM:

0 5 * * 0 /home/ubuntu/cleanup.sh
Check cron logs

Ubuntu:

grep CRON /var/log/syslog

RHEL/CentOS:

grep CRON /var/log/cron
Important cron troubleshooting

Always use full paths:

* * * * * /usr/bin/python3 /home/ubuntu/app.py

Not:

* * * * * python3 app.py
22. Search Files
find / -name file.txt
find /home -name "*.log"
find /var/log -type f -name "*.log"
find / -type f -size +100M
Command	Meaning
find / -name	Search by filename
find -type f	Files only
find -type d	Directories only
find -size	Search by size

Example:

find /var/log -type f -name "*.log"
23. Archive and Compression
tar -cvf backup.tar folder
tar -xvf backup.tar
tar -czvf backup.tar.gz folder
tar -xzvf backup.tar.gz
zip -r backup.zip folder
unzip backup.zip
Command	Meaning
tar -cvf	Create tar
tar -xvf	Extract tar
tar -czvf	Create compressed tar.gz
tar -xzvf	Extract tar.gz
zip -r	Create zip
unzip	Extract zip
24. Environment Variables
env
printenv
echo $PATH
export APP_ENV=production

Permanent variable:

nano ~/.bashrc

Add:

export APP_ENV=production

Apply:

source ~/.bashrc
25. Important Admin Files
File	Purpose
/etc/passwd	User account info
/etc/shadow	Password hashes
/etc/group	Group info
/etc/sudoers	Sudo permissions
/etc/ssh/sshd_config	SSH config
/etc/fstab	Disk mount config
/etc/hosts	Local DNS entries
/etc/resolv.conf	DNS resolver config
/var/log/	Log files

Edit sudoers safely:

sudo visudo

Never directly edit:

sudo nano /etc/sudoers
26. Checking Login and User Activity
who
w
last
lastlog
history
Command	Meaning
who	Logged-in users
w	Logged-in users + activity
last	Login history
lastlog	Last login of all users
history	Command history

Check failed SSH login:

sudo grep "Failed password" /var/log/auth.log
27. Important DevOps Commands
Git
git clone URL
git status
git add .
git commit -m "message"
git push
git pull
git branch
git checkout branch
git switch branch
Docker
docker ps
docker ps -a
docker images
docker build -t app .
docker run -d -p 80:80 app
docker logs container_id
docker exec -it container_id bash
docker stop container_id
docker rm container_id
Kubernetes
kubectl get pods
kubectl get svc
kubectl get nodes
kubectl describe pod podname
kubectl logs podname
kubectl exec -it podname -- bash
kubectl apply -f file.yaml
kubectl delete -f file.yaml
28. Real Troubleshooting Scenarios
Port 80 not working
sudo ss -tuln | grep 80
sudo systemctl status nginx
sudo journalctl -u nginx -xe
sudo ufw status
Disk full
df -h
du -sh /*
find / -type f -size +500M 2>/dev/null
sudo journalctl --vacuum-time=7d
CPU high
top
ps aux --sort=-%cpu | head
Memory high
free -h
ps aux --sort=-%mem | head
SSH not working
sudo systemctl status ssh
sudo ss -tuln | grep 22
sudo ufw status
sudo tail -f /var/log/auth.log
Cron not running
crontab -l
grep CRON /var/log/syslog
chmod +x script.sh
which python3
29. Most Important Commands for Fresher DevOps
ls -la
cd
pwd
cat
less
tail -f
grep
find
chmod
chown
sudo
su -
usermod -aG
systemctl status
journalctl -xe
df -h
du -sh
free -h
top
ps aux
kill
ip a
ip route
ping
curl
ss -tuln
ssh
scp
crontab -e
crontab -l
