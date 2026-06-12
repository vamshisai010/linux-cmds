# Complete Linux Commands Guide for Admin, DevOps, Networking, Permissions, Logs and Troubleshooting

This file is GitHub-ready Markdown.  
Use file extension:

```text
linux-complete-admin-guide.md
```

---

# 1. Basic Linux System Information

System information commands are used to check OS details, kernel version, hostname, logged-in user, uptime, and server identity.

## 1.1 `uname`

### What it does
Shows operating system and kernel information.

### Why we use it
To check the Linux kernel version, architecture, and system information.

### Where we use it
- Server troubleshooting
- Driver/module compatibility checking
- DevOps server documentation
- Cloud instance verification

### Commands

```bash
uname
uname -r
uname -a
uname -m
uname -s
```

### Explanation

| Command | Meaning |
|---|---|
| `uname` | Shows OS name |
| `uname -r` | Shows kernel release/version |
| `uname -a` | Shows all system information |
| `uname -m` | Shows machine architecture |
| `uname -s` | Shows kernel name |

### Example

```bash
uname -r
```

Output example:

```text
6.8.0-31-generic
```

This means the Linux kernel version is `6.8.0-31-generic`.

---

## 1.2 `hostname`

### What it does
Shows the system hostname.

### Why we use it
To identify the server.

### Where we use it
- Multi-server environments
- AWS EC2 instances
- Kubernetes nodes
- DevOps inventory

### Commands

```bash
hostname
hostname -I
hostnamectl
```

### Explanation

| Command | Meaning |
|---|---|
| `hostname` | Shows hostname |
| `hostname -I` | Shows IP address |
| `hostnamectl` | Shows hostname and OS info |

### Change hostname

```bash
sudo hostnamectl set-hostname dev-server-01
```

---

## 1.3 User and uptime commands

```bash
whoami
id
uptime
date
cal
```

| Command | What it does | Why we use it |
|---|---|---|
| `whoami` | Shows current logged-in user | To confirm which user is running commands |
| `id` | Shows UID, GID and groups | Permission troubleshooting |
| `uptime` | Shows system running time and load | Server health check |
| `date` | Shows date/time | Log and cron verification |
| `cal` | Shows calendar | Date checking |

Example:

```bash
whoami
id
uptime
date
```

---

# 2. File and Directory Commands

These commands are used to create, move, copy, delete, list, and navigate files/directories.

---

## 2.1 `pwd`

### What it does
Shows the current working directory.

### Why we use it
To know where we are in the filesystem.

### Example

```bash
pwd
```

Output:

```text
/home/ubuntu
```

---

## 2.2 `ls`

### What it does
Lists files and directories.

### Why we use it
To view files, permissions, ownership, and modification time.

### Commands

```bash
ls
ls -l
ls -a
ls -la
ls -lh
ls -ltr
ls -R
```

### Explanation

| Command | Meaning |
|---|---|
| `ls` | List normal files |
| `ls -l` | Long listing format |
| `ls -a` | Show hidden files |
| `ls -la` | Long format including hidden files |
| `ls -lh` | Human-readable file sizes |
| `ls -ltr` | Sort by time, oldest first |
| `ls -R` | Recursive listing |

### Example

```bash
ls -lah
```

Used to check file permissions, hidden files, and file sizes.

---

## 2.3 `cd`

### What it does
Changes directory.

### Commands

```bash
cd /var/log
cd ..
cd ~
cd -
cd /
```

### Explanation

| Command | Meaning |
|---|---|
| `cd /var/log` | Move to `/var/log` |
| `cd ..` | Go one directory back |
| `cd ~` | Go to current user home |
| `cd -` | Go to previous directory |
| `cd /` | Go to root directory |

---

## 2.4 Create files and directories

```bash
touch file.txt
mkdir project
mkdir -p app/logs/errors
```

| Command | Meaning |
|---|---|
| `touch file.txt` | Create empty file |
| `mkdir project` | Create directory |
| `mkdir -p app/logs/errors` | Create nested directories |

### Example

```bash
mkdir -p /home/ubuntu/app/logs
touch /home/ubuntu/app/logs/app.log
```

Used while preparing application folders.

---

## 2.5 Copy, move, rename, delete

```bash
cp file1.txt file2.txt
cp -r folder1 folder2
mv old.txt new.txt
mv app.log /tmp/
rm file.txt
rm -r folder
rm -rf folder
```

