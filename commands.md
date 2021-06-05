#cloud-config
ssh_authorizes_keys:
  -ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDL+HBmwCOeRh+tjbKkRT6bBrDlLjjr+ZvxPqj3e47POuphbdAVy5fAfQIDQY4sGq9uO9He2RQN63yptCQSS0VfxPiPcXAVkxHoBvfb54XXuECCNP36BON4ilmBdFdo5Fr3oDhuxG238H9oRCGbCSHHSPW1c/iUr03yMD3A8GYuC5W3CUnbFlXUAvD3rR0RwdNW+Z4NbmK4FAN4h2taUyPaOWB7fImfaWE/PG5zjvcUWUdgpLlARcQPmZ5Fyc5A46gOg9vGG8+gCy3hjOumkECYlLVWDbi+fgwPMuDKPGENUDhiMtzaSc9nYphjHeM+5zmLaNFxYgbJXeI2AxtaELCV hadi@hadi-virtual-machine
rancher:
  resize_device: /dev/sda
------------------------------------------
ros config validate -i config.yaml
ros config merge -i  config.yaml
------------------------------------------
ros  config set hostname dwsclass-hadi
reboot 
----------------------------------------------
#cloud-config
  ssh:
    port: 10022
-----------------------------------------
#cloud-config
rancher:
  recovery: false
  debug: false
  disable:
    - password
    - autologin
---------------------------------------------------
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
-----------------------------------------------
ros service  enable  /var/lib/rancher/conf/cloud-config.d/rancher.yaml
ros service  list

reboot
---------------------------------------------------------------------




