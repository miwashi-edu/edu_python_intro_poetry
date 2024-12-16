# edu_python_intro_poetry

## Create Python Machine

```bash
docker network create --driver bridge --subnet 192.168.2.0/24 --gateway 192.168.2.1 pentest
docker run -d -it --network pentest --name python --hostname python python:3.11-slim bash
docker exec -it python bash
```

## Configure Machine

```bash
apt-get update
apt-get install build-essential  -y
apt-get install libssl-dev  -y
apt-get install zlib1g-dev  -y
apt-get install libbz2-dev  -y
apt-get install libreadline-dev  -y
apt-get install libsqlite3-dev  -y
apt-get install curl -y
apt-get install wget  -y
apt-get install git -y
apt-get install libncurses5-dev  -y
apt-get install libncursesw5-dev  -y
apt-get install xz-utils  -y
apt-get install tk-dev  -y
apt-get install libffi-dev  -y
apt-get install git  -y
apt-get install sudo  -y
apt-get install zsh  -y
apt-get install procps -y
apt-get install vim -y
apt-get install vim-nox -y
apt-get install cmake -y
apt-get install python3-dev -y
```

## Add dev user and configure

```bash
adduser [userid] # Prepare a password, and answer all questions
usermod -aG sudo [userid]
su [userid]
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
curl -sSL https://install.python-poetry.org | python3 -
export PATH="$HOME/.local/bin:$PATH"
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
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


