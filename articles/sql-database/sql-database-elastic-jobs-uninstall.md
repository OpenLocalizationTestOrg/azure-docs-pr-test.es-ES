---
title: "Desinstalación de componentes de Trabajos de base de datos elástica"
description: "Desinstalación de componentes de Trabajos de base de datos elástica"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: ae7f0bce452a0a86f6f1e4d9b0c93a0fa1727f21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="90dc0-103">Desinstalación de componentes de Trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="90dc0-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="90dc0-104">**Trabajos de base de datos elástica** se pueden desinstalar mediante el Portal o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90dc0-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="90dc0-105">Desinstalación de componentes de Trabajos de base de datos elástica mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="90dc0-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="90dc0-106">Abra el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="90dc0-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="90dc0-107">Navegue hasta la suscripción que contiene componentes de **Trabajos de base de datos elástica** , es decir, la suscripción en la que se instalaron los componentes de Trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="90dc0-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="90dc0-108">Haga clic en **Examinar** y luego en **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="90dc0-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="90dc0-109">Seleccione el grupo de recursos denominado "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="90dc0-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="90dc0-110">Elimine el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="90dc0-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="90dc0-111">Desinstalación de componentes de Trabajos de base de datos elástica mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="90dc0-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="90dc0-112">Inicie una ventana de comandos de Microsoft Azure PowerShell y navegue hasta el subdirectorio tools en la carpeta Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x: escriba **cd tools**.</span><span class="sxs-lookup"><span data-stu-id="90dc0-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="90dc0-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="90dc0-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="90dc0-114">Ejecute el script .\UninstallElasticDatabaseJobs.ps1 de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90dc0-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="90dc0-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="90dc0-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="90dc0-116">O simplemente, ejecute el siguiente script, suponiendo que se usaron valores predeterminados en la instalación de los componentes:</span><span class="sxs-lookup"><span data-stu-id="90dc0-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "The Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing the Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing the Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="90dc0-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90dc0-117">Next steps</span></span>
<span data-ttu-id="90dc0-118">Para reinstalar Trabajos de base de datos elástica, vea [Instalación del servicio Trabajos de base de datos elástica](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="90dc0-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="90dc0-119">Si desea obtener más información sobre Trabajos de base de datos elástica, vea [Información general de Trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90dc0-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


