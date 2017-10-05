---
title: "Creación de una infraestructura básica de Azure mediante Terraform | Microsoft Docs"
description: "Obtenga información sobre cómo crear recursos de Azure mediante Terraform"
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
ms.openlocfilehash: aa0926de32dd85f4460bbfa84b7a6007e2199d51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="43919-103">Creación de una infraestructura básica de Azure mediante Terraform</span><span class="sxs-lookup"><span data-stu-id="43919-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="43919-104">En este artículo se describen los pasos que necesita realizar para aprovisionar una máquina virtual, en conjunto con la infraestructura subyacente, en Azure.</span><span class="sxs-lookup"><span data-stu-id="43919-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="43919-105">Sabrá cómo escribir scripts de Terraform y cómo visualizar los cambios antes de implementarlos en la infraestructura de nube.</span><span class="sxs-lookup"><span data-stu-id="43919-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="43919-106">También aprenderá a crear infraestructura en Azure mediante Terraform.</span><span class="sxs-lookup"><span data-stu-id="43919-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="43919-107">Para comenzar, cree un archivo llamado \terraform_azure101.tf en el editor de texto que prefiera (Visual Studio Code, Sublime, Vim, etc.).</span><span class="sxs-lookup"><span data-stu-id="43919-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="43919-108">El nombre exacto del archivo no es importante, porque Terraform acepta el nombre de la carpeta como parámetro: todos los scripts de la carpeta se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="43919-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="43919-109">Pegue el código siguiente en el nuevo archivo:</span><span class="sxs-lookup"><span data-stu-id="43919-109">Paste the following code in the new file:</span></span>

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
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
<span data-ttu-id="43919-110">En la sección `provider` del script, indique a Terraform que use un proveedor de Azure para aprovisionar recursos en el script.</span><span class="sxs-lookup"><span data-stu-id="43919-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="43919-111">Para obtener los valores de subscription_id, appId, password y tenant_id, consulte la guía de [instalación y configuración de Terraform](terraform-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="43919-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="43919-112">Si creó variables de entorno para los valores de este bloque, no necesita incluirlo.</span><span class="sxs-lookup"><span data-stu-id="43919-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="43919-113">El recurso `azurerm_resource_group` indica a Terraform que cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="43919-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="43919-114">Puede ver más tipos de recursos que están disponibles en Terraform más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="43919-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="43919-115">Ejecución del script</span><span class="sxs-lookup"><span data-stu-id="43919-115">Execute the script</span></span>
<span data-ttu-id="43919-116">Una vez que guarde el script, salga a la consola o línea de comandos y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="43919-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
 <span data-ttu-id="43919-117">para inicializar el proveedor de Terraform de Azure.</span><span class="sxs-lookup"><span data-stu-id="43919-117">to initialize the Terraform provider for Azure.</span></span> <span data-ttu-id="43919-118">A continuación, cambie el directorio a **terraformscripts** y ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="43919-118">Then change the directory to **terraformscripts**, and issue the following command:</span></span>
```
terraform plan
```
<span data-ttu-id="43919-119">Hemos usado el comando `plan` de Terraform, que examina los recursos definidos en los scripts.</span><span class="sxs-lookup"><span data-stu-id="43919-119">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="43919-120">Los compara con la información de estado que se guarda mediante Terraform y, luego, genera la ejecución planeada _sin_ crear realmente recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="43919-120">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="43919-121">Después de ejecutar el comando anterior, debería ver una pantalla similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="43919-121">After you execute the previous command, you should see something like the following screen:</span></span>

![Plan de Terraform](./media/terraform/tf_plan2.png)

