---
title: "aaaPowerShell ejemplo-monitor-escala-SQL elástico grupo Azure base de datos SQL | Documentos de Microsoft"
description: "Azure toomonitor de secuencia de comandos de ejemplo de PowerShell y la escala de un grupo elástico de SQL en la base de datos de SQL Azure"
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
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="f94f6-103">Usar PowerShell toomonitor y escalar un grupo elástico de SQL en la base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f94f6-103">Use PowerShell toomonitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="f94f6-104">En este ejemplo de secuencia de comandos de PowerShell monitores Hola métricas de rendimiento de un grupo elástico, escala tooa mayor nivel de rendimiento y crea una regla de alerta en una de las métricas de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="f94f6-104">This PowerShell script example monitors hello performance metrics of an elastic pool, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="f94f6-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f94f6-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f94f6-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="f94f6-106">Clean up deployment</span></span>

<span data-ttu-id="f94f6-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="f94f6-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="f94f6-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f94f6-108">Script explanation</span></span>

<span data-ttu-id="f94f6-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="f94f6-109">This script uses hello following commands.</span></span> <span data-ttu-id="f94f6-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="f94f6-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f94f6-111">Comando</span><span class="sxs-lookup"><span data-stu-id="f94f6-111">Command</span></span> | <span data-ttu-id="f94f6-112">Notas</span><span class="sxs-lookup"><span data-stu-id="f94f6-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="f94f6-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f94f6-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f94f6-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="f94f6-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f94f6-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="f94f6-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="f94f6-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="f94f6-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="f94f6-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="f94f6-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="f94f6-118">Crea un grupo elástico en un servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="f94f6-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="f94f6-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="f94f6-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="f94f6-120">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="f94f6-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="f94f6-121">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="f94f6-121">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="f94f6-122">Muestra información de uso de hello tamaño de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f94f6-122">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="f94f6-123">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="f94f6-123">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="f94f6-124">Agrega o actualiza una regla de alerta basada en métricas.</span><span class="sxs-lookup"><span data-stu-id="f94f6-124">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="f94f6-125">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="f94f6-125">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="f94f6-126">Actualiza las propiedades del grupo elástico</span><span class="sxs-lookup"><span data-stu-id="f94f6-126">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="f94f6-127">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="f94f6-127">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="f94f6-128">Establece a una regla de alerta tooautomatically monitor Dtu Hola futuras.</span><span class="sxs-lookup"><span data-stu-id="f94f6-128">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="f94f6-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f94f6-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f94f6-130">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="f94f6-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="f94f6-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f94f6-131">Next steps</span></span>

<span data-ttu-id="f94f6-132">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f94f6-132">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f94f6-133">Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f94f6-133">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
