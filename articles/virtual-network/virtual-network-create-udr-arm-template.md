---
title: Control del enrutamiento y las aplicaciones virtuales en Azure | Microsoft Docs
description: Aprenda a controlar el enrutamiento y las aplicaciones virtuales con una plantilla de Azure Resource Manager.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 832c7831-d0e9-449b-b39c-9a09ba051531
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: b2c962d5449d18b51cfd84b0e1992695b54d1c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-a-template"></a><span data-ttu-id="2190a-103">Creación de rutas definidas por el usuario (UDR) con una plantilla</span><span class="sxs-lookup"><span data-stu-id="2190a-103">Create User-Defined Routes (UDR) using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2190a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2190a-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="2190a-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2190a-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="2190a-106">Plantilla</span><span class="sxs-lookup"><span data-stu-id="2190a-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="2190a-107">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="2190a-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="2190a-108">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="2190a-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

> [!IMPORTANT]
> <span data-ttu-id="2190a-109">Antes de trabajar con recursos de Azure, es importante comprender que Azure tiene actualmente dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="2190a-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="2190a-110">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-resource-manager/resource-manager-deployment-model.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2190a-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="2190a-111">Puede ver la documentación de las distintas herramientas haciendo clic en las fichas en la parte superior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2190a-111">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="2190a-112">Este artículo trata sobre el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="2190a-112">This article covers the Resource Manager deployment model.</span></span> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

## <a name="udr-resources-in-a-template-file"></a><span data-ttu-id="2190a-113">Recursos de las rutas definidas por el usuario en un archivo de plantilla</span><span class="sxs-lookup"><span data-stu-id="2190a-113">UDR resources in a template file</span></span>
<span data-ttu-id="2190a-114">Puede ver y descargar la [plantilla de ejemplo](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR).</span><span class="sxs-lookup"><span data-stu-id="2190a-114">You can view and download the [sample template](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR).</span></span>

<span data-ttu-id="2190a-115">En la sección siguiente se muestra la definición de las rutas definidas por el usuario (UDR) de front-end en el archivo **azuredeploy-vnet-nsg-udr.json** para el escenario:</span><span class="sxs-lookup"><span data-stu-id="2190a-115">The following section shows the definition of the front-end UDR in the **azuredeploy-vnet-nsg-udr.json** file for the scenario:</span></span>

    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/routeTables",
    "name": "[parameters('frontEndRouteTableName')]",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "UDR - FrontEnd"   
    },
    "properties": {
      "routes": [
        {
          "name": "RouteToBackEnd",
          "properties": {
            "addressPrefix": "[parameters('backEndSubnetPrefix')]",
            "nextHopType": "VirtualAppliance",
            "nextHopIpAddress": "[parameters('vmaIpAddress')]"
          }
        }
      ]

<span data-ttu-id="2190a-116">Para asociar las rutas definidas por el usuario a la subred front-end, debe cambiar la definición de la subred en la plantilla y usar el identificador de referencia para la ruta definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="2190a-116">To associate the UDR to the front-end subnet, you have to change the subnet definition in the template, and use the reference id for the UDR.</span></span>

    "subnets": [
        "name": "[parameters('frontEndSubnetName')]",
        "properties": {
          "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
          },
          "routeTable": {
              "id": "[resourceId('Microsoft.Network/routeTables', parameters('frontEndRouteTableName'))]"
          }
        },

<span data-ttu-id="2190a-117">Se hace lo mismo para el grupo de seguridad de red de back-end y la subred back-end en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="2190a-117">Notice the same being done for the back-end NSG and the back-end subnet in the template.</span></span>

<span data-ttu-id="2190a-118">También debe asegurarse de que la máquina virtual **FW1** tiene la propiedad de reenvío de IP habilitada en la NIC, que se usará para recibir y reenviar paquetes.</span><span class="sxs-lookup"><span data-stu-id="2190a-118">You also need to ensure that the **FW1** VM has the IP forwarding property enabled on the NIC that will be used to receive and forward packets.</span></span> <span data-ttu-id="2190a-119">La sección siguiente muestra la definición de la NIC para FW1 en el archivo azuredeploy-nsg-udr.json, según el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="2190a-119">The section below shows the definition of the NIC for FW1 in the azuredeploy-nsg-udr.json file, based on the scenario above.</span></span>

    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DMZ"
    },
    "name": "[concat(variables('fwVMSettings').nicName, copyindex(1))]",
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('fwVMSettings').pipName, copyindex(1))]",
      "[concat('Microsoft.Resources/deployments/', 'vnetTemplate')]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "enableIPForwarding": true,
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat('192.168.0.',copyindex(4))]",
            "publicIPAddress": {
              "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('fwVMSettings').pipName, copyindex(1)))]"
            },
            "subnet": {
              "id": "[variables('dmzSubnetRef')]"
            }
          }
        }
      ]
    },
    "copy": {
      "name": "fwniccount",
      "count": "[parameters('fwCount')]"
    }

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="2190a-120">Implementar la plantilla por medio de un solo clic para implementar</span><span class="sxs-lookup"><span data-stu-id="2190a-120">Deploy the template by using click to deploy</span></span>
<span data-ttu-id="2190a-121">La plantilla de ejemplo disponible en el repositorio público usa un archivo de parámetros que contiene los valores predeterminados utilizados para generar el escenario descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2190a-121">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="2190a-122">Para implementar esta plantilla mediante el método de hacer clic para implementar, siga [esta plantilla](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR), haga clic en **Implementar en Azure**, reemplace los valores de parámetro predeterminados si es necesario y siga las instrucciones del portal.</span><span class="sxs-lookup"><span data-stu-id="2190a-122">To deploy this template using click to deploy, follow [this link](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

