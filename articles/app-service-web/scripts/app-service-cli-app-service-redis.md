---
title: "Ejemplo de script de la CLI de Azure: conexión de una aplicación web a Redis Cache | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: conexión de una aplicación web a Redis Cache"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b697c8508a6c3422b6b0d0ca36843a9c884b505f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-redis-cache"></a>Conexión de una aplicación web a Redis Cache

En este escenario aprenderá a crear una instancia de Azure Redis Cache y una aplicación web de Azure. Y, después, vinculará la instancia de Redis Cache a la aplicación web mediante la configuración de la aplicación.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicación del script

Este script usa los siguientes comandos para crear un grupo de recursos, una aplicación web, una instancia de Redis Cache y todos los recursos relacionados. Cada comando de la tabla crea un vínculo a documentación específica del comando.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Crea un plan de App Service, que es como una granja de servidores para una aplicación web de Azure. |
| [az webapp create](https://docs.microsoft.com/cli/azure/webapp#create) | Crea una aplicación web de Azure. |
| [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) | Crea una instancia nueva de Redis Cache. Aquí es donde se almacenarán los datos. |
| [az redis list-keys](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | Muestra las teclas de acceso de la instancia de Redis Cache. |
| [az webapp config appsettings set](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | Crea o actualiza una configuración de aplicación para una aplicación web de Azure. La configuración de la aplicación se expone como variables de entorno para la aplicación. |

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).

Puede encontrar ejemplos de script adicionales de la CLI de App Service en la [documentación de Azure App Service](../app-service-cli-samples.md).
