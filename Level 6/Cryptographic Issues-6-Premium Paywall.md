# **Cryptographic Issues-6-Premium Paywall**

## 1. Methodology

**Step 1 – Finding the Encryption Key**

- Use a tool like goBuster to discover the /encryptionkeys directory.

**Step 2 – Downloading the Key**

- Download the premium.key file containing the AES-128 key.

**Step 3 – Finding the Encrypted Data**

- Analyze the source code to find the encrypted comments.

**Step 4 – Decryption**

- Use OpenSSL to decrypt the base64 string with the key.

**Step 5 – Accessing the Hidden URL**

- Navigate to the decrypted URL to bypass the paywall. (this/page/is/hidden/behind/an/incredibly/high/paywall/that/could/only/be/unlocked/by/sending/1btc/to/us)

**Step 6 – Validation**

- The challenge is validated by accessing the hidden page.

## Techniques Used:

- Cryptographic Issues
- Sensitive Data Exposure

## Tools Used:

- goBuster
- OpenSSL

---

## 2. Vulnerabilities

**Vulnerability:**

- Cryptographic Issues
- Sensitive Data Exposure

**Affected Component:**

- Encrypted /encryptionkeys directory and comments

**Severity:**

- **High**

---

## 3. Risks

- Exposure of encryption keys and URLs hidden behind paywalls.

- Business impact: loss of user trust, reputational damage, loss of revenue: users have access to exclusive content without any cost.

---

## 4. Actions

**Risk Mitigation**

- Secure sensitive directories and avoid storing keys in plaintext.

**Remediation Fix**

- Use managed keys and encrypt sensitive data properly.

**Best Practices**

- OWASP Cryptographic Failures.

--

**Evidence**

![premium_paywall](./image/premium_paywall.png)