# edu_python_intro_poetry

## Create Python Machine

```bash
docker network create --driver bridge --subnet 192.168.2.0/24 --gateway 192.168.2.1 pentest
docker run -d  -p 2222:22 --network pentest --name python --hostname python python:3.11-slim bash
docker run -d  -p 2222:22 --network pentest --name python --hostname py1 python tail -f /dev/null
docker exec -it python /bin/bash
```

## Configure Machine

```bash
apt-get update
```

## Add devtools

```bash
apt-get install zsh  -y
apt-get install sudo  -y
```

## Add [userid] user

```bash
adduser [userid] # Prepare a password, and answer all questions
usermod -aG sudo [userid]
su [userid]
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git config --global init.defaultBranch main
```

## Set up SSH

```bash
apt-get install -y openssh-server
mkdir -p /var/run/sshd
echo > /etc/ssh/sshd_config << 'EOF'
PermitRootLogin no
PasswordAuthentication yes
PubkeyAuthentication yes
AllowUsers miwa
EOF
service ssh restart
```

## Add dev user and configure

```bash
adduser [userid] # Prepare a password, and answer all questions
usermod -aG sudo [userid]
su [userid]
sudo chsh -s $(which zsh) username
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
export PATH="$HOME/.local/bin:$PATH"
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
pip install --upgrade pip
pip install pipx
pip install poetry
```

## Configure VI

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
echo > ~/.vimrc << 'EOF'
call plug#begin('~/.vim/plugged')

" Python autocompletion
Plug 'davidhalter/jedi-vim'

" PEP8 indentation
Plug 'Vimjas/vim-python-pep8-indent'

call plug#end()
EOF
pip install jedi
```

## In VIM run PlugInstall

```bash
vim
:PlugInstall
```

## Save image for future use

```bash
docker commit python python-dev-image
```


vim-python-pep8-indent
: Python PEP8-compliant indentation.

jedi-vim
: Python autocompletion and navigation using Jedi.


