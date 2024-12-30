# Day 3: SQL Injection (SQLi)  

## 📖 Overview  
SQL Injection (SQLi) is a critical vulnerability that allows attackers to interfere with the queries an application makes to its database. By injecting malicious SQL statements, attackers can manipulate or gain unauthorized access to data, bypass authentication, or even compromise the entire database server.  

---

## 🚩 Key Concepts  

### **What is SQL Injection?**  
SQL Injection occurs when:  
- User inputs are improperly validated or sanitized.  
- SQL queries dynamically include untrusted inputs, allowing manipulation of database operations.  

### **Types of SQL Injection**  
1. **Error-Based SQLi**: Exploits database error messages to extract information.  
2. **Union-Based SQLi**: Uses the `UNION` SQL operator to fetch data from other tables.  
3. **Boolean-Based Blind SQLi**: Infers information by observing application behavior for true/false conditions.  
4. **Time-Based Blind SQLi**: Uses SQL functions like `SLEEP()` to infer data by measuring response delays.  
5. **Out-of-Band SQLi**: Relies on external communication, such as DNS lookups or HTTP requests, to exfiltrate data.  

---

## 🔍 **How to Identify SQL Injection**  

### 🌐 **Common Injection Points**  
1. **Login Forms**: Bypass authentication using `' OR 1=1 --` in username or password fields.  
2. **Search Bars**: Inject payloads like `1' UNION SELECT NULL, version() --` to test for data extraction.  
3. **URL Parameters**: Alter query strings (e.g., `/product?id=1`) with SQL payloads like `1' OR '1'='1`.  
4. **HTTP Headers**: Include payloads in cookies, `User-Agent`, or `Referer` headers.  
5. **API Endpoints**: Exploit dynamic queries in backend APIs.  

---

## **Step-by-Step Process to Find SQLi Vulnerabilities**  

### **1. Analyze Inputs**  
- Identify areas where user inputs influence database queries.  
- Look for parameters in URLs, forms, or API calls.  

### **2. Test for Injection**  
- Use basic payloads to check for syntax errors (e.g., `'`, `"`, `;--`).  
- Escalate with advanced payloads for data extraction (`' UNION SELECT NULL, version() --`).  

### **3. Observe Responses**  
- Look for SQL error messages or unexpected application behavior.  
- Detect anomalies like delays (time-based) or different responses for true/false queries (boolean-based).  

---

## 🛠️ **Exploitation Steps**  

### **Example 1: Login Form Bypass**  
1. Enter `' OR 1=1 --` in the username field.  
2. Leave the password field blank.  
3. If login is successful, the application is vulnerable.  

### **Example 2: Data Extraction via Union-Based SQLi**  
1. Test the number of columns:  
   - Payload: `1' UNION SELECT NULL, NULL --`  
2. Extract database details:  
   - Payload: `1' UNION SELECT NULL, version() --`  

### **Example 3: Time-Based Blind SQLi**  
1. Inject payload: `1' AND IF(1=1, SLEEP(5), 0) --`  
2. Observe delay to confirm vulnerability.  

---

## **SQLi Vulnerability Checklist**  

### **1. Reconnaissance**  
- [ ] Identify dynamic inputs influencing SQL queries.  
- [ ] Analyze forms, search bars, and URL parameters for vulnerabilities.  

### **2. Testing**  
- [ ] Test with special characters (`'`, `"`, `;--`) to check for errors.  
- [ ] Use union-based payloads to extract data (`' UNION SELECT ...`).  
- [ ] Perform boolean or time-based blind testing if no direct errors are observed.  

### **3. Tools to Assist**  
- [ ] **SQLMap**: Automates SQL injection detection and exploitation.  
- [ ] **Burp Suite**: Intercept and modify requests to test for SQLi.  
- [ ] **NoSQLMap**: Use for injection vulnerabilities in NoSQL databases.  

### **4. Verification**  
- [ ] Validate extracted data matches database content.  
- [ ] Ensure payloads work across various endpoints and parameters.  

---

## 🔒 **Mitigation Strategies**  

1. **Use Parameterized Queries**: Ensure all inputs are parameterized (e.g., `Prepared Statements` in SQL).  
2. **Input Validation**: Sanitize and validate all user inputs.  
3. **Least Privilege Principle**: Limit database permissions to reduce impact.  
4. **Error Handling**: Hide detailed database error messages.  
5. **Web Application Firewalls (WAFs)**: Deploy WAFs to detect and block SQL injection attempts.  

---

## 💻 **Hands-on Practice**  
- Try SQLi labs on:  
  - PortSwigger Web Security Academy [https://portswigger.net/web-security/sql-injection]  
  - OWASP Juice Shop [https://owasp.org/www-project-juice-shop/]  

---

## 🛠️ **Resources**  
- [OWASP Top 10: Injection](https://owasp.org/Top10/A03_2021-Injection/)  
- [SQLMap Documentation](https://sqlmap.org/)  

By understanding and testing for SQL Injection, you can identify vulnerabilities, understand their risks, and help secure applications from this critical threat.  --Thank you all
