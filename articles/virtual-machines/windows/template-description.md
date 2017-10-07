---
title: "máquinas de aaaVirtual en una plantilla de Azure Resource Manager | Microsoft Azure"
description: "Más información sobre cómo se definen los recursos de máquina virtual de hello en una plantilla de Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="22072-103">Máquinas virtuales de una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22072-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="22072-104">Este artículo describe aspectos de una plantilla de Azure Resource Manager que se aplican toovirtual máquinas.</span><span class="sxs-lookup"><span data-stu-id="22072-104">This article describes aspects of an Azure Resource Manager template that apply toovirtual machines.</span></span> <span data-ttu-id="22072-105">En este artículo no se describe una plantilla completa para crear una máquina virtual. Para ello, necesita definiciones de recursos de cuentas de almacenamiento, interfaces de red, direcciones IP públicas y redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="22072-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="22072-106">Para obtener más información acerca de cómo se pueden definir estos recursos juntos, vea hello [tutorial de la plantilla de administrador de recursos](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="22072-106">For more information about how these resources can be defined together, see hello [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="22072-107">Hay muchos [plantillas en la Galería de hello](https://azure.microsoft.com/documentation/templates/?term=VM) que incluyen recursos de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-107">There are many [templates in hello gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include hello VM resource.</span></span> <span data-ttu-id="22072-108">No todos los elementos que pueden incorporarse en una plantilla se describen aquí.</span><span class="sxs-lookup"><span data-stu-id="22072-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="22072-109">En este ejemplo se muestra una sección de recursos típica de una plantilla para crear un número especificado de máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="22072-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
><span data-ttu-id="22072-110">Se basa en una cuenta de almacenamiento que se ha creado previamente.</span><span class="sxs-lookup"><span data-stu-id="22072-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="22072-111">Puede crear cuenta de almacenamiento de hello mediante la implementación de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-111">You could create hello storage account by deploying it from hello template.</span></span> <span data-ttu-id="22072-112">ejemplo de Hola también se basa en una interfaz de red y sus recursos dependientes que se pueden definir en plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-112">hello example also relies on a network interface and its dependent resources that would be defined in hello template.</span></span> <span data-ttu-id="22072-113">Estos recursos no se muestran en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-113">These resources are not shown in hello example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="22072-114">Versión de API</span><span class="sxs-lookup"><span data-stu-id="22072-114">API Version</span></span>

<span data-ttu-id="22072-115">Cuando se implementación mediante una plantilla de recursos, tienes toospecify una versión de Hola API toouse.</span><span class="sxs-lookup"><span data-stu-id="22072-115">When you deploy resources using a template, you have toospecify a version of hello API toouse.</span></span> <span data-ttu-id="22072-116">Hola ilustra los recursos de máquina virtual de hello usando este elemento de valor apiVersion:</span><span class="sxs-lookup"><span data-stu-id="22072-116">hello example shows hello virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="22072-117">versión de Hola de hello API que se especifique en la plantilla afecta a qué propiedades se pueden definir en plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-117">hello version of hello API you specify in your template affects which properties you can define in hello template.</span></span> <span data-ttu-id="22072-118">En general, debe seleccionar la versión más reciente de la API de hello al crear plantillas.</span><span class="sxs-lookup"><span data-stu-id="22072-118">In general, you should select hello most recent API version when creating templates.</span></span> <span data-ttu-id="22072-119">Para las plantillas existentes, puede decidir si desea toocontinue utilizando una versión anterior de la API o actualizar la plantilla para hello última versión tootake las nuevas características.</span><span class="sxs-lookup"><span data-stu-id="22072-119">For existing templates, you can decide whether you want toocontinue using an earlier API version, or update your template for hello latest version tootake advantage of new features.</span></span>

<span data-ttu-id="22072-120">Use estas oportunidades para obtener versiones más recientes de API de hello:</span><span class="sxs-lookup"><span data-stu-id="22072-120">Use these opportunities for getting hello latest API versions:</span></span>

- <span data-ttu-id="22072-121">API de REST: [Mostrar todos los proveedores de recursos](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="22072-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="22072-122">PowerShell: [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="22072-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="22072-123">CLI de Azure 2.0: [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="22072-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="22072-124">Parámetros y variables</span><span class="sxs-lookup"><span data-stu-id="22072-124">Parameters and variables</span></span>

<span data-ttu-id="22072-125">[Parámetros](../../resource-group-authoring-templates.md) facilitan la tarea por usted toospecify valores para la plantilla de hello cuando se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="22072-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you toospecify values for hello template when you run it.</span></span> <span data-ttu-id="22072-126">En esta sección de parámetros se utiliza en el ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="22072-126">This parameters section is used in hello example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="22072-127">Al implementar la plantilla de ejemplo de Hola, especificar los valores para nombre de Hola y la contraseña de cuenta de administrador de hello en cada máquina virtual y Hola el número de máquinas virtuales toocreate.</span><span class="sxs-lookup"><span data-stu-id="22072-127">When you deploy hello example template, you enter values for hello name and password of hello administrator account on each VM and hello number of VMs toocreate.</span></span> <span data-ttu-id="22072-128">Tiene la opción de Hola de especificar valores de parámetro en un archivo independiente que se administra con la plantilla de Hola o proporcionar valores cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="22072-128">You have hello option of specifying parameter values in a separate file that's managed with hello template, or providing values when prompted.</span></span>

<span data-ttu-id="22072-129">[Las variables](../../resource-group-authoring-templates.md) facilitan automáticamente tooset valores en plantilla de Hola que se usan varias veces a lo largo de él o que cambian con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="22072-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you tooset up values in hello template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="22072-130">En esta sección de variables se utiliza en el ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="22072-130">This variables section is used in hello example:</span></span>

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

<span data-ttu-id="22072-131">Al implementar la plantilla de ejemplo de Hola, valores de las variables se utilizan para nombre de Hola y el identificador de cuenta de almacenamiento de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="22072-131">When you deploy hello example template, variable values are used for hello name and identifier of hello previously created storage account.</span></span> <span data-ttu-id="22072-132">Las variables también son opciones de Hola de tooprovide usado para la extensión de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-132">Variables are also used tooprovide hello settings for hello diagnostic extension.</span></span> <span data-ttu-id="22072-133">Hola de uso [las prácticas recomendadas para la creación de plantillas de Azure Resource Manager](../../resource-manager-template-best-practices.md) toohelp decida cómo desea toostructure Hola parámetros y variables en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="22072-133">Use hello [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) toohelp you decide how you want toostructure hello parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="22072-134">bucles de recursos</span><span class="sxs-lookup"><span data-stu-id="22072-134">Resource loops</span></span>

<span data-ttu-id="22072-135">Si necesita más de una máquina virtual para la aplicación, puede utilizar un elemento de copia en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="22072-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="22072-136">Este elemento opcional recorre creando Hola número de máquinas virtuales que especifica como un parámetro:</span><span class="sxs-lookup"><span data-stu-id="22072-136">This optional element loops through creating hello number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="22072-137">Además, se utiliza en ejemplo Hola Hola índice de bucle al especificar algunos Hola valores para el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-137">Also, notice in hello example that hello loop index is used when specifying some of hello values for hello resource.</span></span> <span data-ttu-id="22072-138">Por ejemplo, si ha especificado un recuento de instancias de estos tres, nombres de Hola de discos del sistema operativo Hola son myOSDisk1, myOSDisk2 y myOSDisk3:</span><span class="sxs-lookup"><span data-stu-id="22072-138">For example, if you entered an instance count of three, hello names of hello operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="22072-139">Este ejemplo utiliza discos administrados para las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-139">This example uses managed disks for hello virtual machines.</span></span>
>
>

<span data-ttu-id="22072-140">Tenga en cuenta que la creación de un bucle para un recurso de plantilla de hello puede requerir toouse Hola bucle al crear o tener acceso a otros recursos.</span><span class="sxs-lookup"><span data-stu-id="22072-140">Keep in mind that creating a loop for one resource in hello template may require you toouse hello loop when creating or accessing other resources.</span></span> <span data-ttu-id="22072-141">Por ejemplo, varias máquinas virtuales no pueden usar hello misma interfaz de red, por lo que si recorre en bucle la plantilla de creación de tres máquinas virtuales también debe ejecutar un bucle en crear tres interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="22072-141">For example, multiple VMs can’t use hello same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="22072-142">Al asignar un tooa de interfaz de red virtual, índice de bucle de hello es tooidentify usado:</span><span class="sxs-lookup"><span data-stu-id="22072-142">When assigning a network interface tooa VM, hello loop index is used tooidentify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="22072-143">Dependencias</span><span class="sxs-lookup"><span data-stu-id="22072-143">Dependencies</span></span>

<span data-ttu-id="22072-144">Mayoría de los recursos depende otro toowork recursos correctamente.</span><span class="sxs-lookup"><span data-stu-id="22072-144">Most resources depend on other resources toowork correctly.</span></span> <span data-ttu-id="22072-145">Máquinas virtuales deben asociarse con una red virtual y toodo que requiere una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="22072-145">Virtual machines must be associated with a virtual network and toodo that it needs a network interface.</span></span> <span data-ttu-id="22072-146">Hola [dependsOn](../../resource-group-define-dependencies.md) elemento es toomake usado que esa interfaz de red de hello esté listo toobe usa antes de que se crean máquinas virtuales de hello:</span><span class="sxs-lookup"><span data-stu-id="22072-146">hello [dependsOn](../../resource-group-define-dependencies.md) element is used toomake sure that hello network interface is ready toobe used before hello VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="22072-147">Resource Manager implementa en paralelo todos los recursos que no dependan de otro que se vaya a implementar.</span><span class="sxs-lookup"><span data-stu-id="22072-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="22072-148">Tenga cuidado al establecer las dependencias porque puede ralentizar accidentalmente el proceso si define algunas que sean innecesarias.</span><span class="sxs-lookup"><span data-stu-id="22072-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="22072-149">Pueden encadenar las dependencias a través de varios recursos.</span><span class="sxs-lookup"><span data-stu-id="22072-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="22072-150">Por ejemplo, interfaz de red de hello depende de la dirección IP pública hello y recursos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="22072-150">For example, hello network interface depends on hello public IP address and virtual network resources.</span></span>

<span data-ttu-id="22072-151">¿Cómo puede saber si se requiere una dependencia?</span><span class="sxs-lookup"><span data-stu-id="22072-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="22072-152">Ver valores de hello establecido en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-152">Look at hello values you set in hello template.</span></span> <span data-ttu-id="22072-153">Si un elemento de la definición de recursos de máquina virtual de hello apunta tooanother recursos que está implementado en hello misma plantilla, necesita una dependencia.</span><span class="sxs-lookup"><span data-stu-id="22072-153">If an element in hello virtual machine resource definition points tooanother resource that is deployed in hello same template, you need a dependency.</span></span> <span data-ttu-id="22072-154">Por ejemplo, la máquina virtual de ejemplo define un perfil de red:</span><span class="sxs-lookup"><span data-stu-id="22072-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="22072-155">tooset esta propiedad, la interfaz de red de hello debe existir.</span><span class="sxs-lookup"><span data-stu-id="22072-155">tooset this property, hello network interface must exist.</span></span> <span data-ttu-id="22072-156">Por lo tanto, necesita una dependencia.</span><span class="sxs-lookup"><span data-stu-id="22072-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="22072-157">También debe tooset una dependencia cuando se define un recurso (un elemento secundario) dentro de otro recurso (un elemento primario).</span><span class="sxs-lookup"><span data-stu-id="22072-157">You also need tooset a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="22072-158">Por ejemplo, configuración de diagnóstico de Hola y extensiones de secuencias de comandos personalizadas se definen como recursos secundarios de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-158">For example, hello diagnostic settings and custom script extensions are both defined as child resources of hello virtual machine.</span></span> <span data-ttu-id="22072-159">No se creará hasta que la máquina virtual de hello existe.</span><span class="sxs-lookup"><span data-stu-id="22072-159">They cannot be created until hello virtual machine exists.</span></span> <span data-ttu-id="22072-160">Por lo tanto, los recursos se marcan como dependiente de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-160">Therefore, both resources are marked as dependent on hello virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="22072-161">Perfiles</span><span class="sxs-lookup"><span data-stu-id="22072-161">Profiles</span></span>

<span data-ttu-id="22072-162">Al definir un recurso de máquina virtual, se utilizan varios elementos de perfil.</span><span class="sxs-lookup"><span data-stu-id="22072-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="22072-163">Algunos son necesarios y otros, opcionales.</span><span class="sxs-lookup"><span data-stu-id="22072-163">Some are required and some are optional.</span></span> <span data-ttu-id="22072-164">Por ejemplo, elementos de hello hardwareProfile, osProfile, storageProfile y networkProfile son necesarios, pero hello diagnosticsProfile es opcional.</span><span class="sxs-lookup"><span data-stu-id="22072-164">For example, hello hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but hello diagnosticsProfile is optional.</span></span> <span data-ttu-id="22072-165">Estos perfiles definen opciones como:</span><span class="sxs-lookup"><span data-stu-id="22072-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="22072-166">Tamaño</span><span class="sxs-lookup"><span data-stu-id="22072-166">size</span></span>](sizes.md)
- <span data-ttu-id="22072-167">[Nombre](/architecture/best-practices/naming-conventions) y credenciales</span><span class="sxs-lookup"><span data-stu-id="22072-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="22072-168">[Configuración del sistema operativo](cli-ps-findimage.md) y disco</span><span class="sxs-lookup"><span data-stu-id="22072-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="22072-169">Interfaz de red</span><span class="sxs-lookup"><span data-stu-id="22072-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="22072-170">Diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="22072-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="22072-171">Discos e imágenes</span><span class="sxs-lookup"><span data-stu-id="22072-171">Disks and images</span></span>
   
<span data-ttu-id="22072-172">En Azure, los archivos de VHD pueden representar [discos o imágenes](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22072-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="22072-173">Cuando sistema de operativo hello en un archivo de disco duro virtual está especializada toobe una VM específica, es tooas que se hace referencia un disco.</span><span class="sxs-lookup"><span data-stu-id="22072-173">When hello operating system in a vhd file is specialized toobe a specific VM, it is referred tooas a disk.</span></span> <span data-ttu-id="22072-174">Al sistema operativo de hello en un archivo de disco duro virtual se ha generalizado toobe utiliza toocreate muchas máquinas virtuales, es una imagen de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="22072-174">When hello operating system in a vhd file is generalized toobe used toocreate many VMs, it is referred tooas an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="22072-175">Creación de máquinas virtuales y discos a partir de una imagen de plataforma</span><span class="sxs-lookup"><span data-stu-id="22072-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="22072-176">Cuando se crea una máquina virtual, debe decidir qué toouse de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="22072-176">When you create a VM, you must decide what operating system toouse.</span></span> <span data-ttu-id="22072-177">elemento de imageReference de Hello es sistema de operativo hello toodefine utilizadas de una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="22072-177">hello imageReference element is used toodefine hello operating system of a new VM.</span></span> <span data-ttu-id="22072-178">ejemplo de Hola muestra una definición para un sistema operativo Windows Server:</span><span class="sxs-lookup"><span data-stu-id="22072-178">hello example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="22072-179">Si desea toocreate un sistema operativo Linux, puede usar esta definición:</span><span class="sxs-lookup"><span data-stu-id="22072-179">If you want toocreate a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="22072-180">Opciones de configuración de disco del sistema operativo Hola se asignan por elemento de hello osDisk.</span><span class="sxs-lookup"><span data-stu-id="22072-180">Configuration settings for hello operating system disk are assigned with hello osDisk element.</span></span> <span data-ttu-id="22072-181">Hello en el ejemplo se define un nuevo disco administrado por hello demasiado el almacenamiento en caché el conjunto de modos**ReadWrite** y ese disco Hola se crea a partir un [imagen de la plataforma](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="22072-181">hello example defines a new managed disk with hello caching mode set too**ReadWrite** and that hello disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="22072-182">Creación de máquinas virtuales a partir de discos administrados existentes</span><span class="sxs-lookup"><span data-stu-id="22072-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="22072-183">Si desea que las máquinas virtuales de toocreate de discos existentes, quite imageReference hello y elementos de osProfile de Hola y definir esta configuración de disco:</span><span class="sxs-lookup"><span data-stu-id="22072-183">If you want toocreate virtual machines from existing disks, remove hello imageReference and hello osProfile elements and define these disk settings:</span></span>

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="22072-184">Creación de máquinas virtuales a partir de una imagen administrada</span><span class="sxs-lookup"><span data-stu-id="22072-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="22072-185">Si desea que una máquina virtual desde una imagen administrada toocreate, cambiar los elementos de imageReference hello y definir esta configuración de disco:</span><span class="sxs-lookup"><span data-stu-id="22072-185">If you want toocreate a virtual machine from a managed image, change hello imageReference element and define these disk settings:</span></span>

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a><span data-ttu-id="22072-186">Conexión de discos de datos</span><span class="sxs-lookup"><span data-stu-id="22072-186">Attach data disks</span></span>

<span data-ttu-id="22072-187">Si lo desea, puede agregar datos discos toohello máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="22072-187">You can optionally add data disks toohello VMs.</span></span> <span data-ttu-id="22072-188">Hola [número de discos](sizes.md) depende Hola tamaño del disco de sistema operativo que utilice.</span><span class="sxs-lookup"><span data-stu-id="22072-188">hello [number of disks](sizes.md) depends on hello size of operating system disk that you use.</span></span> <span data-ttu-id="22072-189">Con hello tamaño de máquinas virtuales de hello establece tooStandard_DS1_v2, número máximo de Hola de discos de datos que se podrían agregar toohello ellos es dos.</span><span class="sxs-lookup"><span data-stu-id="22072-189">With hello size of hello VMs set tooStandard_DS1_v2, hello maximum number of data disks that could be added toohello them is two.</span></span> <span data-ttu-id="22072-190">En el ejemplo de Hola, un disco de datos administrados se agrega tooeach VM:</span><span class="sxs-lookup"><span data-stu-id="22072-190">In hello example, one managed data disk is being added tooeach VM:</span></span>

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a><span data-ttu-id="22072-191">Extensiones</span><span class="sxs-lookup"><span data-stu-id="22072-191">Extensions</span></span>

<span data-ttu-id="22072-192">Aunque [extensiones](extensions-features.md) son un recurso independiente, sino tooVMs estrechamente relacionados.</span><span class="sxs-lookup"><span data-stu-id="22072-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied tooVMs.</span></span> <span data-ttu-id="22072-193">Las extensiones se pueden agregar como un recurso secundario de hello VM o como un recurso independiente.</span><span class="sxs-lookup"><span data-stu-id="22072-193">Extensions can be added as a child resource of hello VM or as a separate resource.</span></span> <span data-ttu-id="22072-194">ejemplo de Hola muestra hello [extensión de diagnósticos](extensions-diagnostics-template.md) añadidos toohello las máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="22072-194">hello example shows hello [Diagnostics Extension](extensions-diagnostics-template.md) being added toohello VMs:</span></span>

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

<span data-ttu-id="22072-195">Este recurso de extensión usa los valores de tooprovide de variables de diagnóstico de Hola y de variable de storageName Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-195">This extension resource uses hello storageName variable and hello diagnostic variables tooprovide values.</span></span> <span data-ttu-id="22072-196">Si desea toochange Hola datos recopilados por esta extensión, puede agregar más variables de wadperfcounters de toohello de contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="22072-196">If you want toochange hello data that is collected by this extension, you can add more performance counters toohello wadperfcounters variable.</span></span> <span data-ttu-id="22072-197">También puede elegir datos de diagnóstico de hello tooput en una cuenta de almacenamiento diferente a donde se almacenan los discos de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-197">You could also choose tooput hello diagnostics data into a different storage account than where hello VM disks are stored.</span></span>

<span data-ttu-id="22072-198">Existen muchas extensiones que se pueden instalar en una máquina virtual, pero hello más útil es probablemente hello [extensión de Script personalizado](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="22072-198">There are many extensions that you can install on a VM, but hello most useful is probably hello [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="22072-199">En el ejemplo de Hola, un script de PowerShell denominado start.ps1 se ejecuta en cada máquina virtual cuando inicia por primera vez:</span><span class="sxs-lookup"><span data-stu-id="22072-199">In hello example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

<span data-ttu-id="22072-200">secuencia de comandos de Hello start.ps1 puede realizar muchas tareas de configuración.</span><span class="sxs-lookup"><span data-stu-id="22072-200">hello start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="22072-201">Por ejemplo, no se inicializan los discos de datos de Hola que se agregan toohello máquinas virtuales en el ejemplo de Hola; Puede usar un script personalizado de tooinitialize ellos.</span><span class="sxs-lookup"><span data-stu-id="22072-201">For example, hello data disks that are added toohello VMs in hello example are not initialized; you can use a custom script tooinitialize them.</span></span> <span data-ttu-id="22072-202">Si tiene varios toodo de tareas de inicio, puede usar hello start.ps1 archivo toocall otras secuencias de comandos de PowerShell en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="22072-202">If you have multiple startup tasks toodo, you can use hello start.ps1 file toocall other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="22072-203">ejemplo de Hola usa PowerShell, pero puede usar cualquier método de scripting que está disponible en el sistema operativo de Hola que está usando.</span><span class="sxs-lookup"><span data-stu-id="22072-203">hello example uses PowerShell, but you can use any scripting method that is available on hello operating system that you are using.</span></span>

<span data-ttu-id="22072-204">Puede ver estado de Hola de extensiones de hello instalado desde la configuración de extensiones de hello en el portal de hello:</span><span class="sxs-lookup"><span data-stu-id="22072-204">You can see hello status of hello installed extensions from hello Extensions settings in hello portal:</span></span>

![Consulta del estado de la extensión](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="22072-206">También puede obtener información de la extensión mediante hello **Get AzureRmVMExtension** PowerShell comando hello **get de la extensión de vm** comando de CLI de Azure 2.0 o hello **obtener información de la extensión**  API de REST.</span><span class="sxs-lookup"><span data-stu-id="22072-206">You can also get extension information by using hello **Get-AzureRmVMExtension** PowerShell command, hello **vm extension get** Azure CLI 2.0 command, or hello **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="22072-207">Implementaciones</span><span class="sxs-lookup"><span data-stu-id="22072-207">Deployments</span></span>

<span data-ttu-id="22072-208">Cuando se implementa una plantilla, los recursos de hello Azure pistas que ha implementado como un grupo y automáticamente asigna a un grupo de toothis implementado de nombre.</span><span class="sxs-lookup"><span data-stu-id="22072-208">When you deploy a template, Azure tracks hello resources that you deployed as a group and automatically assigns a name toothis deployed group.</span></span> <span data-ttu-id="22072-209">nombre de Hola de implementación de hello es Hola mismo que el nombre de plantilla de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-209">hello name of hello deployment is hello same as hello name of hello template.</span></span>

<span data-ttu-id="22072-210">Si desea obtener sobre el estado de Hola de recursos de implementación de hello, puede usar hoja del grupo de recursos de Hola Hola portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="22072-210">If you are curious about hello status of resources in hello deployment, you can use hello Resource Group blade in hello Azure portal:</span></span>

![Obtención de la información de implementación](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="22072-212">No es un problema toouse Hola los mismos recursos de plantilla toocreate o tooupdate los recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="22072-212">It’s not a problem toouse hello same template toocreate resources or tooupdate existing resources.</span></span> <span data-ttu-id="22072-213">Al utilizar plantillas de toodeploy de comandos, tiene Hola oportunidad toosay que [modo](../../resource-group-template-deploy.md) desea toouse.</span><span class="sxs-lookup"><span data-stu-id="22072-213">When you use commands toodeploy templates, you have hello opportunity toosay which [mode](../../resource-group-template-deploy.md) you want toouse.</span></span> <span data-ttu-id="22072-214">se puede establecer el modo de Hello tooeither **completar** o **Incremental**.</span><span class="sxs-lookup"><span data-stu-id="22072-214">hello mode can be set tooeither **Complete** or **Incremental**.</span></span> <span data-ttu-id="22072-215">valor predeterminado de Hello es toodo las actualizaciones incrementales.</span><span class="sxs-lookup"><span data-stu-id="22072-215">hello default is toodo incremental updates.</span></span> <span data-ttu-id="22072-216">Tenga precaución al utilizar hello **completar** modo porque se pueden eliminar accidentalmente los recursos.</span><span class="sxs-lookup"><span data-stu-id="22072-216">Be careful when using hello **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="22072-217">Al establecer el modo de hello demasiado**completar**, Administrador de recursos elimina los recursos de grupo de recursos de Hola que no están en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="22072-217">When you set hello mode too**Complete**, Resource Manager deletes any resources in hello resource group that are not in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22072-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="22072-218">Next Steps</span></span>

- <span data-ttu-id="22072-219">Cree su propia plantilla con las [Creación de plantillas de Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="22072-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="22072-220">Implementar la plantilla de Hola que creó mediante [crear una máquina virtual de Windows con una plantilla de administrador de recursos](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="22072-220">Deploy hello template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="22072-221">Obtenga información acerca de cómo toomanage Hola las máquinas virtuales que se creó mediante la revisión de [crear y administrar máquinas virtuales de Windows con el módulo de PowerShell de Azure de hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22072-221">Learn how toomanage hello VMs that you created by reviewing [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
