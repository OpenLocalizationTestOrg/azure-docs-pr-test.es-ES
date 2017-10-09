---
title: aaaUsing PowerShell toomanage Traffic Manager de Azure | Documentos de Microsoft
description: Uso de PowerShell para Traffic Manager con Azure Resource Manager
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="2f3c8-103">Usar PowerShell toomanage Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2f3c8-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="2f3c8-104">Administrador de recursos de Azure es la interfaz de administración preferido de hello de servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="2f3c8-105">Los perfiles de Traffic Manager se pueden administrar mediante las herramientas y las API basadas en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="2f3c8-106">Modelo de recursos</span><span class="sxs-lookup"><span data-stu-id="2f3c8-106">Resource model</span></span>

<span data-ttu-id="2f3c8-107">El Administrador de tráfico de Azure se configura con una colección de valores denominada perfil del Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="2f3c8-108">Este perfil contiene la configuración de DNS, la configuración de enrutamiento de tráfico, punto de conexión de configuración de supervisión, y se enruta una lista de tráfico de toowhich de puntos de conexión de servicio.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="2f3c8-109">Cada perfil de Traffic Manager se representa mediante un recurso de tipo "TrafficManagerProfiles".</span><span class="sxs-lookup"><span data-stu-id="2f3c8-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="2f3c8-110">En el nivel de API de REST de Hola Hola URI para cada perfil es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="2f3c8-111">Configuración de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f3c8-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="2f3c8-112">En estas instrucciones se usa PowerShell para Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="2f3c8-113">Hello siguiente artículo se explica cómo tooinstall y configurar Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="2f3c8-114">¿Cómo tooinstall y configurar Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f3c8-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="2f3c8-115">ejemplos de Hello en este artículo se supone que tiene un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="2f3c8-116">Puede crear un grupo de recursos mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="2f3c8-117">Azure Resource Manager requiere que todos los grupos de recursos cuenten con una ubicación.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="2f3c8-118">Esta ubicación se utiliza como valor predeterminado de Hola para recursos creados en ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="2f3c8-119">Sin embargo, puesto que los recursos de perfil de Traffic Manager son globales, no regionales, Hola elección de ubicación del grupo de recursos tiene ningún impacto en Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="2f3c8-120">Creación de un perfil del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="2f3c8-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="2f3c8-121">toocreate un perfil de Traffic Manager, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="2f3c8-122">Hello en la tabla siguiente describe los parámetros de hello:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="2f3c8-123">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f3c8-123">Parameter</span></span> | <span data-ttu-id="2f3c8-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f3c8-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2f3c8-125">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f3c8-125">Name</span></span> |<span data-ttu-id="2f3c8-126">nombre de recurso de Hola para hello recursos de perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="2f3c8-127">Perfiles en hello mismo grupo de recursos debe tener nombres únicos.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="2f3c8-128">Este nombre es independiente de nombre DNS de hello usado para las consultas DNS.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="2f3c8-129">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2f3c8-129">ResourceGroupName</span></span> |<span data-ttu-id="2f3c8-130">nombre de Hola de hello grupo contenedor Hola perfil recurso.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="2f3c8-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="2f3c8-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="2f3c8-132">Especifica Hola enrutamiento de tráfico usa el método toodetermine qué extremo se devuelve como respuesta una consulta DNS.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="2f3c8-133">Los valores posibles son "Performance", "Weighted" o "Priority".</span><span class="sxs-lookup"><span data-stu-id="2f3c8-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="2f3c8-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="2f3c8-134">RelativeDnsName</span></span> |<span data-ttu-id="2f3c8-135">Especifica la parte hostname de Hola Hola del nombre de DNS proporcionada por este perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="2f3c8-136">Este valor se combina con el nombre de dominio DNS de hello utilizada Azure Traffic Manager tooform Hola nombre de dominio completo (FQDN) del perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="2f3c8-137">Por ejemplo, el valor de Hola de "contoso" se convierte en 'contoso.trafficmanager.net'.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="2f3c8-138">TTL</span><span class="sxs-lookup"><span data-stu-id="2f3c8-138">TTL</span></span> |<span data-ttu-id="2f3c8-139">Especifica Hola DNS Time-to-Live (TTL), en segundos.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="2f3c8-140">Este TTL informa a los solucionadores de DNS Local hello y los clientes DNS cuánto toocache las respuestas DNS para este perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="2f3c8-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="2f3c8-141">MonitorProtocol</span></span> |<span data-ttu-id="2f3c8-142">Especifica el estado del extremo de hello protocolo toouse toomonitor.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="2f3c8-143">Los valores posibles son "HTTP" y "HTTPS".</span><span class="sxs-lookup"><span data-stu-id="2f3c8-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="2f3c8-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="2f3c8-144">MonitorPort</span></span> |<span data-ttu-id="2f3c8-145">Especifica Hola el puerto TCP utilizado toomonitor estado del extremo.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="2f3c8-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="2f3c8-146">MonitorPath</span></span> |<span data-ttu-id="2f3c8-147">Especifica el nombre de dominio de punto de conexión de hello ruta de acceso relativa toohello utiliza tooprobe mantenimiento del extremo.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="2f3c8-148">Hola cmdlet crea un perfil de Traffic Manager en Azure y devuelve un tooPowerShell de objeto de perfil correspondiente.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="2f3c8-149">En este momento, el perfil de hello no contiene ningún punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="2f3c8-150">Para obtener más información acerca de cómo agregar perfil de Traffic Manager tooa de puntos de conexión, vea [agregar extremos de Traffic Manager](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="2f3c8-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="2f3c8-151">Obtención de un perfil del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="2f3c8-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="2f3c8-152">tooretrieve un objeto de perfil de Traffic Manager existente, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="2f3c8-153">Este cmdlet devuelve un objeto del perfil del Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="2f3c8-154">Actualización de un perfil de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2f3c8-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="2f3c8-155">Para modificar perfiles de Traffic Manager, se sigue un proceso de tres pasos:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="2f3c8-156">Recuperar Hola perfil mediante `Get-AzureRmTrafficManagerProfile` o usar perfil Hola devuelto por `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="2f3c8-157">Modificar perfil Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-157">Modify hello profile.</span></span> <span data-ttu-id="2f3c8-158">Puede agregar y quitar puntos de conexión o cambiar los parámetros del perfil o el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="2f3c8-159">Estos cambios son operaciones fuera de línea.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-159">These changes are off-line operations.</span></span> <span data-ttu-id="2f3c8-160">Objeto local de hello en la memoria que representa el perfil de hello sólo va a cambiar.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="2f3c8-161">Confirmar cambios mediante hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="2f3c8-162">Todas las propiedades de perfil pueden cambiarse excepto RelativeDnsName del perfil de hello.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="2f3c8-163">toochange Hola RelativeDnsName, debe eliminar el perfil y un nuevo perfil con un nombre nuevo.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="2f3c8-164">Hola siguiente ejemplo muestra cómo toochange Hola TTL del perfil:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="2f3c8-165">Existen tres tipos de puntos de conexión de Administrador de tráfico:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="2f3c8-166">Los **puntos de conexión de Azure** son servicios hospedados en Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="2f3c8-167">Los **puntos de conexión externos** son servicios hospedados fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="2f3c8-168">**Anidar extremos** son jerarquías de tooconstruct uso anidado de perfiles de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="2f3c8-169">Los puntos de conexión anidados hacen posibles configuraciones avanzadas de enrutamiento del tráfico para aplicaciones complejas.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="2f3c8-170">En los tres casos, se pueden agregar puntos de conexión de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="2f3c8-171">Mediante el proceso de tres pasos descrito antes.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="2f3c8-172">ventaja de Hola de este método es que pueden realizarse varios cambios de punto de conexión en una única actualización.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="2f3c8-173">Usando el cmdlet New-AzureRmTrafficManagerEndpoint de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="2f3c8-174">Este cmdlet agrega un perfil de Traffic Manager de punto de conexión tooan existente en una sola operación.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="2f3c8-175">Adición de puntos de conexión de Azure</span><span class="sxs-lookup"><span data-stu-id="2f3c8-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="2f3c8-176">Los puntos de conexión de Azure hacen referencia a servicios hospedados en Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="2f3c8-177">Se admiten dos tipos de puntos de conexión de Azure:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="2f3c8-178">Aplicaciones web de Azure </span><span class="sxs-lookup"><span data-stu-id="2f3c8-178">Azure Web Apps</span></span>
2. <span data-ttu-id="2f3c8-179">Recursos de Azure PublicIpAddress (que pueden ser tooa adjunto de equilibrador de carga o una máquina virtual de NIC).</span><span class="sxs-lookup"><span data-stu-id="2f3c8-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="2f3c8-180">Hola PublicIpAddress debe tener un nombre DNS asignado toobe utilizado en el Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="2f3c8-181">En cada caso:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-181">In each case:</span></span>

