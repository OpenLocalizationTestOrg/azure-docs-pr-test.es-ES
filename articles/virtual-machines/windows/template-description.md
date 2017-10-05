---
title: "Máquinas virtuales de una plantilla de Azure Resource Manager | Microsoft Azure"
description: "Obtenga más información sobre cómo se define el recurso de máquina virtual en una plantilla de Azure Resource Manager."
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
ms.openlocfilehash: d9b9121bc5e38396ba4def6c17f9b373c2b48056
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="35102-103">Máquinas virtuales de una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35102-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="35102-104">En este artículo se explican los aspectos de una plantilla de Azure Resource Manager que se aplican a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="35102-104">This article describes aspects of an Azure Resource Manager template that apply to virtual machines.</span></span> <span data-ttu-id="35102-105">En este artículo no se describe una plantilla completa para crear una máquina virtual. Para ello, necesita definiciones de recursos de cuentas de almacenamiento, interfaces de red, direcciones IP públicas y redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="35102-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="35102-106">Para obtener más información sobre cómo se pueden definir estos recursos juntos, consulte el [tutorial de plantilla de Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="35102-106">For more information about how these resources can be defined together, see the [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="35102-107">Hay muchas [plantillas en la galería](https://azure.microsoft.com/documentation/templates/?term=VM) que incluyen el recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="35102-107">There are many [templates in the gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include the VM resource.</span></span> <span data-ttu-id="35102-108">No todos los elementos que pueden incorporarse en una plantilla se describen aquí.</span><span class="sxs-lookup"><span data-stu-id="35102-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="35102-109">En este ejemplo se muestra una sección de recursos típica de una plantilla para crear un número especificado de máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="35102-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

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
><span data-ttu-id="35102-110">Se basa en una cuenta de almacenamiento que se ha creado previamente.</span><span class="sxs-lookup"><span data-stu-id="35102-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="35102-111">Puede crear la cuenta de almacenamiento implementando la plantilla.</span><span class="sxs-lookup"><span data-stu-id="35102-111">You could create the storage account by deploying it from the template.</span></span> <span data-ttu-id="35102-112">El ejemplo también se basa en una interfaz de red y sus recursos dependientes que se definirían en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="35102-112">The example also relies on a network interface and its dependent resources that would be defined in the template.</span></span> <span data-ttu-id="35102-113">Estos recursos no se muestran en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="35102-113">These resources are not shown in the example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="35102-114">Versión de API</span><span class="sxs-lookup"><span data-stu-id="35102-114">API Version</span></span>

<span data-ttu-id="35102-115">Cuando se implementan recursos mediante una plantilla, tendrá que especificar una versión de la API que se utilizará.</span><span class="sxs-lookup"><span data-stu-id="35102-115">When you deploy resources using a template, you have to specify a version of the API to use.</span></span> <span data-ttu-id="35102-116">En el ejemplo, se muestra el recurso de máquina virtual con este elemento apiVersion:</span><span class="sxs-lookup"><span data-stu-id="35102-116">The example shows the virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="35102-117">La versión de la API que especifica en la plantilla afecta a qué propiedades puede definir en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="35102-117">The version of the API you specify in your template affects which properties you can define in the template.</span></span> <span data-ttu-id="35102-118">En general, seleccionaría la versión de la API más reciente al crear nuevas plantillas.</span><span class="sxs-lookup"><span data-stu-id="35102-118">In general, you should select the most recent API version when creating templates.</span></span> <span data-ttu-id="35102-119">Para las plantillas existentes, puede decidir si quiere continuar usando una versión anterior de la API o actualizar la plantilla para que la versión más reciente aproveche las nuevas características.</span><span class="sxs-lookup"><span data-stu-id="35102-119">For existing templates, you can decide whether you want to continue using an earlier API version, or update your template for the latest version to take advantage of new features.</span></span>

<span data-ttu-id="35102-120">Aproveche estas oportunidades para obtener las últimas versiones de API:</span><span class="sxs-lookup"><span data-stu-id="35102-120">Use these opportunities for getting the latest API versions:</span></span>

