## Mise à jour de Linux

Lors des mises à jour de Linux , il est possible que l'installation de grub échoue à nouveau

Si le PC démarre sur grub> , essayer les commandes suivantes

    grub> normal              -> le PC doit démarrer ( ajouter acpi=off si nécessaire )
    
    lancer un terminal
    sudo su ou su -
    cd /boot/efi/EFI
    cp ubuntu/grubx64.efi BOOT
    update-grub
    
Si la procédure précédente ne marche pas

    redémarrer sur la clé USB et essayer la procédure "07 réparer grub avec reboot"
