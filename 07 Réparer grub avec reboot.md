## Réparer grub avec reboot

Si le PC se plante , il est obligatoire de le redémarrer sur la clé USB

Malheureusement plusieurs cas peuvent se présenter à chaque mise à jour de Linux 

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

## Si cela ne fonctionne pas , il est possible que autre chose que grub ne soit pas correctement installé

	booter sans la clé
	sur le menu de grub , choisir : advanced
	démarrer sur la dernière version ayant fonctionnée ( choisir la deuxième ligne vmlinuz.... , ajouter acpi=off si nécessaire )
	
	verifier que tous les fichiers vmlinuz sont présents sous : /boot
	si il manque un fichier pour la dernière version , ouvrir un terminal en sudo su et executer la commande :
	dpkg --configure -a
	verifier que tous les fichiers vmlinuz sont présents sous : /boot
	redémarrer : reboot
	sur le menu de grub , choisir : Linux Mint ( la première ligne )
	
## Faire "08 Terminer l'installation"
