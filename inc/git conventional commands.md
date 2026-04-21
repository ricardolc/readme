
COMMIT_TEXT= "feat: trainning"
git add . && git commit -m "${COMMIT_TEXT}: $(date +'%d/%m/%Y %H:%M:%S:%3N')" && git push

# Alias para commit
git config --global alias.gc "commit -m" && \
git config --global alias.gp "pull" && \
git config --global alias.gs "status" && \
git config --global alias.co "checkout" && \
git config --global alias.br "branch"

# Alias para log formatado
git config --global alias.lg "log --oneline --graph --decorate --all"

alias gs="git status"
alias gc="git commit -m"
alias gp="git push"
