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
