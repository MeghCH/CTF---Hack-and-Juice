# _Misplaced Signature File – Level 5_

## 1. Methodology

**Step 1 – Préparation**

- Utiliser Burp Suite pour intercepter et modifier les requêtes HTTP.

**Step 2 – Accès au répertoire /ftp**

- Naviguer vers le répertoire /ftp/ exposé publiquement pour accéder aux fichiers.

**Step 3 – Contournement de la restriction d'extension**

- Ajouter %2500 (double encodage du null byte) pour masquer l'extension réelle (.yml) derrière une extension autorisée (.md).

**Step 4 – Téléchargement du fichier**

- Envoyer la requête modifiée : GET /ftp/suspicious_errors.yml%2500.md HTTP/1.1

**Step 5 – Validation**

- Le fichier suspicious_errors.yml est téléchargé, validant le challenge.

## Techniques utilisées:

- File Discovery
- Null Byte Injection
- Double URL Encoding

## Outils utilisés :

- Burp Suite

---

## 2. Vulnerabilities

**Vulnerability:**

- Improper Input Validation
- Sensitive Data Exposure

**Affected component:**

- Filtre d'extension des fichiers dans /ftp/

**Severity:**

- **High**

---

## 3. Risks

- Exposition de fichiers sensibles comme les règles de détection (suspicious_errors.yml).

---

## 4. Actions

**Risk Mitigation**

- Implémenter une validation stricte des extensions sans dépendre du décodage.

**Remediation Fix**

- Bloquer les caractères spéciaux comme %00 et %2500 dans les noms de fichiers.

**Best Practices**

- OWASP Improper Input Validation.

---

## 5. Evidence

**Requête Burp Suite**
![Misplaced Signature File](../image/Misplaced_Signature_File_1.png)