## Ajouter Windows dans grub
	
	Date    : 28/10/2020
	Version : 3.00
	Auteur  : facila@gmx.fr

ACER ne permet pas de changer l'ordre de Boot entre Windows et Linux dans le BIOS

si Windows Boot Manager existe il est toujours démarré en premier

il faut passer par F12 pour démarrer Linux

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
	Coller dans le fichier /etc/grub.d/40_custom

	escape :x!                                                sauvegarder et quitter les fichiers dans vi

	update-grub                                               pour la prise en compte du fichier /etc/grub.d/40_custom

grub retrouve alors le chemin pour démarrer Windows 10 , l'installation est terminée , redémarrer le PC

## Affichage des nouvelles configurations

Au démarrage en appuyant sur F2

	Boot        : Boot priority order     : 1. Linux

Au démarrage en appuyant sur F12

	Titre : Boot Manager
	1. Linux

Il n'y a plus besoin de faire F12 pour démarrer , comme il n'y a qu'une entrée dans le BIOS , le PC démarre sur Linux Grub

Linux devient le premier Boot dans le BIOS et Windows Boot Manager disparait

	efibootmgr -v
	BootCurrent: 0000 seconds
	BootOrder: 0000,2001,2002,2003
	Boot0000\* Linux HD(1,GPT,74e4d112-02f8-41bc-868e-d063f8d9,0x800,0x32000)/File(\EFI\Boot\grubx64.efi)RC
	Boot2001\* EFI USB Device	RC
	Boot2002\* EFI DVD/CDROM	RC
	Boot2003\* EFI Network	        RC

## Mises à jour de Windows

Lors des mises à jour , il est possible que la configuration du boot soit modifiée et que le PC ne redémarre plus

Redémarrer le PC sur la clé USB et exécuter les commandes suivantes

	setxkbmap fr                                            si vous souhaitez passer le clavier en AZERTY
	sudo su
	mount /dev/sda1 /boot/efi				si /dev/sda1 est la partition EFI
	cd /boot/efi/EFI
	si les répertoires MS et Microsoft existent , passer les commandes suivantes
	mv MS MS.old
	mv Microsoft MS

Enlever la clé USB , redémarrer et refaire la procédure pour ajouter Windows dans grub
