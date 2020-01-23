# Cool Terminal
## Install Homebrew
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
## Download iTerm2
You can download and install it from iterm2.com Or use brew install.
```
chsh -s /bin/zsh
or
chsh -s /bin/bash
```
## Install wget
```
brew install wget
```
## Install Oh my zsh
```
$ sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```
## Install pip
```
sudo easy_install pip
```
## Install powerline
```
pip3 install powerline-status --user
```
## Install PowerFonts
```
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```
## Change Theme
```
open ~/.zshrc
ZSH_THEME='your theme'
```
## Useful Plugins
extract, vi-mode, colored-man-pages, perdirectory-history, history-substring-search, zsh-syntax-highlighting, zsh-autosuggestions, autojump...
## Install Tmux
```
brew install tmux
```
