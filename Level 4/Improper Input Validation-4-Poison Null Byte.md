**_Improper Input Validation – Level 4 – Poison Null Byte_**

## 1. Methodology

**Step 1 – Reconnaissance**

- Observation du comportement général de l’application **OWASP Juice Shop**.
- Recherche d’indices et de contenus cachés (Easter Eggs, fichiers oubliés, erreurs serveur).
- Utilisation de **Burp Suite** et **Firefox DevTools** pour intercepter et analyser les requêtes HTTP.

**Step 2 – Exploration via FTP**

- Remplacement du segment `/search` dans l’URL par `/ftp` :

https://juice-shop.example.com/ftp

- Cela révèle un répertoire FTP accessible par erreur (mauvaise configuration serveur).

**Step 3 – Découverte du fichier “eastere.gg”**

- En parcourant les fichiers visibles, un fichier nommé `eastere.gg` attire l’attention.
- Cliquer dessus l’ouvre dans une nouvelle fenêtre, mais le téléchargement direct échoue.

**Step 4 – Exploitation du Poison Null Byte**

- Pour contourner la vérification d’extension côté serveur, injection d’un **Poison Null Byte** :

https://juice-shop.example.com/ftp/eastere.gg%2500.md

`%2500` correspond à un **NULL byte encodé deux fois**.

- Le serveur interprète alors la fin du nom de fichier comme `.md` et autorise le téléchargement.

**Step 5 – Récupération et validation**

- Le fichier est téléchargé avec succès en `.md` et contient l’easter egg.
- En revenant sur la page `/search`, les trois flags sont automatiquement validés :
- **Easter Egg**
- **Poison Null Byte**
- **Error Handling / Git Exposure**

**Outils utilisés :**

- Navigateur web
- Burp Suite
- URL encoding tool (pour générer `%2500`)

---

## 2. Vulnerabilities

**Vulnerability name:**

- Poison Null Byte Injection
- Unrestricted File Access
- Security Misconfiguration
- Sensitive Information Disclosure

**Affected component:**

- File download handler
- FTP directory exposure `/ftp`
- Input validation (filename parsing)

**Severity:** High

---

## 3. Risks

- Accès non autorisé à des fichiers internes.
- Possibilité de contourner les protections d’extension.
- Lecture de données sensibles ou potentiellement critiques.
- Risque d’exposition de chemins, secrets ou de fichiers de configuration.
- Dégradation de la sécurité générale du serveur.

---

## 4. Actions

**Risk mitigation:**

- Filtrer toutes les chaînes incluant `\0`, `%00`, `%2500`.
- Interdire toute navigation dans des répertoires internes.
- Restreindre strictement les formats de fichiers autorisés.

**Remediation fixes:**

- Utiliser des fonctions sûres (non basées sur C) pour gérer les chemins de fichiers.
- Nettoyer les entrées afin de supprimer les Null Bytes.
- Désactiver la page `/ftp` ou la protéger via authentification.

**Best security practices:**

- Ne jamais exposer de répertoires système.
- Valider côté serveur les noms de fichiers et extensions.
- Auditer régulièrement les endpoints accessibles publiquement.

---

## 5. Evidence

**Site sur les Poison Null Byte**
https://www.cardboard-iguana.com/grimoire/spells/poison-null-byte-attack
