## Réparer grub sans reboot

Si l'installation de grub échoue , mais que le PC ne se plante pas , il est possible de réparer grub sans rebooter

Cas rencontré avec Linux Mint 20

	Juste avant la fin , l'installation s'arrête l'écriture dans le BIOS n'étant pas permise par le PC
	L'exécution de grub-install a échoué  ->  cliquer sur KO
	Le programme d'installation a planté  ->  cliquer sur Fermer 
	Installation terminée                 ->  cliquer sur Continuer à tester

## Lancer un terminal et exécuter les commandes suivantes

	"su root" ou "sudo su" ou "su -"

	Les partitions du PC /dev/sd.. sont déjà montées sur /target
	for i in /dev /dev/pts /proc /sys ; do mount -B $i /target$i ; done

	chroot /target                    changement du root directory en /target
	cd /boot/efi/EFI
	cp ubuntu/grubx64.efi BOOT

	update-grub                       création du fichier /boot/grub/grub.cfg

## Faire "08 Terminer l'installation"
