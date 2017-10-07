---
title: base de datos-nuevo servidor de aaaPowerShell copia de ejemplo de Azure SQL | Documentos de Microsoft
description: Toocopy de secuencia de comandos de ejemplo de PowerShell Azure un servidor nuevo de la tooa de base de datos SQL
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
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="5039d-103">Usar PowerShell toocopy un servidor nuevo de la tooa de base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="5039d-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="5039d-104">Este ejemplo de script de PowerShell crea una copia de una base de datos existente en un nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="5039d-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="5039d-105">Copie un nuevo servidor de base de datos tooa</span><span class="sxs-lookup"><span data-stu-id="5039d-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5039d-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="5039d-106">Clean up deployment</span></span>

<span data-ttu-id="5039d-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="5039d-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="5039d-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="5039d-108">Script explanation</span></span>

<span data-ttu-id="5039d-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="5039d-109">This script uses hello following commands.</span></span> <span data-ttu-id="5039d-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="5039d-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5039d-111">Comando</span><span class="sxs-lookup"><span data-stu-id="5039d-111">Command</span></span> | <span data-ttu-id="5039d-112">Notas</span><span class="sxs-lookup"><span data-stu-id="5039d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5039d-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5039d-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5039d-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="5039d-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5039d-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="5039d-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="5039d-116">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="5039d-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="5039d-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="5039d-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="5039d-118">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="5039d-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="5039d-119">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="5039d-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="5039d-120">Crea una copia de una base de datos que utiliza instantáneas hello en hello hora actual.</span><span class="sxs-lookup"><span data-stu-id="5039d-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="5039d-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5039d-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5039d-122">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="5039d-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="5039d-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5039d-123">Next steps</span></span>

<span data-ttu-id="5039d-124">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5039d-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5039d-125">Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5039d-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
