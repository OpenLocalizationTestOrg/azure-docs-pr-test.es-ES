---
title: "aaaPause, reanudar, escalar con REST en el almacén de datos de SQL de Azure | Documentos de Microsoft"
description: Administre la potencia de proceso en SQL Data Warehouse mediante REST, T-SQL y PowerShell.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 21de7337-9356-49bb-a6eb-06c1beeba2c4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 07/25/2017
ms.author: elbutter
ms.openlocfilehash: fc867febb118fb5c86c2637a41b232076021b95d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a><span data-ttu-id="ce37e-103">Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (REST)</span><span class="sxs-lookup"><span data-stu-id="ce37e-103">Manage compute power in Azure SQL Data Warehouse (REST)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce37e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ce37e-104">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="ce37e-105">Portal</span><span class="sxs-lookup"><span data-stu-id="ce37e-105">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="ce37e-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce37e-106">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="ce37e-107">REST</span><span class="sxs-lookup"><span data-stu-id="ce37e-107">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="ce37e-108">TSQL</span><span class="sxs-lookup"><span data-stu-id="ce37e-108">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="ce37e-109">Escalado de la potencia de proceso</span><span class="sxs-lookup"><span data-stu-id="ce37e-109">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="ce37e-110">Hola toochange a Dwu, usar hello [crear o actualizar base de datos] [ Create or Update Database] API de REST.</span><span class="sxs-lookup"><span data-stu-id="ce37e-110">toochange hello DWUs, use hello [Create or Update Database][Create or Update Database] REST API.</span></span> <span data-ttu-id="ce37e-111">Hello en el ejemplo siguiente se establece tooDW1000 objetivo de hello servicio nivel de base de datos de hello MySQLDW que se hospeda en el servidor MyServer.</span><span class="sxs-lookup"><span data-stu-id="ce37e-111">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span> <span data-ttu-id="ce37e-112">servidor Hello está en un grupo de recursos de Azure denominado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="ce37e-112">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
PATCH https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01-preview HTTP/1.1
Content-Type: application/json; charset=UTF-8

{
    "properties": {
        "requestedServiceObjectiveName": DW1000
    }
}
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="ce37e-113">Pausa del proceso</span><span class="sxs-lookup"><span data-stu-id="ce37e-113">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="ce37e-114">toopause una base de datos, usar hello [base de datos de pausa] [ Pause Database] API de REST.</span><span class="sxs-lookup"><span data-stu-id="ce37e-114">toopause a database, use hello [Pause Database][Pause Database] REST API.</span></span> <span data-ttu-id="ce37e-115">Hello en el ejemplo siguiente se pausa una base de datos denominada Database02 hospedado en un servidor denominado Server01.</span><span class="sxs-lookup"><span data-stu-id="ce37e-115">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="ce37e-116">servidor Hello está en un grupo de recursos de Azure denominado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="ce37e-116">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="ce37e-117">Reanudación del proceso</span><span class="sxs-lookup"><span data-stu-id="ce37e-117">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="ce37e-118">toostart una base de datos, usar hello [base de datos de reanudación] [ Resume Database] API de REST.</span><span class="sxs-lookup"><span data-stu-id="ce37e-118">toostart a database, use hello [Resume Database][Resume Database] REST API.</span></span> <span data-ttu-id="ce37e-119">Hello en el ejemplo siguiente se inicia una base de datos denominada Database02 hospedado en un servidor denominado Server01.</span><span class="sxs-lookup"><span data-stu-id="ce37e-119">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="ce37e-120">servidor Hello está en un grupo de recursos de Azure denominado ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="ce37e-120">hello server is in an Azure resource group named ResourceGroup1.</span></span> 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a><span data-ttu-id="ce37e-121">Comprobar el estado de la base de datos</span><span class="sxs-lookup"><span data-stu-id="ce37e-121">Check database state</span></span>

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="ce37e-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce37e-122">Next steps</span></span>
<span data-ttu-id="ce37e-123">Para otras tareas de administración, consulte [Información general de administración][Management overview].</span><span class="sxs-lookup"><span data-stu-id="ce37e-123">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Pause Database]: https://msdn.microsoft.com/library/azure/mt718817.aspx
[Resume Database]: https://msdn.microsoft.com/library/azure/mt718820.aspx
[Create or Update Database]: https://msdn.microsoft.com/library/azure/mt163685.aspx

<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
