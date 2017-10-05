---
title: "Creación de una máquina virtual con una dirección IP pública estática (plantilla de Azure Resource Manager) | Microsoft Docs"
description: "Obtenga información sobre cómo crear una máquina virtual con una dirección IP pública estática mediante una plantilla de Azure Resource Manager."
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
ms.openlocfilehash: 2f503aa60fdd9b7cf66ef482a1041e34c88e5c01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="46059-103">Creación de una máquina virtual con una dirección IP pública estática mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="46059-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="46059-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="46059-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="46059-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="46059-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="46059-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="46059-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="46059-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="46059-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="46059-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="46059-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="46059-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="46059-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="46059-110">En este artículo se describe el uso del modelo de implementación de Resource Manager, recomendado por Microsoft para la mayoría de las nuevas implementaciones en lugar del modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="46059-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="46059-111">Recursos de dirección IP pública en un archivo de plantilla</span><span class="sxs-lookup"><span data-stu-id="46059-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="46059-112">Puede ver y descargar la [plantilla de ejemplo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="46059-112">You can view and download the [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="46059-113">En la sección siguiente se muestra la definición del recurso de dirección IP pública, basada en el escenario anterior:</span><span class="sxs-lookup"><span data-stu-id="46059-113">The following section shows the definition of the public IP resource, based on the scenario above:</span></span>

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

<span data-ttu-id="46059-114">Observe la propiedad **publicIPAllocationMethod** , que se establece en *Static*.</span><span class="sxs-lookup"><span data-stu-id="46059-114">Notice the **publicIPAllocationMethod** property, which is set to *Static*.</span></span> <span data-ttu-id="46059-115">Esta propiedad puede ser *Dynamic* (valor predeterminado) o *Static*.</span><span class="sxs-lookup"><span data-stu-id="46059-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="46059-116">Si se establece en estática, se garantiza que la dirección IP pública asignada no cambiará nunca.</span><span class="sxs-lookup"><span data-stu-id="46059-116">Setting it to static guarantees that the public IP address assigned will never change.</span></span>

<span data-ttu-id="46059-117">En la sección siguiente se muestra la asociación de la dirección IP pública con una interfaz de red:</span><span class="sxs-lookup"><span data-stu-id="46059-117">The following section shows the association of the public IP address with a network interface:</span></span>

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

<span data-ttu-id="46059-118">Observe la propiedad **publicIPAddress** que señala a **Id** de un recurso denominado **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="46059-118">Notice the **publicIPAddress** property pointing to the **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="46059-119">Se trata del nombre del recurso de IP pública que se muestra arriba.</span><span class="sxs-lookup"><span data-stu-id="46059-119">That is the name of the public IP resource shown above.</span></span>

<span data-ttu-id="46059-120">Por último, la interfaz de red anterior se muestra en la propiedad **networkProfile** de la máquina virtual que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="46059-120">Finally, the network interface above is listed in the **networkProfile** property of the VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="46059-121">Implementar la plantilla por medio de un solo clic para implementar</span><span class="sxs-lookup"><span data-stu-id="46059-121">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="46059-122">La plantilla de ejemplo disponible en el repositorio público usa un archivo de parámetros que contiene los valores predeterminados utilizados para generar el escenario descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46059-122">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="46059-123">Para implementar esta plantilla haciendo clic para implementar, haga clic en **Implementar en Azure** en el archivo Readme.md para la plantilla [Máquina virtual con PIP estático](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) .</span><span class="sxs-lookup"><span data-stu-id="46059-123">To deploy this template using click to deploy, click **Deploy to Azure** in the Readme.md file for the [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="46059-124">Reemplace los valores de parámetro predeterminados si lo desea y escriba los valores para los parámetros en blanco.</span><span class="sxs-lookup"><span data-stu-id="46059-124">Replace the default parameter values if desired and enter values for the blank parameters.</span></span>  <span data-ttu-id="46059-125">Siga las instrucciones en el portal para crear una máquina virtual con una dirección IP pública estática.</span><span class="sxs-lookup"><span data-stu-id="46059-125">Follow the instructions in the portal to create a virtual machine with a static public IP address.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="46059-126">Implementación de la plantilla mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="46059-126">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="46059-127">Para implementar la plantilla que descargó con PowerShell, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="46059-127">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="46059-128">Si nunca usó Azure PowerShell, complete los pasos del artículo [How to Install and Configure Azure PowerShell](/powershell/azure/overview) (Cómo instalar y configurar Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="46059-128">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="46059-129">En una consola de PowerShell, ejecute el cmdlet `New-AzureRmResourceGroup` para crear un nuevo grupo de recursos, si fuera necesario.</span><span class="sxs-lookup"><span data-stu-id="46059-129">In a PowerShell console, run the `New-AzureRmResourceGroup` cmdlet to create a new resource group, if necessary.</span></span> <span data-ttu-id="46059-130">Si ya tiene un grupo de recursos creado, vaya al paso 3.</span><span class="sxs-lookup"><span data-stu-id="46059-130">If you already have a resource group created, go to step 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="46059-131">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="46059-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="46059-132">En una consola de PowerShell, ejecute el cmdlet `New-AzureRmResourceGroupDeployment` para implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="46059-132">In a PowerShell console, run the `New-AzureRmResourceGroupDeployment` cmdlet to deploy the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="46059-133">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="46059-133">Expected output:</span></span>
   
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

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="46059-134">Implementación la plantilla ARM mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="46059-134">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="46059-135">Para implementar la plantilla mediante la CLI de Azure, complete los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="46059-135">To deploy the template by using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="46059-136">Si no ha usado nunca la CLI de Azure, siga los pasos del artículo [Instalación de la CLI de Azure](../cli-install-nodejs.md) para instalarla y configurarla.</span><span class="sxs-lookup"><span data-stu-id="46059-136">If you have never used Azure CLI, follow the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article to install and configure it.</span></span>
2. <span data-ttu-id="46059-137">Ejecute el comando `azure config mode` para cambiar al modo Resource Manager, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="46059-137">Run the `azure config mode` command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="46059-138">Este es el resultado esperado del comando anterior:</span><span class="sxs-lookup"><span data-stu-id="46059-138">The expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="46059-139">Abra el [archivo de parámetros](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), seleccione su contenido y guárdelo en un archivo del equipo.</span><span class="sxs-lookup"><span data-stu-id="46059-139">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it to a file in your computer.</span></span> <span data-ttu-id="46059-140">En este ejemplo, los parámetros se guardan en un archivo denominado *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="46059-140">For this example, the parameters are saved to a file named *parameters.json*.</span></span> <span data-ttu-id="46059-141">Cambie los valores de parámetro en el archivo si lo desea, pero como mínimo, se recomienda que cambie el valor para el parámetro adminPassword a una contraseña única y compleja.</span><span class="sxs-lookup"><span data-stu-id="46059-141">Change the parameter values within the file if desired, but at a minimum, it's recommended that you change the value for the adminPassword parameter to a unique, complex password.</span></span>
4. <span data-ttu-id="46059-142">Ejecute el cmd `azure group deployment create` para implementar la nueva red virtual mediante la plantilla y los archivos de parámetros que descargó y modificó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="46059-142">Run the `azure group deployment create` cmd to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="46059-143">En el siguiente comando, reemplace <path> por la ruta de acceso en la que guardó el archivo.</span><span class="sxs-lookup"><span data-stu-id="46059-143">In the command below, replace <path> with the path you saved the file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="46059-144">Resultado esperado (enumera los valores de parámetro utilizados):</span><span class="sxs-lookup"><span data-stu-id="46059-144">Expected output (lists parameter values used):</span></span>

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

