---
title: "aaaAzure herramientas de línea de comandos multiplataforma basada en el Administrador de recursos para la aplicación Web de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola nuevo toomanage basado en Azure Resource Manager herramientas de línea de comandos multiplataforma sus aplicaciones Web de Azure."
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
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="97bf3-103">Uso de la CLI de XPlat basada en Azure Resource Manager para Azure App Service</span><span class="sxs-lookup"><span data-stu-id="97bf3-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97bf3-104">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="97bf3-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="97bf3-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="97bf3-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="97bf3-106">Versión de Hola de versión de las herramientas de línea de comandos entre plataformas de Microsoft Azure 0.10.5, se han agregado nuevos comandos.</span><span class="sxs-lookup"><span data-stu-id="97bf3-106">With hello release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="97bf3-107">Estos comandos proporcionan Hola usuario Hola capacidad toouse basado en el Administrador de recursos de Azure PowerShell comandos toomanage servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="97bf3-107">These commands give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage App Service.</span></span>

<span data-ttu-id="97bf3-108">toolearn acerca de cómo administrar grupos de recursos, consulte [usar hello Azure CLI toomanage Azure y grupos de recursos](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="97bf3-108">toolearn about managing Resource Groups, see [Use hello Azure CLI toomanage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="97bf3-109">Además, pruebe [CLI de Azure 2.0](https://github.com/Azure/azure-cli), una CLI de próxima generación escrito en Python para el modelo de implementación de administración de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bf3-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for hello resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="97bf3-110">Administración de planes del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="97bf3-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="97bf3-111">Creación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="97bf3-111">Create an App Service Plan</span></span>
<span data-ttu-id="97bf3-112">toocreate un plan de servicio de aplicaciones, usar hello **appserviceplan azure crear** comando.</span><span class="sxs-lookup"><span data-stu-id="97bf3-112">toocreate an app service plan, use hello **azure appserviceplan create** command.</span></span>

<span data-ttu-id="97bf3-113">Siguientes son las descripciones de parámetros diferentes hello:</span><span class="sxs-lookup"><span data-stu-id="97bf3-113">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="97bf3-114">**: grupo de recursos**: grupo de recursos que incluye el plan de servicio de aplicación Hola recién creado.</span><span class="sxs-lookup"><span data-stu-id="97bf3-114">**--resource-group**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="97bf3-115">**--nombre**: nombre del plan de servicio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="97bf3-115">**--name**: name of hello app service plan.</span></span>
* <span data-ttu-id="97bf3-116">**--location**: ubicación del plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="97bf3-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="97bf3-117">**--sku**: Hola deseado sku precios (Hola opciones son: F1 (Free).</span><span class="sxs-lookup"><span data-stu-id="97bf3-117">**--sku**:  hello desired pricing sku (hello options are: F1 (Free).</span></span> <span data-ttu-id="97bf3-118">D1 (Compartida).</span><span class="sxs-lookup"><span data-stu-id="97bf3-118">D1 (Shared).</span></span> <span data-ttu-id="97bf3-119">B1 (Básico inferior), B2 (Básico medio) y B3 (Básico superior).</span><span class="sxs-lookup"><span data-stu-id="97bf3-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="97bf3-120">S1 (Estándar inferior), S2 (Estándar medio) y S3 (Estándar superior).</span><span class="sxs-lookup"><span data-stu-id="97bf3-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="97bf3-121">P1 (Premium inferior), P2 (Premium medio) y P3 (Premium superior).)</span><span class="sxs-lookup"><span data-stu-id="97bf3-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="97bf3-122">**--instancias**: Hola el número de trabajos en el plan de servicio de aplicación Hola (el valor predeterminado es 1).</span><span class="sxs-lookup"><span data-stu-id="97bf3-122">**--instances**: hello number of workers in hello app service plan (Default value is 1).</span></span>

<span data-ttu-id="97bf3-123">En el ejemplo se toouse este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="97bf3-123">Example toouse this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="97bf3-124">Creación de un plan de App Service de Linux</span><span class="sxs-lookup"><span data-stu-id="97bf3-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="97bf3-125">Usar Hola mismo **appserviceplan azure crear** comando con hello parámetro adicional **--islinux true**.</span><span class="sxs-lookup"><span data-stu-id="97bf3-125">Using hello same **azure appserviceplan create** command, with hello extra parameter **--islinux true**.</span></span> <span data-ttu-id="97bf3-126">Tenga en cuenta las restricciones de Hola y regiones que se describen en [Introducción tooApp servicio en Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="97bf3-126">Note hello restrictions and regions outlined in [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="97bf3-127">Enumeración de planes del Servicio de aplicaciones existentes</span><span class="sxs-lookup"><span data-stu-id="97bf3-127">List Existing App Service Plans</span></span>
<span data-ttu-id="97bf3-128">usar planes de servicio de aplicación existente de toolist hello, **appserviceplan azure lista** comando.</span><span class="sxs-lookup"><span data-stu-id="97bf3-128">toolist hello existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="97bf3-129">toolist todos los planes de servicio de aplicaciones en un grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="97bf3-129">toolist all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="97bf3-130">tooget un plan de servicio de aplicación específica, use **appserviceplan azure mostrar** comando:</span><span class="sxs-lookup"><span data-stu-id="97bf3-130">tooget a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="97bf3-131">Configuración de un plan del Servicio de aplicaciones existente</span><span class="sxs-lookup"><span data-stu-id="97bf3-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="97bf3-132">toochange Hola de un plan de servicio de aplicación existente, utilice hello **appserviceplan azure config** comando.</span><span class="sxs-lookup"><span data-stu-id="97bf3-132">toochange hello settings for an existing app service plan, use hello **azure appserviceplan config** command.</span></span> <span data-ttu-id="97bf3-133">Puede cambiar Hola sku y el número de trabajos Hola</span><span class="sxs-lookup"><span data-stu-id="97bf3-133">You can change hello sku, and hello number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="97bf3-134">Escalado de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="97bf3-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="97bf3-135">tooscale una existente aplicación Plan del servicio, use:</span><span class="sxs-lookup"><span data-stu-id="97bf3-135">tooscale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a><span data-ttu-id="97bf3-136">Cambiar Hola SKU de un Plan de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="97bf3-136">Changing hello SKU of an App Service Plan</span></span>
<span data-ttu-id="97bf3-137">sku de hello toochange una existente aplicación de servicio del Plan de, use:</span><span class="sxs-lookup"><span data-stu-id="97bf3-137">toochange hello sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="97bf3-138">Eliminación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="97bf3-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="97bf3-139">toodelete un plan de servicio de aplicación existente, todas asignadas aplicaciones necesidad toobe movido o eliminado en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="97bf3-139">toodelete an existing app service plan, all assigned apps need toobe moved or deleted first.</span></span> <span data-ttu-id="97bf3-140">A continuación, usar Hola **webapp azure eliminar** comando se puede eliminar el plan de servicio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="97bf3-140">Then using hello **azure webapp delete** command you can delete hello app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="97bf3-141">Administración de aplicaciones de App Service</span><span class="sxs-lookup"><span data-stu-id="97bf3-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="97bf3-142">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="97bf3-142">Create a web app</span></span>
<span data-ttu-id="97bf3-143">toocreate una aplicación web, utilice hello **crear webapp azure** comando.</span><span class="sxs-lookup"><span data-stu-id="97bf3-143">toocreate a web app, use hello **azure webapp create** command.</span></span>

<span data-ttu-id="97bf3-144">Siguientes son las descripciones de parámetros diferentes hello:</span><span class="sxs-lookup"><span data-stu-id="97bf3-144">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="97bf3-145">**--nombre**: nombre de la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bf3-145">**--name**: name for hello web app.</span></span>
* <span data-ttu-id="97bf3-146">**--plan**: nombre para el plan de servicio Hola utiliza toohost hello web app.</span><span class="sxs-lookup"><span data-stu-id="97bf3-146">**--plan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="97bf3-147">**: grupo de recursos**: grupo de recursos que hospeda el plan de servicio de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="97bf3-147">**--resource-group**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="97bf3-148">**--ubicación**: Hola ubicación de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="97bf3-148">**--location**: hello web app location.</span></span>

<span data-ttu-id="97bf3-149">En el ejemplo se toouse este cmdlet:</span><span class="sxs-lookup"><span data-stu-id="97bf3-149">Example toouse this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="97bf3-150">Eliminación de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="97bf3-150">Delete an existing app</span></span>
<span data-ttu-id="97bf3-151">toodelete una aplicación existente, puede usar hello **webapp azure eliminar** comando.</span><span class="sxs-lookup"><span data-stu-id="97bf3-151">toodelete an existing app, you can use hello **azure webapp delete** command.</span></span> <span data-ttu-id="97bf3-152">Necesita nombre de hello toospecify de aplicación hello y nombre de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="97bf3-152">You need toospecify hello name of hello app and hello resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="97bf3-153">Lista de aplicaciones existentes</span><span class="sxs-lookup"><span data-stu-id="97bf3-153">List existing apps</span></span>
<span data-ttu-id="97bf3-154">toolist hello las aplicaciones existentes, utilice hello **webapp azure lista** comando.</span><span class="sxs-lookup"><span data-stu-id="97bf3-154">toolist hello existing apps, use hello **azure webapp list** command.</span></span>

<span data-ttu-id="97bf3-155">toolist todas las aplicaciones en un grupo de recursos específico, use:</span><span class="sxs-lookup"><span data-stu-id="97bf3-155">toolist all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="97bf3-156">tooget una aplicación específica, use hello **webapp azure mostrar** comando.</span><span class="sxs-lookup"><span data-stu-id="97bf3-156">tooget a specific app, use hello **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="97bf3-157">Configuración de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="97bf3-157">Configure an existing app</span></span>
<span data-ttu-id="97bf3-158">configuraciones de hello toochange y para una aplicación existente, use hello **conjunto de configuración de aplicación Web de azure** comando.</span><span class="sxs-lookup"><span data-stu-id="97bf3-158">toochange hello settings and configurations for an existing app, use hello **azure webapp config set** command.</span></span>

<span data-ttu-id="97bf3-159">Ejemplo (1): cambiar versión de php Hola de una aplicación</span><span class="sxs-lookup"><span data-stu-id="97bf3-159">Example (1): change hello php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="97bf3-160">Ejemplo (2): Adición o cambio de la configuración de una aplicación</span><span class="sxs-lookup"><span data-stu-id="97bf3-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="97bf3-161">tooknow se puede cambiar la configuración de otra, use hello **-h de conjunto de configuración de aplicación Web de azure** comando.</span><span class="sxs-lookup"><span data-stu-id="97bf3-161">tooknow what other configuration can be changed, use hello **azure webapp config set -h** command.</span></span>

### <a name="change-hello-state-of-an-existing-app"></a><span data-ttu-id="97bf3-162">Cambio de estado de Hola de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="97bf3-162">Change hello state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="97bf3-163">Reinicio de una aplicación</span><span class="sxs-lookup"><span data-stu-id="97bf3-163">Restart an app</span></span>
<span data-ttu-id="97bf3-164">toorestart una aplicación, debe especificar Hola nombre del grupo de recursos de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="97bf3-164">toorestart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="97bf3-165">Detener una aplicación</span><span class="sxs-lookup"><span data-stu-id="97bf3-165">Stop an app</span></span>
<span data-ttu-id="97bf3-166">toostop una aplicación, debe especificar Hola nombre del grupo de recursos de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="97bf3-166">toostop an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="97bf3-167">Inicio de una aplicación</span><span class="sxs-lookup"><span data-stu-id="97bf3-167">Start an app</span></span>
<span data-ttu-id="97bf3-168">toostart una aplicación, debe especificar Hola nombre del grupo de recursos de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="97bf3-168">toostart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="97bf3-169">Administración de perfiles de publicación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="97bf3-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="97bf3-170">Cada aplicación tiene un perfil de publicación que puede ser toopublish usado el código.</span><span class="sxs-lookup"><span data-stu-id="97bf3-170">Each app has a publishing profile that can be used toopublish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="97bf3-171">Obtención de un perfil de publicación</span><span class="sxs-lookup"><span data-stu-id="97bf3-171">Get Publishing Profile</span></span>
<span data-ttu-id="97bf3-172">tooget Hola de perfil para una aplicación, el uso de publicación:</span><span class="sxs-lookup"><span data-stu-id="97bf3-172">tooget hello publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="97bf3-173">Este comando devuelve el eco hello línea de comandos de toohello de nombre de usuario y contraseña de perfil de publicación.</span><span class="sxs-lookup"><span data-stu-id="97bf3-173">This command echoes hello publishing profile username and password toohello command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="97bf3-174">Administración de nombres de host de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="97bf3-174">Manage app hostnames</span></span>
<span data-ttu-id="97bf3-175">toomanage enlaces de nombre de host para la aplicación, utilice hello **los nombres de host de configuración de aplicación Web de azure** comando</span><span class="sxs-lookup"><span data-stu-id="97bf3-175">toomanage hostname bindings for your app, use hello **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="97bf3-176">Enumeración de enlaces de nombre de host</span><span class="sxs-lookup"><span data-stu-id="97bf3-176">List hostname bindings</span></span>
<span data-ttu-id="97bf3-177">enlaces tooget Hola de nombre de host actual para una aplicación, use:</span><span class="sxs-lookup"><span data-stu-id="97bf3-177">tooget hello current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="97bf3-178">Adición de enlaces de nombre de host</span><span class="sxs-lookup"><span data-stu-id="97bf3-178">Add hostname bindings</span></span>
<span data-ttu-id="97bf3-179">tooadd hostname enlaces tooan a la aplicación, use:</span><span class="sxs-lookup"><span data-stu-id="97bf3-179">tooadd hostname bindings tooan app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="97bf3-180">Eliminación de enlaces de nombre de host</span><span class="sxs-lookup"><span data-stu-id="97bf3-180">Delete hostname bindings</span></span>
<span data-ttu-id="97bf3-181">enlaces de nombre de host de toodelete, use:</span><span class="sxs-lookup"><span data-stu-id="97bf3-181">toodelete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="97bf3-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97bf3-182">Next Steps</span></span>
* <span data-ttu-id="97bf3-183">toolearn acerca del soporte técnico de Azure Resource Manager CLI, consulte [usar hello Azure CLI toomanage Azure y grupos de recursos.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="97bf3-183">toolearn about Azure Resource Manager CLI support, see [Use hello Azure CLI toomanage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="97bf3-184">toolearn acerca de cómo administrar el servicio de aplicaciones con PowerShell, vea [Using Azure Resource Manager-Based PowerShell tooManage aplicaciones Web de Azure.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="97bf3-184">toolearn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="97bf3-185">toolearn sobre el servicio de aplicaciones de Azure en Linux, consulte [Introducción tooApp servicio en Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="97bf3-185">toolearn about Azure App Service on Linux, see [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>
