---
title: "aaaAzure ejemplo de Script de PowerShell - enrutar el tráfico para lograr alta disponibilidad de aplicaciones | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: enrutamiento del tráfico para la alta disponibilidad de las aplicaciones"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Enrutamiento del tráfico para la alta disponibilidad de las aplicaciones

Este script crea un grupo de recursos, dos planes de App Service, dos aplicaciones web, un perfil de Traffic Manager y dos puntos de conexión de Traffic Manager. Administrador de tráfico dirige la aplicación de toohello de tráfico en una región como región principal de Hola y región secundaria toohello cuando la aplicación hello en la región principal de hello no está disponible. Antes de ejecutar script de Hola, debe cambiar Hola MyWebApp, MyWebAppL1 y MyWebAppL2 valores toounique valores a través de Azure. Después de ejecutar el script de Hola, puede tener acceso a la aplicación hello en la región principal de hello con hello mywebapp.trafficmanager.net de dirección URL.

Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate un grupo de recursos, la aplicación web, el perfil del Administrador de tráfico y todos los recursos relacionados. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Crea un plan de App Service, que es como una granja de servidores para una aplicación web de Azure. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Crea una aplicación web de Azure en hello plan de servicio de aplicaciones. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/new-azurermresource) | Crea una aplicación web de Azure en hello plan de servicio de aplicaciones. |
| [New-AzureRmTrafficManagerProfile](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | Crea un perfil de Azure Traffic Manager. |
| [New-AzureRmTrafficManagerEndpoint](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | Agrega un perfil de Traffic Manager de Azure tooan de punto de conexión. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Encontrará ejemplos de script de PowerShell de red adicionales en hello [documentación de introducción a las redes Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
