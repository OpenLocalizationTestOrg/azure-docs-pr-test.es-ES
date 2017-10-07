---
title: "aaaCreate una máquina virtual con una dirección pública estática de IP - plantilla de Azure Resource Manager | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con una dirección IP pública estática direccionan usando una plantilla de Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="aa8e8-103">Creación de una máquina virtual con una dirección IP pública estática mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="aa8e8-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa8e8-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="aa8e8-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="aa8e8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa8e8-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="aa8e8-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="aa8e8-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="aa8e8-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="aa8e8-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="aa8e8-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="aa8e8-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="aa8e8-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="aa8e8-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="aa8e8-110">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="aa8e8-111">Recursos de dirección IP pública en un archivo de plantilla</span><span class="sxs-lookup"><span data-stu-id="aa8e8-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="aa8e8-112">Puede ver y descargar hello [plantilla de ejemplo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="aa8e8-112">You can view and download hello [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="aa8e8-113">Hello siguiente sección muestra hello definición de recurso IP público hello, basado en el escenario de hello anterior:</span><span class="sxs-lookup"><span data-stu-id="aa8e8-113">hello following section shows hello definition of hello public IP resource, based on hello scenario above:</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

<span data-ttu-id="aa8e8-114">Hola aviso **publicIPAllocationMethod** propiedad, que se establece demasiado*estático*.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-114">Notice hello **publicIPAllocationMethod** property, which is set too*Static*.</span></span> <span data-ttu-id="aa8e8-115">Esta propiedad puede ser *Dynamic* (valor predeterminado) o *Static*.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="aa8e8-116">Si se establece toostatic garantiza que nunca se cambiará la dirección IP pública Hola asignada.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-116">Setting it toostatic guarantees that hello public IP address assigned will never change.</span></span>

<span data-ttu-id="aa8e8-117">Hello siguiente sección muestra la asociación de Hola de dirección IP pública de hello con una interfaz de red:</span><span class="sxs-lookup"><span data-stu-id="aa8e8-117">hello following section shows hello association of hello public IP address with a network interface:</span></span>

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

<span data-ttu-id="aa8e8-118">Hola aviso **publicIPAddress** propiedad que señala toohello **identificador** de un recurso denominado **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-118">Notice hello **publicIPAddress** property pointing toohello **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="aa8e8-119">Que es el nombre de hello del recurso IP público Hola mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-119">That is hello name of hello public IP resource shown above.</span></span>

<span data-ttu-id="aa8e8-120">Por último, interfaz de red de hello anterior se muestra en hello **networkProfile** propiedad de hello VM que se está creando.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-120">Finally, hello network interface above is listed in hello **networkProfile** property of hello VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="aa8e8-121">Implementar la plantilla de hello mediante haga clic en toodeploy</span><span class="sxs-lookup"><span data-stu-id="aa8e8-121">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="aa8e8-122">plantilla de ejemplo Hola disponible en el repositorio público de hello usa un archivo de parámetros que contiene el escenario Hola predeterminada valores utilizados toogenerate Hola descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-122">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="aa8e8-123">toodeploy este uso de la plantilla, haga clic en toodeploy, haga clic en **implementar tooAzure** en archivo Readme.md Hola Hola [VM con PIP estático](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) plantilla.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-123">toodeploy this template using click toodeploy, click **Deploy tooAzure** in hello Readme.md file for hello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="aa8e8-124">Reemplace los valores de parámetro predeterminados Hola si lo desea y especifique valores para parámetros de hello en blanco.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-124">Replace hello default parameter values if desired and enter values for hello blank parameters.</span></span>  <span data-ttu-id="aa8e8-125">Siga las instrucciones de hello en hello portal toocreate una máquina virtual con una dirección IP pública estática.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-125">Follow hello instructions in hello portal toocreate a virtual machine with a static public IP address.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="aa8e8-126">Implementar la plantilla de hello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa8e8-126">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="aa8e8-127">plantilla de hello toodeploy que ha descargado con PowerShell, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-127">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="aa8e8-128">Si nunca ha usado PowerShell de Azure, Hola completa los pasos de hello [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-128">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="aa8e8-129">En una consola de PowerShell, ejecute hello `New-AzureRmResourceGroup` cmdlet toocreate un nuevo grupo de recursos, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-129">In a PowerShell console, run hello `New-AzureRmResourceGroup` cmdlet toocreate a new resource group, if necessary.</span></span> <span data-ttu-id="aa8e8-130">Si ya tiene un grupo de recursos creado, vaya toostep 3.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-130">If you already have a resource group created, go toostep 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="aa8e8-131">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="aa8e8-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="aa8e8-132">En una consola de PowerShell, ejecute hello `New-AzureRmResourceGroupDeployment` plantilla de cmdlet toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-132">In a PowerShell console, run hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="aa8e8-133">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="aa8e8-133">Expected output:</span></span>
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="aa8e8-134">Implementar la plantilla de hello mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="aa8e8-134">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="aa8e8-135">plantilla de hello toodeploy utilizando Hola CLI de Azure, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="aa8e8-135">toodeploy hello template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="aa8e8-136">Si nunca ha utilizado la CLI de Azure, siga los pasos de Hola Hola [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) artículo tooinstall y configurarlo.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-136">If you have never used Azure CLI, follow hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article tooinstall and configure it.</span></span>
2. <span data-ttu-id="aa8e8-137">Ejecute hello `azure config mode` modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-137">Run hello `azure config mode` command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="aa8e8-138">Hola espera salida de hello comando anterior:</span><span class="sxs-lookup"><span data-stu-id="aa8e8-138">hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="aa8e8-139">Abra hello [archivo de parámetros](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), seleccione su contenido y guarde el archivo tooa en el equipo.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-139">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it tooa file in your computer.</span></span> <span data-ttu-id="aa8e8-140">En este ejemplo, los parámetros de Hola se guardan con el nombre de archivo de tooa *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-140">For this example, hello parameters are saved tooa file named *parameters.json*.</span></span> <span data-ttu-id="aa8e8-141">Cambiar los valores de parámetro hello en el archivo de hello si lo desea, pero como mínimo, se recomienda que se cambia de valor de Hola de hello adminPassword parámetro tooa complejos contraseña única.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-141">Change hello parameter values within hello file if desired, but at a minimum, it's recommended that you change hello value for hello adminPassword parameter tooa unique, complex password.</span></span>
4. <span data-ttu-id="aa8e8-142">Ejecute hello `azure group deployment create` cmd toodeploy Hola archivos de red virtual nueva mediante el uso de la plantilla de Hola y los parámetros que ha descargado y modificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-142">Run hello `azure group deployment create` cmd toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="aa8e8-143">En el siguiente comando de hello, reemplace <path> con ruta de acceso de Hola que guardó el archivo de Hola a.</span><span class="sxs-lookup"><span data-stu-id="aa8e8-143">In hello command below, replace <path> with hello path you saved hello file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="aa8e8-144">Resultado esperado (enumera los valores de parámetro utilizados):</span><span class="sxs-lookup"><span data-stu-id="aa8e8-144">Expected output (lists parameter values used):</span></span>

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

