# Installer Linux Mint sur un ACER Aspire ES17 ES1-732

	Date    : 01/10/2019
	Version : 1.00
	Auteur  : facila@gmx.fr

Je ne détaille pas l'installation de Linux Mint : partition , clé bootable , ... 
Je ne détaille pas non plus le fonctionnement général de EFI
Le problème n'est pas là , tous les tutos disponibles sur internet le font trés bien

J'explique comment installer Linux si vous avez fait l'erreur d'acheter un ACER et que vous rencontrerez les problèmes suivants :

- plantage à la fin de l'installation de linux
- plantage à l'installation ou la réparation de grub
- plantage sur la commande efibootmgr lorsque l'on essaye de modifier le BIOS

## Pourquoi l'installation de linux ne marche-t-elle pas ?

Dans son BIOS , ACER :
- ne permet pas à Linux d'écrire , même en ayant Secure Boot : [Disabled] , d'où les plantages
- n'autorise que le Boot Mode : [UEFI] avec 2 valeurs par défaut ( peut être plus , je ne sais pas )

	Windows Boot Manager 	: /EFI/Microsoft/Boot/bootmgfw.efi
	Linux					: /EFI/Boot/grubx64.efi

Linux Mint installe dans la partition EFI , par exemple /dev/sda1

	/EFI/ubuntu/shimx64.efi ou /EFI/ubuntu/grubx64.efi

Le fichier de Linux n'est donc pas reconnu par le BIOS de l'ACER

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

Exécuter l'installation de Linux
Juste avant la fin de l'installation , le PC se plante
L'installation de grub par Linux s'est quand même exécutée , mais l'écriture dans le BIOS n'étant pas permise le PC se plante

Redémarrer le PC sur la clé USB et exécuter les commandes suivantes

	sudo su
	mount /dev/sda1 /boot/efi				si sda1 est la partition EFI
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

au démarrage en appuyant sur F2

	Boot        : Boot priority order     : 1. Linux

au démarrage en appuyant sur F12

	Titre : Boot Manager
	1. Linux
	
Il n'y a plus besoin de faire F12 pour démarrer , comme il n'y a qu'une entrée dans le BIOS , le PC démarre sur Linux Grub	



## Modifier Linux pour réactiver Windows 10 dans grub

remplacer les entrées suivantes

	sudo vi /boot/grub/grub.cfg
	menuentry 'Windows Boot Manager (on /dev/sda1)' 	->	menuentry 'Windows 10'
	chainloader /EFI/Microsoft/Boot/bootmgfw.efi		->	chainloader /EFI/MS/Boot/bootmgfw.efi

grub retrouve alors le chemin pour démarrer Windows 10

## Comment faire autrement ?

Est-ce que quelqu'un à une autre solution ?

Existe-t-il une version de BIOS compatible ACER et Linux Mint ?

ACER peut-il changer de BIOS et faire comme les autres constructeurs ?


Linux Mint peut-il prendre en compte ce cas dans sa procédure d'installation ?
