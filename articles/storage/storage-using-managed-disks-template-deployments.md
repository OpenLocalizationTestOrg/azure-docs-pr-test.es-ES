---
title: discos de plantillas del Administrador de recursos de Azure administrados por aaaUsing | Documentos de Microsoft
description: "Detalla cómo toouse administra misks en plantillas del Administrador de recursos de Azure"
services: storage
documentationcenter: 
author: jboeshart
manager: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/01/2017
ms.author: jaboes
ms.openlocfilehash: ea83f4ed11acfd8f642dbc8331fa8cf077ef577c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="a8c78-103">Uso de discos administrados en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8c78-103">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="a8c78-104">Este documento le guía a través de las diferencias de hello entre los discos administrados y no administrados cuando se usa máquinas virtuales de Azure Resource Manager plantillas tooprovision.</span><span class="sxs-lookup"><span data-stu-id="a8c78-104">This document walks through hello differences between managed and unmanaged disks when using Azure Resource Manager templates tooprovision virtual machines.</span></span> <span data-ttu-id="a8c78-105">Esto le permitirá tooupdate plantillas existentes que usan discos de toomanaged de discos no administrados.</span><span class="sxs-lookup"><span data-stu-id="a8c78-105">This will help you tooupdate existing templates that are using unmanaged Disks toomanaged disks.</span></span> <span data-ttu-id="a8c78-106">Como referencia, estamos utilizando hello [101 vm simple windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) plantilla como guía.</span><span class="sxs-lookup"><span data-stu-id="a8c78-106">For reference, we are using hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="a8c78-107">Puede ver la plantilla Hola utilizan ambos [discos administrados por](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) y una versión anterior usando [sin administrar discos](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) si lo desea toodirectly compararlos.</span><span class="sxs-lookup"><span data-stu-id="a8c78-107">You can see hello template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like toodirectly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="a8c78-108">Formato de plantilla de discos no administrados</span><span class="sxs-lookup"><span data-stu-id="a8c78-108">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="a8c78-109">toobegin, echaremos un vistazo en discos sin administrar cómo se implementan.</span><span class="sxs-lookup"><span data-stu-id="a8c78-109">toobegin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="a8c78-110">Al crear discos no administrados, tiene un archivos de disco duro virtual de almacenamiento cuenta toohold Hola.</span><span class="sxs-lookup"><span data-stu-id="a8c78-110">When creating unmanaged disks, you need a storage account toohold hello VHD files.</span></span> <span data-ttu-id="a8c78-111">Puede crear una cuenta de almacenamiento o usar una ya existente.</span><span class="sxs-lookup"><span data-stu-id="a8c78-111">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="a8c78-112">En este artículo le mostrará cómo toocreate una nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a8c78-112">This article will show you how toocreate a new storage account.</span></span> <span data-ttu-id="a8c78-113">tooaccomplish, necesita un recurso de la cuenta de almacenamiento en bloque de recursos de hello tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="a8c78-113">tooaccomplish this, you need a storage account resource in hello resources block as shown below.</span></span>

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="a8c78-114">En el objeto de máquina virtual de hello, necesitamos una dependencia en tooensure de cuenta de almacenamiento de Hola que ha creado antes de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8c78-114">Within hello virtual machine object, we need a dependency on hello storage account tooensure that it's created before hello virtual machine.</span></span> <span data-ttu-id="a8c78-115">Dentro de hello `storageProfile` sección, a continuación, especificamos Hola URI completo de hello ubicación del disco duro virtual, que hace referencia la cuenta de almacenamiento de Hola y es necesario para el disco de SO de Hola y los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="a8c78-115">Within hello `storageProfile` section, we then specify hello full URI of hello VHD location, which references hello storage account and is needed for hello OS disk and any data disks.</span></span> 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="a8c78-116">Formato de plantilla de discos administrados</span><span class="sxs-lookup"><span data-stu-id="a8c78-116">Managed disks template formatting</span></span>

