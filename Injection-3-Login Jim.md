**_Injection – Level 3 – Login Jim_**

## 1. Methodology

**Step 1 – Find Jim’s Email**

- As in most Juice Shop instances, Jim’s email is:

`jim@juice-sh.op`

**Step 2 – Try a Normal Login**

- Go to the **Login** page.
- Enter:  
  Email: `jim@juice-sh.op`  
  Password: `1234`
- Result: failed -> password is incorrect.

**Step 3 – Attempt an SQL Injection in the Email Field**

- Modify the email by adding an SQL comment:

`jim@juice-sh.op'--`

- The `--` comments out the rest of the SQL query on the server side, bypassing password verification.

**Step 4 – Validate the Login**

- Enter any password.
- Click **Login**.
- The login **succeeds**, as the SQL condition becomes true thanks to the comment.

**Result:**  
-> Successful login **without knowing the password**, through a **basic SQL Injection**.  
-> Challenge validated

---

## Technique Used

- SQL Injection
- Comment-based injection (`--`)

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
- Backend SQL query handling (email field)

**Severity:**

- **Critical**

---

## 3. Risks

- Unauthorized login to user accounts.
- Possible access to sensitive or admin accounts.
- Potential exfiltration of user data.
- Full compromise of the authentication system.
- **Business impact:** Legal risks (GDPR), reputational damage.

---

## 4. Actions

**Risk Mitigation:**

- Never concatenate user input in SQL queries.
- Use prepared statements.
- Enforce strict validation on email formats.

**Remediation Fixes:**

- Sanitize dangerous characters (`'`, `"`, `--`, `;`).
- Apply server-side whitelisting.
- Block SQL comments in user input fields.

**Example:** typical fix against SQL Injection

```js
const query = "SELECT * FROM users WHERE email = ? AND password = ?";
db.execute(query, [email, password]);
```

**Best Security Practices:**

- Implement a Web Application Firewall (WAF) to detect SQL signatures.
- Perform automated testing for injection vulnerabilities.
- Enforce multi-factor authentication (MFA).

---

## 5. Evidence

**References on SQL Injection:**

- https://www.vaadata.com/blog/fr/injections-sql-principes-impacts-exploitations-bonnes-pratiques-securite/

- https://portswigger.net/web-security/sql-injection
