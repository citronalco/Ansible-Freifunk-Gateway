## GRE-Tunnel zu Freifunk Rheinland

Diese Rolle richtet auf Gateways die GRE-Tunnel zu Freifunk Rheinland ein. Es werden nur die Netzwerkinterfaces angelegt.

GRE-Tunnel können bei Freifunk Rheinland hier beantragt werden: https://ticket.freifunk-rheinland.net, Topic: Backbone AS201701

Ein GRE-Tunnel funktioniert nur mit der IP-Adresse aus, mit der er bei Freifunk Rheinland registriert wurde.
Er kann also nicht auf einem anderen Gateway verwendet werden.

### Konfiguration: ####

Achtung: Keine Namen mit Bindestrich für die Tunnel verwenden.

host_vars/beispielgateway:

ffrl_tun:
- name: fra_a
  gre_target: 185.66.194.0
  v4_remote: 100.64.0.140/31
  v4_local: 100.64.0.141/31
  v6_remote: 2a03:2260:0:4e::1/64
  v6_local: 2a03:2260:0:4e::2/64
- name: ber_a
  gre_target: 185.66.195.0
  v4_remote: 100.64.0.142/31
  v4_local: 100.64.0.143/31
  v6_remote: 2a03:2260:0:4f::1/64
  v6_local: 2a03:2260:0:4f::2/64

Die `*_local`-Adressen sind die Adressen auf dem Gateway, die `*_remote`-Adressen die bei Freifunk Rheinland.

