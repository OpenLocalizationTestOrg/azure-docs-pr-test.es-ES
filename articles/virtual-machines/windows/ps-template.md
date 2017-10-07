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
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a>Creación de una máquina virtual Windows con una plantilla de Resource Manager

Este artículo muestra cómo un administrador de recursos de Azure toodeploy plantilla mediante PowerShell. plantilla de Hola que cree implementa una sola máquina virtual que ejecute Windows Server en una nueva red virtual con una sola subred.

Para obtener una descripción detallada del recurso de la máquina virtual de hello, consulte [máquinas virtuales en una plantilla de Azure Resource Manager](template-description.md). Para obtener más información acerca de todos los recursos de hello en una plantilla, consulte [tutorial de plantilla de Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Tardará aproximadamente cinco minutos hello toodo los pasos de este artículo.

## <a name="install-azure-powershell"></a>Azure PowerShell

Vea [cómo tooinstall y configurar Azure PowerShell](../../powershell-install-configure.md) para obtener información acerca de cómo instalar la versión más reciente de Hola de PowerShell de Azure, seleccione su suscripción y tooyour cuenta de inicio de sesión.

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Todos los recursos se deben implementar en un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

1. Obtenga una lista de las ubicaciones donde se pueden crear los recursos.
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. Crear grupo de recursos de hello en ubicación de Hola que seleccione. Este ejemplo muestra la creación de hello de un grupo de recursos denominado **myResourceGroup** en hello **West US** ubicación:

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a>Crear archivos de Hola

En este paso, creará un archivo de plantilla que implementa los recursos de Hola y un archivo de parámetros que proporciona la plantilla de toohello de valores de parámetro. También creará un archivo de autorización es decir, operaciones de Azure Resource Manager tooperform usado.

1. Cree un archivo denominado *CreateVMTemplate.json* y agregue este tooit de código JSON:

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

2. Cree un archivo denominado *Parameters.json* y agregue este tooit de código JSON:

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

3. Cree una nueva cuenta de almacenamiento y un contenedor:

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. Cargar la cuenta de almacenamiento de hello archivos toohello:

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    Cambio Hola - ubicación de toohello las rutas de acceso de archivo donde almacena los archivos de Hola.

## <a name="create-hello-resources"></a>Crear recursos de Hola

Implementar la plantilla de hello mediante parámetros de hello:

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> También puede implementar las plantillas y los parámetros desde archivos locales. más información, consulte toolearn [uso de PowerShell de Azure con el almacenamiento de Azure](../../storage/common/storage-powershell-guide-full.md).

## <a name="next-steps"></a>Pasos siguientes

- Si había problemas con la implementación de hello, puede echar un vistazo [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](../../resource-manager-common-deployment-errors.md).
- Obtenga información acerca de cómo toocreate y administrar una máquina virtual en [crear y administrar máquinas virtuales de Windows con el módulo de PowerShell de Azure de hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

