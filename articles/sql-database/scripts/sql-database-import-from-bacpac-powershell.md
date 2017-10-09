---
title: "base de datos SQL Azure de archivo de bacpac de importación de ejemplo de aaaPowerShell | Documentos de Microsoft"
description: Icono de un bacpac de Azure tooimport de secuencia de comandos de ejemplo de PowerShell en una base de datos SQL
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
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="0c2bc-103">Usar PowerShell tooimport un archivo bacpac en una base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0c2bc-103">Use PowerShell tooimport a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="0c2bc-104">Este script de PowerShell importa una base de datos de un archivo **bacpac** a una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="0c2bc-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="0c2bc-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0c2bc-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0c2bc-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="0c2bc-106">Clean up deployment</span></span>

<span data-ttu-id="0c2bc-107">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="0c2bc-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="0c2bc-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="0c2bc-108">Script explanation</span></span>

<span data-ttu-id="0c2bc-109">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="0c2bc-109">This script uses hello following commands.</span></span> <span data-ttu-id="0c2bc-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="0c2bc-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0c2bc-111">Comando</span><span class="sxs-lookup"><span data-stu-id="0c2bc-111">Command</span></span> | <span data-ttu-id="0c2bc-112">Notas</span><span class="sxs-lookup"><span data-stu-id="0c2bc-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0c2bc-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0c2bc-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0c2bc-114">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="0c2bc-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0c2bc-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="0c2bc-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="0c2bc-116">Crea un servidor lógico que hospeda Hola base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="0c2bc-116">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="0c2bc-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="0c2bc-117">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="0c2bc-118">Crea un tooall de acceso tooallow de regla de firewall bases de datos SQL en servidor de Hola de intervalo de direcciones IP de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="0c2bc-118">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="0c2bc-119">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="0c2bc-119">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="0c2bc-120">Importa un bacpac de archivos y crea una nueva base de datos en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c2bc-120">Imports a .bacpac file and create a new database on hello server.</span></span> |
| [<span data-ttu-id="0c2bc-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0c2bc-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0c2bc-122">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="0c2bc-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0c2bc-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0c2bc-123">Next steps</span></span>

<span data-ttu-id="0c2bc-124">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0c2bc-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0c2bc-125">Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0c2bc-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
