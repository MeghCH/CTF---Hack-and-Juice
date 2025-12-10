# _Broken Access Control – Level 4 – Allowlist Bypass_

## 1. Methodology

**Step 1 – Reconnaissance**

- Analyse du fichier **main.js** via DevTools.

- Recherche du mot-clé **"redirect"**.

- Découverte d'un domaine autorisé dans l'allowlist :

      shop.spreadshirt.com

**Step 2 – Test de l'URL autorisée**

- Construction de l'URL :

      https://juice-shop.example.com/shop.spreadshirt.com

- Ouverture dans un nouvel onglet → page Spreadshirt avec T-shirts.

**Step 3 – Analyse du mécanisme de redirection**

- L'application utilise :

      redirect?to=http://...

**Step 4 – Bypass de l'allowlist**

- Payload :

      ?to=http://google.com/?test=shop.spreadshirt.com/juiceshop

- URL finale :

      https://juice-shop.example.com/redirect?to=http://google.com/?test=shop.spreadshirt.com/juiceshop

- Résultat : redirection vers Google → bypass réussi.

**Step 5 – Validation**

- Le challenge **Allowlist Bypass Level 4** est validé.

---

## 2. Vulnerabilities

**Vulnerability** : Improper Allowlist Validation / Open Redirect\
**Affected Component** : redirect handler\
**Severity:**  
**High**

---

## 3. Risks

- Redirection vers sites malveillants.
- Phishing facilité.
- Perte de confiance utilisateur.

---

## 4. Actions

**Risk Mitigation**

- Vérification stricte du domaine de destination.
- Interdiction des sous-chaînes autorisées dans les paramètres.
- Validation serveur obligatoire.

**Remediation Fix**

- Comparaison exacte des domaines (match complet).
- Canonicalisation avant validation.
- Blocage des redirections externes.

**Best Practices**

- Suivre OWASP Open Redirect Prevention.
- Journaliser les tentatives suspectes.

---
