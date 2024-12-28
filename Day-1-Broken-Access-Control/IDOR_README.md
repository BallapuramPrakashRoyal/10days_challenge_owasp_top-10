
# Day 1: IDOR (Insecure Direct Object References)  

## 📖 Overview  
IDOR (Insecure Direct Object References) is a type of **Broken Access Control** vulnerability. It occurs when an application exposes references to internal implementation objects (e.g., database records, files, or keys) without proper access control checks.  

## 🚩 Key Concepts 
- **What is IDOR?**: Allows attackers to access or manipulate resources they are not authorized to.  
- **Examples of Vulnerable Endpoints**:  
  - User profiles (`/user/123`)  
  - Files or documents (`/files/invoice_456.pdf`)  
  - API calls (`/api/orders?order_id=789`)  

# 🔍 **How to Identify IDOR**

## 🌐 **Commonly Affected Websites**  

IDOR vulnerabilities are more likely to be found in web applications that involve:  

1. **E-commerce Platforms**:  
   - Order details or invoices (`/order/123`).  
   - Product inventory or pricing data (`/product/456`).  

2. **Social Media Platforms**:  
   - User profiles (`/profile/789`).  
   - Private messages or chats (`/messages/123`).  

3. **Content Management Systems (CMS)**:  
   - Files or media uploads (`/uploads/file_456.jpg`).  
   - Article drafts or private posts (`/posts/draft_123`).  

4. **Banking and Financial Applications**:  
   - Transaction histories (`/transaction/789`).  
   - Account statements (`/accounts/123`).  

5. **Health and Education Portals**:  
   - Medical records (`/records/patient_456`).  
   - Exam results or certificates (`/results/789`).  

6. **API-Driven Applications**:  
   - Exposed APIs without robust authorization checks (e.g., `/api/user_data?id=123`).  

7. **File-Sharing Platforms**:  
   - Shared files or folders (`/files/document_456.pdf`).


# *step-by-step process to find idor vulnerabilities*


### **1. Analyzing Endpoints**  
- Look for endpoints exposing object identifiers (e.g., `id`, `user_id`, `file_id`).  
- Check GET, POST, PUT, DELETE, and API request parameters.  

### **2. Testing for IDOR**  
- Modify the identifier (e.g., changing `/user/123` to `/user/124`).  
- Observe whether the application prevents unauthorized access.  

### **3. Tools to Use** 
- **Burp Suite**: Proxy and modify requests.  
- **Postman**: Test API endpoints.  
- **OWASP ZAP**: Automate parameter tampering.  

## 🛠️ *Exploitation Steps*  

### Example 1: User Profile Access  
1. Navigate to `/profile?user_id=123`.  
2. Change `user_id=123` to `user_id=124`.  
3. If you access another user's profile, it's a confirmed IDOR vulnerability.  

### Example 2: Unauthorized File Download  
1. Download a file from `/files/document_123.pdf`.  
2. Change `document_123.pdf` to `document_124.pdf`.  
3. If you can access restricted files, it's an IDOR.


## **IDOR Vulnerability Checklist**  

### **1. Reconnaissance**  
- [ ] **Identify Endpoints**: Look for URLs and API endpoints that contain object references (e.g., `id=123`, `user_id=456`).  
- [ ] **Analyze Parameters**: Focus on query strings, POST data, headers, and JSON bodies for identifiable parameters (`id`, `file_id`, etc.).  
- [ ] **Understand Roles**: Determine different user roles (e.g., admin, regular user, guest) in the application.  
- [ ] **Map Functionality**: List all operations users can perform (e.g., view, edit, delete resources).  

### **2. Testing**  
#### **A. General Steps**  
- [ ] **Modify Identifiers**: Change object references (e.g., increment or decrement `id` values).  
- [ ] **Replay Requests**: Repeat requests with modified parameters to check for unauthorized access.  
- [ ] **Test All HTTP Methods**: Try GET, POST, PUT, DELETE requests for the same endpoint.  

#### **B. Specific Tests**  
- [ ] **User Profiles**: Attempt to view/edit other users’ profiles by changing `user_id`.  
- [ ] **Files/Documents**: Try accessing unauthorized files (e.g., `/files/file_123.pdf`).  
- [ ] **Transactions**: Modify transaction or order IDs (e.g., `/transactions/456`).  
- [ ] **APIs**: Test API endpoints for IDOR vulnerabilities using tools like Postman or Burp Suite.  
- [ ] **Mass Assignment**: Include unexpected object references in POST/PUT requests.  

### **3. Tools to Assist**  
- [ ] **Burp Suite**: Use the Repeater and Intruder tools to test endpoints systematically.  
- [ ] **Postman**: Send API requests and manipulate parameters manually.  
- [ ] **OWASP ZAP**: Automate testing for parameter tampering.  
- [ ] **Fuzzers**: Use parameter fuzzing tools to discover hidden references.  

### **4. Observation and Verification**  
- [ ] **Check Responses**: Look for data or access that belongs to other users.  
- [ ] **Inspect Error Messages**: Identify useful information in server error responses.  
- [ ] **Log Changes**: Check if unauthorized changes persist (e.g., profile updates, file deletions).  

### **5. Documentation**  
- [ ] **Record Steps**: Document how you identified the vulnerability, including requests and responses.  
- [ ] **Provide Impact Analysis**: Describe the potential damage if exploited (e.g., data breach, privilege escalation).  
- [ ] **Suggest Fixes**: Recommend secure coding practices to prevent IDOR (e.g., object-level access checks).  

### **6. Best Practices**  
- [ ] **Role Testing**: Test with multiple user roles (admin, regular user, guest) to identify access control flaws.  
- [ ] **Boundary Testing**: Test edge cases (e.g., IDs like `0`, `-1`, or invalid IDs).  
- [ ] **Session Management**: Use different accounts and sessions to confirm unauthorized access.  
- [ ] **Test Redirects**: Check for IDOR in redirected URLs or hidden endpoints.

## **Bonus Tips**  
- [ ] **Collaborate**: If possible, test with teammates to cover blind spots.  
- [ ] **Use IDOR Labs**: Practice on platforms like PortSwigger Academy or OWASP Juice Shop.  
- [ ] **Monitor Logs**: Look for anomalies during testing to identify hidden flaws.  

By following this checklist, you’ll systematically uncover IDOR vulnerabilities and ensure thorough coverage during your tests.


## 🔒 **Mitigation Strategies**  
1. **Enforce Access Control**: Implement role-based or object-level access controls.  
2. **Avoid Predictable Identifiers**: Use random UUIDs instead of sequential IDs.  
3. **Validate User Permissions**: Ensure each request checks whether the user has permission to access the resource.  
4. **Log and Monitor**: Detect and respond to unauthorized access attempts.  


## 🛡️ **Real-World Examples**  
- **Facebook Bug**: Allowed attackers to view private photos by changing `photo_id`.  
- **E-commerce Site**: Unauthorized users could view others’ invoices by modifying `order_id`.  


## 💻 **Hands-on Practice**  
- Try IDOR labs on:  
  - PortSwigger Web Security Academy [ https://portswigger.net/web-security/access-control/idor ]  
  - OWASP Juice Shop [https://owasp.org/www-project-juice-shop/]  


## 🛠️ **Resources**  
- [OWASP Top 10: Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)  
- [Burp Suite Guide](https://portswigger.net/burp/documentation)  

