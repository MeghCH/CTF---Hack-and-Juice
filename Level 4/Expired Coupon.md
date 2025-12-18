**_Expired Coupon – Level 4_**

## 1. Methodology

**Step 1 – Préparation**

- Navigation vers la page de coupon.
- Observation des conditions d'utilisation.

**Step 2 – Modification de la date**

- Interception de la requête avec Burp.
- Changement de la date d'expiration.

**Step 3 – Soumission**

- Envoi de la requête modifiée.

**Step 4 – Validation**

- Coupon utilisé avec succès.
- Challenge validé.

## Techniques utilisées:

- Parameter Tampering
- Date Manipulation

## Outils utilisés :

- Burp Suite

---

## 2. Vulnerabilities

**Vulnerability:**

- Improper Input Validation
- Weak Date Validation

**Affected component:**

- Système de coupon

**Severity:**

- **High**

---

## 3. Risks

- Utilisation de coupons expirés.

---

## 4. Actions

**Risk Mitigation**

- Valider les dates côté serveur.

**Remediation Fix**

- Implémenter des contrôles stricts.

**Best Practices**

- OWASP Input Validation.

---

## 5. Evidence

**Requête modifiée**
![Requête](../image/Expired_Coupon_1.png)
