# Despliegue de VM Linux en Azure con Terraform

Este taller tiene el objetivo de desplegar una máquina virtual Linux en Azure.

## Prerrequisitos

- [Terraform](https://www.terraform.io/downloads.html) instalado (versión 0.12 o superior)
- [Azure CLI](https://docs.microsoft.com/es-es/cli/azure/install-azure-cli) instalado
- Cuenta de Azure con suscripción activa
- Las credenciales de Azure configuradas

## Variables

El archivo `variables.tf` ya incluye las siguientes variables con sus valores predeterminados:

```hcl
variable "subscription_id" {
  type        = string
  description = "Azure Subscription ID"
  default     = "[Id de mi suscripción]"
}

variable "resource_group_name" {
  type        = string
  description = "Name of the Resource Group"
  default     = "miprimeravmrg"
}

variable "location" {
  type        = string
  description = "Location where resources will be deployed"
  default     = "West Europe"
}

variable "virtual_network_name" {
  type        = string
  description = "Name of the Virtual Network"
  default     = "miprimeravmvnet"
}

variable "address_space" {
  type        = list(string)
  description = "Address space for the Virtual Network"
  default     = ["10.0.0.0/16"]
}

variable "subnet_name" {
  type        = string
  description = "Name of the Subnet"
  default     = "miprimeravmsubnet"
}

variable "subnet_prefix" {
  type        = list(string)
  description = "Subnet address prefix"
  default     = ["10.0.2.0/24"]
}

variable "network_interface_name" {
  type        = string
  description = "Name of the Network Interface"
  default     = "miprimeravmnic"
}

variable "public_ip_name" {
  type        = string
  description = "Name of the Public IP"
  default     = "miprimeravmpublicip"
}

variable "public_ip_allocation" {
  type        = string
  description = "Allocation method for the Public IP"
  default     = "Static"
}

variable "private_ip_allocation" {
  type        = string
  description = "Allocation method for the private IP"
  default     = "Dynamic"
}

variable "vm_name" {
  type        = string
  description = "Name of the Virtual Machine"
  default     = "miprimeravm"
}

variable "vm_size" {
  type        = string
  description = "Size of the Virtual Machine"
  default     = "Standard_F2"
}

variable "admin_username" {
  type        = string
  description = "Admin username for the VM"
  default     = "adminuser"
}

variable "admin_password" {
  type        = string
  description = "Admin password for the VM"
  default   = "adminpassword1234!"
}

variable "disable_password_authentication" {
  type        = bool
  description = "Disable password authentication"
  default     = false
}

variable "provision_vm_agent" {
  type        = bool
  description = "Provision VM agent"
  default     = true
}

variable "os_disk_caching" {
  type        = string
  description = "OS disk caching type"
  default     = "ReadWrite"
}

variable "os_disk_storage_type" {
  type        = string
  description = "OS disk storage account type"
  default     = "Standard_LRS"
}

variable "image_publisher" {
  type        = string
  description = "Publisher of the VM image"
  default     = "Canonical"
}

variable "image_offer" {
  type        = string
  description = "Offer of the VM image"
  default     = "0001-com-ubuntu-server-jammy"
}

variable "image_sku" {
  type        = string
  description = "SKU of the VM image"
  default     = "22_04-lts"
}

variable "image_version" {
  type        = string
  description = "Version of the VM image"
  default     = "latest"
}

variable "nsg_name" {
  type        = string
  description = "Name of the Network Security Group"
  default     = "miprimeravmnsg"
}

variable "ssh_rule_name" {
  type        = string
  description = "Name of the SSH security rule"
  default     = "ssh_rule"
}

variable "ssh_rule_priority" {
  type        = number
  description = "Priority of the SSH security rule"
  default     = 100
}

```

## Paso a paso de ejecución

### 1. Inicializar Terraform (terraform init)

```bash
terraform init
```
![image](https://github.com/user-attachments/assets/7117c848-7849-4ef1-b791-d410f4656556)

### 2. Validar la configuración (terraform validate)

```bash
terraform validate
```
![image](https://github.com/user-attachments/assets/0478f716-fc61-4f07-b730-e8c3a5ff5019)

### 3. Crear un plan de ejecución (terraform plan)

```bash
terraform plan
```
![image](https://github.com/user-attachments/assets/ae4a4fb0-754d-4c10-b428-c0e0f8148953)

### 4. Aplicar los cambios (terraform apply)

```bash
terraform apply
```
![image](https://github.com/user-attachments/assets/c4ce2373-9f72-46a6-920e-b9c9b76a8b77)
![image](https://github.com/user-attachments/assets/60c842cf-4921-418d-bfd2-ce828d76ac33)

### 6. Comprobar conexión con la VM

![image](https://github.com/user-attachments/assets/c7b77940-5a6e-4e36-9a9b-f75f6f04987c)

### 5. Destruir la infraestructura (terraform destroy)

```bash
terraform destroy
```
