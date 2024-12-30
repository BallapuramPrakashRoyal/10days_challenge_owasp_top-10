# Day 3: LDAP Injection  

## 📖 Overview  
LDAP Injection is a critical vulnerability that occurs when user input is not properly sanitized and is used to construct LDAP (Lightweight Directory Access Protocol) queries. This allows attackers to manipulate queries and potentially retrieve, modify, or bypass authentication mechanisms.  

---

## 🚩 Key Concepts  

### **What is LDAP Injection?**  
LDAP Injection occurs when:  
- User-supplied input is incorporated into LDAP queries without proper validation.  
- Attackers can exploit this to execute malicious LDAP statements or retrieve unauthorized data.  

### **Why is LDAP Injection Dangerous?**  
1. **Unauthorized Data Access**: Attackers can extract sensitive information from the directory.  
2. **Bypass Authentication**: Gain unauthorized access by modifying authentication queries.  
3. **Privilege Escalation**: Modify user roles or permissions in the directory.  

---

## 🔍 **How to Identify LDAP Injection Vulnerabilities**  

### 🌐 **Common Injection Points**  
1. **Login Forms**: Authentication queries involving username and password.  
2. **Search Filters**: Inputs used to search user directories.  
3. **User Management Systems**: Parameters for user creation, update, or deletion.  

---

## **Step-by-Step Process to Find LDAP Injection Vulnerabilities**  

### **1. Analyze Inputs**  
- Look for fields interacting with directory services (e.g., login forms, search boxes).  

### **2. Test with Malicious Inputs**  
- Inject special characters like `*`, `)`, `(`, and `|`.  
- Observe the behavior of the application for errors or unexpected outputs.  

---

## 🛠️ **Exploitation Steps**  

### **Example 1: Bypassing Authentication**  
- Query before injection:  
  ```ldap
  (&(uid={USER_INPUT})(password={USER_PASSWORD}))
  ```  
- Malicious input for `USER_INPUT`:  
  ```  
  admin)(&)  
  ```  
- Resulting query:  
  ```ldap
  (&(uid=admin)(&)(password={USER_PASSWORD}))
  ```  
  This allows bypassing authentication if the query evaluates to true.  

### **Example 2: Extracting Data**  
- Query before injection:  
  ```ldap
  (|(uid={USER_INPUT})(mail={USER_INPUT}))
  ```  
- Malicious input:  
  ```  
  *  
  ```  
- Resulting query:  
  ```ldap
  (|(uid=*)(mail=*))
  ```  
  This retrieves all records from the directory.  

### **Example 3: Testing for Errors**  
- Input malformed data to identify potential vulnerabilities:  
  ```  
  )(|(objectClass=*))  
  ```  
  - Errors or unexpected behavior indicate potential injection points.  

---

## **LDAP Injection Vulnerability Checklist**  

### **1. Reconnaissance**  
- [ ] Identify inputs interacting with LDAP queries.  
- [ ] Check for error messages, unexpected results, or behavioral anomalies.  

### **2. Testing**  
- [ ] Inject special characters and observe application responses.  
- [ ] Use payloads to manipulate query logic:  
  - `admin)(objectClass=*)`  
  - `admin*`  

### **3. Verification**  
- [ ] Confirm successful data extraction, authentication bypass, or privilege escalation.  

---

## 🔒 **Mitigation Strategies**  

1. **Parameterized Queries**: Use safe methods to construct LDAP queries (e.g., LDAP prepared statements).  
2. **Input Validation**:  
   - Allow only expected input formats (e.g., alphanumeric characters).  
   - Reject or escape special characters like `*`, `)`, `(`, and `|`.  
3. **Escape User Inputs**: Use built-in functions to sanitize user input (e.g., Java’s `StringEscapeUtils.escapeLDAP()` from Apache Commons).  
4. **Least Privilege Principle**: Restrict LDAP user permissions to limit damage from exploitation.  
5. **Logging and Monitoring**: Detect anomalous LDAP activity.  

---

## 💻 **Hands-on Practice**  
- Test LDAP injection on the following platforms:  
  - [OWASP Mutillidae](http://www.owasp.org/index.php/OWASP_Mutillidae_2_Project)  
  - [Web Security Academy](https://portswigger.net/web-security/authentication)  

---

## 🛠️ **Resources**  
- [OWASP LDAP Injection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/LDAP_Injection_Prevention_Cheat_Sheet.html)  
- [LDAP Syntax and Operations](https://ldap.com/)
