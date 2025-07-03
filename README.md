# rpi-backup

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