<span data-ttu-id="43919-123">Si todo parece correcto, aprovisione este nuevo grupo de recursos en Azure ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="43919-123">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply
```
<span data-ttu-id="43919-124">En Azure Portal, debería ver el nuevo grupo de recursos vacío llamado `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="43919-124">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="43919-125">En la sección siguiente, se agrega una máquina virtual y toda la infraestructura subyacente para esa máquina virtual al grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="43919-125">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="43919-126">Aprovisionamiento de una VM Ubuntu con Terraform</span><span class="sxs-lookup"><span data-stu-id="43919-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="43919-127">Extendamos el script de Terraform que creamos anteriormente con los detalles necesarios para aprovisionar una máquina virtual que ejecute Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="43919-127">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="43919-128">Estos son los recursos que se aprovisionan en las secciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="43919-128">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="43919-129">Una red con una sola subred</span><span class="sxs-lookup"><span data-stu-id="43919-129">A network with a single subnet</span></span>
* <span data-ttu-id="43919-130">Una tarjeta adaptadora de red</span><span class="sxs-lookup"><span data-stu-id="43919-130">A network interface card</span></span> 
* <span data-ttu-id="43919-131">Una cuenta de almacenamiento para el diagnóstico de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="43919-131">A storage account for the virtual machine diagnostics</span></span>
* <span data-ttu-id="43919-132">Una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="43919-132">A public IP</span></span>
* <span data-ttu-id="43919-133">Una máquina virtual que usa todos los recursos anteriores</span><span class="sxs-lookup"><span data-stu-id="43919-133">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="43919-134">Para una documentación detallada de cada uno de los recursos de Terraform para Azure, consulte la [documentación de Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="43919-134">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="43919-135">También se proporciona la versión completa del [script de aprovisionamiento](#complete-terraform-script) para mayor comodidad.</span><span class="sxs-lookup"><span data-stu-id="43919-135">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="43919-136">Extensión del script de Terraform</span><span class="sxs-lookup"><span data-stu-id="43919-136">Extend the Terraform script</span></span>
<span data-ttu-id="43919-137">Extienda el script que se creó con los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="43919-137">Extend the script that was created with the following resources:</span></span> 
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
<span data-ttu-id="43919-138">El script anterior crea una red virtual y una subred dentro de esa red virtual.</span><span class="sxs-lookup"><span data-stu-id="43919-138">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="43919-139">Observe la referencia al grupo de recursos que ya creó mediante "${azurerm_resource_group.helloterraform.name}", tanto en la definición de la red virtual como en la definición de la subred.</span><span class="sxs-lookup"><span data-stu-id="43919-139">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

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
<span data-ttu-id="43919-140">Los fragmentos de código de script anteriores crean una dirección IP pública y una interfaz de red que usa esa dirección.</span><span class="sxs-lookup"><span data-stu-id="43919-140">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="43919-141">Observe las referencias a subnet_id y public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="43919-141">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="43919-142">Terraform tiene inteligencia integrada para comprender que la interfaz de red depende de los recursos que se deben crear antes de crear dicha interfaz.</span><span class="sxs-lookup"><span data-stu-id="43919-142">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

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
<span data-ttu-id="43919-143">En este caso, se crea una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="43919-143">Here, you created a storage account.</span></span> <span data-ttu-id="43919-144">Esta cuenta de almacenamiento es donde la máquina virtual almacenará sus detalles de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="43919-144">This storage account is where the virtual machine will store its diagnostics details.</span></span>

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
<span data-ttu-id="43919-145">Por último, en el fragmento de código anterior crea una máquina virtual que usa todos los recursos ya aprovisionados.</span><span class="sxs-lookup"><span data-stu-id="43919-145">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="43919-146">Son una cuenta de almacenamiento para los diagnósticos de la máquina virtual, una interfaz de red con dirección IP pública y subred especificadas, y el grupo de recursos que ya ha creado.</span><span class="sxs-lookup"><span data-stu-id="43919-146">They are a storage account for the virtual machine diagnostics, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="43919-147">Observe la propiedad vm_size, donde el script especifica un SKU de Azure Estándar DS1v2.</span><span class="sxs-lookup"><span data-stu-id="43919-147">Note the vm_size property, where the script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="43919-148">Debe proporcionar una clave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="43919-148">You are required to supply an SSH public key.</span></span> <span data-ttu-id="43919-149">Coloque el valor de clave pública en la sección **... INSERTE AQUÍ LA CLAVE PÚBLICA OPENSSH...**  anterioR.</span><span class="sxs-lookup"><span data-stu-id="43919-149">Place the public key value into the section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="43919-150">Se puede usar un par de claves ssh existentes o seguir la documentación de [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) o [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) para generar el par de claves.</span><span class="sxs-lookup"><span data-stu-id="43919-150">You can use an existing ssh key pair or follow the [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation to generate the key pair.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="43919-151">Ejecución del script</span><span class="sxs-lookup"><span data-stu-id="43919-151">Execute the script</span></span>
<span data-ttu-id="43919-152">Una vez que guarde todo el script, salga a la consola o línea de comandos y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="43919-152">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply
```
<span data-ttu-id="43919-153">Más tarde, los recursos, incluida una máquina virtual, aparece en el grupo de recursos `terraformtest` en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="43919-153">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="43919-154">Script completo de Terraform</span><span class="sxs-lookup"><span data-stu-id="43919-154">Complete Terraform script</span></span>

<span data-ttu-id="43919-155">Por comodidad, a continuación se muestra el script de Terraform completo que aprovisiona toda la infraestructura descrita en este artículo.</span><span class="sxs-lookup"><span data-stu-id="43919-155">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

```
# Configure the Microsoft Azure Provider
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

## <a name="next-steps"></a><span data-ttu-id="43919-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="43919-156">Next steps</span></span>
<span data-ttu-id="43919-157">Ha creado una infraestructura básica en Azure mediante Terraform.</span><span class="sxs-lookup"><span data-stu-id="43919-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="43919-158">Para escenarios más complejos, incluidos ejemplos sobre cómo usar equilibradores de carga y conjuntos de escalado de máquinas virtuales, consulte los diversos [ejemplos de Terraform para Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="43919-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="43919-159">Para una lista actualizada de los proveedores admitidos de Azure, consulte la [documentación de Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="43919-159">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