* <span data-ttu-id="2f3c8-182">servicio de Hola se especifica mediante hello 'elemento targetResourceId' parámetro de `Add-AzureRmTrafficManagerEndpointConfig` o `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="2f3c8-183">Hello 'Target' y 'EndpointLocation' están implícito en el elemento TargetResourceId Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="2f3c8-184">Especificar hello 'Weight' es opcional.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="2f3c8-185">Pesos solo se usan si el perfil de hello es el método de enrutamiento del tráfico de toouse configurado hello 'Weighted'.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="2f3c8-186">En caso contrario, se pasan por alto.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="2f3c8-187">Si se especifica, el valor de hello debe ser un número entre 1 y 1000.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="2f3c8-188">valor predeterminado de Hello es '1'.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-188">hello default value is '1'.</span></span>
* <span data-ttu-id="2f3c8-189">Hola especificando 'Priority' es opcional.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="2f3c8-190">Las prioridades se usan solo si el perfil de hello es el método de enrutamiento del tráfico de toouse configurado hello 'Priority'.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="2f3c8-191">En caso contrario, se pasan por alto.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="2f3c8-192">Los valores válidos son de 1 too1000 con valores más bajos que indica una prioridad más alta.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="2f3c8-193">Si se especifica para un punto de conexión, se debe especificar para todos los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="2f3c8-194">Si se omite, los valores predeterminados a partir de '1' se aplican en orden de Hola que se enumeran los puntos de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="2f3c8-195">Ejemplo 1: Incorporación de puntos de conexión de aplicación web mediante `Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="2f3c8-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="2f3c8-196">En este ejemplo, se crea un perfil de Traffic Manager y agregue dos extremos de aplicación Web con hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="2f3c8-197">Ejemplo 2: Incorporación de un punto de conexión de publicIpAddress mediante `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="2f3c8-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="2f3c8-198">En este ejemplo, un recurso de dirección IP público se agrega toohello perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="2f3c8-199">la dirección IP pública Hola debe tener un nombre DNS configurado y puede estar enlazado cualquier NIC de un equilibrador de carga de la máquina virtual o tooa toohello.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="2f3c8-200">Adición de puntos de conexión externos</span><span class="sxs-lookup"><span data-stu-id="2f3c8-200">Adding External Endpoints</span></span>

