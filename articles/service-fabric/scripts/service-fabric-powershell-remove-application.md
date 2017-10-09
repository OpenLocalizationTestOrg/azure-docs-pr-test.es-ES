---
title: "aaaAzure ejemplo de Script de PowerShell - quitar aplicación desde un clúster | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: quitar una aplicación de un clúster de Service Fabric."
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
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Eliminación de una aplicación de un clúster de Service Fabric

Este script de ejemplo elimina una instancia de la aplicación de Service Fabric ejecución, anula el registro de un tipo de aplicación y la versión de clúster de Hola y elimina el paquete de aplicación Hola Hola clúster del almacén de imágenes.  Instancia de la aplicación hello eliminar también elimina Hola todas las instancias de servicio asociadas a esa aplicación en ejecución. Personalizar los parámetros de hello según sea necesario. 

Si es necesario, instale el módulo de PowerShell de tejido de servicio de hello con hello [SDK del servicio de Fabric](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | Quita una instancia de la aplicación de Service Fabric ejecución de clúster de Hola.  |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Anula el registro de un tipo de aplicación de Service Fabric y una versión de clúster de Hola. |
| [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Quita un paquete de aplicación de Service Fabric Hola almacén de imágenes.|

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el módulo de PowerShell de tejido de servicio de hello, consulte [documentación de Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Encontrará más ejemplos de Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).
