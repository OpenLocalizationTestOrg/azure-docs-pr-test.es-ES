---
title: Cmdlets de PowerShell para Almacenamiento de datos SQL de Azure
description: Busque los principales cmdlets de PowerShell para Almacenamiento de datos SQL de Azure, incluidos aquellos para pausar y reanudar una base de datos.
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
ms.openlocfilehash: ce3e11587c2e0cb92923868a4f26d7f59c7ef4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="497fd-103">Cmdlets de PowerShell y API de REST para Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="497fd-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="497fd-104">Muchas tareas de administración de Almacenamiento de datos SQL se pueden administrar mediante los cmdlets de Azure PowerShell o las API de REST.</span><span class="sxs-lookup"><span data-stu-id="497fd-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="497fd-105">A continuación se muestran algunos ejemplos de cómo usar comandos de PowerShell para automatizar tareas comunes en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="497fd-105">Below are some examples of how to use PowerShell commands to automate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="497fd-106">Para ver algunos buenos ejemplos de REST, consulte el artículo [Administración de la potencia de proceso en SQL Data Warehouse de Azure (REST)][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="497fd-106">For some good REST examples, see the article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="497fd-107">Para usar Azure PowerShell con Almacenamiento de datos SQL, es necesaria la versión 1.0.3 o posterior de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="497fd-107">In order to use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="497fd-108">Puede comprobar la versión ejecutando **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="497fd-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="497fd-109">Se puede instalar la versión más reciente desde el [Instalador de plataforma web de Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="497fd-109">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="497fd-110">Para más información sobre cómo instalar la versión más reciente, consulte [Cómo instalar y configurar Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="497fd-110">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="497fd-111">Introducción a los cmdlets de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="497fd-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="497fd-112">Abra Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="497fd-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="497fd-113">En el símbolo del sistema de PowerShell, ejecute estos comandos para iniciar sesión en Azure Resource Manager y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="497fd-113">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="497fd-114">Ejemplo de pausa de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="497fd-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="497fd-115">Pausa una base de datos denominada "Database02" que está hospedada en un servidor cuyo nombre es "Server01".</span><span class="sxs-lookup"><span data-stu-id="497fd-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="497fd-116">El servidor está en un grupo de recursos de Azure denominado "ResourceGroup1."</span><span class="sxs-lookup"><span data-stu-id="497fd-116">The server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="497fd-117">Este ejemplo, que es una variación, canaliza el objeto recuperado a [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="497fd-117">A variation, this example pipes the retrieved object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="497fd-118">El resultado es que se pausa la base de datos.</span><span class="sxs-lookup"><span data-stu-id="497fd-118">As a result, the database is paused.</span></span> <span data-ttu-id="497fd-119">El comando final muestra los resultados.</span><span class="sxs-lookup"><span data-stu-id="497fd-119">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="497fd-120">Ejemplo de inicio de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="497fd-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="497fd-121">Reanuda el funcionamiento de una base de datos denominada "Database02" que está hospedada en un servidor cuyo nombre es "Server01".</span><span class="sxs-lookup"><span data-stu-id="497fd-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="497fd-122">El servidor está en un grupo de recursos denominado "ResourceGroup1."</span><span class="sxs-lookup"><span data-stu-id="497fd-122">The server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="497fd-123">Este ejemplo, que es una variación, recupera una base de datos denominada "Database02" desde un servidor cuyo nombre es "Server01" que está incluido en un grupo de recursos denominado "ResourceGroup1".</span><span class="sxs-lookup"><span data-stu-id="497fd-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="497fd-124">Canaliza el objeto recuperado a [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="497fd-124">It pipes the retrieved object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="497fd-125">Tenga en cuenta que si el servidor es foo.database.windows.net, debe usar "foo" como -ServerName en los cmdlets de Powershell.</span><span class="sxs-lookup"><span data-stu-id="497fd-125">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="497fd-126">Otros cmdlets de PowerShell admitidos</span><span class="sxs-lookup"><span data-stu-id="497fd-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="497fd-127">Estos cmdlets de PowerShell se admiten en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="497fd-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="497fd-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="497fd-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="497fd-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="497fd-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="497fd-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="497fd-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="497fd-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="497fd-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="497fd-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="497fd-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="497fd-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="497fd-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="497fd-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="497fd-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="497fd-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="497fd-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="497fd-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="497fd-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="497fd-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="497fd-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="497fd-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="497fd-138">Next steps</span></span>
<span data-ttu-id="497fd-139">Para obtener más ejemplos de PowerShell, consulte:</span><span class="sxs-lookup"><span data-stu-id="497fd-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="497fd-140">[Creación de SQL Data Warehouse con PowerShell][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="497fd-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="497fd-141">[Restauración de base de datos][Database restore]</span><span class="sxs-lookup"><span data-stu-id="497fd-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="497fd-142">Para conocer otras tareas que se pueden automatizar con PowerShell, consulte los [cmdlets de Azure SQL Database][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="497fd-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="497fd-143">Tenga en cuenta que no todos los cmdlets de Azure SQL Database se admiten para Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="497fd-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="497fd-144">Para ver una lista de todas las tareas que se pueden automatizar con PowerShell, consulte [Operaciones para bases de datos SQL de Azure][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="497fd-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

<!--Image references-->

<!--Article references-->
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points to Select-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
