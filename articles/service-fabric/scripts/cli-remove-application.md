---
title: aaaAzure ejemplo para quitar la secuencia de comandos de Service Fabric CLI
description: "Quitar una aplicación de un clúster de Azure Service Fabric mediante hello Azure Service Fabric CLI"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Eliminación de una aplicación de un clúster de Service Fabric

Este script de ejemplo elimina una instancia de la aplicación de Service Fabric ejecución, se anula el registro de un tipo de aplicación y la versión de clúster de Hola.  Instancia de la aplicación hello eliminar también elimina Hola todas las instancias de servicio asociadas a esa aplicación en ejecución. A continuación, se eliminan los archivos de aplicación Hola Hola almacén de imágenes. 

Si es necesario, instale hello [Service Fabric CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Script de ejemplo

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información, vea hello [documentación de Service Fabric CLI](../service-fabric-cli.md).

Encontrará más ejemplos de CLI de tejido de servicio para Azure Service Fabric en hello [ejemplos de CLI de tejido de servicio](../samples-cli.md).
