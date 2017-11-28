---
title: "Ejemplo de PowerShell para trasladar una base de datos SQL de Azure a un grupo elástico de SQL | Microsoft Docs"
description: "Ejemplo de Azure PowerShell para trasladar una base de datos SQL entre grupos elásticos mediante PowerShell"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 58f14dc668f25f17e93fcaf30f72b15a46d71484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-create-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="a4895-103">Uso de PowerShell para crear grupos elásticos y trasladar bases de datos entre grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="a4895-103">Use PowerShell to create elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="a4895-104">Este script de ejemplo de PowerShell crea dos grupos elásticos, traslada una base de datos de un grupo elástico a otro y, a continuación, traslada una base de datos fuera de un grupo elástico a un nivel de rendimiento de base de datos única.</span><span class="sxs-lookup"><span data-stu-id="a4895-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="a4895-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a4895-105">Sample script</span></span>

<span data-ttu-id="a4895-106">[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Traslado de una base de datos de un grupo a otro")]</span><span class="sxs-lookup"><span data-stu-id="a4895-106">[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a4895-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="a4895-107">Clean up deployment</span></span>

<span data-ttu-id="a4895-108">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="a4895-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="a4895-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="a4895-109">Script explanation</span></span>

<span data-ttu-id="a4895-110">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="a4895-110">This script uses the following commands.</span></span> <span data-ttu-id="a4895-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="a4895-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a4895-112">Comando</span><span class="sxs-lookup"><span data-stu-id="a4895-112">Command</span></span> | <span data-ttu-id="a4895-113">Notas</span><span class="sxs-lookup"><span data-stu-id="a4895-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a4895-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a4895-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a4895-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="a4895-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a4895-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="a4895-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="a4895-117">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="a4895-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="a4895-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="a4895-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="a4895-119">Crea un grupo elástico en un servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="a4895-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="a4895-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a4895-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="a4895-121">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="a4895-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="a4895-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="a4895-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="a4895-123">Actualiza las propiedades de la base de datos o traslada una base de datos a un grupo elástico, fuera de este o entre grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="a4895-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="a4895-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a4895-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a4895-125">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="a4895-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="a4895-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4895-126">Next steps</span></span>

<span data-ttu-id="a4895-127">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4895-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a4895-128">Encontrará más ejemplos de scripts de PowerShell de SQL Database en los [scripts de PowerShell de Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a4895-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
