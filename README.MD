# Elastic load balancer with consul registrator and confd


## How to use
  1. Run docker-compose up -d consul (need to start consul frist to make sure registrator runs okay)
  2. docker-compose up -d to bring up the rest of the containers.
  3. Access http://<Host_IP> to see the webapp that prints out the hostname (change 192.168.99.100 to your host ip)
  4. Install confd
  5. copy config.toml to /etc/confd/conf.d/config.toml (make sure the dest is where your nginx config file located)
  6. copy config.conf.tmpl to /etc/confd/templates/config.conf.tmpl
  7. run ./confd -onetime -backend consul -node 192.168.99.100:8500 to generate the changes
  8. enable the webapp3 in the compose and run docker-compose up -d againt to bring it up
  9. run ./confd -onetime -backend consul -node 192.168.99.100:8500 to update the config
  10. Access http://<Host_IP> to see the newly added web app is now part of the cluster
