---
title: base de datos SQL aaaPowerShell ejemplo restaurar copia de seguridad Azure | Documentos de Microsoft
description: "Azure toorestore de secuencia de comandos de ejemplo de PowerShell una base de datos de SQL Azure desde las copias de seguridad con redundancia geográfica"
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
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="be92a-103">Usar PowerShell toorestore una base de datos de SQL Azure desde las copias de seguridad</span><span class="sxs-lookup"><span data-stu-id="be92a-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="be92a-104">En este ejemplo de secuencia de comandos de PowerShell restaura una base de datos de SQL Azure desde una copia de seguridad con redundancia geográfica, restaura un eliminado SQL Azure base de datos tooits última copia de seguridad y restaura un punto específico de la tooa de base de datos SQL de Azure en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="be92a-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="be92a-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="be92a-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="be92a-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="be92a-106">Clean up deployment</span></span>

<span data-ttu-id="be92a-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="be92a-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="be92a-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="be92a-108">Script explanation</span></span>

<span data-ttu-id="be92a-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="be92a-109">This script uses hello following commands.</span></span> <span data-ttu-id="be92a-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="be92a-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="be92a-111">Comando</span><span class="sxs-lookup"><span data-stu-id="be92a-111">Command</span></span> | <span data-ttu-id="be92a-112">Notas</span><span class="sxs-lookup"><span data-stu-id="be92a-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="be92a-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="be92a-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="be92a-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="be92a-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="be92a-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="be92a-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="be92a-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="be92a-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="be92a-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="be92a-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="be92a-118">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="be92a-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="be92a-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="be92a-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="be92a-120">Obtiene una copia de seguridad con redundancia geográfica de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="be92a-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="be92a-121">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="be92a-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="be92a-122">Restaura una Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="be92a-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="be92a-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="be92a-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="be92a-124">Eliminación de una instancia de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="be92a-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="be92a-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="be92a-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="be92a-126">Obtiene una base de datos eliminada que se puede restaurar.</span><span class="sxs-lookup"><span data-stu-id="be92a-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="be92a-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="be92a-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="be92a-128">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="be92a-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="be92a-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be92a-129">Next steps</span></span>

<span data-ttu-id="be92a-130">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="be92a-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="be92a-131">Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="be92a-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
