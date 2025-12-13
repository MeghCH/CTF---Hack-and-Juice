**_Improper Input Validation – Level 4 – Payback Time_**

## 1. Methodology

**Step 1 – Connexion au site**

- Se connecter avec un compte utilisateur classique.

**Step 2 – Ajouter un article au panier**

- Choisir n’importe quel produit et l’ajouter au panier.
- Aller dans la page **Basket**.

**Step 3 – Préparer Burp Suite**

- Ouvrir **Burp Suite**.
- Aller dans **Proxy** → mettre **Intercept OFF** pour ne pas tout capturer au début.

**Step 4 – Interception de la modification du panier**

- Sur la page web, cliquer sur le bouton **+** dans le panier pour augmenter la quantité.
- Activer immédiatement **Intercept ON** dans Burp Proxy.
- La requête interceptée ressemble à :

PUT /api/BasketItems/1  
Content-Type: application/json  
{  
 "quantity": 2  
}

**Step 5 – Modification de la requête interceptée**

- Aller dans l’onglet **Pretty** de Burp.
- Modifier la quantité :

{  
 "quantity": -1000  
}

- Cliquer sur **Forward**.
- Puis désactiver l’interception → **Intercept OFF**.

**Step 6 – Vérifier le panier**

- Revenir sur le site : le montant total du panier devient **négatif**.
- Continuer comme si on finalisait une commande valide.

**Step 7 – Procéder au paiement**

- Ajouter une adresse :
  - Name : NA
  - Street : NA
  - ZIP : 12345678
- Choisir la livraison **One Day Delivery**.
- Cliquer sur **Pay**.

**Résultat :**  
La commande passe même avec un montant négatif → challenge validé.

## Outils utilisés :

- Burp Suite (Proxy)

- Navigateur Web

---

## 2. Vulnerabilities

**Vulnerability name :**

- Broken Access Control
- Price Manipulation
- Integer Underflow / Logic Flaw

**Affected component :**

- Basket Update API (`/api/BasketItems/`)
- Order calculation logic

**Severity :**
**Critical** = permet de manipuler le prix et contourner le paiement.

---

## 3. Risks

- Achats gratuits ou création de montants négatifs.
- Perte financière directe.
- Exploit trivial et reproductible.
- Compromission de la logique de facturation.
- Dégradation de la crédibilité de l'application.

---

## 4. Actions

**Risk Mitigation**

- Valider toutes les quantités côté serveur.
- Interdire les valeurs négatives ou zéro.
- Vérifier les types d’entrées.

**Remediation Fix**

- Forcer `quantity >= 1`.
- Utiliser des entiers non signés (unsigned).
- Recalculer le total **uniquement côté serveur**.

**Best Practices**

- Ne jamais faire confiance au client.
- Effectuer des tests de fuzzing sur les endpoints sensibles.
- Implémenter une logique de panier sécurisée avec validations strictes.

---

## 5. Evidence

Requête modifiée :

PUT /api/BasketItems/1  
Content-Type: application/json  
{  
 "quantity": -1000  
}

Montant du panier affiché en négatif → commande validée.
