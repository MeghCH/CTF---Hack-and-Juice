**_Broken Authentication – Level 4 – Login Bjoern_**

## 1. Methodology

**Step 1 – Recherche d’informations sur l’utilisateur Bjoern**

- Aller dans la page **All Products** puis fouiller.
- Chercher le produit :  
  **OWASP Snakes and Ladders – Web Application**.
- Aller dans la section **Reviews** du produit.
- Copier l’adresse email affichée dans un commentaire laissé par Bjoern.  
  Exemple (souvent présent) :  
  **bjoern.kimminich@owasp.org**

**Step 2 – Déconnexion**

- Se déconnecter du compte actuel pour pouvoir lancer la procédure de réinitialisation.

**Step 3 – Procédure “Forgot Password”**

- Aller sur la page **Login**.
- Cliquer sur **“Forgot your password?”**.
- Entrer l’email de Bjoern trouvé dans les reviews.

**Step 4 – OSINT externe pour récupérer la réponse secrète**

- Ouvrir Google et chercher : **Bjoern Kimminich**.
- Ouvrir la vidéo :  
  **“BeNeLux Day 2018: Juice Shop – OWASP’s Most Broken Flagship – Björn Kimminich”**
- Dans la vidéo, repérer le moment où Björn montre une réinitialisation de mot de passe.
- On voit la **question secrète** utilisée :

  **“Quel est le nom de votre animal de compagnie ?”**

- Et la **réponse** donnée par Björn lors de la démo :

  **Zaya**

**Step 5 – Réinitialisation du mot de passe**

- Retourner sur la page Forgot Password du Juice Shop.
- Entrer :
  - Email : celui de Bjoern
  - Réponse secrète : `Zaya`
- Le site permet alors de définir un **nouveau mot de passe** pour le compte de Bjoern.

**Step 6 – Connexion avec les nouvelles informations**

- Aller sur la page Login.
- Entrer l’email trouvé et le nouveau mot de passe défini.
- Le login réussit → challenge validé.

## Outils utilisés :

- Navigateur Web

- OSINT : recherche Google, YouTube

---

## 2. Vulnerabilities

**Vulnerability name:**

- Broken Authentication
- Weak Security Questions / OSINT leakage
- Account Takeover via Password Reset

**Affected component:**

- Système de réinitialisation du mot de passe (questions secrètes)

**Severity:**

- **High** = permet de prendre le contrôle d’un compte utilisateur.

---

## 3. Risks

- Compromission du compte de Bjoern.
- Lecture ou modification de données personnelles.
- Possibilité d’escalade de privilèges si le compte avait des droits spéciaux.
- Forte exposition due à des informations publiques (OSINT facile).
- Impact business : perte de confiance, exposition de données sensibles.

---

## 4. Actions

**Risk Mitigation**

- Supprimer les questions secrètes statiques.
- Remplacer par un système de réinitialisation par **email avec token unique**.
- Limiter le nombre d’essais de réponse à la question secrète.

**Remediation Fix**

- Utiliser des tokens signés, expirant rapidement.
- Exiger un second facteur pour la réinitialisation de mots de passe sensibles.
- Empêcher l’utilisation d’informations publiques comme questions secrètes.

**Best Practices**

- Toujours privilégier un reset sécurisé (token, MFA).
- Éviter toute forme de questions statiques.
- Effectuer des audits d’OSINT pour identifier les données exposées publiquement.

---
