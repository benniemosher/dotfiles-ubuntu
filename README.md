# dotfiles-ubuntu
🐧 An easy-to-recreate Ubuntu setup for cloud management, via Homebrew and some config files. 🐧

## 📜 Usage:

### Install Homebrew

To install Homebrew, we first need to update our system and install `curl`, `git`, `build-essential`, and `rcm` so that we can successfully install Homebrew and our packages:

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
sudo apt-get install build-essential procps curl file git rcm zsh
```

To install Homebrew run this command:

```bash
# SEE: https://brew.sh for updated installation instructions

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
```

### To install Brave Browser

```bash
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list
sudo apt update
sudo apt install brave-browser
```

### 🗝 Setup Github SSH Key

```bash
# SEE: https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent and
#      https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account for updated instructions

ssh-keygen -t ed25519 -C "benniemosher@gmail.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519
```

### Setup dotfiles

```bash
mkdir -p $HOME/Code/

git clone git@github.com:benniemosher/dotfiles-ubuntu.git $HOME/Code/dotfiles

brew bundle --file=$HOME/Code/dotfiles/Brewfile
```

### To update Brewfile

```bash
brew bundle dump --force --file $HOME/Code/dotfiles/Brewfile
```

### Switch to zsh shell

```bash
chsh -s $(which zsh)
```

### Install oh-my-zsh

```bash
# SEE: https://github.com/ohmyzsh/ohmyzsh/wiki#welcome-to-oh-my-zsh for updated installation instructions

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Sync config files
```bash
rcup -v -d $HOME/Code/dotfiles -x .git -x README.md -x .gitignore -x bin -x Brewfile -x LICENSE -x nord.sh
```

### Install needed gems

```bash
gem install lolcat artii fortune cowsay
```

### Download Nord Colors

```bash
curl -o $HOME/Code/dotfiles/nord.sh https://raw.githubusercontent.com/arcticicestudio/nord-gnome-terminal/develop/src/nord.sh
```

In `Terminal` click on the hamburger menu, then click on Preferences. On the left hand column of the new screen, press the drop-down arrow next to `Nord` then click "Set as default".

### Install VIM plugins

```bash
vim ~

:PlugInstall
```

### Install Keybase

```bash
cd $HOME/Downloads
curl --remote-name https://prerelease.keybase.io/keybase_amd64.deb
sudo apt install ./keybase_amd64.deb
run_keybase
```

### Install GPG and Keybase keys

```bash
keybase login
keybase pgp list
keybase pgp export -q <ID_FROM_ABOVE> | gpg --import
keybase pgp export -q <ID_FROM_ABOVE> --secret | gpg --allow-secret-key-import --import
```
