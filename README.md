## my-bashrc-git-overrides
```bash
git() {
  if [ "$1" == "check" ]; then
    bash <(curl -s https://raw.githubusercontent.com/MichaelDimmitt/git_check_computer/master/git_check_computer.sh)
  elif [ "$1" == "add" ]; then
    $(which git) "$@"
    if [ -f ".hide_tracked" ]; then
      while IFS='' read -r LINE || [ -n "${LINE}" ]; do
        $(which git) reset HEAD $LINE;
      done < .hide_tracked
    fi
  else
    $(which git) "$@"
  fi
}
```
Repos that built this project:
https://github.com/MichaelDimmitt/git_check_computer
https://github.com/MichaelDimmitt/git-hide-tracked-files
https://github.com/MichaelDimmitt/git-main-master-override
