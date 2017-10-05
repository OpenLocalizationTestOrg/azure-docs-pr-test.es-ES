---
title: "Escalado automático de conjuntos de escalado de máquinas virtuales Linux | Microsoft Docs"
description: "Configuración del escalado automático para un conjunto de escalado de máquinas virtuales Linux mediante la CLI de Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: eff4add1cb16fe25022787668dc1d2277845dd95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="37953-103">Escalado automático de máquinas de Linux en un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="37953-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="37953-104">Los conjuntos de escalado de máquinas virtuales facilitan la implementación y administración de máquinas virtuales idénticas como conjunto.</span><span class="sxs-lookup"><span data-stu-id="37953-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="37953-105">Los conjuntos de escala proporcionan una capa de proceso altamente escalable y personalizable para aplicaciones de gran escala y admiten imágenes de la plataforma Windows, imágenes de la plataforma Linux, imágenes personalizadas y extensiones.</span><span class="sxs-lookup"><span data-stu-id="37953-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="37953-106">Para obtener más información, consulte [Virtual Machine Scale Sets Overview (Información general de conjuntos de escalado de máquinas virtuales)](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37953-106">To learn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="37953-107">En este tutorial se muestra cómo crear un conjunto de escalado de máquinas virtuales de Linux con la versión más reciente de Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="37953-107">This tutorial shows you how to create a scale set of Linux virtual machines using the latest version of Ubuntu Linux.</span></span> <span data-ttu-id="37953-108">En el tutorial también se muestra cómo escalar automáticamente las máquinas del conjunto.</span><span class="sxs-lookup"><span data-stu-id="37953-108">The tutorial also shows you how to automatically scale the machines in the set.</span></span> <span data-ttu-id="37953-109">El conjunto de escalado se crea y la configuración de escalado se configura mediante la creación de una plantilla de Azure Resource Manager que se implementa con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="37953-109">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="37953-110">Para más información sobre las plantillas, consulte [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="37953-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="37953-111">Para obtener más información sobre el escalado automático de conjuntos de escalado, consulte [Automatic scaling and Virtual Machine Scale Sets (Escalado automático y conjuntos de escalado de máquinas virtuales)](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37953-111">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="37953-112">En este tutorial, implemente los recursos y las extensiones siguientes:</span><span class="sxs-lookup"><span data-stu-id="37953-112">In this tutorial, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="37953-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="37953-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="37953-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="37953-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="37953-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="37953-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="37953-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="37953-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="37953-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="37953-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="37953-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="37953-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="37953-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="37953-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="37953-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="37953-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="37953-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="37953-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="37953-122">Para más información sobre los recursos de Resource Manager, consulte [Implementación mediante Azure Resource Manager frente al modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="37953-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="37953-123">Antes de empezar con los pasos de este tutorial, [instale la CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="37953-123">Before you get started with the steps in this tutorial, [install the Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="37953-124">Paso 1: Creación de un grupo de recursos y una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="37953-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="37953-125">**Inicie sesión en Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="37953-125">**Sign in to Microsoft Azure**</span></span>  
<span data-ttu-id="37953-126">En la interfaz de la línea de comandos (Bash, Terminal, símbolo del sistema), cambie al modo Resource Manager e [inicie sesión con su identificador profesional o educativo](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Siga las indicaciones para una experiencia de inicio de sesión interactiva a su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="37953-126">In your command-line interface (Bash, Terminal, Command prompt), switch to Resource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow the prompts for an interactive login experience to your Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="37953-127">Si tiene un identificador profesional o educativo y no tiene habilitada la autenticación en dos fases, use `azure login -u` junto con el identificador para iniciar sesión que no sea interactiva.</span><span class="sxs-lookup"><span data-stu-id="37953-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with the ID to log in without an interactive session.</span></span> <span data-ttu-id="37953-128">Si no tiene un identificador profesional o educativo, puede [crear uno desde su cuenta personal de Microsoft](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37953-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="37953-129">**Cree un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="37953-129">**Create a resource group**</span></span>  
<span data-ttu-id="37953-130">Todos los recursos se deben implementar en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="37953-130">All resources must be deployed to a resource group.</span></span> <span data-ttu-id="37953-131">Para este tutorial, asigne el nombre **vmsstest1**al grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="37953-131">For this tutorial, name the resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="37953-132">**Implemente una cuenta de almacenamiento en el nuevo grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="37953-132">**Deploy a storage account into the new resource group**</span></span>  
<span data-ttu-id="37953-133">La cuenta de almacenamiento es donde se almacena la plantilla.</span><span class="sxs-lookup"><span data-stu-id="37953-133">This storage account is where the template is stored.</span></span> <span data-ttu-id="37953-134">Cree una cuenta de almacenamiento denominada " **vmsstestsa**".</span><span class="sxs-lookup"><span data-stu-id="37953-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-the-template"></a><span data-ttu-id="37953-135">Paso 2: Creación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="37953-135">Step 2: Create the template</span></span>
<span data-ttu-id="37953-136">Las plantillas del Administrador de recursos de Azure le permiten implementar y administrar los distintos recursos de Azure en conjunto mediante una descripción de JSON de los recursos y los parámetros de implementación asociados.</span><span class="sxs-lookup"><span data-stu-id="37953-136">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="37953-137">En el editor que prefiera, cree el archivo VMSSTemplate.json y agregue la estructura inicial de JSON para admitir la plantilla.</span><span class="sxs-lookup"><span data-stu-id="37953-137">In your favorite editor, create the file VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

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

2. <span data-ttu-id="37953-138">No siempre se necesitan parámetros, pero proporcionan una manera de introducir valores al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="37953-138">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="37953-139">Agregue estos parámetros en el elemento primario de los parámetros que agregó a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="37953-139">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="37953-140">Un nombre para la máquina virtual independiente que se utiliza para tener acceso a las máquinas del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="37953-140">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
   * <span data-ttu-id="37953-141">Un nombre para la cuenta de almacenamiento donde se almacena la plantilla.</span><span class="sxs-lookup"><span data-stu-id="37953-141">A name for the storage account where the template is stored.</span></span>
   * <span data-ttu-id="37953-142">El número de instancias de máquinas virtuales para crear inicialmente en el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="37953-142">The number of instances of virtual machines to initially create in the scale set.</span></span>
   * <span data-ttu-id="37953-143">Un nombre y contraseña de la cuenta de administrador en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="37953-143">A name and password of the administrator account on the virtual machines.</span></span>
   * <span data-ttu-id="37953-144">Establece un prefijo de nombre de los recursos que se crean para admitir el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="37953-144">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="37953-145">Pueden usarse variables en una plantilla para especificar los valores que pueden cambiar con frecuencia o los valores que se deben crear a partir de una combinación de valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="37953-145">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="37953-146">Agregue estas variables en el elemento primario de las variables que agregó a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="37953-146">Add these variables under the variables parent element that you added to the template.</span></span>

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
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * <span data-ttu-id="37953-147">Nombres DNS que usan las interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="37953-147">DNS names that are used by the network interfaces.</span></span>
   * <span data-ttu-id="37953-148">Los nombres de direcciones IP y los prefijos para la red virtual y las subredes.</span><span class="sxs-lookup"><span data-stu-id="37953-148">The IP address names and prefixes for the virtual network and subnets.</span></span>
   * <span data-ttu-id="37953-149">Los nombres y los identificadores de la red virtual, el equilibrador de carga y las interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="37953-149">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="37953-150">Los nombres de cuentas de almacenamiento para las cuentas asociadas a las máquinas en el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="37953-150">Storage account names for the accounts associated with the machines in the scale set.</span></span>
   * <span data-ttu-id="37953-151">Configuración de la extensión de diagnósticos que se instala en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="37953-151">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="37953-152">Para más información sobre la extensión de diagnósticos, consulte [Crear una máquina virtual de Windows con supervisión y diagnóstico mediante la plantilla de Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="37953-152">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="37953-153">Agregue el recurso de la cuenta de almacenamiento en el elemento primario de recursos que agregó a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="37953-153">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="37953-154">Esta plantilla utiliza un bucle para crear las cinco cuentas de almacenamiento recomendadas donde se guardan los discos del sistema operativo y los datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="37953-154">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="37953-155">Este conjunto de cuentas puede admitir hasta 100 máquinas virtuales en un conjunto de escala, lo cual es el máximo actual.</span><span class="sxs-lookup"><span data-stu-id="37953-155">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="37953-156">Cada cuenta de almacenamiento se denomina con un indicador de letra, que se definió en las variables, y se combina con el sufijo que proporcionó en los parámetros de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="37953-156">Each storage account is named with a letter designator that was defined in the variables combined with the suffix that you provide in the parameters for the template.</span></span>
   
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

5. <span data-ttu-id="37953-157">Agregue el recurso de red virtual.</span><span class="sxs-lookup"><span data-stu-id="37953-157">Add the virtual network resource.</span></span> <span data-ttu-id="37953-158">Consulte [Proveedor de recursos de red](../virtual-network/resource-groups-networking.md)para más información.</span><span class="sxs-lookup"><span data-stu-id="37953-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="37953-159">Agregue los recursos de dirección IP públicos que usan la interfaz de red y el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="37953-159">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

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

7. <span data-ttu-id="37953-160">Agregue el recurso de equilibrador de carga que usa el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="37953-160">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="37953-161">Para más información, consulte [Compatibilidad del Administrador de recursos de Azure con el equilibrador de carga](../load-balancer/load-balancer-arm.md)</span><span class="sxs-lookup"><span data-stu-id="37953-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
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
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="37953-162">Agregue el recurso de interfaz de red que utiliza la máquina virtual independiente.</span><span class="sxs-lookup"><span data-stu-id="37953-162">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="37953-163">Dado que las máquinas de un conjunto de escalado no son accesibles mediante una dirección IP pública, se crea una máquina virtual independiente en la misma red virtual para tener acceso remoto a las máquinas.</span><span class="sxs-lookup"><span data-stu-id="37953-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

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

9. <span data-ttu-id="37953-164">Agregue la máquina virtual en la misma red que el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="37953-164">Add the separate virtual machine in the same network as the scale set.</span></span>

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
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
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

10. <span data-ttu-id="37953-165">Agregue el recurso de conjunto de escalado de máquinas virtuales y especifique la extensión de diagnóstico instalada en todas las máquinas virtuales del conjunto.</span><span class="sxs-lookup"><span data-stu-id="37953-165">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="37953-166">Muchos de los valores para este recurso son similares al recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="37953-166">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="37953-167">Las principales diferencias son el elemento de capacidad, que especifica el número de máquinas virtuales del conjunto de escalado, y upgradePolicy, que especifica cómo se realizan las actualizaciones en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="37953-167">The main differences are the capacity element that specifies the number of virtual machines in the scale set and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="37953-168">El conjunto de escalado no se crea hasta que se crean todas las cuentas de almacenamiento como se especifica en el elemento dependsOn.</span><span class="sxs-lookup"><span data-stu-id="37953-168">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

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
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
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
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="37953-169">Agregue el recurso autoscaleSettings que define cómo el conjunto de escala se ajusta según el uso del procesador en las máquinas del conjunto.</span><span class="sxs-lookup"><span data-stu-id="37953-169">Add the autoscaleSettings resource that defines how the scale set adjusts based on processor usage on the machines in the set.</span></span>

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
                  "metricName": "\\Processor\\PercentProcessorTime",
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
    
    <span data-ttu-id="37953-170">Para este tutorial, destacan estos valores:</span><span class="sxs-lookup"><span data-stu-id="37953-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="37953-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="37953-171">**metricName**</span></span>  
    <span data-ttu-id="37953-172">Este valor es el mismo que el contador de rendimiento que definimos en la variable wadperfcounter.</span><span class="sxs-lookup"><span data-stu-id="37953-172">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="37953-173">Con esta variable, la extensión Diagnósticos recopila los datos del contador **Processor\PercentProcessorTime**.</span><span class="sxs-lookup"><span data-stu-id="37953-173">Using that variable, the Diagnostics extension collects the **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="37953-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="37953-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="37953-175">Este valor es el identificador de recursos del conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="37953-175">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="37953-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="37953-176">**timeGrain**</span></span>  
    <span data-ttu-id="37953-177">Este valor es la granularidad de las métricas que se recopilan.</span><span class="sxs-lookup"><span data-stu-id="37953-177">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="37953-178">En esta plantilla, se establece en un minuto.</span><span class="sxs-lookup"><span data-stu-id="37953-178">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="37953-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="37953-179">**statistic**</span></span>  
    <span data-ttu-id="37953-180">Este valor determina cómo se combinan las métricas para dar cabida a la acción de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="37953-180">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="37953-181">Los valores posibles son: Average, Min y Max.</span><span class="sxs-lookup"><span data-stu-id="37953-181">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="37953-182">En esta plantilla, se recopila el uso promedio total de CPU de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="37953-182">In this template, the average total CPU usage of the virtual machines is collected.</span></span>

    * <span data-ttu-id="37953-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="37953-183">**timeWindow**</span></span>  
    <span data-ttu-id="37953-184">Este valor es el intervalo de tiempo durante el cual se recopilan los datos de instancia.</span><span class="sxs-lookup"><span data-stu-id="37953-184">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="37953-185">Debe estar comprendido entre 5 minutos y 12 horas.</span><span class="sxs-lookup"><span data-stu-id="37953-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="37953-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="37953-186">**timeAggregation**</span></span>  
    <span data-ttu-id="37953-187">Este valor determina la manera en que se deberían combinar los datos recopilados en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="37953-187">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="37953-188">El valor predeterminado es Average.</span><span class="sxs-lookup"><span data-stu-id="37953-188">The default value is Average.</span></span> <span data-ttu-id="37953-189">Los valores posibles son: Average, Minimum, Maximum, Last, Total, Count.</span><span class="sxs-lookup"><span data-stu-id="37953-189">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="37953-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="37953-190">**operator**</span></span>  
    <span data-ttu-id="37953-191">Este valor es el operador que se utiliza para comparar los datos de métrica y el umbral.</span><span class="sxs-lookup"><span data-stu-id="37953-191">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="37953-192">Los valores posibles son: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="37953-192">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="37953-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="37953-193">**threshold**</span></span>  
    <span data-ttu-id="37953-194">Este valor desencadena la acción de escalado.</span><span class="sxs-lookup"><span data-stu-id="37953-194">This value triggers the scale action.</span></span> <span data-ttu-id="37953-195">En esta plantilla, los equipos se agregan al conjunto de escala que se establece cuando el uso promedio de CPU entre máquinas del conjunto es más de un 50%.</span><span class="sxs-lookup"><span data-stu-id="37953-195">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="37953-196">**dirección**</span><span class="sxs-lookup"><span data-stu-id="37953-196">**direction**</span></span>  
    <span data-ttu-id="37953-197">Este valor determina la acción que se realiza cuando se alcanza el valor de umbral.</span><span class="sxs-lookup"><span data-stu-id="37953-197">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="37953-198">Los valores posibles son Increase o Decrease.</span><span class="sxs-lookup"><span data-stu-id="37953-198">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="37953-199">En esta plantilla, se aumenta el número de máquinas virtuales en el conjunto de escala si el umbral es más de un 50% en la ventana de tiempo definido.</span><span class="sxs-lookup"><span data-stu-id="37953-199">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>

    * <span data-ttu-id="37953-200">**type**</span><span class="sxs-lookup"><span data-stu-id="37953-200">**type**</span></span>  
    <span data-ttu-id="37953-201">Este valor es el tipo de acción que debe realizarse y que se debe establecer en ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="37953-201">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="37953-202">**value**</span><span class="sxs-lookup"><span data-stu-id="37953-202">**value**</span></span>  
    <span data-ttu-id="37953-203">Este valor es el número de máquinas virtuales que se agregan o se quitan del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="37953-203">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="37953-204">Este valor debe ser 1 o un valor superior.</span><span class="sxs-lookup"><span data-stu-id="37953-204">This value must be 1 or greater.</span></span> <span data-ttu-id="37953-205">El valor predeterminado es 1.</span><span class="sxs-lookup"><span data-stu-id="37953-205">The default value is 1.</span></span> <span data-ttu-id="37953-206">En esta plantilla, el número de máquinas en el conjunto de escala aumenta en 1 cuando se alcanza el umbral.</span><span class="sxs-lookup"><span data-stu-id="37953-206">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>

    * <span data-ttu-id="37953-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="37953-207">**cooldown**</span></span>  
    <span data-ttu-id="37953-208">Este valor es la cantidad de tiempo de espera desde la última acción de escalado hasta antes de que se produzca la siguiente acción.</span><span class="sxs-lookup"><span data-stu-id="37953-208">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="37953-209">Debe estar comprendido entre un minuto y una semana.</span><span class="sxs-lookup"><span data-stu-id="37953-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="37953-210">Guarde el archivo de plantilla.</span><span class="sxs-lookup"><span data-stu-id="37953-210">Save the template file.</span></span>    

## <a name="step-3-upload-the-template-to-storage"></a><span data-ttu-id="37953-211">Paso 3: Carga de la plantilla en el almacenamiento</span><span class="sxs-lookup"><span data-stu-id="37953-211">Step 3: Upload the template to storage</span></span>
<span data-ttu-id="37953-212">La plantilla se puede cargar siempre y cuando conozca el nombre de cuenta y la clave principal de la cuenta de almacenamiento que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="37953-212">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="37953-213">En la interfaz de línea de comandos (Bash, Terminal, símbolo del sistema), ejecute estos comandos para establecer las variables de entorno que se necesitan para acceder a la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="37953-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands to set the environment variables needed to access the storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="37953-214">Puede obtener la clave haciendo clic en el icono de llave al ver el recurso de la cuenta de almacenamiento en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="37953-214">You can get the key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span> <span data-ttu-id="37953-215">Cuando use un símbolo del sistema de Windows, escriba **set** en lugar de export.</span><span class="sxs-lookup"><span data-stu-id="37953-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="37953-216">Cree el contenedor para almacenar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="37953-216">Create the container for storing the template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="37953-217">Cargue el archivo de plantillas en el nuevo contenedor.</span><span class="sxs-lookup"><span data-stu-id="37953-217">Upload the template file to the new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-the-template"></a><span data-ttu-id="37953-218">Paso 4: Implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="37953-218">Step 4: Deploy the template</span></span>
<span data-ttu-id="37953-219">Ahora que ha creado la plantilla, puede empezar a implementar los recursos.</span><span class="sxs-lookup"><span data-stu-id="37953-219">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="37953-220">Use este comando para iniciar el proceso:</span><span class="sxs-lookup"><span data-stu-id="37953-220">Use this command to start the process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="37953-221">Cuando presione Entrar, se le pedirá que proporcione valores para las variables que asignó.</span><span class="sxs-lookup"><span data-stu-id="37953-221">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="37953-222">Proporcione estos valores:</span><span class="sxs-lookup"><span data-stu-id="37953-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="37953-223">Para que todos los recursos se implementen correctamente se tardará unos 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="37953-223">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="37953-224">También puede usar la capacidad del portal para implementar los recursos.</span><span class="sxs-lookup"><span data-stu-id="37953-224">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="37953-225">Use este vínculo: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="37953-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="37953-226">Paso 5: Supervisión de recursos</span><span class="sxs-lookup"><span data-stu-id="37953-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="37953-227">Puede obtener información acerca de los conjuntos de escala de máquinas virtuales mediante estos métodos:</span><span class="sxs-lookup"><span data-stu-id="37953-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="37953-228">El portal de Azure: actualmente puede obtener una cantidad limitada de información mediante el portal.</span><span class="sxs-lookup"><span data-stu-id="37953-228">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="37953-229">[Explorador de recursos de Azure](https://resources.azure.com/) : es la mejor herramienta para explorar el estado actual del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="37953-229">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="37953-230">Siga esta ruta de acceso y debería ver la vista de instancia del conjunto de escala que creó:</span><span class="sxs-lookup"><span data-stu-id="37953-230">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="37953-231">CLI de Azure. Use este comando para obtener información:</span><span class="sxs-lookup"><span data-stu-id="37953-231">Azure CLI - Use this command to get some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="37953-232">Conéctese a la máquina virtual de jumpbox igual que lo haría con cualquier otra máquina y, a continuación, podrá obtener acceso remoto a las máquinas virtuales del conjunto de escala para supervisar los procesos individuales.</span><span class="sxs-lookup"><span data-stu-id="37953-232">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="37953-233">Una API de REST completa para obtener más información sobre los conjuntos de escala se puede encontrar en [Conjuntos de escala de máquinas virtuales](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="37953-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-the-resources"></a><span data-ttu-id="37953-234">Paso 6: Eliminación de recursos</span><span class="sxs-lookup"><span data-stu-id="37953-234">Step 6: Remove the resources</span></span>
<span data-ttu-id="37953-235">Dado que se le cobrará por los recursos utilizados en Azure, siempre es conveniente eliminar los recursos que ya no sean necesarios.</span><span class="sxs-lookup"><span data-stu-id="37953-235">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="37953-236">No es necesario eliminar por separado cada recurso de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="37953-236">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="37953-237">Puede eliminar el grupo de recursos para que se eliminen automáticamente todos sus recursos.</span><span class="sxs-lookup"><span data-stu-id="37953-237">You can delete the resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="37953-238">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37953-238">Next steps</span></span>
* <span data-ttu-id="37953-239">Encuentre ejemplos de las características de supervisión de Azure Monitor en [Ejemplos de inicio rápido de CLI multiplataforma de Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="37953-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="37953-240">Aprenda sobre las características de notificación en [Uso de acciones de escalado automático para enviar notificaciones de alerta por correo electrónico y Webhook en Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="37953-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="37953-241">Aprenda cómo [usar registros de auditoría para enviar notificaciones de alerta por correo electrónico y webhook en Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="37953-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="37953-242">Consulte la plantilla de la [aplicación de demostración de la autoescala en Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale), en la que se configura una aplicación Python/bottle para practicar la funcionalidad de escalado automático de los conjuntos de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="37953-242">Check out the [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app to exercise the automatic scaling functionality of Virtual Machine Scale Sets.</span></span>
