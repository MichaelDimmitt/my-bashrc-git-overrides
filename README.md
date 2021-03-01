## my-bashrc-git-overrides
```bash
git() {
  if [ "$1" == "check" ]; then
    bash <(curl -s https://raw.githubusercontent.com/MichaelDimmitt/git_check_computer/master/git_check_computer.sh)
  elif [ "$1" == "add" ]; then
    $(which git) "$@"
    while IFS='' read -r LINE || [ -n "${LINE}" ]; do
      $(which git) reset HEAD $LINE;
    done < .hide_tracked
  else
    $(which git) "$@"
  fi
}
```
