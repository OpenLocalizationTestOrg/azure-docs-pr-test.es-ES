---
title: "comandos aaaAzure PowerShell basada en el Administrador de recursos para la aplicación Web de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola toomanage de comandos de PowerShell basada en el Administrador de recursos de Azure nuevo las aplicaciones Web de Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="ef0da-103">Uso de aplicaciones de Web de Azure PowerShell Azure Resource Manager-Based tooManage</span><span class="sxs-lookup"><span data-stu-id="ef0da-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef0da-104">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ef0da-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="ef0da-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef0da-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="ef0da-106">Con Microsoft Azure PowerShell versión 1.0.0 se han agregado nuevos comandos, que le proporcionan Hola usuario Hola capacidad toouse basado en el Administrador de recursos de Azure PowerShell comandos toomanage aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="ef0da-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="ef0da-107">toolearn acerca de cómo administrar grupos de recursos, consulte [con Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ef0da-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="ef0da-108">toolearn acerca de la lista completa de Hola de parámetros y las opciones de hello cmdlets de PowerShell, vea hello [completo referencia de Cmdlet basado en el Administrador de recursos de Azure de aplicación Web de Cmdlets de PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="ef0da-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="ef0da-109">Administración de planes del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ef0da-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="ef0da-110">Creación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ef0da-110">Create an App Service Plan</span></span>
<span data-ttu-id="ef0da-111">toocreate un plan de servicio de aplicaciones, usar hello **AzureRmAppServicePlan New** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef0da-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="ef0da-112">Siguientes son las descripciones de parámetros diferentes hello:</span><span class="sxs-lookup"><span data-stu-id="ef0da-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="ef0da-113">**Nombre**: nombre del plan de servicio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="ef0da-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="ef0da-114">**Location**: ubicación del plan del servicio.</span><span class="sxs-lookup"><span data-stu-id="ef0da-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="ef0da-115">**ResourceGroupName**: grupo de recursos que incluye el plan de servicio de aplicación Hola recién creado.</span><span class="sxs-lookup"><span data-stu-id="ef0da-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="ef0da-116">**Nivel**: Hola deseado tarifa (valor predeterminado es gratuito, otras opciones son compartidos, Basic, Standard y Premium).</span><span class="sxs-lookup"><span data-stu-id="ef0da-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="ef0da-117">**WorkerSize**: Hola tamaño de trabajadores (el valor predeterminado es pequeña si se especificó el parámetro de nivel de hello como Basic, Standard o Premium.</span><span class="sxs-lookup"><span data-stu-id="ef0da-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="ef0da-118">Otras opciones son Mediano y Grande.)</span><span class="sxs-lookup"><span data-stu-id="ef0da-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="ef0da-119">**NumberofWorkers**: Hola el número de trabajos en el plan de servicio de aplicación Hola (el valor predeterminado es 1).</span><span class="sxs-lookup"><span data-stu-id="ef0da-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="ef0da-120">En el ejemplo se toouse este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ef0da-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="ef0da-121">Creación de un plan del Servicio de aplicaciones en un entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ef0da-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="ef0da-122">toocreate planear de un servicio de aplicaciones en un entorno de servicio de aplicaciones, use Hola mismo comando **AzureRmAppServicePlan New** comando con el nombre de hello toospecify de parámetros adicionales del ASE y el nombre del grupo de recursos de ASE.</span><span class="sxs-lookup"><span data-stu-id="ef0da-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="ef0da-123">En el ejemplo se toouse este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ef0da-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="ef0da-124">más información acerca del entorno de servicio de aplicaciones, verificación toolearn [Introducción tooApp entorno del servicio](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ef0da-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="ef0da-125">Enumeración de planes del Servicio de aplicaciones existentes</span><span class="sxs-lookup"><span data-stu-id="ef0da-125">List Existing App Service Plans</span></span>
<span data-ttu-id="ef0da-126">usar planes de servicio de aplicación existente de toolist hello, **AzureRmAppServicePlan Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef0da-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="ef0da-127">toolist todos los planes de servicio de aplicación en su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="ef0da-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="ef0da-128">toolist todos los planes de servicio de aplicaciones en un grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="ef0da-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="ef0da-129">tooget un plan de servicio de aplicación específica, use:</span><span class="sxs-lookup"><span data-stu-id="ef0da-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="ef0da-130">Configuración de un plan del Servicio de aplicaciones existente</span><span class="sxs-lookup"><span data-stu-id="ef0da-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="ef0da-131">toochange Hola de un plan de servicio de aplicación existente, utilice hello **AzureRmAppServicePlan conjunto** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef0da-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="ef0da-132">Puede cambiar el nivel de hello, el tamaño de trabajo y el número de Hola de trabajadores</span><span class="sxs-lookup"><span data-stu-id="ef0da-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="ef0da-133">Escalado de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ef0da-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="ef0da-134">tooscale una existente aplicación Plan del servicio, use:</span><span class="sxs-lookup"><span data-stu-id="ef0da-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="ef0da-135">Cambiar el tamaño de trabajador de Hola de un Plan de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ef0da-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="ef0da-136">tamaño de hello toochange de trabajadores de una existente aplicación servicio previsto, use:</span><span class="sxs-lookup"><span data-stu-id="ef0da-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="ef0da-137">Hola Cambiar nivel de un Plan de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ef0da-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="ef0da-138">nivel de hello toochange una existente aplicación de servicio del Plan de, use:</span><span class="sxs-lookup"><span data-stu-id="ef0da-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="ef0da-139">Eliminación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ef0da-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="ef0da-140">toodelete un plan de servicio de aplicación existente, todas asignadas toobe de necesidad de aplicaciones web movido o eliminado en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="ef0da-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="ef0da-141">A continuación, usar hello **Remove-AzureRmAppServicePlan** cmdlet puede eliminar el plan de servicio de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef0da-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="ef0da-142">Administración de aplicaciones web del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ef0da-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="ef0da-143">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="ef0da-143">Create a Web App</span></span>
<span data-ttu-id="ef0da-144">toocreate una aplicación web, utilice hello **AzureRmWebApp New** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef0da-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="ef0da-145">Siguientes son las descripciones de parámetros diferentes hello:</span><span class="sxs-lookup"><span data-stu-id="ef0da-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="ef0da-146">**Nombre**: nombre de la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef0da-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="ef0da-147">**AppServicePlan**: nombre para el plan de servicio Hola utiliza toohost hello web app.</span><span class="sxs-lookup"><span data-stu-id="ef0da-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="ef0da-148">**ResourceGroupName**: grupo de recursos que hospeda el plan de servicio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="ef0da-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="ef0da-149">**Ubicación**: Hola ubicación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ef0da-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="ef0da-150">En el ejemplo se toouse este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ef0da-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="ef0da-151">Creación de una aplicación web en App Service Environment</span><span class="sxs-lookup"><span data-stu-id="ef0da-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="ef0da-152">toocreate una aplicación web en un entorno de servicio de aplicación (ASE).</span><span class="sxs-lookup"><span data-stu-id="ef0da-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="ef0da-153">Use Hola mismo **AzureRmWebApp New** comando con nombre de hello ASE toospecify de parámetros adicionales y el nombre de grupo de recursos de Hola Hola ASE pertenece a.</span><span class="sxs-lookup"><span data-stu-id="ef0da-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="ef0da-154">más información acerca del entorno de servicio de aplicaciones, verificación toolearn [Introducción tooApp entorno del servicio](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ef0da-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="ef0da-155">Eliminación de una aplicación web existente</span><span class="sxs-lookup"><span data-stu-id="ef0da-155">Delete an existing Web App</span></span>
<span data-ttu-id="ef0da-156">una aplicación web existente que se puede usar hello toodelete **Remove-AzureRmWebApp** cmdlet, necesita nombre de hello toospecify de aplicación web de hello y nombre de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef0da-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="ef0da-157">Lista de aplicaciones web existentes</span><span class="sxs-lookup"><span data-stu-id="ef0da-157">List existing Web Apps</span></span>
<span data-ttu-id="ef0da-158">aplicaciones web existentes a toolist hello, usar hello **AzureRmWebApp Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef0da-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="ef0da-159">toolist todas las aplicaciones web en su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="ef0da-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="ef0da-160">toolist todas las aplicaciones web en un grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="ef0da-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="ef0da-161">tooget una aplicación web específica, use:</span><span class="sxs-lookup"><span data-stu-id="ef0da-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="ef0da-162">Configuración de una aplicación web existente</span><span class="sxs-lookup"><span data-stu-id="ef0da-162">Configure an existing Web App</span></span>
<span data-ttu-id="ef0da-163">configuraciones de hello toochange y para una aplicación web existente, use hello **AzureRmWebApp conjunto** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef0da-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="ef0da-164">Para obtener una lista completa de parámetros, compruebe hello [vínculo de referencia de Cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="ef0da-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="ef0da-165">Ejemplo (1): use este cmdlet toochange las cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="ef0da-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="ef0da-166">Ejemplo (2): Adición o cambio de la configuración de una aplicación</span><span class="sxs-lookup"><span data-stu-id="ef0da-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="ef0da-167">Ejemplo (3): establecer toorun de aplicación web de hello en modo de 64 bits</span><span class="sxs-lookup"><span data-stu-id="ef0da-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="ef0da-168">Cambio de estado de Hola de una aplicación Web existente</span><span class="sxs-lookup"><span data-stu-id="ef0da-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="ef0da-169">Reinicio de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="ef0da-169">Restart a web app</span></span>
<span data-ttu-id="ef0da-170">toorestart una aplicación web, debe especificar Hola nombre del grupo de recursos de aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="ef0da-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="ef0da-171">Detención de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="ef0da-171">Stop a web app</span></span>
<span data-ttu-id="ef0da-172">toostop una aplicación web, debe especificar Hola nombre del grupo de recursos de aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="ef0da-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="ef0da-173">Inicio de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="ef0da-173">Start a web app</span></span>
<span data-ttu-id="ef0da-174">toostart una aplicación web, debe especificar Hola nombre del grupo de recursos de aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="ef0da-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="ef0da-175">Administración de perfiles de publicación de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="ef0da-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="ef0da-176">Cada aplicación web tiene un perfil de publicación que puede ser utilizado toopublish las aplicaciones, se pueden ejecutar varias operaciones en perfiles de publicación.</span><span class="sxs-lookup"><span data-stu-id="ef0da-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="ef0da-177">Obtención de un perfil de publicación</span><span class="sxs-lookup"><span data-stu-id="ef0da-177">Get Publishing Profile</span></span>
<span data-ttu-id="ef0da-178">tooget Hola de perfil para una aplicación web, el uso de publicación:</span><span class="sxs-lookup"><span data-stu-id="ef0da-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="ef0da-179">Este comando eco hello publicación de línea de comandos de toohello de perfil también Hola archivo de texto tooa de perfil de publicación de salida.</span><span class="sxs-lookup"><span data-stu-id="ef0da-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="ef0da-180">Restablecimiento de un perfil de publicación</span><span class="sxs-lookup"><span data-stu-id="ef0da-180">Reset Publishing Profile</span></span>
<span data-ttu-id="ef0da-181">tooreset ambos Hola contraseña de publicación de FTP y web deploy para una aplicación web, use:</span><span class="sxs-lookup"><span data-stu-id="ef0da-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="ef0da-182">Administración de certificados de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="ef0da-182">Manage Web App Certificates</span></span>
<span data-ttu-id="ef0da-183">toolearn acerca de cómo toomanage web certificados de aplicación, consulte [enlace de certificados SSL con PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="ef0da-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="ef0da-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ef0da-184">Next Steps</span></span>
* <span data-ttu-id="ef0da-185">toolearn sobre la compatibilidad con el Administrador de recursos de Azure PowerShell, consulte [con Azure PowerShell con el Administrador de recursos de Azure.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="ef0da-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="ef0da-186">toolearn sobre los entornos de servicio de aplicación, consulte [Introducción tooApp entorno del servicio.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ef0da-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="ef0da-187">toolearn acerca de cómo administrar certificados SSL de servicio de aplicación mediante PowerShell, consulte [enlace de certificados SSL mediante PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="ef0da-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="ef0da-188">toolearn acerca de la lista completa de Hola de cmdlets de PowerShell basada en el Administrador de recursos de Azure para las aplicaciones Web de Azure, consulte [referencia de cmdlets de Azure de Cmdlets de PowerShell del Administrador de recursos de Web aplicaciones de Azure.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="ef0da-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="ef0da-189">toolearn acerca de cómo administrar el servicio de aplicaciones mediante CLI, consulte [Using Azure Resource Manager-Based XPlat CLI para la aplicación Web de Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="ef0da-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

