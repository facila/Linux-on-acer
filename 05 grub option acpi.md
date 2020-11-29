
## Si le PC ne démarre pas sur la clé USB bootable

Problème rencontré pour booter sur la clé USB Linux Mint 20

Il faut ajouter acpi=off dans les options de grub

	Sur le menu de grub , taper e pour edit
  	Ajouter acpi=off aprés /casper/vmlinux ( attention au clavier qwerty a=q )
	Appuyer sur F10
	
	Malheureusement , avec acpi=off le PC ne s'éteindra plus tout seul
	Il devient obligatoire d'appuyer sur arret/marche pour eteindre le PC

## Ajouter acpi=off dans grub.cfg

Pour ne pas avoir à ajouter acpi=off en mode edit à chaque démarrage

	vi /etc/default/grub
		ajouter acpi=off à la variable GRUB_CMDLINE_LINUX_DEFAULT  
	escape :x!                        sauvegarder et quitter le fichier dans vi

	update-grub                       création du fichier /boot/grub/grub.cfg

## Mise à jours de Linux

Suite à des mises à jour de Linux , il est possible que l'arrêt du PC fonctionne à nouveau sans avoir besoin d'appuyer sur marche/arrêt

Il est donc possible de supprimer acpi=off dans grub

	vi /etc/default/grub
		supprimer acpi=off de la variable GRUB_CMDLINE_LINUX_DEFAULT  
	escape :x!                        sauvegarder et quitter le fichier dans vi

	update-grub                       création du fichier /boot/grub/grub.cfg

Malheureusement , l'inverse est également possible 

	Le PC peut ne plus démarrer sans acpi=off suite à des mises à jour
	Il faut donc recommencer l'ajout de l'option acpi=off
