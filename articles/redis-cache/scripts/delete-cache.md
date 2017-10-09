---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure eliminar una caché en Redis de Azure | Documentos de Microsoft"
description: "Ejemplo de script de CLI de Azure: Eliminación de Azure Redis Cache"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 788277f6464d40fedc597ce7f3041130312c07a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-azure-redis-cache"></a>Eliminación de una instancia de Azure Redis Cache

En este escenario, aprenderá cómo toodelete un Redis de Azure almacenan en caché.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toodelete una instancia de caché en Redis de Azure. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [eliminación de az redis](https://docs.microsoft.com/cli/azure/redis#delete) | Elimine una instancia de Redis Cache. |


## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de caché de Redis de Azure en hello [documentación de Azure Redis Cache](../cli-samples.md).
