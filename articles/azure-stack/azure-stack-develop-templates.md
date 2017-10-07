---
title: plantillas de aaaDevelop para la pila de Azure | Documentos de Microsoft
description: "Información sobre las prácticas recomendadas de plantillas de Azure Stack"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 8a5bc713-6f51-49c8-aeed-6ced0145e07b
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 01581abcb7a3616469dcd38a646734f68decd3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-considerations"></a>Consideraciones de la plantilla de Azure Resource Manager
Al desarrollar la aplicación, es importante tooensure portabilidad de plantilla entre Azure y la pila de Azure.  Este tema proporciona consideraciones para el desarrollo de Azure Resource Manager [plantillas](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), por lo que puede prototipo de la implementación de aplicación y prueba en Azure sin el entorno de acceso tooan pila de Azure.

## <a name="public-namespaces"></a>Espacios de nombres públicos
Como la pila de Azure se hospeda en el centro de datos, tiene espacios de nombres de punto de conexión de servicio diferente que Hola nube pública de Azure. Como resultado, codificado de forma rígida los extremos públicos en las plantillas de administrador de recursos producirá un error cuando intente toodeploy les tooAzure pila. En su lugar, puede usar hello *referencia* y *concatenar* función toodynamically crear extremo de servicio de hello en función de los valores recuperados de proveedor de recursos de Hola durante la implementación. Por ejemplo, en lugar de especificar *blob.core.windows.net* en la plantilla, recuperar hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically establecer hello *osDisk.URI* punto de conexión:

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a>Control de versiones de la API
Las versiones de los servicios de Azure pueden diferir entre Azure y Azure Stack. Cada recurso requiere el atributo de valor apiVersion de hello, que define las capacidades de hello ofrecidas. compatibilidad de versiones de tooensure API en la pila de Azure, Hola después son versiones de API válidas para cada proveedor de recursos:

| Proveedor de recursos | apiVersion |
| --- | --- |
| Proceso |`'2015-06-15'` |
| Red |`'2015-06-15'`, `'2015-05-01-preview'` |
| Storage |`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'` |
| KeyVault | `'2015-06-01'` |
| App Service |`'2015-08-01'` |
| MySQL |`'2015-09-01'` |
| SQL |`'2014-04-01-preview'` |

## <a name="template-functions"></a>Funciones de plantillas
El Administrador de recursos [funciones](../azure-resource-manager/resource-group-template-functions.md) proporcionan capacidades necesarios toobuild plantillas dinámicas. Por ejemplo, puede utilizar funciones para tareas como las siguientes:

* Concatenar o recortar cadenas 
* Valores de referencia de otros recursos
* Iterar en recursos toodeploy varias instancias 

Al compilar las plantillas, algunas funciones no están disponibles en el kit de desarrollo de Azure Stack y no deben usarse. Estas funciones son las siguientes:

* Skip
* Take

## <a name="resource-location"></a>Ubicación del recurso
Plantillas de administrador de recursos usan una recursos tooplace de atributo de ubicación durante la implementación. En Azure, ubicaciones consulte región tooa como oeste de Estados Unidos o Sudamérica. En Azure Stack, las ubicaciones son diferentes porque Azure Stack está en el centro de datos.  plantillas de tooensure son transferibles entre Azure y la pila de Azure, debe hacer referencia a ubicación del grupo de recursos de hello como implementar recursos individuales. Puede hacerlo mediante `[resourceGroup().Location]` tooensure heredan todos los recursos Hola ubicación del grupo de recursos.  Hello siguiente extracto de la plantilla de administrador de recursos es un ejemplo del uso de esta función durante la implementación de una cuenta de almacenamiento:

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used toostore hello VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]


## <a name="next-steps"></a>Pasos siguientes
* [Implementación de plantillas con PowerShell](azure-stack-deploy-template-powershell.md)
* [Implementación de plantillas con la CLI de Azure](azure-stack-deploy-template-command-line.md)
* [Implementación de plantillas con Visual Studio](azure-stack-deploy-template-visual-studio.md)

