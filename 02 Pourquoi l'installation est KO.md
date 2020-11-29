## Pourquoi l'installation de linux ne marche-t-elle pas ?

ACER ne permet pas à Linux d'écrire dans son BIOS , même en ayant Secure Boot : [Disabled] , d'où les plantages

De plus , ACER n'autorise que le Boot Mode : [UEFI] avec des valeurs prédéfinies

	Windows Boot Manager 	: /EFI/Microsoft/Boot/bootmgfw.efi
	Linux			: /EFI/Boot/grubx64.efi
	
	La partition pour UEFI est en FAT32 , les majuscules/minuscules n'ont pas d'importance dans le nom du fichier
	Linux installe le répertoire /EFI/BOOT qui fonctionne de la même manière que /EFI/Boot

Linux Mint installe le fichier suivant dans la partition EFI

	/EFI/ubuntu/grubx64.efi

Le fichier de Linux n'est pas reconnu par le BIOS de l'ACER , d'où le redémarrage impossible

Appliquer la procèdure suivante pour corriger les problèmes

	Linux_Mint_19_ACER_ES17.md : Installation testée avec Linux Mint 19.1 et 19.3
	Linux_Mint_20_ACER_ES17.md : Installation testée avec Linux Mint 20 ( en cours )