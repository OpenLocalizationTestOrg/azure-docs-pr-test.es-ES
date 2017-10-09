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
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="81b80-103">Cmdlets de PowerShell y API de REST para Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="81b80-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="81b80-104">Muchas tareas de administración de Almacenamiento de datos SQL se pueden administrar mediante los cmdlets de Azure PowerShell o las API de REST.</span><span class="sxs-lookup"><span data-stu-id="81b80-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="81b80-105">A continuación se muestran algunos ejemplos de cómo toouse PowerShell comandos tooautomate tareas comunes en el almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="81b80-105">Below are some examples of how toouse PowerShell commands tooautomate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="81b80-106">Para algunos buenos ejemplos REST, vea el artículo de hello [administrar escalabilidad con REST][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="81b80-106">For some good REST examples, see hello article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="81b80-107">En orden toouse PowerShell de Azure con el almacenamiento de datos de SQL, necesita Azure PowerShell versión 1.0.3 o mayor.</span><span class="sxs-lookup"><span data-stu-id="81b80-107">In order toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="81b80-108">Puede comprobar la versión ejecutando **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="81b80-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="81b80-109">se puede instalar la versión más reciente de Hola desde [instalador de plataforma Web de Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="81b80-109">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="81b80-110">Para obtener más información acerca de cómo instalar la versión más reciente de hello, consulte [cómo tooinstall y configurar Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="81b80-110">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="81b80-111">Introducción a los cmdlets de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="81b80-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="81b80-112">Abra Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81b80-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="81b80-113">En el símbolo del sistema de PowerShell hello, ejecute estos comandos toosign en toohello Azure Resource Manager y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="81b80-113">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="81b80-114">Ejemplo de pausa de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="81b80-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="81b80-115">Pausa una base de datos denominada "Database02" que está hospedada en un servidor cuyo nombre es "Server01".</span><span class="sxs-lookup"><span data-stu-id="81b80-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="81b80-116">servidor de Hola se encuentra en un grupo de recursos de Azure denominado "ResourceGroup1."</span><span class="sxs-lookup"><span data-stu-id="81b80-116">hello server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="81b80-117">Una variación, este ejemplo canaliza Hola recuperar objeto demasiado[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="81b80-117">A variation, this example pipes hello retrieved object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="81b80-118">Como resultado, la base de datos de hello está en pausa.</span><span class="sxs-lookup"><span data-stu-id="81b80-118">As a result, hello database is paused.</span></span> <span data-ttu-id="81b80-119">comando final Hello muestra resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="81b80-119">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="81b80-120">Ejemplo de inicio de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="81b80-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="81b80-121">Reanuda el funcionamiento de una base de datos denominada "Database02" que está hospedada en un servidor cuyo nombre es "Server01".</span><span class="sxs-lookup"><span data-stu-id="81b80-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="81b80-122">servidor de Hola se encuentra en un grupo de recursos denominado "ResourceGroup1."</span><span class="sxs-lookup"><span data-stu-id="81b80-122">hello server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="81b80-123">Este ejemplo, que es una variación, recupera una base de datos denominada "Database02" desde un servidor cuyo nombre es "Server01" que está incluido en un grupo de recursos denominado "ResourceGroup1".</span><span class="sxs-lookup"><span data-stu-id="81b80-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="81b80-124">Canaliza el objeto de hello recuperar demasiado[reanudar AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="81b80-124">It pipes hello retrieved object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="81b80-125">Tenga en cuenta que si el servidor es foo.database.windows.net, utilice "foo" como Hola - ServerName hello en cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81b80-125">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="81b80-126">Otros cmdlets de PowerShell admitidos</span><span class="sxs-lookup"><span data-stu-id="81b80-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="81b80-127">Estos cmdlets de PowerShell se admiten en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81b80-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="81b80-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="81b80-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="81b80-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="81b80-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="81b80-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="81b80-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="81b80-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="81b80-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="81b80-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="81b80-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="81b80-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="81b80-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="81b80-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="81b80-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="81b80-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="81b80-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="81b80-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="81b80-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="81b80-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="81b80-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="81b80-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="81b80-138">Next steps</span></span>
<span data-ttu-id="81b80-139">Para obtener más ejemplos de PowerShell, consulte:</span><span class="sxs-lookup"><span data-stu-id="81b80-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="81b80-140">[Creación de SQL Data Warehouse con PowerShell][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="81b80-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="81b80-141">[Restauración de base de datos][Database restore]</span><span class="sxs-lookup"><span data-stu-id="81b80-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="81b80-142">Para conocer otras tareas que se pueden automatizar con PowerShell, consulte los [cmdlets de Azure SQL Database][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="81b80-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="81b80-143">Tenga en cuenta que no todos los cmdlets de Azure SQL Database se admiten para Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81b80-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="81b80-144">Para ver una lista de todas las tareas que se pueden automatizar con PowerShell, consulte [Operaciones para bases de datos SQL de Azure][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="81b80-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

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
