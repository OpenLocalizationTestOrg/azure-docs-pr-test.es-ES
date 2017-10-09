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
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="5b8b6-103">Creación de una infraestructura básica de Azure mediante Terraform</span><span class="sxs-lookup"><span data-stu-id="5b8b6-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="5b8b6-104">En este artículo se describe los pasos de hello necesarios tootake tooprovision una máquina virtual, junto con la infraestructura subyacente, en Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="5b8b6-105">Obtendrá información sobre cómo toowrite Terraform scripts y cómo toovisualize Hola cambia antes de que estén en la infraestructura de nube.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="5b8b6-106">También obtendrá información sobre cómo la infraestructura de toocreate en Azure mediante Terraform.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="5b8b6-107">tooget iniciado, cree un archivo denominado \terraform_azure101.tf en el editor de texto preferido (Visual Studio código/fundamentales/Vim/etcetera.).</span><span class="sxs-lookup"><span data-stu-id="5b8b6-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="5b8b6-108">nombre exacto de Hola de archivo hello no es importante porque Terraform acepta un parámetro de nombre de carpeta hello: se ejecutan todos los scripts en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="5b8b6-109">Pegue Hola después el código en un archivo nuevo hello:</span><span class="sxs-lookup"><span data-stu-id="5b8b6-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="5b8b6-110">Hola `provider` sección de hello en el script, puede indicar a Terraform toouse los recursos de tooprovision de un proveedor de Azure en el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="5b8b6-111">valores de tooget para subscription_id, appId, la contraseña y tenant_id, vea hello [instalar y configurar Terraform](terraform-install-configure.md) guía.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="5b8b6-112">Si ha creado variables de entorno para los valores de hello en este bloque, no es necesario tooinclude lo.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="5b8b6-113">Hola `azurerm_resource_group` recurso indica Terraform toocreate un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="5b8b6-114">Puede ver más tipos de recursos que están disponibles en Terraform más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="5b8b6-115">Ejecutar script de Hola</span><span class="sxs-lookup"><span data-stu-id="5b8b6-115">Execute hello script</span></span>
<span data-ttu-id="5b8b6-116">Después de guardar el script de Hola, salir de la línea de comandos de consola/toohello y escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="5b8b6-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
 <span data-ttu-id="5b8b6-117">proveedor de Terraform de hello tooinitialize de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-117">tooinitialize hello Terraform provider for Azure.</span></span> <span data-ttu-id="5b8b6-118">A continuación, cambie el directorio de hello demasiado**terraformscripts**, y Hola problema siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5b8b6-118">Then change hello directory too**terraformscripts**, and issue hello following command:</span></span>
```
terraform plan
```
<span data-ttu-id="5b8b6-119">Utilizamos hello `plan` Terraform comando, que se examina los recursos de hello definidos en las secuencias de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-119">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="5b8b6-120">Compararlas toohello información de estado guardado por Terraform y, a continuación, salidas Hola ejecución planeada _sin_ realmente crear recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-120">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="5b8b6-121">Después de ejecutar el comando anterior hello, debería ver algo parecido a Hola después de pantalla:</span><span class="sxs-lookup"><span data-stu-id="5b8b6-121">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Plan de Terraform](./media/terraform/tf_plan2.png)

