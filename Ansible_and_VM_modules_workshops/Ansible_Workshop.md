# Guía para el Despliegue de Super Mario con Ansible y Docker

Este documento describe cómo utilizar **Ansible** para automatizar la instalación de Docker y desplegar un contenedor con el juego **Super Mario Bros** en una máquina virtual de Azure.

---

## **1. Definición del Inventario**
El archivo `inventory/hosts.ini` especifica los servidores que Ansible gestionará.

```ini
[azure_vm]
ip ansible_user=tu_usuario ansible_ssh_pass=tu_contraseña
```

> **Importante:** Hay que sustituir la dirección IP y las credenciales con las correspondientes a tu entorno.

---

## **2. Configuración de Ansible**
El archivo `ansible.cfg` define configuraciones esenciales para la ejecución de los playbooks.

```ini
[defaults]
host_key_checking = False
roles_path = ./roles
inventory = ./inventory/hosts.ini
```

---

## **3. Instalación de Docker**
El playbook `playbooks/install_docker.yml` ejecuta el rol `docker_install`, encargándose de instalar Docker.

```yaml
---
- hosts: azure_vm
  become: yes
  roles:
    - docker_install
```

### **Procedimiento para instalar Docker**
El archivo `roles/docker_install/tasks/main.yml` contiene las tareas necesarias.

```yaml
- name: Instalar dependencias de Docker
  apt:
    name:
      - apt-transport-https
      - ca-certificates
      - curl
      - software-properties-common
    state: present
    update_cache: yes

- name: Agregar la clave GPG oficial de Docker
  ansible.builtin.apt_key:
    url: https://download.docker.com/linux/ubuntu/gpg
    state: present

- name: Agregar el repositorio de Docker
  ansible.builtin.apt_repository:
    repo: deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable
    state: present

- name: Instalar Docker CE
  apt:
    name: docker-ce
    state: present
    update_cache: yes
```

---

## **4. Implementación del Contenedor de Super Mario**
El playbook `playbooks/run_container.yml` lanza el rol `docker_container`, que se encarga de iniciar el juego en un contenedor.

```yaml
---
- hosts: azure_vm
  become: yes
  roles:
    - docker_container
```

### **Tareas para ejecutar el contenedor**
El archivo `roles/docker_container/tasks/main.yml` contiene las instrucciones necesarias.

```yaml
- name: Ejecutar Mario Bros
  docker_container:
    name: supermario-container
    image: "pengbai/docker-supermario:latest"
    state: started
    ports:
      - "8787:8080"
```

---

## **5. Pasos para Ejecutar el Proyecto**

### **1️ Instalar dependencias en la máquina virtual**
Ejecuta el siguiente comando:
```bash
ansible-playbook -i inventory/hosts.ini playbooks/install_docker.yml
```
![image](https://github.com/user-attachments/assets/357f80a2-4f54-4f07-9b0f-95ba5cd6589c)


### **2️ Implementar el contenedor del juego**
Ejecuta el siguiente comando:
```bash
ansible-playbook -i inventory/hosts.ini playbooks/run_container.yml
```
![image](https://github.com/user-attachments/assets/a1e1a46e-7a79-44d0-b50d-a06fc548ebc5)

### **3️ Acceder al juego desde el navegador**
Abre la siguiente dirección en tu navegador:
```
http://13.95.88.126:8787
```
![image](https://github.com/user-attachments/assets/8dbc6c33-5584-4c70-8eca-b5d61d8f47eb)

> **Nota:** Sustituye `23.97.228.22` por la dirección IP pública de tu máquina virtual.

