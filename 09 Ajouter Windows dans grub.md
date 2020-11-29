## Ajouter Windows dans grub , si vous voulez garder Windows en dual boot
	
ACER ne permet pas de changer l'ordre de Boot entre Windows et Linux dans le BIOS

Si Windows Boot Manager existe il est toujours démarré en premier

Il faut passer par F12 pour démarrer Linux

Redémarrer le PC en appuyant sur F12

	Titre : Boot Manager
	1. Windows Boot Manager
	2. Linux

Sélectionner 2 et valider , le PC démarre sur Linux

Pour ajouter Windows dans grub , passer les commandes suivantes 

	sudo su
	update-grub                                               pour la prise en compte de Windows par os-prober
	mv /boot/efi/EFI/Microsoft /boot/efi/EFI/MS	 	  pour supprimer Windows Boot Manager du menu de Boot

	vi /boot/grub/grub.cfg                                    remplacer les entrées suivantes
		menuentry 'Windows Boot Manager (on /dev/sda1)'   ->	menuentry 'Windows 10'
		chainloader /EFI/Microsoft/Boot/bootmgfw.efi	  ->	chainloader /EFI/MS/Boot/bootmgfw.efi

	Avec le nom MS , chaque modification de grub supprimera le bloc Windows 10
	Il faut donc déplacer le bloc de Windows 10 de la section 30_os-prober dans le fichier /etc/grub.d/40_custom
	
	Selectionner et couper le bloc : menuentry 'Windows 10' de la section ### BEGIN /etc/grub.d/30_os-prober ###
	
	vi /etc/grub.d/40_custom
		Coller dans le fichier 

	escape :x!                                                sauvegarder et quitter les fichiers dans vi

	update-grub                                               pour la prise en compte du fichier /etc/grub.d/40_custom

grub retrouve alors le chemin pour démarrer Windows 10 , l'installation est terminée , redémarrer le PC

Au démarrage en appuyant sur F12

	Titre : Boot Manager
	1. Linux
