# CloudFoundry

- Retrieve the admin user password after deploying CF using [CF Deployment](https://github.com/cloudfoundry/cf-deployment)

  `bosh int deployment-vars.yml --path /cf_admin_password`

- Get the emails (assuming usernames are emails) of every org manager in a foundation

  ```sh
  cf curl /v2/organizations \
  | jq -r '.resources[].metadata.guid' \
  | xargs -I {} cf curl /v2/organizations/{}/managers \
  | jq -r '.resources[].entity.username' \
  | sort -u | grep @
  ```

- View the application security rules attached to a space

  `cf space --security-group-rules <space-name>`

- If you used `aws ec2 stop-instances` to stop your diego cells and now you are seeing weird app behaviour after resarting the cells (i.e. running apps with no instances) then its likely because `props.json` is invalid JSON. Garden writes properties to that file on drain but `stop-instances` will forcibly shut down the instance "[after a short while](https://docs.aws.amazon.com/cli/latest/reference/ec2/stop-instances.html)" sometimes resulting in the write ending mid-stream.

- You can get a `jq` friendly env of a CF app with `cf curl /v2/apps/$(cf app <app_name> --guid)/env`

- When deploying a node app with a phantomjs dependency to a foundation without internet access you can use the phantomjs-prebuilt package and specify the `PHANTOMJS_CDNURL` environment variable in the application manifest. This value can be the route of a staticfile app running in the same foundation containing the phantomjs releases for each OS
