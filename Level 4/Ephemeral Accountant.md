**_Ephemeral Accountant – Level 4_**

## 1. Methodology

**Step 1 – Préparation**

- Recherche d'informations sur l'accountant.

**Step 2 – Injection SQL**

- Utilisation d'une union pour créer un compte temporaire.

**Step 3 – Connexion**

- Connexion avec le compte créé.

**Step 4 – Validation**

- Accès réussi.
- Challenge validé.

## Techniques utilisées:

- SQL Injection
- Account Creation Bypass

## Outils utilisés :

- Burp Suite

---

## 2. Vulnerabilities

**Vulnerability:**

- SQL Injection
- Broken Authentication

**Affected component:**

- Système d'authentification

**Severity:**

- **High**

---

## 3. Risks

- Création de comptes non autorisés.

---

## 4. Actions

**Risk Mitigation**

- Utiliser des requêtes préparées.

**Remediation Fix**

- Valider les entrées.

**Best Practices**

- OWASP SQL Injection Prevention.

---

## 5. Evidence

**Payload SQL**
![Payload](../image/Ephemeral_Accountant_1.png)
