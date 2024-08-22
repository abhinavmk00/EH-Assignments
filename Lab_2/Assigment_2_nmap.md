# Nmap

## Trying to find the os of the scanme.nmap.org server
```terminal
abhi@abhi-Lenovo-IdeaPad-S145-15IKB:~$ nmap -O -T1 scanme.nmap.org
TCP/IP fingerprinting (for OS scan) requires root privileges.
QUITTING!
abhi@abhi-Lenovo-IdeaPad-S145-15IKB:~$ sudo !!
sudo nmap -O -T1 scanme.nmap.org
[sudo] password for abhi:            
Starting Nmap 7.80 ( https://nmap.org ) at 2024-08-22 10:30 IST
Stats: 0:02:32 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 0.70% done
Stats: 0:03:02 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 0.90% done

[1]+  Stopped                 sudo nmap -O -T1 scanme.nmap.org
```
The scan was takeing to long to finish so tried to swithing to a different speed option

## Trying the can with a faster -T5 option
```terminal
abhi@abhi-Lenovo-IdeaPad-S145-15IKB:~$ sudo nmap -O -T5 scanme.nmap.org
Starting Nmap 7.80 ( https://nmap.org ) at 2024-08-22 10:33 IST
Warning: 45.33.32.156 giving up on port because retransmission cap hit (2).
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.21s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 992 closed ports
PORT      STATE    SERVICE
22/tcp    open     ssh
25/tcp    filtered smtp
80/tcp    open     http
135/tcp   filtered msrpc
139/tcp   filtered netbios-ssn
445/tcp   filtered microsoft-ds
9929/tcp  open     nping-echo
31337/tcp open     Elite
OS fingerprint not ideal because: Timing level 5 (Insane) used
No OS matches for host

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 35.67 seconds
```
The scan was compleated in  35 seconds but the os fingerprint couldn't be performed becasue of the speed lets try a lower speed option

