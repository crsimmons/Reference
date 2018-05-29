# Terraform

- If you use `security_groups` in terraform when provisioning an `aws_instance` it recreates the vm on every apply but if you use `vpc_security_group_ids` it doesn’t ([details](https://github.com/hashicorp/terraform/issues/7221))

- Convert tfstate to metadata (in the context of the [Concourse terraform resource](https://github.com/ljfranklin/terraform-resource#metadata-file))

  `terraform output -state=toffee.tfstate -json | jq 'with_entries({"key": .key, "value": .value.value})'`
