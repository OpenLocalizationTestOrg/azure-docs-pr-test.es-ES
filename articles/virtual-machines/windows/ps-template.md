---
title: aaaCreate una VM de Windows desde una plantilla de Azure | Documentos de Microsoft
description: "Use una plantilla de administrador de recursos y PowerShell tooeasily crear una nueva máquina virtual de Windows."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 630111482c7dc046091632e2ed458ac143325d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="d2374-103">Creación de una máquina virtual Windows con una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d2374-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="d2374-104">Este artículo muestra cómo un administrador de recursos de Azure toodeploy plantilla mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2374-104">This article shows you how toodeploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="d2374-105">plantilla de Hola que cree implementa una sola máquina virtual que ejecute Windows Server en una nueva red virtual con una sola subred.</span><span class="sxs-lookup"><span data-stu-id="d2374-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="d2374-106">Para obtener una descripción detallada del recurso de la máquina virtual de hello, consulte [máquinas virtuales en una plantilla de Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="d2374-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="d2374-107">Para obtener más información acerca de todos los recursos de hello en una plantilla, consulte [tutorial de plantilla de Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d2374-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="d2374-108">Tardará aproximadamente cinco minutos hello toodo los pasos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="d2374-108">It should take about five minutes toodo hello steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="d2374-109">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2374-109">Install Azure PowerShell</span></span>

<span data-ttu-id="d2374-110">Vea [cómo tooinstall y configurar Azure PowerShell](../../powershell-install-configure.md) para obtener información acerca de cómo instalar la versión más reciente de Hola de PowerShell de Azure, seleccione su suscripción y tooyour cuenta de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d2374-110">See [How tooinstall and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="d2374-111">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d2374-111">Create a resource group</span></span>

<span data-ttu-id="d2374-112">Todos los recursos se deben implementar en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d2374-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="d2374-113">Obtenga una lista de las ubicaciones donde se pueden crear los recursos.</span><span class="sxs-lookup"><span data-stu-id="d2374-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="d2374-114">Crear grupo de recursos de hello en ubicación de Hola que seleccione.</span><span class="sxs-lookup"><span data-stu-id="d2374-114">Create hello resource group in hello location that you select.</span></span> <span data-ttu-id="d2374-115">Este ejemplo muestra la creación de hello de un grupo de recursos denominado **myResourceGroup** en hello **West US** ubicación:</span><span class="sxs-lookup"><span data-stu-id="d2374-115">This example shows hello creation of a resource group named **myResourceGroup** in hello **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a><span data-ttu-id="d2374-116">Crear archivos de Hola</span><span class="sxs-lookup"><span data-stu-id="d2374-116">Create hello files</span></span>

<span data-ttu-id="d2374-117">En este paso, creará un archivo de plantilla que implementa los recursos de Hola y un archivo de parámetros que proporciona la plantilla de toohello de valores de parámetro.</span><span class="sxs-lookup"><span data-stu-id="d2374-117">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="d2374-118">También creará un archivo de autorización es decir, operaciones de Azure Resource Manager tooperform usado.</span><span class="sxs-lookup"><span data-stu-id="d2374-118">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="d2374-119">Cree un archivo denominado *CreateVMTemplate.json* y agregue este tooit de código JSON:</span><span class="sxs-lookup"><span data-stu-id="d2374-119">Create a file named *CreateVMTemplate.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
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
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. <span data-ttu-id="d2374-120">Cree un archivo denominado *Parameters.json* y agregue este tooit de código JSON:</span><span class="sxs-lookup"><span data-stu-id="d2374-120">Create a file named *Parameters.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. <span data-ttu-id="d2374-121">Cree una nueva cuenta de almacenamiento y un contenedor:</span><span class="sxs-lookup"><span data-stu-id="d2374-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="d2374-122">Cargar la cuenta de almacenamiento de hello archivos toohello:</span><span class="sxs-lookup"><span data-stu-id="d2374-122">Upload hello files toohello storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="d2374-123">Cambio Hola - ubicación de toohello las rutas de acceso de archivo donde almacena los archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2374-123">Change hello -File paths toohello location where you stored hello files.</span></span>

## <a name="create-hello-resources"></a><span data-ttu-id="d2374-124">Crear recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="d2374-124">Create hello resources</span></span>

<span data-ttu-id="d2374-125">Implementar la plantilla de hello mediante parámetros de hello:</span><span class="sxs-lookup"><span data-stu-id="d2374-125">Deploy hello template using hello parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="d2374-126">También puede implementar las plantillas y los parámetros desde archivos locales.</span><span class="sxs-lookup"><span data-stu-id="d2374-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="d2374-127">más información, consulte toolearn [uso de PowerShell de Azure con el almacenamiento de Azure](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="d2374-127">toolearn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2374-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d2374-128">Next Steps</span></span>

- <span data-ttu-id="d2374-129">Si había problemas con la implementación de hello, puede echar un vistazo [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="d2374-129">If there were issues with hello deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="d2374-130">Obtenga información acerca de cómo toocreate y administrar una máquina virtual en [crear y administrar máquinas virtuales de Windows con el módulo de PowerShell de Azure de hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d2374-130">Learn how toocreate and manage a virtual machine in [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

