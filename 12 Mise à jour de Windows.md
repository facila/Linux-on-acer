## Mise à jour de Windows

Lors des mises à jour , il est possible que la configuration du boot soit modifiée et que le PC ne redémarre plus

Redémarrer le PC sur la clé USB et exécuter les commandes suivantes

	setxkbmap fr                                            si vous souhaitez passer le clavier en AZERTY
	sudo su
	mount /dev/sda1 /boot/efi				si /dev/sda1 est la partition EFI
	cd /boot/efi/EFI
	si les répertoires MS et Microsoft existent , passer les commandes suivantes
	mv MS MS.old
	mv Microsoft MS

Enlever la clé USB et redémarrer

Refaire la procédure "09 Ajouter Windows dans grub" si nécessaire
