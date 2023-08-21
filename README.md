# Linux_System_Hardening
Linux system hardening guide to reduce the attack surface for all the baddies out there.

This is a guide to reduce the attack surface by hardening your linux system by applied methods. 

In Scope: 
1. Updates and Security updates:
   While hardening linux server the first important part is keep system up to date. Any old version softwares or packages can increase the threat level. Updates or more importantly security updates are released all the time for the packages that you've installed on you server or system. Because of this it is very hard to stay up to date. Way to prevent this is to automatically install security updates.
You can do this with Unattended Upgrade package which gives you complete control over which updates you want to automatically install.
You can edit the file and enable only for security updates. Just type command

   𝘴𝘶𝘥𝘰 𝘯𝘢𝘯𝘰 /𝘦𝘵𝘤/𝘢𝘱𝘵/𝘢𝘱𝘵.𝘤𝘰𝘯𝘧.𝘥/50𝘶𝘯𝘢𝘵𝘵𝘦𝘯𝘥𝘦𝘥-𝘶𝘱𝘨𝘳𝘢𝘥𝘦𝘴

2. Basic Hardening:
   
   After diagnosing the system look for the users in the system who have root privileges.Multiple users having root privileges increases the threat level. Also in the system if more users can execute command 𝘴𝘶𝘥𝘰 𝘴𝘶 as they are in sudo group increases the security risk.

   To add any user into the sudo group use following command:

   𝘜𝘴𝘦𝘳𝘮𝘰𝘥 –𝘢𝘎 𝘴𝘶𝘥𝘰 <𝘶𝘴𝘦𝘳>

   To remove any user from the sudo group use the following command:

   𝘴𝘶𝘥𝘰 𝘥𝘦𝘭𝘶𝘴𝘦𝘳 𝘶𝘴𝘦𝘳𝘯𝘢𝘮𝘦 𝘴𝘶𝘥𝘰

   For the normal user, even access to sudo should be prohibited.Only put trusty users in sudo group and those users will have privileges to use sudo.

In linux, root is a very powerful user and it increases the risk level multiple times if it isn’t require password for authentication to become the root.

3. SSH Hardening:
   SSH or Secure Shell is the popular protocol for doing system administration on Linux systems. It runs on most systems, often with its default configuration. As this service opens up a potential gateway into the system.
   In the system look for 𝘴𝘴𝘩𝘥_𝘤𝘰𝘯𝘧𝘪𝘨 file in /𝘦𝘵𝘤/𝘴𝘴𝘩 dic, the ssh service is running on a default port 22. Port 22 for ssh is well known and can become potential threat so changing the port 22 to any other port number will be helpful.This will keep attacker away from trying to login ssh. And it will become hard to guess the port where the actual ssh service is running.Also in the same file change permit root login from yes to no.

   In sshd_config change the following

   𝘗𝘢𝘴𝘴𝘸𝘰𝘳𝘥𝘈𝘶𝘵𝘩𝘦𝘯𝘵𝘪𝘤𝘢𝘵𝘪𝘰𝘯 𝘯𝘰

   𝘗𝘦𝘳𝘮𝘪𝘵𝘌𝘮𝘱𝘵𝘺𝘗𝘢𝘴𝘴𝘸𝘰𝘳𝘥𝘴 𝘯𝘰

   After disabling the password login only way to login into the system is using public key.

   If authrized keys are present anywhere in the system increases the level of threat. Either changing read/write permissions of those authorized keys or keeping them safe will reduce the danger.

