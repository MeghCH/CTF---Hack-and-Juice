**_Injection – Level 3 – Login Bender (SQL Injection)_**

## 1. Methodology

**Step 1 – Find Bender’s Email**

- On Juice Shop, user emails often follow the same pattern.
- Bender’s email is:

`bender@juice-sh.op`

**Step 2 – Try a Normal Login**

- Go to the **Login** page.
- Enter:  
  Email: `bender@juice-sh.op`  
  Password: `1234` or another simple password.
- Result: failure -> the password is incorrect.

**Step 3 – Attempt an SQL Injection**

As in similar challenges (Login Jim), inject an SQL comment to bypass password verification.

- Modify the email as follows:

`bender@juice-sh.op'--`

This payload closes the SQL string and comments out the rest of the query, completely bypassing the password check.

**Step 4 – Login**

- Enter any password.
- Click **Login**.
- The login **succeeds immediately** thanks to the SQL Injection.

**Result:**  
-> Bender’s account is accessible **without knowing the password**.  
-> Challenge validated

---

## Techniques Used

- SQL Injection

## Tools Used

- Web Browser

---

## 2. Vulnerabilities

**Vulnerability name:**

- SQL Injection
- Authentication Bypass
- Improper Input Validation

**Affected Component:**

- Login API endpoint
- Back-end SQL query using the email field

**Severity:**

- **Critical**

---

## 3. Risks

- Unauthorized access to user accounts.
- High risk of accessing privileged accounts.
- Possible privilege escalation.
- **Business impact:** User data compromise + major impact on overall application security.

---

## 4. Actions

**Risk Mitigation:**

- Never concatenate user input into SQL queries.
- Use prepared statements.
- Strictly validate user input (email format).

**Remediation Fixes:**

- Escape dangerous characters (`'`, `"`, `--`, `;`).
- Use a whitelist for accepted input formats.
- Implement strong access control on the Login endpoint.

**Example:** typical fix against SQL Injection

```js
const query = "SELECT * FROM users WHERE email = ? AND password = ?";
db.execute(query, [email, password]);
```

**Best Security Practices:**

- Add multi-factor authentication (MFA).
- Deploy a Web Application Firewall (WAF) to detect SQL injection attempts.
- Perform regular penetration tests for injection vulnerabilities.

---

## 5. Evidence

**References on SQL Injection:**

- https://www.vaadata.com/blog/fr/injections-sql-principes-impacts-exploitations-bonnes-pratiques-securite/

- https://portswigger.net/web-security/sql-injection
