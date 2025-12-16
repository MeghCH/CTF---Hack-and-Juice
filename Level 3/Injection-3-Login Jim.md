**_Injection – Level 3 – Login Jim_**

## 1. Methodology

**Step 1 – Trouver l’email de Jim**

- Comme dans presque toutes les instances du Juice Shop, l’email de Jim est :

jim@juice-sh.op

**Step 2 – Essayer une connexion classique**

- Aller sur la page Login.
- Entrer :  
  Email : `jim@juice-sh.op`  
  Password : `1234`
- Résultat : échec → le mot de passe est incorrect.

**Step 3 – Tenter une injection SQL dans le champ email**

- Modifier l’email pour ajouter un commentaire SQL :

jim@juice-sh.op'--

- Le `--` permet de commenter la fin de la requête SQL côté serveur, contournant la vérification du mot de passe.

**Step 4 – Valider la connexion**

- Entrer n’importe quel mot de passe.
- Cliquer sur Login.
- La connexion **réussit**, car la condition SQL devient vraie grâce au commentaire.

**Résultat :**  
→ Connexion réussie **sans mot de passe**, grâce à une **SQL Injection basique**.  
→ Challenge validé.

## Technique utilisée :

- SQL Injection
- Comment-based injection (`--`)

## Outils utilisés :

- Navigateur Web

---

## 2. Vulnerabilities

**Vulnerability name:**

- SQL Injection
- Authentication Bypass
- Improper Input Validation

**Affected component:**

- Login API endpoint
- Backend SQL query handling (email field)

**Severity:**

- **Critical**

---

## 3. Risks

- Connexion non autorisée à des comptes utilisateurs.
- Possibilité d’accéder à des comptes sensibles (ex. administrateurs).
- Exfiltration potentielle des données utilisateurs.
- Compromission complète du système d’authentification.
- Impact business: Risque légal en cas de fuite de données (RGPD)+ mauvaise réputation

---

## 4. Actions

**Risk mitigation:**

- Ne jamais concaténer les entrées utilisateur dans les requêtes SQL.
- Utiliser des requêtes préparées (prepared statements).
- Ajouter une validation stricte sur le format des emails.

**Remediation fixes:**

- Nettoyer les caractères spéciaux (`'`, `"`, `--`, `;`).
- Appliquer un filtrage serveur (whitelist).
- Empêcher les commentaires SQL dans les champs utilisateur.

**Exemple:** exemple typique d’un correctif contre la SQL Injection

```js
const query = "SELECT * FROM users WHERE email = ? AND password = ?";
db.execute(query, [email, password]);
```

**Best security practices:**

- Implémenter un WAF (Web Application Firewall) pour détecter les signatures SQL.
- Effectuer des tests automatisés contre les injections.
- Utiliser une authentification renforcée multi-facteurs (MFA).

---

## 5. Evidence

**Site sur l'injection sql**
https://www.vaadata.com/blog/fr/injections-sql-principes-impacts-exploitations-bonnes-pratiques-securite/

https://portswigger.net/web-security/sql-injection
