---
title: "Ejemplo de secuencia de comandos de CLI - Get hello hostname, puertos y las claves de caché en Redis de Azure aaaAzure | Documentos de Microsoft"
description: "Azure ejemplo de secuencia de comandos CLI - Get hello hostname, puertos y las claves para una instancia de caché en Redis de Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Obtener Hola hostname, puertos y las claves de caché en Redis de Azure

En este escenario, aprenderá cómo claves, puertos y el nombre de host de tooretrieve Hola utilizan la instancia de caché en Redis de Azure de tooconnect tooan.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después el nombre de host de comandos tooretrieve hello, claves y los puertos de una instancia de caché en Redis de Azure. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#show) | Recupera detalles de una instancia de Azure Redis Cache. |
| [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys) | Recupera las claves de acceso para una instancia de Azure Redis Cache. |


## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de caché de Redis de Azure en hello [documentación de Azure Redis Cache](../cli-samples.md).
