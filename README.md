# Vulnerability Scanning with Nessus on Metasploitable

## Table of Contents
**Tools used**

**Executive Summary**
 - Approach
 - Scope
 - Assessment Overview and Recommendations

**Assessment Summary**:
 - Summary of Findings

**Technical Findings Details**

## Tools Used
- **Nessus**: A powerful vulnerability scanning tool used to detect potential security issues across networked systems.
- **Metasploitable**: A purposefully vulnerable Linux VM designed for security testing.
- **VirtualBox**: Virtualization software used to host the Metasploitable machine on a Windows host.
- **Host-Only Adapter**: Network configuration to allow direct communication between the host and VM.

## Project Steps
1. **Network Setup**: 
   - Configured Metasploitable with a host-only network on VirtualBox.
   - Ensured connectivity between Nessus (on the Windows host) and Metasploitable VM.
  
2. **Vulnerability Scanning**:
   - Conducted a **comprehensive scan** using Nessus.
   - Target: Metasploitable VM (IP: `192.168.X.X`).

3. **Analysis**:
   - Identified **111 vulnerabilities**, including:
     - 7 **Critical**
     - 2 **High**
     - 21 **Medium**
     - 8 **Low**
     - 73 **Informational**
  
4. **Reporting**:
   - Generated a detailed PDF report highlighting key findings and recommendations.
   - Vulnerabilities were categorized based on severity and potential impact.

## Executive summary
In this project, we conducted a simulated vulnerability assessment on a deliberately vulnerable machine (Metasploitable) as if tasked by a client. The primary objectives were to identify security weaknesses, assess their potential impact, and document findings in a clear, actionable format with prioritized remediation recommendations.

### Approach
The assessment was conducted between [start date] and [end date] using Nessus, a vulnerability scanning tool, to systematically evaluate the target machine for known weaknesses. Testing followed a “non-invasive” approach, aiming to identify and categorize vulnerabilities without active exploitation. Each vulnerability was analyzed to determine the risk level and possible impact, providing insights into critical, high, medium, and low-severity issues, with remediation recommendations prioritized by risk.
### Scope
The scope of this assessment was limited to a single, internal virtual machine environment: the Metasploitable machine, configured to simulate a vulnerable network for testing and analysis.
#### In-Scope Assets
screenshot

### Assessment Overview and Recommendations
During the vulnerability assessment of the Metasploitable machine, several critical and high-severity vulnerabilities were identified that threaten the confidentiality, integrity, and availability of the system. The findings included insecure configurations, outdated software, and weak authentication mechanisms. These vulnerabilities expose the system to risks such as unauthorized access, data breaches, and full system compromise.

The most concerning issue was the weak password configured on the VNC server. Nessus detected that the password was set to "password," allowing an unauthenticated attacker to take control of the system remotely. Immediate action is required to secure this service with a strong password or disable VNC if it is not essential.
The assessment also revealed that the target system supports SSL 2.0 and SSL 3.0 protocols, which are outdated and vulnerable to cryptographic attacks such as POODLE and man-in-the-middle exploits. These protocols should be disabled, and the system should be reconfigured to use TLS 1.2 or higher with secure cipher suites to ensure encrypted communication remains secure.

A bind shell backdoor was detected on the system, allowing attackers to execute commands directly without authentication. This represents a severe risk of full system compromise. It is critical to investigate whether the system has been compromised, and, if necessary, reinstall the operating system to restore its integrity.
Additionally, the Apache Tomcat server on the system was found to be outdated, running version 5.5.x, which is no longer maintained by its vendor. Outdated software often contains unpatched vulnerabilities, increasing the risk of exploitation. The Apache Tomcat AJP connector was also identified as vulnerable to the "Ghostcat" exploit, which could allow attackers to read files from the server or achieve remote code execution. Both issues should be addressed by upgrading to a supported version of Apache Tomcat and securing the AJP connector configuration.

Lastly, the system’s cryptographic keys were generated using an OpenSSL library affected by a known bug in Debian's random number generator. This vulnerability renders the keys predictable and compromises secure communications. All cryptographic material, including SSH, SSL, and OpenVPN keys, must be regenerated to ensure they are secure.
In conclusion, remediation efforts should prioritize critical issues such as the weak VNC server password, bind shell backdoor, and outdated SSL protocols. High-priority actions include upgrading Apache Tomcat, addressing the AJP connector vulnerability, and regenerating cryptographic keys. Addressing these vulnerabilities promptly will significantly reduce the system's exposure to potential attacks and enhance its overall security posture.

## Assessment summary
The vulnerability assessment was conducted from the perspective of an unauthenticated user on the internal network. Testing targeted a Metasploitable machine, simulating real-world attack scenarios. Network ranges were identified without prior knowledge of the system’s configurations or operating environment.
### Summary of Findings
The vulnerability assessment uncovered a total of 48 findings, categorized by severity level, that pose significant risks to the target system. Additionally, several informational findings were identified, which, if addressed, could improve the system’s overall security posture. Informational findings are observations highlighting areas for improvement and do not constitute direct security vulnerabilities. The table below summarizes the findings by severity level.
screenshot
Below is a high-level overview of each finding identified during testing. These findings are covered in depth in the Technical Findings Details section of this report.
screenshot

## Technical Findings Details


