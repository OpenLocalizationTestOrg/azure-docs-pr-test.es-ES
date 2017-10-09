---
title: "aaaCreate y administrar máquinas virtuales de Linux con Hola CLI de Azure | Documentos de Microsoft"
description: "Tutorial: crear y administrar máquinas virtuales de Linux con Hola CLI de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a><span data-ttu-id="dc6f3-103">Crear y administrar máquinas virtuales de Linux con Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="dc6f3-103">Create and Manage Linux VMs with hello Azure CLI</span></span>

<span data-ttu-id="dc6f3-104">Las máquinas virtuales de Azure proporcionan un entorno informático completamente configurable y flexible.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="dc6f3-105">En este tutorial se tratan elementos básicos de la implementación de máquinas virtuales de Azure, como la selección de su tamaño, la selección de una imagen de máquina virtual y la implementación de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="dc6f3-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="dc6f3-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dc6f3-107">Crear y conectar tooa VM</span><span class="sxs-lookup"><span data-stu-id="dc6f3-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="dc6f3-108">Seleccionar y usar imágenes de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="dc6f3-108">Select and use VM images</span></span>
> * <span data-ttu-id="dc6f3-109">Ver y usar tamaños de una máquina virtual específicos</span><span class="sxs-lookup"><span data-stu-id="dc6f3-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="dc6f3-110">Cambiar el tamaño de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc6f3-110">Resize a VM</span></span>
> * <span data-ttu-id="dc6f3-111">Ver y entender el estado de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="dc6f3-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dc6f3-112">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="dc6f3-113">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="dc6f3-114">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dc6f3-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="dc6f3-115">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="dc6f3-115">Create resource group</span></span>

