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
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a>Creación de una máquina virtual con una dirección IP pública estática mediante una plantilla de Azure Resource Manager

> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [CLI de Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Plantilla](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (clásico)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a>Recursos de dirección IP pública en un archivo de plantilla
Puede ver y descargar hello [plantilla de ejemplo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).

Hello siguiente sección muestra hello definición de recurso IP público hello, basado en el escenario de hello anterior:

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

Hola aviso **publicIPAllocationMethod** propiedad, que se establece demasiado*estático*. Esta propiedad puede ser *Dynamic* (valor predeterminado) o *Static*. Si se establece toostatic garantiza que nunca se cambiará la dirección IP pública Hola asignada.

Hello siguiente sección muestra la asociación de Hola de dirección IP pública de hello con una interfaz de red:

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

Hola aviso **publicIPAddress** propiedad que señala toohello **identificador** de un recurso denominado **variables('webVMSetting').pipName**. Que es el nombre de hello del recurso IP público Hola mostrado anteriormente.

Por último, interfaz de red de hello anterior se muestra en hello **networkProfile** propiedad de hello VM que se está creando.

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Implementar la plantilla de hello mediante haga clic en toodeploy

plantilla de ejemplo Hola disponible en el repositorio público de hello usa un archivo de parámetros que contiene el escenario Hola predeterminada valores utilizados toogenerate Hola descrito anteriormente. toodeploy este uso de la plantilla, haga clic en toodeploy, haga clic en **implementar tooAzure** en archivo Readme.md Hola Hola [VM con PIP estático](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) plantilla. Reemplace los valores de parámetro predeterminados Hola si lo desea y especifique valores para parámetros de hello en blanco.  Siga las instrucciones de hello en hello portal toocreate una máquina virtual con una dirección IP pública estática.

## <a name="deploy-hello-template-by-using-powershell"></a>Implementar la plantilla de hello mediante PowerShell

plantilla de hello toodeploy que ha descargado con PowerShell, siga los pasos de Hola a continuación.

1. Si nunca ha usado PowerShell de Azure, Hola completa los pasos de hello [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.
2. En una consola de PowerShell, ejecute hello `New-AzureRmResourceGroup` cmdlet toocreate un nuevo grupo de recursos, si es necesario. Si ya tiene un grupo de recursos creado, vaya toostep 3.

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    Resultado esperado:
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. En una consola de PowerShell, ejecute hello `New-AzureRmResourceGroupDeployment` plantilla de cmdlet toodeploy Hola.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    Resultado esperado:
   
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

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Implementar la plantilla de hello mediante Hola CLI de Azure
plantilla de hello toodeploy utilizando Hola CLI de Azure, Hola completa pasos:

1. Si nunca ha utilizado la CLI de Azure, siga los pasos de Hola Hola [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) artículo tooinstall y configurarlo.
2. Ejecute hello `azure config mode` modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.

    ```azurecli
    azure config mode arm
    ```

    Hola espera salida de hello comando anterior:

        info:    New mode is arm

3. Abra hello [archivo de parámetros](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), seleccione su contenido y guarde el archivo tooa en el equipo. En este ejemplo, los parámetros de Hola se guardan con el nombre de archivo de tooa *parameters.json*. Cambiar los valores de parámetro hello en el archivo de hello si lo desea, pero como mínimo, se recomienda que se cambia de valor de Hola de hello adminPassword parámetro tooa complejos contraseña única.
4. Ejecute hello `azure group deployment create` cmd toodeploy Hola archivos de red virtual nueva mediante el uso de la plantilla de Hola y los parámetros que ha descargado y modificado anteriormente. En el siguiente comando de hello, reemplace <path> con ruta de acceso de Hola que guardó el archivo de Hola a. 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    Resultado esperado (enumera los valores de parámetro utilizados):

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