<span data-ttu-id="a8c78-117">Con los discos de Azure administrados, disco Hola se convierte en un recurso de nivel superior y ya no requiere una toobe de cuenta de almacenamiento creado por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8c78-117">With Azure Managed Disks, hello disk becomes a top-level resource and no longer requires a storage account toobe created by hello user.</span></span> <span data-ttu-id="a8c78-118">Discos administrados están expuestos en primer lugar en hello `2016-04-30-preview` versión de API, están disponibles en todas las versiones posteriores de API y ahora son tipo de disco de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="a8c78-118">Managed disks were first exposed in hello `2016-04-30-preview` API version, they are available in all subsequent API versions and are now hello default disk type.</span></span> <span data-ttu-id="a8c78-119">Hello las secciones siguientes se guiarán a través de la configuración predeterminada de Hola y de detallan cómo toofurther personalizar los discos.</span><span class="sxs-lookup"><span data-stu-id="a8c78-119">hello following sections walk through hello default settings and detail how toofurther customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="a8c78-120">Se recomienda una API toouse versión posterior a `2016-04-30-preview` tal y como se produjeron cambios importantes entre `2016-04-30-preview` y `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="a8c78-120">It is recommended toouse an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="a8c78-121">Configuración predeterminada de discos administrados</span><span class="sxs-lookup"><span data-stu-id="a8c78-121">Default managed disk settings</span></span>

