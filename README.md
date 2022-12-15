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
rcup -v -d $HOME/Code/dotfiles -x .git -x README.md -x .gitignore -x bin -x Brewfile -x LICENSE
```

### Install oh-my-zsh
# SEE: https://github.com/ohmyzsh/ohmyzsh/wiki#welcome-to-oh-my-zsh for updated installation instructions

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### To update Brewfile

```bash
brew bundle dump --force --file $HOME/Code/dotfiles/Brewfile
```

### Switch to zsh shell

```bash
chsh -s $(which zsh)
```

### Download Nord Colors

```bash
curl -o Nord.itermcolors https://raw.githubusercontent.com/arcticicestudio/nord-iterm2/master/src/xml/Nord.itermcolors
curl -o Nord.terminal https://raw.githubusercontent.com/arcticicestudio/nord-terminal-app/master/src/xml/Nord.terminal
```
