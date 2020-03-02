Diese Rolle installert L2TP-Unterstützung

Dazu wird tunneldigger von https://github.com/wlanslovenija/tunneldigger installiert.
Für jede Domäne wird eine eigene tunneldigger-Instanz gestartet.

Die Broker-Komponente von Tunneldigger lauscht auf eingehende Verbindungen auf Port 20000 + Domänennummer.
Der L2TP-Tunnel selbst wird dann über den unten als "port_base" konfigurierten Port aufgebaut.

Zur Konfiguration muss die Variable "tunneldigger" gesetzt werden:
```
tunneldigger:
  max_tunnels: 1024
  port_base: 20100
```

`max_tunnel` beschränkt die Anzahl der verbundenen Clients auf den gesetzten Wert
`port_base` muss auf einen auf dem Gateway freien Port gesetzt werden.
