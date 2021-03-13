
## Si le PC ne démarre pas sur la clé USB bootable

Problème rencontré pour booter sur la clé USB Linux Mint 20

Il faut ajouter acpi=off dans les options de grub

	Malheureusement , avec acpi=off le PC ne s'éteindra plus tout seul
	Il devient obligatoire d'appuyer sur marche/arrêt pour éteindre le PC
	
## Ajouter ou supprimer acpi=off au démarrage

	Sur le menu de grub , taper e pour edit avant que le démarrage ne commence
  	Ajouter acpi=off aprés /casper/vmlinux ( attention au clavier qwerty a=q )
	Appuyer sur F10
	
	Dans le cas où il faut supprimer acpi=off
	taper e pour edit , supprimer acpi=off de la ligne et appuyer sur F10
	
## Ajouter ou supprimer acpi=off dans grub.cfg

Pour ne pas avoir à ajouter acpi=off en mode edit à chaque démarrage

	vi /etc/default/grub
		ajouter acpi=off à la variable GRUB_CMDLINE_LINUX_DEFAULT  
	escape :x!                        sauvegarder et quitter le fichier dans vi

	update-grub                       création du fichier /boot/grub/grub.cfg

Si le démarrage fonctionne sans acpi=off , il est alors possible de le supprimer dans grub

	vi /etc/default/grub
		supprimer acpi=off de la variable GRUB_CMDLINE_LINUX_DEFAULT 
		ou mettre la ligne en commentaire avec un #
	escape :x!                        sauvegarder et quitter le fichier dans vi

	update-grub                       création du fichier /boot/grub/grub.cfg

## Mise à jours de Linux

Suite à des mises à jour de Linux , il est possible que l'arrêt du PC fonctionne à nouveau sans avoir besoin d'appuyer sur marche/arrêt

Il est donc possible de supprimer acpi=off dans grub

Malheureusement , l'inverse est également possible 

	Le PC peut ne plus démarrer sans acpi=off suite à des mises à jour
	Il faut donc recommencer en ajoutant l'option acpi=off

Dans tous les cas , si vous avez ajouté acpi=off

	voir 08 Terminer l'installation
	faire les tests avec la commande reboot
