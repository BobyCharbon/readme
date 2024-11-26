# Projet CIPEO Support

Bienvenue dans le projet CIPEO Support ! Ce projet vise à automatiser diverses tâches liées au support du CIPEO à l'aide de scripts Python.

## Prérequis
Avant de commencer, assurez-vous d'avoir installé les éléments suivants sur votre machine :
- `Git` : Pour installer Git sur votre MacOS, il vous faut Xcode. Il peut être trouvé directement depuis l'AppStore. 
- Une fois Xcode installé, ouvrez le terminal et tapez la commande: `git`. Une fenêtre d'installation Xcode s'ouvrira.
- GitKraken (pour voir un affichage graphique du projet, mais pas obligatoire) : https://gitkraken.com/download
- Toutes les autres dépendances du script s'installeront automatiquement.
- Être hors-réseau EDU-VD. En effet, certains packages sont bloqués par le filtre de contenu. Il est donc nécessaire d'être connecté à un partage de connexion ou tout autre Wi-Fi que EDU-VD / EDU-VD-PRO.

## Configuration initiale (MacOS)
1. Ouvrez le terminal.

2. Placez-vous dans votre dossier utilisateur :
   ```bash
   cd
   ``` 

4. Clonez ce dépôt en utilisant la commande suivante :
   ```bash
   commande protégée et donnée par Ludovic Trombert
   ```
   Une fois le git cloné, rentrer dans son dossier :
   ```bash
   cd CIPEO_support
   ```

5. Une fois dans le dossier CIPEO_support, exécutez le script d'installation avec la commande :
   ```bash
   ./install
   ```

6. Une fois l'installation des paquets terminée, le processus vous demandera si vous souhaitez installer les alias. Tapez 'y'.

7. Entrez le mot de passe de la session `supporteduvd`. Ce mot de passe sera stocké sur votre Mac pour des raisons de sécurité.

8. Quittez complètement le terminal et rouvrez-le.

9. Exécutez la commande suivante pour lancer le script :
   ```bash
   remote pause
   ```

10. Lorsque le lien Google Chrome s'ouvre, connectez-vous avec vos identifiants EDU-VD et cochez la case "Rester connecté".

11. Assurez-vous que la langue de Jamf est bien en `ANGLAIS`.

12. Dans Jamf, allez dans 'Settings'
    
14. Tapez dans la barre de recherche **'Inventory Display'** _(Computer Management pour le moment)_

15. Cocher les options ci-dessous dans Jamf:
    
   `COMPUTER:`
      Asset Tag / Computer name /Last Check-in /Last Enrollment /Last Reported IP Address

   `HARDWARE:`
      Model / Serial Number

   `OPERATING SYSTEM:`
      Active Directory Status / Number of Avalaible Updates / Operating System /  Operating System Version

   `SECURITY:`
      Remote Desktop Enabled / External Boot Level / Secure Boot Level

   `USER AND LOCATION:`
      Department / Room

   `STORAGE:`
      Boot Drive Available MB

   `EXTENSION ATTRIBUTES:`
      SecureTokenStatus / Bâtiment

_**Veuillez noter que si vous oubliez de cocher une case, les scripts ne fonctionneront pas. Toutefois, vous pouvez en ajouter d'autres selon vos préférences.**_

16. Tapez dans la barre de recherche **'Inventory Display'** _(Device Management)_

17. Cocher les options ci-dessous dans Jamf:
    
   `Mobile Device:`
      Available Space MB / Display Name / iOS Version / Last Enrollment / Last iCloud Backup / Last Iventory Update / Model / Quota Size / Serial Number / Shared iPad

_**Veuillez noter que si vous oubliez de cocher une case, les scripts ne fonctionneront pas. Toutefois, vous pouvez en ajouter d'autres selon vos préférences.**
_
18. Une fois les options cochées, appuyez sur `CTRL + C` dans le terminal pour quitter le script.

19. Installation terminée

## Commandes utiles
- `remote 'asset'`: Récupère les informations d'un poste (iMac ou Mac) depuis Jamf et Leonardo. Ouvre un partage d'écran si le poste est connecté au même réseau.

- `mobile 'asset'`: Récupère les informations d'un poste (Apple TV ou iPad) depuis Jamf et Leonardo.

- `ard 'asset1' 'asset2' 'asset3' etc.`: Effectue des partages d'écran simultanés avec plusieurs hôtes (iMac ou Mac).

- `leo 'asset1' 'asset2' 'asset3 etc.'`: Récupère les informations du/des poste directement depuis Leonardo. Il est plus rapide que le remote étant donné qu'il récupère le numéro de série depuis Leonardo.

- `leoserial 'asset1' 'asset2' 'asset3' etc.'` De la même manière que la commande `leo`, sauf qu'il renseigne les numéro de série dans Leo.`

- `localisation` `serial1` `serial2` `serial3 etc.` Ce script permet de localiser divers numéros de série au sein d'un bâtiment préalablement défini. Il offre la possibilité de sélectionner l'établissement, le bâtiment et la salle. Vous avez également la faculté d'ajouter un commentaire dans la section 'Commentaires CIPEO'. Le script est sensible à la casse, il est donc impératif de respecter les majuscules. De plus, il vous demandera le premier numéro d'asset et l'incrémentera à chaque numéro de série, ce qui s'avère pratique pour les déploiements. Cette fonctionnalité est compatible avec les ATV, iPad, Mac OS, ainsi que tout autre appareil devant être localisé. Veuillez manœuvrer cette commande avec précaution, car elle effectuera des changements de localisation de manière automatisée. À noter que le script fournira à la fin les anciennes localisations, au cas où une erreur aurait été commise.

- `man` `serial1` `serial2` `serial3 etc.` Récupère les infos de Leo/Jamf et check si le poste doit être refait ou en MàN.

- `broker` `serial1` `serial2` `serial3 etc.` Récupère les infos des postes pour le fichier du broker depuis Jamf ou une DB perso.

- `cmd` Affiche toutes les commandes disponibles et leur utilisation

- `prepare` Script pour refaire les disques. Vous devez être admin de votre poste

## Commandes importantes
- `./install` (dans le dossier /CIPEO_support): Réinstalle tous les composants en cas de problème ou de changement de poste.

- `python3 CIPEO_support/remove.py` Ce script supprime l'intégralité des fichiers/dossiers installés. Pratique lorsque nous voulons faire une réinstallation complète.

- `git pull` (dans le dossier /CIPEO_support): Met à jour le projet avec les dernières modifications de l'administrateur du Git.

- `git checkout -f` Si vous éprouvez des difficultés à effectuer un git pull et que la version locale de votre dépôt a été modifiée, utilisez la commande suivante pour restaurer la version originale. Ensuite, assurez-vous de récupérer toutes les dernières mises à jour depuis le dépôt distant avec la commande :
`git pull`

## Suggestions, questions, bugs
Si vous avez des suggestions pour améliorer le projet, que ce soit des fonctionnalités ou la remontée d'un problème, nous vous invitons à créer une **issue** en choisissant le label approprié :
 
https://github.com/BobyCharbon/CIPEO_support/issues/new

---