| Command | Meaning |
|---|---|
| `cp` | Copy file |
| `cp -r` | Copy directory recursively |
| `mv` | Move or rename |
| `rm` | Delete file |
| `rm -r` | Delete directory |
| `rm -rf` | Force delete recursively |

### Warning

```bash
rm -rf /
```

This can destroy the full Linux system. Never run it.

---

# 3. Viewing File Content

Used for checking configuration files, logs, scripts, and application output.

## Commands

```bash
cat file.txt
less file.txt
more file.txt
head file.txt
head -n 20 file.txt
tail file.txt
tail -n 50 file.txt
tail -f /var/log/syslog
```

| Command | What it does | Where used |
|---|---|---|
| `cat` | Shows full file | Small files |
| `less` | Scroll large file | Logs/configs |
| `more` | Page-wise view | Basic file reading |
| `head` | First 10 lines | Check file start |
| `head -n 20` | First 20 lines | Custom output |
| `tail` | Last 10 lines | Recent logs |
| `tail -n 50` | Last 50 lines | Recent errors |
| `tail -f` | Live file monitoring | Logs |

### Example

```bash
sudo tail -f /var/log/nginx/access.log
```

Used to monitor live Nginx access logs.

---

# 4. Editing Files

Linux administrators often edit configuration files, scripts, service files, and cron files.

## 4.1 Nano

```bash
nano file.txt
```

### Why use Nano
Nano is beginner-friendly.

### Save and exit

```text
CTRL + O  save
ENTER     confirm
CTRL + X  exit
```

---

## 4.2 Vim

```bash
vim file.txt
```

### Why use Vim
Vim is powerful and available on most Linux servers.

### Basic Vim shortcuts

| Key | Meaning |
|---|---|
| `i` | Insert mode |
| `ESC` | Exit insert mode |
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |
| `dd` | Delete line |
| `yy` | Copy line |
| `p` | Paste |
| `/text` | Search text |

---

# 5. Modifying File Content with Commands

These commands are used in automation, shell scripts, DevOps pipelines, and config changes.

## 5.1 `echo`

```bash
echo "Hello Linux"
echo "Hello Linux" > file.txt
echo "New line" >> file.txt
```

| Symbol | Meaning |
|---|---|
| `>` | Overwrite file |
| `>>` | Append to file |

### Example

```bash
echo "server_name example.com;" >> nginx.conf
```

---

## 5.2 `sed`

### What it does
Searches and replaces text inside files.

### Why we use it
To modify config files automatically.

### Command

```bash
sed -i 's/old/new/g' file.txt
```

### Explanation

| Part | Meaning |
|---|---|
| `sed` | Stream editor |
| `-i` | Edit file directly |
| `s/old/new/` | Substitute old with new |
| `g` | Replace all occurrences in each line |

### Example

```bash
sed -i 's/localhost/127.0.0.1/g' config.txt
```

---

## 5.3 `grep`

### What it does
Searches text/patterns inside files.

### Why we use it
To find errors, logs, keywords, users, ports, and config values.

### Commands

```bash
grep "error" app.log
grep -i "error" app.log
grep -r "password" /etc/
grep -n "failed" app.log
grep -v "success" app.log
```

| Command | Meaning |
|---|---|
| `grep "error"` | Search exact lowercase error |
| `grep -i` | Case-insensitive search |
| `grep -r` | Recursive search |
| `grep -n` | Show line numbers |
| `grep -v` | Exclude matching lines |

### Example

```bash
sudo grep "Failed password" /var/log/auth.log
```

Used to check failed SSH login attempts.

---

# 6. File Permissions

Linux permissions control who can read, write, and execute files.

## Permission symbols

```text
r = read
w = write
x = execute
```

Example permission:

```text
-rwxr-xr--
```

Meaning:

```text
-      file
rwx    owner can read/write/execute
r-x    group can read/execute
r--    others can only read
```

---

