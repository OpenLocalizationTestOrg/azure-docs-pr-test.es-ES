---
title: "Ejemplo de Script de PowerShell: puerto de la aplicación abierta en el equilibrador de carga aaaAzure | Documentos de Microsoft"
description: "Ejemplo de Script de PowerShell Azure - abrir un puerto en el equilibrador de carga de Azure de Hola para una aplicación de Service Fabric."
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
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a>Abrir un puerto de la aplicación en el equilibrador de carga de Azure Hola

Una aplicación de Service Fabric que se ejecuta en Azure se encuentra detrás de equilibrador de carga de Azure Hola. Este script de ejemplo abre un puerto en un equilibrador de carga de Azure para que una aplicación de Service Fabric se comunique con los clientes externos. Personalizar los parámetros de hello según sea necesario. 

Si es necesario, instale el módulo de PowerShell de tejido de servicio de hello con hello [SDK del servicio de Fabric](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siga los comandos. Cada comando de la tabla de hello vincula documentación específica del toocommand.

| Comando | Notas |
|---|---|
| [Get-AzureRmResource](/powershell/module/azurerm.resources/get-azurermresource) | Obtiene un recurso de Azure.  |
| [Get-AzureRmLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer) | Obtiene el equilibrador de carga de Azure Hola. |
| [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | Agrega un equilibrador de carga de tooa de configuración de sondeo.|
| [Get-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | Obtiene una configuración de sondeo para un equilibrador de carga. |
| [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | Agrega un equilibrador de carga de tooa de configuración de regla. |
| [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer) | Conjuntos de Hola estado de objetivo de un equilibrador de carga. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).

Encontrará más ejemplos de Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).
