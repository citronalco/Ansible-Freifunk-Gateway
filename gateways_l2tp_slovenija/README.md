Diese Rolle installiert Unterstützung für L2TP-Tunnel

Dazu wird tunneldigger von https://github.com/wlanslovenija/tunneldigger installiert.
Für jede Domäne wird eine eigene tunneldigger-Instanz gestartet.

Die Broker-Komponente von Tunneldigger lauscht auf eingehende Verbindungen auf Port 20000 + Domänennummer, also z.B. für Domäne 11 auf Port 20011. Dieser Port muss für die Access Points in der site.conf unter mesh_vpn.tunneldigger.brokers angegeben werden.

Der L2TP-Tunnel selbst wird dann vom Gateway über den unten als "port_base" konfigurierten Port aufgebaut.

Zur Konfiguration muss die Variable `tunneldigger` gesetzt werden, üblicherweise in den `group_vars`:

Beispiel:
```
tunneldigger:
  max_tunnels: 1024
  port_base: 20100
```

- `max_tunnel` beschränkt die maximale Anzahl der verbundenen Clients auf den gesetzten Wert
- `port_base` muss auf einen auf dem Gateway freien Port gesetzt werden.
