# Installer Linux Mint 19 sur un ACER Aspire ES17 ES1-732

	Date    : 28/10/2020
	Version : 3.00
	Auteur  : facila@gmx.fr
       	
## 1 : Installer Linux Mint à partir d'une clé USB bootable

Créer une clé USB bootable sur Linux Mint ( voir la procédure sur internet )

Je vous conseille ensuite de garder cette clé qui pourra servir en cas de problème

Exécuter l'installation de Linux

Juste avant la fin de l'installation sur grub2 , le PC se plante

L'écriture dans le BIOS n'étant pas permise le PC se plante et l'installation de grub par Linux ne se termine pas bien

## 2 : Réinstaller grub manuellement à partir de la clé USB

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
	
	chroot /mnt                                           changement du root directory en /mnt
	rm -rf /boot/efi/EFI/BOOT
	mv /boot/efi/EFI/ubuntu /boot/efi/EFI/Boot            renommer le répertoire créé par Linux Mint /EFI/ubuntu en /EFI/Boot

	update-grub                                           création du fichier /boot/grub/grub.cfg
	
Si Linux est installé seul , l'installation est terminée

	Enlever la clé USB et redémarrer le PC
        
Si Linux est installé avec Windows

  	Appliquer la procédure : Ajouter Windows dans grub
