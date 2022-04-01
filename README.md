## Descripción:

Este laboratorio automatiza en gran parte y hace flexible la generación de un cluster k8s vía Vagrant

## Requisitos:

VirtualBox
```
apt install virtualbox -y
```

Vagrant

```
apt install vagrant -y
```

Plugin de vagrant (para la imagen vagrant "focal64" de ubuntu, que no monta bien las carpetas compartidas)
```
vagrant plugin install vagrant-vbguest
```

## Uso:

Nos situamos en el directorio del Vagrantfile y ejecutamos:
```
vagrant up
vagrant ssh kubemaster
dos2unix ./resources/init-cluster/*
chmod +x ./resources/init-cluster/*
./resources/init-cluster/01-advertise.sh
./resources/init-cluster/02-preflights.sh
./resources/init-cluster/03-network.sh
```
Unimos los nodos (ejecutamos en cada nodo con permisos de root el comando lo tenemos en el fichero de master: /home/vagrant/kubeadm-init.log)
```
./resources/init-cluster/04-label.sh
./resources/init-cluster/05-metrics-server.sh
./resources/init-cluster/06-dashboard.sh
```
Tendremos accesible el dashboard a través de la URL (y el token para acceder lo tenemos en /home/vagrant/dashboard-token.log): 

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

