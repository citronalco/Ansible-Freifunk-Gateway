# gateways_glusterfs

TODO:
- Prüfen ob Variable "gluster" gesetzt!
- TLS-Cert für Monitor-Server erstellen -> Rolle auf allen Servern laufen lassen, wo keine "size" konfiguriert TLS & Mounten
- Fehlende Peers düften kein Problem sein (die fehlen halt dann, Daten liegen aber eh überall), ebenso neu hinzukommende (Befüllung self-healing-daemon)
- Was passiert wenn gw2 durch ein neues gw2 ersetzt wird (gleicher Hostname + IP-Adresse, aber ander UUID und leere Speicher)? Theroretisch müsste der self-healing-daemon das reparieren.
- Pfad für Brick-image-Datei konfigurierbar machen

Konfiguration:

gluster:
  volumes:
  - name: fimware
    size: 128   # mbyte für image, kein resizing!
  - name: wasanderes
    size: 234e32   # mbyte für image, kein resizing!