## 6.1 Check permissions

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 ubuntu ubuntu 1000 Jun 13 file.txt
```

---

## 6.2 `chmod`

### What it does
Changes file permissions.

### Why we use it
To allow or restrict access.

### Commands

```bash
chmod 755 script.sh
chmod 644 file.txt
chmod 600 private.key
chmod +x deploy.sh
chmod u+x script.sh
chmod g+w file.txt
chmod o-r file.txt
```

| Permission | Meaning | Common use |
|---|---|---|
| `777` | Everyone full access | Avoid in production |
| `755` | Owner full, others read/execute | Scripts/directories |
| `644` | Owner read/write, others read | Normal files |
| `600` | Only owner read/write | SSH keys/config secrets |
| `400` | Only owner read | Private keys |

### Example

```bash
chmod 400 key.pem
ssh -i key.pem ubuntu@server-ip
```

AWS SSH private keys usually need secure permission like `400`.

---

## 6.3 `chown`

### What it does
Changes file owner and group.

### Commands

```bash
chown user file.txt
chown user:group file.txt
chown -R ubuntu:ubuntu /var/www/html
```

| Command | Meaning |
|---|---|
| `chown user file` | Change owner |
| `chown user:group file` | Change owner and group |
| `chown -R` | Recursive ownership change |

### Example

```bash
sudo chown -R www-data:www-data /var/www/html
```

Used for web server file ownership.

---

# 7. User Management

Used by Linux administrators to create, delete, switch, and manage users.

## 7.1 Check users

```bash
cat /etc/passwd
cut -d: -f1 /etc/passwd
```

### Why use it
To list all users present on the system.

---

## 7.2 Add user

Ubuntu/Debian:

```bash
sudo adduser user2
```

Generic Linux:

```bash
sudo useradd user2
sudo passwd user2
```

| Command | Meaning |
|---|---|
| `adduser` | Interactive user creation |
| `useradd` | Low-level user creation |
| `passwd` | Set password |

---

## 7.3 Delete user

```bash
sudo userdel user2
sudo userdel -r user2
```

| Command | Meaning |
|---|---|
| `userdel user2` | Delete user only |
| `userdel -r user2` | Delete user and home directory |

---

## 7.4 Switch users

```bash
su - user2
sudo su -
sudo -i
exit
```

| Command | Meaning |
|---|---|
| `su - user2` | Switch to user2 |
| `sudo su -` | Become root |
| `sudo -i` | Root login shell |
| `exit` | Return back |

---

## 7.5 Make user admin

Ubuntu/Debian:

```bash
sudo usermod -aG sudo user2
```

RHEL/CentOS/Amazon Linux:

```bash
sudo usermod -aG wheel user2
```

Check:

```bash
groups user2
```

### Important

Use:

```bash
-aG
```

Because:

| Option | Meaning |
|---|---|
| `-a` | Append user to group |
| `-G` | Supplementary group |

Without `-a`, existing groups may be removed.

---

# 8. Group Management

Groups are used to control shared access.

```bash
sudo groupadd devops
sudo groupdel devops
sudo usermod -aG devops user1
sudo gpasswd -d user1 devops
groups user1
```

| Command | Meaning |
|---|---|
| `groupadd` | Create group |
| `groupdel` | Delete group |
| `usermod -aG` | Add user to group |
| `gpasswd -d` | Remove user from group |
| `groups` | Check groups |

### Example

```bash
sudo groupadd docker
sudo usermod -aG docker ubuntu
```

Used to allow user to run Docker without sudo.

---

# 9. Process Management

Processes are running programs.

## 9.1 View processes

```bash
ps
ps aux
top
htop
```

| Command | Meaning |
|---|---|
| `ps` | Current shell processes |
| `ps aux` | All running processes |
| `top` | Live process monitoring |
| `htop` | Advanced live monitoring |

Install htop:

```bash
sudo apt install htop -y
```

---

## 9.2 Find process

```bash
ps aux | grep nginx
pgrep nginx
pidof nginx
```

### Example

```bash
ps aux | grep java
```

Used to check Java application process.

---

## 9.3 Kill process

```bash
kill PID
kill -9 PID
pkill nginx
killall nginx
```

| Command | Meaning |
|---|---|
| `kill PID` | Gracefully stop process |
| `kill -9 PID` | Force kill |
| `pkill name` | Kill by process name |
| `killall name` | Kill all matching processes |

---

# 10. Service Management

Most modern Linux systems use `systemd`.

## Commands

```bash
sudo systemctl status nginx
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl reload nginx
sudo systemctl enable nginx
sudo systemctl disable nginx
```

| Command | Meaning | Where used |
|---|---|---|
| `status` | Check service status | Troubleshooting |
| `start` | Start service | Manual start |
| `stop` | Stop service | Maintenance |
| `restart` | Restart service | Config changes |
| `reload` | Reload config without full restart | Nginx/Apache |
| `enable` | Start service on boot | Production setup |
| `disable` | Disable boot start | Cleanup |

### Example

```bash
sudo systemctl restart nginx
sudo systemctl status nginx
```

---

# 11. Logs Checking

Logs are critical for troubleshooting.

## 11.1 `journalctl`

```bash
journalctl
journalctl -xe
journalctl -u nginx
journalctl -u docker
journalctl -f
journalctl --since "1 hour ago"
```

| Command | Meaning |
|---|---|
| `journalctl` | Show system logs |
| `journalctl -xe` | Show recent errors with details |
| `journalctl -u nginx` | Show Nginx service logs |
| `journalctl -f` | Follow live logs |
| `--since` | Time-based log filtering |

### Example

```bash
sudo journalctl -u docker -f
```

Used to monitor Docker service logs.

---

## 11.2 Common log files

```text
/var/log/syslog              Ubuntu system logs
/var/log/messages            RHEL/CentOS system logs
/var/log/auth.log            Ubuntu authentication logs
/var/log/secure              RHEL authentication logs
/var/log/dmesg               Kernel boot logs
/var/log/nginx/access.log    Nginx access logs
/var/log/nginx/error.log     Nginx error logs
/var/log/apache2/access.log  Apache access logs
/var/log/apache2/error.log   Apache error logs
```

### Examples

```bash
sudo tail -f /var/log/syslog
sudo tail -f /var/log/auth.log
sudo tail -f /var/log/nginx/error.log
```

---

# 12. Disk Management

Used to check storage usage, partitions, and large files.

## Commands

```bash
df -h
du -sh *
du -sh /var/log
lsblk
blkid
```

| Command | Meaning |
|---|---|
| `df -h` | Show disk usage |
| `du -sh *` | Show folder sizes |
| `lsblk` | Show disks and partitions |
| `blkid` | Show disk UUID |

## Find large files

```bash
find / -type f -size +500M 2>/dev/null
```

## Mount/unmount

```bash
sudo mount /dev/sdb1 /mnt
sudo umount /mnt
```

---

# 13. CPU and Memory Monitoring

```bash
free -h
top
htop
vmstat
uptime
lscpu
```

| Command | Meaning |
|---|---|
| `free -h` | Show RAM usage |
| `top` | CPU and process monitoring |
| `htop` | Better live monitoring |
| `vmstat` | CPU/memory/io stats |
| `uptime` | Load average |
| `lscpu` | CPU details |

### Example

```bash
ps aux --sort=-%cpu | head
ps aux --sort=-%mem | head
```

Used to find high CPU or memory processes.

---

# 14. Networking Commands

Networking commands are used to check IP, DNS, routing, ports, firewall, and connectivity.

## 14.1 IP address

```bash
ip addr
ip a
ifconfig
hostname -I
```

| Command | Meaning |
|---|---|
| `ip addr` | Show IP addresses |
| `ip a` | Short form |
| `ifconfig` | Old network command |
| `hostname -I` | Show system IPs |

Install `ifconfig`:

```bash
sudo apt install net-tools -y
```

---

## 14.2 Routing

```bash
ip route
route -n
```

### Why use it
To check default gateway and network route.

Example:

```bash
ip route
```

---

## 14.3 DNS check

```bash
cat /etc/resolv.conf
nslookup google.com
dig google.com
host google.com
```

Install DNS tools:

```bash
sudo apt install dnsutils -y
```

### Example

```bash
nslookup google.com
```

Used to check if DNS resolution works.

---

## 14.4 Connectivity

```bash
ping google.com
ping 8.8.8.8
traceroute google.com
curl google.com
wget google.com
```

| Command | Meaning |
|---|---|
| `ping` | Check network reachability |
| `traceroute` | Show network path |
| `curl` | Test HTTP/API |
| `wget` | Download/test URL |

Install traceroute:

```bash
sudo apt install traceroute -y
```

---

## 14.5 Check open ports

```bash
ss -tuln
netstat -tuln
lsof -i
sudo ss -tuln | grep 80
```

| Command | Meaning |
|---|---|
| `ss -tuln` | Show listening TCP/UDP ports |
| `netstat -tuln` | Older alternative |
| `lsof -i` | Show network connections |
| `grep 80` | Filter port 80 |

---

## 14.6 Test port connection

```bash
telnet IP PORT
nc -zv IP PORT
```

Examples:

```bash
nc -zv 10.0.1.10 22
nc -zv google.com 443
```

Used to test SSH/HTTPS connectivity.

---

# 15. SSH Commands

SSH is used to connect remote Linux servers.

## Connect to server

```bash
ssh user@server-ip
ssh -i key.pem ubuntu@public-ip
```

## Copy files with SCP

```bash
scp file.txt user@server:/home/user/
scp -i key.pem file.txt ubuntu@ip:/home/ubuntu/
scp -r folder user@server:/tmp/
```

## Sync files with rsync

```bash
rsync -av file.txt user@server:/path/
rsync -avz folder/ user@server:/backup/
```

| Command | Meaning |
|---|---|
| `ssh` | Remote login |
| `scp` | Secure copy |
| `rsync` | Efficient sync/copy |

---

# 16. Firewall Commands

## 16.1 UFW - Ubuntu firewall

```bash
sudo ufw status
sudo ufw enable
sudo ufw disable
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
sudo ufw deny 3306
sudo ufw delete allow 80
```

| Command | Meaning |
|---|---|
| `ufw status` | Check firewall status |
| `ufw enable` | Enable firewall |
| `ufw allow 22` | Allow SSH |
| `ufw allow 80` | Allow HTTP |
| `ufw allow 443` | Allow HTTPS |
| `ufw deny 3306` | Block MySQL |

---

## 16.2 Firewalld - RHEL/CentOS

```bash
sudo firewall-cmd --state
sudo firewall-cmd --list-all
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload
```

---

# 17. Package Management

## 17.1 Ubuntu/Debian - APT

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install nginx -y
sudo apt remove nginx -y
sudo apt purge nginx -y
sudo apt autoremove -y
```

