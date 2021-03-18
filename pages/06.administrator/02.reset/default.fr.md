---
titre : "Soft & Hard reset"
---

Il peut être utile de réinitialiser l'appareil à un moment donné (système d'exploitation qui ne fonctionne pas comme prévu)

Deux méthodes sont disponibles pour réinitialiser l'appareil : la réinitialisation software et la réinitialisation hardware.

## Réinitialisation douce
Le [script bash suivant](https://github.com/bibliosansfrontieres/ideascube-deploy/raw/master/reset.sh) réinitialise "en douceur" l'appareil. Ce script ne peut réparer aucun système d'exploitation endommagé.

Il effectuera l'action suivante : 

1. rétablissement de la configuration réseau d'usine
2. réinitialisation du mot de passe pour l'utilisateur "cap".
3. arrêt & désactivaion & suppression du VPN
4. arrêter, désactivation et suppression du moteur Balena (et les images Docker / conteneurs / réseaux / etc. qui y sont liés)
5. Montage et formatage du disque dur externe
6. enfin, redémarrage de l'appareil

Il doit être exécuté, **en root**, de cette façon :
```
curl -sfL https://github.com/bibliosansfrontieres/ideascube-deploy/raw/master/reset.sh | bash
```

## Remise à zéro

La procédure suivante effectue une réinitialisation _hardware_ et remet l'appareil dans un état d'usine **sans** formater le disque dur externe. **vous devrez le faire manuellement en cas de besoin !**

1. Téléchargez l'[image de récupération](http://drop.bsf-intranet.org/clonezilla-live-RC-RC02.8_silent.zip) (~900Mo)
2. Dézippez le fichier et placez-le à la racine d'une clé USB
3. Branchez la clé USB sur le port USB de l'appareil et alimentez-la
4. La récupération se déroulera automatiquement et s'arrêtera automatiquement à la fin (indicateur LED éteint)
5. Démarrez l'appareil et attendez que ce dernier s'arrête une nouvelle fois
6. C'est terminé ! Vous pouvez alimenter et utiliser l'appareil

### Formater le disque dur manuellement
```
umount -A -l /dev/sda1
mkfs.ext4 -F /dev/sda1
```
