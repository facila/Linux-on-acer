## Réparer grub avec reboot

Si le PC se plante , il est obligatoire de le redémarrer sur la clé USB

Malheureusement plusieurs cas peuvent se présenter à chaque mise à jour de Linux 

## Lancer un terminal et exécuter les commandes suivantes

	setxkbmap fr                                          si vous souhaitez passer le clavier en AZERTY ( taper setxbk,qp fr )
	sudo su ou su -
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
	sur le menu de grub , choisir : options advancées ( deuxième ligne )
	démarrer sur la dernière version ayant fonctionnée , choisir : x-x-x generic ( deuxième ligne )
	editer et ajouter acpi=off si nécessaire
	
	verifier que tous les fichiers initrd.img et vmlinuz sont présents : ll /boot
	si il manque un fichier pour la dernière version
	ouvrir un terminal en root sudo su et exécuter la commande : dpkg --configure -a
	si un message d'erreur s'affiche sur l'installation de grub , continuer l'installation 
	verifier que tous les fichiers initrd.img et vmlinuz sont présents : ll /boot
	redémarrer : reboot
	sur le menu de grub , choisir : Linux Mint ( la première ligne , démarrage normal )
	
	Si vous avez de multiples versions suite aux différentes mises à jour
	vous pouvez faire un peu de ménage en supprimant celle qui sont devenues inutiles ( cela n'est pas obligatoire )
	ouvrir un terminal en sudo su ou su - et exécuter la commande : apt autoremove
	verifier les fichiers présents : ll /boot

## Faire "08 Terminer l'installation"
