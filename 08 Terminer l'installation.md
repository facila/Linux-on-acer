## Terminer l'installation

 	Arrêter le PC
	Si vous avez ajouté acpi=off à l'installation :
		faire un appui long sur le bouton marche/arrêt pour arrêter le PC
	Enlever la clé USB
	
	Si vous avez ajouté acpi=off à l'installation , test du démarrage et de l'arrêt du PC :
	1 : redémarrer le PC sans ajouter acpi=off
		si le PC démarre l'installation de Linux est terminée
		si le PC ne démarre pas , passer au point 2
	2 : redémarrer le PC en ajoutant acpi=off avec la fonction edit de grub
		ouvrir un terminal et taper la commande "reboot" ( redémarrage )
                lorsque le PC est à nouveau redémarré suite au reboot
                éteindre le PC , passer au point 3
	3 : redémarrer le PC sans ajouter acpi=off
		si le PC démarre l'installation de Linux est terminée
		si le PC ne démarre pas , passer au point 4
	4 : redémarrer le PC en ajoutant acpi=off avec la fonction edit de grub
		voir "05 grub option acpi"
	 	Ajouter acpi=off dans grub.cfg    

Si Linux est installé seul l'installation est terminée

Si Linux est installé avec Windows

	Appliquer la procédure : "09 Ajouter Windows dans grub"