| Command | Meaning |
|---|---|
| `apt update` | Refresh package list |
| `apt upgrade` | Upgrade packages |
| `apt install` | Install package |
| `apt remove` | Remove package |
| `apt purge` | Remove package and config |
| `apt autoremove` | Remove unused packages |

---

## 17.2 RHEL/CentOS/Amazon Linux

```bash
sudo yum update -y
sudo yum install nginx -y
sudo yum remove nginx -y
sudo dnf install nginx -y
```

---

# 18. Cron Jobs

Cron is used to schedule repeated jobs.

## Commands

```bash
crontab -e
crontab -l
crontab -r
```

| Command | Meaning |
|---|---|
| `crontab -e` | Edit cron jobs |
| `crontab -l` | List cron jobs |
| `crontab -r` | Remove all cron jobs |

## Cron format

```text
* * * * * command
| | | | |
| | | | day of week
| | | month
| | day of month
| hour
minute
```

## Examples

Every minute:

```cron
* * * * * /home/ubuntu/script.sh
```

Every day at 2 AM:

```cron
0 2 * * * /home/ubuntu/backup.sh
```

Every Sunday at 5 AM:

```cron
0 5 * * 0 /home/ubuntu/cleanup.sh
```

## Check cron logs

Ubuntu:

```bash
grep CRON /var/log/syslog
```

