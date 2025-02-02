# RouterStat per-client traffic monitor

## ddwrt

Starting with some build (approx 45219), bwmon has user traffic built-in and the widget will pick it up automatically. If it doesn’t, you can enable it by adding a [script](https://pastebin.com/S0zFRc0G) on the Commands page, saving it as a Custom script. After that, run  `nvram set mypage_scripts="/tmp/custom.sh"`  to link the script with a custom page and set up Cron in the Management section  `* * * * * root /tmp/custom.sh update`. In builds 43381+, the script name should be `.rc_custom` instead of `custom.sh`.

If the traffic is counted incorrectly (much less than it should be), then you can enable QoS, but do not set any restrictions. This will disable NAT Offload.

![enter image description here](https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/ddwrt1.png)
<img src="https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/padavan1.png" alt="" style="max-width: 500px"/>

![enter image description here](https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/ddwrt2.png)

![enter image description here](https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/ddwrt3.png)

## Padavan

On Padavan, traffic can be enabled in a similar way. On the Administration -> Console page, run two commands sequentially

```
wget https://pastebin.com/raw/S0zFRc0G -O /etc/storage/c2-bwmon.sh
```

```
sed -i 's/\r//' /etc/storage/c2-bwmon.sh && chmod +x /etc/storage/c2-bwmon.sh && mtd_storage.sh save
```

And then you just need to activate and set up Cron on the Services page  `* * * * * /etc/storage/c2-bwmon.sh update`

If the traffic is counted incorrectly (much less than it should be), then you can disable Offload on the WAN page.

![enter image description here](https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/padavan1.png)

![enter image description here](https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/padavan2.png)

![enter image description here](https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/padavan3.png)

## Tp-link with green UI

On tp-links per-user traffic can be activated on the Statistics page, but unfortunately it’s not divided into sent/received.

![enter image description here](https://raw.githubusercontent.com/renr4/misc/refs/heads/main/routerstat/tp-link1.png)
