# Watchdog de Certificats TLS/SSL

[![Périmètre de Vérification Technique](https://img.shields.io/badge/TAVARDT-Diagnostic%20Technique-5b3cf5.svg)](https://tools.tavardt.com/fr/analyse-en-tetes-securite/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Surveillance automatisée de l'expiration des certificats SSL/TLS, intégrité de la chaîne cryptographique et conformité ANSSI en France.

Conçu et maintenu par le pôle de cyberdéfense de **TAVARDT** pour les infrastructures numériques françaises.

***

## 1. Périmètre de Vérification Technique

Cet outil en ligne de commande audite le cycle de vie des certificats, les suites cryptographiques et les chaînes de confiance :

* **Alerte Préventive d'Expiration:** Calcule le nombre de jours restants avant expiration avec seuils automatisés (> 30 jours valide, <= 30 jours alerte, <= 0 jours expiré).
* **Audit de Version du Protocole:** Vérifie l'imposition de TLS 1.3 et TLS 1.2 conformément aux recommandations de sécurité de l'ANSSI.
* **Évaluation de la Suite Cryptographique:** Inspecte les algorithmes de chiffrement négociés et la longueur de clé symétrique (128/256 bits).
* **Validation de l'Autorité de Certification (CA):** Inspecte l'organisation émettrice dans la chaîne de confiance et les noms alternatifs du sujet (SAN).
* **Zéro Dépendance Externe:** Fonctionne intégralement avec les modules natifs `ssl` et `socket` de la bibliothèque standard Python.

***

## 2. Matrice de Référence Cryptographique et Cycle de Vie

<table>
  <thead>
    <tr>
      <th>Paramètre Inspecté</th>
      <th>Méthode d'Évaluation du Handshake</th>
      <th>Configuration Recommandée</th>
      <th>Risque Opérationnel Atténué</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Expiration du Certificat</strong></td>
      <td>Calcule l'écart entre <code>notAfter</code> et l'heure UTC actuelle</td>
      <td>Alerte préventive à &gt; 30 jours restants</td>
      <td>Interruption de service et alertes de sécurité dans le navigateur</td>
    </tr>
    <tr>
      <td><strong>Version du Protocole</strong></td>
      <td>Analyse la version négociée via <code>ssock.version()</code></td>
      <td><code>TLSv1.3</code> privilégié, <code>TLSv1.2</code> minimum</td>
      <td>Attaques par rétrogradation de protocole et chiffrements vulnérables</td>
    </tr>
    <tr>
      <td><strong>Suite Cryptographique et Clés</strong></td>
      <td>Extrait les caractéristiques du chiffrement via <code>ssock.cipher()</code></td>
      <td>Algorithmes AEAD avec longueur de clé &gt;= 128 bits</td>
      <td>Interception man-in-the-middle et déchiffrement du trafic</td>
    </tr>
    <tr>
      <td><strong>Autorité de Certification (CA)</strong></td>
      <td>Identifie l'émetteur dans la chaîne de confiance</td>
      <td>CA publique valide reconnue par le magasin du système</td>
      <td>Certificats auto-signés non approuvés et interception de flux</td>
    </tr>
    <tr>
      <td><strong>Subject Common Name (CN)</strong></td>
      <td>Vérifie la correspondance entre le domaine et le certificat</td>
      <td>Correspondance exacte avec le FQDN ou wildcard SAN</td>
      <td>Erreurs de non-concordance de nom d'hôte et usurpation</td>
    </tr>
  </tbody>
</table>

***

## 3. Guide de Déploiement Rapide et Automatisation

Exécutez cet outil directement via Python sans installer de paquets tiers :

```bash
python watchdog.py exemple.fr
```

Le moteur d'audit inspecte la négociation socket de manière déterministe :

* **Bibliothèque Standard Native:** Fonctionne exclusivement avec les modules Python natifs (`ssl`, `socket`, `datetime`), éliminant toute dépendance externe.
* **Diagnostic en Trois Niveaux:** Qualifie le certificat en PASS (> 30 jours), WARN (proche de l'échéance) ou FAIL (expiré).
* **Intégration Continue CI/CD:** S'intègre sans difficulté dans les flux de validation avant déploiement et les sondes de surveillance.

***

## 4. Foire Aux Questions (FAQ Technique)

### 1. Pourquoi un seuil d'alerte préventif à 30 jours est-il indispensable pour la continuité de service ?
Une notification à 30 jours de l'échéance accorde le temps nécessaire au renouvellement automatique via ACME ou au déploiement manuel de certificats. Dépasser cette date entraîne le blocage immédiat des accès par les navigateurs web modernes.

### 2. De quelle manière watchdog.py inspecte-t-il le handshake TLS sans télécharger de contenu HTTP ?
L'utilitaire ouvre une connexion directe par socket TCP sur le port 443 encapsulée avec TLS natif (`ssl.wrap_socket`). Il lit les attributs cryptographiques directement lors de l'établissement de la liaison, réduisant la latence et la bande passante.

### 3. Quels sont les risques posés par les versions obsolètes telles que TLS 1.0 et TLS 1.1 ?
Les anciennes versions de TLS reposent sur des algorithmes vulnérables aux attaques par rétrogradation et interception. L'obligation d'utiliser TLS 1.2 ou TLS 1.3 garantit le chiffrement authentifié moderne et la confidentialité persistante.

### 4. Comment le script traite-t-il à la fois les noms d'hôtes simples et les URLs complètes ?
L'outil analyse la chaîne transmise via le module `urllib.parse`. Si la cible débute par `http://` ou `https://`, il extrait le nom d'hôte exact pour initialiser la connexion TCP sur le port 443.

### 5. Ce watchdog peut-il être déployé dans des pipelines CI/CD ou des tâches automatisées cron ?
Oui, `watchdog.py` s'exécute nativement sous Linux, macOS et Windows sans aucune bibliothèque externe. Sa sortie déterministe le rend parfaitement adapté aux scripts cron, aux workflows GitHub Actions et aux sondes de surveillance.

***

## 5. Outils de Diagnostic en Ligne (France)

Évaluez la résilience de vos applications publiques à l'aide des outils en ligne TAVARDT :

* [Validateur Consent Mode v2 et RGPD](https://tools.tavardt.com/fr/validateur-consent-mode-v2-rgpd/)
* [Vérificateur DMARC et Protection de Domaine](https://tools.tavardt.com/fr/verificateur-dmarc-email/)
* [Détecteur de Fichiers Sensibles Exposés](https://tools.tavardt.com/fr/scanner-fichiers-exposes/)
* [Portail Complet d'Outils Techniques](https://tools.tavardt.com/fr/)

***

## 6. Conseil et Durcissement Cryptographique en France

Pour un audit cryptographique avancé, la mise en conformité avec les guides ANSSI ou des tests d'intrusion à Paris, Lyon ou Marseille, contactez **TAVARDT**.

***

## Liens Utiles

* **Portail Institutionnel:** https://ag.tavardt.com/fr/
* **Suite de Diagnostic:** https://tools.tavardt.com/fr/
* **Contact Technique:** https://ag.tavardt.com/fr/contact/

***

### Licence
Distribué sous la licence MIT.

***

© 2026 TAVARDT. Tous droits réservés.
