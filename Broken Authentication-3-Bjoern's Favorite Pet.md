**_Broken Authentication – Level 3 – Bjoern's Favorite Pet_**

## 1. Methodology

**Step 1 – Target Research (Internal OSINT)**

- Log in to the Juice Shop website.
- Browse the available **products** to identify possible user information.
- In the product _OWASP Snakes and Ladders – Web Applications_, open the **reviews** section.
- Copy the visible email from a comment:  
  -> Example: bjoern.kimminich@owasp.org

**Step 2 – Logout and Start the Recovery Procedure**

- Log out from the site.
- Go to the **Login** page.
- Click **"Forgot your password?"**
- Enter the email address found in the reviews.

**Step 3 – External OSINT (Google / YouTube)**

- Search online for **“Bjoern Kimminich”**.
- Among the results, open the video:  
  **BeNeLux Day 2018: Juice Shop – OWASP's Most Broken Flagship – Björn Kimminich**
- Watch the part where Björn demonstrates the password recovery page for Juice Shop.
- The video shows the **security question** and its **answer**.

**Step 4 – Extraction of Security Information**  
In the demonstration, the displayed information is:

- **Security Question:** “What is your pet’s name?”  
- **Answer:** “Zaya”

**Step 5 – Password Reset**

- Return to the Forgot Password page.
- Enter:
  - Email: (the one found in the review)
  - Security Answer: `Zaya`
- Validate and set a **new password** for Bjoern’s account.
- Login is now possible with Bjoern’s account.  
- Challenge validated.

---

## Techniques used:

- Type: OSINT + Exploitation of weak security questions (passive social engineering).
- Objective: The password recovery relies on a security question whose answer is publicly accessible, rendering the mechanism ineffective.

## Tools used:

- Web Browser  
- Google Search / OSINT on public information  
- YouTube (official presentation by Björn Kimminich)

---

## 2. Vulnerabilities

**Vulnerability name:**

- Broken Authentication  
- Weak Security Questions

**Affected component:**

- Password Reset System (reset via security question)

**Severity:**

- **High** = user account compromised without direct interaction

---

## 3. Risks

- Full compromise of Bjoern’s account.  
- Potential privilege escalation if the account has elevated rights.  
- Exposure of personal data.  
- Business impact: loss of customer trust and reputational damage.

---

## 4. Actions

**Risk Mitigation**

- Remove the use of static security questions.  
- Replace with modern mechanisms:
  - Password reset via one-time email token
  - MFA (Multi-Factor Authentication)

**Remediation Fix**

- Avoid storing static and predictable answers.  
- Introduce a **secure token-based reset system** with quick expiration.  
- Always verify identity via email or SMS.

**Best Practices**

- Avoid simple or publicly discoverable security questions.  
- Never reuse publicly known security questions.  
- Enforce a strict and secure account management policy.