RHEL/CentOS:

```bash
grep CRON /var/log/cron
```

## Cron troubleshooting

```bash
crontab -l
chmod +x /home/ubuntu/script.sh
which python3
grep CRON /var/log/syslog
```

Use full paths inside cron:

```cron
* * * * * /usr/bin/python3 /home/ubuntu/app.py
```

---

# 19. Search Files

```bash
find / -name file.txt
find /home -name "*.log"
find /var/log -type f -name "*.log"
find / -type f -size +100M
find / -type d -name "nginx"
```

| Command | Meaning |
|---|---|
| `find / -name file.txt` | Search file by name |
| `find /home -name "*.log"` | Search log files |
| `find -type f` | Files only |
| `find -type d` | Directories only |
| `find -size +100M` | Large files |

---

# 20. Archive and Compression

```bash
tar -cvf backup.tar folder
tar -xvf backup.tar
tar -czvf backup.tar.gz folder
tar -xzvf backup.tar.gz
zip -r backup.zip folder
unzip backup.zip
```

| Command | Meaning |
|---|---|
| `tar -cvf` | Create tar archive |
| `tar -xvf` | Extract tar |
| `tar -czvf` | Create tar.gz |
| `tar -xzvf` | Extract tar.gz |
| `zip -r` | Create zip |
| `unzip` | Extract zip |

---

# 21. Environment Variables

```bash
env
printenv
echo $PATH
export APP_ENV=production
```

Permanent environment variable:

```bash
nano ~/.bashrc
```

Add:

```bash
export APP_ENV=production
```

Apply:

```bash
source ~/.bashrc
```

---

# 22. Important Admin Files

| File | Purpose |
|---|---|
| `/etc/passwd` | User account info |
| `/etc/shadow` | Password hashes |
| `/etc/group` | Group info |
| `/etc/sudoers` | Sudo permissions |
| `/etc/ssh/sshd_config` | SSH config |
| `/etc/fstab` | Disk mount config |
| `/etc/hosts` | Local hostname mapping |
| `/etc/resolv.conf` | DNS resolver |
| `/var/log/` | Logs directory |

