---
title: "Escalado automático de conjuntos de escalado de máquinas virtuales Windows | Microsoft Docs"
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
ms.openlocfilehash: 91f731bec46c005221f4e66e95822994070d4c26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="e458d-103">Escalado automático de máquinas en un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="e458d-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="e458d-104">Los conjuntos de escalado de máquinas virtuales facilitan la implementación y administración de máquinas virtuales idénticas como conjunto.</span><span class="sxs-lookup"><span data-stu-id="e458d-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="e458d-105">Los conjuntos de escala proporcionan una capa de proceso altamente escalable y personalizable para aplicaciones de gran escala y admiten imágenes de la plataforma Windows, imágenes de la plataforma Linux, imágenes personalizadas y extensiones.</span><span class="sxs-lookup"><span data-stu-id="e458d-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="e458d-106">Para más información acerca de los conjuntos de escala, consulte [Conjuntos de escala de máquinas virtuales](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e458d-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="e458d-107">Este tutorial muestra cómo crear un conjunto de escalado de máquinas virtuales Windows y cómo escalarlas automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e458d-107">This tutorial shows you how to create a scale set of Windows virtual machines and automatically scale the machines in the set.</span></span> <span data-ttu-id="e458d-108">El conjunto de escalado se crea y la configuración de escalado se configura mediante la creación de una plantilla de Azure Resource Manager que se implementa con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e458d-108">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="e458d-109">Para más información sobre las plantillas, consulte [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e458d-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="e458d-110">Para obtener más información sobre el escalado automático de conjuntos de escalado, consulte [Automatic scaling and Virtual Machine Scale Sets (Escalado automático y conjuntos de escalado de máquinas virtuales)](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e458d-110">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="e458d-111">En este artículo, se implementan los recursos y las extensiones siguientes:</span><span class="sxs-lookup"><span data-stu-id="e458d-111">In this article, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="e458d-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="e458d-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="e458d-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="e458d-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="e458d-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="e458d-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="e458d-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="e458d-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="e458d-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="e458d-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="e458d-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="e458d-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="e458d-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="e458d-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="e458d-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="e458d-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="e458d-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="e458d-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="e458d-121">Para más información sobre los recursos de Resource Manager, consulte [Implementación mediante Azure Resource Manager frente al modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e458d-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="e458d-122">Paso 1: Instalación de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e458d-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="e458d-123">Consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) para más información sobre cómo instalar la versión más reciente de Azure PowerShell, seleccionar la suscripción que desea usar e iniciar sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="e458d-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to Azure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="e458d-124">Paso 2: Creación de un grupo de recursos y una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e458d-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="e458d-125">**Cree un grupo de recursos** : todos los recursos deben implementarse en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e458d-125">**Create a resource group** – All resources must be deployed to a resource group.</span></span> <span data-ttu-id="e458d-126">Para crear un grupo de recursos denominado [vmsstestrg1](https://msdn.microsoft.com/library/mt603739.aspx) , use **New-AzureRmResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="e458d-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) to create a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="e458d-127">**Implemente una cuenta de almacenamiento** : en esta cuenta de almacenamiento se guarda la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e458d-127">**Create a storage account** – This storage account is where the template is stored.</span></span> <span data-ttu-id="e458d-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) para crear una cuenta de almacenamiento denominada " **vmsstestsa**".</span><span class="sxs-lookup"><span data-stu-id="e458d-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) to create a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-the-template"></a><span data-ttu-id="e458d-129">Paso 3: Creación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="e458d-129">Step 3: Create the template</span></span>
<span data-ttu-id="e458d-130">Las plantillas del Administrador de recursos de Azure le permiten implementar y administrar los distintos recursos de Azure en conjunto mediante una descripción de JSON de los recursos y los parámetros de implementación asociados.</span><span class="sxs-lookup"><span data-stu-id="e458d-130">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="e458d-131">En el editor que prefiera, cree el archivo C:\VMSSTemplate.json y agregue la estructura inicial de JSON para admitir la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e458d-131">In your favorite editor, create the file C:\VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

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

2. <span data-ttu-id="e458d-132">No siempre se necesitan parámetros, pero proporcionan una manera de introducir valores al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e458d-132">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="e458d-133">Agregue estos parámetros en el elemento primario de los parámetros que agregó a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e458d-133">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="e458d-134">Un nombre para la máquina virtual independiente que se utiliza para tener acceso a las máquinas del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="e458d-134">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
    * <span data-ttu-id="e458d-135">Un nombre para la cuenta de almacenamiento donde se guarda la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e458d-135">The name of the storage account where the template is stored.</span></span>
    * <span data-ttu-id="e458d-136">El número de máquinas virtuales para crear inicialmente en el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="e458d-136">The number of virtual machines to initially create in the scale set.</span></span>
    * <span data-ttu-id="e458d-137">El nombre y la contraseña de la cuenta de administrador en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e458d-137">The name and password of the administrator account on the virtual machines.</span></span>
    * <span data-ttu-id="e458d-138">Establece un prefijo de nombre de los recursos que se crean para admitir el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="e458d-138">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="e458d-139">Pueden usarse variables en una plantilla para especificar los valores que pueden cambiar con frecuencia o los valores que se deben crear a partir de una combinación de valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="e458d-139">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="e458d-140">Agregue estas variables en el elemento primario de las variables que agregó a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e458d-140">Add these variables under the variables parent element that you added to the template.</span></span>

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
   
    * <span data-ttu-id="e458d-141">Nombres DNS que usan las interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="e458d-141">DNS names that are used by the network interfaces.</span></span>

        * <span data-ttu-id="e458d-142">Los nombres de direcciones IP y los prefijos para la red virtual y las subredes.</span><span class="sxs-lookup"><span data-stu-id="e458d-142">The IP address names and prefixes for the virtual network and subnets.</span></span>
        * <span data-ttu-id="e458d-143">Los nombres y los identificadores de la red virtual, el equilibrador de carga y las interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="e458d-143">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="e458d-144">Los nombres de cuentas de almacenamiento para las cuentas asociadas a las máquinas en el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="e458d-144">Storage account names for the accounts associated with the machines in the scale set.</span></span>
        * <span data-ttu-id="e458d-145">Configuración de la extensión de diagnósticos que se instala en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e458d-145">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="e458d-146">Para más información sobre la extensión de diagnósticos, consulte [Crear una máquina virtual de Windows con supervisión y diagnóstico mediante la plantilla de Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e458d-146">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="e458d-147">Agregue el recurso de la cuenta de almacenamiento en el elemento primario de recursos que agregó a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e458d-147">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="e458d-148">Esta plantilla utiliza un bucle para crear las cinco cuentas de almacenamiento recomendadas donde se guardan los discos del sistema operativo y los datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e458d-148">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="e458d-149">Este conjunto de cuentas puede admitir hasta 100 máquinas virtuales en un conjunto de escala, lo cual es el máximo actual.</span><span class="sxs-lookup"><span data-stu-id="e458d-149">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="e458d-150">Cada cuenta de almacenamiento se denomina con un indicador de letra, que se definió en las variables, y se combina con el prefijo que proporcionó en los parámetros de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e458d-150">Each storage account is named with a letter designator that was defined in the variables combined with the prefix that you provide in the parameters for the template.</span></span>

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

5. <span data-ttu-id="e458d-151">Agregue el recurso de red virtual.</span><span class="sxs-lookup"><span data-stu-id="e458d-151">Add the virtual network resource.</span></span> <span data-ttu-id="e458d-152">Consulte [Proveedor de recursos de red](../virtual-network/resource-groups-networking.md)para más información.</span><span class="sxs-lookup"><span data-stu-id="e458d-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="e458d-153">Agregue los recursos de dirección IP públicos que usan la interfaz de red y el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="e458d-153">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

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

7. <span data-ttu-id="e458d-154">Agregue el recurso de equilibrador de carga que usa el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="e458d-154">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="e458d-155">Para más información, consulte [Compatibilidad del Administrador de recursos de Azure con el equilibrador de carga](../load-balancer/load-balancer-arm.md)</span><span class="sxs-lookup"><span data-stu-id="e458d-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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

8. <span data-ttu-id="e458d-156">Agregue el recurso de interfaz de red que utiliza la máquina virtual independiente.</span><span class="sxs-lookup"><span data-stu-id="e458d-156">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="e458d-157">Dado que las máquinas de un conjunto de escalado no son accesibles mediante una dirección IP pública, se crea una máquina virtual independiente en la misma red virtual para tener acceso remoto a las máquinas.</span><span class="sxs-lookup"><span data-stu-id="e458d-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

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

9. <span data-ttu-id="e458d-158">Agregue la máquina virtual en la misma red que el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="e458d-158">Add the separate virtual machine in the same network as the scale set.</span></span>

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

10. <span data-ttu-id="e458d-159">Agregue el recurso de conjunto de escalado de máquinas virtuales y especifique la extensión de diagnóstico instalada en todas las máquinas virtuales del conjunto.</span><span class="sxs-lookup"><span data-stu-id="e458d-159">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="e458d-160">Muchos de los valores para este recurso son similares al recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e458d-160">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="e458d-161">Las principales diferencias son el elemento de capacidad, que especifica el número de máquinas virtuales del conjunto de escalado, y upgradePolicy, que especifica cómo se realizan las actualizaciones en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e458d-161">The main differences are the capacity element that specifies the number of virtual machines in the scale set, and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="e458d-162">El conjunto de escalado no se crea hasta que se crean todas las cuentas de almacenamiento como se especifica en el elemento dependsOn.</span><span class="sxs-lookup"><span data-stu-id="e458d-162">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

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

11. <span data-ttu-id="e458d-163">Agregue el recurso autoscaleSettings que define cómo el conjunto de escalado se ajusta según el uso del procesador en las máquinas del conjunto.</span><span class="sxs-lookup"><span data-stu-id="e458d-163">Add the autoscaleSettings resource that defines how the scale set adjusts based on the processor usage on the machines in the scale set.</span></span>

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

    <span data-ttu-id="e458d-164">Para este tutorial, destacan estos valores:</span><span class="sxs-lookup"><span data-stu-id="e458d-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="e458d-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="e458d-165">**metricName**</span></span>  
    <span data-ttu-id="e458d-166">Este valor es el mismo que el contador de rendimiento que definimos en la variable wadperfcounter.</span><span class="sxs-lookup"><span data-stu-id="e458d-166">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="e458d-167">Con esta variable, la extensión Diagnósticos recopila los datos del contador **Processor(_Total)\% Processor Time**.</span><span class="sxs-lookup"><span data-stu-id="e458d-167">Using that variable, the Diagnostics extension collects the  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="e458d-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="e458d-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="e458d-169">Este valor es el identificador de recursos del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e458d-169">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="e458d-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="e458d-170">**timeGrain**</span></span>  
    <span data-ttu-id="e458d-171">Este valor es la granularidad de las métricas que se recopilan.</span><span class="sxs-lookup"><span data-stu-id="e458d-171">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="e458d-172">En esta plantilla, se establece en un minuto.</span><span class="sxs-lookup"><span data-stu-id="e458d-172">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="e458d-173">**statistic**</span><span class="sxs-lookup"><span data-stu-id="e458d-173">**statistic**</span></span>  
    <span data-ttu-id="e458d-174">Este valor determina cómo se combinan las métricas para dar cabida a la acción de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="e458d-174">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="e458d-175">Los valores posibles son: Average, Min y Max.</span><span class="sxs-lookup"><span data-stu-id="e458d-175">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="e458d-176">En esta plantilla, se recopila el uso promedio total de CPU de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e458d-176">In this template, the average total CPU usage of the virtual machines is collected.</span></span>
    
    * <span data-ttu-id="e458d-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="e458d-177">**timeWindow**</span></span>  
    <span data-ttu-id="e458d-178">Este valor es el intervalo de tiempo durante el cual se recopilan los datos de instancia.</span><span class="sxs-lookup"><span data-stu-id="e458d-178">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="e458d-179">Debe estar comprendido entre 5 minutos y 12 horas.</span><span class="sxs-lookup"><span data-stu-id="e458d-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="e458d-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="e458d-180">**timeAggregation**</span></span>  
    <span data-ttu-id="e458d-181">Este valor determina la manera en que se deberían combinar los datos recopilados en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="e458d-181">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="e458d-182">El valor predeterminado es Average.</span><span class="sxs-lookup"><span data-stu-id="e458d-182">The default value is Average.</span></span> <span data-ttu-id="e458d-183">Los valores posibles son: Average, Minimum, Maximum, Last, Total, Count.</span><span class="sxs-lookup"><span data-stu-id="e458d-183">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="e458d-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="e458d-184">**operator**</span></span>  
    <span data-ttu-id="e458d-185">Este valor es el operador que se utiliza para comparar los datos de métrica y el umbral.</span><span class="sxs-lookup"><span data-stu-id="e458d-185">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="e458d-186">Los valores posibles son: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="e458d-186">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="e458d-187">**threshold**</span><span class="sxs-lookup"><span data-stu-id="e458d-187">**threshold**</span></span>  
    <span data-ttu-id="e458d-188">Este es el valor que desencadena la acción de escalado.</span><span class="sxs-lookup"><span data-stu-id="e458d-188">This value is the value that triggers the scale action.</span></span> <span data-ttu-id="e458d-189">En esta plantilla, los equipos se agregan al conjunto de escala que se establece cuando el uso promedio de CPU entre máquinas del conjunto es más de un 50%.</span><span class="sxs-lookup"><span data-stu-id="e458d-189">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="e458d-190">**dirección**</span><span class="sxs-lookup"><span data-stu-id="e458d-190">**direction**</span></span>  
    <span data-ttu-id="e458d-191">Este valor determina la acción que se realiza cuando se alcanza el valor de umbral.</span><span class="sxs-lookup"><span data-stu-id="e458d-191">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="e458d-192">Los valores posibles son Increase o Decrease.</span><span class="sxs-lookup"><span data-stu-id="e458d-192">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="e458d-193">En esta plantilla, se aumenta el número de máquinas virtuales en el conjunto de escala si el umbral es más de un 50% en la ventana de tiempo definido.</span><span class="sxs-lookup"><span data-stu-id="e458d-193">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>
    
    * <span data-ttu-id="e458d-194">**type**</span><span class="sxs-lookup"><span data-stu-id="e458d-194">**type**</span></span>  
    <span data-ttu-id="e458d-195">Este valor es el tipo de acción que debe realizarse y que se debe establecer en ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="e458d-195">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="e458d-196">**value**</span><span class="sxs-lookup"><span data-stu-id="e458d-196">**value**</span></span>  
    <span data-ttu-id="e458d-197">Este valor es el número de máquinas virtuales que se agregan o se quitan del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="e458d-197">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="e458d-198">Este valor debe ser 1 o un valor superior.</span><span class="sxs-lookup"><span data-stu-id="e458d-198">This value must be 1 or greater.</span></span> <span data-ttu-id="e458d-199">El valor predeterminado es 1.</span><span class="sxs-lookup"><span data-stu-id="e458d-199">The default value is 1.</span></span> <span data-ttu-id="e458d-200">En esta plantilla, el número de máquinas en el conjunto de escala aumenta en 1 cuando se alcanza el umbral.</span><span class="sxs-lookup"><span data-stu-id="e458d-200">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>
    
    * <span data-ttu-id="e458d-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="e458d-201">**cooldown**</span></span>  
    <span data-ttu-id="e458d-202">Este valor es la cantidad de tiempo de espera desde la última acción de escalado hasta antes de que se produzca la siguiente acción.</span><span class="sxs-lookup"><span data-stu-id="e458d-202">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="e458d-203">Debe estar comprendido entre un minuto y una semana.</span><span class="sxs-lookup"><span data-stu-id="e458d-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="e458d-204">Guarde el archivo de plantilla.</span><span class="sxs-lookup"><span data-stu-id="e458d-204">Save the template file.</span></span>    

## <a name="step-4-upload-the-template-to-storage"></a><span data-ttu-id="e458d-205">Paso 4: Carga de la plantilla en el almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e458d-205">Step 4: Upload the template to storage</span></span>
<span data-ttu-id="e458d-206">La plantilla se puede cargar siempre y cuando conozca el nombre de cuenta y la clave principal de la cuenta de almacenamiento que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="e458d-206">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="e458d-207">En la ventana de Microsoft Azure PowerShell, establezca una variable que especifique el nombre de la cuenta de almacenamiento que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="e458d-207">In the Microsoft Azure PowerShell window, set a variable that specifies the name of the storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="e458d-208">Establezca una variable que especifique la clave principal de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e458d-208">Set a variable that specifies the primary key of the storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="e458d-209">Puede obtener esta clave haciendo clic en el icono de llave al ver el recurso de la cuenta de almacenamiento en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e458d-209">You can get this key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span>
3. <span data-ttu-id="e458d-210">Cree el objeto de contexto de la cuenta de almacenamiento que se usa para validar las operaciones con la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e458d-210">Create the storage account context object that is used to validate operations with the storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="e458d-211">Cree el contenedor para almacenar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="e458d-211">Create the container for storing the template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="e458d-212">Cargue el archivo de plantillas en el nuevo contenedor.</span><span class="sxs-lookup"><span data-stu-id="e458d-212">Upload the template file to the new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-the-template"></a><span data-ttu-id="e458d-213">Paso 5: Implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="e458d-213">Step 5: Deploy the template</span></span>
<span data-ttu-id="e458d-214">Ahora que ha creado la plantilla, puede empezar a implementar los recursos.</span><span class="sxs-lookup"><span data-stu-id="e458d-214">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="e458d-215">Use este comando para iniciar el proceso:</span><span class="sxs-lookup"><span data-stu-id="e458d-215">Use this command to start the process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="e458d-216">Cuando presione Entrar, se le pedirá que proporcione valores para las variables que asignó.</span><span class="sxs-lookup"><span data-stu-id="e458d-216">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="e458d-217">Proporcione estos valores:</span><span class="sxs-lookup"><span data-stu-id="e458d-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="e458d-218">Para que todos los recursos se implementen correctamente se tardará unos 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="e458d-218">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="e458d-219">También puede usar la capacidad del portal para implementar los recursos.</span><span class="sxs-lookup"><span data-stu-id="e458d-219">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="e458d-220">Utilice este vínculo: "https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template>"</span><span class="sxs-lookup"><span data-stu-id="e458d-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="e458d-221">Paso 6: Supervisión de recursos</span><span class="sxs-lookup"><span data-stu-id="e458d-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="e458d-222">Puede obtener información acerca de los conjuntos de escala de máquinas virtuales mediante estos métodos:</span><span class="sxs-lookup"><span data-stu-id="e458d-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="e458d-223">El portal de Azure: actualmente puede obtener una cantidad limitada de información mediante el portal.</span><span class="sxs-lookup"><span data-stu-id="e458d-223">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>
* <span data-ttu-id="e458d-224">[Explorador de recursos de Azure](https://resources.azure.com/) : es la mejor herramienta para explorar el estado actual del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="e458d-224">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="e458d-225">Siga esta ruta de acceso y debería ver la vista de instancia del conjunto de escala que creó:</span><span class="sxs-lookup"><span data-stu-id="e458d-225">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    <span data-ttu-id="e458d-226">Suscripciones > {su suscripción} > resourceGroups > vmsstestrg1 > proveedores > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span><span class="sxs-lookup"><span data-stu-id="e458d-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="e458d-227">Azure PowerShell: use este comando para más información:</span><span class="sxs-lookup"><span data-stu-id="e458d-227">Azure PowerShell - Use this command to get some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="e458d-228">O</span><span class="sxs-lookup"><span data-stu-id="e458d-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="e458d-229">Conéctese a la máquina virtual independiente igual que lo haría con cualquier otra máquina y podrá obtener acceso remoto a las máquinas virtuales del conjunto de escalado para supervisar los procesos individuales.</span><span class="sxs-lookup"><span data-stu-id="e458d-229">Connect to the separate virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="e458d-230">Una API de REST completa para más información acerca de los conjuntos de escala se puede encontrar en [Conjuntos de escala de máquinas virtuales](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="e458d-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-the-resources"></a><span data-ttu-id="e458d-231">Paso 7: Eliminación de recursos</span><span class="sxs-lookup"><span data-stu-id="e458d-231">Step 7: Remove the resources</span></span>
<span data-ttu-id="e458d-232">Dado que se le cobrará por los recursos utilizados en Azure, siempre es conveniente eliminar los recursos que ya no sean necesarios.</span><span class="sxs-lookup"><span data-stu-id="e458d-232">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="e458d-233">No es necesario eliminar por separado cada recurso de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e458d-233">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="e458d-234">Puede eliminar el grupo de recursos para que se eliminen automáticamente todos sus recursos.</span><span class="sxs-lookup"><span data-stu-id="e458d-234">You can delete the resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="e458d-235">Si desea mantener el grupo de recursos, puede eliminar solo el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="e458d-235">If you want to keep your resource group, you can delete the scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="e458d-236">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e458d-236">Next steps</span></span>
* <span data-ttu-id="e458d-237">Administre el conjunto de escalado que acaba de crear con la información de [Administración de máquinas de un conjunto de escalado de máquinas virtuales](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="e458d-237">Manage the scale set that you just created using the information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="e458d-238">Más información sobre el escalado vertical si consulta [Escalado automático vertical con conjuntos de escalado de máquinas virtuales](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span><span class="sxs-lookup"><span data-stu-id="e458d-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="e458d-239">Encuentre ejemplos de características de supervisión de Azure Monitor en [Ejemplos de inicio rápido de PowerShell de Azure Monitor](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e458d-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="e458d-240">Aprenda sobre las características de notificación en [Uso de acciones de escalado automático para enviar notificaciones de alerta por correo electrónico y Webhook en Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="e458d-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="e458d-241">Aprenda cómo [usar registros de auditoría para enviar notificaciones de alerta por correo electrónico y webhook en Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="e458d-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

