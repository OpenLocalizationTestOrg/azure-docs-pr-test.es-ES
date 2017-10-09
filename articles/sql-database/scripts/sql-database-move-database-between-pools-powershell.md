---
title: "grupo elástico de aaaPowerShell ejemplo move SQL de Azure SQL de la base de datos | Documentos de Microsoft"
description: "Azure toomove de script de ejemplo de PowerShell una base de datos SQL entre grupos elásticos con PowerShell"
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
ms.openlocfilehash: 501e82ce93a31264d0625fb0243b4e44dcb2d007
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="b2eba-103">Utilice grupos elásticos toocreate de PowerShell y mover las bases de datos entre grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="b2eba-103">Use PowerShell toocreate elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="b2eba-104">En este ejemplo de secuencia de comandos de PowerShell crea dos grupos elásticos, mueve una base de datos de un grupo elástico en otro grupo elástico y, a continuación, se mueve una base de datos fuera de un nivel de rendimiento de grupo elástico tooa única base de datos.</span><span class="sxs-lookup"><span data-stu-id="b2eba-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool tooa single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="b2eba-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b2eba-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b2eba-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="b2eba-106">Clean up deployment</span></span>

<span data-ttu-id="b2eba-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="b2eba-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b2eba-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="b2eba-108">Script explanation</span></span>

<span data-ttu-id="b2eba-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="b2eba-109">This script uses hello following commands.</span></span> <span data-ttu-id="b2eba-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="b2eba-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b2eba-111">Comando</span><span class="sxs-lookup"><span data-stu-id="b2eba-111">Command</span></span> | <span data-ttu-id="b2eba-112">Notas</span><span class="sxs-lookup"><span data-stu-id="b2eba-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b2eba-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b2eba-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b2eba-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="b2eba-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b2eba-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="b2eba-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="b2eba-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="b2eba-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b2eba-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="b2eba-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="b2eba-118">Crea un grupo elástico en un servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="b2eba-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="b2eba-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b2eba-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="b2eba-120">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="b2eba-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="b2eba-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b2eba-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="b2eba-122">Actualiza las propiedades de la base de datos o traslada una base de datos a un grupo elástico, fuera de este o entre grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="b2eba-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="b2eba-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b2eba-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b2eba-124">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="b2eba-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b2eba-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b2eba-125">Next steps</span></span>

<span data-ttu-id="b2eba-126">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b2eba-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b2eba-127">Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b2eba-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
