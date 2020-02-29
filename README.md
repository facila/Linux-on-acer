# Installer Linux Mint sur un ACER Aspire ES17 ES1-732
	Date    : 29/02/2020
	Version : 1.02
	Auteur  : facila@gmx.fr

Je ne détaille pas l'installation de Linux Mint : partition , clé bootable , ... 

Je ne détaille pas non plus le fonctionnement général de EFI

Le problème n'est pas là , tous les tutos disponibles sur internet le font trés bien

J'explique comment installer Linux si comme moi vous avez un ACER et que vous rencontrerez les problèmes suivants :

- plantage à la fin de l'installation de linux
- plantage à l'installation ou la réparation de grub
- plantage sur la commande efibootmgr lorsque l'on essaye de modifier le BIOS

## Pourquoi l'installation de linux ne marche-t-elle pas ?

ACER ne permet pas à Linux d'écrire dans son BIOS , même en ayant Secure Boot : [Disabled] , d'où les plantages

ACER n'autorise que le Boot Mode : [UEFI] avec 2 valeurs par défaut ( peut être plus , je ne sais pas )

	Windows Boot Manager 	: /EFI/Microsoft/Boot/bootmgfw.efi
	Linux			: /EFI/Boot/grubx64.efi

Linux Mint installe dans la partition EFI , par exemple /dev/sda1

	/EFI/ubuntu/shimx64.efi ou /EFI/ubuntu/grubx64.efi

Le fichier de Linux n'est donc pas reconnu par le BIOS de l'ACER

Il faut donc copier le fichier créé par Linux Mint en /EFI/Boot/grubx64.efi

Et si windows est installé , déplacer le fichier /EFI/Microsoft/Boot/bootmgfw.efi dans un autre répertoire

## Configuration du BIOS de l'ACER :

Appuyer sur F2 au démarrage pour entrer dans le BIOS

	Titre       : InsideH20 Setup Utility : Rev 5.0
	Information : System BIOS Version     : 1.03 à 1.19
	Main        : F12 Boot Menu           : [Enabled]
	Security    : Supervisor Password Is  : Set	mettre un password pour pouvoir modifier Secure Boot
	Boot        : Boot Mode               : [UEFI]
	Boot        : Secure Boot             : [Disabled]
	Boot        : Boot priority order     : 1. Windows Boot Manager

Appuyer sur F12 au démarrage pour afficher le menu de Boot

	Titre : Boot Manager
	1. Windows Boot Manager
	
## Installer Linux Mint à partir d'une clé USB bootable

Créer une clé USB bootable sur Linux Mint ( voir la procédure sur internet )

Je vous conseille ensuite de garder cette clé qui pourra servir en cas de problème

Exécuter l'installation de Linux

Juste avant la fin de l'installation , le PC se plante

L'installation de grub par Linux s'est quand même exécutée , mais l'écriture dans le BIOS n'étant pas permise le PC se plante

Redémarrer le PC sur la clé USB et exécuter les commandes suivantes

	setxkbmap fr                                            si vous souhaitez passer le clavier en AZERTY
	sudo su
	fdisk -l                                                noter le nom de la partition EFI
	mkdir /boot/efi
	mount /dev/sda1 /boot/efi				si /dev/sda1 est la partition EFI
	cd /boot/efi
	mkdir EFI/Boot
	cp EFI/ubuntu/shimx64.efi EFI/Boot/grubx64.efi		si shimx64.efi est le fichier installé par Linux
	
Enlever la clé USB et redémarrer le PC en appuyant sur F12

	Titre : Boot Manager
	1. Windows Boot Manager
	2. Linux

Sélectionner 2 et valider , le PC démarre sur Linux

ACER ne permet pas de changer l'ordre de Boot dans le BIOS , si Windows Boot Manager existe il est toujours en premier 
Actuellement , il faut passer par F12 pour démarrer Linux

## Modifier Linux pour activer le démarrage avec grub

	sudo su
	mount /dev/sda1 /boot/efi				si sda1 est la partition EFI
	cd /boot/efi/EFI
	mv Microsoft MS						MS ou un autre nom de votre choix

Windows Boot Manager n'est alors plus vu par le BIOS

	efibootmgr -v
	BootCurrent: 0000 seconds
	BootOrder: 0000,2001,2002,2003
	Boot0000\* Linux HD(1,GPT,74e4d112-02f8-41bc-868e-d063f8d9,0x800,0x32000)/File(\EFI\Boot\grubx64.efi)RC
	Boot2001\* EFI USB Device	RC
	Boot2002\* EFI DVD/CDROM	RC
	Boot2003\* EFI Network	 RC

Au démarrage en appuyant sur F2

	Boot        : Boot priority order     : 1. Linux

Au démarrage en appuyant sur F12

	Titre : Boot Manager
	1. Linux
	
Il n'y a plus besoin de faire F12 pour démarrer , comme il n'y a qu'une entrée dans le BIOS , le PC démarre sur Linux Grub	

## Modifier Linux pour réactiver Windows 10 dans grub

Modifier le fichier grub.cfg

	sudo vi /boot/grub/grub.cfg
	
Remplacer les entrées suivantes
	
	menuentry 'Windows Boot Manager (on /dev/sda1)' 	->	menuentry 'Windows 10'
	chainloader /EFI/Microsoft/Boot/bootmgfw.efi		->	chainloader /EFI/MS/Boot/bootmgfw.efi

Les mises à jour de Linux peuvent recréer le bloc Windows d'origine

Il faut donc déplacer le bloc de Windows 10 de la section 10_linux à la section 40_custom

	selectionner et couper le bloc : menuentry 'Windows 10' de la section ### BEGIN /etc/grub.d/10_linux ###
	coller le bloc dans la section : ### BEGIN /etc/grub.d/40_custom ###
	
Sauvegarder et quitter le fichier dans vi

	escape :x

grub retrouve alors le chemin pour démarrer Windows 10

## Mise à jour de Windows

Lors des mises à jour , il est possible que la configuration du boot soit modifiée et que le PC ne redémarre plus

Redémarrer le PC sur la clé USB et exécuter les commandes suivantes

	setxkbmap fr                                            si vous souhaitez passer le clavier en AZERTY
	sudo su
	mount /dev/sda1 /boot/efi				si /dev/sda1 est la partition EFI
	cd /boot/efi/EFI
	ll
	si les répertoires MS et Microsoft existent , passer la comme suivante
	mv Microsoft Microsoft.old
	
Enlever la clé USB et redémarrer

## Comment faire autrement ?

Est-ce que quelqu'un à une autre solution ?

Existe-t-il une version de BIOS compatible ACER et Linux Mint ?

ACER peut-il changer de BIOS et faire comme les autres constructeurs ?

Linux Mint peut-il prendre en compte ce cas dans sa procédure d'installation ?
