Linux bash alias

```bash
alias vi='vim'
alias ll='ls -alFG'
alias ls='ls -G'
alias sl='ls -G'
alias subl='open -a /Applications/Sublime\ Text.app  "$@"'
alias gitlog="git log --all --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"
alias grep=" grep -v grep | grep "
alias lamp="ps aux| grep nginx; ps aux| grep 'php-fpm'; ps aux| grep mysql"
alias ListFilesBiggerThanXSize='find . -size +10M -type f -print0 | xargs -0 ls -Ssh | sort -z'

alias gitstatus="git status| grep modified|awk '{print \$2}'|xargs echo"
alias gitstat="git status| grep modified|awk '{print \$2}'|xargs echo"
alias gs="git status"
alias gd="git diff"
alias gc="git checkout"
alias ga="git add"
```
