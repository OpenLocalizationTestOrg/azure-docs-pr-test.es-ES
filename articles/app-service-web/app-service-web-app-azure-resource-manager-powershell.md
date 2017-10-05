---
title: Comandos de PowerShell basados en Azure Resource Manager para aplicaciones web de Azure | Microsoft Docs
description: Aprenda a usar los nuevos comandos de PowerShell basados en Azure Resource Manager para administrar aplicaciones web de Azure.
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
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a><span data-ttu-id="ea8e7-103">Uso de PowerShell basado en Azure Resource Manager para administrar aplicaciones web de Azure</span><span class="sxs-lookup"><span data-stu-id="ea8e7-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea8e7-104">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ea8e7-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="ea8e7-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea8e7-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="ea8e7-106">En la versión 1.0.0 de Microsoft Azure PowerShell se han agregado nuevos comandos que proporcionan al usuario la capacidad de utilizar comandos de PowerShell basados en Azure Resource Manager para administrar aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span></span>

<span data-ttu-id="ea8e7-107">Para obtener información acerca de cómo administrar grupos de recursos, consulte [Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ea8e7-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="ea8e7-108">Para más información acerca de la lista completa de parámetros y opciones de los cmdlets de PowerShell, consulte la [referencia completa de los cmdlets de PowerShell basados en Azure Resource Manager de aplicaciones web](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="ea8e7-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="ea8e7-109">Administración de planes del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ea8e7-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="ea8e7-110">Creación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ea8e7-110">Create an App Service Plan</span></span>
<span data-ttu-id="ea8e7-111">Para crear un plan de App Service, utilice el cmdlet **New-AzureRmAppServicePlan**.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="ea8e7-112">Estas son las descripciones de los distintos parámetros:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-112">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="ea8e7-113">**Name**: el nombre del plan del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-113">**Name**: name of the app service plan.</span></span>
* <span data-ttu-id="ea8e7-114">**Location**: ubicación del plan del servicio.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="ea8e7-115">**ResourceGroupName**: grupo de recursos que incluye el plan del Servicio de aplicaciones recién creado.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="ea8e7-116">**Tier**: el plan de tarifa deseado (el valor predeterminado es Gratis y las restantes opciones son Compartido, Básico, Estándar y Premium).</span><span class="sxs-lookup"><span data-stu-id="ea8e7-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="ea8e7-117">**WorkerSize**: el tamaño de los trabajos (el valor predeterminado es Pequeño si en el parámetro Tier se ha especificado el valor Básico, Estándar o Premium.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="ea8e7-118">Otras opciones son Mediano y Grande.)</span><span class="sxs-lookup"><span data-stu-id="ea8e7-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="ea8e7-119">**NumberofWorkers**: el número de trabajos en el plan del Servicio de aplicaciones (el valor predeterminado es 1).</span><span class="sxs-lookup"><span data-stu-id="ea8e7-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span></span> 

<span data-ttu-id="ea8e7-120">Ejemplo para usar este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-120">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="ea8e7-121">Creación de un plan del Servicio de aplicaciones en un entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ea8e7-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="ea8e7-122">Para crear un plan de App Service en App Service Environment, use el mismo comando **New-AzureRmAppServicePlan** con parámetros adicionales para especificar el nombre del ASE y el nombre del grupo de recursos del ASE.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="ea8e7-123">Ejemplo para usar este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-123">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="ea8e7-124">Para obtener más información acerca del entorno del Servicio de aplicaciones, consulte [Introducción al entorno del Servicio de aplicaciones](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ea8e7-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="ea8e7-125">Enumeración de planes del Servicio de aplicaciones existentes</span><span class="sxs-lookup"><span data-stu-id="ea8e7-125">List Existing App Service Plans</span></span>
<span data-ttu-id="ea8e7-126">Para enumerar los planes del Servicio de aplicaciones existentes, use el cmdlet **Get-AzureRmAppServicePlan** .</span><span class="sxs-lookup"><span data-stu-id="ea8e7-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="ea8e7-127">Para enumerar todos los planes del Servicio de aplicaciones de su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-127">To list all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="ea8e7-128">Para enumerar todos los planes del Servicio de aplicaciones de un grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-128">To list all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="ea8e7-129">Para obtener un plan del Servicio de aplicaciones específico, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-129">To get a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="ea8e7-130">Configuración de un plan del Servicio de aplicaciones existente</span><span class="sxs-lookup"><span data-stu-id="ea8e7-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="ea8e7-131">Para cambiar la configuración de un plan del Servicio de aplicaciones existente, use el cmdlet **Set-AzureRmAppServicePlan** .</span><span class="sxs-lookup"><span data-stu-id="ea8e7-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="ea8e7-132">Puede cambiar el nivel, el tamaño del trabajo y el número de trabajos</span><span class="sxs-lookup"><span data-stu-id="ea8e7-132">You can change the tier, worker size, and the number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="ea8e7-133">Escalado de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ea8e7-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="ea8e7-134">Para escalar un plan del Servicio de aplicaciones existente, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-134">To scale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a><span data-ttu-id="ea8e7-135">Cambio del tamaño de los trabajos de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ea8e7-135">Changing the worker size of an App Service Plan</span></span>
<span data-ttu-id="ea8e7-136">Para cambiar el tamaño de los trabajos de un plan del Servicio de aplicaciones existente, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-136">To change the size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a><span data-ttu-id="ea8e7-137">Cambio del nivel de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ea8e7-137">Changing the Tier of an App Service Plan</span></span>
<span data-ttu-id="ea8e7-138">Para cambiar el nivel de un plan del Servicio de aplicaciones existente, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-138">To change the tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="ea8e7-139">Eliminación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ea8e7-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="ea8e7-140">Para eliminar un plan de App Service existente, primero se deben mover o eliminar todas las aplicaciones web asignadas.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span></span> <span data-ttu-id="ea8e7-141">A continuación, mediante el cmdlet **Remove-AzureRmAppServicePlan** puede eliminar el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="ea8e7-142">Administración de aplicaciones web del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="ea8e7-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="ea8e7-143">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="ea8e7-143">Create a Web App</span></span>
<span data-ttu-id="ea8e7-144">Para crear una aplicación web, use el cmdlet **New-AzureRmWebApp**.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="ea8e7-145">Estas son las descripciones de los distintos parámetros:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-145">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="ea8e7-146">**Name**: nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-146">**Name**: name for the web app.</span></span>
* <span data-ttu-id="ea8e7-147">**AppServicePlan**: nombre del plan del servicio que se utiliza para hospedar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-147">**AppServicePlan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="ea8e7-148">**ResourceGroupName**: grupo de recursos que hospeda el plan del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-148">**ResourceGroupName**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="ea8e7-149">**Location**: la ubicación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-149">**Location**: the web app location.</span></span>

<span data-ttu-id="ea8e7-150">Ejemplo para usar este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-150">Example to use this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="ea8e7-151">Creación de una aplicación web en App Service Environment</span><span class="sxs-lookup"><span data-stu-id="ea8e7-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="ea8e7-152">Creación de una aplicación web en App Service Environment (ASE).</span><span class="sxs-lookup"><span data-stu-id="ea8e7-152">To create a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="ea8e7-153">Use el mismo comando **New-AzureRmWebApp** con parámetros adicionales para especificar el nombre del ASE y el nombre del grupo de recursos al que pertenece el ASE.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="ea8e7-154">Para obtener más información acerca del entorno del Servicio de aplicaciones, consulte [Introducción al entorno del Servicio de aplicaciones](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ea8e7-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="ea8e7-155">Eliminación de una aplicación web existente</span><span class="sxs-lookup"><span data-stu-id="ea8e7-155">Delete an existing Web App</span></span>
<span data-ttu-id="ea8e7-156">Para eliminar una aplicación web existente, puede utilizar el cmdlet **Remove-AzureRmWebApp** , pero debe especificar el nombre de la aplicación web y el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="ea8e7-157">Lista de aplicaciones web existentes</span><span class="sxs-lookup"><span data-stu-id="ea8e7-157">List existing Web Apps</span></span>
<span data-ttu-id="ea8e7-158">Para enumerar las aplicaciones web existentes, use el cmdlet **Get-AzureRmWebApp** .</span><span class="sxs-lookup"><span data-stu-id="ea8e7-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="ea8e7-159">Para enumerar todas las aplicaciones web de su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-159">To list all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="ea8e7-160">Para enumerar todas los aplicaciones web de un grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-160">To list all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="ea8e7-161">Para obtener una aplicación web específica, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-161">To get a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="ea8e7-162">Configuración de una aplicación web existente</span><span class="sxs-lookup"><span data-stu-id="ea8e7-162">Configure an existing Web App</span></span>
<span data-ttu-id="ea8e7-163">Para cambiar los valores y la configuración de una aplicación web existente, use el cmdlet **Set-AzureRmWebApp** .</span><span class="sxs-lookup"><span data-stu-id="ea8e7-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="ea8e7-164">Para obtener la lista completa de parámetros, consulte el [vínculo de referencia de cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="ea8e7-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="ea8e7-165">Ejemplo (1): utilice este cmdlet para cambiar las cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="ea8e7-165">Example (1): use this cmdlet to change connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="ea8e7-166">Ejemplo (2): Adición o cambio de la configuración de una aplicación</span><span class="sxs-lookup"><span data-stu-id="ea8e7-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="ea8e7-167">Ejemplo (3): establezca que la aplicación web se ejecute en modo de 64 bits</span><span class="sxs-lookup"><span data-stu-id="ea8e7-167">Example (3):  set the web app to run in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a><span data-ttu-id="ea8e7-168">Cambio del estado de una aplicación web existente</span><span class="sxs-lookup"><span data-stu-id="ea8e7-168">Change the state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="ea8e7-169">Reinicio de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="ea8e7-169">Restart a web app</span></span>
<span data-ttu-id="ea8e7-170">Para reiniciar una aplicación web, debe especificar el nombre y grupo de recursos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-170">To restart a web app, you must specify the name and resource group of the web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="ea8e7-171">Detención de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="ea8e7-171">Stop a web app</span></span>
<span data-ttu-id="ea8e7-172">Para detener una aplicación web, debe especificar el nombre y grupo de recursos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-172">To stop a web app, you must specify the name and resource group of the web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="ea8e7-173">Inicio de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="ea8e7-173">Start a web app</span></span>
<span data-ttu-id="ea8e7-174">Para iniciar una aplicación web, debe especificar el nombre y grupo de recursos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-174">To start a web app, you must specify the name and resource group of the web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="ea8e7-175">Administración de perfiles de publicación de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="ea8e7-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="ea8e7-176">Cada aplicación web tiene un perfil de publicación que se puede utilizar para publicar las aplicaciones y en dichos perfiles se pueden ejecutar varias operaciones.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="ea8e7-177">Obtención de un perfil de publicación</span><span class="sxs-lookup"><span data-stu-id="ea8e7-177">Get Publishing Profile</span></span>
<span data-ttu-id="ea8e7-178">Para obtener el perfil de publicación de una aplicación web, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-178">To get the publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="ea8e7-179">Este comando reproduce el perfil de publicación en la línea de comandos y enviará el perfil de publicación a un archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="ea8e7-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="ea8e7-180">Restablecimiento de un perfil de publicación</span><span class="sxs-lookup"><span data-stu-id="ea8e7-180">Reset Publishing Profile</span></span>
<span data-ttu-id="ea8e7-181">Para restablecer tanto la contraseña de publicación para FTP como la implementación web de una aplicación web, use:</span><span class="sxs-lookup"><span data-stu-id="ea8e7-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="ea8e7-182">Administración de certificados de aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="ea8e7-182">Manage Web App Certificates</span></span>
<span data-ttu-id="ea8e7-183">Para obtener información acerca de cómo administrar certificados de aplicaciones web, consulte [Enlace de certificados SSL con Servicio de aplicaciones de Azure mediante PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="ea8e7-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="ea8e7-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea8e7-184">Next Steps</span></span>
* <span data-ttu-id="ea8e7-185">Para obtener información sobre la compatibilidad de PowerShell con Azure Resource Manager, consulte [Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="ea8e7-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="ea8e7-186">Para obtener información acerca de los entornos del Servicio de aplicaciones, consulte [Introducción al entorno del Servicio de aplicaciones](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ea8e7-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="ea8e7-187">Para obtener más información acerca de cómo administrar los certificados SSL del Servicio de aplicaciones mediante PowerShell, consulte [Enlace de certificados SSL con Servicio de aplicaciones de Azure mediante PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="ea8e7-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="ea8e7-188">Para obtener más información acerca de la lista completa de los cmdlets de PowerShell basados en Azure Resource Manager para Aplicaciones web de Azure, consulte la [referencia de los cmdlets de PowerShell basados en Azure Resource Manager de aplicaciones web](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="ea8e7-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="ea8e7-189">Para más información acerca de cómo administrar App Service mediante una CLI, consulte [Using Azure Resource Manager-Based XPlat CLI for Azure Web App](app-service-web-app-azure-resource-manager-xplat-cli.md) (Uso de una CLI multiplataforma basada en Azure Resource Manager para aplicaciones web de Azure).</span><span class="sxs-lookup"><span data-stu-id="ea8e7-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

