# Concourse

- You can combine `on_success` and `on_failure` with `aggregate` and `do`

  ```yaml
  on_failure:
    aggregate:
    - put: thing-1
    - put: thing-2

  on_failure:
    do:
    - put: thing-1
    - put: thing-2
  ```

- You can use `do` to do multiple steps in and `ensure` block

- You need at least 1 linux worker in a Concourse installation to have access to the base resource types. You can check what types are available to your workers with `fly workers -d`

- Provide params to the implicit `get` in a `put` step with `get_params`

- You can use [yq](https://github.com/kislyuk/yq) to validate YAML anchors

- Instead of making a Concourse task definition like a sane person:

  ```yaml
  run:
    path: project-src/ci/build.sh
  ```

  This is also works:

  ```yaml
  run:
    path: sh
    args: [project-src/ci/build.sh]
  ```

- If you try running an external task in Concourse (like with `fly execute`) and your script has CLRF line endings the task will fail to start the script with `No such file or directory` as the error even when the file is present. Changing to LF line ending fixes it.

- The Concourse S3 resource non-versioned bucket regexp only supports version capture groups in the filename - not in the path.

- You can run the docker daemon in a hijacked concourse docker image resource container with `dockerd --data-root /scratch/docker [--insecure-registry <private_registry>] >/tmp/docker.log 2>&1 &`
