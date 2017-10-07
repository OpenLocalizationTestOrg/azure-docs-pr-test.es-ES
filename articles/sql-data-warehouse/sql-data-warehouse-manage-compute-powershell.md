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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="0258c-105">Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="0258c-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0258c-106">Información general</span><span class="sxs-lookup"><span data-stu-id="0258c-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="0258c-107">Portal</span><span class="sxs-lookup"><span data-stu-id="0258c-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="0258c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0258c-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="0258c-109">REST</span><span class="sxs-lookup"><span data-stu-id="0258c-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="0258c-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="0258c-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="0258c-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="0258c-111">Before you begin</span></span>
### <a name="install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="0258c-112">Instalar la versión más reciente de Hola de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="0258c-112">Install hello latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="0258c-113">toouse PowerShell de Azure con el almacenamiento de datos de SQL, necesita Azure PowerShell versión 1.0.3 o mayor.</span><span class="sxs-lookup"><span data-stu-id="0258c-113">toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="0258c-114">su versión actual de tooverify ejecutar comando hello **Get-Module - ListAvailable-Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="0258c-114">tooverify your current version run hello command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="0258c-115">Puede instalar la versión más reciente de Hola de [instalador de plataforma Web de Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="0258c-115">You can install hello latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="0258c-116">Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="0258c-116">For more information, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="0258c-117">Introducción a los cmdlets de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0258c-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="0258c-118">tooget iniciado:</span><span class="sxs-lookup"><span data-stu-id="0258c-118">tooget started:</span></span>

1. <span data-ttu-id="0258c-119">Abra Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0258c-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="0258c-120">En el símbolo del sistema de PowerShell hello, ejecute estos comandos toosign en toohello Azure Resource Manager y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="0258c-120">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="0258c-121">Escalado de la potencia de proceso</span><span class="sxs-lookup"><span data-stu-id="0258c-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="0258c-122">Hola toochange a Dwu, usar hello [conjunto AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0258c-122">toochange hello DWUs, use hello [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="0258c-123">Hello en el ejemplo siguiente se establece tooDW1000 objetivo de hello servicio nivel de base de datos de hello MySQLDW que se hospeda en el servidor MyServer.</span><span class="sxs-lookup"><span data-stu-id="0258c-123">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="0258c-124">Pausa del proceso</span><span class="sxs-lookup"><span data-stu-id="0258c-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="0258c-125">toopause una base de datos, usar hello [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0258c-125">toopause a database, use hello [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="0258c-126">Hello en el ejemplo siguiente se pausa una base de datos denominada Database02 hospedado en un servidor denominado Server01.</span><span class="sxs-lookup"><span data-stu-id="0258c-126">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="0258c-127">servidor Hello está en un grupo de recursos de Azure denominado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="0258c-127">hello server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="0258c-128">Tenga en cuenta que si el servidor es foo.database.windows.net, utilice "foo" como Hola - ServerName hello en cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0258c-128">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="0258c-129">Una variación, en el ejemplo siguiente se recupera la base de datos de Hola en objeto hello $database.</span><span class="sxs-lookup"><span data-stu-id="0258c-129">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="0258c-130">A continuación, canaliza el objeto de hello demasiado[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="0258c-130">It then pipes hello object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="0258c-131">Hola resultados se almacenan en hello objeto resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="0258c-131">hello results are stored in hello object resultDatabase.</span></span> <span data-ttu-id="0258c-132">comando final Hello muestra resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="0258c-132">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="0258c-133">Reanudación del proceso</span><span class="sxs-lookup"><span data-stu-id="0258c-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="0258c-134">toostart una base de datos, usar hello [reanudar AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0258c-134">toostart a database, use hello [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="0258c-135">Hello en el ejemplo siguiente se inicia una base de datos denominada Database02 hospedado en un servidor denominado Server01.</span><span class="sxs-lookup"><span data-stu-id="0258c-135">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="0258c-136">servidor Hello está en un grupo de recursos de Azure denominado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="0258c-136">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="0258c-137">Una variación, en el ejemplo siguiente se recupera la base de datos de Hola en objeto hello $database.</span><span class="sxs-lookup"><span data-stu-id="0258c-137">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="0258c-138">A continuación, canaliza el objeto de hello demasiado[reanudar AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] y almacena los resultados de hello en $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="0258c-138">It then pipes hello object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores hello results in $resultDatabase.</span></span> <span data-ttu-id="0258c-139">comando final Hello muestra resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="0258c-139">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="0258c-140">Comprobar el estado de la base de datos</span><span class="sxs-lookup"><span data-stu-id="0258c-140">Check database state</span></span>

<span data-ttu-id="0258c-141">Como se muestra en hello por encima de los ejemplos, se pueden usar [Get AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet tooget información en una base de datos, por tanto, la comprobación de estado de hello, sino también toouse como un argumento.</span><span class="sxs-lookup"><span data-stu-id="0258c-141">As shown in hello above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet tooget information on a database, thereby checking hello status, but also toouse as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="0258c-142">El resultado será similar a este:</span><span class="sxs-lookup"><span data-stu-id="0258c-142">Which will result in something like</span></span> 

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

<span data-ttu-id="0258c-143">Donde, a continuación, puede comprobar hello toosee *estado* de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0258c-143">Where you can then check toosee hello *Status* of hello database.</span></span> <span data-ttu-id="0258c-144">En este caso, puede ver esta base de datos está en línea.</span><span class="sxs-lookup"><span data-stu-id="0258c-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="0258c-145">Al ejecutar este comando, debería recibir uno de los siguientes valores de Estado: Con conexión, Pausando, Resuming, Escalando y En pausa.</span><span class="sxs-lookup"><span data-stu-id="0258c-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="0258c-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0258c-146">Next steps</span></span>
<span data-ttu-id="0258c-147">Para otras tareas de administración, consulte [Información general de administración][Management overview].</span><span class="sxs-lookup"><span data-stu-id="0258c-147">For other management tasks, see [Management overview][Management overview].</span></span>

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
