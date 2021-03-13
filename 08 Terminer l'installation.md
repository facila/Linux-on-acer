## Terminer l'installation

	Enlever la clé USB et redémarrer le PC
	Si vous avez ajouté acpi=off :
	faire un appui long sur le bouton marche/arret pour arrêter le PC
	
	Test de acpi=off :
	1 : redémarrer le PC sans ajouter acpi=off
		si le PC démarre l'installation est terminée
		si le PC ne démarre pas , passer au point 2
	2 : redémarrer le PC en ajoutant acpi=off avec la fonction edit de grub
		ouvrir un terminal et taper la commande "reboot" ( redémarrage )
                lorsque le PC est à nouveau redémarré suite au reboot
                éteindre le PC
	3 : si le PC ne démarre pas sans acpi=off
		voir "05 grub option acpi"
	 	Ajouter acpi=off dans grub.cfg    

Si Linux est installé seul l'installation est terminée

Si Linux est installé avec Windows

	Appliquer la procédure : "09 Ajouter Windows dans grub"
