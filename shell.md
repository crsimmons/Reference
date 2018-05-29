# Shell

- last argument of last command is `$_`

- You can use `${!app_hostname_var}` in a bash script to evaluate the value of `app_hostname_var` as a variable name then get _its_ value out. ([details](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html))

- If you quote the delimiter in a heredoc then the heredoc text is treated literally. Otherwise it is subject to paramter expansion

  ```sh
  cat << EOF
  > \$ Working dir "$PWD" `pwd`
  > EOF
  $ Working dir "/home/user" /home/user
  ```

  vs

  ```sh
  cat << 'EOF'
  > \$ Working dir "$PWD" `pwd`
  > EOF
  \$ Working dir "$PWD" `pwd`
  ```

- Check if a system is listening on port 8080 if `curl`, `wget`, and `nc` are all unavailable:

  ```sh
  exec 3<>/dev/tcp/127.0.0.1/8080
  echo "GET / \c\r" >&3
  cat <&3
  ```
