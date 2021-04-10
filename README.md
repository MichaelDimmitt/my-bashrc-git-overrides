## Repos that built this project:
https://github.com/MichaelDimmitt/git_check_computer<br/>
https://github.com/MichaelDimmitt/git-hide-tracked-files<br/>
https://github.com/MichaelDimmitt/git-main-master-override<br/>

## my-bashrc-git-overrides
You too can improve your git command by adding this content to your ~/.bashrc or ~/.bashrc.local 🎉
```bash
branchOverride() {
    gitCommand="$*"
    errormessage=$(echo "$gitCommand" | exec 2>&1)
    checkBranch "$errormessage"
}
## posix compliant solution:
checkBranch() {
    result=$*
    if [ -z "${result##*'master'*}" ] ;then
        command git checkout main
    elif [ -z "${result##*'main'*}" ] ;then
        command git checkout master
    else
        echo "$result"
    fi
}
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
  elif [ "$1" == "checkout" ]; then
    branchOverride "git $*";
  else
    $(which git) "$@"
  fi
}
```
