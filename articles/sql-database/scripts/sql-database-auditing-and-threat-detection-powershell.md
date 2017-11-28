---
title: "Ejemplo de PowerShell para auditoría y detección de amenazas en Azure SQL Database | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell para configurar la auditoría y la detección de amenazas en Azure SQL Database"
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
ms.openlocfilehash: e039d35474bff3b066a6605a97e04d4a81c365eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="eb013-103">Uso de PowerShell para configurar la auditoría y detección de amenazas en SQL Database</span><span class="sxs-lookup"><span data-stu-id="eb013-103">Use PowerShell to configure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="eb013-104">Este script de ejemplo de PowerShell permite configurar la auditoría y detección de amenazas en SQL Database.</span><span class="sxs-lookup"><span data-stu-id="eb013-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="eb013-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="eb013-105">Sample script</span></span>

<span data-ttu-id="eb013-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configuración de la detección de amenazas y auditoría")]</span><span class="sxs-lookup"><span data-stu-id="eb013-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="eb013-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="eb013-107">Clean up deployment</span></span>

<span data-ttu-id="eb013-108">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="eb013-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="eb013-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="eb013-109">Script explanation</span></span>

<span data-ttu-id="eb013-110">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="eb013-110">This script uses the following commands.</span></span> <span data-ttu-id="eb013-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="eb013-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="eb013-112">Comando</span><span class="sxs-lookup"><span data-stu-id="eb013-112">Command</span></span> | <span data-ttu-id="eb013-113">Notas</span><span class="sxs-lookup"><span data-stu-id="eb013-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eb013-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="eb013-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="eb013-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="eb013-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eb013-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="eb013-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="eb013-117">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="eb013-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="eb013-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="eb013-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="eb013-119">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="eb013-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="eb013-120">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="eb013-120">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="eb013-121">Crea una cuenta de Storage.</span><span class="sxs-lookup"><span data-stu-id="eb013-121">Creates a Storage account.</span></span> |
| [<span data-ttu-id="eb013-122">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="eb013-122">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="eb013-123">Establece la directiva de auditoría para una base de datos.</span><span class="sxs-lookup"><span data-stu-id="eb013-123">Sets the auditing policy for a database.</span></span> |
| [<span data-ttu-id="eb013-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="eb013-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="eb013-125">Establece una directiva de detección de amenazas en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="eb013-125">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="eb013-126">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="eb013-126">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="eb013-127">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="eb013-127">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="eb013-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb013-128">Next steps</span></span>

<span data-ttu-id="eb013-129">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eb013-129">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="eb013-130">Encontrará más ejemplos de scripts de PowerShell de SQL Database en los [scripts de PowerShell de Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="eb013-130">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
