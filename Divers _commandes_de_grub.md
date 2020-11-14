## Divers commandes de grub

Modifier une option au démarrage

    taper e pour edit sur une ligne du menu de grub
    modifier la ligne de commande , par exemple ajouter une option
    appuyer sur F10 pour démarrer
  
Ajouter une option par défaut

    editer et sauvegarder le fichier /etc/default/grub
    faire update-grub
 
Vérifier les variables de grub

    taper c sur le menu de grub
    le prompt grub> apparait
  
    ls  : affiche les disques et les partitions au format utilisé par grub
    set : affiche les variables de grub

    plusieurs variables déterminent les répertoires et les fichiers que grub utilise pour booter
    cmdpath , config_directory , config_file , prefix , root
    il faut donc que les fichiers soient au bon endroit
  
    en cas de problème , il est possible de modifier les variables et de d'exécuter un démarrage
    pour démarrer , taper :
    grub> insmod normal
    grub> normal
