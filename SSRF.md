# 🎯 Server-Side Request Forgery (SSRF)  
*A vulnerability where attackers force a server to make requests to unintended locations, often leading to sensitive data exposure or internal network access.*

---

## 📖 Table of Contents  
- [📜 Definition](#-definition)  
- [🔍 How SSRF Works](#-how-ssrf-works)  
- [💥 Impact](#-impact)  
- [🎯 Common SSRF Scenarios](#-common-ssrf-scenarios)  
- [🔬 Testing Methodology](#-testing-methodology)  
- [📌 Payloads & Examples](#-payloads--examples)  
- [🛠️ Chaining SSRF with Other Bugs](#️-chaining-ssrf-with-other-bugs)  
- [📚 Resources](#-resources)  

---

## 📜 Definition  
SSRF (Server-Side Request Forgery) occurs when an attacker manipulates a server into making requests to internal or external resources. This can lead to:  
- **Sensitive data exposure** (e.g., local files, internal APIs).  
- **Internal network reconnaissance**.  
- **Privilege escalation** or **lateral movement**.  

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
   - The attacker replaces the URL with an internal resource or malicious endpoint:  
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
- **Privilege Escalation**: Accessing admin panels or internal services.  
- **Chaining**: Combining SSRF with other vulnerabilities (e.g., XSS, RCE).  

---

## 🎯 Common SSRF Scenarios  

### 🌐 **1. URL Fetching Functionality**  
- **File Uploads**: Remote file imports or uploads.  
- **Image/Media Previews**: Generating thumbnails from external URLs.  
- **PDF Generation**: Converting web pages to PDFs.  

### 📨 **2. Webhooks & Integrations**  
- **Webhooks**: User-controlled callback URLs.  
- **Third-Party APIs**: Fetching data from external APIs.  

### 📁 **3. File Retrieval & Proxying**  
- **File Downloads**: Downloading files from user-provided URLs.  
- **HTTP Proxies**: Proxying requests to external sites.  

### 📥 **4. Import/Export Features**  
- **Data Imports**: Importing CSV, XML, or JSON from URLs.  
- **Feeds & Syndication**: RSS/Atom feeds or web scraping.  

### 🛠️ **5. API Interactions**  
- **GraphQL/REST APIs**: URL parameters in API requests.  
- **Cloud Metadata**: Accessing AWS/GCP/Azure metadata endpoints.  

### 🔐 **6. Admin Panels & Internal Tools**  
- **Admin Features**: Fetching URLs for previews or testing.  
- **Monitoring Tools**: Pinging or fetching URLs for server checks.  

### 🚦 **7. Uncommon Protocols**  
- **Non-HTTP Protocols**: `file://`, `gopher://`, `ftp://`, `dict://`.  
- **Email Services**: `mailto:` and SMTP interactions.  

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