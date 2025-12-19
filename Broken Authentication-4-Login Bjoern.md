**_Broken Authentication – Level 4 – Login Bjoern_**

## 1. Methodology

**Step 1 – Gathering Information on the User Bjoern**

- Go to the **All Products** page and explore.
- Look for the product:  
  **OWASP Snakes and Ladders – Web Application**.
- Open the **Reviews** section.
- Copy the email address shown in a comment left by Bjoern.  
  Example (commonly found):  
  **bjoern.kimminich@owasp.org**

**Step 2 – Logout**

- Log out from the current account to start the password reset process.

**Step 3 – “Forgot Password” Procedure**

- Go to the **Login** page.
- Click on **“Forgot your password?”**
- Enter the email address found in the product review.

**Step 4 – External OSINT to Retrieve the Secret Answer**

- Use Google to search for: **Bjoern Kimminich**.
- Open the YouTube video:  
  **“BeNeLux Day 2018: Juice Shop – OWASP’s Most Broken Flagship – Björn Kimminich”**
- In the video, Bjoern demonstrates the password reset page.
- The **secret question** shown is:  
  **“What is the name of your pet?”**
- The **answer** used by Bjoern during the demo is:  
  **Zaya**

**Step 5 – Password Reset**

- Return to the **Forgot Password** page.
- Enter:
  - Email: (the one found earlier)
  - Secret answer: `Zaya`
- The site allows setting a **new password** for Bjoern’s account.

**Step 6 – Login with New Credentials**

- Go to the **Login** page.
- Enter Bjoern’s email and the new password.
- Login succeeds -> challenge validated

---

## Techniques Used

- OSINT-based Account Takeover via Weak Password Recovery
- Authentication Bypass through Password Reset Abuse

## Tools Used

- Web Browser
- OSINT (Google, YouTube Search)

---

## 2. Vulnerabilities

**Vulnerability name:**

- Broken Authentication
- Weak Security Questions / OSINT Leakage
- Account Takeover via Password Reset

**Affected Component:**

- Password Reset Mechanism (Secret Questions)

**Severity:**

- **High** = allows complete user account compromise.

---

## 3. Risks

- Full compromise of Bjoern’s account.
- Unauthorized access to personal data.
- Possible privilege escalation if the account has elevated rights.
- Exposure due to publicly available OSINT data.
- **Business impact:** data exposure, loss of user trust, reputational damage.

---

## 4. Actions

**Risk Mitigation**

- Remove static secret questions.
- Replace them with **email-based reset links using unique tokens**.
- Limit the number of secret question attempts.

**Remediation Fix**

- Use signed tokens with short expiration time.
- Require MFA for sensitive password resets.
- Prevent the use of publicly known or guessable information.

**Example:** secure server-side password reset check

```js
if (!isValidResetToken(token)) {
  return res.status(403).json({ error: "Invalid or expired token" });
}
```

**Best Practices**

- Always prefer secure reset mechanisms (token, MFA).
- Avoid static or predictable security questions.
- Conduct OSINT audits to identify publicly exposed information.

---
