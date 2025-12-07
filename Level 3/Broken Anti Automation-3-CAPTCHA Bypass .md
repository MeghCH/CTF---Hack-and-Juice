**_Broken Anti Automation – Level 4 – Feedback Brute Force_**

## 1. Methodology

**Step 1 – Préparation**

- Déconnexion du compte utilisateur pour tester la fonctionnalité publique “Customer Feedback”.
- Navigation vers la page :

https://juice-shop.example.com/#/feedback

**Step 2 – Premier test**

- Saisie du commentaire : `Hi`
- Attribution d’une note de **3 étoiles**
- Résolution du **captcha** manuellement
- Soumission du formulaire pour observer le comportement normal de la requête.

**Step 3 – Capture de la requête HTTP**

- Ouverture de **Burp Suite**
- Activation du mode **Proxy → Intercept is ON**
- Retour sur la page feedback, puis clic sur “Submit”  
  → La requête POST est interceptée dans Burp Suite.

**Step 4 – Observation et sauvegarde**

- Ouverture du **bloc-notes** pour noter les valeurs importantes :
- `id` du commentaire
- `captcha` soumis
- Répétition du processus **2 fois supplémentaires** pour observer les variations dans la requête et les valeurs dynamiques.

**Step 5 – Exploitation**

- Saisie d’un nouveau message : `Hellloooooo`
- Attribution de 3 étoiles, réponse au captcha
- Activation du **Intercept ON** puis soumission du formulaire à nouveau.
- Clic droit → **Send to Repeater** dans Burp Suite.

**Step 6 – Exploitation via Repeater**

- Envoi de la requête une première fois → obtention d’une **Response Header** valide.
- Répétition multiple de la requête (“spam”) via le bouton **Send** dans Repeater.
- Observation : le serveur accepte les requêtes identiques sans blocage ni vérification supplémentaire.

**Step 7 – Validation**

- Retour sur la page web → “All Products”.
- Challenge validé : **Broken Access Control / Rate Limiting / CAPTCHA Weakness**.

**Outils utilisés :**

- **Burp Suite (Proxy + Repeater)**
- **Navigateur web**
- **Bloc-notes**
- **Captcha solver manuel**

---

## 2. Vulnerabilities

**Vulnerability name:**

- Broken Access Control / Weak CAPTCHA Enforcement / Rate Limiting Bypass  
  **Affected component:**
- Feedback submission API endpoint  
  **Severity:**
- **High** = permet un envoi massif de requêtes malgré un captcha censé limiter le spam

---

## 3. Risks

- Possibilité d’abuser du système de feedback (spam, flood, DDoS applicatif).
- Captcha inefficace → automatisation possible via scripts ou Burp Intruder.
- Peut mener à une **pollution de la base de données** (feedbacks multiples inutiles).
- Impact : dégradation du service, atteinte à la crédibilité de la plateforme.

---

## 4. Actions

### Risk Mitigation

- Mettre en place une **vérification serveur du captcha**, pas seulement côté client.
- Implémenter une **limitation du nombre de requêtes par IP ou utilisateur** (rate limiting).
- Introduire des **tokens CSRF** ou des **challenges dynamiques**.

### Remediation Fix

- Valider chaque requête de feedback via un **captcha unique et consommable une seule fois**.
- Rejeter les requêtes répétées ou suspectes en analysant les entêtes.
- Enregistrer un log d’activité suspecte et notifier les administrateurs.

### Best Practices

- Ne jamais se fier à la seule vérification côté client (JavaScript).
- Déployer des protections automatiques type **reCAPTCHA v3** ou **hCaptcha**.
- Configurer des règles WAF pour détecter le flood de requêtes répétées.

---

## 5. Evidence

- Exemple d’URL utilisée :

POST /api/Feedbacks/
Content-Type: application/json
{
"comment": "Hellloooooo",
"rating": 3,
"captcha": "ab12cd"
}
