**_Reset Uvogin's Password – Level 4_**

## 1. Methodology

**Step 1 – Préparation**

- Navigation vers la page de reset de mot de passe.

**Step 2 – Exploitation**

- Utilisation d'une vulnérabilité pour reset le mot de passe d'Uvogin.

**Step 3 – Connexion**

- Connexion avec le nouveau mot de passe.

**Step 4 – Validation**

- Challenge validé.

## Techniques utilisées:

- Password Reset Bypass

## Outils utilisés :

- Burp Suite

---

## 2. Vulnerabilities

**Vulnerability:**

- Broken Authentication
- Weak Password Reset

**Affected component:**

- Système de reset de mot de passe

**Severity:**

- **High**

---

## 3. Risks

- Reset de mots de passe d'autres utilisateurs.

---

## 4. Actions

**Risk Mitigation**

- Implémenter des tokens sécurisés.

**Remediation Fix**

- Vérifier l'identité.

**Best Practices**

- OWASP Password Reset.

---

## 5. Evidence

**Requête de reset**
![Requête](../image/Reset_Uvogin_1.png)
