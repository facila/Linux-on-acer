# Installer Linux Mint sur un ACER Aspire ES17 ES1-732

	Date    : 28/10/2020
	Version : 3.00
	Auteur  : facila@gmx.fr

J'explique comment installer Linux si comme moi vous avez un ACER et que vous rencontrez les problèmes suivants :

- plantage à la fin de l'installation de linux
- plantage à l'installation ou la réparation de grub
- plantage sur la commande efibootmgr lorsque l'on essaye de modifier le BIOS

Je ne détaille pas l'installation de Linux Mint : partition , clé bootable , ... 

Je ne détaille pas non plus le fonctionnement général de EFI

Le problème n'est pas là , tous les tutos disponibles sur internet le font trés bien

## Configuration du BIOS de l'ACER avant l'installation :

Appuyer sur F2 au démarrage pour entrer dans le BIOS

	Titre       : InsydeH20 Setup Utility : Rev 5.0
	Information : System BIOS Version     : 1.03 à 1.19
	Main        : F12 Boot Menu           : [Enabled]
	Security    : Supervisor Password Is  : Set  mettre un password pour pouvoir modifier Secure Boot
	Boot        : Boot Mode               : [UEFI]
	Boot        : Secure Boot             : [Disabled]
	Boot        : Boot priority order     : 1. Windows Boot Manager

## Configuration du BOOT de l'ACER avant l'installation :

Appuyer sur F12 au démarrage pour afficher le menu de Boot

	Titre : Boot Manager
	1. Windows Boot Manager
	
## Pourquoi l'installation de linux ne marche-t-elle pas ?

ACER ne permet pas à Linux d'écrire dans son BIOS , même en ayant Secure Boot : [Disabled] , d'où les plantages

ACER n'autorise que le Boot Mode : [UEFI] avec des valeurs prédéfinies

	Windows Boot Manager 	: /EFI/Microsoft/Boot/bootmgfw.efi
	Linux			: /EFI/Boot/grubx64.efi

Linux Mint installe le fichier suivant dans la partition EFI

	/EFI/ubuntu/grubx64.efi

Le fichier de Linux n'est pas reconnu par le BIOS de l'ACER , d'où le plantage

	Linux_Mint_19_ACER_ES17.md : Installation testée avec Linux Mint 19.1 et 19.3
	Linux_Mint_20_ACER_ES17.md : Installation testée avec Linux Mint 20 ( en cours )
