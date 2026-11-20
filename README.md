# Watchdog Certificats TLS/SSL | TAVARDT France

[![Périmètre de Vérification Technique](https://img.shields.io/badge/TAVARDT-Diagnostic%20Technique-5b3cf5.svg)](https://tools.tavardt.com/fr/analyse-en-tetes-securite/)
[![Juridiction](https://img.shields.io/badge/Juridiction-France-00C853.svg)](https://ag.tavardt.com/fr/cybersecurite/)

Surveillance automatisée de l'expiration des certificats SSL/TLS, de la chaîne de confiance et du chiffrement en France.

Développé et maintenu par le pôle cybersécurité et protection des infrastructures de **[TAVARDT France](https://ag.tavardt.com/fr/)**.

---

## 1. Périmètre de Vérification Technique

Cet utilitaire console analyse la validité temporelle, les algorithmes de chiffrement et l'autorité racine des connexions HTTPS :

* **Alerte d'Expiration Préventive:** Calcule les jours restants avant la fin de validité du certificat avec seuils d'alerte.
* **Audit des Suites Cryptographiques:** Valide l'activation de TLS 1.3 et le rejet des protocoles non sécurisés.
* **Vérification de l'Autorité Émettrice (CA):** Contrôle la chaîne de certification et les noms alternatifs (SAN).
* **Zéro Dépendance Externe:** Fonctionne exclusivement avec les modules natifs ssl et socket de Python.

---

## 2. Guide de Déploiement Rapide

Exécutez cet outil directement via Python sans installer de paquets tiers :

```bash
python watchdog.py exemple.fr
```

---

## 3. Outils de Diagnostic en Ligne (France)

Évaluez la résilience de vos applications publiques à l'aide des outils en ligne TAVARDT :

* [Analyseur d'En-têtes HTTP de Sécurité](https://tools.tavardt.com/fr/analyse-en-tetes-securite/)
* [Validateur Consent Mode v2 et RGPD](https://tools.tavardt.com/fr/validateur-consent-mode-v2-rgpd/)
* [Vérificateur DMARC et Protection de Domaine](https://tools.tavardt.com/fr/verificateur-dmarc-email/)
* [Détecteur de Fichiers Sensibles Exposés](https://tools.tavardt.com/fr/scanner-fichiers-exposes/)
* [Portail Complet d'Outils Techniques](https://tools.tavardt.com/fr/)

---

## 4. Conseil et Remédiation Technique

Pour le durcissement cryptographique de vos serveurs et la réponse à incidents en France, contactez **[TAVARDT France](https://ag.tavardt.com/fr/contact/)**.
