# _Unvalidated Redirects – Level 4 – Allowlist Bypass_

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

- Le challenge est validé.

## Outils utilisés :

- DevTools

---

## 2. Vulnerabilities

**Vulnerability:**

- Unvalidated Redirects
- Improper Allowlist Validation

  **Affected Component:**

  - Gestionnaire de redirection (Redirect handler)

  **Severity:**

  - **High**

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
- Canonicalisation avant validation. (transformer une donnée qui peut s’écrire de mille façons en une forme unique “canonique” afin de pouvoir la comparer, la filtrer et l’autoriser/interdire correctement.)
- Blocage des redirections externes.

**Best Practices**

- Suivre OWASP Open Redirect Prevention.
- Journaliser les tentatives suspectes.

---

## 5. Evidence

**Site OWASP REdirect Prevention**
https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html
