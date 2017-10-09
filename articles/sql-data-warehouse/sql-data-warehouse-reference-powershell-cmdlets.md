---
title: cmdlets de aaaPowerShell para almacenamiento de datos de SQL Azure
description: Encontrar Hola superiores cmdlets de PowerShell para almacenamiento de datos de SQL de Azure e incluye toopause y reanudar una base de datos.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a>Cmdlets de PowerShell y API de REST para Almacenamiento de datos SQL
Muchas tareas de administración de Almacenamiento de datos SQL se pueden administrar mediante los cmdlets de Azure PowerShell o las API de REST.  A continuación se muestran algunos ejemplos de cómo toouse PowerShell comandos tooautomate tareas comunes en el almacenamiento de datos de SQL.  Para algunos buenos ejemplos REST, vea el artículo de hello [administrar escalabilidad con REST][Manage scalability with REST].

> [!NOTE]
> En orden toouse PowerShell de Azure con el almacenamiento de datos de SQL, necesita Azure PowerShell versión 1.0.3 o mayor.  Puede comprobar la versión ejecutando **Get-Module -ListAvailable -Name Azure**.  se puede instalar la versión más reciente de Hola desde [instalador de plataforma Web de Microsoft][Microsoft Web Platform Installer].  Para obtener más información acerca de cómo instalar la versión más reciente de hello, consulte [cómo tooinstall y configurar Azure PowerShell][How tooinstall and configure Azure PowerShell].
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a>Introducción a los cmdlets de Azure PowerShell
1. Abra Windows PowerShell.
2. En el símbolo del sistema de PowerShell hello, ejecute estos comandos toosign en toohello Azure Resource Manager y seleccione su suscripción.
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a>Ejemplo de pausa de Almacenamiento de datos SQL
Pausa una base de datos denominada "Database02" que está hospedada en un servidor cuyo nombre es "Server01".  servidor de Hola se encuentra en un grupo de recursos de Azure denominado "ResourceGroup1."

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
Una variación, este ejemplo canaliza Hola recuperar objeto demasiado[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].  Como resultado, la base de datos de hello está en pausa. comando final Hello muestra resultados de Hola.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a>Ejemplo de inicio de Almacenamiento de datos SQL
Reanuda el funcionamiento de una base de datos denominada "Database02" que está hospedada en un servidor cuyo nombre es "Server01". servidor de Hola se encuentra en un grupo de recursos denominado "ResourceGroup1."

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

Este ejemplo, que es una variación, recupera una base de datos denominada "Database02" desde un servidor cuyo nombre es "Server01" que está incluido en un grupo de recursos denominado "ResourceGroup1". Canaliza el objeto de hello recuperar demasiado[reanudar AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> Tenga en cuenta que si el servidor es foo.database.windows.net, utilice "foo" como Hola - ServerName hello en cmdlets de PowerShell.
> 
> 

## <a name="other-supported-powershell-cmdlets"></a>Otros cmdlets de PowerShell admitidos
Estos cmdlets de PowerShell se admiten en Azure SQL Data Warehouse.

* [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]
* [Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]
* [Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]
* [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]
* [Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]
* [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]
* [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]
* [Select-AzureRmSubscription][Select-AzureRmSubscription]
* [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]
* [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más ejemplos de PowerShell, consulte:

* [Creación de SQL Data Warehouse con PowerShell][Create a SQL Data Warehouse using PowerShell]
* [Restauración de base de datos][Database restore]

Para conocer otras tareas que se pueden automatizar con PowerShell, consulte los [cmdlets de Azure SQL Database][Azure SQL Database Cmdlets]. Tenga en cuenta que no todos los cmdlets de Azure SQL Database se admiten para Azure SQL Data Warehouse.  Para ver una lista de todas las tareas que se pueden automatizar con PowerShell, consulte [Operaciones para bases de datos SQL de Azure][Operations for Azure SQL Databases].

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
