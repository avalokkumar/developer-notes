# Nmap
Nmap, short for Network Mapper, is a powerful open-source tool and network scanning utility that is widely used for network discovery and security auditing. It is designed to help network administrators and security professionals identify devices running on a network, discover open ports and services, gather information about those services, and assess the security of the network.

### Here's how Nmap works and how it is commonly used:

1. **Network Discovery**: Nmap is used to discover devices on a network. It can scan a range of IP addresses to determine which hosts are online and reachable. This is particularly useful for identifying all the devices connected to a network, including computers, servers, routers, and more.

2. **Port Scanning**: Nmap can perform port scanning, which involves probing a target system to determine which ports are open and what services are running on those ports. This is crucial for network administrators to understand the network's topology and the services exposed on each device.

3. **Service Fingerprinting**: Nmap can attempt to identify the version and type of services running on open ports. This is valuable for assessing the security of those services, as outdated or vulnerable software versions can be a security risk.

4. **OS Detection**: Nmap has the capability to guess the operating system of a target host based on various network characteristics and responses. This helps administrators understand the types of systems on their network.

5. **Scripting and Automation**: Nmap supports scripting using the Nmap Scripting Engine (NSE). Users can create custom scripts or use existing scripts to automate tasks such as vulnerability scanning, service enumeration, and more.

6. **Vulnerability Assessment**: Security professionals use Nmap to identify potential vulnerabilities in networked devices. By scanning for open ports and known vulnerabilities associated with specific services, Nmap can help identify areas of concern that require further investigation.

7. **Security Auditing**: Nmap is a valuable tool for conducting security audits of networks. It helps identify weak points, misconfigurations, and potential security risks, enabling administrators to take proactive measures to enhance network security.

8. **Penetration Testing**: Ethical hackers and penetration testers use Nmap to assess the security posture of a network. By identifying open ports and services, they can attempt to exploit vulnerabilities and report findings to improve security.

**How to Use Nmap**:

Using Nmap typically involves running it from the command line with various options and arguments. Here's a basic example of how to perform a simple Nmap scan:

```bash
nmap target_ip
```

- Replace `target_ip` with the IP address of the host or network you want to scan.

Nmap offers a wide range of command-line options and customization features. Users can specify scan types, port ranges, and output formats, among other things. Here are some common Nmap scan types:

- **TCP Connect Scan**: This is the default scan type that establishes a full TCP connection to each target port.
- **SYN Scan (Half-open Scan)**: Sends SYN packets to target ports to determine if they are open. It's faster and more stealthy than a full connect scan.
- **UDP Scan**: Scans UDP ports to identify open services. UDP scans can be slower and less reliable than TCP scans.
- **Aggressive Scan (-A)**: Performs OS detection, version detection, script scanning, and traceroute.

### More Examples:

**1. Network Discovery:**
   - Scan a single IP address to check if it's online:
     ```
     nmap 192.168.1.100
     ```

   - Scan a range of IP addresses to discover online hosts:
     ```
     nmap 192.168.1.1-50
     ```

   - Perform a ping scan to identify online hosts without port scanning:
     ```
     nmap -sn 192.168.1.0/24
     ```

**2. Port Scanning:**
   - Perform a basic scan of common ports on a single host:
     ```
     nmap -p 80,443 example.com
     ```

   - Scan all 65,535 ports on a host (may take longer):
     ```
     nmap -p- example.com
     ```

   - Scan a range of ports on multiple hosts:
     ```
     nmap -p 22,80 192.168.1.100-110
     ```

**3. Service Fingerprinting:**
   - Perform a service version scan to identify software and version information:
     ```
     nmap -sV example.com
     ```

**4. OS Detection:**
   - Attempt to detect the operating system of a target host:
     ```
     nmap -O example.com
     ```

**5. Scripting and Automation:**
   - Run a specific Nmap script to gather information about web servers:
     ```
     nmap --script http-enum example.com
     ```

   - List available NSE scripts:
     ```
     nmap --script-help
     ```

**6. Vulnerability Assessment:**
   - Use Nmap's vulnerability scripts to scan for known vulnerabilities:
     ```
     nmap --script vuln example.com
     ```

**7. Security Auditing:**
   - Perform an aggressive scan to identify potential security issues:
     ```
     nmap -A example.com
     ```

