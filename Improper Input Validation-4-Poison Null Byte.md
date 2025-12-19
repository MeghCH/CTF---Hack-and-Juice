**_Improper Input Validation – Level 4 – Poison Null Byte_**

## 1. Methodology

**Step 1 – Reconnaissance**

- Observation of the general behavior of the **OWASP Juice Shop** application.
- Search for hidden content (Easter Eggs, forgotten files, server errors).

**Step 2 – Exploration via FTP**

- Replace the `/search` segment in the URL with `/ftp`:

`https://juice-shop.example.com/ftp`

- This reveals an **FTP directory** mistakenly accessible due to a **server misconfiguration**.

**Step 3 – Discovery of the “eastere.gg” File**

- While browsing the visible files, a file named `eastere.gg` stands out.
- Clicking it opens a new tab, but the direct download fails.

**Step 4 – Exploitation of the Poison Null Byte**

- To bypass the file extension check on the server, inject a **Poison Null Byte**:

`https://juice-shop.example.com/ftp/eastere.gg%2500.md`

- `%2500` corresponds to a **double-encoded NULL byte**.
- The server interprets the filename as ending with `.md`, allowing the download.

**Step 5 – Retrieval and Validation**

- The file successfully downloads as `.md` and contains the Easter Egg.
- Returning to the `/search` page automatically validates three challenges:
  - **Easter Egg**
  - **Poison Null Byte**
  - **Error Handling / Git Exposure**

---

## Techniques Used

- Directory enumeration (FTP folder discovery)
- Security Misconfiguration Exploitation
- Poison Null Byte Injection
- File Extension Bypass
- Unrestricted File Access

## Tools Used

- Web Browser
- URL Encoding Tool (to generate `%2500`)

---

## 2. Vulnerabilities

**Vulnerability Name:**

- Improper Input Validation
- Poison Null Byte Injection
- Unrestricted File Access
- Security Misconfiguration
- Sensitive Information Disclosure

**Affected Component:**

- File Download Handler
- FTP Directory Exposure (`/ftp`)

**Severity:**

- **High**

---

## 3. Risks

- Unauthorized access to internal files.
- Ability to bypass file extension validation.
- Exposure of sensitive or critical data.
- Disclosure of configuration or secret information.
- General degradation of server security.
- **Business Impact:** internal file exposure leading to data leakage, user trust loss, and reputational damage.

---

## 4. Actions

**Risk Mitigation**

- Filter all strings containing `\0`, `%00`, `%2500`.
- Block navigation into internal directories.
- Restrict strictly allowed file formats.

**Remediation Fixes**

- Use safe functions for file path management.
- Sanitize inputs to remove Null Bytes.
- Disable or protect the `/ftp` directory with authentication.

**Example:** Secure filename validation

```js
function isValidFilename(filename) {
  // Reject null bytes
  if (filename.includes("\0") || filename.includes("%00")) {
    return false;
  }

  // Allow specific extensions
  const allowedExtensions = [".md", ".txt"];
  return allowedExtensions.some((ext) => filename.endsWith(ext));
}

if (!isValidFilename(requestedFile)) {
  return res.status(400).json({ error: "Invalid file name" });
}
```

**Best Security Practices**

- Never expose system directories publicly.
- Always validate filenames and extensions on the server side.
- Perform regular audits of public endpoints.

---

## 5. Evidence

**Reference on Poison Null Byte Attacks:**  
https://www.cardboard-iguana.com/grimoire/spells/poison-null-byte-attack
