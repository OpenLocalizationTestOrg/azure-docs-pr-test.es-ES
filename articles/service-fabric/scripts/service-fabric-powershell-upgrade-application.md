---
title: "Ejemplo de Script de PowerShell - aaaAzure actualizar una aplicación de Service Fabric | Documentos de Microsoft"
description: "Script de ejemplo de Azure PowerShell: actualización de una aplicación de Service Fabric."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a>Actualización de una aplicación de Service Fabric

Este script de ejemplo actualiza una ejecución tooversion de instancia de aplicación de Service Fabric 1.3.0. script de Hola copia el almacén de imágenes de hello nueva aplicación paquete toohello clúster, registra el tipo de aplicación Hola, inicia una actualización supervisada y comprueba continuamente el estado de actualización de hello hasta que la actualización Hola complete o se revierte. Personalizar los parámetros de hello según sea necesario. 

Si es necesario, instale el módulo de PowerShell de tejido de servicio de hello con hello [SDK del servicio de Fabric](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Obtiene todas las aplicaciones de hello en clúster de Service Fabric de Hola o una aplicación específica.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | Obtiene el estado de saludo de una actualización de la aplicación de Service Fabric. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Obtiene tipos de aplicaciones de Service Fabric Hola registrados en el clúster de Service Fabric Hola. |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Anula el registro de un tipo de aplicación de Service Fabric.  |
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Copia una imagen de toohello del paquete de aplicación de Service Fabric almacén.  |
| [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Registra un tipo de aplicación de Service Fabric. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | Actualiza una versión de tipo de Service Fabric aplicación toohello aplicación especificada. |


## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el módulo de PowerShell de tejido de servicio de hello, consulte [documentación de Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Encontrará más ejemplos de Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).
