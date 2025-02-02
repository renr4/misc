# RouterStat per-client traffic monitor

## ddwrt

Начиная с какой-то сборки (примерно с 45219) в ddwrt появился учет трафика и в таком случае виджет сразу его подхватит. Если же его нет, то включить трафик можно добавив [скрипт](https://pastebin.com/S0zFRc0G) в разделе Commands и сохранив его как Custom script. После этого выполнить команду  `nvram set mypage_scripts="/tmp/custom.sh"`  и настроить планировщик крон на странице Management  `* * * * * root /tmp/custom.sh update`. На сборках 43381+ имя скрипта в обоих случаях вместо `custom.sh` должно быть `.rc_custom`.

Если трафик считается неверно (сильно меньше), то нужно включить QoS, не выставляя при этом никаких ограничений. Это деактивирует NAT Offload.

<!-- ![enter image description here](https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/ddwrt1.png) -->
<img src="https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/ddwrt1.png" alt="" width="400" />

<img src="https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/ddwrt2.png" alt="" width="400" />

<img src="https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/ddwrt3.png" alt="" width="400" />

## Padavan

В падаване трафика вообще нет, но его можно добавить похожим образом. На странице Administration -> Console ввести последовательно команды

```
wget https://pastebin.com/raw/S0zFRc0G -O /etc/storage/c2-bwmon.sh
```

```
sed -i 's/\r//' /etc/storage/c2-bwmon.sh && chmod +x /etc/storage/c2-bwmon.sh && mtd_storage.sh save
```

После этого на странице Services включить крон и добавить задание  `* * * * * /etc/storage/c2-bwmon.sh update`.

Если трафик считается неверно (сильно меньше), то нужно выключить Offload на странице WAN.

<img src="https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/padavan1.png" alt="" width="400" />

<img src="https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/padavan2.png" alt="" width="400" />

<img src="https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/padavan3.png" alt="" width="400" />

## Tp-link with green UI

На tp-link-ах трафик включается в разделе Statistics, но считается общее значение и переданного и полученного и с этим ничего не поделать.

<img src="https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/tp-link1.png" alt="" width="400" />
