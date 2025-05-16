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



