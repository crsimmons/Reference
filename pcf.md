# PCF

- Get the properties JSON for a tile

  `om curl /api/v0/staged/products/<product-guid>/properties`

- Get the admin client for the UAA

  `om curl /api/v0/deployed/products/cf-someguid/credentials/.uaa.admin_client_credentials`

  Then get the token with [uaac](https://github.com/cloudfoundry/cf-uaac)

  ```sh
  uaac target "https://uaa.<system_domain>"
  uaac token client get admin -s mySecret
  ```

- [Pipeline for deploying prometheus for PCF](https://github.com/pivotal-cf/pcf-prometheus-pipeline)

- If you try to log in to Ops Manager with the wrong password too many time (i.e. if you have a misconfigured healthcheck pipeline) it will lock and not allow you to log in for some unknown period of time. You cat get around this using [ops manager rescue mode](https://discuss.pivotal.io/hc/en-us/articles/221439147-How-to-put-Ops-Manager-into-Rescue-Mode) with these steps:

  1. ssh into Ops Manager
  1. `sudo touch /var/tempest/workspaces/default/rescue_mode` then `sudo service tempest-web restart` to enable rescue mode
  1. `sudo rm /var/tempest/workspaces/default/rescue_mode` then `sudo service tempest-web restart` to disable rescue mode
  1. Go to the Ops Manager url and enter the decryption password
