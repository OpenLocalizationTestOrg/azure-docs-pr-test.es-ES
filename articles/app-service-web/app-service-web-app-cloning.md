---
title: "aaaWeb aplicación clonación con PowerShell"
description: "Obtenga información acerca de cómo tooclone las aplicaciones de Web toonew de aplicaciones Web con PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="7185f-103">Clonación de aplicaciones del Servicio de aplicaciones de Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7185f-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="7185f-104">Con versión de Hola de Microsoft Azure PowerShell versión 1.1.0 una nueva opción ha sido agregado AzureRMWebApp tooNew que daría Hola usuario Hola capacidad tooclone una aplicación de tooa que acaba de crear aplicación Web existente en una región diferente o en hello misma región.</span><span class="sxs-lookup"><span data-stu-id="7185f-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new option has been added tooNew-AzureRMWebApp that would give hello user hello ability tooclone an existing Web App tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="7185f-105">Esto le permitirá clientes toodeploy un número de aplicaciones en diferentes regiones rápida y fácilmente.</span><span class="sxs-lookup"><span data-stu-id="7185f-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="7185f-106">La clonación de aplicaciones actualmente solo se admite para los planes de Servicio de aplicaciones de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="7185f-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="7185f-107">los usos de característica nuevos Hola Hola mismo limitaciones como característica de copia de seguridad de aplicaciones Web, consulte [copia de seguridad una aplicación web en el servicio de aplicación de Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="7185f-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="7185f-108">toolearn sobre el uso de Azure Resource Manager según toomanage de cmdlets de PowerShell de Azure, la protección de aplicaciones Web [Azure Resource Manager según los comandos de PowerShell para la aplicación Web de Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="7185f-108">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="7185f-109">Clonación de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="7185f-109">Cloning an existing App</span></span>
<span data-ttu-id="7185f-110">Escenario: Una aplicación web existente en la región Ee.uu. Central sur, usuario Hola gustaría tooclone Hola contenido tooa nueva aplicación web en la región Ee.uu. Central Norte.</span><span class="sxs-lookup"><span data-stu-id="7185f-110">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app in North Central US region.</span></span> <span data-ttu-id="7185f-111">Esto puede realizarse con la versión de Azure Resource Manager de Hola de hello PowerShell cmdlet toocreate una nueva aplicación web con la opción de hello - SourceWebApp.</span><span class="sxs-lookup"><span data-stu-id="7185f-111">This can be accomplished by using hello Azure Resource Manager version of hello PowerShell cmdlet toocreate a new web app with hello -SourceWebApp option.</span></span>

<span data-ttu-id="7185f-112">Conocer los recursos de hello nombre del grupo que contiene la aplicación web de origen de hello, podemos usar Hola siguiendo la información de la aplicación de PowerShell comando tooget Hola origen web (en este caso denominado webapp de origen):</span><span class="sxs-lookup"><span data-stu-id="7185f-112">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="7185f-113">toocreate un nuevo Plan de servicio de aplicación, podemos utilizar comando New-AzureRmAppServicePlan como en el siguiente ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="7185f-113">toocreate a new App Service Plan, we can use New-AzureRmAppServicePlan command as in hello following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="7185f-114">Con hello AzureRmWebApp nuevo comando, podemos crear nueva aplicación de web hello en región de hello Ee.uu. Central Norte y asociar los niveles de premium existente tooan Plan de servicio de aplicaciones, además, podemos utilizar Hola mismo recurso de grupo como aplicación web de origen de Hola o definir un nuevo grupo de recursos , siguiente Hola demuestra que:</span><span class="sxs-lookup"><span data-stu-id="7185f-114">Using hello New-AzureRmWebApp command, we can create hello new web app in hello North Central US region, and tie it tooan existing premium tier App Service Plan, moreover we can use hello same resource group as hello source web app, or define a new resource group, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="7185f-115">tooclone una aplicación web existente incluidas todas las ranuras de implementación asociado, el usuario de hello deberá toouse Hola IncludeSourceWebAppSlots parámetro, Hola siguiente comando de PowerShell muestra el uso de Hola de ese parámetro con hello AzureRmWebApp nuevo comando:</span><span class="sxs-lookup"><span data-stu-id="7185f-115">tooclone an existing web app including all associated deployment slots, hello user will need toouse hello IncludeSourceWebAppSlots parameter, hello following PowerShell command demonstrates hello use of that parameter with hello New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="7185f-116">tooclone una aplicación web existente en hello misma región, el usuario de hello deberá toocreate un nuevo grupo de recursos y un nuevo servicio de aplicación plan Hola Hola misma región y, a continuación, usar después de la aplicación web de PowerShell comando tooclone hello</span><span class="sxs-lookup"><span data-stu-id="7185f-116">tooclone an existing web app within hello same region, hello user will need toocreate a new resource group and a new app service plan in hello same region, and then using hello following PowerShell command tooclone hello web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="7185f-117">Clonar un tooan de aplicación existente entorno del servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7185f-117">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="7185f-118">Escenario: Una aplicación web existente en la región Ee.uu. Central sur, usuario Hola gustaría tooclone Hola contenido tooa nueva web app tooan existente entorno de servicio de aplicación (ASE).</span><span class="sxs-lookup"><span data-stu-id="7185f-118">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app tooan existing App Service Environment (ASE).</span></span>

<span data-ttu-id="7185f-119">Conocer los recursos de hello nombre del grupo que contiene la aplicación web de origen de hello, podemos usar Hola siguiendo la información de la aplicación de PowerShell comando tooget Hola origen web (en este caso denominado webapp de origen):</span><span class="sxs-lookup"><span data-stu-id="7185f-119">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="7185f-120">Conocer el nombre del saludo ASE y nombre de grupo de recursos de Hola Hola ASE pertenece a, usuario de hello puede utilizar comandos Hola New-AzureRmWebApp toocreate Hola nueva aplicación web incluida en hello existente ASE, Hola después de que muestra:</span><span class="sxs-lookup"><span data-stu-id="7185f-120">Knowing hello ASE's name, and hello resource group name that hello ASE belongs to, hello user can use hello New-AzureRmWebApp command toocreate hello new web app in hello existing ASE, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="7185f-121">parámetro de ubicación de Hello es necesario debido a razón de toolegacy, pero en caso de hello de creación de una aplicación en un ASE se omitirán.</span><span class="sxs-lookup"><span data-stu-id="7185f-121">hello Location parameter is required due toolegacy reason, but in hello case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="7185f-122">Clonación de una ranura de aplicación existente</span><span class="sxs-lookup"><span data-stu-id="7185f-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="7185f-123">Escenario: usuario Hola gustaría tooclone un tooeither de ranura de aplicación Web una nueva aplicación Web existente o una nueva ranura de aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="7185f-123">Scenario: hello user would like tooclone an existing Web App Slot tooeither a new Web App or a new Web App slot.</span></span> <span data-ttu-id="7185f-124">Hola nueva aplicación Web puede estar en hello misma región como ranura de aplicación Web de hello original o en una región distinta.</span><span class="sxs-lookup"><span data-stu-id="7185f-124">hello new Web App can be in hello same region as hello original Web App slot or in a different region.</span></span>

<span data-ttu-id="7185f-125">Conocer los recursos de hello nombre del grupo que contiene la aplicación web de origen de hello, podemos usar Hola siguiente información de tooget Hola origen ranura de aplicación web (en este caso se denomina origen webappslot) vinculada tooWeb de aplicación origen webapp de comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7185f-125">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app slot's information (in this case named source-webappslot) tied tooWeb App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="7185f-126">siguiente Hello muestra cómo crear un clon de hello web app tooa nueva aplicación web de origen:</span><span class="sxs-lookup"><span data-stu-id="7185f-126">hello following demonstrates creating a clone of hello source web app tooa new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="7185f-127">Configuración del Administrador de tráfico durante la clonación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="7185f-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="7185f-128">Crear aplicaciones web de varias regiones y configurar Azure Traffic Manager tooroute tráfico tooall estas aplicaciones web, es un tooinsure n escenario importante que las aplicaciones de los clientes son de alta disponibilidad, al clonar una aplicación web existente que tenga Hola opción tooconnect ambos web aplicaciones tooeither un nuevo perfil de administrador de tráfico o uno existente: tenga en cuenta que el Administrador de recursos de Azure solo la versión de Traffic Manager es compatible.</span><span class="sxs-lookup"><span data-stu-id="7185f-128">Creating multi-region web apps and configuring Azure Traffic Manager tooroute traffic tooall these web apps, is a n important scenario tooinsure that customers' apps are highly available, when cloning an existing web app you have hello option tooconnect both web apps tooeither a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="7185f-129">Creación de un nuevo perfil del Administrador de tráfico durante la clonación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="7185f-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="7185f-130">Escenario: usuario Hola gustaría tooclone una región de tooanother de aplicación web, al configurar un perfil de administrador de tráfico de Azure Resource Manager que incluyen las dos aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="7185f-130">Scenario: hello user would like tooclone an web app tooanother region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="7185f-131">siguiente Hello muestra cómo crear un clon de hello web app tooa nueva aplicación web de origen al configurar un nuevo perfil de Traffic Manager:</span><span class="sxs-lookup"><span data-stu-id="7185f-131">hello following demonstrates creating a clone of hello source web app tooa new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a><span data-ttu-id="7185f-132">Agregar nueva clonado aplicación Web tooan Traffic Manager perfil existente</span><span class="sxs-lookup"><span data-stu-id="7185f-132">Adding new cloned Web App tooan existing Traffic Manager profile</span></span>
<span data-ttu-id="7185f-133">Escenario: Hola el usuario tiene un perfil de administrador de tráfico de Azure Resource Manager que gustaría tooadd ambas aplicaciones como extremos web.</span><span class="sxs-lookup"><span data-stu-id="7185f-133">Scenario: hello user already have an Azure Resource Manager traffic manager profile that he would like tooadd both web apps as endpoints.</span></span> <span data-ttu-id="7185f-134">toodo por lo tanto, es necesario tooassemble Hola existente de Id. de perfil de administrador de tráfico, necesitamos Id. de suscripción de Hola, nombre del grupo de recursos y nombre de perfil de tráfico existente de hello manager.</span><span class="sxs-lookup"><span data-stu-id="7185f-134">toodo so, we first need tooassemble hello existing traffic manager profile id, we will need hello subscription id, resource group name and hello existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="7185f-135">Si tiene Id. de administrador de tráfico de hello, siguiente hello muestra la creación de un clon de hello web app tooa nueva aplicación web de origen al agregarlos tooan perfil de Traffic Manager existente:</span><span class="sxs-lookup"><span data-stu-id="7185f-135">After having hello traffic manger id, hello following demonstrates creating a clone of hello source web app tooa new web app while adding them tooan existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="7185f-136">Restricciones actuales</span><span class="sxs-lookup"><span data-stu-id="7185f-136">Current Restrictions</span></span>
<span data-ttu-id="7185f-137">Esta característica está actualmente en vista previa, estamos trabajando tooadd nuevas capacidades con el tiempo, Hola lista siguiente se Hola restricciones conocidas de la versión actual de Hola de clonación de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="7185f-137">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current version of app cloning:</span></span>

* <span data-ttu-id="7185f-138">No se clona la configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="7185f-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="7185f-139">No se clona la configuración de programación de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7185f-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="7185f-140">No se clona la configuración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="7185f-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="7185f-141">Detalles de aplicaciones no se establecen automáticamente en la aplicación web de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="7185f-141">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="7185f-142">No se clona la configuración de Easy Auth.</span><span class="sxs-lookup"><span data-stu-id="7185f-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="7185f-143">No se clona la extensión Kudu.</span><span class="sxs-lookup"><span data-stu-id="7185f-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="7185f-144">No se clonan las reglas de TiP.</span><span class="sxs-lookup"><span data-stu-id="7185f-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="7185f-145">No se clona el contenido de la base de datos</span><span class="sxs-lookup"><span data-stu-id="7185f-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="7185f-146">Referencias</span><span class="sxs-lookup"><span data-stu-id="7185f-146">References</span></span>
* [<span data-ttu-id="7185f-147">Comandos de PowerShell basados en Azure Resource Manager para aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="7185f-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="7185f-148">Clonación de aplicaciones web con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7185f-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="7185f-149">Hacer copia de seguridad de una aplicación web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="7185f-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="7185f-150">Compatibilidad de Azure Resource Manager con Traffic Manager (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="7185f-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="7185f-151">Introducción tooApp entorno del servicio</span><span class="sxs-lookup"><span data-stu-id="7185f-151">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="7185f-152">Uso de Azure PowerShell con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7185f-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

