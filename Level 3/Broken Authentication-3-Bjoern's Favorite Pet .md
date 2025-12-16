**_Broken Authentication – Level 3 – Bjoern's Favorite Pet_**

## 1. Methodology

**Step 1 – Recherche de la cible (OSINT interne)**

- Se connecter au site Juice Shop.
- Parcourir les **produits** disponibles afin d’identifier des informations utilisateurs.
- Dans le produit _OWASP Snakes and Ladders – Web Applications_, accéder aux **reviews**.
- Copier/coller l’email visible dans un commentaire :  
  → Exemple : bjoern.kimminich@owasp.org

**Step 2 – Déconnexion et lancement de la procédure de récupération**

- Se déconnecter du site.
- Aller sur la page **Login**.
- Cliquer sur **"Forgot your password?"**.
- Entrer l’adresse email trouvée dans les reviews.

**Step 3 – OSINT externe (Google / YouTube)**

- Recherche sur Internet : **“Bjoern Kimminich”**.
- Parmi les résultats, ouvrir la vidéo :  
  **BeNeLux Day 2018: Juice Shop – OWASP's Most Broken Flagship – Björn Kimminich**
- Visionner la partie où Björn montre la page de récupération de mot de passe pour Juice Shop.
- On y voit la **question secrète** qu'il a utilisée et sa **réponse**.

**Step 4 – Extraction des informations de sécurité**  
Dans la démonstration, les informations affichées sont :

- **Question secrète:** “Quel est le nom de votre animal de compagnie ?”
- **Réponse:** “Zaya”

**Step 5 – Réinitialisation du mot de passe**

- Retourner sur la page Forgot Password.
- Entrer :
  - Email : (celui récupéré dans la review)
  - Réponse secrète : `Zaya`
- Valider et saisir un **nouveau mot de passe** pour le compte de Bjoern.
- On peut se connecter avec le compte de Bjoern.
- Challenge validé.

## Techniques utilisées :

- Type: OSINT + Exploitation de questions de sécurité faibles (social engineering passif).
- Objectif: La récupération du mot de passe repose sur une question de sécurité dont la réponse est publiquement accessible, rendant le mécanisme inefficace.

## Outils utilisés :

- Navigateur Web
- Recherche Google / OSINT appliqué aux informations publiques
- YouTube (présentation officielle de Björn Kimminich)

---

## 2. Vulnerabilities

**Vulnerability name:**

- Broken Authentication
- Weak Security Questions

**Affected component:**

- Password Reset System (réinitialisation via question secrète)

**Severity:**

- **High** = compromission d’un compte utilisateur sans interaction.

---

## 3. Risks

- Compromission complète du compte de Bjoern.
- Escalade potentielle si le compte a des privilèges importants.
- Exposition de données personnelles.
- Impact business : perte de confiance client et atteinte à la réputation.

---

## 4. Actions

**Risk Mitigation**

- Supprimer l’usage des questions secrètes statiques.
- Remplacer par des mécanismes modernes :
  - Reset par email avec token à usage unique
  - MFA (Authentification multi-facteurs)

**Remediation Fix**

- Ne plus stocker de réponses statiques et prévisibles.
- Introduire un système de reset basé sur un **jeton chiffré**, expirant rapidement.
- Vérifier systématiquement l’identité par email ou SMS.

**Best Practices**

- Éviter les questions secrètes trop simples ou trouvables via OSINT.
- Ne jamais réutiliser des questions de sécurité démontrées publiques.
- Imposer une politique de gestion sécurisée des comptes.

---
