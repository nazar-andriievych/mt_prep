# mt_prep

## Practise 10.1

Scan ip address of VM for open ports: 
- sudo nmap localhost -p 0-1000 (MacOS/Linux)
- nmap localhost -p 0-1000 (Windows)

login via ssh 
- ssh ubuntu@<ip of VM> -p 22

if no - check that public key (cat ~/.ssh/id_ed25519.pub) from your host was added to (nano ~/.ssh/authorized_keys) on VM

edit configuration of ssh:
- sudo systemctl edit ssh.socket

And place or update the following block of code
[Socket]
ListenStream=
ListenStream=2222

Save the file and perform the following commands:
- sudo systemctl daemon-reload
- sudo systemctl restart ssh.socket

## Practise 11.1

Add new user with the name test(choose any password you like and all other values can be skipped by pressing Enter)
- sudo adduser test

Let's edit ssh config to allow access with password.
- sudo nano /etc/ssh/sshd_config
and ensure that the following line is uncommented and set to yes(You can use Ctrl+W combination to search for that lines)
- PasswordAuthentication yes
- KbdInteractiveAuthentication yes

To apply config we should restart ssh service:
- sudo systemctl restart ssh

Use commands (whoami) and (pwd) to ensure that you just logined as the user test

## Extra tasks

### from 10.1

1. Organisation A wants to build a single wifi network. The regular count of devices is 240 devices but during different events it may reach up to 350 devices. Calculate the smallest subnet(ip range, network address, broadcast address) which matches the organisation needs if we want a router to use address 10.3.115.1.
- Router Address: 10.3.115.1
- Subnet: 10.3.114.0/23
- Network Address: 10.3.114.0
- Broadcast Address: 10.3.115.255
- Valid Host Range: 10.3.114.1 to 10.3.115.254

2. Find IP Address of linux.org:
- nslookup linux.org

3. Identify the first 5 hops to kernel.org.
- traceroute -m 5 kernel.org

### from 11.1

1. Organisation has 3 departments. Here is the table with the data

Department  | People Count  | Max device count per user
Dep1        |       40      |       3
Dep2        |       10      |       10
Dep3        |       20      |       2

Calculate the smallest subnet which will satisfy the organisation needs if we know that IP 10.13.27.1 should be a part of the netowrk. Result should be in form: subnet mask, IP address range, network address and broadcast address.
- Subnet Mask: /23 (255.255.254.0)
- IP Address Range: 10.13.26.1 – 10.13.27.254
- Network Address: 10.13.26.0
- Broadcast Address: 10.13.27.255

2. Company wants to block access to FTPS server for all hosts except localhost and 10.12.24.5. Propose iptables rules that may be used to perform that task.
- sudo iptables -I INPUT -p tcp --dport 990 -s 127.0.0.1 -j ACCEPT
- sudo iptables -I INPUT -p tcp --dport 990 -s 10.12.24.5 -j ACCEPT
- sudo iptables -A INPUT -p tcp --dport 990 -j REJECT

3. Find all files in /usr/bin containing 'star' in the name:
- find /usr/bin -type f -name "*star*"

## Wifi network

Calculate all
- sudo apt install ipcalc
- ipcalc 10.0.0.1/23

Convert numbers
- echo "obase=2; <decimal>" | bc
- echo "ibase=1; <binary>" | bc

Powers of 2
2^1 = 2
2^2 = 4
2^3 = 8
2^4 = 16
2^5 = 32
2^6 = 64
2^7 = 128
2^8 = 256
2^9 = 512
2^10 = 1024




