# 00 - BASICS (Fondations Cisco IOS)

---

- Référence du routeur : `Cisco 4221`
- Référence du switch : `Cisco Catalyst 3752 v2 Series`

---

## 🔑︲Accès & Modes

### `enable`

* **But** : passer en mode privilégié (`#`)
* **Effet réel** : donne accès à toutes les commandes critiques (config, debug, save)
* **À savoir** :

  * Sans ça → accès très limité
  * C’est la première commande à faire

---

### `configure terminal`

* **But** : entrer en mode configuration globale
* **Effet réel** : permet de modifier la configuration en RAM (active immédiatement)
* **À savoir** :

  * Rien n’est sauvegardé automatiquement
  * Toute modif peut être perdue au reboot

---

## 🏷️︲Identification

### `hostname SW1`

* **But** : nommer l’équipement
* **Effet réel** :

  * change le prompt (ex: `SW1#`)
  * utile pour debug, logs, réseau réel
* **À savoir** :

  * aucun impact technique réseau

---

## 🚫︲Confort & stabilité

### `no ip domain-lookup`

* **But** : désactiver la résolution DNS automatique
* **Effet réel** :

  * empêche le switch/routeur de chercher un DNS si commande inconnue
* **Problème évité** :

  * freeze de plusieurs secondes après une faute de frappe

---

## 🔐︲Sécurité de base

### `enable secret PASSWORD`

* **But** : définir le mot de passe du mode privilégié
* **Effet réel** :

  * stocké en hash (sécurisé)
* **À savoir** :

  * remplace `enable password` (non sécurisé)
  * indispensable en production

---

### `service password-encryption`

* **But** : chiffrer les mots de passe dans la config
* **Effet réel** :

  * évite le stockage en clair dans `show running-config`
* **Limite** :

  * chiffrement faible (réversible)
  * utile pour éviter lecture directe, pas pour sécurité forte

---

## 📢︲Avertissement légal

### `banner motd # MESSAGE`

* **But** : afficher un message avant connexion
* **Effet réel** :

  * avertissement utilisateur (souvent obligatoire)
* **À savoir** :

  * le symbole (# ici) sert de délimiteur → doit être identique au début et à la fin

---

## 🔌︲Accès console (local)

### `line console 0`

* **But** : configurer l’accès via câble console
* **Effet réel** :

  * sécurise accès physique

### `password PASSWORD`

* **But** : définir mot de passe console

### `login`

* **But** : activer la demande de mot de passe
* **Piège critique** :

  * sans `login` → le mot de passe est ignoré

### `logging synchronous`

* **But** : éviter que les logs coupent la saisie
* **Effet réel** :

  * améliore lisibilité en console

---

## 🌐︲Accès distant (SSH)

### `line vty 0 4`

* **But** : configurer accès distant (5 connexions simultanées)

---

### `transport input ssh`

* **But** : autoriser uniquement SSH
* **Effet réel** :

  * bloque Telnet (non sécurisé)
* **À savoir** :

  * nécessite config SSH complète

---

### `ip domain-name lab.local`

* **But** : définir un domaine
* **Effet réel** :

  * requis pour génération des clés SSH

---

### `crypto key generate rsa`

* **But** : générer clés RSA
* **Effet réel** :

  * active SSH
* **À savoir** :

  * taille recommandée : 1024 ou 2048 bits

---

### `username admin secret PASSWORD`

* **But** : créer utilisateur local
* **Effet réel** :

  * utilisé pour connexion SSH
* **Piège** :

  * sans user → SSH inutilisable

---

## 💾︲Sauvegarde

### `copy running-config startup-config`

* **But** : sauvegarder la config
* **Effet réel** :

  * copie RAM → NVRAM
* **Piège critique** :

  * si oublié → tout est perdu au reboot

---
