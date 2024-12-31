### **GitHub README for Day 4: File Upload Vulnerabilities**  

---

## 📖 **Overview**  
File upload vulnerabilities arise when web applications fail to properly validate or handle user-uploaded files. These vulnerabilities allow attackers to upload malicious files, leading to remote code execution, server compromise, or unauthorized access.  

---

## 🚩 **Key Concepts**  
1. **Unrestricted File Uploads**: Uploading any file without validation.  
2. **Malicious File Uploads**: Executing harmful scripts (e.g., `.php`, `.jsp`).  
3. **Directory Traversal**: Placing files in unintended directories.  
4. **Content-Type Bypass**: Altering MIME types to bypass restrictions.  

---

## 🔍 **How to Identify File Upload Vulnerabilities**  

### **1. Analyze Upload Functionality**  
- Look for endpoints accepting files (`/upload`, `/profile/upload`).  
- Test for allowed file extensions.  

### **2. Common Exploitation Techniques**  
- **Upload Web Shells**: Malicious scripts like `shell.php` or `reverse.jsp`.  
- **Bypass Restrictions**: Modify Content-Type headers or use double extensions (`file.php.jpg`).  
- **Directory Traversal**: Save files in unintended locations (e.g., `../../uploads`).  
- **File Overwriting**: Replace critical files with malicious ones.  

---

## 🛠️ **Testing Tools**  
- **Burp Suite**: Modify file headers and test server responses.  
- **OWASP ZAP**: Automate file upload testing.  
- **Postman**: Craft custom upload requests.  
- **Fuzzing Tools**: Test unexpected file names, extensions, or payloads.  

---

## 🧪 **Example Exploits**  

### **1. PHP Web Shell Upload**  
1. Upload `shell.php`.  
2. Access it via `/uploads/shell.php`.  
3. Execute commands like `ls`, `whoami`, or inject further payloads.  

### **2. Bypass MIME Type Restrictions**  
1. Upload `malicious.exe` with a MIME type of `image/png`.  
2. If accepted, the server processes it, leading to execution.  

### **3. Overwriting Existing Files**  
1. Upload `index.html` to overwrite the homepage.  
2. Alter site functionality or deface the application.  

---

## ✅ **Checklist for File Upload Vulnerabilities**  

### **1. Pre-Test Analysis**  
- [ ] Identify file upload points in the application.  
- [ ] Check allowed file extensions and MIME types.  
- [ ] Test upload limits (e.g., size, type).  

### **2. Testing Techniques**  
- [ ] **File Extension Checks**: Upload files with various extensions (`.php`, `.jsp`, `.exe`).  
- [ ] **Header Manipulation**: Modify headers to bypass restrictions.  
- [ ] **Double Extension Test**: Use filenames like `shell.php.jpg`.  
- [ ] **Directory Traversal**: Attempt uploads to restricted directories (`../../`).  
- [ ] **File Content Validation**: Ensure the server inspects the file’s actual content.  

---

## 🔒 **Mitigation Strategies**  
1. **Whitelist Extensions**: Only allow specific file types (e.g., `.jpg`, `.png`).  
2. **Validate File Content**: Verify the content matches the declared type.  
3. **Restrict Execution Permissions**: Store uploads in directories without execute permissions.  
4. **Rename Files**: Rename uploaded files to prevent directory traversal.  
5. **Implement Content Security Policy (CSP)**: Prevent harmful file execution.  

---

## 🛡️ **Real-World Examples**  
- **Image Upload RCE**: An attacker uploads a PHP shell disguised as an image (`image.php.jpg`) and executes commands.  
- **Server Overload**: Uploading massive files to exhaust storage resources.  

---

## 💻 **Hands-on Practice**  
- Test your skills on platforms like:  
  - OWASP Juice Shop ([https://owasp.org/www-project-juice-shop/](https://owasp.org/www-project-juice-shop/))  
  - DVWA ([http://www.dvwa.co.uk/](http://www.dvwa.co.uk/))  

---

## 🔗 **References**  
- [OWASP File Upload Guidelines](https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload)  
- [Burp Suite Documentation](https://portswigger.net/burp/documentation)  

---
