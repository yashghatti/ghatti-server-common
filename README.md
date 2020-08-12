# ghatti-server-common
Common services for ghatti-server as podman containers

### elasticsearch
```
Image   -  elasticsearch:7.8.1
Ports   -  9200, 9300
Volume  -  /var/lib/elastic/search:/usr/share/elasticsearch/data
Env     -  "discovery.type=single-node"
```
