# CyberCenturionNotes
```
sudo apt update
sudo apt upgrade
sudo apt install ufw lynis auditd libpam-pwquality unhide

sudo ufw enable

sudo apt install clamav
sudo freshclam
clamscan -r -i /

sudo apt install chkroootkit
sudo chkrootkit -q

sudo nano /etc/ssh/sshd_config
#See Below
sudo systemctl restart ssh

sudo nano /etc/samba/smb.conf
#See below
sudo systemctl restart smb

sudo apt install aptitude
comm -23 <(aptitude search '~i !~M' -F '%p' | sed "s/ *$//" | sort -u) <(gzip -dc /var/log/installer/initial-status.gz | sed -n 's/^Package: //p' | sort -u)
#Look for Packages
sudo apt remove nmap wireshark ophcrack ftpscan

sudo nano /etc/pam.d/common-password
#See below
#Check for nullok and remove

sudo nano /etc/pam.d/common-auth
# Add: auth required pam_tally2.so onerr=fail deny=3 unlock_time=300 audit even_deny_root
# Check for nullok

sudo nano /etc/login.defs
#See below

sudo apt install fail2ban
sudo systemctl status fail2ban

#sudo apt install lynis
#lynis audit system

sudo apt install auditd audispd-plugins
systemctl --now enable auditd

#PAM modules /etc/pam.d
#common-passwords
#common-auths

#Check Cron Jobs
sudo systemctl status cron/crond
#Check for output

#Other Things - DO NOT RUN BEFORE RESEARCH
#suid binaries
#getcap -r
#restrict sudo commands to users
#cron jobs - check for scripts
#database username and password
#general service issues
```

## Ubuntu Pro
```
sudo apt update
sudo apt install ubuntu-advantage-tools
sudo ua attach C12NzmyPywD8EGVXQDx948xexkYoeZ
sudo ua enable usg
sudo apt install usg
sudo usg generate-tailoring cis_level1_workstation tailor.xml
#Change file to selected=false on essential services
usg fix --tailoring-file tailor.xml
```

## Sample SSHD Changes

```
PermitEmptyPasswords no
PermitRootLogin no
X11Forwarding no
Protocol 2
ClientAliveInterval 180
MaxAuthTries 3
UsePAM yes
```

## Sample smb.conf
```
[global]
disable netbios=yes
min protocol = SMB2
encrypt passwords = yes   
smb encrypt = required

#disable anonymous shares
#disable read/write acess
#change umask NOT 077
```

## Sample common-password changes

```
#After pam_pwquailty.so
retry=3 minlen=10 lcredit=-1 ucredit=-1 ocredit=-1 dcredit=-1 reject_username difok=3 enforce_for_root
#After pam_unix.so 
sha512 minlen=10 remeber=3 obscure rounds=5
```

## Sample login.defs file
```
PASS_MAX_DAYS	30
PASS_MIN_DAYS	2
PASS_MIN_LEN	10
PASS_WARN_AGE	7
ENCRYPT_METHOD SHA512
```

## Possible Bad Packages
```
john, abc, sqlmap, aria2
aquisition, bitcomet, bitlet, bitspirit
endless-sky, zenmap, minetest, minetest-server
armitage, crack, apt pureg knocker, aircrack-ng
airbase-ng, hydra, freeciv
wireshark, tshark
hydra-gtk, netcat, netcat-traditional, netcat-openbsd
netcat-ubuntu, netcat-minimal, qbittorrent, ctorrent
ktorrent, rtorrent, deluge, transmission-common
transmission-bittorrent-client, tixati, frostwise, vuse
irssi, transmission-gtk, utorrent, kismet
medusa, telnet, exim4, telnetd
bind9, crunch, tcpdump, tomcat
tomcat6, vncserver, tightvnc, tightvnc-common
tightvncserver, vnc4server, nmdb, dhclient
telnet-server, ophcrack, cryptcat, cups
cupsd, tcpspray, ettercap
wesnoth, snort, pryit
weplab, wireshark, nikto, lcrack
postfix, snmp, icmp, dovecot
pop3, p0f, dsniff, hunt
ember, nbtscan, rsync, freeciv-client-extras
freeciv-data, freeciv-server, freeciv-client-gtk
```

## NFS /etc/exports
```
#check for root squash
#check for guid squash
#prevent permisssion sharing
#check version - maybe higher, set to higher
#maybe no_root_squash
```

