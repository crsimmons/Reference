# BOSH

- There is no `bosh delete-runtime-config`. In order to wipe one out you need to update with a config of:

  ```yaml
  releases: []
  addons: []
  ```

- `bosh recreate` doesn't honour changes to the cloud config
