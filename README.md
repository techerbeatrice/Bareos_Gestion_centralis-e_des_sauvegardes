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

**Installation du serveur bareos sur une vm ubuntu 22.04.1**  

__

**Mettre à jour Ubuntu avant d'installer les packages logiciels. Exécutez les commandes suivantes pour ce faire**    
 
_sudo apt update_   
_sudo apt dist-upgrade_   
_sudo apt autoremove_   

Cela devrait mettre Ubuntu à jour et supprimer tous les packages obsolètes de votre système. C'est également une bonne idée de réinitialiser l'ordinateur une fois la mise à jour terminée.
____

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
C'est un message d’avertissement ; « Gérer les fichiers de trousseaux de clés dans trust.gpg.d ».  

Ubuntu ne veut pas que vous ajoutiez toutes les clés de signature dans le fichier unique /etc/apt/trusted.gpg. Il suggère d'utiliser un fichier séparé situé dans le répertoire /etc/apt/trusted.gpg.d.    
____

sudo apt-get install bareos   
sudo apt-get install --yes bareos.com-director bareos.com-storage bareos.com-filedaemon bareos.com-database-postgresql bareos.com-bconsole   


