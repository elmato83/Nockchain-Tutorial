# Nockchain-Tutorial
Nockchain Tutorial Instalación

**1) Instalamos Dependencias**

* Actualizamos paquetes
```
sudo apt-get update && sudo apt-get upgrade -y
```

* Instalamos paquetes
```
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
```

* Instalamos Rust (elegimos opción 1 instalación estándar)
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

* Configuramos la variable de entorno para el terminal
```
source $HOME/.cargo/env
```

* Instalamos Docker (parece se usará en la Mainnet)
```
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world

sudo systemctl enable docker
sudo systemctl restart docker
```

**2) Clonamos el repo de Nockchain**
```
git clone https://github.com/zorp-corp/nockchain
```

**3) Instalamos compilador Hoon**
```
cd nockchain
make install-hoonc
```

**4) Compilamos** (cada proceso llevará varios minutos, paciencia)
```
# Eden ZKVM, Jock language
make build-hoon-all
```

```
# Rust-based node and drivers
make build
```

**5) Creamos la Wallet**
```
# Instalamos el módulo
make install-nockchain-wallet
```

```
# Generamos wallet
nockchain-wallet keygen
```
* Guardamos el mnemónico, la clave pública y clave privada

**6) Modificamos archivo de configuración**
```
nano Makefile
```
* En MINING_PUBKEY: Reemplazamos con el valor de nuestra clave pública. Nos aseguramos que nuestra clave no quede dividida por un salto de línea, pues nos daría error después. Guardamos el fichero.

**7) Instalamos Screen si no está instalado**
```
sudo apt install screen
```

**8) Lanzamos el nodo Leader**
```
# Abrimos una screen para el leader
screen -S leader
```

```
# Iniciamos el nodo leader y esperamos que instale
make run-nockchain-leader
```
* Para salir de screen pulsamos Ctrl + A + D

**9) Lanzamos el nodo Follower**
```
# Abrimos otro terminal y entramos al folder nockchain. Abrimos screen para el leader
cd nockchain
screen -S follower
```

```
# Iniciamos el nodo follower y esperamos que instale
make run-nockchain-follower
```
* Para salir de screen pulsamos Ctrl + A + D

**10) Comandos Útiles Screen**
```
# Obtener logs de la screen leader
screen -r leader

# Obtener logs de la screen follower
screen -r follower

# Salir de una screen
Press: CTRL + A + D

# Listar las screens que hay abiertas
screen -ls

# Parar el nodo dentro de una screen
Press: Ctrl + C

# Eliminar screen desde fuera de ella
screen -XS nombrescreen quit
```



