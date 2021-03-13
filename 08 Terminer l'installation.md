## Terminer l'installation

 	Arrêter le PC
	Si vous avez ajouté acpi=off à l'installation :
		faire un appui long sur le bouton marche/arrêt pour arrêter le PC
	Enlever la clé USB
	
	1 : redémarrer le PC sans ajouter acpi=off
	    si le PC démarre l'installation de Linux est terminée
	    sinon passer au point 2
	
	2 : Il est possible que le passage par un reboot du PC règle le problème de l'acpi=off
  	    redémarrer le PC en ajoutant acpi=off avec la fonction edit de grub
	    ouvrir un terminal et taper la commande "reboot" ( redémarrage )
	    attendre que le PC redémarre suite au reboot
	    éteindre le PC	

	3 : redémarrer le PC sans ajouter acpi=off
	    si le PC démarre l'installation de Linux est terminée
	    sinon passer au point 4

	4 : redémarrer le PC en ajoutant acpi=off avec la fonction edit de grub
	    voir "05 grub option acpi"
	    Ajouter acpi=off dans grub.cfg    

Si Linux est installé seul l'installation est terminée

Si Linux est installé avec Windows

	Appliquer la procédure : "09 Ajouter Windows dans grub"