<span data-ttu-id="5b8b6-123">Si todo parece correcto, el aprovisionamiento de este nuevo grupo de recursos en Azure ejecutando Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b8b6-123">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply
```
<span data-ttu-id="5b8b6-124">Hola portal de Azure, debería ver Hola nueva vacía grupo de recursos denominado `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-124">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="5b8b6-125">En hello la siguiente sección, agregará que una máquina virtual y todos Hola infraestructura de soporte para ese grupo de recursos de máquina virtual toohello.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-125">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="5b8b6-126">Aprovisionamiento de una VM Ubuntu con Terraform</span><span class="sxs-lookup"><span data-stu-id="5b8b6-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="5b8b6-127">Vamos a ampliar script de Hola Terraform que hemos creado con detalles de hello tooprovision necesaria una máquina virtual con Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-127">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="5b8b6-128">Hola de recursos que se aprovisiona en las secciones siguientes de hello es:</span><span class="sxs-lookup"><span data-stu-id="5b8b6-128">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="5b8b6-129">Una red con una sola subred</span><span class="sxs-lookup"><span data-stu-id="5b8b6-129">A network with a single subnet</span></span>
* <span data-ttu-id="5b8b6-130">Una tarjeta adaptadora de red</span><span class="sxs-lookup"><span data-stu-id="5b8b6-130">A network interface card</span></span> 
* <span data-ttu-id="5b8b6-131">Una cuenta de almacenamiento para diagnósticos de la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="5b8b6-131">A storage account for hello virtual machine diagnostics</span></span>
* <span data-ttu-id="5b8b6-132">Una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="5b8b6-132">A public IP</span></span>
* <span data-ttu-id="5b8b6-133">Una máquina virtual que usa todos los recursos anteriores Hola</span><span class="sxs-lookup"><span data-stu-id="5b8b6-133">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="5b8b6-134">Para obtener documentación completa para cada uno de los recursos de Azure Terraform Hola, vea hello [Terraform documentación](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="5b8b6-134">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="5b8b6-135">versión completa de Hola de hello [script de aprovisionamiento](#complete-terraform-script) también se proporciona por comodidad.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-135">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="5b8b6-136">Ampliar la secuencia de comandos de hello Terraform</span><span class="sxs-lookup"><span data-stu-id="5b8b6-136">Extend hello Terraform script</span></span>
<span data-ttu-id="5b8b6-137">Extender el script de Hola que se creó con hello recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5b8b6-137">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="5b8b6-138">script de Hola anterior crea una red virtual y una subred dentro de esa red virtual.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-138">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="5b8b6-139">Tenga en cuenta grupo de recursos de toohello Hola referencia que ya creados a través de "${azurerm_resource_group.helloterraform.name}" en la red virtual de Hola y la definición de subred Hola.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-139">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="5b8b6-140">los fragmentos de código de la secuencia de comandos anterior Hola crean una IP pública y una interfaz de red que usa IP pública Hola creado.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-140">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="5b8b6-141">Tenga en cuenta Hola referencias toosubnet_id y public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-141">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="5b8b6-142">Terraform tiene inteligencia incorporada toounderstand ese Hola interfaz de red tiene una dependencia de recursos de Hola que toobe necesidad creado antes de la creación de hello de interfaz de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-142">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="5b8b6-143">En este caso, se crea una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-143">Here, you created a storage account.</span></span> <span data-ttu-id="5b8b6-144">Esta cuenta de almacenamiento es donde va a almacenar máquina virtual de hello sus detalles de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-144">This storage account is where hello virtual machine will store its diagnostics details.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="5b8b6-145">Por último, fragmento anterior Hola crea una máquina virtual que usa todos los recursos de hello aprovisionados ya.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-145">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="5b8b6-146">Son una cuenta de almacenamiento para diagnósticos de la máquina virtual de hello, una interfaz de red con direcciones IP públicas y subred especificada y grupo de recursos de Hola que ya haya creado.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-146">They are a storage account for hello virtual machine diagnostics, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="5b8b6-147">Tenga en cuenta propiedad vm_size de hello, donde el script de Hola especifica un SKU de DS1v2 estándar de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-147">Note hello vm_size property, where hello script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="5b8b6-148">Son toosupply requiere una clave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-148">You are required toosupply an SSH public key.</span></span> <span data-ttu-id="5b8b6-149">Colocar el valor de clave pública de hello en sección hello **... INSERTE AQUÍ LA CLAVE PÚBLICA OPENSSH...**  anterioR.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-149">Place hello public key value into hello section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="5b8b6-150">Se puede usar una existente ssh par de claves o siga hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) o [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) par de claves de documentación toogenerate Hola.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-150">You can use an existing ssh key pair or follow hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation toogenerate hello key pair.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="5b8b6-151">Ejecutar script de Hola</span><span class="sxs-lookup"><span data-stu-id="5b8b6-151">Execute hello script</span></span>
<span data-ttu-id="5b8b6-152">Con script completo de hello guardado, salir de la línea de comandos de consola/toohello y escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="5b8b6-152">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply
```
<span data-ttu-id="5b8b6-153">Más tarde, los recursos de hello, incluida una máquina virtual, aparecen en hello `terraformtest` grupo de recursos de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-153">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="5b8b6-154">Script completo de Terraform</span><span class="sxs-lookup"><span data-stu-id="5b8b6-154">Complete Terraform script</span></span>

<span data-ttu-id="5b8b6-155">Para su comodidad, a continuación se muestra completa del script Terraform Hola que aprovisiona toda infraestructura Hola de descrito en este artículo.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-155">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
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

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="5b8b6-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b8b6-156">Next steps</span></span>
<span data-ttu-id="5b8b6-157">Ha creado una infraestructura básica en Azure mediante Terraform.</span><span class="sxs-lookup"><span data-stu-id="5b8b6-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="5b8b6-158">Para escenarios más complejos, incluidos ejemplos sobre cómo usar equilibradores de carga y conjuntos de escalado de máquinas virtuales, consulte los diversos [ejemplos de Terraform para Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="5b8b6-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="5b8b6-159">Para obtener una lista actualizada de proveedores de Azure admitidos, vea hello [Terraform documentación](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="5b8b6-159">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
