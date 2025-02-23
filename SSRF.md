# 🎯 Server-Side Request Forgery (SSRF)  
*A vulnerability where attackers force a server to make requests to unintended locations.*

---

## 📜 What is SSRF?  
SSRF (Server-Side Request Forgery) allows attackers to make the server-side application send requests to unintended locations, such as internal systems or external servers. This can lead to:  
- Retrieving sensitive data (e.g., local files, internal APIs).  
- Internal network reconnaissance.  
- Escalating privileges or chaining with other vulnerabilities.  

---

## 🔍 How SSRF Works  
1. **Vulnerable Endpoint**:  
   - A server accepts user input (e.g., a URL) and makes a request to that input.  
   - Example:  
     ```http
     GET /fetch?url=http://example.com HTTP/1.1
     Host: vulnerable.com
     ```  

2. **Exploitation**:  
   - Replace the URL with an internal resource or malicious endpoint:  
     ```http
     GET /fetch?url=http://localhost:8080/admin HTTP/1.1
     Host: vulnerable.com
     ```  

3. **Server Response**:  
   - The server retrieves the unintended resource, exposing sensitive data or performing unintended actions.  

---

## 💥 Impact  
- **Data Exposure**: Access to internal files, databases, or APIs.  
- **Reconnaissance**: Mapping internal networks or cloud metadata.  
- **Chaining**: Combining SSRF with other vulnerabilities (e.g., XSS, RCE).  

---

## 🎯 Common SSRF Scenarios  
1. **URL Fetching**:  
   - File uploads, image previews, PDF generation.  
2. **Webhooks & Integrations**:  
   - User-controlled callback URLs.  
3. **File Retrieval & Proxying**:  
   - Downloading files or proxying requests.  
4. **Import/Export Features**:  
   - Importing data from URLs (e.g., CSV, XML).  
5. **API Interactions**:  
   - URL parameters in GraphQL/REST APIs.  
6. **Admin Panels & Internal Tools**:  
   - Fetching URLs for previews or testing.  
7. **Uncommon Protocols**:  
   - `file://`, `gopher://`, `ftp://`, `dict://`.  

---

## 🔬 Testing Methodology  
1. **Identify Input Points**:  
   - Look for endpoints that accept URLs (e.g., file uploads, webhooks).  

2. **Test for SSRF**:  
   - Replace the URL with internal resources:  
     ```http
     GET /fetch?url=http://localhost:8080/admin HTTP/1.1
     Host: vulnerable.com
     ```  
   - Use tools like **Burp Collaborator** or **Interactsh** for out-of-band testing.  

3. **Escalate**:  
   - Chain SSRF with other vulnerabilities (e.g., XSS, RCE).  

---

## 📌 Payloads & Examples  

### Internal Scanning  
```http
http://localhost:8000/admin
http://127.0.0.1:3306 (MySQL)
http://169.254.169.254/latest/meta-data (AWS Metadata)
http://169.254.169.254/latest/meta-data/iam/security-credentials/ (Cloud Metadata)
http://internal-api.local/api/v1/users (Internal APIs)
