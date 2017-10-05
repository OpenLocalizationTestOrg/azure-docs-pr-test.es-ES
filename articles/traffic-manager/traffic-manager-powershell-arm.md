---
title: Uso de PowerShell para administrar Traffic Manager en Azure | Microsoft Docs
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
ms.openlocfilehash: 1cd7bd7e32c96398d72c7cd3b51e2b456d60f01d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="using-powershell-to-manage-traffic-manager"></a><span data-ttu-id="dc994-103">Uso de PowerShell para administrar Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="dc994-103">Using PowerShell to manage Traffic Manager</span></span>

<span data-ttu-id="dc994-104">Azure Resource Manager es la interfaz de administración de servicios preferida en Azure.</span><span class="sxs-lookup"><span data-stu-id="dc994-104">Azure Resource Manager is the preferred management interface for services in Azure.</span></span> <span data-ttu-id="dc994-105">Los perfiles de Traffic Manager se pueden administrar mediante las herramientas y las API basadas en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dc994-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="dc994-106">Modelo de recursos</span><span class="sxs-lookup"><span data-stu-id="dc994-106">Resource model</span></span>

<span data-ttu-id="dc994-107">El Administrador de tráfico de Azure se configura con una colección de valores denominada perfil del Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="dc994-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="dc994-108">Este perfil contiene la configuración de DNS, la de enrutamiento del tráfico, la de supervisión de puntos de conexión y una lista de los puntos de conexión de servicio a los que se enruta el tráfico.</span><span class="sxs-lookup"><span data-stu-id="dc994-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints to which traffic is routed.</span></span>

