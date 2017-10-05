---
title: "Ejemplo de PowerShell para configurar la replicación geográfica activa para una instancia única de Azure SQL Database | Microsoft Docs"
description: "Script de ejemplo de Azure PowerShell para configurar la replicación geográfica activa para una instancia única de Azure SQL Database"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: b25bc02acda7905cd4c08bbafee1d9b29907d332
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="635ee-103">Use PowerShell para configurar la replicación geográfica activa para una instancia única de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="635ee-103">Use PowerShell to configure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="635ee-104">En este ejemplo de script de PowerShell se configura una replicación geográfica activa para una única instancia de Azure SQL Database y se conmuta por error a una réplica secundaria de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="635ee-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="635ee-105">Scripts de ejemplo</span><span class="sxs-lookup"><span data-stu-id="635ee-105">Sample scripts</span></span>

<span data-ttu-id="635ee-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Configuración de la replicación geográfica activa para una base de datos única")]</span><span class="sxs-lookup"><span data-stu-id="635ee-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="635ee-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="635ee-107">Clean up deployment</span></span>

<span data-ttu-id="635ee-108">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="635ee-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="635ee-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="635ee-109">Script explanation</span></span>

<span data-ttu-id="635ee-110">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="635ee-110">This script uses the following commands.</span></span> <span data-ttu-id="635ee-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="635ee-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="635ee-112">Comando</span><span class="sxs-lookup"><span data-stu-id="635ee-112">Command</span></span> | <span data-ttu-id="635ee-113">Notas</span><span class="sxs-lookup"><span data-stu-id="635ee-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="635ee-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="635ee-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="635ee-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="635ee-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="635ee-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="635ee-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="635ee-117">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="635ee-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="635ee-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="635ee-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="635ee-119">Crea un grupo elástico en un servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="635ee-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="635ee-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="635ee-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="635ee-121">Actualiza las propiedades de la base de datos o traslada una base de datos a un grupo elástico, fuera de este o entre grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="635ee-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="635ee-122">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="635ee-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="635ee-123">Crea una base de datos secundaria para una base de datos existente e inicia la replicación de datos.</span><span class="sxs-lookup"><span data-stu-id="635ee-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="635ee-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="635ee-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="635ee-125">Obtiene una o más bases de datos.</span><span class="sxs-lookup"><span data-stu-id="635ee-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="635ee-126">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="635ee-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="635ee-127">Convierte una base de datos secundaria en principal para iniciar la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="635ee-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="635ee-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="635ee-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="635ee-129">Obtiene los vínculos de replicación geográfica entre una Base de datos SQL de Azure y un grupo de recursos o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="635ee-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="635ee-130">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="635ee-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="635ee-131">Finaliza una replicación de datos entre una base de datos SQL y la base de datos secundaria especificada.</span><span class="sxs-lookup"><span data-stu-id="635ee-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="635ee-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="635ee-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="635ee-133">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="635ee-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="635ee-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="635ee-134">Next steps</span></span>

<span data-ttu-id="635ee-135">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="635ee-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="635ee-136">Encontrará más ejemplos de scripts de PowerShell de SQL Database en los [scripts de PowerShell de Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="635ee-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
