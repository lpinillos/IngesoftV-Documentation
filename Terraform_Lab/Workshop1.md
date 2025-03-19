# Taller de Terraform con Azure Functions

Este taller guía la implementación de una Azure Function utilizando Terraform. Sigue los pasos a continuación para configurar y desplegar tu infraestructura en Azure.

## Prerrequisitos

Antes de comenzar, asegúrate de tener instalados los siguientes requisitos:

- [Git](https://git-scm.com/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- [Terraform](https://developer.hashicorp.com/terraform/tutorials/azure-get-started/install-cli)

## Pasos

### 1. Clonar el repositorio

```sh
git clone https://github.com/ChristianFlor/azfunction-tf.git
cd azfunction-tf
```

### 2. Abrir el proyecto en Visual Studio Code

```sh
code .
```

### 3. Autenticarse en Azure

```sh
az login
```

### 4. Inicializar Terraform

```sh
terraform init
```
![image](https://github.com/user-attachments/assets/a18e8ba4-19a3-469e-9b82-7e98203b81d7)

### 5. Validar la configuración de Terraform

```sh
terraform validate
```
![image](https://github.com/user-attachments/assets/98dbe511-93d4-4d77-ac99-85798b9596ff)

### 6. Ver el plan de ejecución

```sh
terraform plan
```
![image](https://github.com/user-attachments/assets/d82937fa-c412-4683-b546-58724b8b8b40)

### 7. Obtener el ID de la suscripción de Azure

Ejecuta el siguiente comando para obtener tu ID de suscripción:

```sh
az account show
```

Busca el campo `id` en la salida y cópialo.

### 8. Agregar el ID de suscripción en `main.tf`

Edita el archivo `main.tf` y agrega la siguiente línea debajo de `features`:

```hcl
subscription_id = "TU_CODIGO"
```
![image](https://github.com/user-attachments/assets/dc2a5c67-cd15-40f9-9fdb-a9246b5a48f2)

### 9. Verificar el plan de ejecución nuevamente

```sh
terraform plan
```
![image](https://github.com/user-attachments/assets/6ce5dafe-e5dd-448d-b990-a2af84b21fab)

### 10. Aplicar la configuración

```sh
terraform apply
```
![image](https://github.com/user-attachments/assets/3d1831ff-cd09-49d5-aecd-450eb0e5d20f)
![image](https://github.com/user-attachments/assets/692ef8ab-6382-4b6c-a69e-2280ea7a9884)

