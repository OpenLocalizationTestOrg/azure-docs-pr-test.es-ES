---
title: base de datos-nuevo servidor de aaaPowerShell copia de ejemplo de Azure SQL | Documentos de Microsoft
description: Toocopy de secuencia de comandos de ejemplo de PowerShell Azure un servidor nuevo de la tooa de base de datos SQL
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a>Usar PowerShell toocopy un servidor nuevo de la tooa de base de datos SQL

Este ejemplo de script de PowerShell crea una copia de una base de datos existente en un nuevo servidor. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a>Copie un nuevo servidor de base de datos tooa

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | Crea un servidor lógico que hospeda una base de datos o un grupo elástico. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | Crea una base de datos en un servidor lógico como una base de datos única o agrupada. |
| [New-AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | Crea una copia de una base de datos que utiliza instantáneas hello en hello hora actual. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |
|||

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).

Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).
