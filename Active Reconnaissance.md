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

