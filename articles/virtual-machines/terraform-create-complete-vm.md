---
title: "infraestructura básica aaaCreate en Azure mediante el uso de Terraform | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate Azure recursos mediante el uso de Terraform"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 916a838c118f28b3fbd373188e0acb2afc655081
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Creación de una infraestructura básica de Azure mediante Terraform
En este artículo se describe los pasos de hello necesarios tootake tooprovision una máquina virtual, junto con la infraestructura subyacente, en Azure. Obtendrá información sobre cómo toowrite Terraform scripts y cómo toovisualize Hola cambia antes de que estén en la infraestructura de nube. También obtendrá información sobre cómo la infraestructura de toocreate en Azure mediante Terraform.

tooget iniciado, cree un archivo denominado \terraform_azure101.tf en el editor de texto preferido (Visual Studio código/fundamentales/Vim/etcetera.). nombre exacto de Hola de archivo hello no es importante porque Terraform acepta un parámetro de nombre de carpeta hello: se ejecutan todos los scripts en la carpeta de Hola. Pegue Hola después el código en un archivo nuevo hello:

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
Hola `provider` sección de hello en el script, puede indicar a Terraform toouse los recursos de tooprovision de un proveedor de Azure en el script de Hola. valores de tooget para subscription_id, appId, la contraseña y tenant_id, vea hello [instalar y configurar Terraform](terraform-install-configure.md) guía. Si ha creado variables de entorno para los valores de hello en este bloque, no es necesario tooinclude lo. 

Hola `azurerm_resource_group` recurso indica Terraform toocreate un nuevo grupo de recursos. Puede ver más tipos de recursos que están disponibles en Terraform más adelante en este artículo.

## <a name="execute-hello-script"></a>Ejecutar script de Hola
Después de guardar el script de Hola, salir de la línea de comandos de consola/toohello y escriba Hola siguiente:
```
terraform init
```
tooinitialize Terraform proveedor de Azure. A continuación, escriba lo siguiente hello:
```
terraform plan terraformscripts
```
Se supone que `terraformscripts` es carpeta Hola donde se guardó el script de Hola. Utilizamos hello `plan` Terraform comando, que se examina los recursos de hello definidos en las secuencias de comandos de Hola. Compararlas toohello información de estado guardado por Terraform y, a continuación, salidas Hola ejecución planeada _sin_ realmente crear recursos en Azure. 

Después de ejecutar el comando anterior hello, debería ver algo parecido a Hola después de pantalla:

![Plan de Terraform](linux/media/terraform/tf_plan2.png)

Si todo parece correcto, el aprovisionamiento de este nuevo grupo de recursos en Azure ejecutando Hola siguientes: 
```
terraform apply terraformscripts
```
Hola portal de Azure, debería ver Hola nueva vacía grupo de recursos denominado `terraformtest`. En hello la siguiente sección, agregará que una máquina virtual y todos Hola infraestructura de soporte para ese grupo de recursos de máquina virtual toohello.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Aprovisionamiento de una VM Ubuntu con Terraform
Vamos a ampliar script de Hola Terraform que hemos creado con detalles de hello tooprovision necesaria una máquina virtual con Ubuntu. Hola de recursos que se aprovisiona en las secciones siguientes de hello es:

* Una red con una sola subred
* Una tarjeta adaptadora de red 
* Una cuenta de almacenamiento con un contenedor de almacenamiento
* Una dirección IP pública
* Una máquina virtual que usa todos los recursos anteriores Hola 

Para obtener documentación completa para cada uno de los recursos de Azure Terraform Hola, vea hello [Terraform documentación](https://www.terraform.io/docs/providers/azurerm/index.html).

versión completa de Hola de hello [script de aprovisionamiento](#complete-terraform-script) también se proporciona por comodidad.

### <a name="extend-hello-terraform-script"></a>Ampliar la secuencia de comandos de hello Terraform
Extender el script de Hola que se creó con hello recursos siguientes: 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
script de Hola anterior crea una red virtual y una subred dentro de esa red virtual. Tenga en cuenta grupo de recursos de toohello Hola referencia que ya creados a través de "${azurerm_resource_group.helloterraform.name}" en la red virtual de Hola y la definición de subred Hola.

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}
~~~~
los fragmentos de código de la secuencia de comandos anterior Hola crean una IP pública y una interfaz de red que usa IP pública Hola creado. Tenga en cuenta Hola referencias toosubnet_id y public_ip_address_id. Terraform tiene inteligencia incorporada toounderstand ese Hola interfaz de red tiene una dependencia de recursos de Hola que toobe necesidad creado antes de la creación de hello de interfaz de red de Hola.

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
Aquí, ha creado una cuenta de almacenamiento y definido un contenedor de almacenamiento dentro de dicha cuenta. Esta cuenta de almacenamiento es donde se almacenan los discos duros virtuales (VHD) para la máquina virtual de hello sobre toobe creado.

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
Por último, fragmento anterior Hola crea una máquina virtual que usa todos los recursos de hello aprovisionados ya. Son una cuenta de almacenamiento y un contenedor para un disco duro virtual, una interfaz de red con direcciones IP públicas y subred especificada, y grupo de recursos de Hola que ya haya creado. Tenga en cuenta propiedad vm_size de hello, donde el script de Hola especifica un SKU de A0 de Azure.

### <a name="execute-hello-script"></a>Ejecutar script de Hola
Con script completo de hello guardado, salir de la línea de comandos de consola/toohello y escriba Hola siguiente:
```
terraform apply terraformscripts
```
Más tarde, los recursos de hello, incluida una máquina virtual, aparecen en hello `terraformtest` grupo de recursos de hello portal de Azure.

## <a name="complete-terraform-script"></a>Script completo de Terraform

Para su comodidad, a continuación se muestra completa del script Terraform Hola que aprovisiona toda infraestructura Hola de descrito en este artículo.

```
variable "resourcesname" {
  default = "helloterraform"
}

# Configure hello Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
Ha creado una infraestructura básica en Azure mediante Terraform. Para escenarios más complejos, incluidos ejemplos sobre cómo usar equilibradores de carga y conjuntos de escalado de máquinas virtuales, consulte los diversos [ejemplos de Terraform para Azure](https://github.com/hashicorp/terraform/tree/master/examples). Para obtener una lista actualizada de proveedores de Azure admitidos, vea hello [Terraform documentación](https://www.terraform.io/docs/providers/azurerm/index.html).
