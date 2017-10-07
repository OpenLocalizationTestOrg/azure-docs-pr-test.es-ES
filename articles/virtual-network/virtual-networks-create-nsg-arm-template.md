---
title: aaaCreate de red de grupos de seguridad - plantilla de administrador de recursos de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate e implementar grupos de seguridad de red mediante una plantilla de Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a>Creación de grupos de seguridad de red mediante una plantilla de Azure Resource Manager

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación del Administrador de recursos de Hola. También puede [crear NSG en el modelo de implementación clásica de hello](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a>Recursos de grupo de seguridad de red en un archivo de plantilla
Puede ver y descargar hello [plantilla de ejemplo](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).

Hello siguiente sección muestra hello definición de hello NSG front-end, según el escenario de Hola.

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
tooassociate subred de front-end de toohello de hello NSG, tienes toochange la definición de subred hello en plantilla de Hola y usar Id. de referencia de Hola para hello NSG.

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

Tenga en cuenta Hola mismo hace para hello subred back-end hello y NSG back-end en la plantilla de Hola.

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Implementar la plantilla de ARM de hello mediante haga clic en toodeploy
plantilla de ejemplo Hola disponible en el repositorio público de hello usa un archivo de parámetros que contiene el escenario Hola predeterminada valores utilizados toogenerate Hola descrito anteriormente. toodeploy este uso de la plantilla, haga clic en toodeploy, siga [este vínculo](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), haga clic en **implementar tooAzure**, reemplazar valores de parámetro predeterminados de hello si es necesario y siga las instrucciones de hello del portal de Hola.

## <a name="deploy-hello-arm-template-by-using-powershell"></a>Implementar la plantilla de ARM de hello mediante PowerShell
plantilla de ARM de hello toodeploy descargó con PowerShell, siga los pasos de Hola a continuación.

1. Si nunca ha usado PowerShell de Azure, siga las instrucciones de Hola Hola [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) tooinstall y configurarlo.
2. Ejecute hello  **`New-AzureRmResourceGroup`**  toocreate cmdlet un grupo de recursos con Hola plantilla.

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Resultado esperado:

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
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a>Implementar la plantilla de ARM de hello mediante Hola CLI de Azure
plantilla ARM de hello toodeploy mediante Hola CLI de Azure, siga estos pasos Hola.

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.
2. Ejecute hello  **`azure config mode`**  modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.

    ```azurecli
    azure config mode arm
    ```

    Hola te mostramos la salida de hello esperada de comando de hello:

        info:    New mode is arm

3. Ejecute hello  **`azure group deployment create`**  archivos de red virtual nueva mediante el uso de la plantilla de Hola y los parámetros de cmdlet toodeploy Hola que ha descargado y modificado anteriormente. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Resultado esperado:
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * **-n (o --name)**. Nombre de toobe de grupo de recursos de hello creado.
   * **-l (o --location)**. Región de Azure donde se creará el grupo de recursos de Hola.
   * **-f (o --template-file)**. Archivo de plantilla de ruta de acceso tooyour ARM.
   * **-e (o --parameters-file)**. Archivo de parámetros de ruta de acceso tooyour ARM.