1. <span data-ttu-id="2190a-123">Si es la primera vez que usa Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) y siga las instrucciones hasta el final para iniciar sesión en Azure y seleccionar su suscripción.</span><span class="sxs-lookup"><span data-stu-id="2190a-123">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="2190a-124">Ejecute el comando siguiente para crear un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="2190a-124">Run the following command to create a resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location westus
    ```

3. <span data-ttu-id="2190a-125">Ejecute el siguiente comando para implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="2190a-125">Run the following command to deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployUDR -ResourceGroupName TestRG `
        -TemplateUri https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.parameters.json
    ```

    <span data-ttu-id="2190a-126">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="2190a-126">Expected output:</span></span>
   
        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              : 
        Permissions       : 
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         : 
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            ASFW                Microsoft.Compute/availabilitySets       westus  
                            ASSQL               Microsoft.Compute/availabilitySets       westus  
                            ASWEB               Microsoft.Compute/availabilitySets       westus  
                            FW1                 Microsoft.Compute/virtualMachines        westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            WEB1                Microsoft.Compute/virtualMachines        westus  
                            WEB2                Microsoft.Compute/virtualMachines        westus  
                            NICFW1              Microsoft.Network/networkInterfaces      westus  
                            NICSQL1             Microsoft.Network/networkInterfaces      westus  
                            NICSQL2             Microsoft.Network/networkInterfaces      westus  
                            NICWEB1             Microsoft.Network/networkInterfaces      westus  
                            NICWEB2             Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            PIPFW1              Microsoft.Network/publicIPAddresses      westus  
                            PIPSQL1             Microsoft.Network/publicIPAddresses      westus  
                            PIPSQL2             Microsoft.Network/publicIPAddresses      westus  
                            PIPWEB1             Microsoft.Network/publicIPAddresses      westus  
                            PIPWEB2             Microsoft.Network/publicIPAddresses      westus  
                            UDR-BackEnd         Microsoft.Network/routeTables            westus  
                            UDR-FrontEnd        Microsoft.Network/routeTables            westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus

        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="2190a-127">Implementación la plantilla ARM mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2190a-127">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="2190a-128">Para implementar la plantilla de ARM mediante la CLI de Azure, complete los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2190a-128">To deploy the ARM template by using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="2190a-129">Si nunca ha usado la CLI de Azure, consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md) y siga las instrucciones hasta el punto donde deba seleccionar su cuenta y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2190a-129">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="2190a-130">Ejecute el siguiente comando para cambiar al modo de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="2190a-130">Run the following command to switch to Resource Manager mode:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="2190a-131">Este es el resultado esperado del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="2190a-131">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="2190a-132">En el explorador, vaya a **https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.parameters.json**, copie el contenido del archivo json y péguelo en un archivo nuevo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2190a-132">From your browser, navigate to **https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.parameters.json**, copy the contents of the json file, and paste into a new file in your computer.</span></span> <span data-ttu-id="2190a-133">En este escenario, va a copiar los valores siguientes en un archivo denominado **c:\udr\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="2190a-133">For this scenario, you would be copying the values below to a file named **c:\udr\azuredeploy.parameters.json**.</span></span>

    ```json
        {
          "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "fwCount": {
              "value": 1
            },
            "webCount": {
              "value": 2
            },
            "sqlCount": {
              "value": 2
            }
          }
        }
    ```

4. <span data-ttu-id="2190a-134">Ejecute el siguiente comando para implementar la nueva red virtual mediante la plantilla y los archivos de parámetros que descargó y modificó antes:</span><span class="sxs-lookup"><span data-stu-id="2190a-134">Run the following command to deploy the new VNet by using the template and parameter files you downloaded and modified above:</span></span>

    ```azurecli
    azure group create -n TestRG -l westus --template-uri 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.json' -e 'c:\udr\azuredeploy.parameters.json'
    ```

    <span data-ttu-id="2190a-135">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="2190a-135">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Updating resource group TestRG
        info:    Updated resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription Id]/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK

5. <span data-ttu-id="2190a-136">Ejecute el siguiente comando para ver los recursos creados en el nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="2190a-136">Run the following command to view the resources created in the new resource group:</span></span>

    ```azurecli
    azure group show TestRG
    ```

    <span data-ttu-id="2190a-137">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="2190a-137">Expected result:</span></span>

            info:    Executing command group show
            info:    Listing resource groups
            info:    Listing resources for the group
            data:    Id:                  /subscriptions/[Subscription Id]/resourceGroups/TestRG
            data:    Name:                TestRG
            data:    Location:            westus
            data:    Provisioning State:  Succeeded
            data:    Tags: null
            data:    Resources:
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/availabilitySets/ASFW
            data:      Name    : ASFW
            data:      Type    : availabilitySets
            data:      Location: westus
            data:      Tags    : displayName=AvailabilitySet - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/availabilitySets/ASSQL
            data:      Name    : ASSQL
            data:      Type    : availabilitySets
            data:      Location: westus
            data:      Tags    : displayName=AvailabilitySet - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/availabilitySets/ASWEB
            data:      Name    : ASWEB
            data:      Type    : availabilitySets
            data:      Location: westus
            data:      Tags    : displayName=AvailabilitySet - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1
            data:      Name    : FW1
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/SQL1
            data:      Name    : SQL1
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/SQL2
            data:      Name    : SQL2
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WEB1
            data:      Name    : WEB1
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WEB2
            data:      Name    : WEB2
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
                data:      Name    : NICFW1
        data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1
            data:      Name    : NICSQL1
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2
            data:      Name    : NICSQL2
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1
            data:      Name    : NICWEB1
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2
            data:      Name    : NICWEB2
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd
            data:      Name    : NSG-BackEnd
            data:      Type    : networkSecurityGroups
            data:      Location: westus
            data:      Tags    : displayName=NSG - Front End
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
            data:      Name    : NSG-FrontEnd
            data:      Type    : networkSecurityGroups
            data:      Location: westus
            data:      Tags    : displayName=NSG - Remote Access
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1
            data:      Name    : PIPFW1
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPSQL1
            data:      Name    : PIPSQL1
                data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPSQL2
            data:      Name    : PIPSQL2
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPWEB1
            data:      Name    : PIPWEB1
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPWEB2
            data:      Name    : PIPWEB2
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd
            data:      Name    : UDR-BackEnd
            data:      Type    : routeTables
            data:      Location: westus
            data:      Tags    : displayName=Route Table - Back End
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd
            data:      Name    : UDR-FrontEnd
            data:      Type    : routeTables
            data:      Location: westus
            data:      Tags    : displayName=UDR - FrontEnd
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
            data:      Name    : TestVNet
            data:      Type    : virtualNetworks
            data:      Location: westus
            data:      Tags    : displayName=VNet
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Storage/storageAccounts/testvnetstorageprm
            data:      Name    : testvnetstorageprm
            data:      Type    : storageAccounts
            data:      Location: westus
            data:      Tags    : displayName=Storage Account - Premium
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Storage/storageAccounts/testvnetstoragestd
            data:      Name    : testvnetstoragestd
            data:      Type    : storageAccounts
            data:      Location: westus
            data:      Tags    : displayName=Storage Account - Simple
            data:    
            data:    Permissions:
            data:      Actions: *
            data:      NotActions: 
            data:
            info:    group show command OK

> [!TIP]
> <span data-ttu-id="2190a-138">Si no ve todos los recursos, ejecute el comando `azure group deployment show` para asegurarse de que el estado de aprovisionamiento de la implementación sea *Correcto*.</span><span class="sxs-lookup"><span data-stu-id="2190a-138">If you do not see all the resources, run the `azure group deployment show` command to ensure the provisioning state of the deployment is *Succeded*.</span></span>
> 
