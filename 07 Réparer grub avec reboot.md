## Réparer grub avec reboot

Si le PC se plante , il est obligatoire de le redémarrer sur la clé USB

Cas rencontré avec Linux Mint 19.3

## Lancer un terminal et exécuter les commandes suivantes

	setxkbmap fr                                          si vous souhaitez passer le clavier en AZERTY ( taper setxbk,qp fr )
	sudo su
	fdisk -l                                              noter le nom de la partition EFI et de la partition root de Linux
	
	mount /dev/sda5 /mnt    		              si /dev/sda5 est la partition root de Linux
	mount /dev/sda1 /mnt/boot/efi		    	      si /dev/sda1 est la partition EFI
	for i in /dev /dev/pts /proc /sys ; do mount -B $i /mnt$i ; done
	
	apt-get install --reinstall grub-efi-amd64
	
	chroot /mnt                                           changement du root directory en /mnt
	grub-install --no-nvram                               création du fichier grubx64.efi , --no-nvram ne fait pas l'installation dans le BIOS
	cd /boot/efi/EFI
	cp ubuntu/grubx64.efi BOOT
	update-grub                                           création du fichier /boot/grub/grub.cfg
	
Si Linux est installé seul , l'installation est terminée

	Enlever la clé USB et redémarrer le PC
	Si acpi=off , faire un appui long sur le bouton marche/arret pour arreter le PC
        
Si Linux est installé avec Windows

  	Appliquer la procédure : "08 Ajouter Windows dans grub"