Edit sudoers safely:

```bash
sudo visudo
```

Do not directly edit sudoers with normal editor unless necessary.

---

# 23. Login and User Activity

```bash
who
w
last
lastlog
history
```

| Command | Meaning |
|---|---|
| `who` | Logged-in users |
| `w` | Logged-in users and activity |
| `last` | Login history |
| `lastlog` | Last login of users |
| `history` | Command history |

Failed SSH attempts:

```bash
sudo grep "Failed password" /var/log/auth.log
```

---

# 24. Git Commands

```bash
git clone URL
git status
git add .
git commit -m "message"
git push
git pull
git branch
git checkout branch
git switch branch
```

| Command | Meaning |
|---|---|
| `git clone` | Download repository |
| `git status` | Check file changes |
| `git add .` | Stage files |
| `git commit` | Save changes locally |
| `git push` | Upload to remote |
| `git pull` | Download latest changes |
| `git branch` | List/create branches |
| `git checkout` | Switch branch |
| `git switch` | Modern branch switch |

---

# 25. Docker Commands

```bash
docker ps
docker ps -a
docker images
docker build -t app .
docker run -d -p 80:80 app
docker logs container_id
docker exec -it container_id bash
docker stop container_id
docker rm container_id
```

| Command | Meaning |
|---|---|
| `docker ps` | Running containers |
| `docker ps -a` | All containers |
| `docker images` | Local images |
| `docker build` | Build image |
| `docker run` | Run container |
| `docker logs` | Container logs |
| `docker exec` | Enter container |
| `docker stop` | Stop container |
| `docker rm` | Remove container |

---

# 26. Kubernetes Commands

```bash
kubectl get pods
kubectl get svc
kubectl get nodes
kubectl describe pod podname
kubectl logs podname
kubectl exec -it podname -- bash
kubectl apply -f file.yaml
kubectl delete -f file.yaml
```

| Command | Meaning |
|---|---|
| `kubectl get pods` | List pods |
| `kubectl get svc` | List services |
| `kubectl get nodes` | List nodes |
| `kubectl describe pod` | Detailed pod info |
| `kubectl logs` | Pod logs |
| `kubectl exec` | Enter pod |
| `kubectl apply` | Create/update resource |
| `kubectl delete` | Delete resource |

---

# 27. Troubleshooting Scenarios

## 27.1 Port 80 not working

```bash
sudo ss -tuln | grep 80
sudo systemctl status nginx
sudo journalctl -u nginx -xe
sudo ufw status
```

### Why
Checks whether service is listening, running, logging errors, or blocked by firewall.

---

## 27.2 Disk full

```bash
df -h
du -sh /*
find / -type f -size +500M 2>/dev/null
sudo journalctl --vacuum-time=7d
```

### Why
Finds large directories/files and clears old journal logs.

---

## 27.3 CPU high

```bash
top
ps aux --sort=-%cpu | head
```

### Why
Finds processes using high CPU.

---

## 27.4 Memory high

```bash
free -h
ps aux --sort=-%mem | head
```

### Why
Finds memory-consuming processes.

---

## 27.5 SSH not working

```bash
sudo systemctl status ssh
sudo ss -tuln | grep 22
sudo ufw status
sudo tail -f /var/log/auth.log
```

### Why
Checks SSH service, port 22, firewall, and authentication logs.

---

## 27.6 Cron not running

```bash
crontab -l
grep CRON /var/log/syslog
chmod +x script.sh
which python3
```

### Why
Checks cron schedule, logs, script permission, and command path.

---

# 28. Most Important Commands for Fresher DevOps

```bash
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
git status
docker ps
kubectl get pods
```

---

# 29. Practice Task for Beginners

Try these tasks on Ubuntu:

```bash
mkdir linux-practice
cd linux-practice
touch notes.txt
echo "Linux practice started" > notes.txt
cat notes.txt
chmod 644 notes.txt
ls -l
mkdir logs
touch logs/app.log
echo "error: nginx failed" >> logs/app.log
grep "error" logs/app.log
cd ..
tar -czvf linux-practice.tar.gz linux-practice
```

This task covers:
- Directory creation
- File creation
- Writing content
- Reading content
- Permissions
- Grep search
- Archive creation

---

# End of Linux Admin / DevOps Guide
