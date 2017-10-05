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
ms.openlocfilehash: 9660a95b440c2e4311829979e270d9f10099f624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="64989-103">Creación de una infraestructura básica de Azure mediante Terraform</span><span class="sxs-lookup"><span data-stu-id="64989-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="64989-104">En este artículo se describen los pasos que necesita realizar para aprovisionar una máquina virtual, en conjunto con la infraestructura subyacente, en Azure.</span><span class="sxs-lookup"><span data-stu-id="64989-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="64989-105">Sabrá cómo escribir scripts de Terraform y cómo visualizar los cambios antes de implementarlos en la infraestructura de nube.</span><span class="sxs-lookup"><span data-stu-id="64989-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="64989-106">También aprenderá a crear infraestructura en Azure mediante Terraform.</span><span class="sxs-lookup"><span data-stu-id="64989-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="64989-107">Para comenzar, cree un archivo llamado \terraform_azure101.tf en el editor de texto que prefiera (Visual Studio Code, Sublime, Vim, etc.).</span><span class="sxs-lookup"><span data-stu-id="64989-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="64989-108">El nombre exacto del archivo no es importante, porque Terraform acepta el nombre de la carpeta como parámetro: todos los scripts de la carpeta se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="64989-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="64989-109">Pegue el código siguiente en el nuevo archivo:</span><span class="sxs-lookup"><span data-stu-id="64989-109">Paste the following code in the new file:</span></span>

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
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
<span data-ttu-id="64989-110">En la sección `provider` del script, indique a Terraform que use un proveedor de Azure para aprovisionar recursos en el script.</span><span class="sxs-lookup"><span data-stu-id="64989-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="64989-111">Para obtener los valores de subscription_id, appId, password y tenant_id, consulte la guía de [instalación y configuración de Terraform](terraform-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="64989-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="64989-112">Si creó variables de entorno para los valores de este bloque, no necesita incluirlo.</span><span class="sxs-lookup"><span data-stu-id="64989-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="64989-113">El recurso `azurerm_resource_group` indica a Terraform que cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="64989-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="64989-114">Puede ver más tipos de recursos que están disponibles en Terraform más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="64989-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="64989-115">Ejecución del script</span><span class="sxs-lookup"><span data-stu-id="64989-115">Execute the script</span></span>
<span data-ttu-id="64989-116">Una vez que guarde el script, salga a la consola o línea de comandos y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="64989-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
<span data-ttu-id="64989-117">para inicializar el proveedor de Terraform de Azure.</span><span class="sxs-lookup"><span data-stu-id="64989-117">to initialize Terraform provider for Azure.</span></span> <span data-ttu-id="64989-118">A continuación, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="64989-118">Then type the following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="64989-119">Se supone que `terraformscripts` es la carpeta donde se guardó el script.</span><span class="sxs-lookup"><span data-stu-id="64989-119">We assume that `terraformscripts` is the folder where the script was saved.</span></span> <span data-ttu-id="64989-120">Hemos usado el comando `plan` de Terraform, que examina los recursos definidos en los scripts.</span><span class="sxs-lookup"><span data-stu-id="64989-120">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="64989-121">Los compara con la información de estado que se guarda mediante Terraform y, luego, genera la ejecución planeada _sin_ crear realmente recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="64989-121">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="64989-122">Después de ejecutar el comando anterior, debería ver una pantalla similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="64989-122">After you execute the previous command, you should see something like the following screen:</span></span>

