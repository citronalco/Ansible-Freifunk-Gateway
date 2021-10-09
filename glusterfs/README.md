# gateways_glusterfs

Konfiguration:
group_vars/all:
```
gluster_server:
- volume: test1
  peers: "{{ groups['gateways'] }}"
  bricksize: 128
  brickfile: "/testa14.img" # default:/volumename.image"
- volume: test2
  peers:
  - gw4
  - gw3
  bricksize: 64
```

host_vars/monitor:
```
gluster_client:
- volume: test1
  path: /mnt/test_1a
- volume: test1
  path: /mnt/test_1b
- volume: test2
  path: /mnt/test_2
```

