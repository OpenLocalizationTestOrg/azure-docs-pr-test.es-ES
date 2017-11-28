# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="d27c4-101">Uso de discos administrados en plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d27c4-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="d27c4-102">En este documento se describen las diferencias entre discos administrados y discos no administrados cuando se usan plantillas de Azure Resource Manager para aprovisionar máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d27c4-102">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="d27c4-103">Esto le ayudará a actualizar las plantillas existentes que usan discos no administrados a discos administrados.</span><span class="sxs-lookup"><span data-stu-id="d27c4-103">This will help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="d27c4-104">Como referencia, usamos la plantilla [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) como guía.</span><span class="sxs-lookup"><span data-stu-id="d27c4-104">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="d27c4-105">Puede ver la plantilla usando tanto [discos administrados](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) como una versión usando [discos no administrados](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) si desea compararlas directamente.</span><span class="sxs-lookup"><span data-stu-id="d27c4-105">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="d27c4-106">Formato de plantilla de discos no administrados</span><span class="sxs-lookup"><span data-stu-id="d27c4-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="d27c4-107">Para comenzar, veremos cómo se implementan los discos no administrados.</span><span class="sxs-lookup"><span data-stu-id="d27c4-107">To begin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="d27c4-108">Cuando se crean discos no administrados, se necesita una cuenta de almacenamiento para contener los archivos VHD.</span><span class="sxs-lookup"><span data-stu-id="d27c4-108">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="d27c4-109">Puede crear una cuenta de almacenamiento o usar una ya existente.</span><span class="sxs-lookup"><span data-stu-id="d27c4-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="d27c4-110">En este artículo aprenderá a crear una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d27c4-110">This article will show you how to create a new storage account.</span></span> <span data-ttu-id="d27c4-111">Para ello, necesita un recurso de cuenta de almacenamiento en el bloque de recursos, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="d27c4-111">To accomplish this, you need a storage account resource in the resources block as shown below.</span></span>

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

<span data-ttu-id="d27c4-112">Dentro del objeto de máquina virtual, necesitamos una dependencia de la cuenta de almacenamiento para garantizar que se cree antes que la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d27c4-112">Within the virtual machine object, we need a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="d27c4-113">En la sección `storageProfile`, se especifica el URI completo de la ubicación de VHD, que hace referencia a la cuenta de almacenamiento y se necesita para el disco de OS y cualquier disco de datos.</span><span class="sxs-lookup"><span data-stu-id="d27c4-113">Within the `storageProfile` section, we then specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span> 

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

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="d27c4-114">Formato de plantilla de discos administrados</span><span class="sxs-lookup"><span data-stu-id="d27c4-114">Managed disks template formatting</span></span>

<span data-ttu-id="d27c4-115">Con Azure Managed Disks, el disco se convierte en un recurso de nivel superior y ya no es necesario que el usuario cree una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d27c4-115">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="d27c4-116">Los discos de Managed Disks se publicaron primero en la versión de API `2016-04-30-preview`; están disponibles en todas las versiones posteriores de API y, ahora, son el tipo de disco predeterminado.</span><span class="sxs-lookup"><span data-stu-id="d27c4-116">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="d27c4-117">En las secciones siguientes se describe la configuración predeterminada y se detalla cómo personalizar aún más los discos.</span><span class="sxs-lookup"><span data-stu-id="d27c4-117">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="d27c4-118">Se recomienda usar una versión de API posterior a `2016-04-30-preview`, ya que se produjeron cambios importantes entre `2016-04-30-preview` y `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="d27c4-118">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="d27c4-119">Configuración predeterminada de discos administrados</span><span class="sxs-lookup"><span data-stu-id="d27c4-119">Default managed disk settings</span></span>

