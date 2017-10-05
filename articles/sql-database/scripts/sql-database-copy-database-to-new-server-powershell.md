---
title: Ejemplo de PowerShell para copiar una instancia de Azure SQL Database en un servidor nuevo | Microsoft Docs
description: Script de ejemplo de Azure PowerShell para copiar una instancia de SQL Database en un servidor nuevo
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 005ea2e782f8e1cff29f743d9584eb2af2c77509
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-copy-a-sql-database-to-a-new-server"></a><span data-ttu-id="20e97-103">Uso de PowerShell para copiar una instancia de SQL Database en un servidor nuevo</span><span class="sxs-lookup"><span data-stu-id="20e97-103">Use PowerShell to copy a SQL database to a new server</span></span>

<span data-ttu-id="20e97-104">Este ejemplo de script de PowerShell crea una copia de una base de datos existente en un nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="20e97-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-to-a-new-server"></a><span data-ttu-id="20e97-105">Copia de una base de datos en un nuevo servidor</span><span class="sxs-lookup"><span data-stu-id="20e97-105">Copy a database to a new server</span></span>

<span data-ttu-id="20e97-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copia de una base de datos en un nuevo servidor")]</span><span class="sxs-lookup"><span data-stu-id="20e97-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database to new server")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="20e97-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="20e97-107">Clean up deployment</span></span>

<span data-ttu-id="20e97-108">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="20e97-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="20e97-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="20e97-109">Script explanation</span></span>

<span data-ttu-id="20e97-110">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="20e97-110">This script uses the following commands.</span></span> <span data-ttu-id="20e97-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="20e97-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="20e97-112">Comando</span><span class="sxs-lookup"><span data-stu-id="20e97-112">Command</span></span> | <span data-ttu-id="20e97-113">Notas</span><span class="sxs-lookup"><span data-stu-id="20e97-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="20e97-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="20e97-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="20e97-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="20e97-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="20e97-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="20e97-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="20e97-117">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="20e97-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="20e97-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="20e97-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="20e97-119">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="20e97-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="20e97-120">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="20e97-120">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="20e97-121">Crea una copia de una base de datos que utiliza la instantánea en el momento actual.</span><span class="sxs-lookup"><span data-stu-id="20e97-121">Creates a copy of a database that uses the snapshot at the current time.</span></span> |
| [<span data-ttu-id="20e97-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="20e97-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="20e97-123">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="20e97-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="20e97-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="20e97-124">Next steps</span></span>

<span data-ttu-id="20e97-125">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="20e97-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="20e97-126">Encontrará más ejemplos de scripts de PowerShell de SQL Database en los [scripts de PowerShell de Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="20e97-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
