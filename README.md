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

**Installation du serveur bareos**  

___

**Mettre à jour Ubuntu avant d'installer les packages logiciels. Exécutez les commandes suivantes pour ce faire**    
 
sudo apt update   
sudo apt dist-upgrade   
sudo apt autoremove   

Cela devrait mettre Ubuntu à jour et supprimer tous les packages obsolètes de votre système. C'est également une bonne idée de réinitialiser l'ordinateur une fois la mise à jour terminée.
____

Après avoir mis à niveau Ubuntu, vous devrez ajouter le référentiel Bareos et le fichier clé à votre ordinateur. Les packages les plus récents seront mis à disposition sur votre machine dès que son référentiel sera ajouté.   

Exécutez les instructions ci-dessous pour ajouter le référentiel avec les packages et la clé les plus récents :   

____

Passer en root avec _sudo su_ et télécharger la clé avec _sudo wget -q http://download.bareos.org/bareos/release/latest/Ubuntu_22.04.1/Release.key -O- | apt-key add --_  

sudo apt-get install bareos   
sudo apt-get install --yes bareos.com-director bareos.com-storage bareos.com-filedaemon bareos.com-database-postgresql bareos.com-bconsole   

![image](https://github.com/techerbeatrice/Bareos_Gestion_centralis-e_des_sauvegardes/assets/138071140/3bc781c4-2ade-4e0b-8122-a12295695803)
