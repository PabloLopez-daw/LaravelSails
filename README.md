# LaravelSails
Laravel  sails


## 1.Iniciamos el Vagrant y ponemos lo siguiente y hacemos vagrant up: 
```bash
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  config.vm.network "private_network", ip: "192.168.56.10"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt update
    apt install -y ca-certificates curl gnupg lsb-release

    # Docker
    curl -fsSL https://get.docker.com | sh
    usermod -aG docker vagrant

    # Docker Compose
    curl -L "https://github.com/docker/compose/releases/download/v2.25.0/docker-compose-linux-x86_64" -o /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
  SHELL
end
```

## 2.Hacemos vagrant ssh y nos metemos en la maquina 
```bash
vagrant ssh
```

## 3.Vamos al directorio compartido  y creamos el proyecto de laravel
```bash
cd /vagrant

curl -s https://laravel.build/miapp | bash
```

## 4.Entramos al proyecto en la app y levantamos los contenedores
```bash
cd miapp

./vendor/bin/sail up -d

docker ps
```
