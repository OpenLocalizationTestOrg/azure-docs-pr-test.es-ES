---
title: "Herramientas de línea de comandos multiplataforma basadas en Azure Resource Manager | Microsoft Docs"
description: "Aprenda a usar las nuevas herramientas de línea de comandos multiplataforma basadas en Azure Resource Manager para administrar sus aplicaciones web de Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="6aa0d-103">Uso de la CLI de XPlat basada en Azure Resource Manager para Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6aa0d-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6aa0d-104">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6aa0d-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="6aa0d-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6aa0d-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="6aa0d-106">Con el lanzamiento de la versión 0.10.5 de las herramientas de línea de comandos multiplataforma de Microsoft Azure, se han agregado nuevos comandos.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="6aa0d-107">Estos comandos ofrecen la posibilidad de usar comandos de PowerShell basados en Azure Resource Manager para administrar App Service.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span></span>

<span data-ttu-id="6aa0d-108">Para más información sobre cómo administrar grupos de recursos, consulte [Uso de la CLI de Azure para administrar los recursos y grupos de recursos de Azure](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6aa0d-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="6aa0d-109">Además, pruebe la [CLI de Azure 2.0](https://github.com/Azure/azure-cli), una CLI de última generación escrita en Python para el modelo de implementación de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="6aa0d-110">Administración de planes del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6aa0d-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="6aa0d-111">Creación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6aa0d-111">Create an App Service Plan</span></span>
<span data-ttu-id="6aa0d-112">Para crear un plan de App Service, use el comando **azure appserviceplan create**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-112">To create an app service plan, use the **azure appserviceplan create** command.</span></span>

<span data-ttu-id="6aa0d-113">Estas son las descripciones de los distintos parámetros:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-113">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="6aa0d-114">**--resource-group**: grupo de recursos que incluye el plan de App Service reciñen creado.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-114">**--resource-group**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="6aa0d-115">**--name**: nombre del plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-115">**--name**: name of the app service plan.</span></span>
* <span data-ttu-id="6aa0d-116">**--location**: ubicación del plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="6aa0d-117">**--sku**:  la sku de precios deseada; las opciones son: F1 (Gratis).</span><span class="sxs-lookup"><span data-stu-id="6aa0d-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span></span> <span data-ttu-id="6aa0d-118">D1 (Compartida).</span><span class="sxs-lookup"><span data-stu-id="6aa0d-118">D1 (Shared).</span></span> <span data-ttu-id="6aa0d-119">B1 (Básico inferior), B2 (Básico medio) y B3 (Básico superior).</span><span class="sxs-lookup"><span data-stu-id="6aa0d-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="6aa0d-120">S1 (Estándar inferior), S2 (Estándar medio) y S3 (Estándar superior).</span><span class="sxs-lookup"><span data-stu-id="6aa0d-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="6aa0d-121">P1 (Premium inferior), P2 (Premium medio) y P3 (Premium superior).)</span><span class="sxs-lookup"><span data-stu-id="6aa0d-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="6aa0d-122">**--instances**: el número de trabajos en el plan de App Service (el valor predeterminado es 1).</span><span class="sxs-lookup"><span data-stu-id="6aa0d-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span></span>

<span data-ttu-id="6aa0d-123">Ejemplo para usar este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-123">Example to use this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="6aa0d-124">Creación de un plan de App Service de Linux</span><span class="sxs-lookup"><span data-stu-id="6aa0d-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="6aa0d-125">Con el mismo comando **azure appserviceplan create**, con el parámetro adicional **--islinux true**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span></span> <span data-ttu-id="6aa0d-126">Tenga en cuenta las restricciones y las regiones que se describen en [Introducción a App Service en Linux](app-service-linux-intro.md).</span><span class="sxs-lookup"><span data-stu-id="6aa0d-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="6aa0d-127">Enumeración de planes del Servicio de aplicaciones existentes</span><span class="sxs-lookup"><span data-stu-id="6aa0d-127">List Existing App Service Plans</span></span>
<span data-ttu-id="6aa0d-128">Para enumerar los planes de App Service existentes, use el cmdlet **azure appserviceplan list**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-128">To list the existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="6aa0d-129">Para enumerar todos los planes del Servicio de aplicaciones de un grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-129">To list all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="6aa0d-130">Para obtener un plan de App Service específico, use el cmdlet **azure appserviceplan show**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-130">To get a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="6aa0d-131">Configuración de un plan del Servicio de aplicaciones existente</span><span class="sxs-lookup"><span data-stu-id="6aa0d-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="6aa0d-132">Para cambiar la configuración de un plan de App Service existente, use el cmdlet **azure appserviceplan config**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span></span> <span data-ttu-id="6aa0d-133">Puede cambiar la sku y el número de trabajos.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-133">You can change the sku, and the number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="6aa0d-134">Escalado de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6aa0d-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="6aa0d-135">Para escalar un plan del Servicio de aplicaciones existente, use:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-135">To scale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a><span data-ttu-id="6aa0d-136">Cambio de la SKU de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="6aa0d-136">Changing the SKU of an App Service Plan</span></span>
<span data-ttu-id="6aa0d-137">Para cambiar la sku de un plan de App Service, use:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-137">To change the sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="6aa0d-138">Eliminación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6aa0d-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="6aa0d-139">Para eliminar un plan de App Service existente, primero se deben mover o eliminar todas las aplicaciones asignadas.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span></span> <span data-ttu-id="6aa0d-140">A continuación, mediante el comando **azure webapp delete**, puede eliminar el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-140">Then using the **azure webapp delete** command you can delete the app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="6aa0d-141">Administración de aplicaciones de App Service</span><span class="sxs-lookup"><span data-stu-id="6aa0d-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="6aa0d-142">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="6aa0d-142">Create a web app</span></span>
<span data-ttu-id="6aa0d-143">Para crear una aplicación web, use el comando **azure webapp create**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-143">To create a web app, use the **azure webapp create** command.</span></span>

<span data-ttu-id="6aa0d-144">Estas son las descripciones de los distintos parámetros:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-144">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="6aa0d-145">**--name**: nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-145">**--name**: name for the web app.</span></span>
* <span data-ttu-id="6aa0d-146">**--plan**: nombre del plan usado para hospedar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-146">**--plan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="6aa0d-147">**--resource-group**: grupo de recursos que hospeda el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-147">**--resource-group**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="6aa0d-148">**--location**: la ubicación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-148">**--location**: the web app location.</span></span>

<span data-ttu-id="6aa0d-149">Ejemplo para usar este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-149">Example to use this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="6aa0d-150">Eliminación de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="6aa0d-150">Delete an existing app</span></span>
<span data-ttu-id="6aa0d-151">Para eliminar una aplicación existente, puede usar el comando **zure webapp delete**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-151">To delete an existing app, you can use the **azure webapp delete** command.</span></span> <span data-ttu-id="6aa0d-152">Debe especificar el nombre de la aplicación y el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-152">You need to specify the name of the app and the resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="6aa0d-153">Lista de aplicaciones existentes</span><span class="sxs-lookup"><span data-stu-id="6aa0d-153">List existing apps</span></span>
<span data-ttu-id="6aa0d-154">Para enumerar las aplicaciones existentes, use el comando **azure webapp list**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-154">To list the existing apps, use the **azure webapp list** command.</span></span>

<span data-ttu-id="6aa0d-155">Para enumerar todas los aplicaciones de un grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-155">To list all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="6aa0d-156">Para obtener una aplicación específica, use el comando **azure webapp show**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-156">To get a specific app, use the **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="6aa0d-157">Configuración de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="6aa0d-157">Configure an existing app</span></span>
<span data-ttu-id="6aa0d-158">Para cambiar los valores y las configuraciones de una aplicación existente, use el comando **azure webapp config set**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span></span>

<span data-ttu-id="6aa0d-159">Ejemplo (1): Cambio de la versión de php de una aplicación</span><span class="sxs-lookup"><span data-stu-id="6aa0d-159">Example (1): change the php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="6aa0d-160">Ejemplo (2): Adición o cambio de la configuración de una aplicación</span><span class="sxs-lookup"><span data-stu-id="6aa0d-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="6aa0d-161">Para saber qué otra configuración se puede cambiar, use el comando **azure webapp config set -h**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span></span>

### <a name="change-the-state-of-an-existing-app"></a><span data-ttu-id="6aa0d-162">Cambio del estado de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="6aa0d-162">Change the state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="6aa0d-163">Reinicio de una aplicación</span><span class="sxs-lookup"><span data-stu-id="6aa0d-163">Restart an app</span></span>
<span data-ttu-id="6aa0d-164">Para reiniciar una aplicación, debe especificar el nombre y grupo de recursos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-164">To restart an app, you must specify the name and resource group of the app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="6aa0d-165">Detener una aplicación</span><span class="sxs-lookup"><span data-stu-id="6aa0d-165">Stop an app</span></span>
<span data-ttu-id="6aa0d-166">Para detener una aplicación, debe especificar el nombre y grupo de recursos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-166">To stop an app, you must specify the name and resource group of the app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="6aa0d-167">Inicio de una aplicación</span><span class="sxs-lookup"><span data-stu-id="6aa0d-167">Start an app</span></span>
<span data-ttu-id="6aa0d-168">Para iniciar una aplicación, debe especificar el nombre y grupo de recursos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-168">To start an app, you must specify the name and resource group of the app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="6aa0d-169">Administración de perfiles de publicación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="6aa0d-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="6aa0d-170">Cada aplicación tiene un perfil de publicación que puede usarse para publicar el código.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-170">Each app has a publishing profile that can be used to publish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="6aa0d-171">Obtención de un perfil de publicación</span><span class="sxs-lookup"><span data-stu-id="6aa0d-171">Get Publishing Profile</span></span>
<span data-ttu-id="6aa0d-172">Para obtener el perfil de publicación de una aplicación, use:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-172">To get the publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="6aa0d-173">Este comando devuelve el nombre de usuario y la contraseña del perfil de publicación a la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-173">This command echoes the publishing profile username and password to the command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="6aa0d-174">Administración de nombres de host de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="6aa0d-174">Manage app hostnames</span></span>
<span data-ttu-id="6aa0d-175">Para administrar los enlaces de nombre de host de la aplicación, use el comando **azure webapp config hostnames**.</span><span class="sxs-lookup"><span data-stu-id="6aa0d-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="6aa0d-176">Enumeración de enlaces de nombre de host</span><span class="sxs-lookup"><span data-stu-id="6aa0d-176">List hostname bindings</span></span>
<span data-ttu-id="6aa0d-177">Para obtener los enlaces de nombre de host actuales de una aplicación, use:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-177">To get the current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="6aa0d-178">Adición de enlaces de nombre de host</span><span class="sxs-lookup"><span data-stu-id="6aa0d-178">Add hostname bindings</span></span>
<span data-ttu-id="6aa0d-179">Para agregar enlaces de nombre de host a una aplicación, use:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-179">To add hostname bindings to an app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="6aa0d-180">Eliminación de enlaces de nombre de host</span><span class="sxs-lookup"><span data-stu-id="6aa0d-180">Delete hostname bindings</span></span>
<span data-ttu-id="6aa0d-181">Para eliminar enlaces de nombre de host, use:</span><span class="sxs-lookup"><span data-stu-id="6aa0d-181">To delete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="6aa0d-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6aa0d-182">Next Steps</span></span>
* <span data-ttu-id="6aa0d-183">Para aprender sobre la compatibilidad con la CLI de Azure Resource Manager, consulte [Uso de la CLI de Azure para administrar los recursos y grupos de recursos de Azure.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="6aa0d-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="6aa0d-184">Para más información sobre cómo administrar App Service con PowerShell, consulte [Uso de PowerShell basado en Azure Resource Manager para administrar aplicaciones web de Azure.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="6aa0d-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="6aa0d-185">Para más información sobre Azure App Service, consulte [Introducción a App Service en Linux](app-service-linux-intro.md).</span><span class="sxs-lookup"><span data-stu-id="6aa0d-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>
