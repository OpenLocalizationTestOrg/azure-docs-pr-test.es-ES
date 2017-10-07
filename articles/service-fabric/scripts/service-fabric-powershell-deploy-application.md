---
title: "Ejemplo de Script de PowerShell: aaaAzure implementar aplicación tooa clúster | Documentos de Microsoft"
description: "Script de Azure PowerShell de ejemplo: implementar un clúster de Service Fabric tooa de aplicación."
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Implementar un clúster de Service Fabric tooa de aplicación

Este script de ejemplo copia un almacén de imágenes de clúster de aplicación paquete tooa, registra el tipo de aplicación hello en clúster de Hola y crea una instancia de la aplicación del tipo de aplicación Hola.  Si los servicios predeterminados se definieron en el manifiesto de aplicación Hola del tipo de aplicación de destino de hello, dichos servicios se crean en este momento. Personalizar los parámetros de hello según sea necesario. 

Si es necesario, instale el módulo de PowerShell de tejido de servicio de hello con hello [SDK del servicio de Fabric](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Después de ejecutar el ejemplo de script de Hola, Hola script en [quitar una aplicación](service-fabric-powershell-remove-application.md) puede ser instancia de la aplicación hello tooremove usado, anular el registro del tipo de aplicación hello y eliminar paquete de aplicación Hola Hola almacén de imágenes.

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Copie un almacén de imágenes de clúster de aplicación paquete toohello.  |
|[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| Registra un tipo de aplicación y la versión en clúster de Hola. |
|[New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| Crea una aplicación a partir de un tipo de aplicación registrada. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el módulo de PowerShell de tejido de servicio de hello, consulte [documentación de Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Encontrará más ejemplos de Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).
