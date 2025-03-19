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

### 5. Validar la configuración de Terraform

```sh
terraform validate
```

### 6. Ver el plan de ejecución

```sh
terraform plan
```

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

### 9. Verificar el plan de ejecución nuevamente

```sh
terraform plan
```

### 10. Aplicar la configuración

```sh
terraform apply
```

