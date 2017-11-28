---
title: "aaaAutoscale conjuntos de escalas de máquina Virtual de Windows | Documentos de Microsoft"
description: "Configuración del escalado automático para un conjunto de escalado de máquinas virtuales Windows mediante Azure PowerShell"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="2817c-103">Escalado automático de máquinas en un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="2817c-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="2817c-104">Conjuntos de escalas de máquina virtual hacen más sencillo para usted toodeploy y administran máquinas virtuales idénticas como un conjunto.</span><span class="sxs-lookup"><span data-stu-id="2817c-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="2817c-105">Los conjuntos de escala proporcionan una capa de proceso altamente escalable y personalizable para aplicaciones de gran escala y admiten imágenes de la plataforma Windows, imágenes de la plataforma Linux, imágenes personalizadas y extensiones.</span><span class="sxs-lookup"><span data-stu-id="2817c-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="2817c-106">Para más información acerca de los conjuntos de escala, consulte [Conjuntos de escala de máquinas virtuales](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2817c-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="2817c-107">Este tutorial muestra cómo establece un conjunto de escala de máquinas virtuales de Windows y, automáticamente, escala de máquinas de Hola Hola toocreate.</span><span class="sxs-lookup"><span data-stu-id="2817c-107">This tutorial shows you how toocreate a scale set of Windows virtual machines and automatically scale hello machines in hello set.</span></span> <span data-ttu-id="2817c-108">Crear escala de hello establecer y configurar el escalado mediante la creación de una plantilla de Azure Resource Manager e implementación mediante PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="2817c-108">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="2817c-109">Para más información sobre las plantillas, consulte [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2817c-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="2817c-110">toolearn más información acerca de escalado automático de conjuntos de escalado, consulte [el escalado automático y establece de la escala en la máquina Virtual](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2817c-110">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="2817c-111">En este artículo, implementar siguiente Hola recursos y extensiones:</span><span class="sxs-lookup"><span data-stu-id="2817c-111">In this article, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="2817c-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="2817c-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="2817c-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="2817c-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="2817c-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="2817c-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="2817c-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="2817c-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="2817c-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="2817c-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="2817c-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="2817c-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="2817c-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="2817c-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="2817c-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="2817c-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="2817c-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="2817c-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="2817c-121">Para más información sobre los recursos de Resource Manager, consulte [Implementación mediante Azure Resource Manager frente al modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2817c-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="2817c-122">Paso 1: Instalación de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2817c-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="2817c-123">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener información acerca de cómo instalar la versión más reciente de Hola de PowerShell de Azure, seleccione su suscripción y firma en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2817c-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooAzure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="2817c-124">Paso 2: Creación de un grupo de recursos y una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="2817c-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="2817c-125">**Crear un grupo de recursos** : todos los recursos deben ser el grupo de recursos de tooa implementado.</span><span class="sxs-lookup"><span data-stu-id="2817c-125">**Create a resource group** – All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="2817c-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate un grupo de recursos denominado **vmsstestrg1**.</span><span class="sxs-lookup"><span data-stu-id="2817c-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="2817c-127">**Crear una cuenta de almacenamiento** : esta cuenta de almacenamiento es donde se almacena la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-127">**Create a storage account** – This storage account is where hello template is stored.</span></span> <span data-ttu-id="2817c-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate una cuenta de almacenamiento denominada **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="2817c-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-hello-template"></a><span data-ttu-id="2817c-129">Paso 3: Crear plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="2817c-129">Step 3: Create hello template</span></span>
<span data-ttu-id="2817c-130">Una plantilla de Azure Resource Manager hace posible toodeploy y administrar recursos de Azure de forma conjunta mediante una descripción de JSON de recursos de Hola y parámetros de implementación asociados.</span><span class="sxs-lookup"><span data-stu-id="2817c-130">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="2817c-131">En su editor favorito, cree el archivo hello C:\VMSSTemplate.json y agregue Hola inicial JSON toosupport Hola plantilla de la estructura.</span><span class="sxs-lookup"><span data-stu-id="2817c-131">In your favorite editor, create hello file C:\VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="2817c-132">Parámetros no son siempre obligatorios, pero proporcionan una manera tooinput valores cuando se implementa la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-132">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="2817c-133">Agregue estos parámetros en el elemento primario Hola parámetros que agregó toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="2817c-133">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="2817c-134">Un nombre para la máquina virtual independiente hello tooaccess usado Hola máquinas en conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-134">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
    * <span data-ttu-id="2817c-135">nombre de Hola de cuenta de almacenamiento de Hola donde se almacena la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-135">hello name of hello storage account where hello template is stored.</span></span>
    * <span data-ttu-id="2817c-136">número de Hola de máquinas virtuales tooinitially crear en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-136">hello number of virtual machines tooinitially create in hello scale set.</span></span>
    * <span data-ttu-id="2817c-137">nombre de Hola y la contraseña de cuenta de administrador de hello en máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-137">hello name and password of hello administrator account on hello virtual machines.</span></span>
    * <span data-ttu-id="2817c-138">Establece un prefijo de nombre de los recursos de Hola que se crean la escala de hello toosupport.</span><span class="sxs-lookup"><span data-stu-id="2817c-138">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="2817c-139">Las variables pueden usarse en un valores toospecify de plantilla que se pueden cambiar con frecuencia o valores que necesitan toobe crean a partir de una combinación de valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="2817c-139">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="2817c-140">Agregue estas variables en el elemento primario Hola variables que agregó toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="2817c-140">Add these variables under hello variables parent element that you added toohello template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * <span data-ttu-id="2817c-141">Los nombres DNS que se usan por hello interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="2817c-141">DNS names that are used by hello network interfaces.</span></span>

        * <span data-ttu-id="2817c-142">Hola nombres de las direcciones IP y los prefijos de red virtual de Hola y las subredes.</span><span class="sxs-lookup"><span data-stu-id="2817c-142">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
        * <span data-ttu-id="2817c-143">Hello nombres e identificadores de red virtual de hello, equilibrador de carga y las interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="2817c-143">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="2817c-144">Nombres de cuenta de almacenamiento para las cuentas de hello asociados a las máquinas de hello en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-144">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
        * <span data-ttu-id="2817c-145">Configuración de extensión de diagnóstico que se instala en máquinas virtuales de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-145">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="2817c-146">Para obtener más información acerca de la extensión de diagnósticos de hello, consulte [crear una máquina Virtual de Windows con la supervisión y diagnósticos mediante la plantilla de administrador de recursos de Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2817c-146">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="2817c-147">Agregar recurso de cuenta de almacenamiento de hello bajo el elemento primario Hola recursos que agregó toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="2817c-147">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="2817c-148">Esta plantilla utiliza un hello toocreate de bucle recomendada cinco cuentas de almacenamiento donde se almacenan los discos del sistema operativo hello y datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="2817c-148">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="2817c-149">Puede admitir este conjunto de cuentas de seguridad de máquinas virtuales de too100 en un conjunto de escala, que es el máximo actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-149">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="2817c-150">Cada cuenta de almacenamiento se denomina con un designador de letra que se definió en variables de hello combinadas con prefijo de Hola que se proporciona en los parámetros de hello para la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-150">Each storage account is named with a letter designator that was defined in hello variables combined with hello prefix that you provide in hello parameters for hello template.</span></span>

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. <span data-ttu-id="2817c-151">Agregar recursos de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-151">Add hello virtual network resource.</span></span> <span data-ttu-id="2817c-152">Consulte [Proveedor de recursos de red](../virtual-network/resource-groups-networking.md)para más información.</span><span class="sxs-lookup"><span data-stu-id="2817c-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="2817c-153">Agregar Hola públicos recursos de dirección IP que se usan por hello equilibrador de carga y la interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="2817c-153">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="2817c-154">Agregar recurso de equilibrador de carga de hello utilizado por el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-154">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="2817c-155">Para más información, consulte [Compatibilidad del Administrador de recursos de Azure con el equilibrador de carga](../load-balancer/load-balancer-arm.md)</span><span class="sxs-lookup"><span data-stu-id="2817c-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="2817c-156">Agregar recurso de interfaz de red de Hola que usa la máquina virtual independiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-156">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="2817c-157">Dado que las máquinas en un conjunto de escala no están accesibles a través de una dirección IP pública, una máquina virtual independiente se crea en Hola mismo virtual máquinas Hola de tooremotely acceso de red.</span><span class="sxs-lookup"><span data-stu-id="2817c-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="2817c-158">Agregar máquina virtual independiente que Hola Hola misma red que el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-158">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
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
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"        
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="2817c-159">Agregar el recurso de conjunto de escalas de máquina virtual de Hola y especifique la extensión de diagnósticos de Hola que está instalado en todas las máquinas virtuales en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-159">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="2817c-160">Muchos de los valores de hello para este recurso son similares con el recurso de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-160">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="2817c-161">Hola principales diferencias son elementos de capacidad de Hola que especifica el número de Hola de máquinas virtuales en el conjunto de escalas de Hola y upgradePolicy que especifica cómo se realizan las actualizaciones toovirtual máquinas.</span><span class="sxs-lookup"><span data-stu-id="2817c-161">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set, and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="2817c-162">Hello conjunto de escala no se crea hasta que se crean todas las cuentas de almacenamiento de hello según se haya especificado con el elemento dependsOn de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-162">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="2817c-163">Agregue hello autoscaleSettings recurso que define cómo se ajusta según el uso de procesador de hello en máquinas de hello en el conjunto de escalas de Hola Hola conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="2817c-163">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on hello processor usage on hello machines in hello scale set.</span></span>

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    <span data-ttu-id="2817c-164">Para este tutorial, destacan estos valores:</span><span class="sxs-lookup"><span data-stu-id="2817c-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="2817c-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="2817c-165">**metricName**</span></span>  
    <span data-ttu-id="2817c-166">Este valor es Hola igual que el contador de rendimiento de Hola que hemos definido en la variable de wadperfcounter Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-166">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="2817c-167">Con esa variable, extensión de diagnósticos de hello recopila hello **procesador (_Total)\% tiempo de procesador** contador.</span><span class="sxs-lookup"><span data-stu-id="2817c-167">Using that variable, hello Diagnostics extension collects hello  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="2817c-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="2817c-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="2817c-169">Este valor es el identificador de recurso de hello del conjunto de escalas de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-169">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="2817c-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="2817c-170">**timeGrain**</span></span>  
    <span data-ttu-id="2817c-171">Este valor es la granularidad de Hola de métricas de Hola que se recopilan.</span><span class="sxs-lookup"><span data-stu-id="2817c-171">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="2817c-172">En esta plantilla, se establece tooone minuto.</span><span class="sxs-lookup"><span data-stu-id="2817c-172">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="2817c-173">**statistic**</span><span class="sxs-lookup"><span data-stu-id="2817c-173">**statistic**</span></span>  
    <span data-ttu-id="2817c-174">Este valor determina la forma métricas Hola Hola combinado tooaccommodate acción de escala automática.</span><span class="sxs-lookup"><span data-stu-id="2817c-174">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="2817c-175">Hola los valores posibles son: Average, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="2817c-175">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="2817c-176">En esta plantilla, se recopila Hola promedio uso total de CPU de las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-176">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>
    
    * <span data-ttu-id="2817c-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="2817c-177">**timeWindow**</span></span>  
    <span data-ttu-id="2817c-178">Este valor es Hola intervalo de tiempo en el que se recopilan datos de instancia.</span><span class="sxs-lookup"><span data-stu-id="2817c-178">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="2817c-179">Debe estar comprendido entre 5 minutos y 12 horas.</span><span class="sxs-lookup"><span data-stu-id="2817c-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="2817c-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="2817c-180">**timeAggregation**</span></span>  
    <span data-ttu-id="2817c-181">su valor determina cómo se deben combinar los datos de Hola que se recopilan con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="2817c-181">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="2817c-182">valor predeterminado de Hello es Media.</span><span class="sxs-lookup"><span data-stu-id="2817c-182">hello default value is Average.</span></span> <span data-ttu-id="2817c-183">Hola los valores posibles son: promedio, mínimo, máximo, último, Total, recuento.</span><span class="sxs-lookup"><span data-stu-id="2817c-183">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="2817c-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="2817c-184">**operator**</span></span>  
    <span data-ttu-id="2817c-185">Este valor es el operador de Hola que es usado toocompare Hola hello y datos de umbral de métrica.</span><span class="sxs-lookup"><span data-stu-id="2817c-185">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="2817c-186">Hola los valores posibles son: es igual a, valores, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="2817c-186">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="2817c-187">**threshold**</span><span class="sxs-lookup"><span data-stu-id="2817c-187">**threshold**</span></span>  
    <span data-ttu-id="2817c-188">Este valor es el valor de Hola que desencadena la acción de escalado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-188">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="2817c-189">En esta plantilla, las máquinas se agregan escala toohello establecer una vez Hola uso de la CPU entre máquinas en conjunto hello más de 50%.</span><span class="sxs-lookup"><span data-stu-id="2817c-189">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="2817c-190">**dirección**</span><span class="sxs-lookup"><span data-stu-id="2817c-190">**direction**</span></span>  
    <span data-ttu-id="2817c-191">Este valor determina la acción de Hola que se realiza cuando se obtiene el valor de umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-191">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="2817c-192">valores posibles de Hello son aumentan o disminuyen.</span><span class="sxs-lookup"><span data-stu-id="2817c-192">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="2817c-193">En esta plantilla, hello número de máquinas virtuales en el conjunto de escalas de hello aumenta si el umbral de hello es más de 50% en el período de tiempo de hello definido.</span><span class="sxs-lookup"><span data-stu-id="2817c-193">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>
    
    * <span data-ttu-id="2817c-194">**type**</span><span class="sxs-lookup"><span data-stu-id="2817c-194">**type**</span></span>  
    <span data-ttu-id="2817c-195">Este valor es el tipo de Hola de acción que se realizarán y se debe establecer tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="2817c-195">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="2817c-196">**value**</span><span class="sxs-lookup"><span data-stu-id="2817c-196">**value**</span></span>  
    <span data-ttu-id="2817c-197">Este valor es el número de Hola de máquinas virtuales que se agregan o quitan del conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-197">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="2817c-198">Este valor debe ser 1 o un valor superior.</span><span class="sxs-lookup"><span data-stu-id="2817c-198">This value must be 1 or greater.</span></span> <span data-ttu-id="2817c-199">valor predeterminado de Hello es 1.</span><span class="sxs-lookup"><span data-stu-id="2817c-199">hello default value is 1.</span></span> <span data-ttu-id="2817c-200">En esta plantilla, Hola establece número de máquinas en escala de hello aumenta 1 cuando se alcanza el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-200">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>
    
    * <span data-ttu-id="2817c-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="2817c-201">**cooldown**</span></span>  
    <span data-ttu-id="2817c-202">Este valor es cantidad de Hola de toowait de tiempo desde la última acción de escalado de hello antes de que se produce la acción siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-202">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="2817c-203">Debe estar comprendido entre un minuto y una semana.</span><span class="sxs-lookup"><span data-stu-id="2817c-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="2817c-204">Guarde el archivo de plantilla de hello.</span><span class="sxs-lookup"><span data-stu-id="2817c-204">Save hello template file.</span></span>    

## <a name="step-4-upload-hello-template-toostorage"></a><span data-ttu-id="2817c-205">Paso 4: Cargar Hola plantilla toostorage</span><span class="sxs-lookup"><span data-stu-id="2817c-205">Step 4: Upload hello template toostorage</span></span>
<span data-ttu-id="2817c-206">plantilla de Hola se puede cargar como sabe hello y clave principal de la cuenta de almacenamiento de Hola que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="2817c-206">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="2817c-207">En la ventana de Microsoft Azure PowerShell hello, establecer una variable que especifica el nombre de Hola de cuenta de almacenamiento de Hola que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="2817c-207">In hello Microsoft Azure PowerShell window, set a variable that specifies hello name of hello storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="2817c-208">Establecer una variable que especifica la clave principal de Hola de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-208">Set a variable that specifies hello primary key of hello storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="2817c-209">Puede obtener esta clave, haga clic en un icono de llave Hola al ver los recursos de cuenta de almacenamiento de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2817c-209">You can get this key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span>
3. <span data-ttu-id="2817c-210">Crear objeto de contexto de cuenta de almacenamiento de hello es decir, las operaciones de toovalidate utilizado con la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-210">Create hello storage account context object that is used toovalidate operations with hello storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="2817c-211">Crear contenedor de Hola para almacenar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-211">Create hello container for storing hello template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="2817c-212">Cargar nuevo contenedor toohello del archivo de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-212">Upload hello template file toohello new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a><span data-ttu-id="2817c-213">Paso 5: Implementar la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="2817c-213">Step 5: Deploy hello template</span></span>
<span data-ttu-id="2817c-214">Ahora que ha creado la plantilla de hello, puede empezar a implementar los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-214">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="2817c-215">Utilice este proceso de hello toostart de comando:</span><span class="sxs-lookup"><span data-stu-id="2817c-215">Use this command toostart hello process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="2817c-216">Cuando se presiona escriba, son valores tooprovide solicitadas para las variables de Hola que asignó.</span><span class="sxs-lookup"><span data-stu-id="2817c-216">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="2817c-217">Proporcione estos valores:</span><span class="sxs-lookup"><span data-stu-id="2817c-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="2817c-218">Para implementar todos los toosuccessfully de recursos de hello tardará aproximadamente 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="2817c-218">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="2817c-219">También puede usar recursos del portal de hello capacidad toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-219">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="2817c-220">Utilice este vínculo: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span><span class="sxs-lookup"><span data-stu-id="2817c-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="2817c-221">Paso 6: Supervisión de recursos</span><span class="sxs-lookup"><span data-stu-id="2817c-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="2817c-222">Puede obtener información acerca de los conjuntos de escala de máquinas virtuales mediante estos métodos:</span><span class="sxs-lookup"><span data-stu-id="2817c-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="2817c-223">Hola portal de Azure: actualmente, puede obtener una cantidad limitada de información mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-223">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>
* <span data-ttu-id="2817c-224">Hola [Explorador de recursos de Azure](https://resources.azure.com/) -esta herramienta es más adecuado para explorar el estado actual de Hola de su conjunto de escalas de hello.</span><span class="sxs-lookup"><span data-stu-id="2817c-224">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="2817c-225">Siga esta ruta de acceso y debería ver la vista de instancia de Hola de escala de hello establecido que creó:</span><span class="sxs-lookup"><span data-stu-id="2817c-225">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    <span data-ttu-id="2817c-226">Suscripciones > {su suscripción} > resourceGroups > vmsstestrg1 > proveedores > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span><span class="sxs-lookup"><span data-stu-id="2817c-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="2817c-227">Azure PowerShell, Use este comando tooget cierta información:</span><span class="sxs-lookup"><span data-stu-id="2817c-227">Azure PowerShell - Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="2817c-228">O</span><span class="sxs-lookup"><span data-stu-id="2817c-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="2817c-229">Conectar máquina virtual independiente que toohello tal como lo haría con cualquier otro equipo y, a continuación, se pueden obtener acceso remoto a máquinas virtuales de hello en procesos individuales de hello escala conjunto toomonitor.</span><span class="sxs-lookup"><span data-stu-id="2817c-229">Connect toohello separate virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="2817c-230">Una API de REST completa para más información acerca de los conjuntos de escala se puede encontrar en [Conjuntos de escala de máquinas virtuales](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="2817c-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-hello-resources"></a><span data-ttu-id="2817c-231">Paso 7: Quitar recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="2817c-231">Step 7: Remove hello resources</span></span>
<span data-ttu-id="2817c-232">Dado que se le cobra por recursos que usa en Azure, siempre es un recursos toodelete recomendable que ya no son necesarios.</span><span class="sxs-lookup"><span data-stu-id="2817c-232">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="2817c-233">No es necesario toodelete cada recurso por separado de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2817c-233">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="2817c-234">Puede eliminar el grupo de recursos de Hola y todos sus recursos se eliminan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2817c-234">You can delete hello resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="2817c-235">Si desea tookeep el grupo de recursos, puede eliminar sólo al conjunto de escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="2817c-235">If you want tookeep your resource group, you can delete hello scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="2817c-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2817c-236">Next steps</span></span>
* <span data-ttu-id="2817c-237">Administrar conjunto de escalas de hello recién creado con información de hello en [administrar máquinas virtuales en un conjunto de escala de máquinas virtuales](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="2817c-237">Manage hello scale set that you just created using hello information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="2817c-238">Más información sobre el escalado vertical si consulta [Escalado automático vertical con conjuntos de escalado de máquinas virtuales](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span><span class="sxs-lookup"><span data-stu-id="2817c-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="2817c-239">Encuentre ejemplos de características de supervisión de Azure Monitor en [Ejemplos de inicio rápido de PowerShell de Azure Monitor](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2817c-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="2817c-240">Obtenga información sobre las características de notificación de [usar escalado automático acciones toosend correo electrónico y webhook notificaciones de alerta en el Monitor de Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="2817c-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="2817c-241">Obtenga información acerca de cómo demasiado[toosend webhook y correo electrónico notificaciones de alerta de registros de auditoría de uso en el Monitor de Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="2817c-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

