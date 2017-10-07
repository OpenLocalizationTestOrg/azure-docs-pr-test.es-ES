---
title: "Azure PowerShell: Creación de una instancia de SQL Database | Microsoft Docs"
description: "Obtenga información acerca de cómo toocreate un servidor lógico de la base de datos SQL, regla de firewall de nivel de servidor y bases de datos de Hola portal de Azure."
keywords: "tutorial de sql database, creación de una base de datos sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a>Creación de una sola instancia de Azure SQL Database con PowerShell

PowerShell es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts. Esta guía de detalles mediante PowerShell toodeploy una base de datos de SQL Azure en un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) en un [servidor lógico de base de datos de SQL Azure](sql-database-features.md).

Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.

Este tutorial requiere hello Azure PowerShell versión 4.0 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps). 

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure

Inicie sesión en tooyour suscripción de Azure con hello [AzureRmAccount agregar](/powershell/module/azurerm.profile/add-azurermaccount) comando y siga hello en pantalla instrucciones.

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a>Creación de variables

Definir variables para su uso en scripts de hello en esta guía de inicio rápido.

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) con hello [AzureRmResourceGroup New](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando. Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo. Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westeurope` ubicación.

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a>un servidor lógico

Crear un [servidor lógico de base de datos de SQL Azure](sql-database-features.md) con hello [AzureRmSqlServer New](/powershell/module/azurerm.sql/new-azurermsqlserver) comando. Un servidor lógico contiene un conjunto de bases de datos administradas como un grupo. Hello en el ejemplo siguiente se crea un servidor de forma aleatoria con nombre en el grupo de recursos con un inicio de sesión de administración denominado `ServerAdmin` y una contraseña de `ChangeYourAdminPassword1`. Cambie estos valores predefinidos por los que prefiera.

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a>Configuración de una regla de firewall del servidor

Crear un [regla de firewall de nivel de servidor de base de datos de SQL Azure](sql-database-firewall-configure.md) con hello [AzureRmSqlServerFirewallRule New](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) comando. Una regla de firewall de nivel de servidor permite que una aplicación externa, como SQL Server Management Studio o hello SQLCMD utilidad tooconnect tooa base de datos SQL a través de firewall de servicio de base de datos SQL de Hola. En el siguiente ejemplo de Hola, solo se abrirá el firewall de Hola para otros recursos de Azure. tooenable conectividad externa, cambio Hola IP dirección tooan dirección adecuada para su entorno. tooopen todas las direcciones IP, utilice 0.0.0.0 como Hola a partir de dirección IP y 255.255.255.255 como Hola dirección final.

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> SQL Database se comunica a través del puerto 1433. Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 1433. Si es así, no será capaz de tooconnect tooyour base de datos de SQL Azure servidor a menos que el departamento de TI abre el puerto 1433.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Crear una base de datos en el servidor de hello con datos de ejemplo

Crear una base de datos con un [nivel de rendimiento S0](sql-database-service-tiers.md) en servidor de hello mediante Hola [AzureRmSqlDatabase New](/powershell/module/azurerm.sql/new-azurermsqldatabase) comando. Hello en el ejemplo siguiente se crea una base de datos denominada `mySampleDatabase` y carga Hola datos de ejemplo AdventureWorksLT en esta base de datos. Reemplazar predefinidos de estos valores según sea necesario (otras guías rápidas en esta colección se basan en valores de hello en esta guía de inicio rápido).

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a>Limpieza de recursos

Otras guías de inicio rápido de esta colección se basan en los valores de esta. 

> [!TIP]
> Si tiene previsto toocontinue toowork con guías rápidas posteriores, no limpiar los recursos de hello creados en esta rápida se inician. Si no tiene previsto toocontinue, use Hola seguido toodelete pasos creado todos los recursos de esta guía de inicio rápido en hello portal de Azure.
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene una base de datos, puede conectarse y realizar consultas con las herramientas que desee. Para más información, seleccione una de las herramientas siguientes:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [código de Visual Studio](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

