**_Manipulate Basket – Level 3_**

## 1. Méthodologie

**Étape 1 – Préparation**

- Se connecter avec deux comptes différents.

**Étape 2 – Interception**

- Ajouter un produit au panier en utilisant Burp Intercept pour capturer la requête.

**Étape 3 – Modification**

- Changer l'ID de l'utilisateur dans la requête pour viser le panier d'un autre.

**Étape 4 – Validation**

- Le produit est ajouté au panier de l'autre utilisateur.
- Défi réussi.

## Techniques utilisées :

- IDOR (Référence directe d'objet non sécurisée)
- Manipulation de paramètres

## Outils utilisés :

- Burp Suite

---

## 2. Vulnérabilités

**Vulnérabilité :**

- Référence directe d'objet non sécurisée (IDOR)

**Composant affecté :**

- Point d'accès du panier

**Sévérité :**

- **Élevée**

---

## 3. Risques

- Possibilité de changer les données d'autres utilisateurs.

---

## 4. Actions

**Réduction des risques**

- Vérifier les permissions pour chaque requête.

**Correction**

- Mettre en place des contrôles d'accès.

**Bonnes pratiques**

- OWASP IDOR.

---

## 5. Preuves

**Site OWASP IDOR**
https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/05-Authorization_Testing/04-Testing_for_Insecure_Direct_Object_References

**Requête manipulée**
![Requête](../image/Manipulate_Basket_1.png)
