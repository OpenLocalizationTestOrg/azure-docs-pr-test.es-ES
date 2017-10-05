---
title: "Creación de una máquina virtual Windows desde una plantilla de Azure | Microsoft Docs"
description: "Use una plantilla de Resource Manager y PowerShell para crear fácilmente una nueva máquina virtual de Windows."
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
ms.openlocfilehash: ddab80262fe27c1f5995858ec7de75d7c46df081
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="fed48-103">Creación de una máquina virtual Windows con una plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fed48-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="fed48-104">En este artículo se muestra cómo implementar una plantilla de Azure Resource Manager con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fed48-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="fed48-105">La plantilla que crea implementa una sola máquina virtual que ejecuta Windows Server en una nueva red virtual con una sola subred.</span><span class="sxs-lookup"><span data-stu-id="fed48-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="fed48-106">Para obtener una descripción detallada del recurso de máquina virtual, consulte [Virtual machines in an Azure Resource Manager template](template-description.md) (Máquinas virtuales en una plantilla de Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="fed48-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="fed48-107">Para obtener más información acerca de todos los recursos de una plantilla, consulte [Tutorial de la plantilla de Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="fed48-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="fed48-108">Tardará unos cinco minutos en realizar los pasos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="fed48-108">It should take about five minutes to do the steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="fed48-109">Instalar Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="fed48-109">Install Azure PowerShell</span></span>

<span data-ttu-id="fed48-110">Consulte [Cómo instalar y configurar Azure PowerShell](../../powershell-install-configure.md) para obtener más información sobre cómo instalar la versión más reciente de Azure PowerShell, seleccionar la suscripción que quiere usar e iniciar sesión en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="fed48-110">See [How to install and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="fed48-111">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="fed48-111">Create a resource group</span></span>

<span data-ttu-id="fed48-112">Todos los recursos se deben implementar en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fed48-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="fed48-113">Obtenga una lista de las ubicaciones donde se pueden crear los recursos.</span><span class="sxs-lookup"><span data-stu-id="fed48-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="fed48-114">Cree el grupo de recursos en la ubicación que seleccione.</span><span class="sxs-lookup"><span data-stu-id="fed48-114">Create the resource group in the location that you select.</span></span> <span data-ttu-id="fed48-115">En este ejemplo se muestra la creación de un grupo de recursos denominado **myResourceGroup** en la ubicación **Oeste de EE. UU.**:</span><span class="sxs-lookup"><span data-stu-id="fed48-115">This example shows the creation of a resource group named **myResourceGroup** in the **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-the-files"></a><span data-ttu-id="fed48-116">Creación de los archivos</span><span class="sxs-lookup"><span data-stu-id="fed48-116">Create the files</span></span>

<span data-ttu-id="fed48-117">En este paso, creará un archivo de plantilla que implementa los recursos y un archivo de parámetros que proporciona valores de parámetro a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="fed48-117">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="fed48-118">También creará un archivo de autorización que se utiliza para realizar operaciones de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fed48-118">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="fed48-119">Cree un archivo denominado *CreateVMTemplate.json* y agréguele este código JSON:</span><span class="sxs-lookup"><span data-stu-id="fed48-119">Create a file named *CreateVMTemplate.json* and add this JSON code to it:</span></span>

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

2. <span data-ttu-id="fed48-120">Cree un archivo denominado *Parameters.json* y agréguele este código JSON:</span><span class="sxs-lookup"><span data-stu-id="fed48-120">Create a file named *Parameters.json* and add this JSON code to it:</span></span>

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

3. <span data-ttu-id="fed48-121">Cree una nueva cuenta de almacenamiento y un contenedor:</span><span class="sxs-lookup"><span data-stu-id="fed48-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="fed48-122">Cargue los archivos en la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="fed48-122">Upload the files to the storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="fed48-123">Cambio las rutas de acceso de -File a la ubicación donde almacenó los archivos.</span><span class="sxs-lookup"><span data-stu-id="fed48-123">Change the -File paths to the location where you stored the files.</span></span>

## <a name="create-the-resources"></a><span data-ttu-id="fed48-124">Creación de los recursos</span><span class="sxs-lookup"><span data-stu-id="fed48-124">Create the resources</span></span>

<span data-ttu-id="fed48-125">Implemente la plantilla mediante los parámetros:</span><span class="sxs-lookup"><span data-stu-id="fed48-125">Deploy the template using the parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="fed48-126">También puede implementar las plantillas y los parámetros desde archivos locales.</span><span class="sxs-lookup"><span data-stu-id="fed48-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="fed48-127">Para obtener más información, consulte [Usar Azure PowerShell con Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="fed48-127">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fed48-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fed48-128">Next Steps</span></span>

- <span data-ttu-id="fed48-129">Si se produjeron problemas con la implementación, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="fed48-129">If there were issues with the deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="fed48-130">Aprenda a crear y administrar una máquina virtual en [Creación y administración de máquinas virtuales Windows con el módulo de Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fed48-130">Learn how to create and manage a virtual machine in [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

