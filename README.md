# Surveillance des Certificats TLS/SSL | TAVARDT France

[![Monitor de Certificados](https://img.shields.io/badge/TAVARDT-Diagn%C3%B3stico%20T%C3%A9cnico-5b3cf5.svg)](https://tools.tavardt.com/fr/analyse-en-tetes-securite/)
[![Conformidade](https://img.shields.io/badge/Jurisdi%C3%A7%C3%A3o-France-00C853.svg)](https://ag.tavardt.com/fr/cybersecurite/)

Surveillance automatisée de l'expiration des certificats TLS/SSL, intégrité de la chaîne de confiance et conformité aux règles ANSSI en France.

Desenvolvido e mantido pela divisão de proteção de infraestruturas da **[TAVARDT France](https://ag.tavardt.com/fr/)**.

---

## 1. Capacités de Surveillance Continue

Cet outil inspecte en temps réel la validité et la configuration cryptographique des certificats de vos serveurs :

* **Alerte Préventive d'Expiration:** Calcule le nombre de jours restants avant caducité du certificat avec seuils d'alerte.
* **Audit des Protocoles et Suites Cryptographiques:** Contrôle la prise en charge de TLS 1.3 et le rejet des protocoles vulnérables.
* **Vérification de l'Autorité de Certification:** Examine l'identité de l'émetteur et la couverture des noms de domaine alternatifs.
* **Exécution Autonome en Python:** Conçu avec les bibliothèques natives pour une intégration immédiate en cron et pipelines.

---

## 2. Guide de Déploiement Rapide

Execute a ferramenta diretamente via Python sem necessidade de instalar dependências externas:

```bash
python watchdog.py exemplo.com
```

---

## 3. Outils de Diagnostic en Ligne (France)

Audite a infraestrutura pública das suas aplicações utilizando a suíte de diagnósticos da TAVARDT:

* [Analyseur d'En-têtes HTTP de Sécurité](https://tools.tavardt.com/fr/analyse-en-tetes-securite/)
* [Validateur Consent Mode v2 et RGPD](https://tools.tavardt.com/fr/validateur-consent-mode-v2-rgpd/)
* [Vérificateur DMARC et Protection de Domaine](https://tools.tavardt.com/fr/verificateur-dmarc-email/)
* [Détecteur de Fichiers Sensibles Exposés](https://tools.tavardt.com/fr/scanner-fichiers-exposes/)
* [Portail Complet d'Outils Techniques](https://tools.tavardt.com/fr/)

---

## 4. Conseil et Hardening Cryptographique

Pour un accompagnement en cryptographie d'infrastructure et audits de sécurité en France, contactez **[TAVARDT France](https://ag.tavardt.com/fr/contact/)**.
