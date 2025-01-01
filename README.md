# edu_python_intro_poetry

## Create Python Machine

```bash
docker network create --driver bridge --subnet 192.168.2.0/24 --gateway 192.168.2.1 pentest

docker run -d  -p 2222:22 --network pentest --name python --hostname py1 python tail -f /dev/null
docker exec -it python /bin/bash
```

## Configure Machine

```bash
apt-get update
```

## Add devtools

```bash
sudo apt-get install vim-gtk3 -y
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
pip install jedi
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
cat > ~/.vimrc << 'EOF'
call plug#begin('~/.vim/plugged')

" Python autocompletion
Plug 'davidhalter/jedi-vim'

" PEP8 indentation
Plug 'Vimjas/vim-python-pep8-indent'

call plug#end()
EOF
```

## In VIM run PlugInstall

```bash
vim
:PlugInstall
```

## Save image for future use

```bash
docker commit python python-dev-image
docker run -d  -p 2222:22 --network pentest --ip 192.168.2.10 --name python-client --hostname py1 python-dev-image tail -f /dev/null
docker run -d  -p 2223:22 --network pentest --ip 192.168.2.11 --name python-server --hostname py2 python-dev-image tail -f /dev/null

ssh miwa@localhost -p 2222
ssh miwa@localhost -p 2223
```


vim-python-pep8-indent
: Python PEP8-compliant indentation.

jedi-vim
: Python autocompletion and navigation using Jedi.

```python
import socket

def start_server(host, port):
    # Create a socket object using IPv4 and TCP protocol
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    
    # Bind the socket to the address and port
    server_socket.bind((host, port))
    
    # Enable the server to accept connections, with 1 client in the waiting queue
    server_socket.listen(1)
    print(f"Server listening on {host}:{port}")
    
    # Wait for a client connection
    client_socket, addr = server_socket.accept()
    print(f"Connection from {addr}")
    
    # Send a message to the connected client
    message = "Hello, client! This is a TCP server."
    client_socket.send(message.encode())  # Encode string to bytes
    
    # Close the client socket
    client_socket.close()
    
    # Close the server socket
    server_socket.close()

# Start the server with local host IP and port 12345
start_server('127.0.0.1', 12345)
```

```python
import socket

def connect_to_server(host, port):
    # Create a socket object using IPv4 and TCP protocol
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    
    # Connect to the server
    client_socket.connect((host, port))
    
    # Receive data from the server
    data = client_socket.recv(1024)  # Buffer size of 1024 bytes
    print("Received from server:", data.decode())  # Decode bytes to string
    
    # Close the socket
    client_socket.close()

# Connect to the server with local host IP and port 12345
connect_to_server('127.0.0.1', 12345)
```

## Poetry

> Add poetry plugin to plugins=(git poetry) in .zshrc

```bash
mkdir $ZSH_CUSTOM/plugins/poetry
poetry completions zsh > $ZSH_CUSTOM/plugins/poetry/_poetry
```





