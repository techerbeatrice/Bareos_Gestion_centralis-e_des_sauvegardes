# Bareos : gestion centralisée des sauvegardes   

___

🔬 Installation, configuration et test de bareos

L'installation d'un serveur bareos
Pour cette mise en pratique, utlises un unique serveur GNU/Linux (qui peut évidemment être une VM) sur lequel tu dois donc installer postgresql (pour le catalogue) ainsi que l'ensemble des composants bareos qui s'installe par le méta-paquet bareos.

L'installation sur le même serveur de Bareos Webui

Procède ensuite à toute la partie tutorial qui t'amène à

Lancer et découvrir la console.
Lancer un premier job et faire ta première sauvegarde.
Faire une restauration des données sauvegardées.
Ajouter un client. Ce client est une deuxième machine (ou VM) sur laquelle tu installes uniquement bareos-fd.
Configurer le serveur et le client pour que la communication soit possible.
Lancer une sauvegarde sur le client.

___

**Installation du serveur bareos sur une vm debian**  

__  

Faire un **_sudo apt-get update && sudo apt upgrade_**     
Si refus, passer en root avec la commande **_su root_** pour ajouter votre nom d'utilisateur au **fichier sudoers** de debian pour avoir les droits d'exécuter des commandes   

pour ajouter mon nom d'utilisateur :  **_sudo adduser beatrice sudo_**, sortir du root avec **_exit_**     

ensuite refaire un **_sudo apt-get update && sudo apt updrade_**     

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/f584f271-5fd1-4a4c-8dff-7af2e5aa8607)

____

Connaître la version de son debian avec **_lsb_release -a_** pour pouvoir après, importer le référentiel et la clé de signature GPG propres à la version :     

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/f0cb7b05-6894-42aa-ba10-ed4213ebc291)

___

Exécutez les instructions ci-dessous pour ajouter le référentiel avec les packages et la clé les plus récents :   

Créez le fichier avec la commande suivante :   

**_sudo nano /etc/apt/sources.list.d/bareos.list_**     

Ajoutez le texte suivant dans le fichier puis sauvegardez-le :

**_deb http://download.bareos.org/bareos/release/latest/Debian_12/ /_**     

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/1584bc07-2944-4c16-b0e4-39c209157aa2)

____

Télécharger la clé et l’ajouter, entrez la commande suivante dans le terminal :

**_wget -q http://download.bareos.org/bareos/release/latest/Debian_12/Release.key -O- | apt-key add --_**  

https://download.bareos.org/current/Debian_12/Release

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/117d2580-6c14-4f14-83cf-5fc11954e79b)

___

S'affiche le message : **_apt-key est obsolète_** et **_Gérer les fichiers de trousseaux de clés dans trust.gpg.d_**    

Ici Debian veut que vous sépariez les clés GPG   
C'est un message d’avertissement ; « Gérer les fichiers de trousseaux de clés dans trust.gpg.d » et depuis 2020, ajouter une clé GPG pour les dépôts utilisés par apt ne doit plus se faire par le biais de la **_commande _apt-key_** ; celle-ci est déclaré obsolète ET ne doit plus être utilisée ! 

Debian ne veut pas que vous ajoutiez toutes les clés de signature dans le fichier unique **_/etc/apt/trusted.gpg_**. Il suggère d'utiliser un fichier séparé situé dans le répertoire **_/etc/apt/trusted.gpg.d_**.

wget -O /usr/share/keyrings/<un-nom>-archive-keyring.gpg https://depot.example.net/debian/<nom-fichier-cle>.gpg

donc nouvelle commande à taper : **sudo wget -O /usr/share/keyrings/<bareos-archive-keyring.gpg http://download.bareos.org/bareos/release/latest/Debian_12.0/Release.key -O- | sudo apt-key add - | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/bareos.gpg_**   

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/d62a8d5a-dc31-4a74-9442-9c2e6aa7cfd0)

____

sudo apt-get install bareos   
sudo apt-get install --yes bareos.com-director bareos.com-storage bareos.com-filedaemon bareos.com-database-postgresql bareos.com-bconsole   

____

**Autre méthode d'installation de Bareos qui ne fonctionne qu'avec debian 11 :**  

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/2bbc967d-d551-4806-b043-a9f5d6790c6e)

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/92875781-053c-46e7-b962-32133208a06c)





![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/9eecc873-7b23-424c-9d9e-75906121252e)

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/6ec5b064-b9f8-45cb-b7ee-f77ac0d5dfd9)

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/b301f4ed-5199-4a5a-b141-b69881f24266)

____

Installation de Bareos terminée :   

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/5b8eca60-fa1b-4558-9679-d4c1e75fa3ae)

___

Ouvrir un mavigateur web et saisir l’url de Bareos :   
