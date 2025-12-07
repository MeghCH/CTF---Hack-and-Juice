**_Injection – Level 3 – Login Bender (SQL Injection)_**

## 1. Methodology

**Step 1 – Trouver l’email de Bender**

- Sur Juice Shop, les emails suivent souvent le même modèle.
- L’email de Bender est généralement :

bender@juice-sh.op

**Step 2 – Essayer une connexion classique**

- Aller sur la page Login.
- Entrer :  
  Email : `bender@juice-sh.op`  
  Password : `1234` ou autre mot de passe simple.
- Résultat : échec → le mot de passe n’est pas correct.

**Step 3 – Tenter une injection SQL**  
Comme pour d’autres challenges similaires (ex : Login Jim), on injecte un commentaire SQL pour contourner la vérification du mot de passe.

- Modifier l’email comme suit :

bender@juice-sh.op'--

Ce payload ferme la chaîne SQL puis commente la suite, ce qui annule totalement la vérification du mot de passe.

**Step 4 – Connexion**

- Entrer n’importe quel mot de passe (ou laisser vide).
- Cliquer sur Login.
- La connexion **réussit immédiatement** grâce à la SQL Injection.

**Résultat :**  
→ Le compte de Bender est accessible **sans connaître son mot de passe**.  
→ Challenge validé.

---

## 2. Vulnerabilities

**Vulnerability name:**

- SQL Injection
- Authentication Bypass
- Improper Input Validation

**Affected component:**

- Login API endpoint (`/rest/user/login`)
- Back-end SQL query using the email field

**Severity:**

**Critical**

---

## 3. Risks

- Accès non autorisé aux comptes utilisateurs.
- Risque élevé d’accès à des comptes sensibles.
- Possibilité d’escalade de privilèges.
- Compromission des données utilisateurs.
- Impact majeur sur la sécurité globale de l’application.

---

## 4. Actions

**Risk Mitigation:**

- Interdire toute concaténation directe de données utilisateur dans des requêtes SQL.
- Utiliser des requêtes préparées (prepared statements).
- Valider strictement les entrées utilisateur (format email).

**Remediation fixes:**

- Échapper les caractères dangereux (`'`, `"`, `--`, `;`).
- Utiliser une whitelist sur les formats acceptés.
- Implémenter un contrôle d’accès fort pour l’endpoint Login.

**Best security practices:**

- Ajouter une authentification multifacteur.
- Mettre en place un WAF pour détecter la SQLi.
- Réaliser des tests réguliers d’injection.

---
