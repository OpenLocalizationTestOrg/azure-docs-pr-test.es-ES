---
title: 'ejemplo: crear aaaPowerShell una base de datos SQL de Azure | Documentos de Microsoft'
description: Azure toocreate de secuencia de comandos de ejemplo de PowerShell una base de datos de SQL Azure
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae57b2018f4a550bf2c6da688d6e49bdadf3d3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="d6c3c-103">Usar PowerShell toocreate una sola base de datos de SQL Azure y configurar una regla de firewall</span><span class="sxs-lookup"><span data-stu-id="d6c3c-103">Use PowerShell toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="d6c3c-104">Este ejemplo de script de PowerShell crea una instancia de Azure SQL Database y configura una regla de firewall en el nivel de servidor.</span><span class="sxs-lookup"><span data-stu-id="d6c3c-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="d6c3c-105">Una vez que se ha ejecutado correctamente el script de Hola, base de datos SQL puede tener acceso desde todos los servicios de Azure de Hola y Hola configuran dirección IP.</span><span class="sxs-lookup"><span data-stu-id="d6c3c-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="d6c3c-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="d6c3c-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d6c3c-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="d6c3c-107">Clean up deployment</span></span>

<span data-ttu-id="d6c3c-108">Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.</span><span class="sxs-lookup"><span data-stu-id="d6c3c-108">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d6c3c-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="d6c3c-109">Script explanation</span></span>

<span data-ttu-id="d6c3c-110">Este script utiliza Hola siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="d6c3c-110">This script uses hello following commands.</span></span> <span data-ttu-id="d6c3c-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="d6c3c-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d6c3c-112">Comando</span><span class="sxs-lookup"><span data-stu-id="d6c3c-112">Command</span></span> | <span data-ttu-id="d6c3c-113">Notas</span><span class="sxs-lookup"><span data-stu-id="d6c3c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d6c3c-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d6c3c-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d6c3c-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="d6c3c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d6c3c-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="d6c3c-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="d6c3c-117">Crea un servidor lógico que hospeda una base de datos o un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="d6c3c-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d6c3c-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="d6c3c-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="d6c3c-119">Crea un tooall de acceso tooallow de regla de firewall bases de datos SQL en servidor de Hola de intervalo de direcciones IP de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="d6c3c-119">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="d6c3c-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d6c3c-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="d6c3c-121">Crea una base de datos en un servidor lógico como una base de datos única o agrupada.</span><span class="sxs-lookup"><span data-stu-id="d6c3c-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="d6c3c-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d6c3c-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d6c3c-123">Elimina un grupo de recursos, incluidos todos los recursos anidados.</span><span class="sxs-lookup"><span data-stu-id="d6c3c-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d6c3c-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6c3c-124">Next steps</span></span>

<span data-ttu-id="d6c3c-125">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6c3c-125">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d6c3c-126">Encontrará más ejemplos de secuencias de comandos de PowerShell de la base de datos de SQL en hello [scripts de PowerShell de base de datos de SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d6c3c-126">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