<span data-ttu-id="d27c4-120">Para crear una máquina virtual con discos administrados, ya no es necesario crear el recurso de cuenta de almacenamiento y es posible actualizar el recurso de máquina virtual como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="d27c4-120">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="d27c4-121">Observe específicamente que `apiVersion` refleja `2017-03-30` y ni `osDisk` ni `dataDisks` hacen referencia ya a un URI específico para el VHD.</span><span class="sxs-lookup"><span data-stu-id="d27c4-121">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="d27c4-122">Cuando la implementación se realiza sin especificar propiedades adicionales, el disco usará el [almacenamiento LRS estándar](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="d27c4-122">When deploying without specifying additional properties, the disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="d27c4-123">Si no se especifica ningún nombre, toma el formato de `<VMName>_OsDisk_1_<randomstring>` para el disco de SO y `<VMName>_disk<#>_<randomstring>` para cada disco de datos.</span><span class="sxs-lookup"><span data-stu-id="d27c4-123">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="d27c4-124">De manera predeterminada, Azure Disk Encryption está deshabilitado; el almacenamiento en caché es Lectura/escritura en el caso del disco de SO y Ninguno para los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="d27c4-124">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="d27c4-125">En el ejemplo siguiente, puede observar que todavía existe una dependencia de cuenta de almacenamiento, pero es solo para el almacenamiento de diagnósticos y no es necesaria para almacenamiento en disco.</span><span class="sxs-lookup"><span data-stu-id="d27c4-125">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

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

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="d27c4-126">Uso de un recurso de disco administrado de nivel superior</span><span class="sxs-lookup"><span data-stu-id="d27c4-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="d27c4-127">Como alternativa para especificar la configuración de disco en el objeto de máquina virtual, puede crear un recurso de disco de nivel superior y adjuntarlo como parte de la creación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d27c4-127">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="d27c4-128">Por ejemplo, podemos crear un recurso de disco de la manera siguiente para usarlo como un disco de datos.</span><span class="sxs-lookup"><span data-stu-id="d27c4-128">For example, we can create a disk resource as follows to use as a data disk.</span></span>

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

<span data-ttu-id="d27c4-129">Dentro del objeto de máquina virtual, podemos hacer referencia a este objeto de disco para adjuntarlo.</span><span class="sxs-lookup"><span data-stu-id="d27c4-129">Within the VM object, we can then reference this disk object to be attached.</span></span> <span data-ttu-id="d27c4-130">Especificar el identificador de recurso del disco administrado que creamos en la propiedad `managedDisk` permite adjuntar el disco cuando se crea la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d27c4-130">Specifying the resource ID of the managed disk we created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="d27c4-131">Tenga en cuenta que el valor de la propiedad `apiVersion` del recurso de máquina virtual está establecido en `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="d27c4-131">Note that the `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="d27c4-132">Además, tenga en cuenta que creamos una dependencia del recurso de disco para garantizar que se cree correctamente antes de la creación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d27c4-132">Also note that we've created a dependency on the disk resource to ensure it's successfully created before VM creation.</span></span> 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="d27c4-133">Creación de conjuntos de disponibilidad administrados con máquinas virtuales con discos administrados</span><span class="sxs-lookup"><span data-stu-id="d27c4-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="d27c4-134">Para crear conjuntos de disponibilidad administrados con máquinas virtuales con discos administrados, agregue el objeto `sku` al recurso de conjunto de disponibilidad y establezca la propiedad `name` en `Aligned`.</span><span class="sxs-lookup"><span data-stu-id="d27c4-134">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="d27c4-135">Esto garantiza que los discos de cada máquina virtual estén suficientemente aislados entre sí para evitar puntos únicos de error.</span><span class="sxs-lookup"><span data-stu-id="d27c4-135">This ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="d27c4-136">Tenga en cuenta también que el valor de la propiedad `apiVersion` del recurso del conjunto de disponibilidad está establecido en `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="d27c4-136">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

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

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="d27c4-137">Personalizaciones y escenarios adicionales</span><span class="sxs-lookup"><span data-stu-id="d27c4-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="d27c4-138">Para información completa sobre las especificaciones de API de REST, revise la [documentación sobre cómo crear una API de REST de disco administrado](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="d27c4-138">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="d27c4-139">Encontrará escenarios adicionales, además de los valores predeterminados y aceptables que se pueden enviar a la API a través de implementaciones de plantilla.</span><span class="sxs-lookup"><span data-stu-id="d27c4-139">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d27c4-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d27c4-140">Next steps</span></span>

* <span data-ttu-id="d27c4-141">Para conocer las plantillas completas que usan discos administrados, viste los vínculos siguientes al repositorio de inicio rápido de Azure.</span><span class="sxs-lookup"><span data-stu-id="d27c4-141">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="d27c4-142">Máquina virtual Windows con disco administrado</span><span class="sxs-lookup"><span data-stu-id="d27c4-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="d27c4-143">Máquina virtual Linux con disco administrado</span><span class="sxs-lookup"><span data-stu-id="d27c4-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="d27c4-144">Lista completa de plantillas de discos administrados</span><span class="sxs-lookup"><span data-stu-id="d27c4-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="d27c4-145">Visite el documento [Introducción a Azure Managed Disks](../articles/virtual-machines/windows/managed-disks-overview.md) para más información sobre los discos administrados.</span><span class="sxs-lookup"><span data-stu-id="d27c4-145">Visit the [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="d27c4-146">Revise la documentación de referencia de plantilla de los recursos de máquina virtual en el documento de [referencia de plantilla Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines).</span><span class="sxs-lookup"><span data-stu-id="d27c4-146">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="d27c4-147">Revise la documentación de referencia de plantilla de los recursos de disco en el documento de [referencia de plantilla Microsoft.Compute/disks](/templates/microsoft.compute/disks).</span><span class="sxs-lookup"><span data-stu-id="d27c4-147">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
