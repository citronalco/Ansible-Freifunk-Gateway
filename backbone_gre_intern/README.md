## Interne GRE-Tunnel

Diese Rolle legt GRE-Tunnel zwischen allen Gateways an.

Die Netzwerkschnittstellen für die Tunnel werden `bck-<ZIELGATEWAY>` benannt.

Die IP-Adressen der Tunnelendpunke werden aus der Host-Variable `vm_id` berechnet.
