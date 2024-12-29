### **GitHub README for Day 2: Security Misconfigurations**  

**Day 2: Diving Deep into Security Misconfigurations**  

---

#### **Overview**  
Security Misconfigurations occur when systems or applications are not securely configured, leaving them vulnerable to exploitation. These vulnerabilities often result from improper server setups, unprotected files, or weak configurations.

---

#### **Common Vulnerabilities**  
- **Default Credentials:** Admin:admin or root:password still in use.  
- **Exposed Files:** Sensitive files like `.env`, `.git`, `backup.zip` accessible publicly.  
- **Unrestricted HTTP Methods:** PUT, DELETE enabled without need.  
- **Directory Listing Enabled:** Attackers can view files in web directories.  
- **Misconfigured CORS:** Allows unauthorized cross-origin requests.  
- **Error Messages Leaking Information:** Detailed errors exposing sensitive data.  

---

#### **Where They’re Found**  
- Web servers and application platforms (e.g., Apache, Nginx).  
- Admin panels, APIs, and login pages.  
- File servers and backup endpoints.  

---

#### **Checklist for Finding Security Misconfigurations**  

1. [ ] Check for **publicly accessible sensitive files** using tools like Dirsearch or manually.  
2. [ ] Test **CORS policies** with Burp Suite to ensure they don’t allow unauthorized domains.  
3. [ ] Verify **enabled HTTP methods** with tools like Nikto or cURL.  
4. [ ] Search for **default credentials** on login portals and admin panels.  
5. [ ] Look for **detailed error messages** during testing.  
6. [ ] Test for **directory listings** by accessing `/` and common directory paths.  

---

#### **Tools Used**  

- Dirsearch  
- Burp Suite  
- Nikto  
- cURL  
- Gobuster  

---

#### **References**

- [OWASP Security Misconfiguration Details](https://owasp.org/www-project-top-ten/2021/A05_2021-Security_Misconfiguration/)  
- [CORS Exploitation Guide](https://portswigger.net/web-security/cors)  

---