<span data-ttu-id="dc994-109">Cada perfil de Traffic Manager se representa mediante un recurso de tipo "TrafficManagerProfiles".</span><span class="sxs-lookup"><span data-stu-id="dc994-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="dc994-110">En el nivel de la API de REST, el URI de cada perfil es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc994-110">At the REST API level, the URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="dc994-111">Configuración de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc994-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="dc994-112">En estas instrucciones se usa PowerShell para Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dc994-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="dc994-113">En el siguiente artículo se explica cómo instalar y configurar Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc994-113">The following article explains how to install and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="dc994-114">Cómo instalar y configurar Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc994-114">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="dc994-115">En los ejemplos de este artículo se da por supuesto que ya tiene un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dc994-115">The examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="dc994-116">Puede crear uno mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="dc994-116">You can create a resource group using the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="dc994-117">Azure Resource Manager requiere que todos los grupos de recursos cuenten con una ubicación.</span><span class="sxs-lookup"><span data-stu-id="dc994-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="dc994-118">Esta se utiliza como predeterminada para los recursos que se crean en ese grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dc994-118">This location is used as the default for resources created in that resource group.</span></span> <span data-ttu-id="dc994-119">Sin embargo, puesto que los recursos del perfil de Traffic Manager son globales y no regionales, la elección de la ubicación del grupo de recursos no afecta a Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="dc994-119">However, since Traffic Manager profile resources are global, not regional, the choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="dc994-120">Creación de un perfil del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="dc994-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="dc994-121">Para crear un perfil de Traffic Manager, use el cmdlet `New-AzureRmTrafficManagerProfile`:</span><span class="sxs-lookup"><span data-stu-id="dc994-121">To create a Traffic Manager profile, use the `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="dc994-122">En la siguiente tabla se describen los parámetros:</span><span class="sxs-lookup"><span data-stu-id="dc994-122">The following table describes the parameters:</span></span>

| <span data-ttu-id="dc994-123">Parámetro</span><span class="sxs-lookup"><span data-stu-id="dc994-123">Parameter</span></span> | <span data-ttu-id="dc994-124">Descripción</span><span class="sxs-lookup"><span data-stu-id="dc994-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dc994-125">Nombre</span><span class="sxs-lookup"><span data-stu-id="dc994-125">Name</span></span> |<span data-ttu-id="dc994-126">Nombre del recurso del perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="dc994-126">The resource name for the Traffic Manager profile resource.</span></span> <span data-ttu-id="dc994-127">Los perfiles del mismo grupo de recursos deben tener nombres únicos.</span><span class="sxs-lookup"><span data-stu-id="dc994-127">Profiles in the same resource group must have unique names.</span></span> <span data-ttu-id="dc994-128">Este nombre es independiente del nombre DNS que se utiliza para las consultas de DNS.</span><span class="sxs-lookup"><span data-stu-id="dc994-128">This name is separate from the DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="dc994-129">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="dc994-129">ResourceGroupName</span></span> |<span data-ttu-id="dc994-130">Nombre del grupo de recursos que contiene el recurso de perfil.</span><span class="sxs-lookup"><span data-stu-id="dc994-130">The name of the resource group containing the profile resource.</span></span> |
| <span data-ttu-id="dc994-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="dc994-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="dc994-132">Especifica el método de enrutamiento del tráfico que se usa para determinar qué punto de conexión se devuelve en respuesta a una consulta de DNS.</span><span class="sxs-lookup"><span data-stu-id="dc994-132">Specifies the traffic-routing method used to determine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="dc994-133">Los valores posibles son "Performance", "Weighted" o "Priority".</span><span class="sxs-lookup"><span data-stu-id="dc994-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="dc994-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="dc994-134">RelativeDnsName</span></span> |<span data-ttu-id="dc994-135">Especifica la parte correspondiente al nombre de host del nombre DNS proporcionado por este perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="dc994-135">Specifies the hostname portion of the DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="dc994-136">Este valor se combina con el nombre de dominio DNS usado por Azure Traffic Manager para formar el nombre de dominio completo (FQDN) del perfil.</span><span class="sxs-lookup"><span data-stu-id="dc994-136">This value is combined with the DNS domain name used by Azure Traffic Manager to form the fully qualified domain name (FQDN) of the profile.</span></span> <span data-ttu-id="dc994-137">Por ejemplo, con el valor "contoso", se obtiene "contoso.trafficmanager.net".</span><span class="sxs-lookup"><span data-stu-id="dc994-137">For example, setting the value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="dc994-138">TTL</span><span class="sxs-lookup"><span data-stu-id="dc994-138">TTL</span></span> |<span data-ttu-id="dc994-139">Especifica el período de vida (TTL) de DNS, en segundos.</span><span class="sxs-lookup"><span data-stu-id="dc994-139">Specifies the DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="dc994-140">Este TTL informa a las resoluciones DNS locales y a los clientes DNS de cuánto tiempo se guardan en memoria caché las respuestas DNS proporcionadas por este perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="dc994-140">This TTL informs the Local DNS resolvers and DNS clients how long to cache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="dc994-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="dc994-141">MonitorProtocol</span></span> |<span data-ttu-id="dc994-142">Especifica el protocolo que se va a usar para supervisar el estado de los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="dc994-142">Specifies the protocol to use to monitor endpoint health.</span></span> <span data-ttu-id="dc994-143">Los valores posibles son "HTTP" y "HTTPS".</span><span class="sxs-lookup"><span data-stu-id="dc994-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="dc994-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="dc994-144">MonitorPort</span></span> |<span data-ttu-id="dc994-145">Especifica el puerto TCP usado para supervisar el estado de los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="dc994-145">Specifies the TCP port used to monitor endpoint health.</span></span> |
| <span data-ttu-id="dc994-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="dc994-146">MonitorPath</span></span> |<span data-ttu-id="dc994-147">Especifica la ruta de acceso relativa al nombre de dominio de punto de conexión usado para sondear el estado del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="dc994-147">Specifies the path relative to the endpoint domain name used to probe for endpoint health.</span></span> |

<span data-ttu-id="dc994-148">El cmdlet crea un perfil de Traffic Manager en Azure y devuelve un objeto de perfil correspondiente a PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc994-148">The cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object to PowerShell.</span></span> <span data-ttu-id="dc994-149">El perfil aún no contiene puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="dc994-149">At this point, the profile does not contain any endpoints.</span></span> <span data-ttu-id="dc994-150">Para más información sobre cómo agregar puntos de conexión a un perfil de Traffic Manager, consulte [Incorporación de puntos de conexión de Traffic Manager](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="dc994-150">For more information about adding endpoints to a Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="dc994-151">Obtención de un perfil del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="dc994-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="dc994-152">Para recuperar un objeto del perfil de Traffic Manager existente, use el cmdlet `Get-AzureRmTrafficManagerProfle`:</span><span class="sxs-lookup"><span data-stu-id="dc994-152">To retrieve an existing Traffic Manager profile object, use the `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="dc994-153">Este cmdlet devuelve un objeto del perfil del Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="dc994-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="dc994-154">Actualización de un perfil de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="dc994-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="dc994-155">Para modificar perfiles de Traffic Manager, se sigue un proceso de tres pasos:</span><span class="sxs-lookup"><span data-stu-id="dc994-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="dc994-156">Recupere el perfil mediante `Get-AzureRmTrafficManagerProfile` o use el devuelto por `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="dc994-156">Retrieve the profile using `Get-AzureRmTrafficManagerProfile` or use the profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="dc994-157">Modifique el perfil.</span><span class="sxs-lookup"><span data-stu-id="dc994-157">Modify the profile.</span></span> <span data-ttu-id="dc994-158">Puede agregar y quitar puntos de conexión o cambiar los parámetros del perfil o el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="dc994-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="dc994-159">Estos cambios son operaciones fuera de línea.</span><span class="sxs-lookup"><span data-stu-id="dc994-159">These changes are off-line operations.</span></span> <span data-ttu-id="dc994-160">Solo cambia el objeto el objeto local en memoria que representa el perfil.</span><span class="sxs-lookup"><span data-stu-id="dc994-160">You are only changing the local object in memory that represents the profile.</span></span>
3. <span data-ttu-id="dc994-161">Confirme los cambios mediante el cmdlet `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="dc994-161">Commit your changes using the `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="dc994-162">Se pueden cambiar todas las propiedades del perfil, excepto RelativeDnsName para el perfil.</span><span class="sxs-lookup"><span data-stu-id="dc994-162">All profile properties can be changed except the profile's RelativeDnsName.</span></span> <span data-ttu-id="dc994-163">Para cambiar RelativeDnsName, debe eliminar el perfil y crear uno con un nombre diferente.</span><span class="sxs-lookup"><span data-stu-id="dc994-163">To change the RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="dc994-164">En el ejemplo siguiente se muestra cómo cambiar el TTL del perfil:</span><span class="sxs-lookup"><span data-stu-id="dc994-164">The following example demonstrates how to change the profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="dc994-165">Existen tres tipos de puntos de conexión de Administrador de tráfico:</span><span class="sxs-lookup"><span data-stu-id="dc994-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="dc994-166">Los **puntos de conexión de Azure** son servicios hospedados en Azure.</span><span class="sxs-lookup"><span data-stu-id="dc994-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="dc994-167">Los **puntos de conexión externos** son servicios hospedados fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc994-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="dc994-168">Los **puntos de conexión anidados** se usan para construir jerarquías anidadas de perfiles de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="dc994-168">**Nested endpoints** are used to construct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="dc994-169">Los puntos de conexión anidados hacen posibles configuraciones avanzadas de enrutamiento del tráfico para aplicaciones complejas.</span><span class="sxs-lookup"><span data-stu-id="dc994-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="dc994-170">En los tres casos, se pueden agregar puntos de conexión de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="dc994-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="dc994-171">Mediante el proceso de tres pasos descrito antes.</span><span class="sxs-lookup"><span data-stu-id="dc994-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="dc994-172">La ventaja de este método es que se pueden realizar varios cambios en el punto de conexión en una sola actualización.</span><span class="sxs-lookup"><span data-stu-id="dc994-172">The advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="dc994-173">Con el cmdlet New-AzureRmTrafficManagerEndpoint.</span><span class="sxs-lookup"><span data-stu-id="dc994-173">Using the New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="dc994-174">Este cmdlet agrega un punto de conexión a un perfil de Traffic Manager existente en una sola operación.</span><span class="sxs-lookup"><span data-stu-id="dc994-174">This cmdlet adds an endpoint to an existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="dc994-175">Adición de puntos de conexión de Azure</span><span class="sxs-lookup"><span data-stu-id="dc994-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="dc994-176">Los puntos de conexión de Azure hacen referencia a servicios hospedados en Azure.</span><span class="sxs-lookup"><span data-stu-id="dc994-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="dc994-177">Se admiten dos tipos de puntos de conexión de Azure:</span><span class="sxs-lookup"><span data-stu-id="dc994-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="dc994-178">Aplicaciones web de Azure </span><span class="sxs-lookup"><span data-stu-id="dc994-178">Azure Web Apps</span></span>
2. <span data-ttu-id="dc994-179">Recursos de PublicIpAddress de Azure (que pueden estar asociados a un equilibrador de carga o a una NIC de máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="dc994-179">Azure PublicIpAddress resources (which can be attached to a load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="dc994-180">PublicIpAddress debe tener un nombre DNS asignado para usarse en Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="dc994-180">The PublicIpAddress must have a DNS name assigned to be used in Traffic Manager.</span></span>

<span data-ttu-id="dc994-181">En cada caso:</span><span class="sxs-lookup"><span data-stu-id="dc994-181">In each case:</span></span>

* <span data-ttu-id="dc994-182">El servicio se especifica mediante el parámetro '"targetResourceId" de `Add-AzureRmTrafficManagerEndpointConfig` o `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="dc994-182">The service is specified using the 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="dc994-183">Los parámetros "Target" y "EndpointLocation" están implícitos en TargetResourceId.</span><span class="sxs-lookup"><span data-stu-id="dc994-183">The 'Target' and 'EndpointLocation' are implied by the TargetResourceId.</span></span>
* <span data-ttu-id="dc994-184">Especificar el valor de 'Weight' es opcional.</span><span class="sxs-lookup"><span data-stu-id="dc994-184">Specifying the 'Weight' is optional.</span></span> <span data-ttu-id="dc994-185">La ponderación solo se usa si el perfil está configurado para usar el método de enrutamiento del tráfico "Weighted".</span><span class="sxs-lookup"><span data-stu-id="dc994-185">Weights are only used if the profile is configured to use the 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="dc994-186">En caso contrario, se pasan por alto.</span><span class="sxs-lookup"><span data-stu-id="dc994-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="dc994-187">Si se especifica, el valor debe ser un número entre 1 y 1000.</span><span class="sxs-lookup"><span data-stu-id="dc994-187">If specified, the value must be a number between 1 and 1000.</span></span> <span data-ttu-id="dc994-188">El valor predeterminado es 1.</span><span class="sxs-lookup"><span data-stu-id="dc994-188">The default value is '1'.</span></span>
* <span data-ttu-id="dc994-189">Especificar el valor de 'Priority' es opcional.</span><span class="sxs-lookup"><span data-stu-id="dc994-189">Specifying the 'Priority' is optional.</span></span> <span data-ttu-id="dc994-190">Las prioridades solo se usan si el perfil está configurado para usar el método de enrutamiento del tráfico "Priority".</span><span class="sxs-lookup"><span data-stu-id="dc994-190">Priorities are only used if the profile is configured to use the 'Priority' traffic-routing method.</span></span> <span data-ttu-id="dc994-191">En caso contrario, se pasan por alto.</span><span class="sxs-lookup"><span data-stu-id="dc994-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="dc994-192">Los valores válidos son de 1 a 1000; los valores más bajos indican una prioridad más alta.</span><span class="sxs-lookup"><span data-stu-id="dc994-192">Valid values are from 1 to 1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="dc994-193">Si se especifica para un punto de conexión, se debe especificar para todos los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="dc994-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="dc994-194">Si se omite, se aplican los valores predeterminados a partir de "1" en el orden en que se indican los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="dc994-194">If omitted, default values starting from '1' are applied in the order that the endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="dc994-195">Ejemplo 1: Incorporación de puntos de conexión de aplicación web mediante `Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="dc994-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="dc994-196">En este ejemplo, se crea un perfil de Traffic Manager y se agregan dos puntos de conexión de aplicación web mediante el cmdlet `Add-AzureRmTrafficManagerEndpointConfig`.</span><span class="sxs-lookup"><span data-stu-id="dc994-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using the `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="dc994-197">Ejemplo 2: Incorporación de un punto de conexión de publicIpAddress mediante `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="dc994-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="dc994-198">En este ejemplo, se agrega un recurso de dirección IP pública al perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="dc994-198">In this example, a public IP address resource is added to the Traffic Manager profile.</span></span> <span data-ttu-id="dc994-199">La dirección IP pública debe tener un nombre DNS configurado y puede enlazarse a la NIC de una máquina virtual o a un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="dc994-199">The public IP address must have a DNS name configured, and can be bound either to the NIC of a VM or to a load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="dc994-200">Adición de puntos de conexión externos</span><span class="sxs-lookup"><span data-stu-id="dc994-200">Adding External Endpoints</span></span>

<span data-ttu-id="dc994-201">Administrador de tráfico usa los puntos de conexión externos para dirigir el tráfico a los servicios hospedados fuera de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc994-201">Traffic Manager uses external endpoints to direct traffic to services hosted outside of Azure.</span></span> <span data-ttu-id="dc994-202">Al igual que en el caso de los puntos de conexión de Azure, los puntos de conexión externos se pueden agregar mediante `Add-AzureRmTrafficManagerEndpointConfig` seguido de `Set-AzureRmTrafficManagerProfile` o `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="dc994-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="dc994-203">Cuando se especifican puntos de conexión externos:</span><span class="sxs-lookup"><span data-stu-id="dc994-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="dc994-204">Se debe especificar el nombre de dominio del punto de conexión con el parámetro Target.</span><span class="sxs-lookup"><span data-stu-id="dc994-204">The endpoint domain name must be specified using the 'Target' parameter</span></span>
* <span data-ttu-id="dc994-205">Si se usa el método de enrutamiento del tráfico "Performance", se necesita "EndpointLocation".</span><span class="sxs-lookup"><span data-stu-id="dc994-205">If the 'Performance' traffic-routing method is used, the 'EndpointLocation' is required.</span></span> <span data-ttu-id="dc994-206">De lo contrario, es opcional.</span><span class="sxs-lookup"><span data-stu-id="dc994-206">Otherwise it is optional.</span></span> <span data-ttu-id="dc994-207">El valor debe ser un [nombre de región de Azure válido](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="dc994-207">The value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="dc994-208">Los parámetros "Weight" y "Priority" son opcionales.</span><span class="sxs-lookup"><span data-stu-id="dc994-208">The 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="dc994-209">Ejemplo 1: Incorporación de puntos de conexión externos mediante `Add-AzureRmTrafficManagerEndpointConfig` y `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="dc994-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="dc994-210">En este ejemplo, se crea un perfil de Traffic Manager, se agregan dos puntos de conexión externos y se confirman los cambios.</span><span class="sxs-lookup"><span data-stu-id="dc994-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit the changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="dc994-211">Ejemplo 2: Incorporación de puntos de conexión externos mediante `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="dc994-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="dc994-212">En este ejemplo, se agrega un punto de conexión externo a un perfil existente.</span><span class="sxs-lookup"><span data-stu-id="dc994-212">In this example, we add an external endpoint to an existing profile.</span></span> <span data-ttu-id="dc994-213">El perfil se especifica mediante los nombres del grupo de recursos y del perfil.</span><span class="sxs-lookup"><span data-stu-id="dc994-213">The profile is specified using the profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="dc994-214">Adición de puntos de conexión "Anidados"</span><span class="sxs-lookup"><span data-stu-id="dc994-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="dc994-215">Cada perfil del Administrador de tráfico especifica un único método de enrutamiento del tráfico.</span><span class="sxs-lookup"><span data-stu-id="dc994-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="dc994-216">No obstante, hay escenarios en que se requiere un enrutamiento del tráfico más sofisticado que el proporcionado mediante un único perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="dc994-216">However, there are scenarios that require more sophisticated traffic routing than the routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="dc994-217">Puede anidar perfiles de Traffic Manager para combinar las ventajas de más de un método de enrutamiento del tráfico.</span><span class="sxs-lookup"><span data-stu-id="dc994-217">You can nest Traffic Manager profiles to combine the benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="dc994-218">Los perfiles anidados permiten invalidar el comportamiento predeterminado de Traffic Manager para admitir implementaciones de aplicaciones más grandes y complejas.</span><span class="sxs-lookup"><span data-stu-id="dc994-218">Nested profiles allow you to override the default Traffic Manager behavior to support larger and more complex application deployments.</span></span> <span data-ttu-id="dc994-219">Para ejemplos más detallados, consulte [Perfiles anidados de Traffic Manager](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="dc994-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="dc994-220">Los puntos de conexión anidados se configuran en el perfil primario, utilizando un tipo de punto de conexión específico: 'NestedEndpoints'.</span><span class="sxs-lookup"><span data-stu-id="dc994-220">Nested endpoints are configured at the parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="dc994-221">Cuando se especifican puntos de conexión anidados:</span><span class="sxs-lookup"><span data-stu-id="dc994-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="dc994-222">El punto de conexión se debe especificar con el parámetro "targetResourceId".</span><span class="sxs-lookup"><span data-stu-id="dc994-222">The endpoint must be specified using the 'targetResourceId' parameter</span></span>
* <span data-ttu-id="dc994-223">Si se usa el método de enrutamiento del tráfico "Performance", se necesita "EndpointLocation".</span><span class="sxs-lookup"><span data-stu-id="dc994-223">If the 'Performance' traffic-routing method is used, the 'EndpointLocation' is required.</span></span> <span data-ttu-id="dc994-224">De lo contrario, es opcional.</span><span class="sxs-lookup"><span data-stu-id="dc994-224">Otherwise it is optional.</span></span> <span data-ttu-id="dc994-225">El valor debe ser un [nombre de región de Azure válido](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="dc994-225">The value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="dc994-226">Los parámetros Weight y Priority son opcionales en cuanto a los puntos de conexión de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc994-226">The 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="dc994-227">El parámetro "MinChildEndpoints" es opcional.</span><span class="sxs-lookup"><span data-stu-id="dc994-227">The 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="dc994-228">El valor predeterminado es 1.</span><span class="sxs-lookup"><span data-stu-id="dc994-228">The default value is '1'.</span></span> <span data-ttu-id="dc994-229">Si el número de puntos de conexión disponibles se encuentra por debajo de este umbral, el perfil primario considera que dicho perfil está "degradado" y desvía el tráfico a los demás puntos de conexión del perfil primario.</span><span class="sxs-lookup"><span data-stu-id="dc994-229">If the number of available endpoints falls below this threshold, the parent profile considers the child profile 'degraded' and diverts traffic to the other endpoints in the parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="dc994-230">Ejemplo 1: Incorporación de puntos de conexión anidados mediante `Add-AzureRmTrafficManagerEndpointConfig` y `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="dc994-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="dc994-231">En este ejemplo, se crean un perfil primario y otro secundario de Traffic Manager, se agrega el secundario como punto de conexión anidado al primario y se confirman los cambios.</span><span class="sxs-lookup"><span data-stu-id="dc994-231">In this example, we create new Traffic Manager child and parent profiles, add the child as a nested endpoint to the parent, and commit the changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="dc994-232">Por brevedad, en este ejemplo, no se han agregado otros puntos de conexión al perfil primario ni al secundario.</span><span class="sxs-lookup"><span data-stu-id="dc994-232">For brevity in this example, we did not add any other endpoints to the child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="dc994-233">Ejemplo 2: Incorporación de puntos de conexión anidados mediante `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="dc994-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="dc994-234">En este ejemplo, agregamos un perfil secundario existente como punto de conexión anidado a un perfil primario existente.</span><span class="sxs-lookup"><span data-stu-id="dc994-234">In this example, we add an existing child profile as a nested endpoint to an existing parent profile.</span></span> <span data-ttu-id="dc994-235">El perfil se especifica mediante los nombres del grupo de recursos y del perfil.</span><span class="sxs-lookup"><span data-stu-id="dc994-235">The profile is specified using the profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="dc994-236">Actualización de un punto de conexión de Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="dc994-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="dc994-237">Hay dos maneras de actualizar un punto de conexión del Administrador de tráfico existente:</span><span class="sxs-lookup"><span data-stu-id="dc994-237">There are two ways to update an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="dc994-238">Obtenga el perfil de Traffic Manager mediante `Get-AzureRmTrafficManagerProfile`, actualice las propiedades de punto de conexión en el perfil y confirme los cambios con `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="dc994-238">Get the Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update the endpoint properties within the profile, and commit the changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="dc994-239">Este método tiene la ventaja de poder actualizar más de un punto de conexión en una sola operación.</span><span class="sxs-lookup"><span data-stu-id="dc994-239">This method has the advantage of being able to update more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="dc994-240">Obtenga el perfil de Traffic Manager mediante `Get-AzureRmTrafficManagerEndpoint`, actualice las propiedades de punto de conexión y confirme los cambios con `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="dc994-240">Get the Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update the endpoint properties, and commit the changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="dc994-241">Este método es más sencillo, ya que no requiere la indexación de la matriz de puntos de conexión en el perfil.</span><span class="sxs-lookup"><span data-stu-id="dc994-241">This method is simpler, since it does not require indexing into the Endpoints array in the profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="dc994-242">Ejemplo 1: Actualización de puntos de conexión mediante `Get-AzureRmTrafficManagerProfile` y `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="dc994-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="dc994-243">En este ejemplo, se va a modificar la prioridad de dos puntos de conexión en un perfil existente.</span><span class="sxs-lookup"><span data-stu-id="dc994-243">In this example, we modify the priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="dc994-244">Ejemplo 2: Actualización de un punto de conexión mediante `Get-AzureRmTrafficManagerEndpoint` y `Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="dc994-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="dc994-245">En este ejemplo, se modifica la ponderación de un solo punto de conexión en un perfil existente.</span><span class="sxs-lookup"><span data-stu-id="dc994-245">In this example, we modify the weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="dc994-246">Habilitación y deshabilitación de puntos de conexión y perfiles</span><span class="sxs-lookup"><span data-stu-id="dc994-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="dc994-247">Administrador de tráfico permite que se habiliten y deshabiliten puntos de conexión individuales, además de permitir la habilitación y deshabilitación de perfiles completos.</span><span class="sxs-lookup"><span data-stu-id="dc994-247">Traffic Manager allows individual endpoints to be enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="dc994-248">Estos cambios pueden realizarse mediante la obtención, actualización o configuración los recursos del perfil o del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="dc994-248">These changes can be made by getting/updating/setting the endpoint or profile resources.</span></span> <span data-ttu-id="dc994-249">Para facilitar estas operaciones comunes, también se admiten a través de cmdlets dedicados.</span><span class="sxs-lookup"><span data-stu-id="dc994-249">To streamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="dc994-250">Ejemplo 1: Habilitación y deshabilitación de un perfil de Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="dc994-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="dc994-251">Para habilitar un perfil de Traffic Manager, use `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="dc994-251">To enable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="dc994-252">El perfil se puede especificar mediante un objeto de perfil.</span><span class="sxs-lookup"><span data-stu-id="dc994-252">The profile can be specified using a profile object.</span></span> <span data-ttu-id="dc994-253">El objeto de perfil se puede pasar a través de la canalización o mediante el parámetro "-TrafficManagerProfile".</span><span class="sxs-lookup"><span data-stu-id="dc994-253">The profile object can be passed via the pipeline or by using the '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="dc994-254">En este ejemplo, se especifica el perfil mediante el nombre del grupo de recursos y del perfil.</span><span class="sxs-lookup"><span data-stu-id="dc994-254">In this example, we specify the profile by the profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="dc994-255">Para deshabilitar un perfil de Traffic Manager:</span><span class="sxs-lookup"><span data-stu-id="dc994-255">To disable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="dc994-256">El cmdlet Disable-AzureRmTrafficManagerProfile solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="dc994-256">The Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="dc994-257">Se puede suprimir este mensaje con el parámetro "-Force".</span><span class="sxs-lookup"><span data-stu-id="dc994-257">This prompt can be suppressed using the '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="dc994-258">Ejemplo 2: Habilitación y deshabilitación de un punto de conexión de Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="dc994-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="dc994-259">Para habilitar un punto de conexión de Traffic Manager, use `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="dc994-259">To enable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="dc994-260">Hay dos maneras de especificar el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="dc994-260">There are two ways to specify the endpoint</span></span>

1. <span data-ttu-id="dc994-261">Mediante un objeto TrafficManagerEndpoint pasado a través de la canalización o con el parámetro "-TrafficManagerEndpoint"</span><span class="sxs-lookup"><span data-stu-id="dc994-261">Using a TrafficManagerEndpoint object passed via the pipeline or using the '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="dc994-262">Mediante el nombre del punto de conexión, el tipo de punto de conexión, el nombre del perfil y el nombre del grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="dc994-262">Using the endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="dc994-263">De forma similar, para deshabilitar un punto de conexión de Administrador de tráfico:</span><span class="sxs-lookup"><span data-stu-id="dc994-263">Similarly, to disable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="dc994-264">Al igual que con `Disable-AzureRmTrafficManagerProfile`, el cmdlet `Disable-AzureRmTrafficManagerEndpoint` solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="dc994-264">As with `Disable-AzureRmTrafficManagerProfile`, the `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="dc994-265">Se puede suprimir este mensaje con el parámetro "-Force".</span><span class="sxs-lookup"><span data-stu-id="dc994-265">This prompt can be suppressed using the '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="dc994-266">Eliminación de un punto de conexión de Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="dc994-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="dc994-267">Para quitar puntos de conexión individuales, use el cmdlet `Remove-AzureRmTrafficManagerEndpoint`:</span><span class="sxs-lookup"><span data-stu-id="dc994-267">To remove individual endpoints, use the `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="dc994-268">Este cmdlet solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="dc994-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="dc994-269">Se puede suprimir este mensaje con el parámetro "-Force".</span><span class="sxs-lookup"><span data-stu-id="dc994-269">This prompt can be suppressed using the '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="dc994-270">Eliminación de un perfil del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="dc994-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="dc994-271">Para eliminar un perfil de Traffic Manager, use el cmdlet `Remove-AzureRmTrafficManagerProfile`, especificando el nombre del perfil y el del grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="dc994-271">To delete a Traffic Manager profile, use the `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying the profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="dc994-272">Este cmdlet solicita confirmación.</span><span class="sxs-lookup"><span data-stu-id="dc994-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="dc994-273">Se puede suprimir este mensaje con el parámetro "-Force".</span><span class="sxs-lookup"><span data-stu-id="dc994-273">This prompt can be suppressed using the '-Force' parameter.</span></span>

<span data-ttu-id="dc994-274">El perfil que se va a eliminar también se puede especificar con un objeto de perfil:</span><span class="sxs-lookup"><span data-stu-id="dc994-274">The profile to be deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="dc994-275">Se puede canalizar igualmente esta secuencia:</span><span class="sxs-lookup"><span data-stu-id="dc994-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="dc994-276">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc994-276">Next steps</span></span>

[<span data-ttu-id="dc994-277">Supervisión del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="dc994-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="dc994-278">Consideraciones de rendimiento sobre el Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="dc994-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
