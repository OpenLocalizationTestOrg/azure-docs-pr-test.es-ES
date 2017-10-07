---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure enlazar una aplicación de la función de tooa de certificado SSL personalizada | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos CLI Azure - enlace una aplicación de función personalizada de tooa certificados SSL en Azure"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a>Enlazar una aplicación de la función de tooa de certificado SSL personalizada

Este script de ejemplo crea una aplicación de la función de servicio de aplicaciones con sus recursos relacionados, a continuación, enlaza el certificado SSL de Hola de un tooit de nombre de dominio personalizado. Para este ejemplo, se necesita:

* Obtener acceso a la página de configuración de DNS del registrador de dominios tooyour.
* Válido. Archivo PFX y su contraseña para hello SSL certificado que desee tooupload y enlazar.

toobind un certificado SSL, la aplicación de la función debe crearse en un plan de servicio de aplicaciones y no en un plan de consumo.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Crea un toobind requerido un plan de servicio de aplicaciones certificados SSL. |
| [az functionapp create]() | Crea una aplicación de función. |
| [az appservice web config hostname add](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Asigna una aplicación de función de toohello de dominio personalizado. |
| [az appservice web config ssl upload](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | Carga una aplicación de función de tooa de certificado SSL. |
| [az appservice web config ssl bind](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | Enlaza una aplicación de la función de tooa de certificado SSL cargada. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de servicio de aplicación Hola [documentación de servicio de aplicaciones de Azure]().
