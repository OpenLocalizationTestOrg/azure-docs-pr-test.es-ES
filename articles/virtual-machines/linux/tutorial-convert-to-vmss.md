---
title: "establece de aaaConvert una escala de tooa de máquina virtual de Azure | Documentos de Microsoft"
description: "Cree e implemente una escala de máquinas virtuales de Linux Azure establecido con hello CLI de Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="61a7c-103">Convertir un conjunto de escala de tooa de máquina virtual de Azure existente</span><span class="sxs-lookup"><span data-stu-id="61a7c-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="61a7c-104">Este tutorial muestra cómo toouse CLI de Azure 2.0 tooconvert una escala de máquinas virtuales de máquina virtual tooa establece.</span><span class="sxs-lookup"><span data-stu-id="61a7c-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="61a7c-105">También aprenderá cómo establece la configuración de hello tooautomate de máquinas virtuales de hello en escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a7c-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="61a7c-106">Para obtener más información sobre cómo tooinstall CLI de Azure 2.0, consulte [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="61a7c-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="61a7c-107">Para más información acerca de los conjuntos de escala, consulte [Conjuntos de escala de máquinas virtuales](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61a7c-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="61a7c-108">Paso 1: desaprovisionar Hola VM</span><span class="sxs-lookup"><span data-stu-id="61a7c-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="61a7c-109">Utilizar SSH tooconnect toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61a7c-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="61a7c-110">Hola de desaprovisionamiento VM utilizando archivos de toodelete del agente de máquina virtual de Azure de Hola y los datos.</span><span class="sxs-lookup"><span data-stu-id="61a7c-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="61a7c-111">Para obtener una descripción detallada de desaprovisionamiento, consulte [Captura una máquina virtual Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="61a7c-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="61a7c-112">Paso 2: capturar una imagen de máquina virtual de hello</span><span class="sxs-lookup"><span data-stu-id="61a7c-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="61a7c-113">Para obtener una descripción detallada de la captura, consulte [Captura de una máquina virtual Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="61a7c-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="61a7c-114">Cancela la asignación de Hola VM con [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="61a7c-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="61a7c-115">Generalizar Hola VM con [az vm generalizar](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="61a7c-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="61a7c-116">Crear una imagen desde el recurso de máquina virtual de hello con [crear imagen az](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="61a7c-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="61a7c-117">Paso 3: crear el conjunto de escalas de Hola</span><span class="sxs-lookup"><span data-stu-id="61a7c-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="61a7c-118">Obtener hello **identificador** de imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a7c-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="61a7c-119">Cree una máquina virtual a partir de un recurso de imagen con [az vmss create](/cli/azure/vmss#create):</span><span class="sxs-lookup"><span data-stu-id="61a7c-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="61a7c-120">Este comando también adjunta un disco de datos de 10gb.</span><span class="sxs-lookup"><span data-stu-id="61a7c-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="61a7c-121">Tenga en cuenta que dependiendo de hello VM tamaño elegido (utilizáramos **Standard_DS1_v2**), número de Hola de discos de datos permitido es diferente.</span><span class="sxs-lookup"><span data-stu-id="61a7c-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="61a7c-122">Para obtener más información, consulte hello [tamaños de máquina virtual](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="61a7c-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="61a7c-123">Una vez que termine de conjunto de escalado de hello, conectar tooit.</span><span class="sxs-lookup"><span data-stu-id="61a7c-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="61a7c-124">Obtener una lista de direcciones IP para las instancias de Hola de SSH con [vmss az-instancia de lista-info conexión](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="61a7c-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="61a7c-125">Ahora puede conectar el disco de datos de la instancia tooinitialize toohello máquina virtual Hola</span><span class="sxs-lookup"><span data-stu-id="61a7c-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="61a7c-126">Paso 4: disco de datos de inicialización Hola</span><span class="sxs-lookup"><span data-stu-id="61a7c-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="61a7c-127">Mientras la máquina virtual de toohello conectado, particionar el disco de hello con `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="61a7c-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="61a7c-128">Escribir una partición de toohello de sistema de archivos con hello `mkfs` comando:</span><span class="sxs-lookup"><span data-stu-id="61a7c-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="61a7c-129">Montar el disco nuevo de Hola para que sea accesible en el sistema operativo de hello:</span><span class="sxs-lookup"><span data-stu-id="61a7c-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="61a7c-130">disco de Hello ahora puede tener acceso a través de hello datadrive punto de montaje, que se puede comprobar con `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="61a7c-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="61a7c-131">Finalizar la sesión SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="61a7c-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="61a7c-132">Paso 5: Configuración del firewall</span><span class="sxs-lookup"><span data-stu-id="61a7c-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="61a7c-133">Perforación un "agujero" a través de hello firewall toohello webserver hospedado por conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a7c-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="61a7c-134">Cuando se creó el conjunto de escalas de hello, también se ha creado un equilibrador de carga y utilizó **SSH** toohello las máquinas virtuales individuales.</span><span class="sxs-lookup"><span data-stu-id="61a7c-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="61a7c-135">tooopen un puerto, necesita dos fragmentos de información, que puede obtener mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="61a7c-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="61a7c-136">**Grupo de direcciones IP de front-end**</span><span class="sxs-lookup"><span data-stu-id="61a7c-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="61a7c-137">**Grupo de direcciones IP de back-end**</span><span class="sxs-lookup"><span data-stu-id="61a7c-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="61a7c-138">Con los dos nombres, puede abrir el puerto **80**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="61a7c-139">Paso 6: Automatización de la configuración</span><span class="sxs-lookup"><span data-stu-id="61a7c-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="61a7c-140">disco de datos de Hello debe toobe configurado en cada instancia de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61a7c-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="61a7c-141">Se puede automatizar la configuración de Hola de máquina virtual de hello con hello **CustomScript** extensión.</span><span class="sxs-lookup"><span data-stu-id="61a7c-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="61a7c-142">En primer lugar, cree un *.sh* secuencia de comandos que incluye comandos de formato de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a7c-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="61a7c-143">A continuación, cargar ese Hola de toowhere del archivo de script **CustomScript** extensión puede tener acceso a él.</span><span class="sxs-lookup"><span data-stu-id="61a7c-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="61a7c-144">Hay disponible una copia [aquí](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="61a7c-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="61a7c-145">Cree un archivo local denominado **settings.json** y put hello siguiente bloque JSON en ella.</span><span class="sxs-lookup"><span data-stu-id="61a7c-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="61a7c-146">Hola `flieUris` propiedad se debe establecer toowhere cargado en el archivo de script.</span><span class="sxs-lookup"><span data-stu-id="61a7c-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="61a7c-147">Implementar esta escala de tooyour comando establecida con hello **CustomScript** extensión, que hacen referencia a hello **settings.json** archivos que acabamos de crear.</span><span class="sxs-lookup"><span data-stu-id="61a7c-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="61a7c-148">Esta extensión se ejecuta automáticamente en todas las instancias actuales y en todas las instancias creadas después ajustando la escala.</span><span class="sxs-lookup"><span data-stu-id="61a7c-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="61a7c-149">Paso 7: Configuración de reglas de escalado automático</span><span class="sxs-lookup"><span data-stu-id="61a7c-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="61a7c-150">Actualmente, no se pueden establecer reglas de escalado automático en la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="61a7c-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="61a7c-151">Hola de uso [portal de Azure](https://portal.azure.com) tooconfigure Autoescala.</span><span class="sxs-lookup"><span data-stu-id="61a7c-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="61a7c-152">Paso 8: Tareas de administración</span><span class="sxs-lookup"><span data-stu-id="61a7c-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="61a7c-153">A lo largo del ciclo de vida de Hola de conjunto de escalas de hello, puede que necesite toorun una o más tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="61a7c-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="61a7c-154">Además, puede que desee toocreate scripts que automaticen diversas tareas de ciclo de vida y Hola CLI de Azure proporciona una manera rápida toodo esas tareas.</span><span class="sxs-lookup"><span data-stu-id="61a7c-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="61a7c-155">A continuación, presentamos algunas tareas comunes.</span><span class="sxs-lookup"><span data-stu-id="61a7c-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="61a7c-156">Obtención de información de conexión</span><span class="sxs-lookup"><span data-stu-id="61a7c-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="61a7c-157">Establecimiento del número de instancias (escalado manual)</span><span class="sxs-lookup"><span data-stu-id="61a7c-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="61a7c-158">Eliminación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="61a7c-158">Delete resource group</span></span>

<span data-ttu-id="61a7c-159">Al eliminar un grupo de recursos se eliminan también todos los recursos contenidos en el mismo.</span><span class="sxs-lookup"><span data-stu-id="61a7c-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="61a7c-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61a7c-160">Next steps</span></span>
<span data-ttu-id="61a7c-161">toolearn más información sobre algunas de las escalas de máquina virtual de hello establecer características presentadas en este tutorial, vea Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="61a7c-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="61a7c-162">Introducción a los conjuntos de escalado de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="61a7c-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="61a7c-163">Información general sobre Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="61a7c-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="61a7c-164">Control del flujo de tráfico de red con grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="61a7c-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)