# Despliegue de Máquina Virtual con Vagrant

Este repositorio contiene un archivo de configuración de Vagrant (`Vagrantfile`) que despliega una máquina virtual con Ubuntu 18.04 (bionic64) utilizando VirtualBox como proveedor. La máquina virtual se configura para instalar Apache HTTP Server automáticamente y sincronizar una carpeta local con el directorio web de Apache.

## Requisitos Previos

Antes de comenzar, asegúrate de tener instalados los siguientes componentes:

- [Vagrant](https://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

## Contenido del Vagrantfile
```
# Configuración de Vagrant usando la versión 2 de la API
Vagrant.configure("2") do |config|

  # Usar una box de Ubuntu 18.04 de 64 bits como imagen base
  config.vm.box = "ubuntu/bionic64"

  # Configurar una red privada para la VM con asignación automática de IP por DHCP
  config.vm.network "private_network", type: "dhcp"

  # Provisión de la VM para instalar Apache usando un script de shell
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update                # Actualizar la lista de paquetes
    apt-get install -y apache2    # Instalar el servidor web Apache
  SHELL

  # Sincronizar la carpeta actual del host con el directorio web de Apache en la VM
  config.vm.synced_folder ".", "/var/www/html"

  # Configurar la VM con VirtualBox como proveedor
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"            # Asignar 1024 MB de memoria RAM a la VM
  end
end
```

## Instrucciones de Uso

Sigue los pasos a continuación para configurar y ejecutar la máquina virtual:

### 1. Clonar el Repositorio

Clona este repositorio en tu máquina local:

```
git clone <https://github.com/JesusGarce22/VagrantApp.git>
cd <VagrantApp>
```

### 2. Inicializar y Configurar la Máquina Virtual
Ejecuta el siguiente comando para inicializar y configurar la máquina virtual definida en el Vagrantfile:

```
vagrant up
```

![](/imgs/vagrant.png)

Revisa que la maquina virtual ya este corriendo en virtualbox

![](/imgs/Captura%20de%20pantalla%202024-08-28%20194810.png)

### 3. Ejecuta el siguiente comando para obtener la ip de la donde esta corriendo la VM
```
VagrantApp>vagrant ssh -c "hostname -I"
```

### 4. Ingresar en el navegador a la direccion ip correspondiente para ver la siguiente pantalla.
![](/imgs/WhatsApp%20Image%202024-08-28%20at%207.30.09%20PM.jpeg)