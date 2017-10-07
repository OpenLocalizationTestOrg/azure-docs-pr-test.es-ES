---
title: "herramienta de trabajos de bases de datos elástico de aaaHow toouninstall"
description: "¿Cómo toouninstall Hola herramienta de trabajos de bases de datos elásticas"
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
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="399ef-103">Desinstalación de componentes de Trabajos de base de datos elástica.</span><span class="sxs-lookup"><span data-stu-id="399ef-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="399ef-104">**Trabajos de base de datos elásticos** componentes se pueden desinstalar mediante el Portal de Hola o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="399ef-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="399ef-105">Desinstalar componentes de trabajos de bases de datos elásticas mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="399ef-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="399ef-106">Abra hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="399ef-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="399ef-107">Navegar por suscripción toohello que contiene **trabajos de base de datos elástica** componentes, es decir Hola suscripción en la base de datos elástico se instalaron componentes de trabajos.</span><span class="sxs-lookup"><span data-stu-id="399ef-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="399ef-108">Haga clic en **Examinar** y luego en **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="399ef-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="399ef-109">Grupo de recursos de hello seleccione llamado "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="399ef-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="399ef-110">Elimine el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="399ef-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="399ef-111">Desinstalación de componentes de Trabajos de base de datos elástica mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="399ef-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="399ef-112">Inicia una ventana de comandos de PowerShell de Microsoft Azure y ve subdirectorio herramientas toohello bajo la carpeta de Hola Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x: tipo **cd herramientas**.</span><span class="sxs-lookup"><span data-stu-id="399ef-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="399ef-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="399ef-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="399ef-114">Ejecutar script de PowerShell de hello.\UninstallElasticDatabaseJobs.ps1.</span><span class="sxs-lookup"><span data-stu-id="399ef-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="399ef-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="399ef-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="399ef-116">O simplemente, ejecute hello siguiente secuencia de comandos, suponiendo que de forma predeterminada valores donde usadas en la instalación de componentes de hello:</span><span class="sxs-lookup"><span data-stu-id="399ef-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="399ef-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="399ef-117">Next steps</span></span>
<span data-ttu-id="399ef-118">trabajos de base de datos elástica toore instalación, consulte [instalar el servicio de trabajo de base de datos elástica Hola](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="399ef-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="399ef-119">Si desea obtener más información sobre Trabajos de base de datos elástica, vea [Información general de Trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="399ef-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


