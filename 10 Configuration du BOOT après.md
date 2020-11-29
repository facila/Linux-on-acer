## Configuration du BOOT de l'ACER après l'installation :

Au démarrage en appuyant sur F2

	Boot        : Boot priority order     : 1. Linux

Au démarrage en appuyant sur F12

	Titre : Boot Manager
	1. Linux

Il n'y a plus besoin de faire F12 pour démarrer , comme il n'y a qu'une entrée dans le BIOS , le PC démarre sur Linux grub

Linux devient le premier Boot dans le BIOS et Windows Boot Manager disparait

	efibootmgr -v
	BootCurrent: 0000 seconds
	BootOrder: 0000,2001,2002,2003
	Boot0000\* Linux HD(1,GPT,74e4d112-02f8-41bc-868e-d063f8d9,0x800,0x32000)/File(\EFI\Boot\grubx64.efi)RC
	Boot2001\* EFI USB Device	RC
	Boot2002\* EFI DVD/CDROM	RC
	Boot2003\* EFI Network	        RC


s
