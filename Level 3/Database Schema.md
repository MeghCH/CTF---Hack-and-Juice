**_Database Schema – Level 3_**

## 1. Méthodologie

**Étape 1 – Préparation**

- Lancer Burp Suite pour capturer les requêtes envoyées au site.
- Aller sur la page où on cherche des produits.

**Étape 2 – Injection SQL**

- Entrer un code spécial pour voir combien de colonnes il y a dans la base de données :

        valeur')) union all select 1,2,3,4,5,6,6,7,9 --

- Regarder les erreurs ou les nombres qui s'affichent.

**Étape 3 – Extraire le schéma**

- Utiliser une union pour sortir les infos de la table sqlite_master :

        danyvalue')) union all select 1,2,3,sql,5,6,7,8,9 from sqlite_master --

- Récupérer la structure de la base de données.

**Étape 4 – Validation**

- Envoyer la requête et voir ce qui se passe.
- Défi réussi.

## Techniques utilisées :

- Injection SQL
- Injection basée sur union

## Outils utilisés :

- Burp Suite (Repeater)
- Navigateur web

---

## 2. Vulnérabilités

**Vulnérabilité :**

- Injection SQL
- Exposition du schéma de la base de données

**Composant affecté :**

- Point d'accès pour la recherche de produits

**Sévérité :**

- **Élevée** = permet de sortir des données sensibles de la base.

---

## 3. Risques

- La structure de la base est visible.
- On peut récupérer des infos privées.
- Risque d'accès non autorisé aux données des utilisateurs.

---

## 4. Actions

**Réduction des risques**

- Employer des requêtes préparées.
- Vérifier et nettoyer les entrées des utilisateurs.

**Correction**

- Mettre en place des contrôles stricts sur les entrées.
- Utiliser un ORM pour éviter les injections.

**Bonnes pratiques**

- Vérifier régulièrement les failles SQL.
- Suivre les conseils OWASP sur les injections.

---

## 5. Preuves

**Site OWASP Injection SQL**
https://owasp.org/www-community/attacks/SQL_Injection

**Requête d'injection**
![Requête](../image/SQL_Injection_1.png)
