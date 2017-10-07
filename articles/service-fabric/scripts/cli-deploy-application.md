---
title: aaaAzure ejemplo para implementar la secuencia de comandos de Service Fabric CLI
description: "Implementar un clúster de Azure Service Fabric tooan de aplicación con hello Azure Service Fabric CLI"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Implementar un clúster de Service Fabric tooa de aplicación

Este script de ejemplo copia un almacén de imágenes de clúster de aplicación paquete tooa, registra el tipo de aplicación hello en clúster de Hola y crea una instancia de la aplicación del tipo de aplicación Hola. En este momento también se crea cualquier servicio predeterminado.

Si es necesario, instale hello [Service Fabric CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Script de ejemplo

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Cuando haya finalizado, Hola [quitar](cli-remove-application.md) script puede ser la aplicación de hello tooremove usado. script de Hola remove elimina la instancia de la aplicación hello, anula el registro de tipo de aplicación hello y elimina el paquete de aplicación Hola desde el almacén de imágenes.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información, vea hello [documentación de Service Fabric CLI](../service-fabric-cli.md).

Encontrará más ejemplos de CLI de tejido de servicio para Azure Service Fabric en hello [ejemplos de CLI de tejido de servicio](../samples-cli.md).
