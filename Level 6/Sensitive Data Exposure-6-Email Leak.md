# **Sensitive Data Exposure-6-Email Leak**

## 1. Methodology

**Step 1 – Preparation**

- Use Burp Suite and FoxyProxy to intercept requests.

**Step 2 – API access**

- Navigate to the /rest/user/whoami endpoint with a callback parameter.

**Step 3 – Callback exploitation**

- Use a callback like anyname to retrieve user information.

**Step 4 – Data observation**

- The API returns information of logged-in users, including email.

**Step 5 – Validation**

- The challenge is validated by accessing sensitive data cross-domain.

## Techniques used:

- Sensitive Data Exposure
- API Callback Exploitation

## Tools used :

- Burp Suite
- FoxyProxy

---

## 2. Vulnerabilities

**Vulnerability:**

- Sensitive Data Exposure

**Affected component:**

- Endpoint /rest/user/whoami

**Severity:**

- **High**

---

## 3. Risks

- Exposure of emails and information of logged-in users via unsecured API calls.

-Business impact: user trust loss,reputational damage,Loss of confidential data can lead to marketing problems.

---

## 4. Actions

**Risk Mitigation**

- Implement strict access controls on API endpoints.

**Remediation Fix**

- Disable unauthorized callbacks and add authentication.

**Best Practices**

- OWASP Sensitive Data Exposure.

---

**Evidences**

![Email_leak](./image/email_leak.png)
