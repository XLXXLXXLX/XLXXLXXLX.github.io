```sh
sudo apt install zsh
chsh -s /usr/bin/zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```


```sh
source ~/.scripts/enabled/*

ulimit -c unlimited


export ZSH="$HOME/.oh-my-zsh"

ZSH_THEME="af-magic"

plugins=(git
        zsh-completions
        zsh-autosuggestions
        zsh-syntax-highlighting
        z
        sudo
        rsync
        python
        golang
        )

source $ZSH/oh-my-zsh.sh

# Compilation flags
# export ARCHFLAGS="-arch x86_64"
alias zshconfig="vim ~/.zshrc"
alias omzconfig="vim ~/.oh-my-zsh"

eval "$(register-python-argcomplete pipx)"


[[ -s "/home/chito/.gvm/scripts/gvm" ]] && source "/home/chito/.gvm/scripts/gvm"

```