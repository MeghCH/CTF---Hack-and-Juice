# **Sensitive Data Exposure-5-Misplaced signature file**

## 1. Methodology

**Step 1 – Preparation**

- Use Burp Suite to intercept and modify HTTP requests.

**Step 2 – Access to /ftp directory**

- Navigate to the /ftp/ directory to access suspicious_errors.yml file.

**Step 3 – Bypass extension restriction**

- Add %2500 (double encoding of null byte) to mask the real extension (.yml) behind an allowed extension (.md).

**Step 4 – Download the file**

- Send the modified request: GET /ftp/suspicious_errors.yml%2500.md HTTP/1.1

**Step 5 – Validation**

- The suspicious_errors.yml file is downloaded, validating the challenge.

## Techniques used:

- File Discovery
- Null Byte Injection
- Double URL Encoding

## Tools used :

- Burp Suite

---

## 2. Vulnerabilities

**Vulnerability:**

- Improper Input Validation
- Sensitive Data Exposure

**Affected component:**

- File extension filter in /ftp/

**Severity:**

- **High**

---

## 3. Risks

- Exposure of sensitive files like detection rules (suspicious_errors.yml).

-Business impact: user trust loss, reputational damage.

---

## 4. Actions

**Risk Mitigation**

- Implement strict extension validation without relying on decoding.

**Remediation Fix**

- Block special characters like %00 and %2500 in filenames.

**Best Practices**

- OWASP Improper Input Validation.

---

## 5. Proofs


![Misplaced Signature File](./image/Misplaced_Signature_File.png)
