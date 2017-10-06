---
title: "Ejemplo de Script de PowerShell - aaaAzure supervisar una aplicación web con registros de servidor web | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: supervisión de una aplicación web con registros de servidor web"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: efaae1e19f5153e33d1f5d5decadb9f6c4649f8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a>Supervisión de una aplicación web con registros de servidor web

En este escenario creará un grupo de recursos, el plan de servicio de aplicaciones, la aplicación web y configurar registros de servidor web de hello web app tooenable. A continuación, se descargarán los archivos de registro de hello para su revisión.

Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser grupo de recursos de hello tooremove usado, aplicación web y todos ellos relacionados con recursos.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Crea un plan de App Service, |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Crea una aplicación web. |
| [Set-AzureRmWebApp](/powershell/module/azurerm.websites/set-azurermwebapp) | Modifica la configuración de una aplicación web. |
| [Get-AzureRMWebAppMetrics](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | Obtiene las métricas de una aplicación web. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).

Encontrará más ejemplos de Powershell de Azure para aplicaciones de Web del servicio de aplicación de Azure en hello [ejemplos de PowerShell de Azure](../app-service-powershell-samples.md).
