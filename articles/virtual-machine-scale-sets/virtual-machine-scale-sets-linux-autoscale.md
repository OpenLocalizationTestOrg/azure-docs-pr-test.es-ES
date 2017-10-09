---
title: "aaaAutoscale conjuntos de escalas de máquina Virtual de Linux | Documentos de Microsoft"
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
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="78f41-103">Escalado automático de máquinas de Linux en un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="78f41-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="78f41-104">Conjuntos de escalas de máquina virtual hacen más sencillo para usted toodeploy y administran máquinas virtuales idénticas como un conjunto.</span><span class="sxs-lookup"><span data-stu-id="78f41-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="78f41-105">Los conjuntos de escala proporcionan una capa de proceso altamente escalable y personalizable para aplicaciones de gran escala y admiten imágenes de la plataforma Windows, imágenes de la plataforma Linux, imágenes personalizadas y extensiones.</span><span class="sxs-lookup"><span data-stu-id="78f41-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="78f41-106">más información, consulte toolearn [información general de conjuntos de escala de máquina Virtual](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78f41-106">toolearn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="78f41-107">Este tutorial muestra cómo establece toocreate una escala de máquinas virtuales de Linux con la versión más reciente de Hola de Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="78f41-107">This tutorial shows you how toocreate a scale set of Linux virtual machines using hello latest version of Ubuntu Linux.</span></span> <span data-ttu-id="78f41-108">Hola también se muestra cómo establecer máquinas tooautomatically escala Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-108">hello tutorial also shows you how tooautomatically scale hello machines in hello set.</span></span> <span data-ttu-id="78f41-109">Crear escala de hello establecer y configurar el escalado mediante la creación de una plantilla de Azure Resource Manager e implementación mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="78f41-109">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="78f41-110">Para más información sobre las plantillas, consulte [Creación de plantillas del Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="78f41-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="78f41-111">toolearn más información acerca de escalado automático de conjuntos de escalado, consulte [el escalado automático y establece de la escala en la máquina Virtual](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78f41-111">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="78f41-112">En este tutorial, se implementa siguiente Hola recursos y extensiones:</span><span class="sxs-lookup"><span data-stu-id="78f41-112">In this tutorial, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="78f41-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="78f41-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="78f41-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="78f41-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="78f41-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="78f41-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="78f41-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="78f41-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="78f41-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="78f41-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="78f41-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="78f41-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="78f41-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="78f41-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="78f41-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="78f41-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="78f41-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="78f41-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="78f41-122">Para más información sobre los recursos de Resource Manager, consulte [Implementación mediante Azure Resource Manager frente al modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="78f41-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="78f41-123">Antes de empezar a trabajar con los pasos de hello en este tutorial, [instalar hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="78f41-123">Before you get started with hello steps in this tutorial, [install hello Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="78f41-124">Paso 1: Creación de un grupo de recursos y una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="78f41-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="78f41-125">**Inicie sesión en Azure tooMicrosoft**</span><span class="sxs-lookup"><span data-stu-id="78f41-125">**Sign in tooMicrosoft Azure**</span></span>  
<span data-ttu-id="78f41-126">En la interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema), cambiar el modo de administrador de tooResource y, a continuación, [iniciar sesión con su Id. de trabajo o escuela](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Siga las indicaciones de Hola para un tooyour de experiencia de inicio de sesión interactivo cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="78f41-126">In your command-line interface (Bash, Terminal, Command prompt), switch tooResource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow hello prompts for an interactive login experience tooyour Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="78f41-127">Si dispone de un trabajo o Id. de la escuela y no tiene habilitada la autenticación de dos factores, utilice `azure login -u` con toolog de Id. de hello en sin una sesión interactiva.</span><span class="sxs-lookup"><span data-stu-id="78f41-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with hello ID toolog in without an interactive session.</span></span> <span data-ttu-id="78f41-128">Si no tiene un identificador profesional o educativo, puede [crear uno desde su cuenta personal de Microsoft](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78f41-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="78f41-129">**Cree un grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="78f41-129">**Create a resource group**</span></span>  
<span data-ttu-id="78f41-130">Todos los recursos deben ser implementado tooa grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="78f41-130">All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="78f41-131">Para este tutorial, asigne el nombre de grupo de recursos de hello **vmsstest1**.</span><span class="sxs-lookup"><span data-stu-id="78f41-131">For this tutorial, name hello resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="78f41-132">**Implementar una cuenta de almacenamiento en el nuevo grupo de recursos Hola**</span><span class="sxs-lookup"><span data-stu-id="78f41-132">**Deploy a storage account into hello new resource group**</span></span>  
<span data-ttu-id="78f41-133">Esta cuenta de almacenamiento es donde se almacena la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-133">This storage account is where hello template is stored.</span></span> <span data-ttu-id="78f41-134">Cree una cuenta de almacenamiento denominada " **vmsstestsa**".</span><span class="sxs-lookup"><span data-stu-id="78f41-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a><span data-ttu-id="78f41-135">Paso 2: Crear plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="78f41-135">Step 2: Create hello template</span></span>
<span data-ttu-id="78f41-136">Una plantilla de Azure Resource Manager hace posible toodeploy y administrar recursos de Azure de forma conjunta mediante una descripción de JSON de recursos de Hola y parámetros de implementación asociados.</span><span class="sxs-lookup"><span data-stu-id="78f41-136">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="78f41-137">En su editor favorito, cree el archivo hello VMSSTemplate.json y agregue Hola inicial JSON toosupport Hola plantilla de la estructura.</span><span class="sxs-lookup"><span data-stu-id="78f41-137">In your favorite editor, create hello file VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="78f41-138">Parámetros no son siempre obligatorios, pero proporcionan una manera tooinput valores cuando se implementa la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-138">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="78f41-139">Agregue estos parámetros en el elemento primario Hola parámetros que agregó toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="78f41-139">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="78f41-140">Un nombre para la máquina virtual independiente hello tooaccess usado Hola máquinas en conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-140">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
   * <span data-ttu-id="78f41-141">Un nombre para la cuenta de almacenamiento de Hola donde se almacena la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-141">A name for hello storage account where hello template is stored.</span></span>
   * <span data-ttu-id="78f41-142">número de Hola de instancias de máquinas virtuales tooinitially crea en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-142">hello number of instances of virtual machines tooinitially create in hello scale set.</span></span>
   * <span data-ttu-id="78f41-143">Un nombre y una contraseña de cuenta de administrador de hello en máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-143">A name and password of hello administrator account on hello virtual machines.</span></span>
   * <span data-ttu-id="78f41-144">Establece un prefijo de nombre de los recursos de Hola que se crean la escala de hello toosupport.</span><span class="sxs-lookup"><span data-stu-id="78f41-144">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="78f41-145">Las variables pueden usarse en un valores toospecify de plantilla que se pueden cambiar con frecuencia o valores que necesitan toobe crean a partir de una combinación de valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="78f41-145">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="78f41-146">Agregue estas variables en el elemento primario Hola variables que agregó toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="78f41-146">Add these variables under hello variables parent element that you added toohello template.</span></span>

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

   * <span data-ttu-id="78f41-147">Los nombres DNS que se usan por hello interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="78f41-147">DNS names that are used by hello network interfaces.</span></span>
   * <span data-ttu-id="78f41-148">Hola nombres de las direcciones IP y los prefijos de red virtual de Hola y las subredes.</span><span class="sxs-lookup"><span data-stu-id="78f41-148">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
   * <span data-ttu-id="78f41-149">Hello nombres e identificadores de red virtual de hello, equilibrador de carga y las interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="78f41-149">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="78f41-150">Nombres de cuenta de almacenamiento para las cuentas de hello asociados a las máquinas de hello en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-150">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
   * <span data-ttu-id="78f41-151">Configuración de extensión de diagnóstico que se instala en máquinas virtuales de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-151">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="78f41-152">Para obtener más información acerca de la extensión de diagnósticos de hello, consulte [crear una máquina Virtual de Windows con la supervisión y diagnósticos mediante la plantilla de administrador de recursos de Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78f41-152">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="78f41-153">Agregar recurso de cuenta de almacenamiento de hello bajo el elemento primario Hola recursos que agregó toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="78f41-153">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="78f41-154">Esta plantilla utiliza un hello toocreate de bucle recomendada cinco cuentas de almacenamiento donde se almacenan los discos del sistema operativo hello y datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="78f41-154">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="78f41-155">Puede admitir este conjunto de cuentas de seguridad de máquinas virtuales de too100 en un conjunto de escala, que es el máximo actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-155">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="78f41-156">Cada cuenta de almacenamiento se denomina con un designador de letra que se definió en variables de hello combinadas con el sufijo de Hola que se proporciona en los parámetros de hello para la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-156">Each storage account is named with a letter designator that was defined in hello variables combined with hello suffix that you provide in hello parameters for hello template.</span></span>
   
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

5. <span data-ttu-id="78f41-157">Agregar recursos de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-157">Add hello virtual network resource.</span></span> <span data-ttu-id="78f41-158">Consulte [Proveedor de recursos de red](../virtual-network/resource-groups-networking.md)para más información.</span><span class="sxs-lookup"><span data-stu-id="78f41-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="78f41-159">Agregar Hola públicos recursos de dirección IP que se usan por hello equilibrador de carga y la interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="78f41-159">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="78f41-160">Agregar recurso de equilibrador de carga de hello utilizado por el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-160">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="78f41-161">Para más información, consulte [Compatibilidad del Administrador de recursos de Azure con el equilibrador de carga](../load-balancer/load-balancer-arm.md)</span><span class="sxs-lookup"><span data-stu-id="78f41-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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

8. <span data-ttu-id="78f41-162">Agregar recurso de interfaz de red de Hola que usa la máquina virtual independiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-162">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="78f41-163">Dado que las máquinas en un conjunto de escala no están accesibles a través de una dirección IP pública, una máquina virtual independiente se crea en Hola mismo virtual máquinas Hola de tooremotely acceso de red.</span><span class="sxs-lookup"><span data-stu-id="78f41-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="78f41-164">Agregar máquina virtual independiente que Hola Hola misma red que el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-164">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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

10. <span data-ttu-id="78f41-165">Agregar el recurso de conjunto de escalas de máquina virtual de Hola y especifique la extensión de diagnósticos de Hola que está instalado en todas las máquinas virtuales en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-165">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="78f41-166">Muchos de los valores de hello para este recurso son similares con el recurso de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-166">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="78f41-167">Hola principales diferencias son elementos de la capacidad de Hola que especifica el número de Hola de máquinas virtuales en el conjunto de escalas de Hola y upgradePolicy que especifica cómo se realizan las actualizaciones toovirtual máquinas.</span><span class="sxs-lookup"><span data-stu-id="78f41-167">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="78f41-168">Hello conjunto de escala no se crea hasta que se crean todas las cuentas de almacenamiento de hello según se haya especificado con el elemento dependsOn de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-168">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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

11. <span data-ttu-id="78f41-169">Agregue hello autoscaleSettings recurso que define cómo se ajusta según el uso de procesador en máquinas de hello en el conjunto de Hola Hola conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="78f41-169">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on processor usage on hello machines in hello set.</span></span>

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
    
    <span data-ttu-id="78f41-170">Para este tutorial, destacan estos valores:</span><span class="sxs-lookup"><span data-stu-id="78f41-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="78f41-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="78f41-171">**metricName**</span></span>  
    <span data-ttu-id="78f41-172">Este valor es Hola igual que el contador de rendimiento de Hola que hemos definido en la variable de wadperfcounter Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-172">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="78f41-173">Con esa variable, extensión de diagnósticos de hello recopila hello **Processor\PercentProcessorTime** contador.</span><span class="sxs-lookup"><span data-stu-id="78f41-173">Using that variable, hello Diagnostics extension collects hello **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="78f41-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="78f41-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="78f41-175">Este valor es el identificador de recurso de hello del conjunto de escalas de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-175">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="78f41-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="78f41-176">**timeGrain**</span></span>  
    <span data-ttu-id="78f41-177">Este valor es la granularidad de Hola de métricas de Hola que se recopilan.</span><span class="sxs-lookup"><span data-stu-id="78f41-177">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="78f41-178">En esta plantilla, se establece tooone minuto.</span><span class="sxs-lookup"><span data-stu-id="78f41-178">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="78f41-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="78f41-179">**statistic**</span></span>  
    <span data-ttu-id="78f41-180">Este valor determina la forma métricas Hola Hola combinado tooaccommodate acción de escala automática.</span><span class="sxs-lookup"><span data-stu-id="78f41-180">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="78f41-181">Hola los valores posibles son: Average, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="78f41-181">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="78f41-182">En esta plantilla, se recopila Hola promedio uso total de CPU de las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-182">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>

    * <span data-ttu-id="78f41-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="78f41-183">**timeWindow**</span></span>  
    <span data-ttu-id="78f41-184">Este valor es Hola intervalo de tiempo en el que se recopilan datos de instancia.</span><span class="sxs-lookup"><span data-stu-id="78f41-184">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="78f41-185">Debe estar comprendido entre 5 minutos y 12 horas.</span><span class="sxs-lookup"><span data-stu-id="78f41-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="78f41-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="78f41-186">**timeAggregation**</span></span>  
    <span data-ttu-id="78f41-187">su valor determina cómo se deben combinar los datos de Hola que se recopilan con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="78f41-187">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="78f41-188">valor predeterminado de Hello es Media.</span><span class="sxs-lookup"><span data-stu-id="78f41-188">hello default value is Average.</span></span> <span data-ttu-id="78f41-189">Hola los valores posibles son: promedio, mínimo, máximo, último, Total, recuento.</span><span class="sxs-lookup"><span data-stu-id="78f41-189">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="78f41-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="78f41-190">**operator**</span></span>  
    <span data-ttu-id="78f41-191">Este valor es el operador de Hola que es usado toocompare Hola hello y datos de umbral de métrica.</span><span class="sxs-lookup"><span data-stu-id="78f41-191">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="78f41-192">Hola los valores posibles son: es igual a, valores, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="78f41-192">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="78f41-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="78f41-193">**threshold**</span></span>  
    <span data-ttu-id="78f41-194">Este valor desencadena la acción de escalado de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-194">This value triggers hello scale action.</span></span> <span data-ttu-id="78f41-195">En esta plantilla, las máquinas se agregan escala toohello establecer una vez Hola uso de la CPU entre máquinas en conjunto hello más de 50%.</span><span class="sxs-lookup"><span data-stu-id="78f41-195">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="78f41-196">**dirección**</span><span class="sxs-lookup"><span data-stu-id="78f41-196">**direction**</span></span>  
    <span data-ttu-id="78f41-197">Este valor determina la acción de Hola que se realiza cuando se obtiene el valor de umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-197">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="78f41-198">valores posibles de Hello son aumentan o disminuyen.</span><span class="sxs-lookup"><span data-stu-id="78f41-198">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="78f41-199">En esta plantilla, hello número de máquinas virtuales en el conjunto de escalas de hello aumenta si el umbral de hello es más de 50% en el período de tiempo de hello definido.</span><span class="sxs-lookup"><span data-stu-id="78f41-199">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>

    * <span data-ttu-id="78f41-200">**type**</span><span class="sxs-lookup"><span data-stu-id="78f41-200">**type**</span></span>  
    <span data-ttu-id="78f41-201">Este valor es el tipo de Hola de acción que se realizarán y se debe establecer tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="78f41-201">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="78f41-202">**value**</span><span class="sxs-lookup"><span data-stu-id="78f41-202">**value**</span></span>  
    <span data-ttu-id="78f41-203">Este valor es el número de Hola de máquinas virtuales que se agregan o quitan del conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-203">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="78f41-204">Este valor debe ser 1 o un valor superior.</span><span class="sxs-lookup"><span data-stu-id="78f41-204">This value must be 1 or greater.</span></span> <span data-ttu-id="78f41-205">valor predeterminado de Hello es 1.</span><span class="sxs-lookup"><span data-stu-id="78f41-205">hello default value is 1.</span></span> <span data-ttu-id="78f41-206">En esta plantilla, Hola establece número de máquinas en escala de hello aumenta 1 cuando se alcanza el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-206">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>

    * <span data-ttu-id="78f41-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="78f41-207">**cooldown**</span></span>  
    <span data-ttu-id="78f41-208">Este valor es cantidad de Hola de toowait de tiempo desde la última acción de escalado de hello antes de que se produce la acción siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-208">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="78f41-209">Debe estar comprendido entre un minuto y una semana.</span><span class="sxs-lookup"><span data-stu-id="78f41-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="78f41-210">Guarde el archivo de plantilla de hello.</span><span class="sxs-lookup"><span data-stu-id="78f41-210">Save hello template file.</span></span>    

## <a name="step-3-upload-hello-template-toostorage"></a><span data-ttu-id="78f41-211">Paso 3: Cargar Hola plantilla toostorage</span><span class="sxs-lookup"><span data-stu-id="78f41-211">Step 3: Upload hello template toostorage</span></span>
<span data-ttu-id="78f41-212">plantilla de Hola se puede cargar como sabe hello y clave principal de la cuenta de almacenamiento de Hola que creó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="78f41-212">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="78f41-213">En la interfaz de línea de comandos (intensiva de errores, Terminal, símbolo del sistema), ejecutar estos comandos tooset variables de entorno de hello necesarios tooaccess Hola cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="78f41-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands tooset hello environment variables needed tooaccess hello storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="78f41-214">Puede obtener la clave de hello haciendo clic en un icono de llave Hola al ver los recursos de cuenta de almacenamiento de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="78f41-214">You can get hello key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span> <span data-ttu-id="78f41-215">Cuando use un símbolo del sistema de Windows, escriba **set** en lugar de export.</span><span class="sxs-lookup"><span data-stu-id="78f41-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="78f41-216">Crear contenedor de Hola para almacenar la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-216">Create hello container for storing hello template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="78f41-217">Cargar nuevo contenedor toohello del archivo de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-217">Upload hello template file toohello new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a><span data-ttu-id="78f41-218">Paso 4: Implementar la plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="78f41-218">Step 4: Deploy hello template</span></span>
<span data-ttu-id="78f41-219">Ahora que ha creado la plantilla de hello, puede empezar a implementar los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-219">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="78f41-220">Utilice este proceso de hello toostart de comando:</span><span class="sxs-lookup"><span data-stu-id="78f41-220">Use this command toostart hello process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="78f41-221">Cuando se presiona escriba, son valores tooprovide solicitadas para las variables de Hola que asignó.</span><span class="sxs-lookup"><span data-stu-id="78f41-221">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="78f41-222">Proporcione estos valores:</span><span class="sxs-lookup"><span data-stu-id="78f41-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="78f41-223">Para implementar todos los toosuccessfully de recursos de hello tardará aproximadamente 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="78f41-223">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="78f41-224">También puede usar recursos del portal de hello capacidad toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-224">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="78f41-225">Use este vínculo: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="78f41-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="78f41-226">Paso 5: Supervisión de recursos</span><span class="sxs-lookup"><span data-stu-id="78f41-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="78f41-227">Puede obtener información acerca de los conjuntos de escala de máquinas virtuales mediante estos métodos:</span><span class="sxs-lookup"><span data-stu-id="78f41-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="78f41-228">Hola portal de Azure: actualmente, puede obtener una cantidad limitada de información mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="78f41-228">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="78f41-229">Hola [Explorador de recursos de Azure](https://resources.azure.com/) -esta herramienta es más adecuado para explorar el estado actual de Hola de su conjunto de escalas de hello.</span><span class="sxs-lookup"><span data-stu-id="78f41-229">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="78f41-230">Siga esta ruta de acceso y debería ver la vista de instancia de Hola de escala de hello establecido que creó:</span><span class="sxs-lookup"><span data-stu-id="78f41-230">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="78f41-231">CLI de Azure - usar este comando tooget cierta información:</span><span class="sxs-lookup"><span data-stu-id="78f41-231">Azure CLI - Use this command tooget some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="78f41-232">Conectar máquina virtual de toohello jumpbox tal como lo haría con cualquier otro equipo y, a continuación, se pueden obtener acceso remoto a máquinas virtuales de hello en procesos individuales de hello escala conjunto toomonitor.</span><span class="sxs-lookup"><span data-stu-id="78f41-232">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="78f41-233">Una API de REST completa para obtener más información sobre los conjuntos de escala se puede encontrar en [Conjuntos de escala de máquinas virtuales](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="78f41-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-hello-resources"></a><span data-ttu-id="78f41-234">Paso 6: Quitar recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="78f41-234">Step 6: Remove hello resources</span></span>
<span data-ttu-id="78f41-235">Dado que se le cobra por recursos que usa en Azure, siempre es un recursos toodelete recomendable que ya no son necesarios.</span><span class="sxs-lookup"><span data-stu-id="78f41-235">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="78f41-236">No es necesario toodelete cada recurso por separado de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="78f41-236">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="78f41-237">Puede eliminar el grupo de recursos de Hola y todos sus recursos se eliminan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="78f41-237">You can delete hello resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="78f41-238">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78f41-238">Next steps</span></span>
* <span data-ttu-id="78f41-239">Encuentre ejemplos de las características de supervisión de Azure Monitor en [Ejemplos de inicio rápido de CLI multiplataforma de Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="78f41-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="78f41-240">Obtenga información sobre las características de notificación de [usar escalado automático acciones toosend correo electrónico y webhook notificaciones de alerta en el Monitor de Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="78f41-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="78f41-241">Obtenga información acerca de cómo demasiado[toosend webhook y correo electrónico notificaciones de alerta de registros de auditoría de uso en el Monitor de Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="78f41-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="78f41-242">Extraer del repositorio hello [aplicación de demostración de escalado automático en Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) plantilla que configura un hello tooexercise de aplicación de Python/bottle automática de ajuste de escala en la funcionalidad de los conjuntos de la escala en la máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="78f41-242">Check out hello [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app tooexercise hello automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

