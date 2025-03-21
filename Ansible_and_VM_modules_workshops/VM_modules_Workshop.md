# Despliegue de Máquina Virtual de Linux con Modulos

Este proyecto permite la implementación automatizada de una máquina virtual Linux en Microsoft Azure utilizando Terraform. La infraestructura se organiza en módulos para mejorar su mantenimiento y reutilización.

El módulo `vm` se encarga de configurar la red y la máquina virtual, mientras que la configuración principal administra el grupo de recursos, la red virtual y la subred.

## **Requisitos Previos**

Antes de comenzar, asegúrate de contar con lo siguiente:

- Una cuenta activa en Microsoft Azure.
- Terraform instalado en tu sistema.
- Credenciales configuradas para autenticarte en Azure.

## **Estructura del Proyecto**

### **1. Módulo de Máquina Virtual (modules/vm)**
Este módulo define la configuración necesaria para desplegar una máquina virtual Linux, incluyendo sus parámetros de red y seguridad.

#### **Archivos principales:**

- **`main.tf`**:
  - Configura la interfaz de red (`azurerm_network_interface`).
  - Crea una dirección IP pública (`azurerm_public_ip`).
  - Implementa la máquina virtual Linux (`azurerm_linux_virtual_machine`).
  - Configura las reglas de seguridad para acceso SSH y Ansible mediante un grupo de seguridad (`azurerm_network_security_group`).

- **`variables.tf`**:
  - Define los parámetros personalizables como el nombre de la VM, la ubicación y las credenciales de acceso.

- **`outputs.tf`**:
  - Expone la dirección IP pública de la máquina virtual.

### **2. Configuración Principal (`./`)**

Este directorio contiene la configuración general del proyecto.

#### **Archivos principales:**

- **`main.tf`**:
  - Define el proveedor de Azure.
  - Crea el grupo de recursos.
  - Configura la red virtual y la subred.
  - Invoca el módulo `vm` con los valores adecuados.

- **`variables.tf`**:
  - Contiene las variables globales del proyecto, como la suscripción de Azure y la configuración de red.

## **Pasos para el Despliegue**

1. Inicializar Terraform:
   ```sh
   terraform init
   ```

2. Validar la configuración:
   ```sh
   terraform validate
   ```

3. Aplicar la infraestructura:
   ```sh
   terraform apply
   ```

![image](https://github.com/user-attachments/assets/d3ef9c66-06fc-47d5-a19f-38e76f40744b)
![image](https://github.com/user-attachments/assets/3f789d0a-c4e5-4078-86b4-06e1a6f7c7d0)


## **Eliminación de la Infraestructura**

Si deseas eliminar todos los recursos creados, ejecuta:
```sh
terraform destroy
```

