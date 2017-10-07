---
title: "capacidad de almacenamiento de datos de SQL Azure (PowerShell) de cálculo aaaManage | Documentos de Microsoft"
description: Capacidad de proceso de PowerShell tareas toomanage. Escalado de los recursos de proceso ajustando DWU. O bien, puede pausar y reanudar los costos de toosave de recursos de proceso.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a>Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (PowerShell)
> [!div class="op_single_selector"]
> * [Información general](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a>Antes de empezar
### <a name="install-hello-latest-version-of-azure-powershell"></a>Instalar la versión más reciente de Hola de PowerShell de Azure
> [!NOTE]
> toouse PowerShell de Azure con el almacenamiento de datos de SQL, necesita Azure PowerShell versión 1.0.3 o mayor.  su versión actual de tooverify ejecutar comando hello **Get-Module - ListAvailable-Name Azure**. Puede instalar la versión más reciente de Hola de [instalador de plataforma Web de Microsoft][Microsoft Web Platform Installer].  Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell][How tooinstall and configure Azure PowerShell].
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a>Introducción a los cmdlets de Azure PowerShell
tooget iniciado:

1. Abra Azure PowerShell.
2. En el símbolo del sistema de PowerShell hello, ejecute estos comandos toosign en toohello Azure Resource Manager y seleccione su suscripción.

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a>Escalado de la potencia de proceso
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

Hola toochange a Dwu, usar hello [conjunto AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] cmdlet de PowerShell. Hello en el ejemplo siguiente se establece tooDW1000 objetivo de hello servicio nivel de base de datos de hello MySQLDW que se hospeda en el servidor MyServer.

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Pausa del proceso
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause una base de datos, usar hello [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet. Hello en el ejemplo siguiente se pausa una base de datos denominada Database02 hospedado en un servidor denominado Server01. servidor Hello está en un grupo de recursos de Azure denominado ResourceGroup1.

> [!NOTE]
> Tenga en cuenta que si el servidor es foo.database.windows.net, utilice "foo" como Hola - ServerName hello en cmdlets de PowerShell.
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
Una variación, en el ejemplo siguiente se recupera la base de datos de Hola en objeto hello $database. A continuación, canaliza el objeto de hello demasiado[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]. Hola resultados se almacenan en hello objeto resultDatabase. comando final Hello muestra resultados de Hola.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Reanudación del proceso
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

toostart una base de datos, usar hello [reanudar AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet. Hello en el ejemplo siguiente se inicia una base de datos denominada Database02 hospedado en un servidor denominado Server01. servidor Hello está en un grupo de recursos de Azure denominado ResourceGroup1.

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

Una variación, en el ejemplo siguiente se recupera la base de datos de Hola en objeto hello $database. A continuación, canaliza el objeto de hello demasiado[reanudar AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] y almacena los resultados de hello en $resultDatabase. comando final Hello muestra resultados de Hola.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a>Comprobar el estado de la base de datos

Como se muestra en hello por encima de los ejemplos, se pueden usar [Get AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet tooget información en una base de datos, por tanto, la comprobación de estado de hello, sino también toouse como un argumento. 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

El resultado será similar a este: 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

Donde, a continuación, puede comprobar hello toosee *estado* de base de datos de Hola. En este caso, puede ver esta base de datos está en línea. 

Al ejecutar este comando, debería recibir uno de los siguientes valores de Estado: Con conexión, Pausando, Resuming, Escalando y En pausa.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Pasos siguientes
Para otras tareas de administración, consulte [Información general de administración][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