<span data-ttu-id="2f3c8-201">El tráfico Manager usa extremos externos toodirect tráfico tooservices hospedado fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="2f3c8-202">Al igual que en el caso de los puntos de conexión de Azure, los puntos de conexión externos se pueden agregar mediante `Add-AzureRmTrafficManagerEndpointConfig` seguido de `Set-AzureRmTrafficManagerProfile` o `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="2f3c8-203">Cuando se especifican puntos de conexión externos:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="2f3c8-204">nombre de dominio de punto de conexión de Hello debe especificarse con el parámetro de 'Target' hello</span><span class="sxs-lookup"><span data-stu-id="2f3c8-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="2f3c8-205">Si se utiliza el método de enrutamiento de tráfico 'Rendimiento' hello, hello 'EndpointLocation' es necesario.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="2f3c8-206">De lo contrario, es opcional.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-206">Otherwise it is optional.</span></span> <span data-ttu-id="2f3c8-207">Hola valor debe ser un [nombre de la región de Azure válida](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="2f3c8-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="2f3c8-208">Hola 'Peso' y 'Priority' es opcional.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="2f3c8-209">Ejemplo 1: Incorporación de puntos de conexión externos mediante `Add-AzureRmTrafficManagerEndpointConfig` y `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="2f3c8-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="2f3c8-210">En este ejemplo, se crea un perfil de Traffic Manager, agregar dos extremos externos y confirmar los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="2f3c8-211">Ejemplo 2: Incorporación de puntos de conexión externos mediante `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="2f3c8-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="2f3c8-212">En este ejemplo, se agrega un perfil existente de tooan de extremo externo.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="2f3c8-213">perfil de Hola se especifica utilizando nombres de grupos de recursos y perfil Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="2f3c8-214">Adición de puntos de conexión "Anidados"</span><span class="sxs-lookup"><span data-stu-id="2f3c8-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="2f3c8-215">Cada perfil del Administrador de tráfico especifica un único método de enrutamiento del tráfico.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="2f3c8-216">Sin embargo, hay escenarios que requieren el enrutamiento del tráfico más sofisticadas de hello enrutamiento proporcionada por un solo perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="2f3c8-217">Puede anidar ventajas de hello toocombine de los perfiles de Traffic Manager de más de un método de enrutamiento de tráfico.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="2f3c8-218">Perfiles anidados permiten toooverride Hola predeterminado Traffic Manager comportamiento toosupport mayor y las implementaciones de aplicaciones más complejas.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="2f3c8-219">Para ejemplos más detallados, consulte [Perfiles anidados de Traffic Manager](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="2f3c8-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="2f3c8-220">Extremos anidados se configuran en el perfil de hello primaria, con un tipo de punto de conexión concreto, 'NestedEndpoints'.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="2f3c8-221">Cuando se especifican puntos de conexión anidados:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="2f3c8-222">punto de conexión de Hello debe especificarse con el parámetro de 'elemento targetResourceId' hello</span><span class="sxs-lookup"><span data-stu-id="2f3c8-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="2f3c8-223">Si se utiliza el método de enrutamiento de tráfico 'Rendimiento' hello, hello 'EndpointLocation' es necesario.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="2f3c8-224">De lo contrario, es opcional.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-224">Otherwise it is optional.</span></span> <span data-ttu-id="2f3c8-225">Hola valor debe ser un [nombre de la región de Azure válida](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="2f3c8-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="2f3c8-226">Hola 'Peso' y 'Priority' es opcional, como para los extremos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="2f3c8-227">parámetro de 'MinChildEndpoints' Hello es opcional.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="2f3c8-228">valor predeterminado de Hello es '1'.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-228">hello default value is '1'.</span></span> <span data-ttu-id="2f3c8-229">Si número Hola de puntos de conexión disponibles cae por debajo del umbral, perfil principal de hello considera perfil secundario de hello 'Degradado' y desvía tráfico toohello otros extremos en el perfil de hello primario.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="2f3c8-230">Ejemplo 1: Incorporación de puntos de conexión anidados mediante `Add-AzureRmTrafficManagerEndpointConfig` y `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="2f3c8-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="2f3c8-231">En este ejemplo, se crear primarias y secundarias de Traffic Manager nuevos perfiles, agrega a secundario hello como elemento primario toohello anidadas de punto de conexión y confirmar los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="2f3c8-232">Por razones de brevedad en este ejemplo, no se ha agregado los otros extremos toohello secundarias o primarias perfiles.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="2f3c8-233">Ejemplo 2: Incorporación de puntos de conexión anidados mediante `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="2f3c8-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="2f3c8-234">En este ejemplo, agregamos un perfil secundario existente como un perfil de primario de extremo anidada tooan existente.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="2f3c8-235">perfil de Hola se especifica utilizando nombres de grupos de recursos y perfil Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="2f3c8-236">Actualización de un punto de conexión de Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="2f3c8-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="2f3c8-237">Hay dos tooupdate formas un punto de conexión de administrador de tráfico existente:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="2f3c8-238">Obtener perfil de Traffic Manager de hello mediante `Get-AzureRmTrafficManagerProfile`, actualizar las propiedades de punto de conexión de hello en el perfil de Hola y confirmar los cambios de hello mediante `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="2f3c8-239">Este método tiene la ventaja de Hola de ser tooupdate capaz de más de un punto de conexión en una sola operación.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="2f3c8-240">Obtener el punto de conexión de administrador de tráfico de hello mediante `Get-AzureRmTrafficManagerEndpoint`, actualizar las propiedades de punto de conexión de Hola y confirmar los cambios de hello mediante `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="2f3c8-241">Este método es más sencillo, ya que no requieren la indización en la matriz de puntos de conexión de hello en el perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="2f3c8-242">Ejemplo 1: Actualización de puntos de conexión mediante `Get-AzureRmTrafficManagerProfile` y `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="2f3c8-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="2f3c8-243">En este ejemplo, se modifique la prioridad de hello en dos puntos de conexión dentro de un perfil existente.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="2f3c8-244">Ejemplo 2: Actualización de un punto de conexión mediante `Get-AzureRmTrafficManagerEndpoint` y `Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="2f3c8-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="2f3c8-245">En este ejemplo, se modifique el peso de Hola de un solo punto de conexión en un perfil existente.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="2f3c8-246">Habilitación y deshabilitación de puntos de conexión y perfiles</span><span class="sxs-lookup"><span data-stu-id="2f3c8-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="2f3c8-247">Traffic Manager permite extremos individuales toobe habilitados y deshabilitados, además de permitir la habilitación y deshabilitación de perfiles completos.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="2f3c8-248">Estos cambios pueden realizarse por los recursos de extremo o un perfil de hello obtener/actualizar/configuración.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="2f3c8-249">toostreamline estas operaciones comunes, también se admiten a través de los cmdlets dedicados.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="2f3c8-250">Ejemplo 1: Habilitación y deshabilitación de un perfil de Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="2f3c8-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="2f3c8-251">tooenable un perfil de Traffic Manager, use `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="2f3c8-252">perfil de Hello puede especificarse mediante un objeto de perfil.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="2f3c8-253">Hello objeto de perfil se puede pasar a través de la canalización de Hola o mediante el uso de hello '-TrafficManagerProfile' parámetro.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="2f3c8-254">En este ejemplo, especificamos perfil Hola por nombre de grupo de recursos y perfil Hola.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="2f3c8-255">toodisable un perfil de Traffic Manager:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="2f3c8-256">Hola Disable-AzureRmTrafficManagerProfile cmdlet pide confirmación.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="2f3c8-257">Este mensaje se puede suprimir con hello '-Force' parámetro.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="2f3c8-258">Ejemplo 2: Habilitación y deshabilitación de un punto de conexión de Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="2f3c8-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="2f3c8-259">usar un punto de conexión de administrador de tráfico, tooenable `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="2f3c8-260">Hay el punto de conexión de dos maneras toospecify Hola</span><span class="sxs-lookup"><span data-stu-id="2f3c8-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="2f3c8-261">Mediante un objeto TrafficManagerEndpoint pasado a través de la canalización de Hola o con hello '-TrafficManagerEndpoint' parámetro</span><span class="sxs-lookup"><span data-stu-id="2f3c8-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="2f3c8-262">Uso de nombre de punto de conexión de hello, tipo de extremo, nombre del perfil y el nombre del grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="2f3c8-263">Toodisable del mismo modo, un punto de conexión de administrador de tráfico:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="2f3c8-264">Al igual que con `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet pide confirmación.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="2f3c8-265">Este mensaje se puede suprimir con hello '-Force' parámetro.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="2f3c8-266">Eliminación de un punto de conexión de Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="2f3c8-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="2f3c8-267">tooremove extremos individuales, utilice hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="2f3c8-268">Este cmdlet solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="2f3c8-269">Este mensaje se puede suprimir con hello '-Force' parámetro.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="2f3c8-270">Eliminación de un perfil del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="2f3c8-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="2f3c8-271">toodelete un perfil de Traffic Manager, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, especificar los nombres de grupo de recursos y perfil de hello:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="2f3c8-272">Este cmdlet solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="2f3c8-273">Este mensaje se puede suprimir con hello '-Force' parámetro.</span><span class="sxs-lookup"><span data-stu-id="2f3c8-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="2f3c8-274">Hola perfil toobe elimina también puede especificarse mediante un objeto de perfil:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="2f3c8-275">Se puede canalizar igualmente esta secuencia:</span><span class="sxs-lookup"><span data-stu-id="2f3c8-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="2f3c8-276">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f3c8-276">Next steps</span></span>

[<span data-ttu-id="2f3c8-277">Supervisión del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="2f3c8-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="2f3c8-278">Consideraciones de rendimiento sobre el Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="2f3c8-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
