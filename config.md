node-exporter:
  container_name: exporter
  image: prom/node-exporter
  net: host
  restart: always
  labels:
    io.rancher.os.scope: system
    io.rancher.os.detach: "true"
    io.rancher.os.reloadconfig: "true"
    io.rancher.os.after: network
