---
title: "aaaCreate una máquina virtual con varias NIC - plantilla de Azure Resource Manager | Documentos de Microsoft"
description: "Cree una máquina virtual con varias NIC mediante una plantilla de Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a>Crear una VM con varias NIC mediante una plantilla
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](virtual-network-deploy-multinic-classic-ps.md).
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Hello pasos siguientes utiliza un grupo de recursos denominado *IaaSStory* para servidores WEB de Hola y un grupo de recursos denominado *IaaSStory-back-end* para servidores de Hola DB.

## <a name="prerequisites"></a>Requisitos previos
Para poder crear Hola servidores de base de datos, necesita hello toocreate *IaaSStory* grupo de recursos con todos los recursos necesarios de Hola para este escenario. toocreate estos recursos, completar Hola lo siguiente:

1. Navegue demasiado[página de la plantilla de hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. En página de la plantilla de hello, toohello derecha de **grupo de recursos primario**, haga clic en **implementar tooAzure**.
3. Si es necesario, cambiar los valores de parámetro de hello, a continuación, siga los pasos de hello en grupo de recursos de hello vista previa de Azure portal toodeploy Hola.

> [!IMPORTANT]
> Asegúrese de que los nombres de cuenta de almacenamiento sean únicos. No puede tener nombres de cuenta de almacenamiento duplicados en Azure.
> 

## <a name="understand-hello-deployment-template"></a>Comprender la plantilla de implementación de Hola
Antes de implementar la plantilla de hello proporcionada con esta documentación, asegúrese de que comprende lo que hace. Hola pasos proporciona una buena información general de la plantilla de hello:

1. Navegue demasiado[página de la plantilla de hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Haga clic en **azuredeploy.json** archivo de plantilla de hello tooopen.
3. Hola aviso *osType* los parámetros mostrados a continuación. Este parámetro es tooselect usa valores relacionados con qué toouse de imagen de máquina virtual para el servidor de base de datos de hello, junto con varios sistemas operativos.

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. Desplácese hacia abajo toohello lista de variables y compruebe la definición de Hola para hello **dbVMSetting** variables, que figuran a continuación. Recibe uno de los elementos de la matriz de hello contenidos en hello **dbVMSettings** variable. Si está familiarizado con la terminología de desarrollo de software, puede ver hello **dbVMSettings** variable como una tabla hash o un diccionario.

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. Suponga que decide toodeploy máquinas virtuales de Windows ejecutando SQL en hello back-end. Hola, a continuación, el valor de **osType** sería *Windows*, hello y **dbVMSetting** variable contendría el elemento Hola enumerado a continuación, que representa el primer valor de Hola Hola **dbVMSettings** variable.

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. Hola aviso **vmSize** contiene el valor de hello *Standard_DS3*. Solo determinados tamaños de VM permiten Hola uso de varias NIC. Puede comprobar qué tamaños de máquina virtual, es compatible con varias NIC leer hello [tamaños de máquina virtual de Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [tamaños de VM de Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artículos.

7. Desplácese hacia abajo demasiado**recursos** y observe Hola primer elemento. Describe una cuenta de almacenamiento. Esta cuenta de almacenamiento será toomaintain usa discos de datos de hello utilizados por cada máquina virtual de la base de datos. En este escenario, cada máquina virtual de base de datos tiene un disco de sistema operativo almacenado en almacenamiento normal y dos discos de datos almacenados en el almacenamiento SSD (Premium).

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. Desplácese hacia abajo de toohello siguiente recurso, como se muestra a continuación. Este recurso representa Hola NIC que se utiliza para el acceso a la base de datos en cada máquina virtual de la base de datos. Uso de Hola de aviso de hello **copia** función de este recurso. plantilla de Hello permite toodeploy como muchas máquinas virtuales como desee, en función de hello **dbCount** parámetro. Por lo tanto debe toocreate Hola la misma cantidad de NIC para el acceso de la base de datos, uno para cada máquina virtual.

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. Desplácese hacia abajo de toohello siguiente recurso, como se muestra a continuación. Este recurso representa Hola NIC que se usa para la administración en cada máquina virtual de la base de datos. Una vez más, necesita una de estas NIC para cada máquina virtual de base de datos. Hola aviso **grupos** elemento, vincular un NSG que permita tooRDP/SSH toothis NIC de acceso solo.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. Desplácese hacia abajo de toohello siguiente recurso, como se muestra a continuación. Este recurso representa un toobe de conjunto de disponibilidad compartida por todas las máquinas virtuales de la base de datos. De este modo, se garantiza que siempre habrá una máquina virtual en hello establecer ejecutando durante el mantenimiento.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. Desplácese hacia abajo toohello siguiente recurso. Este recurso representa la base de datos de hello las máquinas virtuales, tal como se muestra en hello primero algunas líneas que se muestran a continuación. Uso de Hola de aviso de hello **copia** volver a funcionar, asegurándose de que varias máquinas virtuales se crean en función de hello **dbCount** parámetro. Observe también hello **dependsOn** colección. Se muestran dos NIC que se va a toobe es necesario creado antes de Hola que se implementa la máquina virtual, junto con el conjunto de disponibilidad de Hola y cuenta de almacenamiento de Hola.

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. Desplácese hacia abajo en hello VM recursos toohello **networkProfile** elemento, como se muestra a continuación. Observe que existen dos NIC que hacen referencia a cada máquina virtual. Al crear varias NIC para una máquina virtual, debe establecer hello **principal** propiedad de uno de hello NIC demasiado*true*, y Hola rest demasiado*false*.

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Implementar la plantilla de ARM de hello mediante haga clic en toodeploy

> [!IMPORTANT]
> Asegúrese de que siga hello [requisitos previos](#Pre-requisites) pasos antes de seguir estas instrucciones Hola.
> 

plantilla de ejemplo Hola disponible en el repositorio público de hello usa un archivo de parámetros que contiene el escenario Hola predeterminada valores utilizados toogenerate Hola descrito anteriormente. toodeploy este uso de la plantilla, haga clic en toodeploy, siga [este vínculo](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello derecha de **(vea la documentación de) el grupo de recursos de back-end** haga clic en **implementar tooAzure**, reemplazar Hola valores de parámetro predeterminados si es necesario y siga las instrucciones de hello en el portal de Hola.

Hola siguiente ilustración muestra el contenido de Hola Hola nuevos del grupo de recursos, después de la implementación.

![Grupo de recursos back-end](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a>Implementar la plantilla de hello mediante PowerShell
plantilla de hello toodeploy que ha descargado con PowerShell, instalar y configurar PowerShell siguiendo los pasos de Hola Hola [instalar y configurar PowerShell](/powershell/azure/overview) artículo y, a continuación, complete Hola pasos:

Ejecute hello  **`New-AzureRmResourceGroup`**  toocreate cmdlet un grupo de recursos con Hola plantilla.

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

Resultado esperado:

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Implementar la plantilla de hello mediante Hola CLI de Azure
plantilla de hello toodeploy mediante el uso de hello CLI de Azure, siga los pasos de Hola a continuación.

1. Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.
2. Ejecute hello  **`azure config mode`**  modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.

    ```azurecli
    azure config mode arm
    ```

    Hola espera salida se indica a continuación:

        info:    New mode is arm

3. Abra hello [archivo de parámetros](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), seleccione su contenido y guarde el archivo tooa en el equipo. En este ejemplo, hemos guardado archivo de parámetros de hello demasiado*parameters.json*.
4. Ejecute hello  **`azure group deployment create`**  archivos de red virtual nueva mediante el uso de la plantilla de Hola y los parámetros de cmdlet toodeploy Hola que ha descargado y modificado anteriormente. lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    Resultado esperado:
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