## Trying to run at a slower speed -T4
```terminal
abhi@abhi-Lenovo-IdeaPad-S145-15IKB:~$ sudo nmap -O -T4 scanme.nmap.org
Starting Nmap 7.80 ( https://nmap.org ) at 2024-08-22 10:34 IST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.29s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 992 closed ports
PORT      STATE    SERVICE
22/tcp    open     ssh
25/tcp    filtered smtp
80/tcp    filtered http
135/tcp   filtered msrpc
139/tcp   filtered netbios-ssn
445/tcp   filtered microsoft-ds
9929/tcp  open     nping-echo
31337/tcp open     Elite
OS fingerprint not ideal because: Didn't receive UDP response. Please try again with -sSU
No OS matches for host

OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 46.82 seconds
```
still haveing trouble finding the os but got suggested to use the -sSU option
## Trying the -sSU option
```terminal
abhi@abhi-Lenovo-IdeaPad-S145-15IKB:~$ sudo nmap -O -T4 -sSU scanme.nmap.org
Starting Nmap 7.80 ( https://nmap.org ) at 2024-08-22 10:36 IST
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.26s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 999 open|filtered ports, 992 closed ports
PORT      STATE    SERVICE
22/tcp    open     ssh
25/tcp    filtered smtp
80/tcp    open     http
135/tcp   filtered msrpc
139/tcp   filtered netbios-ssn
445/tcp   filtered microsoft-ds
9929/tcp  open     nping-echo
31337/tcp open     Elite
123/udp   open     ntp
No OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.80%E=4%D=8/22%OT=22%CT=1%CU=%PV=N%G=Y%TM=66C6C7AB%P=x86_64-pc-l
OS:inux-gnu)SEQ(SP=105%GCD=1%ISR=108%TI=Z%CI=Z%II=Z%TS=A)OPS(O1=M514ST11NW7
OS:%O2=M514ST11NW7%O3=M514NNT11NW7%O4=M514ST11NW7%O5=M514ST11NW7%O6=M514ST1
OS:1)WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)ECN(R=Y%DF=Y%TG=40
OS:%W=FAF0%O=M514NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%TG=40%S=O%A=S+%F=AS%RD=0%Q=)T2(
OS:R=N)T3(R=N)T4(R=Y%DF=Y%TG=FF%W=400%S=A%A=S%F=AR%O=%RD=0%Q=)T5(R=Y%DF=Y%T
OS:G=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%TG=FF%W=8000%S=A%A=S%F=AR%
OS:O=%RD=0%Q=)T7(R=N)U1(R=N)IE(R=Y%DFI=Y%TG=40%CD=S)


OS detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 90.30 seconds
```
It prints the TCP/IP fingerprint but can't recognize the os yet
## Tring the verbose flag in default speed to get a os fingerprint
```terminal
abhi@abhi-Lenovo-IdeaPad-S145-15IKB:~$ nmap -v -A scanme.nmap.org
Starting Nmap 7.80 ( https://nmap.org ) at 2024-08-22 10:39 IST
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 10:39
Completed NSE at 10:39, 0.00s elapsed
Initiating NSE at 10:39
Completed NSE at 10:39, 0.00s elapsed
Initiating NSE at 10:39
Completed NSE at 10:39, 0.00s elapsed
Initiating Ping Scan at 10:39
Scanning scanme.nmap.org (45.33.32.156) [2 ports]
Completed Ping Scan at 10:39, 0.67s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 10:39
Completed Parallel DNS resolution of 1 host. at 10:39, 0.00s elapsed
Initiating Connect Scan at 10:39
Scanning scanme.nmap.org (45.33.32.156) [1000 ports]
Discovered open port 22/tcp on 45.33.32.156
Discovered open port 9929/tcp on 45.33.32.156
Increasing send delay for 45.33.32.156 from 0 to 5 due to 24 out of 78 dropped probes since last increase.
Discovered open port 31337/tcp on 45.33.32.156
Connect Scan Timing: About 40.60% done; ETC: 10:40 (0:00:45 remaining)
Increasing send delay for 45.33.32.156 from 5 to 10 due to max_successful_tryno increase to 4
Increasing send delay for 45.33.32.156 from 10 to 20 due to max_successful_tryno increase to 5
Increasing send delay for 45.33.32.156 from 20 to 40 due to max_successful_tryno increase to 6
Increasing send delay for 45.33.32.156 from 40 to 80 due to max_successful_tryno increase to 7
Completed Connect Scan at 10:41, 94.75s elapsed (1000 total ports)
Initiating Service scan at 10:41
Scanning 3 services on scanme.nmap.org (45.33.32.156)
Completed Service scan at 10:41, 1.45s elapsed (3 services on 1 host)
NSE: Script scanning 45.33.32.156.
Initiating NSE at 10:41
Completed NSE at 10:41, 16.64s elapsed
Initiating NSE at 10:41
Completed NSE at 10:41, 0.00s elapsed
Initiating NSE at 10:41
Completed NSE at 10:41, 0.00s elapsed
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.31s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 992 closed ports
PORT      STATE    SERVICE      VERSION
22/tcp    open     ssh          OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 ac:00:a0:1a:82:ff:cc:55:99:dc:67:2b:34:97:6b:75 (DSA)
|   2048 20:3d:2d:44:62:2a:b0:5a:9d:b5:b3:05:14:c2:a6:b2 (RSA)
|   256 96:02:bb:5e:57:54:1c:4e:45:2f:56:4c:4a:24:b2:57 (ECDSA)
|_  256 33:fa:91:0f:e0:e1:7b:1f:6d:05:a2:b0:f1:54:41:56 (ED25519)
25/tcp    filtered smtp
80/tcp    filtered http
135/tcp   filtered msrpc
139/tcp   filtered netbios-ssn
445/tcp   filtered microsoft-ds
9929/tcp  open     nping-echo   Nping echo
31337/tcp open     tcpwrapped
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
Initiating NSE at 10:41
Completed NSE at 10:41, 0.00s elapsed
Initiating NSE at 10:41
Completed NSE at 10:41, 0.00s elapsed
Initiating NSE at 10:41
Completed NSE at 10:41, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 114.07 seconds 
```
In the service info we find the OS to be Linux
And because of the scripts that ran by useing the -A flag we could also see that the port for ssh is open and the virsion of the os is seen to be ubuntu 

## Conclution

We found some of the services that are running on the server namely:

|PORT         |STATE        |SERVICE      |
|-------------|-------------|-------------|
|22/tcp       |open         |ssh          |
|25/tcp    |filtered |smtp|
|80/tcp    |open     |http|
|135/tcp   |filtered |msrpc|
|139/tcp   |filtered |netbios-ssn|
|445/tcp   |filtered |microsoft-ds|
|9929/tcp  |open     |nping-echo|
|31337/tcp |open     |Elite|
|123/udp   |open     |ntp|

some of these ports are open and some of them are filtered

in addition to this we know the server is running ubuntu