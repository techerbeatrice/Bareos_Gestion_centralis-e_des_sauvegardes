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




Après avoir mis à niveau Ubuntu, vous devrez **ajouter le référentiel Bareos et le fichier clé à votre ordinateur**. Les packages les plus récents seront mis à disposition sur votre machine dès que son référentiel sera ajouté.   

Exécutez les instructions ci-dessous pour ajouter le référentiel avec les packages et la clé les plus récents :   

_sudo sh -c 'echo "deb http://download.bareos.org/bareos/release/latest//xUbuntu_22.04.1 /" >> /etc/apt/sources.list.d/bareos.list'_

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/9a82dbc2-825e-4bc5-b075-586b9b5f4af2)

____

Après avoir ajouté le référentiel, exécutez les instructions suivantes pour **importer la clé GPG du référentiel** :   

_sudo wget -q http://download.bareos.org/bareos/release/latest/xUbuntu_22.04.1/Release.key -O- | sudo apt-key add -_  

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralisee_des_sauvegardes/assets/138071140/ec25c298-b700-4c08-9630-cec878917d55)

S'affiche le message : _apt-key est obsolète_ et _Gérer les fichiers de trousseaux de clés dans trust.gpg.d_  

Ici Ubuntu veut que vous sépariez les clés GPG   
C'est un message d’avertissement ; « Gérer les fichiers de trousseaux de clés dans trust.gpg.d » et depuis 2020, ajouter une clé GPG pour les dépôts utilisés par apt ne doit plus se faire par le biais de la commande _apt-key_ ; celle-ci est déclaré obsolète ET ne doit plus être utilisée ! 

Ubuntu ne veut pas que vous ajoutiez toutes les clés de signature dans le fichier unique /etc/apt/trusted.gpg. Il suggère d'utiliser un fichier séparé situé dans le répertoire /etc/apt/trusted.gpg.d.   

donc nouvelle commande à taper : _sudo wget -q http://download.bareos.org/bareos/release/latest/xUbuntu_22.04.1/Release.key -O- | sudo apt-key add - | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/bareos.gpg_  


____

sudo apt-get install bareos   
sudo apt-get install --yes bareos.com-director bareos.com-storage bareos.com-filedaemon bareos.com-database-postgresql bareos.com-bconsole   


