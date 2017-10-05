---
title: "Inicio rápido de Azure: creación de máquinas virtuales con la CLI Microsoft Docs"
description: "Aprenda rápidamente a crear una máquina virtual Windows con la CLI de Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: fcb2f1389b3434d0d2e3145217e54ceb2326b969
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="cfe78-103">Creación de una máquina virtual Windows con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cfe78-103">Create a Windows virtual machine with the Azure CLI</span></span>

<span data-ttu-id="cfe78-104">La CLI de Azure se usa para crear y administrar recursos de Azure desde la línea de comandos o en scripts.</span><span class="sxs-lookup"><span data-stu-id="cfe78-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="cfe78-105">Esta guía se detalla cómo usar la CLI de Azure para implementar máquinas virtuales con Windows Server 2016. </span><span class="sxs-lookup"><span data-stu-id="cfe78-105">This guide details using the Azure CLI to deploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="cfe78-106">Una vez completada la implementación, nos conectaremos al servidor e instalaremos IIS.
</span><span class="sxs-lookup"><span data-stu-id="cfe78-106">Once deployment is complete, we connect to the server and install IIS.</span></span>

<span data-ttu-id="cfe78-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="cfe78-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cfe78-108">Si decide instalar y usar la CLI localmente, para esta guía de inicio rápido es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="cfe78-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cfe78-109">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="cfe78-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="cfe78-110">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cfe78-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="cfe78-111">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cfe78-111">Create a resource group</span></span>

<span data-ttu-id="cfe78-112">Cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="cfe78-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="cfe78-113">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe78-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="cfe78-114">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *eastus*.</span><span class="sxs-lookup"><span data-stu-id="cfe78-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="cfe78-115">Crear máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cfe78-115">Create virtual machine</span></span>

<span data-ttu-id="cfe78-116">Cree la máquina virtual con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="cfe78-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="cfe78-117">En el ejemplo siguiente se crea una máquina virtual denominada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="cfe78-117">The following example creates a VM named *myVM*.</span></span> <span data-ttu-id="cfe78-118">En este ejemplo se utiliza *azureuser* como nombre de usuario administrativo y *myPassword12* como contraseña.</span><span class="sxs-lookup"><span data-stu-id="cfe78-118">This example uses *azureuser* for an administrative user name and *myPassword12* as the password.</span></span> <span data-ttu-id="cfe78-119">Actualice estos valores a un valor apropiado para su entorno.</span><span class="sxs-lookup"><span data-stu-id="cfe78-119">Update these values to something appropriate to your environment.</span></span> <span data-ttu-id="cfe78-120">Estos valores son necesarios cuando se crea una conexión con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfe78-120">These values are needed when creating a connection with the virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="cfe78-121">Cuando se ha creado la máquina virtual, la CLI de Azure muestra información similar al ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="cfe78-121">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="cfe78-122">Anote el valor de `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="cfe78-122">Take note of the `publicIpAaddress`.</span></span> <span data-ttu-id="cfe78-123">Esta dirección se utiliza para tener acceso a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfe78-123">This address is used to access the VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="cfe78-124">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="cfe78-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="cfe78-125">De forma predeterminada, solo se permiten conexiones RDP con las máquinas virtuales Windows implementadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe78-125">By default only RDP connections are allowed in to Windows virtual machines deployed in Azure.</span></span> <span data-ttu-id="cfe78-126">Si esta máquina virtual va a ser un servidor web, debe abrir el puerto 80 desde Internet.</span><span class="sxs-lookup"><span data-stu-id="cfe78-126">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="cfe78-127">Use el comando [az vm open-port](/cli/azure/vm#open-port) para abrir el puerto deseado.</span><span class="sxs-lookup"><span data-stu-id="cfe78-127">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="cfe78-128">Conexión a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cfe78-128">Connect to virtual machine</span></span>

<span data-ttu-id="cfe78-129">Ejecute el comando siguiente para crear una sesión del Escritorio remoto con la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfe78-129">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="cfe78-130">Reemplace la dirección IP con la dirección IP pública de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfe78-130">Replace the IP address with the public IP address of your virtual machine.</span></span> <span data-ttu-id="cfe78-131">Cuando se le solicite, escriba las credenciales usadas al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfe78-131">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="cfe78-132">Instalación de IIS mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="cfe78-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="cfe78-133">Ahora que ha iniciado sesión en la máquina virtual de Azure, puede usar una sola línea de PowerShell para instalar IIS y habilitar la regla de firewall local para permitir el tráfico web.</span><span class="sxs-lookup"><span data-stu-id="cfe78-133">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="cfe78-134">Abra una ventana de PowerShell y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cfe78-134">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="cfe78-135">Página principal de IIS</span><span class="sxs-lookup"><span data-stu-id="cfe78-135">View the IIS welcome page</span></span>

<span data-ttu-id="cfe78-136">Con IIS instalado y el puerto 80 abierto en la máquina virtual desde Internet, puede usar el explorador web que elija para ver la página principal de IIS.</span><span class="sxs-lookup"><span data-stu-id="cfe78-136">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="cfe78-137">Asegúrese de utilizar la dirección IP pública que ha anotado antes para visitar la página predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cfe78-137">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Sitio predeterminado de IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="cfe78-139">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="cfe78-139">Clean up resources</span></span>

<span data-ttu-id="cfe78-140">Cuando ya no se necesiten, puede usar el comando [az group delete](/cli/azure/group#delete) para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="cfe78-140">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="cfe78-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cfe78-141">Next steps</span></span>

<span data-ttu-id="cfe78-142">En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web.</span><span class="sxs-lookup"><span data-stu-id="cfe78-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="cfe78-143">Para más información acerca de las máquinas virtuales de Azure, continúe con el tutorial de máquinas virtuales Windows.</span><span class="sxs-lookup"><span data-stu-id="cfe78-143">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cfe78-144">Tutoriales de máquinas virtuales Windows de Azure</span><span class="sxs-lookup"><span data-stu-id="cfe78-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
