# Day 10: Server-Side Request Forgery (SSRF)

## 📚 Overview
Server-Side Request Forgery (SSRF) is a critical vulnerability where attackers can manipulate server-side applications to send malicious requests to unintended destinations. This can result in accessing internal services, stealing sensitive data, or even compromising the entire system.

---

## 🔍 Understanding SSRF
- **What Happens?**  
  A server processes unvalidated user input to make HTTP requests to internal or external resources, potentially exposing sensitive systems.  
- **Attack Goals**:  
  - Access internal infrastructure.  
  - Extract sensitive data (e.g., AWS metadata).  
  - Perform internal scans.  
  - Exploit secondary vulnerabilities.  

---

## 🚩 Real-World Impacts
- **Capital One Breach (2019)**: SSRF in AWS Metadata Service caused a massive data leak.  
- **GitHub Enterprise SSRF**: Attackers used SSRF to scan internal GitHub Enterprise instances.  

---

## 🛠️ Steps to Identify SSRF
### 1️⃣ Locate Vulnerable Endpoints  
- Parameters accepting URLs: `url=`, `link=`, `callback=`.
- Features like PDF generation, webhooks, or file uploads.

### 2️⃣ Test with Malicious URLs  
- Internal IPs: `http://127.0.0.1`, `http://192.168.x.x`.  
- Metadata services: `http://169.254.169.254`.  
- External OOB tools: Burp Collaborator or Interactsh.  

### 3️⃣ Observe Responses  
- Access denied errors indicate internal resource attempts.  
- Metadata responses often confirm SSRF vulnerabilities.

---

## 🔒 Mitigation Strategies
### ✅ Input Validation  
- Whitelist allowed domains and protocols.  
- Reject private IP ranges and localhost.

### ✅ Network Restrictions  
- Restrict server access to internal systems.  
- Use firewalls and segmentation to block sensitive resources.

### ✅ Secure Cloud Configurations  
- Disable metadata service if unnecessary.  
- Use enhanced metadata security (e.g., AWS IMDSv2).

### ✅ Monitoring and Alerts  
- Implement comprehensive logging of server requests.  
- Monitor for anomalies in outbound traffic.

---

## 🧰 Tools for Testing SSRF
1. **Burp Suite**: Intercept and manipulate HTTP requests.  
2. **SSRFmap**: Automates payload delivery for SSRF testing.  
3. **Collaborator/Interactsh**: Detect OOB interactions.  

---

## 🌟 Practical Labs
- [PortSwigger Academy SSRF Labs](https://portswigger.net/web-security/ssrf)  
- [Hack The Box](https://www.hackthebox.com): Practice SSRF challenges.  
- [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/): Test SSRF in a safe environment.

---

## 🛡️ Learn More
- [OWASP SSRF Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html)  
- [PortSwigger SSRF Guide](https://portswigger.net/web-security/ssrf)  

---

## 🤝 Contribute
Help make this guide better! Open an issue or submit a pull request.  

🌐 **Follow for More**: Stay updated with my GitHub for more cybersecurity resources and projects!  
```
