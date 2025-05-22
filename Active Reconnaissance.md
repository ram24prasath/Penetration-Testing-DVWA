# Active Reconnaissance

Active Reconnaissance is directly interacting with the application with the intention of gathering information that can later help out finding vulnerabilties. 

In this phase, it involes activities like sending requests to DVWA application and analyzing its response.

Commonly used tools:
1. nmap
2. Burp Suite
3. gobuster
4. dirbuster
5. nikto

---

## Recon using nmap
***nmap*** is a free and open source tool designed for network discovery and security auditing. It is mainly used for port scanning, network inventory and identifying vulnerability.

**Basic Scanning using nmap**:

`nmap -h`

Usage: nmap [Scan Type(s)] [Options] {target specification}

**Scan Type** - This tells Nmap what type of scan will be performed, such as: -sS for TCP SYN scan, -sU for UDP scan, or -sn for a ping scan.

**Options** - This allows you to specify additional elements of the scan, such as: -O for the operating system, -p for port range, or -A for detailed information.

**Target** - This defines the target as either a single IP address, a range of IP addresses, or a domain.

Port Scan using nmap:

`nmap -p- -A 127.0.0.1`

This command tells Nmap to scan all ports using the -p- flag and return detailed information about the target host using the -A flag. 
These results can then be used to identify potential security risks and vulnerabilities present on the target host.

### Scanning for Vulnerability using vulscan

Vulscan uses nmap as the main scanner to scan the IP addresses and domains, the easiest and useful tool for reconnaissance of network. 

***Installation***:
  ``` bash
  cd /usr/share/nmap/script

  sudo git clone https://github.com/scipag/vulscan.git

  sudo nmap --script-updatedb
  ```
Vulscan performs the scan by checking the banners and service versions on the target. 
It is essentially a custom-built scan using Nmap functions and leveraging them against key, reputable sources for vulnerabilities.

This script extends the functionality of Nmap and pulls in vulnerability databases from several different sources, such as NVD, CVE, and OVAL, among others.

``` bash
nmap -sV -p 4280 --script vulscan/vulscan.nse 127.0.0.1 -oN dvwa_nmap_scan.txt
```

The scan results are saved in the text file [dvwa_nmap_scan.txt](dvwa_nmap_scan.txt).

---

## Enumerating directories and files using gobuster

**Install gobuster**:

``` bash
sudo apt-get install gobuster
```

**Install gobuster SecLists repository,which contains “common.txt” wordlist contains a good number of common directory names.**

``` bash
sudo apt-get install seclists
```

**Scan Directories and Files on DVWA**:

``` bash
gobuster dir -u http://localhost:4280/ -w /usr/share/wordlists/dirb/common.txt
```

This command enumerates DVWA directories using the common directory names from seclists.

``` bash
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://localhost:4280/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htpasswd            (Status: 403) [Size: 276]
/.htaccess            (Status: 403) [Size: 276]
/.hta                 (Status: 403) [Size: 276]
/config               (Status: 301) [Size: 314] [--> http://localhost:4280/config/]
/database             (Status: 301) [Size: 316] [--> http://localhost:4280/database/]
/docs                 (Status: 301) [Size: 312] [--> http://localhost:4280/docs/]
/external             (Status: 301) [Size: 316] [--> http://localhost:4280/external/]
/favicon.ico          (Status: 200) [Size: 1406]
/index.php            (Status: 302) [Size: 0] [--> login.php]
/php.ini              (Status: 200) [Size: 154]
/phpinfo.php          (Status: 302) [Size: 0] [--> login.php]
/robots.txt           (Status: 200) [Size: 25]
/server-status        (Status: 403) [Size: 276]
/tests                (Status: 301) [Size: 313] [--> http://localhost:4280/tests/]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
===============================================================

```