- <span data-ttu-id="35102-121">API de REST: [Mostrar todos los proveedores de recursos](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="35102-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="35102-122">PowerShell: [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="35102-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="35102-123">CLI de Azure 2.0: [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="35102-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="35102-124">Parámetros y variables</span><span class="sxs-lookup"><span data-stu-id="35102-124">Parameters and variables</span></span>

<span data-ttu-id="35102-125">Los [parámetros](../../resource-group-authoring-templates.md) facilitan la tarea de especificar valores para la plantilla cuando la ejecuta.</span><span class="sxs-lookup"><span data-stu-id="35102-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you to specify values for the template when you run it.</span></span> <span data-ttu-id="35102-126">Esta sección de parámetros se utiliza en el ejemplo:</span><span class="sxs-lookup"><span data-stu-id="35102-126">This parameters section is used in the example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="35102-127">Al implementar la plantilla de ejemplo, escriba valores para el nombre y la contraseña de la cuenta de administrador de cada máquina virtual y el número de máquinas virtuales que creará.</span><span class="sxs-lookup"><span data-stu-id="35102-127">When you deploy the example template, you enter values for the name and password of the administrator account on each VM and the number of VMs to create.</span></span> <span data-ttu-id="35102-128">Tiene la opción de especificar valores de parámetro en un archivo independiente que se administra con la plantilla, o bien proporcionarlos se le solicite.</span><span class="sxs-lookup"><span data-stu-id="35102-128">You have the option of specifying parameter values in a separate file that's managed with the template, or providing values when prompted.</span></span>

<span data-ttu-id="35102-129">Las [variables](../../resource-group-authoring-templates.md) facilitan la tarea de establecer valores en la plantilla que se usan varias veces en ella o que cambian con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="35102-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you to set up values in the template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="35102-130">Esta sección de variables se utiliza en el ejemplo:</span><span class="sxs-lookup"><span data-stu-id="35102-130">This variables section is used in the example:</span></span>

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

<span data-ttu-id="35102-131">Al implementar la plantilla de ejemplo, los valores de las variables se utilizan para el nombre y el identificador de la cuenta de almacenamiento creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="35102-131">When you deploy the example template, variable values are used for the name and identifier of the previously created storage account.</span></span> <span data-ttu-id="35102-132">También se usan variables para proporcionar los valores de la extensión de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="35102-132">Variables are also used to provide the settings for the diagnostic extension.</span></span> <span data-ttu-id="35102-133">Lea [Procedimientos recomendados para crear plantillas de Azure Resource Manager](../../resource-manager-template-best-practices.md) para ayudarlo a decidir cómo desea estructurar los parámetros y variables de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="35102-133">Use the [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) to help you decide how you want to structure the parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="35102-134">bucles de recursos</span><span class="sxs-lookup"><span data-stu-id="35102-134">Resource loops</span></span>

<span data-ttu-id="35102-135">Si necesita más de una máquina virtual para la aplicación, puede utilizar un elemento de copia en una plantilla.</span><span class="sxs-lookup"><span data-stu-id="35102-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="35102-136">Este elemento opcional recorre en bucle la creación del número de máquinas virtuales que especificó como un parámetro:</span><span class="sxs-lookup"><span data-stu-id="35102-136">This optional element loops through creating the number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="35102-137">Además, tenga en cuenta en el ejemplo se utiliza el índice de bucle al especificar algunos de los valores para el recurso.</span><span class="sxs-lookup"><span data-stu-id="35102-137">Also, notice in the example that the loop index is used when specifying some of the values for the resource.</span></span> <span data-ttu-id="35102-138">Por ejemplo, si ha especificado un recuento de las tres instancias, los nombres de los discos del SO son "myOSDisk1", "myOSDisk2" y "myOSDisk3":</span><span class="sxs-lookup"><span data-stu-id="35102-138">For example, if you entered an instance count of three, the names of the operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="35102-139">Este ejemplo utiliza discos administrados para las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="35102-139">This example uses managed disks for the virtual machines.</span></span>
>
>

<span data-ttu-id="35102-140">Tenga en cuenta que la creación de un bucle para un recurso de la plantilla puede requerir que se utilice dicho bucle al crear otros recursos o acceder a ellos.</span><span class="sxs-lookup"><span data-stu-id="35102-140">Keep in mind that creating a loop for one resource in the template may require you to use the loop when creating or accessing other resources.</span></span> <span data-ttu-id="35102-141">Por ejemplo, varias máquinas virtuales no pueden usar la misma interfaz de red; por tanto, si recorre en bucle la creación de tres máquinas virtuales, también debe hacerlo con la generación de las tres interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="35102-141">For example, multiple VMs can’t use the same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="35102-142">Al asignar una interfaz de red a una máquina virtual, el índice de bucle se utiliza para identificarlo:</span><span class="sxs-lookup"><span data-stu-id="35102-142">When assigning a network interface to a VM, the loop index is used to identify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="35102-143">Dependencias</span><span class="sxs-lookup"><span data-stu-id="35102-143">Dependencies</span></span>

<span data-ttu-id="35102-144">La mayoría de los recursos dependen de otros para que funcionen correctamente.</span><span class="sxs-lookup"><span data-stu-id="35102-144">Most resources depend on other resources to work correctly.</span></span> <span data-ttu-id="35102-145">Las máquinas virtuales deben estar asociadas con una red virtual y, para tal fin, necesita una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="35102-145">Virtual machines must be associated with a virtual network and to do that it needs a network interface.</span></span> <span data-ttu-id="35102-146">El elemento [dependsOn](../../resource-group-define-dependencies.md) se utiliza para asegurarse de que la interfaz de red está lista para usarse antes de que se creen las máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="35102-146">The [dependsOn](../../resource-group-define-dependencies.md) element is used to make sure that the network interface is ready to be used before the VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="35102-147">Resource Manager implementa en paralelo todos los recursos que no dependan de otro que se vaya a implementar.</span><span class="sxs-lookup"><span data-stu-id="35102-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="35102-148">Tenga cuidado al establecer las dependencias porque puede ralentizar accidentalmente el proceso si define algunas que sean innecesarias.</span><span class="sxs-lookup"><span data-stu-id="35102-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="35102-149">Pueden encadenar las dependencias a través de varios recursos.</span><span class="sxs-lookup"><span data-stu-id="35102-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="35102-150">Por ejemplo, la interfaz de red depende de la dirección IP pública y los recursos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="35102-150">For example, the network interface depends on the public IP address and virtual network resources.</span></span>

<span data-ttu-id="35102-151">¿Cómo puede saber si se requiere una dependencia?</span><span class="sxs-lookup"><span data-stu-id="35102-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="35102-152">Examine los valores establecidos en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="35102-152">Look at the values you set in the template.</span></span> <span data-ttu-id="35102-153">Si un elemento de la definición de máquina virtual apunta a otro recurso que se implementa en la misma plantilla, necesita una dependencia.</span><span class="sxs-lookup"><span data-stu-id="35102-153">If an element in the virtual machine resource definition points to another resource that is deployed in the same template, you need a dependency.</span></span> <span data-ttu-id="35102-154">Por ejemplo, la máquina virtual de ejemplo define un perfil de red:</span><span class="sxs-lookup"><span data-stu-id="35102-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="35102-155">Para establecer esta propiedad, debe existir la interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="35102-155">To set this property, the network interface must exist.</span></span> <span data-ttu-id="35102-156">Por lo tanto, necesita una dependencia.</span><span class="sxs-lookup"><span data-stu-id="35102-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="35102-157">También debe establecer una dependencia cuando se define un recurso (un elemento secundario) dentro de otro recurso (un elemento primario).</span><span class="sxs-lookup"><span data-stu-id="35102-157">You also need to set a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="35102-158">Por ejemplo, las extensiones de script personalizado y la configuración de diagnóstico se definen como recursos secundarios de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="35102-158">For example, the diagnostic settings and custom script extensions are both defined as child resources of the virtual machine.</span></span> <span data-ttu-id="35102-159">No se creará hasta que la máquina virtual exista.</span><span class="sxs-lookup"><span data-stu-id="35102-159">They cannot be created until the virtual machine exists.</span></span> <span data-ttu-id="35102-160">Por lo tanto, los recursos se marcan como dependientes de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="35102-160">Therefore, both resources are marked as dependent on the virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="35102-161">Perfiles</span><span class="sxs-lookup"><span data-stu-id="35102-161">Profiles</span></span>

<span data-ttu-id="35102-162">Al definir un recurso de máquina virtual, se utilizan varios elementos de perfil.</span><span class="sxs-lookup"><span data-stu-id="35102-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="35102-163">Algunos son necesarios y otros, opcionales.</span><span class="sxs-lookup"><span data-stu-id="35102-163">Some are required and some are optional.</span></span> <span data-ttu-id="35102-164">Por ejemplo, los elementos hardwareProfile, osProfile, storageProfile y networkProfile son necesarios, pero diagnosticsProfile es opcional.</span><span class="sxs-lookup"><span data-stu-id="35102-164">For example, the hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but the diagnosticsProfile is optional.</span></span> <span data-ttu-id="35102-165">Estos perfiles definen opciones como:</span><span class="sxs-lookup"><span data-stu-id="35102-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="35102-166">Tamaño</span><span class="sxs-lookup"><span data-stu-id="35102-166">size</span></span>](sizes.md)
- <span data-ttu-id="35102-167">[Nombre](/architecture/best-practices/naming-conventions) y credenciales</span><span class="sxs-lookup"><span data-stu-id="35102-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="35102-168">[Configuración del sistema operativo](cli-ps-findimage.md) y disco</span><span class="sxs-lookup"><span data-stu-id="35102-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="35102-169">Interfaz de red</span><span class="sxs-lookup"><span data-stu-id="35102-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="35102-170">Diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="35102-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="35102-171">Discos e imágenes</span><span class="sxs-lookup"><span data-stu-id="35102-171">Disks and images</span></span>
   
<span data-ttu-id="35102-172">En Azure, los archivos de VHD pueden representar [discos o imágenes](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="35102-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="35102-173">Cuando el sistema operativo de un archivo de VHD está especializado para ser una máquina virtual específica, se conoce como "disco".</span><span class="sxs-lookup"><span data-stu-id="35102-173">When the operating system in a vhd file is specialized to be a specific VM, it is referred to as a disk.</span></span> <span data-ttu-id="35102-174">Cuando el sistema operativo de un archivo de VHD está generalizado para crear muchas máquinas virtuales, se conoce como "imagen".</span><span class="sxs-lookup"><span data-stu-id="35102-174">When the operating system in a vhd file is generalized to be used to create many VMs, it is referred to as an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="35102-175">Creación de máquinas virtuales y discos a partir de una imagen de plataforma</span><span class="sxs-lookup"><span data-stu-id="35102-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="35102-176">Cuando se crea una máquina virtual, debe decidir qué sistema operativo usar.</span><span class="sxs-lookup"><span data-stu-id="35102-176">When you create a VM, you must decide what operating system to use.</span></span> <span data-ttu-id="35102-177">El elemento imageReference se utiliza para definir el sistema operativo de una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="35102-177">The imageReference element is used to define the operating system of a new VM.</span></span> <span data-ttu-id="35102-178">En el ejemplo se muestra una definición de un sistema operativo Windows Server:</span><span class="sxs-lookup"><span data-stu-id="35102-178">The example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="35102-179">Si desea crear un sistema operativo Linux, puede usar esta definición:</span><span class="sxs-lookup"><span data-stu-id="35102-179">If you want to create a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="35102-180">Los valores de configuración del disco del SO se asignan con el elemento osDisk.</span><span class="sxs-lookup"><span data-stu-id="35102-180">Configuration settings for the operating system disk are assigned with the osDisk element.</span></span> <span data-ttu-id="35102-181">En el ejemplo se define un nuevo disco administrado con el modo de almacenamiento en caché establecido en **ReadWrite** y que se va a crear el disco de un [imagen de plataforma](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="35102-181">The example defines a new managed disk with the caching mode set to **ReadWrite** and that the disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="35102-182">Creación de máquinas virtuales a partir de discos administrados existentes</span><span class="sxs-lookup"><span data-stu-id="35102-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="35102-183">Si desea crear máquinas virtuales a partir de discos existentes, quite los elementos imageReference y osProfile, y defina esta configuración de disco:</span><span class="sxs-lookup"><span data-stu-id="35102-183">If you want to create virtual machines from existing disks, remove the imageReference and the osProfile elements and define these disk settings:</span></span>

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

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="35102-184">Creación de máquinas virtuales a partir de una imagen administrada</span><span class="sxs-lookup"><span data-stu-id="35102-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="35102-185">Si desea crear una máquina virtual a partir de una imagen personalizada, cambie el elemento imageReference y defina esta configuración de disco:</span><span class="sxs-lookup"><span data-stu-id="35102-185">If you want to create a virtual machine from a managed image, change the imageReference element and define these disk settings:</span></span>

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

### <a name="attach-data-disks"></a><span data-ttu-id="35102-186">Conexión de discos de datos</span><span class="sxs-lookup"><span data-stu-id="35102-186">Attach data disks</span></span>

<span data-ttu-id="35102-187">Si lo desea, puede agregar discos de datos a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="35102-187">You can optionally add data disks to the VMs.</span></span> <span data-ttu-id="35102-188">El [número de discos](sizes.md) depende del tamaño del disco de sistema operativo que utilice.</span><span class="sxs-lookup"><span data-stu-id="35102-188">The [number of disks](sizes.md) depends on the size of operating system disk that you use.</span></span> <span data-ttu-id="35102-189">Con el tamaño de las máquinas virtuales establecido en Standard_DS1_v2, el número máximo de discos de datos que podría agregarse a es 2.</span><span class="sxs-lookup"><span data-stu-id="35102-189">With the size of the VMs set to Standard_DS1_v2, the maximum number of data disks that could be added to the them is two.</span></span> <span data-ttu-id="35102-190">En el ejemplo, se agrega un disco administrado a cada máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="35102-190">In the example, one managed data disk is being added to each VM:</span></span>

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

## <a name="extensions"></a><span data-ttu-id="35102-191">Extensiones</span><span class="sxs-lookup"><span data-stu-id="35102-191">Extensions</span></span>

<span data-ttu-id="35102-192">Aunque las [extensiones](extensions-features.md) son un recurso independiente, están estrechamente relacionadas con las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="35102-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied to VMs.</span></span> <span data-ttu-id="35102-193">Las extensiones pueden agregar como un recurso secundario de la máquina virtual o como uno independiente.</span><span class="sxs-lookup"><span data-stu-id="35102-193">Extensions can be added as a child resource of the VM or as a separate resource.</span></span> <span data-ttu-id="35102-194">El ejemplo muestra la [extensión de diagnóstico](extensions-diagnostics-template.md) que se agrega a las máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="35102-194">The example shows the [Diagnostics Extension](extensions-diagnostics-template.md) being added to the VMs:</span></span>

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

<span data-ttu-id="35102-195">Este recurso de extensión usa la variable storageName y las variables de diagnóstico para proporcionar valores.</span><span class="sxs-lookup"><span data-stu-id="35102-195">This extension resource uses the storageName variable and the diagnostic variables to provide values.</span></span> <span data-ttu-id="35102-196">Si desea cambiar los datos recopilados mediante esta extensión, puede agregar más contadores de rendimiento a la variable wadperfcounters.</span><span class="sxs-lookup"><span data-stu-id="35102-196">If you want to change the data that is collected by this extension, you can add more performance counters to the wadperfcounters variable.</span></span> <span data-ttu-id="35102-197">También podría elegir poner los datos de diagnóstico en una cuenta de almacenamiento diferente a donde se almacenan los discos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="35102-197">You could also choose to put the diagnostics data into a different storage account than where the VM disks are stored.</span></span>

<span data-ttu-id="35102-198">Existen muchas extensiones que se pueden instalar en una máquina virtual, pero la más útil es probablemente la de [script personalizado](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="35102-198">There are many extensions that you can install on a VM, but the most useful is probably the [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="35102-199">En el ejemplo, un script de PowerShell denominado "start.ps1" se ejecuta en cada máquina virtual cuando se inicia por primera vez:</span><span class="sxs-lookup"><span data-stu-id="35102-199">In the example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

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

<span data-ttu-id="35102-200">El script start.ps1 puede realizar muchas tareas de configuración.</span><span class="sxs-lookup"><span data-stu-id="35102-200">The start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="35102-201">Por ejemplo, no se inicializan los discos de datos que se agregan a las máquinas virtuales en el ejemplo; puede usar uno personalizado para inicializarlos.</span><span class="sxs-lookup"><span data-stu-id="35102-201">For example, the data disks that are added to the VMs in the example are not initialized; you can use a custom script to initialize them.</span></span> <span data-ttu-id="35102-202">Si tiene varias tareas de inicio para realizar, puede utilizar el archivo start.ps1 para llamar a otros scripts de PowerShell en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="35102-202">If you have multiple startup tasks to do, you can use the start.ps1 file to call other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="35102-203">En el ejemplo se usa PowerShell, pero puede usar cualquier método de scripting que esté disponible en el sistema operativo que esté utilizando.</span><span class="sxs-lookup"><span data-stu-id="35102-203">The example uses PowerShell, but you can use any scripting method that is available on the operating system that you are using.</span></span>

<span data-ttu-id="35102-204">Puede ver el estado de las extensiones instaladas en la configuración de extensiones del portal:</span><span class="sxs-lookup"><span data-stu-id="35102-204">You can see the status of the installed extensions from the Extensions settings in the portal:</span></span>

![Consulta del estado de la extensión](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="35102-206">También puede obtener información de la extensión mediante el comando de PowerShell **Get-AzureRmVMExtension**, el comando de la CLI 2.0 de Azure, **vm extension get** o la API de REST de **obtención de información de extensiones**.</span><span class="sxs-lookup"><span data-stu-id="35102-206">You can also get extension information by using the **Get-AzureRmVMExtension** PowerShell command, the **vm extension get** Azure CLI 2.0 command, or the **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="35102-207">Implementaciones</span><span class="sxs-lookup"><span data-stu-id="35102-207">Deployments</span></span>

<span data-ttu-id="35102-208">Cuando se implementa una plantilla, Azure realiza un seguimiento de los recursos implementados como un grupo y asigna automáticamente un nombre para este grupo implementado.</span><span class="sxs-lookup"><span data-stu-id="35102-208">When you deploy a template, Azure tracks the resources that you deployed as a group and automatically assigns a name to this deployed group.</span></span> <span data-ttu-id="35102-209">El nombre de la implementación es el mismo que el de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="35102-209">The name of the deployment is the same as the name of the template.</span></span>

<span data-ttu-id="35102-210">Si le preocupa el estado de los recursos de la implementación, puede usar la hoja Grupo de recursos de Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="35102-210">If you are curious about the status of resources in the deployment, you can use the Resource Group blade in the Azure portal:</span></span>

![Obtención de la información de implementación](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="35102-212">No pasa nada por usar la misma plantilla para crear o actualizar recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="35102-212">It’s not a problem to use the same template to create resources or to update existing resources.</span></span> <span data-ttu-id="35102-213">Al usar comandos para implementar plantillas, tiene la oportunidad de indicar qué [modo](../../resource-group-template-deploy.md) usar.</span><span class="sxs-lookup"><span data-stu-id="35102-213">When you use commands to deploy templates, you have the opportunity to say which [mode](../../resource-group-template-deploy.md) you want to use.</span></span> <span data-ttu-id="35102-214">El modo se puede establecer en **Completo** o **Incremental**.</span><span class="sxs-lookup"><span data-stu-id="35102-214">The mode can be set to either **Complete** or **Incremental**.</span></span> <span data-ttu-id="35102-215">El valor predeterminado son actualizaciones incrementales.</span><span class="sxs-lookup"><span data-stu-id="35102-215">The default is to do incremental updates.</span></span> <span data-ttu-id="35102-216">Tenga precaución al utilizar el modo **Completo** porque se pueden eliminar accidentalmente los recursos.</span><span class="sxs-lookup"><span data-stu-id="35102-216">Be careful when using the **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="35102-217">Cuando se establece el modo en **Completo**, Resource Manager elimina los recursos del grupo de recursos que no están en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="35102-217">When you set the mode to **Complete**, Resource Manager deletes any resources in the resource group that are not in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35102-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35102-218">Next Steps</span></span>

- <span data-ttu-id="35102-219">Cree su propia plantilla con las [Creación de plantillas de Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="35102-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="35102-220">Implemente la plantilla que creó mediante [Creación de una máquina virtual Windows con una plantilla de Resource Manager](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="35102-220">Deploy the template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="35102-221">Aprenda a administrar la máquina virtual que ha creado repasando el tema [Creación y administración de máquinas virtuales Windows con el módulo de Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="35102-221">Learn how to manage the VMs that you created by reviewing [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
