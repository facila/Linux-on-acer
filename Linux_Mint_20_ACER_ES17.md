## Installer Linux Mint 20 sur un ACER Aspire ES17 ES1-732

	Date    : 14/11/2020
	Version : 1.00
	Auteur  : facila@gmx.fr

## 1 : Installer Linux Mint à partir d'une clé USB bootable

Créer une clé USB bootable sur Linux Mint ( voir la procédure sur internet )

Je vous conseille ensuite de garder cette clé qui pourra servir en cas de problème

Pour booter sur la clè USB Linux Mint 20 , il faut ajouter acpi=off dans les options de grub

	Sur le menu de grub , taper e pour edit
  	Ajouter acpi=off aprés /casper/vmlinux ( attention au clavier qwerty a=q )
	Appuyer sur F10
	Malheureusement , avec acpi=off le PC ne s'éteindra plus tout seul
	Il devient obligatoire d'appuyer sur arret/marche pour etaindre le PC
	
Exécuter l'installation de Linux

	Juste avant la fin , l'installation s'arrête l'écriture dans le BIOS n'étant pas permise par le PC
	L'exécution de grub-install a échoué  ->  cliquer sur KO
	Le programme d'installation a planté  ->  cliquer sur Fermer 
	Installation terminée                 ->  cliquer sur Continuer à tester

Contrairement à Linux Mint 19 , il est possible de continuer sans rebooter le PC

## 2 : Corriger l'installation de grub à partir d'un terminal

	sudo su

	Les partitions du PC /dev/sd.. sont déjà montées sur /target
	for i in /dev /dev/pts /proc /sys ; do mount -B $i /target$i ; done

	chroot /target                    changement du root directory en /target
	cd /boot/efi/EFI
	cp ubuntu/grubx64.efi BOOT

	vi /etc/default/grub
		ajouter acpi=off à la variable GRUB_CMDLINE_LINUX_DEFAULT  
	escape :x!                        sauvegarder et quitter le fichier dans vi

	update-grub                       création du fichier /boot/grub/grub.cfg

Si Linux est installé seul , l'installation est terminée

	Enlever la clé USB et redémarrer le PC
	Il faut faire un appui long sur le bouton marche/arret pour arreter le PC

Si Linux est installé avec Windows

	Appliquer la procédure : Ajouter Windows dans grub
	
## 3 : Mise à jours de Linux

Une fois installé , de nombreuses mises à jour sont faites lors d'une connexion à internet

La mise à jour de grub finie à nouveau en echec , à priori sans conséquences sur l'installation

Par contre , l'arrêt du PC fonctionne à nouveau sans avoir besoin d'appuyer sur marche/arrêt

Il est donc possible d'enlever acpi=off dans grub

	vi /etc/default/grub
		supprimer acpi=off de la variable GRUB_CMDLINE_LINUX_DEFAULT  
	escape :x!                        sauvegarder et quitter le fichier dans vi

	update-grub                       création du fichier /boot/grub/grub.cfg

