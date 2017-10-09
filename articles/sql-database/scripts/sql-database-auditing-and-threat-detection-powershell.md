---
title: "aaaPowerShell de amenaza auditoría ejemplo detección Azure base de datos SQL | Documentos de Microsoft"
description: "Azure PowerShell ejemplo script tooconfigure auditoría y amenaza para la detección en una base de datos de SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="024a4-103">Utilice la detección de amenazas y auditoría de la base de datos SQL del tooconfigure PowerShell</span><span class="sxs-lookup"><span data-stu-id="024a4-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="024a4-104">Este script de ejemplo de PowerShell permite configurar la auditoría y detección de amenazas en SQL Database.</span><span class="sxs-lookup"><span data-stu-id="024a4-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="024a4-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="024a4-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="024a4-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="024a4-106">Clean up deployment</span></span>

<span data-ttu-id="024a4-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="024a4-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="024a4-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="024a4-108">Script explanation</span></span>

<span data-ttu-id="024a4-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="024a4-109">This script uses hello following commands.</span></span> <span data-ttu-id="024a4-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="024a4-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="024a4-111">Comando</span><span class="sxs-lookup"><span data-stu-id="024a4-111">Command</span></span> | <span data-ttu-id="024a4-112">Notas</span><span class="sxs-lookup"><span data-stu-id="024a4-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="024a4-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="024a4-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="024a4-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="024a4-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="024a4-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="024a4-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="024a4-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="024a4-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="024a4-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="024a4-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="024a4-118">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="024a4-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="024a4-119">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="024a4-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="024a4-120">Crea una cuenta de Storage.</span><span class="sxs-lookup"><span data-stu-id="024a4-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="024a4-121">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="024a4-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="024a4-122">Establece la directiva de auditoría de Hola para una base de datos.</span><span class="sxs-lookup"><span data-stu-id="024a4-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="024a4-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="024a4-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="024a4-124">Establece una directiva de detección de amenazas en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="024a4-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="024a4-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="024a4-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="024a4-126">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="024a4-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="024a4-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="024a4-127">Next steps</span></span>

<span data-ttu-id="024a4-128">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="024a4-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="024a4-129">Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="024a4-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
