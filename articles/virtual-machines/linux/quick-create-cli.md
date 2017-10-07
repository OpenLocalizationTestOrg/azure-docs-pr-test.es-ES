---
title: "aaaAzure inicio rápido: crear VM CLI | Documentos de Microsoft"
description: "Aprender rápidamente máquinas virtuales de toocreate con hello CLI de Azure."
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
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="05c7e-103">Crear una máquina virtual Linux con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="05c7e-103">Create a Linux virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="05c7e-104">Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="05c7e-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="05c7e-105">Esta guía se detalla con hello Azure CLI toodeploy una máquina virtual con Ubuntu server.</span><span class="sxs-lookup"><span data-stu-id="05c7e-105">This guide details using hello Azure CLI toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="05c7e-106">Una vez implementado el servidor de hello, se crea una conexión SSH y se instala un servidor Web NGINX.</span><span class="sxs-lookup"><span data-stu-id="05c7e-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="05c7e-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="05c7e-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="05c7e-108">Si elige tooinstall y usar hello CLI localmente, este tutorial rápido requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="05c7e-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="05c7e-109">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c7e-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="05c7e-110">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="05c7e-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="05c7e-111">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="05c7e-111">Create a resource group</span></span>

<span data-ttu-id="05c7e-112">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="05c7e-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="05c7e-113">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="05c7e-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="05c7e-114">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.</span><span class="sxs-lookup"><span data-stu-id="05c7e-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="05c7e-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="05c7e-115">Create virtual machine</span></span>

<span data-ttu-id="05c7e-116">Crear una máquina virtual con hello [crear vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="05c7e-116">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="05c7e-117">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM* y crea las claves de SSH si aún no existen en una ubicación de la clave predeterminada.</span><span class="sxs-lookup"><span data-stu-id="05c7e-117">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="05c7e-118">toouse con un conjunto específico de claves, use hello `--ssh-key-value` opción.</span><span class="sxs-lookup"><span data-stu-id="05c7e-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="05c7e-119">Cuando se ha creado la VM de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="05c7e-119">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="05c7e-120">Tome nota de hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="05c7e-120">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="05c7e-121">Esta dirección es hello tooaccess usa máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="05c7e-121">This address is used tooaccess hello VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="05c7e-122">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="05c7e-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="05c7e-123">De forma predeterminada, solo se permiten conexiones mediante SSH con las máquinas virtuales Linux implementadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="05c7e-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="05c7e-124">Si esta máquina virtual va toobe un servidor Web, deberá tooopen puerto 80 de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="05c7e-124">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="05c7e-125">Hola de uso [az de vm abrir puerto](/cli/azure/vm#open-port) comando tooopen hello deseado puerto.</span><span class="sxs-lookup"><span data-stu-id="05c7e-125">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="05c7e-126">Conexión SSH con la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="05c7e-126">SSH into your VM</span></span>

<span data-ttu-id="05c7e-127">Siguiente Hola de uso del comando toocreate una sesión SSH con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c7e-127">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="05c7e-128">Asegúrese de que tooreplace  *<publicIpAddress>*  con hello corregir la dirección IP pública de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="05c7e-128">Make sure tooreplace *<publicIpAddress>* with hello correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="05c7e-129">En el ejemplo anterior, la dirección IP era *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="05c7e-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="05c7e-130">Instalación de NGINX</span><span class="sxs-lookup"><span data-stu-id="05c7e-130">Install NGINX</span></span>

<span data-ttu-id="05c7e-131">Hola a uso continuación bash orígenes de paquetes de secuencia de comandos tooupdate e instala paquete NGINX más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="05c7e-131">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="05c7e-132">Página de bienvenida de vista hello NGINX</span><span class="sxs-lookup"><span data-stu-id="05c7e-132">View hello NGINX welcome page</span></span>

<span data-ttu-id="05c7e-133">Con NGINX instalado y el puerto 80 ahora abierta en la máquina virtual de Internet - Hola puede usar un explorador web de su elección tooview hello NGINX página de bienvenida predeterminada.</span><span class="sxs-lookup"><span data-stu-id="05c7e-133">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="05c7e-134">Estar seguro de hello toouse *publicIpAddress* documentó anteriormente página predeterminada de toovisit Hola.</span><span class="sxs-lookup"><span data-stu-id="05c7e-134">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Sitio predeterminado de NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="05c7e-136">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="05c7e-136">Clean up resources</span></span>

<span data-ttu-id="05c7e-137">Cuando ya no necesite, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="05c7e-137">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="05c7e-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05c7e-138">Next steps</span></span>

<span data-ttu-id="05c7e-139">En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web.</span><span class="sxs-lookup"><span data-stu-id="05c7e-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="05c7e-140">toolearn más información acerca de máquinas virtuales de Azure, continuar con tutorial toohello para máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="05c7e-140">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="05c7e-141">Tutoriales de máquinas virtuales Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="05c7e-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
