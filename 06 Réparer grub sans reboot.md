## Reparer grub sans reboot

Si l'installation de grub échoue , mais que le PC ne se plante pas , il est possible de réparer grub sans rebooter

Cas rencontré avec Linux Mint 20

	Juste avant la fin , l'installation s'arrête l'écriture dans le BIOS n'étant pas permise par le PC
	L'exécution de grub-install a échoué  ->  cliquer sur KO
	Le programme d'installation a planté  ->  cliquer sur Fermer 
	Installation terminée                 ->  cliquer sur Continuer à tester

## Lancer un terminal 

	sudo su

	Les partitions du PC /dev/sd.. sont déjà montées sur /target
	for i in /dev /dev/pts /proc /sys ; do mount -B $i /target$i ; done

	chroot /target                    changement du root directory en /target
	cd /boot/efi/EFI
	cp ubuntu/grubx64.efi BOOT

	update-grub                       création du fichier /boot/grub/grub.cfg

Si Linux est installé seul , l'installation est terminée

	Enlever la clé USB et redémarrer le PC
	Il faut faire un appui long sur le bouton marche/arret pour arreter le PC

Si Linux est installé avec Windows

	Appliquer la procédure : 08 Ajouter Windows dans grub
