---
title: "Discos de datos conectados de máquina Virtual escala conjuntos aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse adjuntar discos de datos con conjuntos de escalas de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="60a41-103">Conjuntos de escalado de máquinas virtuales de Azure y discos de datos conectados</span><span class="sxs-lookup"><span data-stu-id="60a41-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="60a41-104">Los [conjuntos de escalado de máquinas virtuales](/azure/virtual-machine-scale-sets/) de Azure ahora son compatibles con máquinas virtuales con discos de datos conectados.</span><span class="sxs-lookup"><span data-stu-id="60a41-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="60a41-105">Discos de datos se pueden definir en el perfil de almacenamiento de Hola para conjuntos de escala que se han creado con discos de Azure administrados.</span><span class="sxs-lookup"><span data-stu-id="60a41-105">Data disks can be defined in hello storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="60a41-106">Anteriormente hello únicas opciones de almacenamiento directamente conectado disponibles con las máquinas virtuales en conjuntos de escalas eran unidad Hola sistema operativo y unidades temporales.</span><span class="sxs-lookup"><span data-stu-id="60a41-106">Previously hello only directly attached storage options available with VMs in scale sets were hello OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="60a41-107">Cuando se crea una escala establecida con discos de datos adjuntos definidos, todavía necesita toomount y Hola formato discos desde dentro de una máquina virtual toouse ellos (al igual que para máquinas virtuales de Azure independiente).</span><span class="sxs-lookup"><span data-stu-id="60a41-107">When you create a scale set with attached data disks defined, you still need toomount and format hello disks from within a VM toouse them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="60a41-108">Una manera cómoda de toodo es toouse una extensión de script personalizado que llama a una secuencia de comandos estándar toopartition y dar formato a todos los discos de datos de hello en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60a41-108">A convenient way toodo this is toouse a custom script extension which calls a standard script toopartition and format all hello data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="60a41-109">Creación de un conjunto de escalado con discos de datos conectados</span><span class="sxs-lookup"><span data-stu-id="60a41-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="60a41-110">Un toocreate de forma sencilla una escala configurada con discos conectados es hello de toouse [CLI de Azure](https://github.com/Azure/azure-cli) _vmss crear_ comando.</span><span class="sxs-lookup"><span data-stu-id="60a41-110">A simple way toocreate a scale set with attached disks is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="60a41-111">Hola de ejemplo siguiente crea un grupo de recursos de Azure y un conjunto de escala de la máquina virtual de 10 Ubuntu máquinas virtuales, cada uno con discos de datos adjuntos 2, de 50 GB y 100 GB, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="60a41-111">hello following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="60a41-112">Tenga en cuenta que hello _vmss crear_ ciertos valores de configuración si no los especifica valores predeterminados de comando.</span><span class="sxs-lookup"><span data-stu-id="60a41-112">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="60a41-113">toosee Hola opciones disponibles que puede invalidar try:</span><span class="sxs-lookup"><span data-stu-id="60a41-113">toosee hello available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="60a41-114">Incluir otro toocreate de manera que una escala establecida con discos de datos adjuntos es toodefine una escala establecida en una plantilla de Azure Resource Manager, un _dataDisks_ sección Hola _storageProfile_e implementar Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="60a41-114">Another way toocreate a scale set with attached data disks is toodefine a scale set in an Azure Resource Manager template, include a _dataDisks_ section in hello _storageProfile_, and deploy hello template.</span></span> <span data-ttu-id="60a41-115">Hola 50 y 100 GB disco ejemplo anterior se definiría como esta plantilla hello:</span><span class="sxs-lookup"><span data-stu-id="60a41-115">hello 50 GB and 100 GB disk example above would be defined like this in hello template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="60a41-116">Puede ver un ejemplo completo, listo toodeploy de una plantilla de conjunto de escala con un disco conectado definido aquí: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="60a41-116">You can see a complete, ready toodeploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a><span data-ttu-id="60a41-117">Agregar una escala existente de datos disco tooan conjunto</span><span class="sxs-lookup"><span data-stu-id="60a41-117">Adding a data disk tooan existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="60a41-118">Sólo se puede asociar el conjunto de escala de tooa de discos de datos que se ha creado con [discos de Azure administrados](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="60a41-118">You can only attach data disks tooa scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="60a41-119">Puede agregar una escala de VM tooa de disco de datos establecida mediante Azure CLI _adjuntar disco de az vmss_ comando.</span><span class="sxs-lookup"><span data-stu-id="60a41-119">You can add a data disk tooa VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="60a41-120">Asegúrese de que especifica un valor de lun que ya no esté en uso.</span><span class="sxs-lookup"><span data-stu-id="60a41-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="60a41-121">Hola CLI ejemplo siguiente agrega un toolun de unidad de 50 GB 3:</span><span class="sxs-lookup"><span data-stu-id="60a41-121">hello following CLI example adds a 50 GB drive toolun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="60a41-122">Hola PowerShell ejemplo siguiente agrega un toolun de unidad de 50 GB 3:</span><span class="sxs-lookup"><span data-stu-id="60a41-122">hello following PowerShell example adds a 50 GB drive toolun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="60a41-123">Diferentes tamaños de máquinas virtuales tienen distintos límites en números de Hola de unidades adjuntas que admiten.</span><span class="sxs-lookup"><span data-stu-id="60a41-123">Different VM sizes have different limits on hello numbers of attached drives they support.</span></span> <span data-ttu-id="60a41-124">Comprobar hello [características de tamaño de máquina virtual](../virtual-machines/windows/sizes.md) antes de agregar un nuevo disco.</span><span class="sxs-lookup"><span data-stu-id="60a41-124">Check hello [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="60a41-125">También puede agregar un disco mediante la adición de un nuevo toohello entrada _dataDisks_ propiedad Hola _storageProfile_ de una escala establece definición y aplicar cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="60a41-125">You can also add a disk by adding a new entry toohello _dataDisks_ property in hello _storageProfile_ of a scale set definition and applying hello change.</span></span> <span data-ttu-id="60a41-126">tootest, buscar una definición de conjunto de escala existente en hello [Explorador de recursos de Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="60a41-126">tootest this, find an existing scale set definition in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="60a41-127">Seleccione _modificar_ y agregar una nueva lista de toohello de disco de los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="60a41-127">Select _Edit_ and add a new disk toohello list of data disks.</span></span> <span data-ttu-id="60a41-128">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="60a41-128">E.g.</span></span> <span data-ttu-id="60a41-129">uso de ejemplo de Hola anterior:</span><span class="sxs-lookup"><span data-stu-id="60a41-129">using hello example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="60a41-130">A continuación, seleccione _colocar_ tooapply Hola cambia el conjunto de escalas de tooyour.</span><span class="sxs-lookup"><span data-stu-id="60a41-130">Then select _PUT_ tooapply hello changes tooyour scale set.</span></span> <span data-ttu-id="60a41-131">Este ejemplo podría funcionar siempre y cuando se utilice un tamaño de máquina virtual que admite más de dos discos de datos conectados.</span><span class="sxs-lookup"><span data-stu-id="60a41-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="60a41-132">Cuando realice definición como agregar o quitar un disco de datos del conjunto de una escala de tooa de cambio, se aplica a las máquinas virtuales de tooall recién creado, pero solo se aplica tooexisting las máquinas virtuales si hello _upgradePolicy_ propiedad se establece demasiado "automática".</span><span class="sxs-lookup"><span data-stu-id="60a41-132">When you make a change tooa scale set definition such as adding or removing a data disk, it applies tooall newly created VMs, but only applies tooexisting VMs if hello _upgradePolicy_ property is set too"Automatic".</span></span> <span data-ttu-id="60a41-133">Si se establece demasiado "Manual", debe toomanually aplicar Hola nuevo modelo tooexisting máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="60a41-133">If it is set too"Manual", you need toomanually apply hello new model tooexisting VMs.</span></span> <span data-ttu-id="60a41-134">Para hacer esto en el portal de hello, con hello _actualización AzureRmVmssInstance_ PowerShell comando, o mediante hello _az vmss update-instancias_ comando de CLI.</span><span class="sxs-lookup"><span data-stu-id="60a41-134">You can do this in hello portal, using hello _Update-AzureRmVmssInstance_ PowerShell command, or using hello _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a><span data-ttu-id="60a41-135">Agregar conjunto de escalas existente de tooan de discos de datos rellenada previamente</span><span class="sxs-lookup"><span data-stu-id="60a41-135">Adding pre-populated data disks tooan existent scale set</span></span> 
> <span data-ttu-id="60a41-136">Al agregar discos tooan existente conjunto de escalado de modelo, por diseño, disco de hello siempre se pueden crear vacío.</span><span class="sxs-lookup"><span data-stu-id="60a41-136">When you add disks tooan existent scale set model, by design, hello disk will always be created empty.</span></span> <span data-ttu-id="60a41-137">Este escenario también incluye nuevas instancias creadas por conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="60a41-137">This scenario also includes new instances created by hello scale set.</span></span> <span data-ttu-id="60a41-138">Este comportamiento es porque la definición de scaleset hello tiene un disco de datos vacía.</span><span class="sxs-lookup"><span data-stu-id="60a41-138">This behaviour is because hello scaleset definition has an empty data disk.</span></span> <span data-ttu-id="60a41-139">En orden toocreate unidades de datos rellenada previamente para un modelo de conjunto de escala existente, puede elegir cualquiera de las dos opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="60a41-139">In order toocreate pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="60a41-140">Copiar datos de discos de datos de hello instancia 0 VM toohello Hola otras máquinas virtuales mediante la ejecución de un script personalizado.</span><span class="sxs-lookup"><span data-stu-id="60a41-140">Copy data from hello instance 0 VM toohello data disk(s) in hello other VMs by running a custom script.</span></span>
* <span data-ttu-id="60a41-141">Crea una imagen administrada con disco Hola SO más disco de datos (con datos de hello necesaria) y cree un nuevo scaleset con imagen Hola.</span><span class="sxs-lookup"><span data-stu-id="60a41-141">Create a managed image with hello OS disk plus data disk (with hello required data) and create a new scaleset with hello image.</span></span> <span data-ttu-id="60a41-142">Esta manera cada nueva máquina virtual creado tendrá un datos en disco que se proporciona en la definición de Hola de hello scaleset.</span><span class="sxs-lookup"><span data-stu-id="60a41-142">This way every new VM created will have a data disk that that is provided in hello definition of hello scaleset.</span></span> <span data-ttu-id="60a41-143">Puesto que esta definición hará referencia tooan imagen con un disco de datos que ha personalizado datos, cada máquina virtual en hello scaleset automáticamente aparecerá con estos cambios.</span><span class="sxs-lookup"><span data-stu-id="60a41-143">Since this definition will refer tooan image with a data disk that has customized data, every virtual machine on hello scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="60a41-144">Hola toocreate de manera que una imagen personalizada se puede encontrar aquí: [crear una imagen administrada de una VM generalizada en Azure](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="60a41-144">hello way toocreate a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="60a41-145">Hello usuario necesita toocapture Hola instancia 0 de máquina virtual que ha Hola datos necesarios y, a continuación, usar ese archivo vhd para la definición de la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="60a41-145">hello user needs toocapture hello instance 0 VM which has hello required data, and then use that vhd for hello image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="60a41-146">Supresión de un disco de datos de un conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="60a41-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="60a41-147">Puede quitar un disco de datos de un conjunto de escalado de la máquina virtual mediante el comando _az vmss disk detach_ de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="60a41-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="60a41-148">Por ejemplo hello comando siguiente quita Hola disco definido en el lun 2:</span><span class="sxs-lookup"><span data-stu-id="60a41-148">For example hello following command removes hello disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="60a41-149">De igual forma también puede quitar un disco de una escala establecida mediante la eliminación de una entrada de hello _dataDisks_ propiedad Hola _storageProfile_ y aplicar cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="60a41-149">Similarly you can also remove a disk from a scale set by removing an entry from hello _dataDisks_ property in hello _storageProfile_ and applying hello change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="60a41-150">Notas adicionales</span><span class="sxs-lookup"><span data-stu-id="60a41-150">Additional notes</span></span>
<span data-ttu-id="60a41-151">Soporte para discos de datos adjuntos del conjunto de discos administrados de Azure y la escala está disponible en la versión de API [ _2016-04-30-versión preliminar_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) o una versión posterior de hello Microsoft.Compute API.</span><span class="sxs-lookup"><span data-stu-id="60a41-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of hello Microsoft.Compute API.</span></span>

<span data-ttu-id="60a41-152">En implementación inicial de Hola de soporte técnico de disco conectado para conjuntos de escalas, no se puede conectar o desconectar discos de datos de máquinas virtuales individuales en un conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="60a41-152">In hello initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="60a41-153">La compatibilidad con Azure Portal para discos de datos conectados en los conjuntos de escalado está limitada inicialmente.</span><span class="sxs-lookup"><span data-stu-id="60a41-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="60a41-154">Dependiendo de los requisitos que se puede usar plantillas de Azure, toomanage CLI, PowerShell, SDK y API de REST de los discos conectados.</span><span class="sxs-lookup"><span data-stu-id="60a41-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API toomanage attached disks.</span></span>