**8. Penetration Testing:**
   - Run a scan to identify open ports and potential vulnerabilities:
     ```
     nmap -p 1-65535 -A example.com
     ```

**9. Scan Specific Top Ports:**
   - Scan the top 100 most common ports:
     ```
     nmap --top-ports 100 example.com
     ```

**10. Scan IPv6 Addresses:**
   - Perform an IPv6 scan on a target:
     ```
     nmap -6 example.com
     ```

**11. Scan Multiple Hosts in a File:**
   - Scan a list of hosts stored in a text file:
     ```
     nmap -iL hostlist.txt
     ```

**12. Exclude Specific Ports:**
   - Scan all ports except a specified range:
     ```
     nmap --exclude-ports 20-30 example.com
     ```

**13. Scan for UDP Services:**
   - Perform a UDP scan to identify services running on UDP ports:
     ```
     nmap -sU example.com
     ```

**14. Scan for Specific DNS Records:**
   - Perform a DNS query to retrieve specific DNS records (e.g., MX records for mail servers):
     ```
     nmap --script dns-nsec-enum example.com
     ```

**15. Scan Using a Specific Source IP:**
   - Specify a source IP address for scanning:
     ```
     nmap --source-ip 192.168.1.2 example.com
     ```

**16. Save Output to a File:**
   - Save scan results to a file for further analysis:
     ```
     nmap -oN output.txt example.com
     ```

**17. Aggressive Timing and OS Detection:**
   - Use aggressive timing settings and attempt OS detection:
     ```
     nmap -T4 -A example.com
     ```

**18. Scan a Range of Hosts in a CIDR Notation:**
    - Scan a range of hosts using CIDR notation:
      ```
      nmap 192.168.1.0/24
      ```

**19. Scan Using a Specific Network Interface:**
    - Specify the network interface to use for scanning:
      ```
      nmap -e eth0 example.com
      ```

**20. Display Hostnames:**
    - Resolve and display hostnames during the scan:
      ```
      nmap -sL example.com
      ```

**21. Fast Scan (Top 100 Ports):**
    - Perform a quick scan of the top 100 ports:
      ```
      nmap -F example.com
      ```

**22. Scan a Specific IP Range:**
   - Scan a specific range of IP addresses:
     ```
     nmap 192.168.1.1-20
     ```

**23. Perform a Fast Scan with No DNS Resolution:**
   - Scan quickly and skip DNS resolution:
     ```
     nmap -T4 -F -n example.com
     ```

**24. Scan for Vulnerabilities with CVEs:**
   - Use the vulners script to check for Common Vulnerabilities and Exposures (CVEs):
     ```
     nmap --script vulners example.com
     ```

**25. Scan Using Randomized Timing:**
   - Randomize the timing to evade intrusion detection systems:
     ```
     nmap -T5 -r example.com
     ```

**26. Scan a Target Multiple Times:**
   - Scan the same target multiple times for reliability:
     ```
     nmap -p 80 -oX scan1.xml example.com && nmap -p 80 -oX scan2.xml example.com
     ```

**27. Scan a Host to Check for Heartbleed Vulnerability:**
   - Use a specific script to check for the Heartbleed vulnerability:
     ```
     nmap --script ssl-heartbleed example.com
     ```

**28. Detect and Identify Web Application Firewalls (WAFs):**
   - Identify if a target uses a WAF:
     ```
     nmap --script http-waf-detect example.com
     ```

**29. Scan a Range of Ports for Specific Services:**
   - Scan a range of ports for specific services, like HTTP and SSH:
     ```
     nmap -p 80,22 example.com
     ```

**30. Scan Using a Proxy:**
   - Use a proxy server for scanning:
     ```
     nmap --proxy http://proxy-server:8080 example.com
     ```

**31. Perform a Slow Comprehensive Scan:**
    - Use a comprehensive scan with slower timing and more detail:
      ```
      nmap -T2 -p- -sV --script "default or safe" example.com
      ```

**32. Show Live Hosts Only:**
    - Display only hosts that are online:
      ```
      nmap -sP 192.168.1.0/24
      ```

**33. Scan for SNMP Services:**
    - Scan for Simple Network Management Protocol (SNMP) services:
      ```
      nmap -p 161,162 example.com
      ```


