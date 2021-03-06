# reverse-proxy

Diese Rolle installiert einen Reverse-Proxy mit Nginx.

Ein Reverse-Proxy nimmt Anfragen auf Freifunk-Subdomains aus dem Internet entgegen und leitet sie an interne Webserver weiter.

Die Kommunikation zwischen Reverse-Proxy und internen Webservern läuft über HTTP oder HTTPS.
Für die Kommunikation zum Internet wird HTTPS oder HTTP verwendet. Die für HTTPS nötigen Zertifkate werden durch Certbot automatisch von Let's Encrypt besorgt und vor Ablauf aktualisiert.

Zugriffe werden unter `/var/log/nginx/access.log` protokolliert. Bei IP-Adressen wird dabei zur Anonymisierung bei IPv4 das letzte Tupel auf 0 gesetzt, bei IPv6 die letzten 64 Bit.

## Konfiguration
Für die Registrierung bei Let's Encrypt wird die unter `freifunk.email` gesetzte E-Mailadresse verwendet.
Die Zuordnung von Subdomain zu internem Webserver erfolgt über die Variable `reverse_proxy`. Die Subdomains liegen unterhalb von `freiunk.domain` und müssen im DNS eingetragen sein:

```
reverse_proxy:
  http:
    <Subdomain>[:Port]:
      aliases:
        - <hostname>
      backend: <Protokoll>://<Host>[:Port]
      anonymize: False
  https:
    <Subdomain>[:Port]:
      aliases:
        - <hostname>
      backend: <Protokoll>://<Host>[:Port]
```

### Subdomain
**Subdomain** ist die Subdomäne unterhalb der mit `freifunk.domain` konfigurierten Domain, unter der der unter "backend" eingetragene Webserver erreichbar gemacht werden soll.

Je nachdem, ob die Subdomain im Abschnitt "http" oder "https" konfiguriert wird, ist sie von außen über HTTP oder eben HTTPS erreichbar. Wird sie in beiden Abschnitten konfiguriert, ist sie über HTTP und HTTPS erreichbar.

Die Angabe von **Port** ist optional. Als Standard wird "443" bei im Abschnitt "https" gelisteten Subdomains und "80" bei "http" verwendet.

#### Aliases (Optional)
Soll die Subdomain zusätzlich auf Anfragen auf einen oder mehrere Aliasnamen antworten, können diese Aliasnamen als FQDN angegeben werden.

#### Backend
Das Backend ist der interne Server, der die Anfragen für die jeweilige Subdomain beantworten soll.

Das **Protokoll** das Backends kann entweder "http" oder "https" sein.

Als **Host** kann entweder eine IP-Adresse oder ein Hostname eingetragen werden.
Wenn als Backend-Protokoll https verwendet wird und als "Host" ein IP-Adresse angegeben ist, dann wird das Zertifikat des Backend-Servers nicht geprüft.

Die Angabe von **Port** ist optional. Wenn kein Port angegeben ist wird "80" verwendet.

#### Anonymize
Optional. Wenn **anonymize** auf "False" gesetzt ist, wird für diese Subdomain die Anonymisierung der IP-Adressen in der Logdatei deaktiviert.


## Beispiel:

```
freifunk.domain: freifunk-musterstadt.de
```
und
```
reverse_proxy:
  http:
    foo:
      backend: http://192.168.123.5:82
    bar:464:
      backend: https://example.com
  https:
    foo:
      backend: http://192.168.123.5:82
      aliases:
        - demo.test.com
        - demo2.test.com
    baz:
      backend: https://127.0.0.1:8080
      anonymize: False
```
Hier leitet der Reverse-Proxy vom Internet eingehende Anfragen wie folgt an interne Webserver weiter:
- "http://foo.freifunk-musterstadt.de" zu "http://192.168.123.5:82"
- "http://bar.freifunk-musterstadt.de:464" zu "https://example.com", der Reverse Proxy überprüft das Zertifikat von example.com
- "https://foo.freifunk-musterstadt.de", "https://demo.test.com" und "https://demo2.test.com" zu "http://192.168.123.5:82"
- "https://baz.freifunk-musterstadt.de" zu "https://127.0.0.1:8080", der Reverse-Proxy überprüft **nicht** das Zertifikat von 127.0.0.1:8080. Die IP-Adressen der zugreifenden Clients werden ohne Anonymisierung protokolliert.
