---
title: Ejemplo de PowerShell para restaurar una instancia de Azure SQL Database a partir de una copia de seguridad | Microsoft Docs
description: "Script de ejemplo de Azure PowerShell para restaurar una instancia de Azure SQL Database a partir de copias de seguridad con redundancia geográfica"
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
ms.openlocfilehash: ae1d0c828ae1e7e1e7e07dcc7d6157187a3859d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-restore-an-azure-sql-database-from-backups"></a><span data-ttu-id="ec65f-103">Uso de PowerShell para restaurar una instancia de Azure SQL Database a partir de copias de seguridad</span><span class="sxs-lookup"><span data-stu-id="ec65f-103">Use PowerShell to restore an Azure SQL database from backups</span></span>

<span data-ttu-id="ec65f-104">Este script de PowerShell restaura una instancia de Azure SQL Database desde una copia de seguridad con redundancia geográfica y restaura una instancia de Azure SQL Database eliminada a la copia de seguridad más reciente y restaura una instancia de Azure SQL Database a un momento dado.</span><span class="sxs-lookup"><span data-stu-id="ec65f-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database to its latest backup, and restores an Azure SQL database to a specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="ec65f-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ec65f-105">Sample script</span></span>

<span data-ttu-id="ec65f-106">[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Creación de una base de datos SQL")]</span><span class="sxs-lookup"><span data-stu-id="ec65f-106">[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ec65f-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="ec65f-107">Clean up deployment</span></span>

<span data-ttu-id="ec65f-108">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="ec65f-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="ec65f-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="ec65f-109">Script explanation</span></span>

<span data-ttu-id="ec65f-110">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="ec65f-110">This script uses the following commands.</span></span> <span data-ttu-id="ec65f-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="ec65f-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ec65f-112">Comando</span><span class="sxs-lookup"><span data-stu-id="ec65f-112">Command</span></span> | <span data-ttu-id="ec65f-113">Notas</span><span class="sxs-lookup"><span data-stu-id="ec65f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ec65f-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ec65f-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="ec65f-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="ec65f-115">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="ec65f-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="ec65f-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="ec65f-117">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="ec65f-117">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="ec65f-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ec65f-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="ec65f-119">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="ec65f-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="ec65f-120">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="ec65f-120">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="ec65f-121">Obtiene una copia de seguridad con redundancia geográfica de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="ec65f-121">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="ec65f-122">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ec65f-122">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="ec65f-123">Restaura una Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="ec65f-123">Restores a SQL database.</span></span> |
|[<span data-ttu-id="ec65f-124">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ec65f-124">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="ec65f-125">Eliminación de una instancia de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ec65f-125">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="ec65f-126">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="ec65f-126">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="ec65f-127">Obtiene una base de datos eliminada que se puede restaurar.</span><span class="sxs-lookup"><span data-stu-id="ec65f-127">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="ec65f-128">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ec65f-128">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ec65f-129">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="ec65f-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ec65f-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ec65f-130">Next steps</span></span>

<span data-ttu-id="ec65f-131">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ec65f-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ec65f-132">Encontrará más ejemplos de scripts de PowerShell de SQL Database en los [scripts de PowerShell de Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ec65f-132">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
