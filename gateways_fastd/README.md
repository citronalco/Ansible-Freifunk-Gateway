Diese Rolle installiert fastd

Die globale Konfiguration erfolgt durch die Variable `fastd` (am Besten in `group_vars/all` definieren):
```
fastd:
  mtu: 1320
  port_base: 10000
```
`mtu` (optional): MTU für fastd. Muss mit dem mesh_vpn.mtu-Wert in site.conf übereinstimmen. Wenn nicht gesetzt wird 1406 benutzt.

`port_base`: Aus "port_base" + Domänennummer ergibt sich der Port, auf dem fastd für jeweilige Domäne lauscht. Der Port muss mit dem in der site.conf gesetzten Port übereinstimmen.
**Beispiel:** Wenn "port_base" auf 10000 gesetzt ist, lauscht fastd für Domäne 10 auf Port 10010 und für Domäne 20 auf Port 10020.

Wenn der über "port_base" berechnete fastd-Port für eine Domäne nicht passt, kann für diese Domäne der fastd-Port mit der der Variable `domaenen.<Domänennummer>.fastd_port_forced` abweichend gesetzt werden:
```
domaenen:
  "10":
    name: Beispieldorf
    community: Musterstadt
    fastd_port_forced: 5000
    ...
```

Fastd benötigt pro Domäne und pro Server ein Schlüsselpaar. Der Public Key wird in der site.conf veröffentlicht, der Private Key wird auf dem Server benötigt.

Das Schlüsselpaar kann im Ansible Inventory in `host_vars/<servername>` gesetzt werden. Wird dies nicht getan und es existiert auf dem Server für die jeweilige Domäne noch kein Schlüsselpaar wird ein Public- und Private Key direkt auf dem Server erzeugt und verwendet.


```
domaenenliste:
  "10":
     dhcp_start: 10.10.10.0
     dhcp_ende: 10.10.19.255
     fastd_key:
       secret: 010101010101010101010101
       public: 2222222222222222222222222
   "20":
     dhcp_start: 10.10.20.0
     dhcp_ende: 10.10.29.255
   "30":
     dhcp_start: 10.10.30.0
     dhcp_ende: 10.10.39.255
     fastd: true
```