<span data-ttu-id="a8c78-122">toocreate una máquina virtual con discos administrados, que ya no necesita el recurso de cuenta de almacenamiento de toocreate hello y puede actualizar el recurso de máquina virtual como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="a8c78-122">toocreate a VM with managed disks, you no longer need toocreate hello storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="a8c78-123">Tenga en cuenta específicamente esa hello `apiVersion` refleja `2017-03-30` hello y `osDisk` y `dataDisks` ya no hacen referencia tooa URI específico para hello VHD.</span><span class="sxs-lookup"><span data-stu-id="a8c78-123">Specifically note that hello `apiVersion` reflects `2017-03-30` and hello `osDisk` and `dataDisks` no longer refer tooa specific URI for hello VHD.</span></span> <span data-ttu-id="a8c78-124">Al implementar sin especificar propiedades adicionales, usará el disco de hello [almacenamiento estándar LRS](storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="a8c78-124">When deploying without specifying additional properties, hello disk will use [Standard LRS storage](storage-redundancy.md).</span></span> <span data-ttu-id="a8c78-125">Si no se especifica ningún nombre, toma el formato hello `<VMName>_OsDisk_1_<randomstring>` para el disco de SO de Hola y `<VMName>_disk<#>_<randomstring>` para cada disco de datos.</span><span class="sxs-lookup"><span data-stu-id="a8c78-125">If no name is specified, it takes hello format of `<VMName>_OsDisk_1_<randomstring>` for hello OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="a8c78-126">De forma predeterminada, se deshabilita el cifrado de disco de Azure; almacenamiento en caché es lectura/escritura para el disco de SO de Hola y ninguno de los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="a8c78-126">By default, Azure disk encryption is disabled; caching is Read/Write for hello OS disk and None for data disks.</span></span> <span data-ttu-id="a8c78-127">Puede observar en el siguiente ejemplo de Hola que sigue habiendo una dependencia de cuenta de almacenamiento, aunque esto es solo para el almacenamiento de diagnósticos y no es necesario para el almacenamiento en disco.</span><span class="sxs-lookup"><span data-stu-id="a8c78-127">You may notice in hello example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="a8c78-128">Uso de un recurso de disco administrado de nivel superior</span><span class="sxs-lookup"><span data-stu-id="a8c78-128">Using a top-level managed disk resource</span></span>

<span data-ttu-id="a8c78-129">Como una configuración de disco de hello toospecifying alternativo en el objeto de máquina virtual de hello, puede crear un recurso de disco de nivel superior y adjuntar como parte de la creación de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8c78-129">As an alternative toospecifying hello disk configuration in hello virtual machine object, you can create a top-level disk resource and attach it as part of hello virtual machine creation.</span></span> <span data-ttu-id="a8c78-130">Por ejemplo, podemos crear un recurso de disco de manera toouse como un disco de datos.</span><span class="sxs-lookup"><span data-stu-id="a8c78-130">For example, we can create a disk resource as follows toouse as a data disk.</span></span>

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="a8c78-131">En el objeto de máquina virtual de hello, a continuación, podemos hacer referencia a este toobe de objeto de disco conectado.</span><span class="sxs-lookup"><span data-stu-id="a8c78-131">Within hello VM object, we can then reference this disk object toobe attached.</span></span> <span data-ttu-id="a8c78-132">Especificar el Id. de recurso de Hola de hello administrado disco que creamos en hello `managedDisk` datos adjuntos de hello del disco de hello como Hola se crea la máquina virtual que permite la propiedad.</span><span class="sxs-lookup"><span data-stu-id="a8c78-132">Specifying hello resource ID of hello managed disk we created in hello `managedDisk` property allows hello attachment of hello disk as hello VM is created.</span></span> <span data-ttu-id="a8c78-133">Tenga en cuenta que hello `apiVersion` de hello recurso de máquina virtual se establece demasiado`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="a8c78-133">Note that hello `apiVersion` for hello VM resource is set too`2017-03-30`.</span></span> <span data-ttu-id="a8c78-134">Tenga en cuenta también que hemos creado una dependencia en tooensure de recursos de disco Hola se crea correctamente antes de la creación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a8c78-134">Also note that we've created a dependency on hello disk resource tooensure it's successfully created before VM creation.</span></span> 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="a8c78-135">Creación de conjuntos de disponibilidad administrados con máquinas virtuales con discos administrados</span><span class="sxs-lookup"><span data-stu-id="a8c78-135">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="a8c78-136">toocreate administrado disponibilidad conjuntos con máquinas virtuales con discos administrados, agregar hello `sku` disponibilidad toohello de objeto establezca recursos y hello `name` propiedad demasiado`Aligned`.</span><span class="sxs-lookup"><span data-stu-id="a8c78-136">toocreate managed availability sets with VMs using managed disks, add hello `sku` object toohello availability set resource and set hello `name` property too`Aligned`.</span></span> <span data-ttu-id="a8c78-137">Esto garantiza que los discos de Hola para cada máquina virtual estén suficientemente aislados entre sí tooavoid puntos únicos de error.</span><span class="sxs-lookup"><span data-stu-id="a8c78-137">This ensures that hello disks for each VM are sufficiently isolated from each other tooavoid single points of failure.</span></span> <span data-ttu-id="a8c78-138">Tenga en cuenta también que hello `apiVersion` para recurso de conjunto de disponibilidad de Hola se establece demasiado`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="a8c78-138">Also note that hello `apiVersion` for hello availability set resource is set too`2017-03-30`.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="a8c78-139">Personalizaciones y escenarios adicionales</span><span class="sxs-lookup"><span data-stu-id="a8c78-139">Additional scenarios and customizations</span></span>

<span data-ttu-id="a8c78-140">toofind toda la información de especificaciones de la API de REST de hello, revise hello [crear un disco administrado documentación de la API de REST](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="a8c78-140">toofind full information on hello REST API specifications, please review hello [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="a8c78-141">Encontrará escenarios adicionales, así como valor predeterminado y los valores aceptables que pueden ser API toohello enviados a través de las implementaciones de plantilla.</span><span class="sxs-lookup"><span data-stu-id="a8c78-141">You will find additional scenarios, as well as default and acceptable values that can be submitted toohello API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a8c78-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8c78-142">Next steps</span></span>

* <span data-ttu-id="a8c78-143">Para plantillas completas que usan discos administrados visitan Hola siguientes vínculos de repositorio de inicio rápido de Azure.</span><span class="sxs-lookup"><span data-stu-id="a8c78-143">For full templates that use managed disks visit hello following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="a8c78-144">Máquina virtual Windows con disco administrado</span><span class="sxs-lookup"><span data-stu-id="a8c78-144">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="a8c78-145">Máquina virtual Linux con disco administrado</span><span class="sxs-lookup"><span data-stu-id="a8c78-145">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="a8c78-146">Lista completa de plantillas de discos administrados</span><span class="sxs-lookup"><span data-stu-id="a8c78-146">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="a8c78-147">Visite hello [información general de Azure administra discos](storage-managed-disks-overview.md) documento toolearn Obtenga más información sobre discos administrados.</span><span class="sxs-lookup"><span data-stu-id="a8c78-147">Visit hello [Azure Managed Disks Overview](storage-managed-disks-overview.md) document toolearn more about managed disks.</span></span>
* <span data-ttu-id="a8c78-148">Consultar la documentación de referencia de plantilla de Hola para recursos de máquina virtual visitando hello [referencia de plantillas de Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) documento.</span><span class="sxs-lookup"><span data-stu-id="a8c78-148">Review hello template reference documentation for virtual machine resources by visiting hello [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="a8c78-149">Consultar la documentación de referencia de plantilla de Hola para recursos de disco visitando hello [referencia de plantillas de Microsoft.Compute/disks](/templates/microsoft.compute/disks) documento.</span><span class="sxs-lookup"><span data-stu-id="a8c78-149">Review hello template reference documentation for disk resources by visiting hello [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
