---
title: Ejemplo de PowerShell para supervisar y escalar una instancia de Azure SQL Database | Microsoft Docs
description: Script de ejemplo de Azure PowerShell para supervisar y escalar una instancia de Azure SQL Database
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
ms.openlocfilehash: 5d08335f4b1d6c5c6a120cbfb86ab2c62b79bb9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="386e6-103">Uso de PowerShell para supervisar y escalar una sola base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="386e6-103">Use PowerShell to monitor and scale a single SQL database</span></span>

<span data-ttu-id="386e6-104">Este ejemplo de script de PowerShell supervisa las métricas de rendimiento de una base de datos, la escala a un nivel de rendimiento superior y crea una regla de alertas en una de las métricas de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="386e6-104">This PowerShell script example monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="386e6-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="386e6-105">Sample script</span></span>

<span data-ttu-id="386e6-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Supervisión y escalado de una instancia única de SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="386e6-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="386e6-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="386e6-107">Clean up deployment</span></span>

<span data-ttu-id="386e6-108">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="386e6-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="386e6-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="386e6-109">Script explanation</span></span>

<span data-ttu-id="386e6-110">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="386e6-110">This script uses the following commands.</span></span> <span data-ttu-id="386e6-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="386e6-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="386e6-112">Comando</span><span class="sxs-lookup"><span data-stu-id="386e6-112">Command</span></span> | <span data-ttu-id="386e6-113">Notas</span><span class="sxs-lookup"><span data-stu-id="386e6-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="386e6-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="386e6-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="386e6-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="386e6-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="386e6-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="386e6-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="386e6-117">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="386e6-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="386e6-118">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="386e6-118">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="386e6-119">Muestra la información de uso del tamaño de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="386e6-119">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="386e6-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="386e6-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="386e6-121">Actualiza las propiedades de la base de datos o traslada una base de datos a un grupo elástico, fuera de este o entre grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="386e6-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="386e6-122">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="386e6-122">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="386e6-123">Establece una regla de alerta para supervisar automáticamente las DTU en el futuro.</span><span class="sxs-lookup"><span data-stu-id="386e6-123">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="386e6-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="386e6-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="386e6-125">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="386e6-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="386e6-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="386e6-126">Next steps</span></span>

<span data-ttu-id="386e6-127">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="386e6-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="386e6-128">Encontrará más ejemplos de scripts de PowerShell de SQL Database en los [scripts de PowerShell de Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="386e6-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
