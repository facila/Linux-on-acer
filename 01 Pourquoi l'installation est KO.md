## Pourquoi l'installation de Linux Mint ne marche-t-elle pas ?

ACER ne permet pas à Linux d'écrire dans son BIOS , même en ayant Secure Boot : [Disabled] , d'où les plantages

De plus , ACER n'autorise que le Boot Mode : [UEFI] avec des valeurs prédéfinies

	Windows Boot Manager 	: /EFI/Microsoft/Boot/bootmgfw.efi
	Linux			: /EFI/Boot/grubx64.efi
	
	La partition pour UEFI est en FAT32 , les majuscules/minuscules n'ont pas d'importance dans le nom du fichier
	Linux installe le répertoire /EFI/BOOT qui fonctionne de la même manière que /EFI/Boot

Linux Mint installe le fichier suivant dans la partition EFI

	/EFI/ubuntu/grubx64.efi

Le fichier de Linux n'est pas reconnu par le BIOS de l'ACER , d'où le redémarrage impossible

L'installation de Linux est une vraie galère , pour ne plus avoir ce genre de problème , il faudrait

	Soit que ACER modifie son BIOS et fasse comme tous les autres PC
	Soit que Linux Mint adapte l'installation de grub dans EFI/BOOT et n'essaye plus d'écrire dans le BIOS
	
