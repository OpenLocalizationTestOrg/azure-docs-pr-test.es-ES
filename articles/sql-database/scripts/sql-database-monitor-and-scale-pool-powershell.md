---
title: "aaaPowerShell ejemplo-monitor-escala-SQL elástico grupo Azure base de datos SQL | Documentos de Microsoft"
description: "Azure toomonitor de secuencia de comandos de ejemplo de PowerShell y la escala de un grupo elástico de SQL en la base de datos de SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a>Usar PowerShell toomonitor y escalar un grupo elástico de SQL en la base de datos de SQL Azure

En este ejemplo de secuencia de comandos de PowerShell monitores Hola métricas de rendimiento de un grupo elástico, escala tooa mayor nivel de rendimiento y crea una regla de alerta en una de las métricas de rendimiento de Hola. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | Crea un servidor lógico que hospeda una base de datos o un grupo elástico. |
| [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | Crea un grupo elástico en un servidor lógico. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | Crea una base de datos en un servidor lógico como una base de datos única o agrupada. |
| [Get-AzureRmMetric](/powershell/module/azurerm.insights/get-azurermmetric) | Muestra información de uso de hello tamaño de base de datos de Hola.|
| [Add-AzureRMMetricAlertRule](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | Agrega o actualiza una regla de alerta basada en métricas. |
| [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | Actualiza las propiedades del grupo elástico |
| [Add-AzureRMMetricAlertRule](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | Establece a una regla de alerta tooautomatically monitor Dtu Hola futuras. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |
|||

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).

Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).