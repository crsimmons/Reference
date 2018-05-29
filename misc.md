# Miscellaneous

- Bypass chrome's invalid cert page by typing `thisisunsafe` (it used to be `badidea`)

- If you want to reference a key in json which is prepended with a dot using `jq` you can do so by wrapping it in quotes

  ```sh
  $ cat example.json
  {
    ".example_key": "example_value"
  }

  $ jq -r '.".example_key"' example.json
  example_value
  ```

- `jq`'s `with_entries(foo)` is shorthand for `to_entries | map(foo) | from_entries` ([more details](https://stedolan.github.io/jq/manual/#Builtinoperatorsandfunctions))

- Calculate the total size of a set of S3 buckets matching a query string in TB

  ```sh
  aws s3api list-buckets \
  | jq -r '.Buckets[].Name | select(contains("query"))' \
  | xargs -I {} aws \
  s3 ls s3://{} --recursive \
  | awk '{total+=$3} END{print total/1024/1024/1024/1024}'
  ```

- Extract the ID of a VPC that matches a given <TAG_NAME>

  `aws ec2 describe-vpcs --query 'Vpcs[?Tags[?Key==`Name`]|[?Value==`TAG_NAME`]].VpcId' --output text`

- In the AWS GO SDK you can use the following pattern to set debug log level:

  ```go
  sess := session.Must(session.NewSession())
  sess.Config.LogLevel = aws.LogLevel(aws.LogDebug)
  ec2Client := ec2.New(sess)
  ```

- You can use `ginkgo build` to compile ginkgo test suites into runnable binaries. This is particularly useful when testing vms in an environment where aquiring dependencies is difficult

- Put a single backtick into code formatting in a markdown document like this `` ` `` with:

  ```sh
  `` ` ``
  ```

- In cmd the escape character is `^` and in powershell its `` ` ``

- When connecting to a remote mysql server through the CLI the password option can’t have a space after it.

  ```sh
  shell> mysql -ptest
  shell> mysql -p test
  ```

  The first command instructs mysql to use a password value of test, but specifies no default database. The second instructs mysql to prompt for the password value and to use test as the default database.
