# _Upload Type – Level 3_

## 1. Methodology

**Step 1 – Préparation**

- Utiliser Burp Suite pour intercepter les requêtes d'upload.

**Step 2 – Tentative d'upload**

- Essayer d'uploader un fichier non-PDF via l'interface.

**Step 3 – Modification de la requête**

- Intercepter la requête POST dans Burp et modifier le Content-Type à application/pdf.

**Step 4 – Envoi de la requête modifiée**

- Envoyer la requête via Burp Repeater.

**Step 5 – Validation**

- Le serveur accepte l'upload (réponse 204 No Content), validant le challenge.

## Techniques utilisées:

- Improper Input Validation Bypass
- Header Manipulation

## Outils utilisés :

- Burp Suite

---

## 2. Vulnerabilities

**Vulnerability:**

- Improper Input Validation

**Affected component:**

- Fonction d'upload de fichiers

**Severity:**

- **High**

---

## 3. Risks

- Upload de fichiers malveillants (webshells, scripts) en contournant les restrictions de type.

---

## 4. Actions

**Risk Mitigation**

- Implémenter une validation stricte côté serveur des types MIME et du contenu réel.

**Remediation Fix**

- Vérifier les magic bytes du fichier et ne pas se fier aux headers client.

**Best Practices**

- OWASP Improper Input Validation.

---