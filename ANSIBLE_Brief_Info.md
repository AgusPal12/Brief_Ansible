# Command & Control (C2) via Ansible

Mise en place d'une administration centralisée et sécurisée via Ansible.

L'apprenant doit configurer un nœud de contrôle sous Ubuntu 24.04, établir un inventaire, et rédiger une série de playbooks YAML.
L'objectif est d'automatiser le durcissement d'un serveur cible (mise à jour, sécurisation des accès via clés SSH) et le déploiement reproductible d'un service web (Nginx).**

## Contexte du projet

En tant que administrateur d'Infrastructures Sécurisées, dans le cadre de
la remédiation et de l'application de la politique de sécurité, les
actions suivantes doivent être réalisées :

* Préparation de
  l'outillage : Déployer un nœud de contrôle Ansible sous Ubuntu 24.04
  pour centraliser la gestion des configurations.
* Durcissement du
  système (Mise en œuvre de la politique - C9) : Développer et exécuter un
  Playbook Ansible chargé de forcer la mise à jour complète de l'OS
  (application des correctifs de sécurité).
* Sécurisation des accès
  (Mise en œuvre de la politique - C9) : Rédiger un Playbook pour
  industrialiser la création de comptes de service dédiés, intégrant le
  déploiement de clés SSH et limitant l'usage des mots de passe.
* Déploiement
  standardisé : Créer un Playbook pour installer et configurer un service
  Nginx et déployer une page web de façon reproductible.
* Validation
  (Mesure et analyse - C8) : Effectuer des tests de connexion
  post-déploiement (ping SSH sans mot de passe, vérification du statut
  Nginx) pour analyser et valider que le niveau de sécurité attendu est
  bien atteint sur la cible.

## Modalités pédagogiques

* Format : Travail individuel
* Durée estimée : 8 heures (modulable selon le niveau initial).
* Environnement
  technique : Mise à disposition de 2x Container LXC Ubuntu 24.04 par
  environnement de travail (1 Controller, 1 Cible).

## Modalités d'évaluation

Évaluation sommative (Restitution) : Démonstration technique finale (5 minutes par apprenant) où l'apprenant exécute ses playbooks devant le formateur sur un environnement vierge pour prouver l'automatisation.
Revue de code : Analyse des fichiers YAML pour vérifier le respect des bonnes pratiques (indentation, clarté, commentaires).

## Livrables

Un dossier compressé (ou un dépôt Git) contenant obligatoirement :

- Le fichier d'inventaire (inventory.ini)
- Les 3 playbooks documentés (1-update-os.yml, 2-create-user.yml, 3-deploy-website.yml)
- Le fichier source de la page web (index.html)
- Un court fichier README.md expliquant les commandes exactes à taper pour exécuter les playbooks dans le bon ordre

## Critères de performance

Fonctionnalité : Les playbooks s'exécutent de bout en bout sans erreur (code retour OK)
Sécurité (C8/C9) : Le compte de service est bien créé sur la cible, la clé publique SSH est correctement déployée, et l'accès SSH via cette clé fonctionne sans interaction manuelle.
Disponibilité : Le serveur web Nginx est actif, exposé sur le port 80, et affiche la page HTML personnalisée définie dans le playbook.