4. Network Hardening:

   Fail2ban:

   Fail2ban scans log files (e.g. /var/log/apache/error_log) and bans IPs that show the malicious signs such as too many password failures, seeking or exploits, etc.. Generally Fail2Ban is then used to update firewall rules to reject the IP addresses for a specified amount of time, although any arbitrary other action (e.g. sending an email) could also be configured. Out of the box Fail2Ban comes with filters for various services (apache, courier, ssh, etc.).

   Fail2Ban is able to reduce the rate of incorrect authentications attempts however it cannot eliminate the risk that weak authentication presents. Configure services to use only two factor or public/private authentication mechanisms if you really want to protect services.
   To install fail2ban into the system type following command:

   𝘴𝘶𝘥𝘰 𝘢𝘱𝘵 𝘪𝘯𝘴𝘵𝘢𝘭𝘭 𝘧𝘢𝘪𝘭2𝘣𝘢𝘯

   In /etc/fail2ban/jail.conf edit maxretry, findtime and bantime. If attacker tries to authenticate more that configured trial limit fail2ban will ban that IP for configured time duration.


   UFW utility:

   UFW (uncomplicated firewall) is a firewall configuration tool that runs on top of iptables, included by default within Ubuntu distributions. It provides a streamlined interface for configuring common firewall use cases via the command line.

   To install the ufw use following command:

   𝘴𝘶𝘥𝘰 𝘢𝘱𝘵-𝘨𝘦𝘵 𝘪𝘯𝘴𝘵𝘢𝘭𝘭 𝘶𝘧𝘸

   To set the default rules use following command:

   𝘴𝘶𝘥𝘰 𝘶𝘧𝘸 𝘥𝘦𝘧𝘢𝘶𝘭𝘵 𝘢𝘭𝘭𝘰𝘸 𝘰𝘶𝘵𝘨𝘰𝘪𝘯𝘨

   𝘴𝘶𝘥𝘰 𝘶𝘧𝘸 𝘥𝘦𝘧𝘢𝘶𝘭𝘵 𝘥𝘦𝘯𝘺 𝘪𝘯𝘤𝘰𝘮𝘪𝘯𝘨

   Rules can be added by mentioning the port number or the service. For example

    𝘴𝘶𝘥𝘰 𝘶𝘧𝘸 𝘢𝘭𝘭𝘰𝘸 𝘴𝘴𝘩

    𝘴𝘶𝘥𝘰 𝘶𝘧𝘸 𝘢𝘭𝘭𝘰𝘸 22

   UFW allows you to allow/block by IP addresses, subnets, and a IP address/subnet/port combinations. For example

    To allow connections from an IP address:

    𝘴𝘶𝘥𝘰 𝘶𝘧𝘸 𝘢𝘭𝘭𝘰𝘸 𝘧𝘳𝘰𝘮 198.168.1.2

    To allow connections from a specific subnet:

    𝘴𝘶𝘥𝘰 𝘶𝘧𝘸 𝘢𝘭𝘭𝘰𝘸 𝘧𝘳𝘰𝘮 198.51.100.0/24

    To remove a rule, add 𝘥𝘦𝘭𝘦𝘵𝘦 before the rule implementation.

5. Lynis and Linpeas:

   Lynis is a battle-tested security tool for systems running Linux, mac OS, or Unix-based operating system. It performs an extensive health scan of your systems to support system hardening and compliance testing.Everyday system audit and vulnerability audits reduces the threat level.

   To install lynis into the system type following command:

   𝘴𝘶𝘥𝘰 𝘢𝘱𝘵 𝘪𝘯𝘴𝘵𝘢𝘭𝘭 𝘭𝘺𝘯𝘪𝘴

   To perform local system audit:

   𝘭𝘺𝘯𝘪𝘴 𝘢𝘶𝘥𝘪𝘵 𝘴𝘺𝘴𝘵𝘦𝘮

   You can analyze dockerfile, do remote security scans, refer to lynis man page.


   Linpeas is a well-known enumeration script that searches for possible paths to escalate privileges on Linux/Unix* targets. To install linpeas : https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS

   ./𝘭𝘪𝘯𝘱𝘦𝘢𝘴 –𝘩 this will show you all the flags you can use.

   Use ./𝘭𝘪𝘯𝘱𝘦𝘢𝘴 –𝘢, it will check for entire system.

6. Pwdquality installation and configuration for new user:

   Security level of your system increases when the every user's password meets the certain requirements. To install the pwdquality into the system use below command.

    𝘴𝘶𝘥𝘰 𝘢𝘱𝘵-𝘨𝘦𝘵 𝘪𝘯𝘴𝘵𝘢𝘭𝘭 𝘭𝘪𝘣𝘱𝘢𝘮-𝘱𝘸𝘥𝘲𝘶𝘢𝘭𝘪𝘵𝘺

   Now to edit the pwdquality conf. file navigate to /etc/security/pwdquality.conf, and edit password character limit to 16. Small length passwords increases the threat levels. Make sure you're root user or has sudo priviledges. 
   