![Plan de Terraform](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="64989-124">Si todo parece correcto, aprovisione este nuevo grupo de recursos en Azure ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="64989-124">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="64989-125">En Azure Portal, debería ver el nuevo grupo de recursos vacío llamado `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="64989-125">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="64989-126">En la sección siguiente, se agrega una máquina virtual y toda la infraestructura subyacente para esa máquina virtual al grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="64989-126">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="64989-127">Aprovisionamiento de una VM Ubuntu con Terraform</span><span class="sxs-lookup"><span data-stu-id="64989-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="64989-128">Extendamos el script de Terraform que creamos anteriormente con los detalles necesarios para aprovisionar una máquina virtual que ejecute Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="64989-128">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="64989-129">Estos son los recursos que se aprovisionan en las secciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="64989-129">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="64989-130">Una red con una sola subred</span><span class="sxs-lookup"><span data-stu-id="64989-130">A network with a single subnet</span></span>
* <span data-ttu-id="64989-131">Una tarjeta adaptadora de red</span><span class="sxs-lookup"><span data-stu-id="64989-131">A network interface card</span></span> 
* <span data-ttu-id="64989-132">Una cuenta de almacenamiento con un contenedor de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="64989-132">A storage account with a storage container</span></span>
* <span data-ttu-id="64989-133">Una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="64989-133">A public IP</span></span>
* <span data-ttu-id="64989-134">Una máquina virtual que usa todos los recursos anteriores</span><span class="sxs-lookup"><span data-stu-id="64989-134">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="64989-135">Para una documentación detallada de cada uno de los recursos de Terraform para Azure, consulte la [documentación de Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="64989-135">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="64989-136">También se proporciona la versión completa del [script de aprovisionamiento](#complete-terraform-script) para mayor comodidad.</span><span class="sxs-lookup"><span data-stu-id="64989-136">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="64989-137">Extensión del script de Terraform</span><span class="sxs-lookup"><span data-stu-id="64989-137">Extend the Terraform script</span></span>
<span data-ttu-id="64989-138">Extienda el script que se creó con los recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="64989-138">Extend the script that was created with the following resources:</span></span> 
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
<span data-ttu-id="64989-139">El script anterior crea una red virtual y una subred dentro de esa red virtual.</span><span class="sxs-lookup"><span data-stu-id="64989-139">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="64989-140">Observe la referencia al grupo de recursos que ya creó mediante "${azurerm_resource_group.helloterraform.name}", tanto en la definición de la red virtual como en la definición de la subred.</span><span class="sxs-lookup"><span data-stu-id="64989-140">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

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
<span data-ttu-id="64989-141">Los fragmentos de código de script anteriores crean una dirección IP pública y una interfaz de red que usa esa dirección.</span><span class="sxs-lookup"><span data-stu-id="64989-141">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="64989-142">Observe las referencias a subnet_id y public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="64989-142">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="64989-143">Terraform tiene inteligencia integrada para comprender que la interfaz de red depende de los recursos que se deben crear antes de crear dicha interfaz.</span><span class="sxs-lookup"><span data-stu-id="64989-143">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

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
<span data-ttu-id="64989-144">Aquí, ha creado una cuenta de almacenamiento y definido un contenedor de almacenamiento dentro de dicha cuenta.</span><span class="sxs-lookup"><span data-stu-id="64989-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="64989-145">Esta cuenta de almacenamiento es donde se almacenan los discos duros virtuales (VHD) para la máquina virtual que va a crear.</span><span class="sxs-lookup"><span data-stu-id="64989-145">This storage account is where you store virtual hard disks (VHDs) for the virtual machine about to be created.</span></span>

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
<span data-ttu-id="64989-146">Por último, en el fragmento de código anterior crea una máquina virtual que usa todos los recursos ya aprovisionados.</span><span class="sxs-lookup"><span data-stu-id="64989-146">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="64989-147">Son una cuenta de almacenamiento y un contenedor para un VHD, una interfaz de red con dirección IP pública y subred especificadas, y el grupo de recursos que ya creó.</span><span class="sxs-lookup"><span data-stu-id="64989-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="64989-148">Observe la propiedad vm_size, donde el script especifica un SKU de Azure A0.</span><span class="sxs-lookup"><span data-stu-id="64989-148">Note the vm_size property, where the script specifies an Azure A0 SKU.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="64989-149">Ejecución del script</span><span class="sxs-lookup"><span data-stu-id="64989-149">Execute the script</span></span>
<span data-ttu-id="64989-150">Una vez que guarde todo el script, salga a la consola o línea de comandos y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="64989-150">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="64989-151">Más tarde, los recursos, incluida una máquina virtual, aparece en el grupo de recursos `terraformtest` en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="64989-151">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="64989-152">Script completo de Terraform</span><span class="sxs-lookup"><span data-stu-id="64989-152">Complete Terraform script</span></span>

<span data-ttu-id="64989-153">Por comodidad, a continuación se muestra el script de Terraform completo que aprovisiona toda la infraestructura descrita en este artículo.</span><span class="sxs-lookup"><span data-stu-id="64989-153">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

```
variable "resourcesname" {
  default = "helloterraform"
}

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

## <a name="next-steps"></a><span data-ttu-id="64989-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64989-154">Next steps</span></span>
<span data-ttu-id="64989-155">Ha creado una infraestructura básica en Azure mediante Terraform.</span><span class="sxs-lookup"><span data-stu-id="64989-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="64989-156">Para escenarios más complejos, incluidos ejemplos sobre cómo usar equilibradores de carga y conjuntos de escalado de máquinas virtuales, consulte los diversos [ejemplos de Terraform para Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="64989-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="64989-157">Para una lista actualizada de los proveedores admitidos de Azure, consulte la [documentación de Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="64989-157">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
