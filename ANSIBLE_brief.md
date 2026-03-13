# Brief_ANSIBLE

## Command & Control (C2) via Ansible

---

### Contexte du lab

#### VMware

* Lubuntu Master - **Ansible Host** : (192.168.72.129)
* Lubuntu Clone **Ansible Control Node** (192.168.72.255)

(même nom d'user pour les deux machines "serveur1")

---

### **Ansible Control Node**

#### Installation

    sudo apt update

    sudo apt install ansible

#### Creation repertoire  

    sudo mkdir /etc/ansible

#### Installer l'utilitaire de mot de passe

    sudo apt install sshpass -y

#### Créer l'inventaire

    nano /etc/ansible/inventory.ini

![alt text](Ansible_inventory-ini_1.png)

#### Configuration de clés SSH

![alt text](Gen_Key_Node.png)

    ssh-copy-id serveur1@192.168.72.129

#### Test (Ping)

![alt text](ping_serveur.png)

---

### **Playbooks**

**UPDATE_OS**

    nano 1-update-os.yml

![alt text](1-update-OS-YML.png)

**Exécution**

![alt text](playbook1_exc.png)

**CREATE_USER**

    nano 2-create-user.yml

![alt text](2-create_Usr-YML.png)

**Exécution**

![alt text](playbook2_exc.png)

**Test connexion ssh**

![alt text](Conexion_ssh-nvoUsr.png)

---
### **Ansible Host**

#### Renseignement d'un utilisateur autorisé sudoers

    sudo usermod -aG sudo devops

![alt text](Grp_sudo.png)
---

**DEPLOYMENT NGINX + SITE DEMO**

Preparations des répertoires + téléchargement des fichiers du site demo

![alt text](repertoires-files-SiteDemo.png)

    nano 3-create-site_web.yml

![alt text](3-create-site-YML.png)

**Exécution**

![alt text](3-create-site_web.png)

#### Test du site depuis un VM Windows

![alt text](Test.png)

---

### Creation fichier ansible.cfg

    nano ansible.cfg

![alt text](cat_ansible-cfg.png)

Test sans MDP (devops ajouté au visudo avec <devops ALL=(ALL) NOPASSWD:ALL> ) Ajout de MDP Plus tard avec **Ansible Vault**

![alt text](ansible-cfg.png)


---

## **Sécurisation des secrets avec Ansible Vault**

### **Création du coffre-fort (Vault)**

    ansible-vault create secrets.yml

![alt text](creation_vault.png)    

### Modification temporaire des fichiers inventory.ini et ansible.cfg

![alt text](Modif_inventory-ansible.png)

### Suppression de l'ancien user devops dans la machine host

![alt text](sup_devops.png)


### **Creation du password de "devops"**

#### Playbook

![alt text](4-mdp_devops-YML.png)

**Execution** 

![alt text](4-mdp_devops_exec.png)

**Test connexion ssh et ping**

![alt text](test_ping-2.png)

![alt text](Test_devops_2.png)

### Modification definitive inventory.ini et ansible.cfg

![alt text](inventory-ansible_definitif.png)

### Modification du vault pour ajouter `ansible_become_pass`

    ansible-vault edit secrets.yml

on ajoute la ligne : `ansible_become_pass: "{{ secret_password_devops }}"` #il appel la variable qu'on avait inséré avant (`secret_password_devops: "mon_mdp_devops"`) pour le mdp sudo.

### Modification du Playbook 1 (1-update-os.yml) de mise à jour pour test de Ansible Vault

![alt text](modif_playbook-1_vault.png)

**Execution**

![alt text](1-update-OS-YML_vault.png)









