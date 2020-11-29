## Mise à jour de Linux

Lors de mises à jour de Linux , il est possible que l'installation de grub échoue à nouveau

Si le PC démarre sur grub> , essayer les commandes suivantes

    grub> normal              -> le PC doit démarrer
    
    lancer un terminal
    sudo su
    cd /boot/efi/EFI
    cp ubuntu/grubx34.efi BOOT
    update-grub
    
Si la procédure précédente ne marche pas

    redémarrer sur la clé USB et essayer la procédure "06 réparer grub avec reboot"
