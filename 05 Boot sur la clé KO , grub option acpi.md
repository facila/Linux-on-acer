
## Si le PC ne démarre pas sur la clé USB bootable

Problème rencontré pour booter sur la clè USB Linux Mint 20

Il faut ajouter acpi=off dans les options de grub

	Sur le menu de grub , taper e pour edit
  	Ajouter acpi=off aprés /casper/vmlinux ( attention au clavier qwerty a=q )
	Appuyer sur F10
	Malheureusement , avec acpi=off le PC ne s'éteindra plus tout seul
	Il devient obligatoire d'appuyer sur arret/marche pour eteindre le PC
