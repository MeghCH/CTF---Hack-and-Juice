**_Improper Input Validation – Level 3 – Admin Registration_**

## 1. Methodology

**Step 1 – Accès à la page d’inscription**

- Aller sur la page Login :  
  https://juice-shop.example.com/#/login
- Cliquer sur “Not yet a customer?” pour accéder au formulaire d’enregistrement.

**Step 2 – Création d’un compte normal**

- Remplir les champs du formulaire (email, password, passwordRepeat).
- Ouvrir Burp Suite → Proxy → Intercept ON.
- Cliquer sur Register pour envoyer la requête.

**Step 3 – Interception de la requête**

Requête capturée :

POST /api/Users/  
Content-Type: application/json  
{  
 "email": "test@example.com",  
 "password": "123456",  
 "passwordRepeat": "123456"  
}

- Clic droit → Send to Repeater.

**Step 4 – Vérification du rôle retourné**  
Dans Repeater → Send :

- Aller dans l'onglet **Raw** de Burp

Réponse :

{  
 "user": {  
 "email": "test@example.com",  
 "role": "customer"  
 }  
}

→ Le rôle est automatiquement défini sur "customer".

**Step 5 – Manipulation du rôle**

- Retour dans Proxy → Intercept ON
- Resoumettre le formulaire Register
- Modifier la requête JSON en ajoutant `"role": "admin"` :

{  
 "email": "admin_test@example.com",  
 "password": "123456",  
 "passwordRepeat": "123456",  
 "role": "admin"  
}

- Cliquer sur Forward
- Puis Drop
- Désactiver Intercept OFF

**Step 6 – Validation**

- Le compte créé devient administrateur.
- Challenge validé.

## Techniques utilisées :

- Types: Parameter tampering
- Client-side trust abuse
- Broken access control testing

## Outils utilisés :

- Burp Suite (Proxy + Repeater)
- Navigateur Web
- JSON viewer

---

## 2. Vulnerabilities

**Vulnerability name:**

- Improper Input Validation
- Broken Access Control

**Affected component:**

- User registration API

**Severity :**

- **High** = L’API accepte un champ "role" non prévu et fait confiance aux données envoyées par l’utilisateur.

---

## 3. Risks

- Création de comptes admin non autorisés
- Compromission totale de l’application
- Accès aux données sensibles
- Perte de contrôle du système
- Impact business : perte de confiance, incident de sécurité majeur, arrêt du service.

---

## 4. Actions

**Risk Mitigation**

- Filtrer les champs JSON côté serveur
- Ignorer les rôles envoyés depuis le client
- Forcer systématiquement le rôle “customer”

**Remediation Fix**

- Supprimer toute prise en charge du champ "role" côté client
- Validation serveur stricte des entrées utilisateur
- Contrôle d’accès renforcé

**Example:** Forcer le rôle côté serveur

```js
const user = {
  email: req.body.email,
  password: hash(req.body.password),
  role: "customer",
};
```

**Best Practices**

- Ne jamais faire confiance aux données client
- Gestion interne des rôles sur le backend uniquement
- Tests réguliers de contrôle d’accès

---
