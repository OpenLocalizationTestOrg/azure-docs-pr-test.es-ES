---
title: "herramienta de trabajos de bases de datos elástico de aaaHow toouninstall"
description: "¿Cómo toouninstall Hola herramienta de trabajos de bases de datos elásticas"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a>Desinstalación de componentes de Trabajos de base de datos elástica.
**Trabajos de base de datos elásticos** componentes se pueden desinstalar mediante el Portal de Hola o PowerShell.

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>Desinstalar componentes de trabajos de bases de datos elásticas mediante Hola portal de Azure
1. Abra hello [portal de Azure](https://portal.azure.com/).
2. Navegar por suscripción toohello que contiene **trabajos de base de datos elástica** componentes, es decir Hola suscripción en la base de datos elástico se instalaron componentes de trabajos.
3. Haga clic en **Examinar** y luego en **Grupos de recursos**.
4. Grupo de recursos de hello seleccione llamado "__ElasticDatabaseJob".
5. Elimine el grupo de recursos de Hola.

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>Desinstalación de componentes de Trabajos de base de datos elástica mediante PowerShell
1. Inicia una ventana de comandos de PowerShell de Microsoft Azure y ve subdirectorio herramientas toohello bajo la carpeta de Hola Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x: tipo **cd herramientas**.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools
2. Ejecutar script de PowerShell de hello.\UninstallElasticDatabaseJobs.ps1.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1

O simplemente, ejecute hello siguiente secuencia de comandos, suponiendo que de forma predeterminada valores donde usadas en la instalación de componentes de hello:

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a>Pasos siguientes
trabajos de base de datos elástica toore instalación, consulte [instalar el servicio de trabajo de base de datos elástica Hola](sql-database-elastic-jobs-service-installation.md)

Si desea obtener más información sobre Trabajos de base de datos elástica, vea [Información general de Trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md).

<!--Image references-->


