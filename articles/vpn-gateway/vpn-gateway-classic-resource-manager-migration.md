---
title: "aaaVPN clásico de puerta de enlace tooResource migración Manager | Documentos de Microsoft"
description: "Esta página proporciona una visión general de hello clásico de puerta de enlace de VPN tooResource migración del administrador."
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a><span data-ttu-id="63003-103">Puerta de enlace VPN clásico tooResource migración del administrador</span><span class="sxs-lookup"><span data-stu-id="63003-103">VPN Gateway classic tooResource Manager migration</span></span>
<span data-ttu-id="63003-104">Las puertas de enlace de VPN ahora se pueden migrar desde el modelo de implementación del Administrador de tooResource clásico.</span><span class="sxs-lookup"><span data-stu-id="63003-104">VPN Gateways can now be migrated from classic tooResource Manager deployment model.</span></span> <span data-ttu-id="63003-105">Puede leer más información sobre las [características y ventajas](../azure-resource-manager/resource-group-overview.md) de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="63003-105">You can read more about Azure Resource Manager [features and benefits](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="63003-106">En este artículo se detalla cómo toomigrate desde implementaciones clásico toonewer el Administrador de recursos según el modelo.</span><span class="sxs-lookup"><span data-stu-id="63003-106">In this article, we  detail how toomigrate from classic deployments toonewer Resource Manager based model.</span></span> 

<span data-ttu-id="63003-107">Las puertas de enlace de VPN se migran como parte de la migración de red virtual de tooResource clásico Manager.</span><span class="sxs-lookup"><span data-stu-id="63003-107">VPN Gateways are migrated as part of VNet migration from classic tooResource Manager.</span></span> <span data-ttu-id="63003-108">Esta migración se realiza con una red virtual cada vez.</span><span class="sxs-lookup"><span data-stu-id="63003-108">This migration is done one VNet at a time.</span></span> <span data-ttu-id="63003-109">No hay ningún requisito adicional en cuanto a toomigration herramientas o requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="63003-109">There is no additional requirement in terms of tools or prerequisites toomigration.</span></span> <span data-ttu-id="63003-110">Pasos de migración son la migración de red virtual tooexisting idénticos y se documentan en [página de migración de recursos de IaaS](../virtual-machines/windows/migration-classic-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="63003-110">Migration steps are identical tooexisting VNet migration and are documented at [IaaS resources migration page](../virtual-machines/windows/migration-classic-resource-manager-ps.md).</span></span> <span data-ttu-id="63003-111">No hay ningún tiempo de inactividad de ruta de acceso de datos durante la migración y, por tanto, las cargas de trabajo existentes seguirán toofunction sin pérdida de conectividad local durante la migración.</span><span class="sxs-lookup"><span data-stu-id="63003-111">There is no data path downtime during migration and thus existing workloads would continue toofunction without loss of on-premises connectivity during migration.</span></span> <span data-ttu-id="63003-112">dirección IP pública Hola asociado a la puerta de enlace VPN de hello no cambia durante el proceso de migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="63003-112">hello public IP address associated with hello VPN gateway does not change during hello migration process.</span></span> <span data-ttu-id="63003-113">Esto implica que no necesitará tooreconfigure el enrutador local una vez completada la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="63003-113">This implies that you will not need tooreconfigure your on-premises router once hello migration is completed.</span></span>  

<span data-ttu-id="63003-114">modelo de Hello en el Administrador de recursos es diferente del modelo clásico y se compone de las puertas de enlace de red virtual, las puertas de enlace de red local y los recursos de conexión.</span><span class="sxs-lookup"><span data-stu-id="63003-114">hello model in Resource Manager is different from classic model and is composed of virtual network gateways, local network gateways and connection resources.</span></span> <span data-ttu-id="63003-115">Estos representan la puerta de enlace VPN de hello propio, Hola sitio local que representa en el espacio de direcciones local y la conectividad entre Hola dos respectivamente.</span><span class="sxs-lookup"><span data-stu-id="63003-115">These represent hello VPN gateway itself, hello local-site representing on premises address space and connectivity between hello two respectively.</span></span> <span data-ttu-id="63003-116">Una vez completada la migración, las puertas de enlace no estarán disponibles en el modelo clásico y todas las operaciones de administración en puertas de enlace de red virtual, puertas de enlace de red local y objetos de conexión se deben llevar a cabo mediante el modelo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="63003-116">Once migration is completed your gateways would not be available in classic model and all management operations on virtual network gateways, local network gateways, and connection objects must be performed using Resource Manager model.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="63003-117">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="63003-117">Supported scenarios</span></span>
<span data-ttu-id="63003-118">Escenarios más comunes de conectividad VPN están cubiertos por tooResource clásico migración del administrador.</span><span class="sxs-lookup"><span data-stu-id="63003-118">Most common VPN connectivity scenarios are covered by classic tooResource Manager migration.</span></span> <span data-ttu-id="63003-119">escenarios de Hello compatibles incluyen:</span><span class="sxs-lookup"><span data-stu-id="63003-119">hello supported scenarios include -</span></span>

* <span data-ttu-id="63003-120">Conectividad de punto toosite</span><span class="sxs-lookup"><span data-stu-id="63003-120">Point toosite connectivity</span></span>
* <span data-ttu-id="63003-121">Conectividad de sitio toosite con puerta de enlace VPN conectado ubicación local de tooon</span><span class="sxs-lookup"><span data-stu-id="63003-121">Site toosite connectivity with VPN Gateway connected tooon premises location</span></span>
* <span data-ttu-id="63003-122">Conectividad de red virtual tooVNet entre dos redes virtuales con puertas de enlace VPN</span><span class="sxs-lookup"><span data-stu-id="63003-122">VNet tooVNet connectivity between two VNets using VPN gateways</span></span>
* <span data-ttu-id="63003-123">Varias redes virtuales conectadas toosame en la ubicación local</span><span class="sxs-lookup"><span data-stu-id="63003-123">Multiple VNets connected toosame on premises location</span></span>
* <span data-ttu-id="63003-124">Conectividad multisitio</span><span class="sxs-lookup"><span data-stu-id="63003-124">Multi-site connectivity</span></span>
* <span data-ttu-id="63003-125">Redes virtuales con la tunelización forzada habilitada</span><span class="sxs-lookup"><span data-stu-id="63003-125">Forced tunneling enabled VNets</span></span>

<span data-ttu-id="63003-126">Entre los escenarios no admitidos, se incluyen:</span><span class="sxs-lookup"><span data-stu-id="63003-126">Scenarios which are not supported include -</span></span>  

* <span data-ttu-id="63003-127">No se admite actualmente la red virtual con la puerta de enlace de ExpressRoute y puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="63003-127">VNet with both ExpressRoute Gateway and VPN Gateway is not currently supported.</span></span>
* <span data-ttu-id="63003-128">Tránsito escenarios donde las extensiones de VM son servidores locales tooon conectado.</span><span class="sxs-lookup"><span data-stu-id="63003-128">Transit scenarios where VM extensions are connected tooon-premises servers.</span></span> <span data-ttu-id="63003-129">A continuación, se detallan las limitaciones de conectividad VPN de tránsito.</span><span class="sxs-lookup"><span data-stu-id="63003-129">Transit VPN connectivity limitations are detailed below.</span></span>

> [!NOTE]
> <span data-ttu-id="63003-130">Validación de CIDR en el modelo de administrador de recursos es más estricta que Hola uno en el modelo clásico.</span><span class="sxs-lookup"><span data-stu-id="63003-130">CIDR validation in Resource Manager model is more strict than hello one in classic model.</span></span> <span data-ttu-id="63003-131">Antes de migrar Asegúrese de que los intervalos de direcciones clásico dado ajustan formato CIDR de toovalid antes de comenzar la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="63003-131">Before migrating ensure that classic address ranges given conform toovalid CIDR format before beginning hello migration.</span></span> <span data-ttu-id="63003-132">Se puede validar CIDR mediante alguno de los validadores de CIDR habituales.</span><span class="sxs-lookup"><span data-stu-id="63003-132">CIDR can be validated using any common CIDR validators.</span></span> <span data-ttu-id="63003-133">Si se migran sitios locales o redes virtuales con intervalos de CIDR no válidos, se producirá un estado de error.</span><span class="sxs-lookup"><span data-stu-id="63003-133">VNet or local sites with invalid CIDR ranges when migrated would result in failed state.</span></span>
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a><span data-ttu-id="63003-134">Migración de conectividad de red virtual tooVNet</span><span class="sxs-lookup"><span data-stu-id="63003-134">VNet tooVNet connectivity migration</span></span>
<span data-ttu-id="63003-135">Conectividad de red virtual tooVNet en clásico se logra mediante la creación de un sitio local de representación de hello conectados red virtual.</span><span class="sxs-lookup"><span data-stu-id="63003-135">VNet tooVNet connectivity in classic was achieved by creating a local site representation of hello connected VNet.</span></span> <span data-ttu-id="63003-136">Clientes estaban toocreate requiere dos sitios locales que representan Hola dos redes virtuales que necesita toobe conectadas entre sí.</span><span class="sxs-lookup"><span data-stu-id="63003-136">Customers were required toocreate two local sites which represented hello two VNets which needed toobe connected together.</span></span> <span data-ttu-id="63003-137">Se trataba, a continuación, toohello conectado correspondiente redes virtuales con conectividad de tooestablish de túnel de IPsec entre dos redes virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="63003-137">These were then connected toohello corresponding VNets using IPsec tunnel tooestablish connectivity between hello two VNets.</span></span> <span data-ttu-id="63003-138">Este modelo tiene desafíos de facilidad de uso, puesto que los cambios de intervalo de direcciones en una red virtual también deben mantenerse en representación de sitio local de Hola.</span><span class="sxs-lookup"><span data-stu-id="63003-138">This model has manageability challenges since any address range changes in one VNet must also be maintained in hello corresponding local site representation.</span></span> <span data-ttu-id="63003-139">En el modelo de Resource Manager, esta solución ya no es necesaria.</span><span class="sxs-lookup"><span data-stu-id="63003-139">In Resource Manager model this workaround is no longer needed.</span></span> <span data-ttu-id="63003-140">Hola conexión entre dos redes virtuales pueden lograrse directamente mediante el tipo de conexión de 'Vnet2Vnet' en el recurso de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="63003-140">hello connection between hello two VNets can be directly achieved using 'Vnet2Vnet' connection type in Connection resource.</span></span> 

![Migración de tooVNet de captura de pantalla de red virtual.](./media/vpn-gateway-migration/migration1.png)

<span data-ttu-id="63003-142">Durante la migración de red virtual detectamos que Hola entidad conectada puerta de enlace VPN de la red virtual toocurrent es otra VNet y asegúrese de que una vez completada la migración de ambas redes virtuales, ya no verá dos sitios locales que representa Hola otra VNet.</span><span class="sxs-lookup"><span data-stu-id="63003-142">During VNet migration we detect that hello connected entity toocurrent VNet's VPN gateway is another VNet and ensure that once migration of both VNets is completed, you would no longer see two local sites representing hello other VNet.</span></span> <span data-ttu-id="63003-143">modelo clásico de Hola de dos puertas de enlace VPN, dos sitios locales y dos conexiones entre ellos es transformado tooResource modelo de administrador con dos puertas de enlace VPN y dos conexiones de tipo Vnet2Vnet.</span><span class="sxs-lookup"><span data-stu-id="63003-143">hello classic model of two VPN gateways, two local sites and two connections between them is transformed tooResource Manager model with two VPN gateways and two connections of type Vnet2Vnet.</span></span>

## <a name="transit-vpn-connectivity"></a><span data-ttu-id="63003-144">Conectividad de VPN de tránsito</span><span class="sxs-lookup"><span data-stu-id="63003-144">Transit VPN connectivity</span></span>
<span data-ttu-id="63003-145">Puede configurar puertas de enlace VPN en una topología de forma que la conectividad local para una red virtual se logra mediante la conexión de red virtual que está directamente conectado tooon local tooanother.</span><span class="sxs-lookup"><span data-stu-id="63003-145">You can configure VPN gateways in a topology such that on-premises connectivity for a VNet is achieved by connecting tooanother VNet that is directly connected tooon-premises.</span></span> <span data-ttu-id="63003-146">Esto es tránsito conectividad VPN donde instancias en la primera red virtual son recursos locales tooon conectado a través de puerta de enlace VPN de tránsito toohello en la red virtual conectado que está directamente conectado tooon local.</span><span class="sxs-lookup"><span data-stu-id="63003-146">This is transit VPN connectivity where instances in first VNet are connected tooon-premises resources via transit toohello VPN gateway in connected VNet that is directly connected tooon-premises.</span></span> <span data-ttu-id="63003-147">tooachieve esta configuración en el modelo de implementación clásica, necesitaría toocreate un sitio local que se agrega los prefijos que representa tanto espacio de direcciones de red virtual y local de hello conectado.</span><span class="sxs-lookup"><span data-stu-id="63003-147">tooachieve this configuration in classic deployment model, you would need toocreate a local site which has aggregated prefixes representing both hello connected VNet and on-premises address space.</span></span> <span data-ttu-id="63003-148">Este sitio local representational es, a continuación, conectividad de tránsito conectado toohello tooachieve de red virtual.</span><span class="sxs-lookup"><span data-stu-id="63003-148">This representational local site is then connected toohello VNet tooachieve transit connectivity.</span></span> <span data-ttu-id="63003-149">Este modelo clásico también tiene desafíos de facilidad de uso similares, puesto que cualquier cambio en el intervalo de direcciones local también debe conservarse en el sitio local de Hola que representa el agregado de Hola de red virtual y local.</span><span class="sxs-lookup"><span data-stu-id="63003-149">This classic model also has similar manageability challenges since any change in on-premises address range must also be maintained on hello local site representing hello aggregate of VNet and on-premises.</span></span> <span data-ttu-id="63003-150">Introducido la compatibilidad con BGP en puertas de enlace de administrador de recursos admite simplifica la administración, ya que hello las puertas de enlace conectados pueden obtener rutas desde local sin modificación manual tooprefixes.</span><span class="sxs-lookup"><span data-stu-id="63003-150">Introduction of BGP support in Resource Manager supported gateways simplifies manageability since hello connected gateways can learn routes from on premises without manual modification tooprefixes.</span></span>

![Captura de pantalla de escenario de enrutamiento de tránsito.](./media/vpn-gateway-migration/migration2.png)

<span data-ttu-id="63003-152">Puesto que se transforme la conectividad de red virtual tooVNet sin necesidad de sitios locales, escenario de tránsito de hello pierde conectividad local para la red virtual que está conectada indirectamente tooon local.</span><span class="sxs-lookup"><span data-stu-id="63003-152">Since we transform VNet tooVNet connectivity without requiring local sites, hello transit scenario loses on-premises connectivity for VNet that is indirectly connected tooon-premises.</span></span> <span data-ttu-id="63003-153">Hello pérdida de conectividad puede ser mitigada Hola después de dos maneras diferentes: una vez completada la migración:</span><span class="sxs-lookup"><span data-stu-id="63003-153">hello loss of connectivity can be mitigated in hello following two ways, after migration is completed -</span></span> 

* <span data-ttu-id="63003-154">Habilitar BGP en puertas de enlace VPN que están conectadas entre sí y tooon local.</span><span class="sxs-lookup"><span data-stu-id="63003-154">Enable BGP on VPN gateways that are connected together and tooon-premises.</span></span> <span data-ttu-id="63003-155">Al habilitarse BGP, se restaura la conectividad sin realizar ningún otro cambio de configuración, ya que las rutas se aprenden y anuncian entre las puertas de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="63003-155">Enabling BGP restores connectivity without any other configuration change since routes are learned and advertised between VNet gateways.</span></span> <span data-ttu-id="63003-156">Tenga en cuenta que la opción de BGP solo está disponible en las SKU Estándar y superiores.</span><span class="sxs-lookup"><span data-stu-id="63003-156">Note that BGP option is only available on Standard and higher SKUs.</span></span>
* <span data-ttu-id="63003-157">Establecer una conexión explícita de afectados VNet toohello red local puerta de enlace que representa la ubicación local.</span><span class="sxs-lookup"><span data-stu-id="63003-157">Establish an explicit connection from affected VNet toohello local network gateway representing on-premises location.</span></span> <span data-ttu-id="63003-158">También se podría necesita cambiar la configuración en hello local enrutador toocreate y configurarán túnel IPsec de Hola.</span><span class="sxs-lookup"><span data-stu-id="63003-158">This would also require changing configuration on hello on-premises router toocreate and configure hello IPsec tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63003-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="63003-159">Next steps</span></span>
<span data-ttu-id="63003-160">Después de aprender sobre la compatibilidad con la migración de puerta de enlace VPN, vaya demasiado[admitida por la plataforma de migración de los recursos de IaaS de clásico tooResource Manager](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="63003-160">After learning about VPN gateway migration support, go too[platform-supported migration of IaaS resources from classic tooResource Manager](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget started.</span></span>
