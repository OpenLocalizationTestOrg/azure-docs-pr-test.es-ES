---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure supervisar una aplicación web con registros de servidor web | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: supervisión de una aplicación web con registros de servidor web"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 012b800c03af77387bed3d098fae3c96d82aee29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a>Supervisión de una aplicación web con registros de servidor web

En este escenario creará un grupo de recursos, el plan de servicio de aplicaciones, la aplicación web y configurar registros de servidor web de hello web app tooenable. A continuación, se descargarán los archivos de registro de hello para su revisión.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siguientes comandos toocreate un grupo de recursos, aplicación web y todos ellos relacionados con recursos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Crea un plan de App Service, que es como una granja de servidores para una aplicación web de Azure. |
| [az webapp create](https://docs.microsoft.com/cli/azure/webapp#create) | Crea una aplicación web de Azure. |
| [az webapp log config](https://docs.microsoft.com/cli/azure/webapp/log#config) | Configura los registros que conservará una aplicación web de Azure. |
| [az webapp log download](https://docs.microsoft.com/cli/azure/webapp/log#download) | Hola de descargas de los registros del programa Hola a un equipo local de la tooyour de aplicación web de Azure. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure](../app-service-cli-samples.md).
