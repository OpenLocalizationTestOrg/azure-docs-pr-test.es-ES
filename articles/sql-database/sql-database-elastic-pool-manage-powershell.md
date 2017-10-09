---
title: "PowerShell: Creación y administración de un grupo elástico de Azure SQL | Microsoft Docs"
description: "Obtenga información acerca de cómo toouse PowerShell toomanage un grupo elástico."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Creación y administración de un grupo elástico con PowerShell
Este tema muestra cómo toocreate y administrar escalable [grupos elásticos](sql-database-elastic-pool.md) con PowerShell.  También puede crear y administrar un grupo elástico Azure con hello [portal de Azure](https://portal.azure.com/), API de REST, o [C#](sql-database-elastic-pool-manage-csharp.md). También puede crear y mover bases de datos dentro y fuera de los grupos elásticos mediante [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Creación de un grupo elástico
Hola [AzureRmSqlElasticPool New](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet crea un grupo elástico. valores de Hello de eDTU por grupo, min y max Dtu están restringidos por el valor de nivel de servicio de hello (Basic, Standard, Premium o RS Premium). Consulte la sección [Límites de almacenamiento y de eDTU para grupos elásticos y bases de datos agrupadas](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Creación de una base de datos agrupada en un grupo elástico
Hola de uso [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet conjunto hello y **ElasticPoolName** bloque de destino de parámetro toohello. Consulte una base de datos existente en un grupo elástico, toomove [mover una base de datos en un grupo elástico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>Completar script
Este script crea un grupo de recursos de Azure y un servidor. Cuando se le solicite, proporcione un nombre de usuario de administrador y la contraseña de nuevo servidor de hello (no sus credenciales de Azure).

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>Creación de un grupo elástico y adición de varias bases de datos agrupadas
Creación de varias bases de datos en un grupo elástico puede tardar tiempo cuando se realiza mediante el portal de Hola o los cmdlets de PowerShell que crean una sola base de datos a la vez. creación de tooautomate en un grupo elástico, consulte [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).

## <a name="move-a-database-into-an-elastic-pool"></a>Movimiento de una base de datos a un grupo elástico
Puede mover una base de datos dentro o fuera de un grupo elástico con hello [AzureRmSqlDatabase conjunto](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>Cambio de la configuración de rendimiento de un grupo elástico
Cuando el rendimiento se ve afectado, puede cambiar configuración de Hola de crecimiento de hello grupo tooaccommodate. Hola de uso [AzureRmSqlElasticPool conjunto](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet. Establecer hello - Dtu parámetro toohello Edtu por grupo. Consulte los posibles valores en el artículo sobre [límites de almacenamiento y de eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>Cambiar el límite de almacenamiento de Hola para un grupo elástico

Hola de uso [conjunto AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _StorageMB -_ parámetro. Proporcione el límite de almacenamiento de hello en MB (por ejemplo, 2097152 conjuntos Hola almacenamiento límite too2 TB). Consulte los posibles valores en el artículo sobre [límites de almacenamiento y de eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

> [!IMPORTANT]
> almacenamiento de datos max Hola predeterminado por grupo de grupos de Premium con Edtu de 1500 o más están 750 GB. Hola tooobtain superior _máximo tamaño de almacenamiento de datos por grupo de_, se debe establecer explícitamente el límite de almacenamiento de Hola. Grupos de Premium con más de 750 GB de almacenamiento está actualmente en versión preliminar pública Hola siguientes regiones: UU 2, oeste de Estados Unidos, nos Gov Virginia, Europa occidental, Central de Alemania, sudeste de Asia, este de Japón, Australia Oriental, Canadá Central y este de Canadá.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>Obtener estado de Hola de las operaciones de grupo
La creación de un grupo elástico puede llevar tiempo. estado de hello tootrack de las operaciones del fondo incluidos creación y las actualizaciones, utilice hello [AzureRmSqlElasticPoolActivity Get](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Obtener estado de Hola de mover una base de datos dentro y fuera de un grupo elástico
El proceso de mover bases de datos puede llevar tiempo. Realizar un seguimiento de un estado de movimiento mediante hello [AzureRmSqlDatabaseActivity Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Obtención de datos de uso de recursos para un grupo elástico
Métricas que se pueden recuperar como un porcentaje del límite de grupo de recursos de hello:

| Nombre de métrica | Descripción |
|:--- |:--- |
| cpu\_percent |Uso de proceso promedio expresado en porcentaje del límite de Hola de grupo de Hola. |
| physical\_data\_read\_percent |Uso promedio de E/S en porcentaje según Hola límite de grupo de Hola. |
| log\_write\_percent |Utilización de recursos de escritura promedio expresado en porcentaje del límite de Hola de grupo de Hola. |
| DTU\_consumption\_percent |Uso de eDTU promedio en porcentaje del límite de eDTU de grupo de Hola |
| storage\_percent |Promedio de utilización del almacenamiento de información como un porcentaje del límite de almacenamiento de Hola de grupo de Hola. |
| workers\_percent |Máximos simultáneos trabajadores (solicitudes) de porcentaje se basa en el límite de Hola de grupo de Hola. |
| sessions\_percent |Número máximo de sesiones simultáneo de porcentaje se basa en el límite de Hola de grupo de Hola. |
| eDTU_limit |Configuración de cantidad máxima de DTU de grupos elásticos actual para este grupo elástico durante este intervalo. |
| storage\_limit |Configuración de límite máximo de almacenamiento de grupos elásticos actual para este grupo elástico en megabytes durante este intervalo. |
| eDTU\_used |Edtu promedio utilizada por el grupo de hello en este intervalo. |
| storage\_used |Almacenamiento medio utilizado por el grupo de hello en este intervalo de bytes |

**Métricas de períodos de retención y granularidad:**

* Los datos se devuelven con una granularidad de 5 minutos.  
* La retención de datos es de 35 días.  

Este cmdlet y API limita el número de Hola de filas que se pueden recuperar en una llamada too1000 filas (aproximadamente 3 días de datos con granularidad de 5 minutos). Pero este comando se puede llamar varias veces con tooretrieve de intervalos de tiempo de inicio y fin diferentes más datos

métricas de Hola tooretrieve:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Obtención de datos de uso de recursos de una base de datos en un grupo elástico
Estas API son Hola igual Hola API que se usan para supervisar la utilización de recursos de Hola de una base de datos, excepto Hola después diferencia semántica: métricas recuperadas se expresan como un porcentaje de hello por Edtu de base de datos max (o cap equivalente para hello subyacente métrica como CPU o E/S) establecido para ese grupo. Por ejemplo, 50% de utilización de cualquiera de estas métricas indica que el consumo de recursos específicos de hello es en el 50% de hello por límite de base de datos para ese recurso en el grupo primario de Hola.

métricas de Hola tooretrieve:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Agregar un recurso de grupo elástico tooan alerta
Puede agregar reglas de alerta tooan grupo elástico toosend notificaciones por correo electrónico o las cadenas de alerta demasiado[puntos de conexión URL](https://msdn.microsoft.com/library/mt718036.aspx) al grupo elástico Hola alcanza un umbral de uso que configuró. Use el cmdlet de hello AzureRmMetricAlertRule agregar.

> [!IMPORTANT]
> La supervisión del uso de recursos de grupos elásticos tiene un retraso de, al menos, 5 minutos. En estos momentos, no se pueden establecer alertas de menos de 10 minutos para grupos elásticos. Las alertas establezcan para grupos elásticos con un período (parámetro denominado "-WindowSize" en la API de PowerShell) de menos de 10 minutos. no se puede desencadenar. Asegúrese de que las alertas que defina para grupos elásticos utilicen un período (WindowSize) de 10 minutos o más.
>
>

En este ejemplo se agrega una alerta para recibir una notificación cuando el consumo de eDTU de un grupo elástico supere un umbral determinado.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

Para más información, consulte cómo [crear alertas de SQL Database en Azure Portal](sql-database-insights-alerts-portal.md).

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>Agregar bases de datos de alertas tooall en un grupo elástico
Puede agregar reglas de alerta tooall base de datos en un grupo elástico toosend notificaciones por correo electrónico o las cadenas de alerta demasiado[puntos de conexión URL](https://msdn.microsoft.com/library/mt718036.aspx) cuando un recurso alcanza un umbral de utilización de configurar la alerta de Hola.

> [!IMPORTANT]
> La supervisión del uso de recursos de grupos elásticos tiene un retraso de, al menos, 5 minutos. En estos momentos, no se pueden establecer alertas de menos de 10 minutos para grupos elásticos. Las alertas establezcan para grupos elásticos con un período (parámetro denominado "-WindowSize" en la API de PowerShell) de menos de 10 minutos. no se puede desencadenar. Asegúrese de que las alertas que defina para grupos elásticos utilicen un período (WindowSize) de 10 minutos o más.
>

Este ejemplo agrega una alerta tooeach de bases de datos de hello en un grupo elástico para recibir una notificación cuando el consumo de DTU de esa base de datos está por encima de cierto umbral.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Recopilación y supervisión de los datos de uso de recursos entre varios grupos de una suscripción
Cuando se tienen muchas bases de datos en una suscripción, es toomonitor complicada cada flexible del grupo por separado. En su lugar, los cmdlets de PowerShell de base de datos SQL y las consultas de T-SQL pueden ser toocollect combinados los datos de uso de recursos de varios grupos y sus bases de datos para la supervisión y análisis de uso de recursos. A [implementación del ejemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) de este tipo de un conjunto de powershell scripts pueden encontrarse en el repositorio de ejemplos de hello GitHub SQL Server junto con documentación en lo que hace y cómo toouse lo.

toouse esta implementación de ejemplo, siga estos pasos.

1. Descargar hello [scripts y más documentación](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Modifique los scripts de Hola para su entorno. Especifique uno o más servidores en los que se alojan los grupos elásticos.
3. Especifique una base de datos de telemetría donde hello recopiladas métricas son toobe almacenado.
4. Personalizar Hola script toospecify Hola dure la ejecución de las secuencias de comandos de Hola.

En un nivel alto, las secuencias de comandos de Hola Hola siguientes:

* Enumera todos los servidores de una determinada suscripción de Azure (o una lista de servidores especificada).
* Ejecuta un trabajo en segundo plano para cada servidor. trabajo de Hola se ejecuta en un bucle a intervalos regulares y recopila los datos de telemetría para todos los grupos de hello en el servidor de Hola. A continuación, carga Hola recopilan datos en la base de datos de telemetría especificado Hola.
* Enumera la lista de bases de datos de cada datos de uso de recursos de base de datos de grupo toocollect Hola. A continuación, carga Hola recopilan datos en la base de datos de telemetría de Hola.

Hello recopilados las métricas de base de datos de telemetría de Hola pueden ser analizados toomonitor Hola Mantenimiento grupos elásticos y bases de datos de hello en ella. script de Hola también instala una función de valores de tabla (TVF) predefinida en métricas Hola agregado toohelp de base de datos de telemetría de Hola para un período de tiempo especificado. Por ejemplo, puede ser resultado de hello TVF usa tooshow "top N grupos elásticos con un uso máximo de eDTU hello en un período de tiempo determinado." Si lo desea, usar herramientas analíticas, como Excel o Power BI tooquery y analizar los datos recopilado de Hola.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Ejemplo: recuperación de métricas de consumo de recursos de un grupo elástico y de sus bases de datos
Este ejemplo recupera las métricas de consumo de Hola para un determinado grupo elástico y todas sus bases de datos. Los datos recopilados es el formato y escritos el archivo con formato .csv de tooa. se pueden examinar el archivo Hello con Excel.

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a>Latencia de las operaciones de grupos elásticos
* Cambiar normalmente Hola min Edtu por base de datos o el número máximo de Edtu por base de datos completa en 5 minutos o menos.
* Cambiar hello Edtu por grupo de depende de la cantidad total de Hola de espacio utilizado por todas las bases de datos de grupo de Hola. Los cambios tienen un duración media de 90 minutos o menos por cada 100 GB. Por ejemplo, si utiliza el espacio total de Hola por todas las bases de datos de grupo de hello es de 200 GB, Hola espera latencia para cambiar hello eDTU del grupo por grupo es de 3 horas o menos.



## <a name="next-steps"></a>Pasos siguientes
* [Crear trabajos elásticos](sql-database-elastic-jobs-overview.md) trabajos elásticos le permiten ejecutar scripts T-SQL en cualquier número de bases de datos de grupo de Hola.
* Vea [escalado horizontal con base de datos de SQL Azure](sql-database-elastic-scale-introduction.md): usar herramientas elásticas tooscale out, mover los datos, consultar o crear las transacciones.
