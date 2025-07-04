# rpi-backup

## Archi

### LXC
Container LXC qui tourne sur Proxmox dans mon homelab chez moi

A une ip publique (en IP v6) et est dans le DNS de sciure-et-silicium.fr sous `rpi-backup-1.sciure-et-silicium.fr`
Il fait tourner sshd avec en config la possibilité de faire du reverse. 

### RPI
Raspbeery Pi qui est chez un copain et qui contien un disque dur assez gros

N'est pas forcément exposé sur internet car derriere une box internet. peut être que si en ipv6 mais bon, on va partir du principe que non.
A un service, autossh qui vient ouvrir un reverse ssh sur LXC. la commande c'est `ssh -R 2222:localhost:22 ruben@rpi-backup-1.sciure-et-silicium.fr`
Le service est sensé se lancer des que la machine est up. Garantissant que le tunnel ssh est toujours dispo pour le bakcup.

### NAS
Nas Synology qui tourne chez moi et qui contien les photos a sauvegarder

A une tache de backup configurée dans hyperbackup. elle pointe directement sur `rpi-backup-1.sciure-et-silicium.fr` mais sur le port 2222. comme ça ça tombe sur le RPI

## Conso & Temp

### Reduire la fréquence proc
```
> cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
powersave
> cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq
900000
> cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
600000
```

### Surveiller la température

```
cat /sys/class/thermal/thermal_zone0/temp
47236
```

## TODO
- desactivé l'authentification par mot de passe en faveur des clés publiques. A faire comme indiqué ici : [https://community.synology.com/enu/forum/1/post/140590](https://community.synology.com/enu/forum/1/post/140590)
- lister toutes les modifications faites, aussi bien dans home, etc et les paquets installés et tout mettre dans ce repo
