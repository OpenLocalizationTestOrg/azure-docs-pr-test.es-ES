---
title: "Inicio rápido de Azure: creación de máquinas virtuales con la CLI | Microsoft Docs"
description: "Aprenda rápidamente a crear una máquina virtual con la CLI de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: a7cba5b2c43704d92e36d6f808efaa9fc73fdf36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="cbddd-103">Creación de una máquina virtual Linux con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cbddd-103">Create a Linux virtual machine with the Azure CLI</span></span>

<span data-ttu-id="cbddd-104">La CLI de Azure se usa para crear y administrar recursos de Azure desde la línea de comandos o en scripts.</span><span class="sxs-lookup"><span data-stu-id="cbddd-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="cbddd-105">En esta guía se detalla cómo usar la CLI de Azure para implementar máquinas virtuales que ejecutan el servidor de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="cbddd-105">This guide details using the Azure CLI to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="cbddd-106">Una vez implementado el servidor, se crea una conexión SSH y se instala un servidor web NGINX.</span><span class="sxs-lookup"><span data-stu-id="cbddd-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="cbddd-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="cbddd-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cbddd-108">Si decide instalar y usar la CLI localmente, para esta guía de inicio rápido es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="cbddd-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cbddd-109">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="cbddd-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="cbddd-110">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cbddd-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="cbddd-111">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cbddd-111">Create a resource group</span></span>

<span data-ttu-id="cbddd-112">Cree un grupo de recursos con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="cbddd-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="cbddd-113">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="cbddd-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="cbddd-114">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *eastus*.</span><span class="sxs-lookup"><span data-stu-id="cbddd-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="cbddd-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="cbddd-115">Create virtual machine</span></span>

<span data-ttu-id="cbddd-116">Cree la máquina virtual con el comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="cbddd-116">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="cbddd-117">En el ejemplo siguiente, se crea una máquina virtual denominada *myVM* y las claves SSH si aún no existen en una ubicación de claves predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cbddd-117">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="cbddd-118">Para utilizar un conjunto específico de claves, utilice la opción `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="cbddd-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="cbddd-119">Cuando se ha creado la máquina virtual, la CLI de Azure muestra información similar al ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="cbddd-119">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="cbddd-120">Anote el valor de `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="cbddd-120">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="cbddd-121">Esta dirección se utiliza para tener acceso a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cbddd-121">This address is used to access the VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="cbddd-122">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="cbddd-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="cbddd-123">De forma predeterminada, solo se permiten conexiones mediante SSH con las máquinas virtuales Linux implementadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="cbddd-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="cbddd-124">Si esta máquina virtual va a ser un servidor web, debe abrir el puerto 80 desde Internet.</span><span class="sxs-lookup"><span data-stu-id="cbddd-124">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="cbddd-125">Use el comando [az vm open-port](/cli/azure/vm#open-port) para abrir el puerto deseado.</span><span class="sxs-lookup"><span data-stu-id="cbddd-125">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="cbddd-126">Conexión SSH con la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cbddd-126">SSH into your VM</span></span>

<span data-ttu-id="cbddd-127">Ejecute el comando siguiente para crear una sesión SSH con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cbddd-127">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="cbddd-128">Asegúrese de reemplazar *<publicIpAddress>* por la dirección IP pública correcta de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cbddd-128">Make sure to replace *<publicIpAddress>* with the correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="cbddd-129">En el ejemplo anterior, la dirección IP era *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="cbddd-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="cbddd-130">Instalación de NGINX</span><span class="sxs-lookup"><span data-stu-id="cbddd-130">Install NGINX</span></span>

<span data-ttu-id="cbddd-131">Use el siguiente script de bash para actualizar los orígenes de paquetes e instalar el paquete NGINX más reciente.</span><span class="sxs-lookup"><span data-stu-id="cbddd-131">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="cbddd-132">Visualización de la página de bienvenida de NGINX</span><span class="sxs-lookup"><span data-stu-id="cbddd-132">View the NGINX welcome page</span></span>

<span data-ttu-id="cbddd-133">Con NGINX instalado y el puerto 80 abierto en la máquina virtual desde Internet, puede usar el explorador web que elija para ver la página principal de NGINX.</span><span class="sxs-lookup"><span data-stu-id="cbddd-133">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="cbddd-134">Asegúrese de utilizar el valor de *publicIpAddress* que ha anotado antes para visitar la página predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cbddd-134">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![Sitio predeterminado de NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="cbddd-136">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="cbddd-136">Clean up resources</span></span>

<span data-ttu-id="cbddd-137">Cuando ya no se necesiten, puede usar el comando [az group delete](/cli/azure/group#delete) para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="cbddd-137">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="cbddd-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cbddd-138">Next steps</span></span>

<span data-ttu-id="cbddd-139">En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web.</span><span class="sxs-lookup"><span data-stu-id="cbddd-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="cbddd-140">Para más información acerca de las máquinas virtuales de Azure, continúe con el tutorial de máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="cbddd-140">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="cbddd-141">Tutoriales de máquinas virtuales Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="cbddd-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
