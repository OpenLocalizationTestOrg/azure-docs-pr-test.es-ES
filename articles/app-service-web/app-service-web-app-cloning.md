---
title: "Clonación de aplicaciones web con PowerShell"
description: Aprenda a clonar sus aplicaciones web en nuevas aplicaciones web con PowerShell.
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
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="2ddd2-103">Clonación de aplicaciones del Servicio de aplicaciones de Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ddd2-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="2ddd2-104">Con el lanzamiento de Microsoft Azure PowerShell versión 1.1.0, se ha agregado una nueva opción a New-AzureRMWebApp que podría proporcionar al usuario la capacidad para clonar una aplicación web existente en una aplicación recién creada de una región diferente o de la misma.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="2ddd2-105">Esto permitirá que los clientes implementen varias aplicaciones en diferentes regiones de una forma rápida y sencilla.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="2ddd2-106">La clonación de aplicaciones actualmente solo se admite para los planes de Servicio de aplicaciones de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="2ddd2-107">La nueva característica cuenta con las mismas limitaciones que la característica de copia de seguridad de aplicaciones web; consulte [Hacer copia de seguridad de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="2ddd2-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="2ddd2-108">Para obtener información acerca del uso de cmdlets de Azure PowerShell basados en Azure Resource Manager para administrar aplicaciones web, consulte [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="2ddd2-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="2ddd2-109">Clonación de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="2ddd2-109">Cloning an existing App</span></span>
<span data-ttu-id="2ddd2-110">Escenario: Una aplicación web existente en la región centro-sur de EE. UU.; el usuario desea clonar el contenido en una nueva aplicación web en la región centro-norte de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="2ddd2-111">Esto puede realizarse mediante la versión Azure Resource Manager del cmdlet de PowerShell para crear una nueva aplicación web con la opción -SourceWebApp.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span></span>

<span data-ttu-id="2ddd2-112">Conociendo el nombre del grupo de recursos que contiene la aplicación web de origen, podemos usar el siguiente comando de PowerShell para obtener la información de la aplicación web de origen (en este caso, llamada source-webapp):</span><span class="sxs-lookup"><span data-stu-id="2ddd2-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="2ddd2-113">Para crear un nuevo plan de Servicio de aplicaciones, podemos usar el comando New-AzureRmAppServicePlan como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2ddd2-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="2ddd2-114">Con el comando New-AzureRmWebApp, podemos crear la nueva aplicación web en la región centro-norte de EE. UU. y vincularla a un plan de Servicio de aplicaciones de nivel Premium existente. Además, podemos usar el mismo grupo de recursos que la aplicación web de origen, o bien definir uno nuevo como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="2ddd2-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="2ddd2-115">Para clonar una aplicación web existente, incluidas todas las ranuras de implementación asociadas, el usuario deberá usar el parámetro IncludeSourceWebAppSlots; el siguiente comando de PowerShell muestra el uso de este parámetro con el comando New-AzureRmWebApp:</span><span class="sxs-lookup"><span data-stu-id="2ddd2-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="2ddd2-116">Para clonar una aplicación web existente en la misma región, el usuario deberá crear un nuevo grupo de recursos y un nuevo plan de Servicio de aplicaciones en la misma región y después usar el siguiente comando de PowerShell para clonar la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="2ddd2-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="2ddd2-117">Clonación de una aplicación existente en un entorno de Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="2ddd2-117">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="2ddd2-118">Escenario: Una aplicación web existente en la región centro-sur de EE. UU.; el usuario desea clonar el contenido en una nueva aplicación web en un entorno de Servicio de aplicaciones (ASE) existente.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="2ddd2-119">Conociendo el nombre del grupo de recursos que contiene la aplicación web de origen, podemos usar el siguiente comando de PowerShell para obtener la información de la aplicación web de origen (en este caso, llamada source-webapp):</span><span class="sxs-lookup"><span data-stu-id="2ddd2-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="2ddd2-120">Conociendo el nombre del ASE y el nombre del grupo de recursos al que este pertenece, el usuario puede utilizar el comando New-AzureRmWebApp para crear la nueva aplicación web en el ASE existente, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="2ddd2-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="2ddd2-121">El parámetro Location es necesario por un motivo heredado, pero se pasará por alto cuando se cree una aplicación en un ASE.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="2ddd2-122">Clonación de una ranura de aplicación existente</span><span class="sxs-lookup"><span data-stu-id="2ddd2-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="2ddd2-123">Escenario: El usuario desea clonar una ranura de aplicación web existente en una nueva aplicación web o una nueva ranura de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="2ddd2-124">La nueva aplicación web puede estar en la misma región que la ranura de aplicación web original o en una distinta.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="2ddd2-125">Conociendo el nombre del grupo de recursos que contiene la aplicación web de origen, podemos usar el siguiente comando de PowerShell para obtener la información de la ranura de aplicación web de origen (en este caso, llamada source-webappslot) vinculada a la aplicación web source-webapp:</span><span class="sxs-lookup"><span data-stu-id="2ddd2-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="2ddd2-126">A continuación, se muestra la creación de un clon de la aplicación web de origen en una nueva aplicación web:</span><span class="sxs-lookup"><span data-stu-id="2ddd2-126">The following demonstrates creating a clone of the source web app to a new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="2ddd2-127">Configuración del Administrador de tráfico durante la clonación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="2ddd2-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="2ddd2-128">La creación de aplicaciones web de varias regiones y la configuración del Administrador de tráfico de Azure para enrutar el tráfico a todas estas aplicaciones web son escenarios importantes para asegurarse de que las aplicaciones de los clientes son de alta disponibilidad; al clonar una aplicación web existente, tiene la opción de conectar ambas aplicaciones web a un perfil nuevo del Administrador de tráfico nuevo, o a uno existente. Tenga en cuenta que solo se admite la versión de Azure Resource Manager del Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="2ddd2-129">Creación de un nuevo perfil del Administrador de tráfico durante la clonación de una aplicación</span><span class="sxs-lookup"><span data-stu-id="2ddd2-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="2ddd2-130">Escenario: el usuario desea clonar una aplicación web en otra región, al mismo tiempo que configura un perfil del Administrador de tráfico de Azure Resource Manager que incluya ambas aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="2ddd2-131">Lo siguiente demuestra la creación de un clon de la aplicación web de origen en una nueva aplicación web al tiempo que se configura un nuevo perfil del Administrador de tráfico:</span><span class="sxs-lookup"><span data-stu-id="2ddd2-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="2ddd2-132">Incorporación de una nueva aplicación web clonada a un perfil del Administrador de tráfico existente</span><span class="sxs-lookup"><span data-stu-id="2ddd2-132">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="2ddd2-133">Escenario: el usuario ya tiene un perfil de Administrador de tráfico de Azure Resource Manager al que quiere agregar tanto aplicaciones web como puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span></span> <span data-ttu-id="2ddd2-134">Para hacerlo, primero es necesario ensamblar el identificador del perfil del Administrador de tráfico existente; se necesitará el identificador de la suscripción, el nombre del grupo de recursos y el nombre del perfil del Administrador de tráfico existente.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="2ddd2-135">Después de obtener el identificador del Administrador de tráfico, lo siguiente muestra cómo crear un clon de la aplicación web de origen en una nueva aplicación web al mismo tiempo que se agregan ambas a un perfil del Administrador de tráfico existente:</span><span class="sxs-lookup"><span data-stu-id="2ddd2-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="2ddd2-136">Restricciones actuales</span><span class="sxs-lookup"><span data-stu-id="2ddd2-136">Current Restrictions</span></span>
<span data-ttu-id="2ddd2-137">Esta característica se encuentra actualmente en versión preliminar y estamos trabajando para agregar nueva funcionalidad con el tiempo. En la siguiente lista, se incluyen las restricciones conocidas de la versión actual de la clonación de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="2ddd2-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="2ddd2-138">No se clona la configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="2ddd2-139">No se clona la configuración de programación de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="2ddd2-140">No se clona la configuración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="2ddd2-141">No se instala automáticamente App Insights en la aplicación web de destino.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-141">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="2ddd2-142">No se clona la configuración de Easy Auth.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="2ddd2-143">No se clona la extensión Kudu.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="2ddd2-144">No se clonan las reglas de TiP.</span><span class="sxs-lookup"><span data-stu-id="2ddd2-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="2ddd2-145">No se clona el contenido de la base de datos</span><span class="sxs-lookup"><span data-stu-id="2ddd2-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="2ddd2-146">Referencias</span><span class="sxs-lookup"><span data-stu-id="2ddd2-146">References</span></span>
* [<span data-ttu-id="2ddd2-147">Comandos de PowerShell basados en Azure Resource Manager para aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="2ddd2-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="2ddd2-148">Clonación de aplicaciones web con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2ddd2-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="2ddd2-149">Hacer copia de seguridad de una aplicación web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="2ddd2-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="2ddd2-150">Compatibilidad de Azure Resource Manager con Traffic Manager (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="2ddd2-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="2ddd2-151">Introducción al entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="2ddd2-151">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="2ddd2-152">Uso de Azure PowerShell con el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="2ddd2-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

