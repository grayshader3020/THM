###  Vulnerabilities_101

```
What vulnerabilities are
Why they're worthy of learning about
How are vulnerabilities rated
Databases for vulnerability research
A showcase of how vulnerability research is used on ACKme's engagement
```
**Introduction to Vulnerabilities**

- A vulnerability in cybersecurity is defined as a weakness or flaw in the design, 	       implementation or behaviours of a system or application.
- Vulnerabilities can originate from many factors, including a poor design of an          application or an oversight of the intended actions from a user

- There are 5 main types of vulnerabilities

1. Operating System

	These types of vulnerabilities are found within Operating Systems (OSs) and often result in privilege escalation.

2. (Mis)Configuration-based

	These types of vulnerability stem from an incorrectly configured application or service. For example, a website exposing customer details.

3. Weak or Default Credentials

	Applications and services that have an element of authentication will come with default credentials when installed. For example, an administrator dashboard may have the username and password of "admin". These are easy to guess by an attacker. 

4. Application Logic

	These vulnerabilities are a result of poorly designed applications. For example, poorly implemented authentication mechanisms that may result in an attacker being able to impersonate a user.

5. Human-Factor

	Human-Factor vulnerabilities are vulnerabilities that leverage human behaviour. For example, phishing emails are designed to trick humans into believing they are legitimate.


**Scoring Vulnerabilities (CVSS & VPR)**

- Vulnerability management is the process of evaluating, categorising and ultimately remediating threats (vulnerabilities) faced by an organisation.

- Vulnerability scoring serves a vital role in vulnerability management and is used to determine the potential risk and impact a vulnerability may have on a network or computer system

*CVSS*

- First introduced in 2005, the Common Vulnerability Scoring System (or CVSS) is a very popular framework for vulnerability scoring and has three major iterations

 1. How easy is it to exploit the vulnerability?

 2. Do exploits exist for this?

 3. How does this vulnerability interfere with the CIA triad?

``
 ---------------------------
	None	|  0
	Low	    | 10.1 - 3.9
	Medium	| 4.0 - 6.9
	High	| 7.0 - 8.9
	Critical| 9.0 - 10.0
``

*Advantages of CVSS*
	1. CVSS has been around for a long time.
	2. CVSS is popular in organisations.
	3. CVSS is a free framework to adopt and recommended by organisations such as NIST.

*Disadvantages of CVSS*
	1.CVSS was never designed to help prioritise vulnerabilities, instead, just assign    value of severity.
	2. CVSS heavily assesses vulnerabilities on an exploit being available. However, only  of all vulnerabilities have an exploit available (Tenable., 2020) .
	3. Vulnerabilities rarely change scoring after assessment despite the fact that new developments such as exploits may be found.

*VPR*

- The VPR framework is a much more modern framework in vulnerability management - developed by Tenable, an industry solutions provider for vulnerability management
- Unlike CVSS, VPR scoring takes into account the relevancy of a vulnerability


``
 ---------------------------
	Low	    | 0.0-3.9
	Medium	| 4.0 - 6.9
	High	| 7.0 - 8.9
	Critical| 9.0 - 10.0
``

*Advantages of VPR*
	1.VPR is a modern framework that is real-world.
	2.VPR considers over 150 factors when calculating risk.
	3.VPR is risk-driven and used by organisations to help prioritise patching vulnerabilities.
	4.Scorings are not final and are very dynamic, meaning the priority a vulnerability should be given can change as the vulnerability ages.

*Disadvantages of VPR*
	1. VPR is not open-source like some other vulnerability management frameworks.
	2. VPR can only be adopted apart of a commercial platform.
	3. VPR does not consider the CIA triad to the extent that CVSS does; meaning that risk to the confidentiality, integrity and availability of data does not play a large factor in scoring vulnerabilities when using VPR

***Vulnerability Databases***

1. Using NVD, how many CVEs were published in July 2021?
```
	1554
```
2. Who is the author of Exploit-DB?
```
 	offsec
```

**An Example of Finding a Vulnerability**

1. What type of vulnerability did we use to find the name and version of the application in this example?
```
	Version Disclosure
```

**Showcase: Exploiting Ackme's Application**

Scope defined is : 240.228.189.136

- Company details
	
```
Companies Report
Company Info
Established: 2017
Business Type: Corporation
Purpose: IT Support Services
Clients: 800+
CEO
Danny Phantom
d.phantom@ackme.thm
```
nmap scan::
```
	PORT STATE SERVICE
	22/tcp open ssh
	80/tcp open http
	443/tcp open https
```
Acme portal of Version 1.5.2

1. Follow along with the showcase of exploiting ACKme's application to the end to retrieve a flag. What is this flag?
```
	THM{ACKME_ENGAGEMENT}

```

**Conclusion**