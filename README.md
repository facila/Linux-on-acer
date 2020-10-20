# Installer Linux Mint sur un ACER Aspire ES17 ES1-732

	Date    : 20/10/2020
	Version : 2.00
	Auteur  : facila@gmx.fr

Installation testée avec Linux Mint 19.1 et 19.3

Cette procèdure ne marche pas avec Linux Mint 20 , l'ACER Aspire ES17 ne boot pas sur la clé usb dans cette version

Je ne détaille pas l'installation de Linux Mint : partition , clé bootable , ... 

Je ne détaille pas non plus le fonctionnement général de EFI

Le problème n'est pas là , tous les tutos disponibles sur internet le font trés bien

J'explique comment installer Linux si comme moi vous avez un ACER et que vous rencontrerez les problèmes suivants :

- plantage à la fin de l'installation de linux
- plantage à l'installation ou la réparation de grub
- plantage sur la commande efibootmgr lorsque l'on essaye de modifier le BIOS

## Configuration du BIOS et du BOOT de l'ACER avant l'installation :

Appuyer sur F2 au démarrage pour entrer dans le BIOS

	Titre       : InsydeH20 Setup Utility : Rev 5.0
	Information : System BIOS Version     : 1.03 à 1.19
	Main        : F12 Boot Menu           : [Enabled]
	Security    : Supervisor Password Is  : Set	mettre un password pour pouvoir modifier Secure Boot
	Boot        : Boot Mode               : [UEFI]
	Boot        : Secure Boot             : [Disabled]
	Boot        : Boot priority order     : 1. Windows Boot Manager

Appuyer sur F12 au démarrage pour afficher le menu de Boot

	Titre : Boot Manager
	1. Windows Boot Manager
	
## Pourquoi l'installation de linux ne marche-t-elle pas ?

ACER ne permet pas à Linux d'écrire dans son BIOS , même en ayant Secure Boot : [Disabled] , d'où les plantages

ACER n'autorise que le Boot Mode : [UEFI] avec 2 valeurs par défaut ( peut être plus , je ne sais pas )

	Windows Boot Manager 	: /EFI/Microsoft/Boot/bootmgfw.efi
	Linux			: /EFI/Boot/grubx64.efi

Linux Mint installe le fichier suivant dans la partition EFI

	/EFI/ubuntu/grubx64.efi

Le fichier de Linux n'est pas reconnu par le BIOS de l'ACER , il faut donc :
	
	1 : Installer Linux Mint à partir d'une clé USB bootable
	2 : Réinstaller grub
	3 : Modifier grub.cfg pour prendre en compte Windows
        	
## 1 : Installer Linux Mint à partir d'une clé USB bootable

Créer une clé USB bootable sur Linux Mint ( voir la procédure sur internet )

Je vous conseille ensuite de garder cette clé qui pourra servir en cas de problème

Exécuter l'installation de Linux

Juste avant la fin de l'installation sur grub2 , le PC se plante

L'écriture dans le BIOS n'étant pas permise le PC se plante et l'installation de grub par Linux ne se termine pas bien

## 2 : Réinstaller grub

Redémarrer le PC sur la clé USB et exécuter les commandes suivantes

	setxkbmap fr                                          si vous souhaitez passer le clavier en AZERTY ( taper setxbk,qp fr )
	sudo su
	fdisk -l                                              noter le nom de la partition EFI et de la partition root de Linux
	
	mount /dev/sda5 /mnt    		              si /dev/sda5 est la partition root de Linux
	mount /dev/sda1 /mnt/boot/efi		    	      si /dev/sda1 est la partition EFI
	for i in /dev /dev/pts /proc /sys ; do mount -B $i /mnt$i ; done
	
	rm -rf /mnt/boot/efi/EFI/ubuntu
	apt-get install --reinstall grub-efi-amd64
	grub-install --no-nvram --root-directory=/mnt         création du fichier grubx64.efi , --no-nvram ne fait pas l'installation dans le BIOS
	
	rm -rf /mnt/boot/efi/EFI/BOOT
	mv /mnt/boot/efi/EFI/ubuntu /mnt/boot/efi/EFI/Boot    renommer le répertoire créé par Linux Mint /EFI/ubuntu en /EFI/Boot
	
	chroot /mnt                                           changement du root directory en /mnt
	update-grub                                           création du fichier /boot/grub/grub.cfg
	
Si Linux est installé seul , l'installation est terminée

	Enlever la clé et redémarrer le PC
        
Si linux est installé avec Windows , continuer au point 3
	
## 3 : Modifier grub.cfg pour prendre en compte Windows

Enlever la clé USB et redémarrer le PC en appuyant sur F12

	Titre : Boot Manager
	1. Windows Boot Manager
	2. Linux

Sélectionner 2 et valider , le PC démarre sur Linux

ACER ne permet pas de changer l'ordre de Boot dans le BIOS , si Windows Boot Manager existe il est toujours en premier

Actuellement , il faut passer par F12 pour démarrer Linux

	sudo su
        update-grub                                             pour la prise en compte de Windows par os-prober
	mv /boot/efi/EFI/Microsoft /boot/efi/EFI/MS	 	MS ou un autre nom de votre choix

	vi /boot/grub/grub.cfg
           Remplacer les entrées suivantes
	     menuentry 'Windows Boot Manager (on /dev/sda1)' 	->	menuentry 'Windows 10'
	     chainloader /EFI/Microsoft/Boot/bootmgfw.efi	->	chainloader /EFI/MS/Boot/bootmgfw.efi

	   Les mises à jour de Linux peuvent recréer le bloc Windows d'origine
           Il faut donc déplacer le bloc de Windows 10 de la section 30_os-prober à la section 40_custom
           Selectionner et couper le bloc : menuentry 'Windows 10' de la section ### BEGIN /etc/grub.d/30_os-prober ###
  	   Coller le bloc dans la section : ### BEGIN /etc/grub.d/40_custom ###
	
	escape :x!                                              Sauvegarder et quitter le fichier dans vi

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
	Boot2003\* EFI Network	 RC
	
## Mise à jour de Windows

Lors des mises à jour , il est possible que la configuration du boot soit modifiée et que le PC ne redémarre plus

Redémarrer le PC sur la clé USB et exécuter les commandes suivantes

	setxkbmap fr                                            si vous souhaitez passer le clavier en AZERTY
	sudo su
	mount /dev/sda1 /boot/efi				si /dev/sda1 est la partition EFI
	cd /boot/efi/EFI
	si les répertoires MS et Microsoft existent , passer la comme suivante
	mv MS MS.old
	mv Microsoft MS
	
Enlever la clé USB et redémarrer

## Comment faire autrement ?

Est-ce que quelqu'un à une autre solution ?

Existe-t-il une version de BIOS compatible ACER et Linux Mint ?

ACER peut-il changer de BIOS et faire comme les autres constructeurs ?

Linux Mint peut-il prendre en compte ce cas dans sa procédure d'installation ?