<span data-ttu-id="dc6f3-116">Crear un grupo de recursos con hello [crear grupo az](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-116">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="dc6f3-117">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="dc6f3-118">Se debe crear un grupo de recursos antes de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="dc6f3-119">En este ejemplo, un grupo de recursos denominado *myResourceGroupVM* se crea en hello *eastus* región.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-119">In this example, a resource group named *myResourceGroupVM* is created in hello *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="dc6f3-120">grupo de recursos de Hola se especifica al crear o modificar una máquina virtual, que puede ser vista a lo largo de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="dc6f3-121">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="dc6f3-121">Create virtual machine</span></span>

<span data-ttu-id="dc6f3-122">Crear una máquina virtual con hello [crear vm az](https://docs.microsoft.com/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-122">Create a virtual machine with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="dc6f3-123">Al crear una máquina virtual, están disponibles varias opciones, como la imagen de sistema operativo, tamaño de disco y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="dc6f3-124">En este ejemplo, se crea una máquina virtual llamada *myVM* que se ejecuta en Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="dc6f3-125">Una vez Hola que se ha creado la máquina virtual, Hola CLI de Azure genera información acerca de hello VM.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-125">Once hello VM has been created, hello Azure CLI outputs information about hello VM.</span></span> <span data-ttu-id="dc6f3-126">Tome nota de hello `publicIpAddress`, esta dirección puede ser una máquina virtual de tooaccess usado Hola...</span><span class="sxs-lookup"><span data-stu-id="dc6f3-126">Take note of hello `publicIpAddress`, this address can be used tooaccess hello virtual machine..</span></span> 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a><span data-ttu-id="dc6f3-127">Conectar tooVM</span><span class="sxs-lookup"><span data-stu-id="dc6f3-127">Connect tooVM</span></span>

<span data-ttu-id="dc6f3-128">Ahora puede conectarse toohello VM mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-128">You can now connect toohello VM using SSH.</span></span> <span data-ttu-id="dc6f3-129">Reemplace la dirección IP de ejemplo de Hola con hello `publicIpAddress` anotó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-129">Replace hello example IP address with hello `publicIpAddress` noted in hello previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="dc6f3-130">Una vez finalizado con hello VM, cierre la sesión de SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-130">Once finished with hello VM, close hello SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="dc6f3-131">Descripción de las imágenes de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc6f3-131">Understand VM images</span></span>

<span data-ttu-id="dc6f3-132">Hello Azure marketplace incluye muchas imágenes que pueden ser utilizados toocreate las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-132">hello Azure marketplace includes many images that can be used toocreate VMs.</span></span> <span data-ttu-id="dc6f3-133">En los pasos anteriores de hello, una máquina virtual se creó con una imagen de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-133">In hello previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="dc6f3-134">En este paso, Hola que CLI de Azure es marketplace de hello toosearch usado para una imagen de CentOS, que es, a continuación, utiliza toodeploy una segunda máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-134">In this step, hello Azure CLI is used toosearch hello marketplace for a CentOS image, which is then used toodeploy a second virtual machine.</span></span>  

<span data-ttu-id="dc6f3-135">toosee una lista de hello suelen usarse imágenes, use hello [lista de imágenes de máquina virtual de az](/cli/azure/vm/image#list) comando.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-135">toosee a list of hello most commonly used images, use hello [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="dc6f3-136">resultado del comando Hello devuelve imágenes de máquina virtual más populares de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-136">hello command output returns hello most popular VM images on Azure.</span></span>

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

<span data-ttu-id="dc6f3-137">Puede ver una lista completa mediante la adición de hello `--all` argumento.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-137">A full list can be seen by adding hello `--all` argument.</span></span> <span data-ttu-id="dc6f3-138">También se puede filtrar la lista de imágenes de Hola por `--publisher` o `–-offer`.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-138">hello image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="dc6f3-139">En este ejemplo, se filtra la lista de Hola para todas las imágenes con una oferta que coincida con *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-139">In this example, hello list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="dc6f3-140">Salida parcial:</span><span class="sxs-lookup"><span data-stu-id="dc6f3-140">Partial output:</span></span>

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

<span data-ttu-id="dc6f3-141">toodeploy una máquina virtual mediante una imagen específica, tome nota del valor de hello en hello *Urn* columna.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-141">toodeploy a VM using a specific image, take note of hello value in hello *Urn* column.</span></span> <span data-ttu-id="dc6f3-142">Al especificar la imagen de hello, número de versión de imagen de hello puede reemplazarse con "más reciente", que selecciona la versión más reciente de Hola de distribución de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-142">When specifying hello image, hello image version number can be replaced with “latest”, which selects hello latest version of hello distribution.</span></span> <span data-ttu-id="dc6f3-143">En este ejemplo, Hola `--image` argumento es la versión más reciente de hello toospecify utilizadas de una imagen de CentOS 6.5.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-143">In this example, hello `--image` argument is used toospecify hello latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="dc6f3-144">Comprensión de los tamaños de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc6f3-144">Understand VM sizes</span></span>

<span data-ttu-id="dc6f3-145">Un tamaño de máquina virtual determina la cantidad de Hola de recursos de proceso, como CPU y GPU, memoria que se realizan la máquina virtual de toohello disponible.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-145">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="dc6f3-146">Máquinas virtuales deben toobe el tamaño adecuado para la carga de trabajo de hello esperado.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-146">Virtual machines need toobe sized appropriately for hello expected work load.</span></span> <span data-ttu-id="dc6f3-147">Si aumenta la carga de trabajo, se puede cambiar el tamaño de una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="dc6f3-148">Tamaños de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc6f3-148">VM Sizes</span></span>

<span data-ttu-id="dc6f3-149">Hello en la tabla siguiente clasifica tamaños en casos de uso.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-149">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="dc6f3-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="dc6f3-150">Type</span></span>                     | <span data-ttu-id="dc6f3-151">Tamaños</span><span class="sxs-lookup"><span data-stu-id="dc6f3-151">Sizes</span></span>           |    <span data-ttu-id="dc6f3-152">Descripción</span><span class="sxs-lookup"><span data-stu-id="dc6f3-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="dc6f3-153">Uso general</span><span class="sxs-lookup"><span data-stu-id="dc6f3-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="dc6f3-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="dc6f3-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="dc6f3-155">Uso equilibrado de CPU y memoria.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="dc6f3-156">Ideal para desarrollo / pruebas y las soluciones de aplicaciones y datos de toomedium pequeños.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-156">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| [<span data-ttu-id="dc6f3-157">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="dc6f3-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="dc6f3-158">Fs, F</span><span class="sxs-lookup"><span data-stu-id="dc6f3-158">Fs, F</span></span>             | <span data-ttu-id="dc6f3-159">Uso elevado de la CPU respecto a la memoria.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-159">High CPU-to-memory.</span></span> <span data-ttu-id="dc6f3-160">Adecuado para aplicaciones, dispositivos de red y procesos por lotes con tráfico mediano.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="dc6f3-161">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="dc6f3-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="dc6f3-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="dc6f3-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="dc6f3-163">Uso elevado de memoria respecto al núcleo.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-163">High memory-to-core.</span></span> <span data-ttu-id="dc6f3-164">Muy bien para bases de datos relacionales, las cachés de toolarge intermedio y análisis en memoria.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-164">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="dc6f3-165">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="dc6f3-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="dc6f3-166">LS</span><span class="sxs-lookup"><span data-stu-id="dc6f3-166">Ls</span></span>                | <span data-ttu-id="dc6f3-167">Alto rendimiento de disco y E/S.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-167">High disk throughput and IO.</span></span> <span data-ttu-id="dc6f3-168">Perfecto para bases de datos SQL y NoSQL y macrodatos.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="dc6f3-169">GPU</span><span class="sxs-lookup"><span data-stu-id="dc6f3-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="dc6f3-170">NV, NC</span><span class="sxs-lookup"><span data-stu-id="dc6f3-170">NV, NC</span></span>            | <span data-ttu-id="dc6f3-171">Máquinas virtuales especializadas específicas para actividades intensas de representación de gráficos y edición de vídeo.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="dc6f3-172">Alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="dc6f3-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="dc6f3-173">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="dc6f3-173">H, A8-11</span></span>          | <span data-ttu-id="dc6f3-174">Nuestras máquinas virtuales con CPU más eficaces e interfaces de red de alto rendimiento (RDMA) opcionales.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="dc6f3-175">Búsqueda de los tamaños de máquina virtual disponibles</span><span class="sxs-lookup"><span data-stu-id="dc6f3-175">Find available VM sizes</span></span>

<span data-ttu-id="dc6f3-176">toosee una lista de la máquina virtual los tamaños disponibles en una región determinada, use hello [tamaños de lista de máquinas virtuales az](/cli/azure/vm#list-sizes) comando.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-176">toosee a list of VM sizes available in a particular region, use hello [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="dc6f3-177">Salida parcial:</span><span class="sxs-lookup"><span data-stu-id="dc6f3-177">Partial output:</span></span>

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="dc6f3-178">Creación de máquinas virtuales con un tamaño específico</span><span class="sxs-lookup"><span data-stu-id="dc6f3-178">Create VM with specific size</span></span>

<span data-ttu-id="dc6f3-179">En el ejemplo de creación de VM anterior hello, un tamaño no se proporcionó, lo que produce un tamaño predeterminado.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-179">In hello previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="dc6f3-180">Se puede seleccionar un tamaño de máquina virtual en el momento de creación utilizando [crear vm az](/cli/azure/vm#create) hello y `--size` argumento.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and hello `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="dc6f3-181">Cambiar el tamaño de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc6f3-181">Resize a VM</span></span>

<span data-ttu-id="dc6f3-182">Una vez implementada una máquina virtual, puede tooincrease cuyo tamaño ha cambiado o reducir la asignación de recursos.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-182">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="dc6f3-183">Antes de cambiar el tamaño de una máquina virtual, compruebe si hello tamaño deseado está disponible en el clúster de Azure actual Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-183">Before resizing a VM, check if hello desired size is available on hello current Azure cluster.</span></span> <span data-ttu-id="dc6f3-184">Hola [lista de vm az-vm-resize-options](/cli/azure/vm#list-vm-resize-options) comando devuelve la lista de tamaños de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-184">hello [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns hello list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="dc6f3-185">Si Hola deseado tamaño está disponible, hello VM puede cambiarse desde un estado encendido, sin embargo, se reinicia durante la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-185">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span> <span data-ttu-id="dc6f3-186">Hola de uso [cambiar el tamaño de vm az]( /cli/azure/vm#resize) comando tooperform Hola resize.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-186">Use hello [az vm resize]( /cli/azure/vm#resize) command tooperform hello resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="dc6f3-187">Si Hola tamaño deseado no está en el clúster actual hello, Hola VM necesidades puede producirse toobe cancela la asignación antes de hello cambiar el tamaño de operación.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-187">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="dc6f3-188">Hola de uso [cancelar la asignación de máquina virtual az]( /cli/azure/vm#deallocate) comando toostop y cancelar la asignación Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-188">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span> <span data-ttu-id="dc6f3-189">Tenga en cuenta que cuando hello máquina virtual está encendida volver, desaparecerán todos los datos en disco temporal de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-189">Note, when hello VM is powered back on, any data on hello temp disk may be removed.</span></span> <span data-ttu-id="dc6f3-190">dirección IP pública de Hello también cambia a menos que se está usando una dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-190">hello public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="dc6f3-191">Una vez cancelada la asignación, puede producirse el cambio de tamaño de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-191">Once deallocated, hello resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="dc6f3-192">Después de cambiar el tamaño de hello, Hola VM se puede iniciar.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-192">After hello resize, hello VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="dc6f3-193">Estados de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc6f3-193">VM power states</span></span>

<span data-ttu-id="dc6f3-194">Una máquina virtual de Azure puede tener uno de muchos estados de energía.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="dc6f3-195">Este estado representa estado actual de Hola de hello VM desde la perspectiva de Hola de hipervisor de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-195">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="dc6f3-196">Estados de energía</span><span class="sxs-lookup"><span data-stu-id="dc6f3-196">Power states</span></span>

| <span data-ttu-id="dc6f3-197">Estado de energía</span><span class="sxs-lookup"><span data-stu-id="dc6f3-197">Power State</span></span> | <span data-ttu-id="dc6f3-198">Descripción</span><span class="sxs-lookup"><span data-stu-id="dc6f3-198">Description</span></span>
|----|----|
| <span data-ttu-id="dc6f3-199">Iniciando</span><span class="sxs-lookup"><span data-stu-id="dc6f3-199">Starting</span></span> | <span data-ttu-id="dc6f3-200">Indica que se está iniciando la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-200">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="dc6f3-201">En ejecución</span><span class="sxs-lookup"><span data-stu-id="dc6f3-201">Running</span></span> | <span data-ttu-id="dc6f3-202">Indica que la máquina virtual Hola se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-202">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="dc6f3-203">Deteniéndose</span><span class="sxs-lookup"><span data-stu-id="dc6f3-203">Stopping</span></span> | <span data-ttu-id="dc6f3-204">Indica que la máquina virtual Hola se está deteniendo.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-204">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="dc6f3-205">Stopped</span><span class="sxs-lookup"><span data-stu-id="dc6f3-205">Stopped</span></span> | <span data-ttu-id="dc6f3-206">Indica que la máquina virtual Hola se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-206">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="dc6f3-207">Máquinas virtuales en estado de hello detenido sigue acumulando cargos de proceso.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-207">Virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="dc6f3-208">Desasignando</span><span class="sxs-lookup"><span data-stu-id="dc6f3-208">Deallocating</span></span> | <span data-ttu-id="dc6f3-209">Indica que la máquina virtual Hola se está desasignando.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-209">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="dc6f3-210">Desasignado</span><span class="sxs-lookup"><span data-stu-id="dc6f3-210">Deallocated</span></span> | <span data-ttu-id="dc6f3-211">Indica que la máquina virtual Hola está quitarse de hipervisor de hello pero seguirá estando disponible en el plano de control de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-211">Indicates that hello virtual machine is removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="dc6f3-212">Máquinas virtuales en estado desasignado hello no acumulando cargos de proceso.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-212">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="dc6f3-213">Indica que el estado de energía de Hola de máquina virtual de hello es desconocido.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-213">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="dc6f3-214">Búsqueda del estado de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc6f3-214">Find power state</span></span>

<span data-ttu-id="dc6f3-215">estado de hello tooretrieve de una máquina virtual concreta, use hello [az vm obtener vista de instancia](/cli/azure/vm#get-instance-view) comando.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-215">tooretrieve hello state of a particular VM, use hello [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="dc6f3-216">Ser seguro toospecify un nombre válido para una máquina virtual y el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-216">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="dc6f3-217">Salida:</span><span class="sxs-lookup"><span data-stu-id="dc6f3-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="dc6f3-218">Tareas de administración</span><span class="sxs-lookup"><span data-stu-id="dc6f3-218">Management tasks</span></span>

<span data-ttu-id="dc6f3-219">Durante el ciclo de vida Hola de una máquina virtual, puede desear toorun tareas de administración, como iniciar, detener o eliminar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-219">During hello life-cycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="dc6f3-220">Además, puede que desee toocreate tooautomate repetitivas o complejas tareas de secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-220">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="dc6f3-221">Con hello CLI de Azure, muchas tareas comunes de administración se pueden ejecutar desde la línea de comandos de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-221">Using hello Azure CLI, many common management tasks can be run from hello command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="dc6f3-222">Obtención de dirección IP</span><span class="sxs-lookup"><span data-stu-id="dc6f3-222">Get IP address</span></span>

<span data-ttu-id="dc6f3-223">Este comando devuelve las direcciones IP de hello públicas y privadas de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-223">This command returns hello private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="dc6f3-224">Detener una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc6f3-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="dc6f3-225">Iniciar una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc6f3-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="dc6f3-226">Eliminación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="dc6f3-226">Delete resource group</span></span>

<span data-ttu-id="dc6f3-227">Al eliminar un grupo de recursos se eliminan también todos los recursos contenidos en el mismo.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="dc6f3-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc6f3-228">Next steps</span></span>

<span data-ttu-id="dc6f3-229">En este tutorial, ha aprendido conceptos básicos sobre la creación y administración de máquinas virtuales. Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dc6f3-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dc6f3-230">Crear y conectar tooa VM</span><span class="sxs-lookup"><span data-stu-id="dc6f3-230">Create and connect tooa VM</span></span>
> * <span data-ttu-id="dc6f3-231">Seleccionar y usar imágenes de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="dc6f3-231">Select and use VM images</span></span>
> * <span data-ttu-id="dc6f3-232">Ver y usar tamaños de una máquina virtual específicos</span><span class="sxs-lookup"><span data-stu-id="dc6f3-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="dc6f3-233">Cambiar el tamaño de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc6f3-233">Resize a VM</span></span>
> * <span data-ttu-id="dc6f3-234">Ver y entender el estado de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="dc6f3-234">View and understand VM state</span></span>

<span data-ttu-id="dc6f3-235">Avanzar toohello toolearn de tutorial siguiente acerca de los discos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dc6f3-235">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc6f3-236">Creación y administración de discos de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="dc6f3-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
