---
title: Ejemplo de PowerShell para importar un archivo bacpac en una base de datos SQL de Azure | Microsoft Docs
description: Script de ejemplo de Azure PowerShell para importar un archivo bacpac en una base de datos SQL
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
ms.openlocfilehash: 20e1d4c195314d6e828e1dac6afae8be11805b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-import-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="0b730-103">Uso de Powershell para importar un archivo bacpac en una base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="0b730-103">Use PowerShell to import a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="0b730-104">Este script de PowerShell importa una base de datos de un archivo **bacpac** a una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b730-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="0b730-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0b730-105">Sample script</span></span>

<span data-ttu-id="0b730-106">[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Creación de una base de datos SQL")]</span><span class="sxs-lookup"><span data-stu-id="0b730-106">[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0b730-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="0b730-107">Clean up deployment</span></span>

<span data-ttu-id="0b730-108">Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="0b730-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0b730-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="0b730-109">Script explanation</span></span>

<span data-ttu-id="0b730-110">Este script usa los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="0b730-110">This script uses the following commands.</span></span> <span data-ttu-id="0b730-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="0b730-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0b730-112">Comando</span><span class="sxs-lookup"><span data-stu-id="0b730-112">Command</span></span> | <span data-ttu-id="0b730-113">Notas</span><span class="sxs-lookup"><span data-stu-id="0b730-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0b730-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0b730-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0b730-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="0b730-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0b730-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="0b730-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="0b730-117">Crea un servidor lógico que hospeda la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="0b730-117">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="0b730-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="0b730-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="0b730-119">Crea una regla de firewall para permitir el acceso a todas las bases de datos SQL en el servidor desde el intervalo de direcciones IP especificado.</span><span class="sxs-lookup"><span data-stu-id="0b730-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="0b730-120">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="0b730-120">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="0b730-121">Importa un archivo bacpac y crea una nueva base de datos en el servidor.</span><span class="sxs-lookup"><span data-stu-id="0b730-121">Imports a .bacpac file and create a new database on the server.</span></span> |
| [<span data-ttu-id="0b730-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0b730-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0b730-123">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="0b730-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0b730-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b730-124">Next steps</span></span>

<span data-ttu-id="0b730-125">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0b730-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0b730-126">Encontrará más ejemplos de scripts de PowerShell de SQL Database en los [scripts de PowerShell de Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0b730-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
