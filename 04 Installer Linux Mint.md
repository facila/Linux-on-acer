# Installer Linux Mint sur un ACER Aspire ES17 ES1-732

J'explique comment installer Linux si comme moi vous avez un ACER et que vous rencontrez les problèmes suivants :

- plantage à la fin de l'installation de linux
- plantage à l'installation ou la réparation de grub
- plantage sur la commande efibootmgr lorsque l'on essaye de modifier le BIOS

		je ne détaille pas l'installation de Linux Mint : partition , clé bootable , ... 
		je ne détaille pas non plus le fonctionnement général de EFI
		le problème n'est pas là , tous les tutos disponibles sur internet le font trés bien

## Créer une clé USB bootable sur Linux Mint

	voir la procédure sur internet
	il y a plusieurs méthodes pour créer la clé USB bootable
	la suivante , avec mkusb , permet en plus de pouvoir écrire ensuite sur la clé
	cela peut être interessant pour sauvegarder des fichiers d'installation et les réutiliser en copier/coller
	https://www.debugpoint.com/2019/10/how-to-create-persistent-usb-ubuntu-linux-mint/

Je vous conseille ensuite de garder cette clé qui pourra servir en cas de problème

Exécuter l'installation de Linux

	voir la procédure sur internet
	juste avant la fin de l'installation sur grub2
	l'écriture dans le BIOS n'étant pas permise
	l'installation se plante ou le PC se bloque
