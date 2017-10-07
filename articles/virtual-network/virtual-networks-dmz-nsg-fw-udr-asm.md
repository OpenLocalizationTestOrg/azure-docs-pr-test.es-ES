---
title: 'aaaDMZ ejemplo: crear una red Perimetral tooProtect redes con un Firewall, UDR y NSG | Documentos de Microsoft'
description: "Creación de una red perimetral con un firewall, enrutamiento definido por el usuario (UDR) y grupos de seguridad de red (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="569f1-103">Ejemplo 3: crear una red Perimetral tooProtect redes con un Firewall, UDR y NSG</span><span class="sxs-lookup"><span data-stu-id="569f1-103">Example 3 – Build a DMZ tooProtect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="569f1-104">[Devolver toohello página de prácticas recomendadas de seguridad límite][HOME]</span><span class="sxs-lookup"><span data-stu-id="569f1-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="569f1-105">En este ejemplo se creará una red perimetral con un firewall, cuatro servidores Windows, enrutamiento definido por el usuario y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="569f1-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="569f1-106">También guiará a través de cada uno de los tooprovide de comandos pertinentes de hello una comprensión más profunda de cada paso.</span><span class="sxs-lookup"><span data-stu-id="569f1-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="569f1-107">También hay un escenario de tráfico sección tooprovide una detallada paso a paso cómo tráfico pasa a través de las capas de defensa en Hola Hola red Perimetral.</span><span class="sxs-lookup"><span data-stu-id="569f1-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="569f1-108">Por último, en la sección de referencias de hello es código completo de Hola e instrucción toobuild este entorno tootest y experimentar con diferentes escenarios.</span><span class="sxs-lookup"><span data-stu-id="569f1-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="569f1-109">![Red perimetral bidireccional con un dispositivo de red virtual, grupos de seguridad de red y enrutamiento definido por el usuario][1]</span><span class="sxs-lookup"><span data-stu-id="569f1-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="569f1-110">Configuración del entorno</span><span class="sxs-lookup"><span data-stu-id="569f1-110">Environment Setup</span></span>
<span data-ttu-id="569f1-111">En este ejemplo hay una suscripción que contiene Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="569f1-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="569f1-112">Tres servicios en la nube: “SecSvc001”, “FrontEnd001” y “BackEnd001”</span><span class="sxs-lookup"><span data-stu-id="569f1-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="569f1-113">Una red virtual, CorpNetwork, con tres subredes: SecNet, FrontEnd y BackEnd</span><span class="sxs-lookup"><span data-stu-id="569f1-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="569f1-114">Un dispositivo de red virtual, en este ejemplo, un firewall, conectado toohello SecNet subred</span><span class="sxs-lookup"><span data-stu-id="569f1-114">A network virtual appliance, in this example a firewall, connected toohello SecNet subnet</span></span>
* <span data-ttu-id="569f1-115">Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="569f1-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="569f1-116">Dos servidores Windows que representan servidores back-end de aplicaciones (“AppVM01”, “AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="569f1-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="569f1-117">Un servidor Windows que representa un servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="569f1-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="569f1-118">En la sección de referencias de Hola a continuación hay un script de PowerShell que se compilará la mayor parte del entorno de Hola que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="569f1-118">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="569f1-119">Hola de crear las máquinas virtuales y redes virtuales, aunque se realizan mediante el script de ejemplo de Hola, no se describen en detalle en este documento.</span><span class="sxs-lookup"><span data-stu-id="569f1-119">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="569f1-120">entorno de Hola toobuild:</span><span class="sxs-lookup"><span data-stu-id="569f1-120">toobuild hello environment:</span></span>

1. <span data-ttu-id="569f1-121">Guardar archivo de xml de configuración Hola red incluido en la sección de referencias de hello (actualizada con nombres, la ubicación y el escenario de hello dada de toomatch de direcciones IP)</span><span class="sxs-lookup"><span data-stu-id="569f1-121">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="569f1-122">Variables de usuario de actualización hello en hello toomatch Hola entorno Hola de script es toobe ejecutarán (suscripciones, los nombres de servicio, etcetera)</span><span class="sxs-lookup"><span data-stu-id="569f1-122">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="569f1-123">Ejecutar script de Hola en PowerShell</span><span class="sxs-lookup"><span data-stu-id="569f1-123">Execute hello script in PowerShell</span></span>

<span data-ttu-id="569f1-124">**Tenga en cuenta**: región Hola indicado en el script de PowerShell de hello debe coincidir con la región Hola indicado en el archivo de xml de configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-124">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="569f1-125">Una vez que el script de Hola se ejecuta correctamente puede tener Hola siguiendo los pasos posteriores a la secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="569f1-125">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="569f1-126">Configurar reglas de firewall de hello, este tema se trata en la sección de hello siguiente titulada: descripción de la regla de Firewall.</span><span class="sxs-lookup"><span data-stu-id="569f1-126">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="569f1-127">Opcionalmente, en la sección de referencias de hello son dos tooset de secuencias de comandos de hello web y servidor de aplicaciones con una tooallow de aplicación web simple pruebas con esta configuración de red Perimetral.</span><span class="sxs-lookup"><span data-stu-id="569f1-127">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="569f1-128">Una vez que el script de Hola se ejecuta correctamente las reglas de firewall de hello necesitarán toobe completado, este tema se trata en la sección de hello: las reglas de Firewall.</span><span class="sxs-lookup"><span data-stu-id="569f1-128">Once hello script runs successfully hello firewall rules will need toobe completed, this is covered in hello section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="569f1-129">Enrutamiento definido por el usuario (UDR)</span><span class="sxs-lookup"><span data-stu-id="569f1-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="569f1-130">De forma predeterminada, Hola siguiendo las rutas del sistema se define como:</span><span class="sxs-lookup"><span data-stu-id="569f1-130">By default, hello following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="569f1-131">Hola VNETLocal siempre es Hola definido dirección prefix(es) de hello red virtual para dicha red específica (es decir dejará de red virtual tooVNet dependiendo de cómo se defina cada red virtual específica).</span><span class="sxs-lookup"><span data-stu-id="569f1-131">hello VNETLocal is always hello defined address prefix(es) of hello VNet for that specific network (ie it will change from VNet tooVNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="569f1-132">rutas de sistema de Hello restantes son estáticas y predeterminado como anteriormente.</span><span class="sxs-lookup"><span data-stu-id="569f1-132">hello remaining system routes are static and default as above.</span></span>

<span data-ttu-id="569f1-133">Como prioridad, las rutas se procesan a través del método de coincidencia de prefijo más largo (LPM) hello, así hello ruta más específica en la tabla de hello aplicaría tooa partir de dirección de destino.</span><span class="sxs-lookup"><span data-stu-id="569f1-133">As for priority, routes are processed via hello Longest Prefix Match (LPM) method, thus hello most specific route in hello table would apply tooa given destination address.</span></span>

<span data-ttu-id="569f1-134">Por lo tanto, se enrutaría tráfico (por ejemplo toohello DNS01 server, 10.0.2.4) que se usa para la red local de hello (10.0.0.0/16) a través de destino de tooits de red virtual de hello debido toohello 10.0.0.0/16 ruta.</span><span class="sxs-lookup"><span data-stu-id="569f1-134">Therefore, traffic (for example toohello DNS01 server, 10.0.2.4) intended for hello local network (10.0.0.0/16) would be routed across hello VNet tooits destination due toohello 10.0.0.0/16 route.</span></span> <span data-ttu-id="569f1-135">En otras palabras, para 10.0.2.4, ruta de hello 10.0.0.0/16 es ruta más específica de hello, aunque 0.0.0.0/0 y Hola 10.0.0.0/8 también pudieron aplicar, pero ya que son menos específicos no afectan a este tráfico.</span><span class="sxs-lookup"><span data-stu-id="569f1-135">In other words, for 10.0.2.4, hello 10.0.0.0/16 route is hello most specific route, even though hello 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="569f1-136">Por lo tanto Hola tráfico too10.0.2.4 tendría un próximo salto de Hola red virtual local y simplemente enrutar toohello destino.</span><span class="sxs-lookup"><span data-stu-id="569f1-136">Thus hello traffic too10.0.2.4 would have a next hop of hello local VNet and simply route toohello destination.</span></span>

<span data-ttu-id="569f1-137">Si el tráfico se ha diseñado para 10.1.1.1 por ejemplo, no aplica la ruta de hello 10.0.0.0/16, pero Hola 10.0.0.0/8 sería hello más específica, y este tráfico Hola sería quitar ("negro holed"), ya que Hola próximo salto es Null.</span><span class="sxs-lookup"><span data-stu-id="569f1-137">If traffic was intended for 10.1.1.1 for example, hello 10.0.0.0/16 route wouldn’t apply, but hello 10.0.0.0/8 would be hello most specific, and this hello traffic would be dropped (“black holed”) since hello next hop is Null.</span></span> 

<span data-ttu-id="569f1-138">Si destino hello no aplica tooany de prefijos de Null de Hola o prefijos de VNETLocal hello, seguiría Hola menos específica enrutar, 0.0.0.0/0 y enrutarse toohello Internet como próximo salto de hello y, por tanto, out perimetral de internet de Azure.</span><span class="sxs-lookup"><span data-stu-id="569f1-138">If hello destination didn’t apply tooany of hello Null prefixes or hello VNETLocal prefixes, then it would follow hello least specific route, 0.0.0.0/0 and be routed out toohello Internet as hello next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="569f1-139">Si hay dos prefijos idénticos en la tabla de rutas de hello, Hola aquí te mostramos orden Hola de preferencia en función de atributo de "origen" de las rutas de hello:</span><span class="sxs-lookup"><span data-stu-id="569f1-139">If there are two identical prefixes in hello route table, hello following is hello order of preference based on hello routes “source” attribute:</span></span>

1. <span data-ttu-id="569f1-140">"VirtualAppliance" = una tabla de agregados manualmente toohello ruta definida por el usuario</span><span class="sxs-lookup"><span data-stu-id="569f1-140">"VirtualAppliance" = A User Defined Route manually added toohello table</span></span>
2. <span data-ttu-id="569f1-141">"VPNGateway" = una ruta dinámicos BGP (cuando se usa con las redes híbridas), agrega un protocolo de red dinámica, estas rutas pueden cambiar con el tiempo como protocolo de dinámica de hello automáticamente refleja los cambios de red emparejar</span><span class="sxs-lookup"><span data-stu-id="569f1-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as hello dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="569f1-142">"Default" = Hola sistema rutas, Hola entradas estáticas de hello y red virtual locales tal y como se muestra en la tabla de rutas de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="569f1-142">“Default” = hello System Routes, hello local VNet and hello static entries as shown in hello route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="569f1-143">Ahora puede usar enrutamiento definido por usuario (UDR) con ExpressRoute y puertas de enlace VPN tooforce saliente y entrantes entre entornos tráfico toobe tooa enrutado virtual otros dispositivos de red (NVA).</span><span class="sxs-lookup"><span data-stu-id="569f1-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways tooforce outbound and inbound cross-premises traffic toobe routed tooa network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-hello-local-routes"></a><span data-ttu-id="569f1-144">Creación de hello las rutas locales</span><span class="sxs-lookup"><span data-stu-id="569f1-144">Creating hello local routes</span></span>
<span data-ttu-id="569f1-145">En este ejemplo, se necesitan dos tablas de enrutamiento, uno para las subredes de front-end y back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-145">In this example, two routing tables are needed, one each for hello Frontend and Backend subnets.</span></span> <span data-ttu-id="569f1-146">Cada tabla se carga con rutas estáticas adecuadas para hello dada la subred.</span><span class="sxs-lookup"><span data-stu-id="569f1-146">Each table is loaded with static routes appropriate for hello given subnet.</span></span> <span data-ttu-id="569f1-147">A fin de Hola de este ejemplo, cada tabla tiene tres rutas:</span><span class="sxs-lookup"><span data-stu-id="569f1-147">For hello purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="569f1-148">Tráfico de subred local con ningún servidor de seguridad de próximo salto define tooallow subred local tráfico toobypass Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-148">Local subnet traffic with no Next Hop defined tooallow local subnet traffic toobypass hello firewall</span></span>
2. <span data-ttu-id="569f1-149">Tráfico de red virtual con un próximo salto definido como firewall, se invalida la regla predeterminada de Hola que permite tooroute de tráfico de red virtual local directamente</span><span class="sxs-lookup"><span data-stu-id="569f1-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides hello default rule that allows local VNet traffic tooroute directly</span></span>
3. <span data-ttu-id="569f1-150">Tráfico todas las restante (0/0) con un próximo salto se define como Hola firewall</span><span class="sxs-lookup"><span data-stu-id="569f1-150">All remaining traffic (0/0) with a Next Hop defined as hello firewall</span></span>

<span data-ttu-id="569f1-151">Una vez creadas las tablas de enrutamiento de hello son subredes tootheir enlazado.</span><span class="sxs-lookup"><span data-stu-id="569f1-151">Once hello routing tables are created they are bound tootheir subnets.</span></span> <span data-ttu-id="569f1-152">Para la tabla de enrutamiento de hello front-end subred, una vez que crea y enlaza toohello subred debe ser similar a:</span><span class="sxs-lookup"><span data-stu-id="569f1-152">For hello Frontend subnet routing table, once created and bound toohello subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="569f1-153">En este ejemplo, siguiente Hola comandos son toobuild usa una tabla de rutas hello, agregue una ruta definida por el usuario y, a continuación, enlazar la subred de tooa de tabla de ruta de hello (tenga en cuenta; los elementos situados debajo de la que comienza con un signo de dólar (p. ej.: $BESubnet) son variables definidas por el usuario desde un script de Hola en sección de referencia de Hola de este documento):</span><span class="sxs-lookup"><span data-stu-id="569f1-153">For this example, hello following commands are used toobuild hello route table, add a user defined route, and then bind hello route table tooa subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="569f1-154">Se debe crear la primera Hola base tabla de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="569f1-154">First hello base routing table must be created.</span></span> <span data-ttu-id="569f1-155">Este fragmento de código muestra la creación de hello de tabla de hello para la subred de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-155">This snippet shows hello creation of hello table for hello Backend subnet.</span></span> <span data-ttu-id="569f1-156">En el script de Hola, también se crea una tabla correspondiente para la subred de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-156">In hello script, a corresponding table is also created for hello Frontend subnet.</span></span>
   
     <span data-ttu-id="569f1-157">New-AzureRouteTable -Name $BERouteTableName \`</span><span class="sxs-lookup"><span data-stu-id="569f1-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="569f1-158">Una vez que se crea la tabla de rutas de hello, se pueden agregar rutas definidas por el usuario específico.</span><span class="sxs-lookup"><span data-stu-id="569f1-158">Once hello route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="569f1-159">En este fragmento, se enrutará todo el tráfico (0.0.0.0/0) a través del dispositivo virtual de hello (una variable, $VMIP [0] es toopass usado en la dirección IP de hello asignada al dispositivo virtual Hola se creó anteriormente en el script de Hola).</span><span class="sxs-lookup"><span data-stu-id="569f1-159">In this snipped, all traffic (0.0.0.0/0) will be routed through hello virtual appliance (a variable, $VMIP[0], is used toopass in hello IP address assigned when hello virtual appliance was created earlier in hello script).</span></span> <span data-ttu-id="569f1-160">En el script de Hola, también se crea una regla correspondiente en la tabla de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-160">In hello script, a corresponding rule is also created in hello Frontend table.</span></span>
   
     <span data-ttu-id="569f1-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="569f1-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="569f1-162">Hola por encima de las entradas de ruta invalidará ruta de hello predeterminada "0.0.0.0/0", pero regla 10.0.0.0/16 Hola predeterminada que aún existen de forma que permitiría tráfico dentro de tooroute de red virtual de hello directamente toohello destino y no toohello dispositivo de red Virtual.</span><span class="sxs-lookup"><span data-stu-id="569f1-162">hello above route entry will override hello default "0.0.0.0/0" route, but hello default 10.0.0.0/16 rule still existing which would allow traffic within hello VNet tooroute directly toohello destination and not toohello Network Virtual Appliance.</span></span> <span data-ttu-id="569f1-163">toocorrect que se debe agregar esta regla de seguimiento de Hola de comportamiento.</span><span class="sxs-lookup"><span data-stu-id="569f1-163">toocorrect this behavior hello follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="569f1-164">En este momento no hay un toobe elección realizado.</span><span class="sxs-lookup"><span data-stu-id="569f1-164">At this point there is a choice toobe made.</span></span> <span data-ttu-id="569f1-165">Con hello por encima de dos rutas todo el tráfico enrutará toohello firewall para evaluación, incluso el tráfico dentro de una sola subred.</span><span class="sxs-lookup"><span data-stu-id="569f1-165">With hello above two routes all traffic will route toohello firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="569f1-166">Esto puede ser deseable, pero tooallow tráfico dentro de un tooroute de subred localmente sin la participación del firewall de Hola se puede agregar una regla en tercer lugar, muy específica.</span><span class="sxs-lookup"><span data-stu-id="569f1-166">This may be desired, however tooallow traffic within a subnet tooroute locally without involvement from hello firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="569f1-167">Esta ruta enrutan directamente los Estados que destine de cualquier dirección de subred local de hello puede simplemente (NextHopType = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="569f1-167">This route states that any address destine for hello local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="569f1-168">Por último, con la tabla de enrutamiento de hello crean y rellenan con un rutas definidas por el usuario, tabla de hello debe ser subred tooa enlazado.</span><span class="sxs-lookup"><span data-stu-id="569f1-168">Finally, with hello routing table created and populated with a user defined routes, hello table must now be bound tooa subnet.</span></span> <span data-ttu-id="569f1-169">En el script de Hola, tabla de rutas de front-end de hello también es dependiente toohello subred de front-end.</span><span class="sxs-lookup"><span data-stu-id="569f1-169">In hello script, hello front end route table is also bound toohello Frontend subnet.</span></span> <span data-ttu-id="569f1-170">Este es el script de enlace de hello para la subred de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-170">Here is hello binding script for hello back end subnet.</span></span>
   
     <span data-ttu-id="569f1-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span><span class="sxs-lookup"><span data-stu-id="569f1-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="569f1-172">reenvío de IP</span><span class="sxs-lookup"><span data-stu-id="569f1-172">IP Forwarding</span></span>
<span data-ttu-id="569f1-173">Un tooUDR de característica complementaria, es el reenvío IP.</span><span class="sxs-lookup"><span data-stu-id="569f1-173">A companion feature tooUDR, is IP Forwarding.</span></span> <span data-ttu-id="569f1-174">Se trata de una configuración en un dispositivo Virtual que permita el tráfico de tooreceive no específicamente dirigidos toohello dispositivo y, a continuación, reenviar ese destino final de tooits de tráfico.</span><span class="sxs-lookup"><span data-stu-id="569f1-174">This is a setting on a Virtual Appliance that allows it tooreceive traffic not specifically addressed toohello appliance and then forward that traffic tooits ultimate destination.</span></span>

<span data-ttu-id="569f1-175">Por ejemplo, si el tráfico de AppVM01 hace que un servidor de DNS01 toohello de solicitud, UDR enrutaría este firewall toohello.</span><span class="sxs-lookup"><span data-stu-id="569f1-175">As an example, if traffic from AppVM01 makes a request toohello DNS01 server, UDR would route this toohello firewall.</span></span> <span data-ttu-id="569f1-176">Con el reenvío IP habilitada, se aceptarán por dispositivo de hello (10.0.0.4) y, a continuación, reenvía el destino último tooits (10.0.2.4) tráfico hello para el destino de hello DNS01 (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="569f1-176">With IP Forwarding enabled, hello traffic for hello DNS01 destination (10.0.2.4) will be accepted by hello appliance (10.0.0.4) and then forwarded tooits ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="569f1-177">Sin el reenvío IP habilitado en hello Firewall, tráfico no haría aceptado por dispositivo de Hola a pesar de la tabla de rutas Hola dispone firewall Hola salto siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-177">Without IP Forwarding enabled on hello Firewall, traffic would not be accepted by hello appliance even though hello route table has hello firewall as hello next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="569f1-178">Es crítico tooremember tooenable el reenvío IP junto con usuario definido el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="569f1-178">It’s critical tooremember tooenable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="569f1-179">Para configurar el reenvío IP se usa un solo comando y puede realizarse durante la creación de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="569f1-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="569f1-180">Para hello flujo de este fragmento de código de ejemplo Hola es hacia el final de hello del script de Hola y agrupado con comandos de Hola UDR:</span><span class="sxs-lookup"><span data-stu-id="569f1-180">For hello flow of this example hello code snippet is towards hello end of hello script and grouped with hello UDR commands:</span></span>

1. <span data-ttu-id="569f1-181">Llame a la instancia de la máquina virtual de Hola que es su dispositivo virtual, Hola firewall en este caso y habilitar el reenvío IP (tenga en cuenta; cualquier elemento de rojo que comienza con un signo de dólar (p. ej.: $VMName[0]) es una variable definida por el usuario desde un script de Hola en la sección de referencia de Hola de este documento.</span><span class="sxs-lookup"><span data-stu-id="569f1-181">Call hello VM instance that is your virtual appliance, hello firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="569f1-182">Hola cero entre corchetes, [0], representa Hola primera VM de matriz de Hola de máquinas virtuales, para toowork de script de ejemplo de Hola sin modificaciones, debe ser la primera máquina virtual (VM 0) de Hola Hola firewall):</span><span class="sxs-lookup"><span data-stu-id="569f1-182">hello zero in brackets, [0], represents hello first VM in hello array of VMs, for hello example script toowork without modification, hello first VM (VM 0) must be hello firewall):</span></span>
   
     <span data-ttu-id="569f1-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span><span class="sxs-lookup"><span data-stu-id="569f1-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="569f1-184">Grupos de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="569f1-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="569f1-185">En este ejemplo, se crea un grupo de seguridad de red y se carga después una única regla.</span><span class="sxs-lookup"><span data-stu-id="569f1-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="569f1-186">Este grupo es, a continuación, enlazar sólo toohello front-end y back-end subredes (y no Hola SecNet).</span><span class="sxs-lookup"><span data-stu-id="569f1-186">This group is then bound only toohello Frontend and Backend subnets (not hello SecNet).</span></span> <span data-ttu-id="569f1-187">Mediante declaración se va a compilar Hola siguiente regla:</span><span class="sxs-lookup"><span data-stu-id="569f1-187">Declaratively hello following rule is being built:</span></span>

1. <span data-ttu-id="569f1-188">Todo (todos los puertos) el tráfico de hello Internet toohello se deniega todo red virtual (todas las subredes)</span><span class="sxs-lookup"><span data-stu-id="569f1-188">Any traffic (all ports) from hello Internet toohello entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="569f1-189">Aunque en este ejemplo se usan grupos de seguridad de red, su principal objetivo es constituir un segundo nivel de defensa frente a errores de configuración manual.</span><span class="sxs-lookup"><span data-stu-id="569f1-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="569f1-190">Queremos tooblock tráfico todo el tráfico entrante de hello tooeither de internet Hola front-end o subredes de back-end, el tráfico solo deben fluya a través de Hola firewall de toohello de subred SecNet (y a continuación si adecuados en toohello front-end o back-end de subredes).</span><span class="sxs-lookup"><span data-stu-id="569f1-190">We want tooblock all inbound traffic from hello internet tooeither hello Frontend or Backend subnets, traffic should only flow through hello SecNet subnet toohello firewall (and then if appropriate on toohello Frontend or Backend subnets).</span></span> <span data-ttu-id="569f1-191">Además, con las reglas UDR de hello en su lugar, todo el tráfico que ha llegado en hello subredes front-end o back-end se dirigirá out toohello firewall (gracias tooUDR).</span><span class="sxs-lookup"><span data-stu-id="569f1-191">Plus, with hello UDR rules in place, any traffic that did make it into hello Frontend or Backend subnets would be directed out toohello firewall (thanks tooUDR).</span></span> <span data-ttu-id="569f1-192">firewall de Hola que vea esto como un flujo asimétrico y reduciría el tráfico saliente Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-192">hello firewall would see this as an asymmetric flow and would drop hello outbound traffic.</span></span> <span data-ttu-id="569f1-193">Por tanto, hay tres niveles de Hola de protección de seguridad front-end y back-end subredes; (1) no tiene extremos abiertos en hello FrontEnd001 y BackEnd001 servicios en la nube, (2) NSG denegar el tráfico de Internet, firewall de hello (3) quitar tráfico asimétrico de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-193">Thus there are three layers of security protecting hello Frontend and Backend subnets; 1) no open endpoints on hello FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from hello Internet, 3) hello firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="569f1-194">Un punto interesante sobre Hola grupo de seguridad de red en este ejemplo es que contiene una única regla, que se muestra a continuación, que es toodeny internet tráfico toohello toda red virtual que incluiría la subred de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-194">One interesting point regarding hello Network Security Group in this example is that it contains only one rule, shown below, which is toodeny internet traffic toohello entire virtual network which would include hello Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="569f1-195">Sin embargo, puesto que hello NSG solo está enlazado toohello front-end y back-end subredes, no procesa Hola regla en el tráfico de subred de seguridad toohello de entrada.</span><span class="sxs-lookup"><span data-stu-id="569f1-195">However, since hello NSG is only bound toohello Frontend and Backend subnets, hello rule isn’t processed on traffic inbound toohello Security subnet.</span></span> <span data-ttu-id="569f1-196">Como resultado, incluso si la regla NSG Hola no indica ninguna dirección de tooany del tráfico de Internet en Hola de red virtual, porque hello que NSG nunca fue enlazado toohello subred de seguridad, el tráfico fluirá toohello subred de seguridad.</span><span class="sxs-lookup"><span data-stu-id="569f1-196">As a result, even though hello NSG rule says no Internet traffic tooany address on hello VNet, because hello NSG was never bound toohello Security subnet, traffic will flow toohello Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="569f1-197">Reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="569f1-197">Firewall Rules</span></span>
<span data-ttu-id="569f1-198">En firewall de hello, las reglas de reenvío debe toobe creado.</span><span class="sxs-lookup"><span data-stu-id="569f1-198">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="569f1-199">Puesto que firewall de hello es tráfico de bloqueo o reenvío todo el tráfico entrante, saliente y intra-red virtual son necesarias muchas reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="569f1-199">Since hello firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="569f1-200">Además, todo el tráfico entrante llegará a la dirección IP pública de hello servicio de seguridad (en puertos diferentes), toobe procesados por firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-200">Also, all inbound traffic will hit hello Security Service public IP address (on different ports), toobe processed by hello firewall.</span></span> <span data-ttu-id="569f1-201">Una práctica recomendada es flujos lógicos de hello toodiagram antes de configurar la repetición de tooavoid de reglas de firewall y subredes de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="569f1-201">A best practice is toodiagram hello logical flows before setting up hello subnets and firewall rules tooavoid rework later.</span></span> <span data-ttu-id="569f1-202">Hello siguiente ilustración es una vista lógica de reglas de firewall de hello en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="569f1-202">hello following figure is a logical view of hello firewall rules for this example:</span></span>

<span data-ttu-id="569f1-203">![Vista lógica de hello las reglas de Firewall][2]</span><span class="sxs-lookup"><span data-stu-id="569f1-203">![Logical View of hello Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="569f1-204">En función de hello que usa el dispositivo de red Virtual, los puertos de administración de hello varían.</span><span class="sxs-lookup"><span data-stu-id="569f1-204">Based on hello Network Virtual Appliance used, hello management ports will vary.</span></span> <span data-ttu-id="569f1-205">En este ejemplo se hace referencia a un firewall Barracuda NextGen que utiliza los puertos 22, 801 y 807.</span><span class="sxs-lookup"><span data-stu-id="569f1-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="569f1-206">Consulte Hola dispositivo proveedor documentación toofind Hola exacta puertos utilizados para la administración de dispositivos Hola usándola.</span><span class="sxs-lookup"><span data-stu-id="569f1-206">Please consult hello appliance vendor documentation toofind hello exact ports used for management of hello device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="569f1-207">Descripción de las reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="569f1-207">Logical Rule Description</span></span>
<span data-ttu-id="569f1-208">En el diagrama lógico Hola anterior, subred de seguridad de hello no se muestra ya que firewall de hello es el único recurso al que hello en la subred, y este diagrama muestra las reglas de firewall de Hola y cómo lógicamente permitir o denegación flujos de tráfico y no Hola enrutado ruta de acceso real.</span><span class="sxs-lookup"><span data-stu-id="569f1-208">In hello logical diagram above, hello security subnet is not shown since hello firewall is hello only resource on that subnet, and this diagram is showing hello firewall rules and how they logically allow or deny traffic flows and not hello actual routed path.</span></span> <span data-ttu-id="569f1-209">Además, puertos externos Hola seleccionados para hello tráfico de RDP son puertos rango superior (8014 – 8026) y se han seleccionado toosomewhat alinear con hello última dos octetos de la dirección IP local de Hola para mejorar la legibilidad sea más fácil (por ejemplo, dirección de servidor local 10.0.1.4 está asociado puerto externo 8014), sin embargo podría utilizarse ninguno de los puertos no conflictivos superior.</span><span class="sxs-lookup"><span data-stu-id="569f1-209">Also, hello external ports selected for hello RDP traffic are higher ranged ports (8014 – 8026) and were selected toosomewhat align with hello last two octets of hello local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="569f1-210">En este ejemplo, necesitamos siete tipos de reglas que se describen a continuación:</span><span class="sxs-lookup"><span data-stu-id="569f1-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="569f1-211">Reglas externas (para el tráfico entrante):</span><span class="sxs-lookup"><span data-stu-id="569f1-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="569f1-212">Regla de Firewall de administración: Esta regla de redirección de la aplicación permite que los puertos de administración de tráfico toopass toohello del dispositivo de hello red virtual.</span><span class="sxs-lookup"><span data-stu-id="569f1-212">Firewall Management Rule: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance.</span></span>
  2. <span data-ttu-id="569f1-213">Las reglas de RDP (para cada servidor de windows): estos cuatro reglas (uno para cada servidor) le permitirá la administración de hello servidores individuales a través de RDP.</span><span class="sxs-lookup"><span data-stu-id="569f1-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of hello individual servers via RDP.</span></span> <span data-ttu-id="569f1-214">Esto se podría incluirse también en una regla de función de las capacidades de Hola de hello de dispositivo de red Virtual que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="569f1-214">This could also be bundled into one rule depending on hello capabilities of hello Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="569f1-215">Las reglas de tráfico de aplicación: Hay dos reglas de tráfico de la aplicación, Hola primero para el tráfico de web front-end de Hola y Hola en segundo lugar para el tráfico de back-end de hello (por ejemplo, la capa del toodata servidor web).</span><span class="sxs-lookup"><span data-stu-id="569f1-215">Application Traffic Rules: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="569f1-216">configuración de Hola de estas reglas dependerá de arquitectura de red de hello (donde se colocan los servidores) y flujos de tráfico (el tráfico de Hola de qué dirección fluye y qué puertos se usan).</span><span class="sxs-lookup"><span data-stu-id="569f1-216">hello configuration of these rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="569f1-217">primera regla de Hola permitirá a servidor de aplicaciones de hello aplicación real tráfico tooreach Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-217">hello first rule will allow hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="569f1-218">Mientras hello otras reglas permiten para la seguridad, administración, etc., reglas de aplicación son los que permiten tooaccess de los usuarios o servicios externos Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="569f1-218">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="569f1-219">En este ejemplo, hay un único servidor web en el puerto 80, lo que una única aplicación regla de firewall redirigirá el tráfico entrante toohello externo IP, dirección IP interna de servidores de web de toohello.</span><span class="sxs-lookup"><span data-stu-id="569f1-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span> <span data-ttu-id="569f1-220">Hola redirigido sesión tráfico podría ser NAT tenía toohello interno del servidor.</span><span class="sxs-lookup"><span data-stu-id="569f1-220">hello redirected traffic session would be NAT’d toohello internal server.</span></span>
     * <span data-ttu-id="569f1-221">Hola es la segunda regla de tráfico de la aplicación Hola back-end regla tooallow hello Web tootalk toohello AppVM01 servidor (pero no AppVM02) a través de cualquier puerto.</span><span class="sxs-lookup"><span data-stu-id="569f1-221">hello second Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="569f1-222">Reglas internas (para el tráfico entre redes virtuales)</span><span class="sxs-lookup"><span data-stu-id="569f1-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="569f1-223">Regla de salida tooInternet: esta regla para permitir el tráfico de cualquier red toopass toohello seleccionado redes.</span><span class="sxs-lookup"><span data-stu-id="569f1-223">Outbound tooInternet Rule: This rule will allow traffic from any network toopass toohello selected networks.</span></span> <span data-ttu-id="569f1-224">Esta regla suele ser una regla predeterminada ya en firewall de hello, pero en un estado deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="569f1-224">This rule is usually a default rule already on hello firewall, but in a disabled state.</span></span> <span data-ttu-id="569f1-225">Esta regla debe habilitarse para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="569f1-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="569f1-226">Regla DNS: Esta regla permite a sólo DNS (el puerto 53) tráfico toopass toohello servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="569f1-226">DNS Rule: This rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="569f1-227">Para este entorno que se bloquea la mayor parte del tráfico de hello front-end toohello back-end, esta regla se lo permita específicamente DNS desde cualquier subred local.</span><span class="sxs-lookup"><span data-stu-id="569f1-227">For this environment most traffic from hello Frontend toohello Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="569f1-228">Subred tooSubnet regla: esta regla es tooallow cualquier servidor de copia de hello Terminar server de tooany de subred tooconnect de subred de front-end de hello (pero no Hola inversa).</span><span class="sxs-lookup"><span data-stu-id="569f1-228">Subnet tooSubnet Rule: This rule is tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet (but not hello reverse).</span></span>
* <span data-ttu-id="569f1-229">Regla para notificaciones de error (para el tráfico que no cumple alguna de hello anterior):</span><span class="sxs-lookup"><span data-stu-id="569f1-229">Fail-safe Rule (for traffic that doesn’t meet any of hello above):</span></span>
  1. <span data-ttu-id="569f1-230">Denegar todas las reglas de tráfico: Esto siempre debe ser regla final de hello (en términos de prioridad) y por lo tanto si el tráfico de un flujo se produce un error toomatch cualquiera de hello anteriores se eliminarán por esta regla de reglas.</span><span class="sxs-lookup"><span data-stu-id="569f1-230">Deny All Traffic Rule: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="569f1-231">Esta es una regla predeterminada y normalmente está activada; normalmente no se necesitan modificaciones.</span><span class="sxs-lookup"><span data-stu-id="569f1-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="569f1-232">En la regla de tráfico de aplicación segundo hello, cualquier puerto está permitido para fácil de este ejemplo, Hola de un escenario real más específicos puertos e intervalos de direcciones deben ser la superficie expuesta a ataques hello tooreduce usadas de esta regla.</span><span class="sxs-lookup"><span data-stu-id="569f1-232">On hello second application traffic rule, any port is allowed for easy of this example, in a real scenario hello most specific port and address ranges should be used tooreduce hello attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="569f1-233">Una vez que se crean todos Hola por encima de las reglas, es importante tooreview prioridad Hola el tráfico de tooensure de cada regla se permitirá o denegará según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="569f1-233">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="569f1-234">En este ejemplo, reglas de hello están en orden de prioridad.</span><span class="sxs-lookup"><span data-stu-id="569f1-234">For this example, hello rules are in priority order.</span></span> <span data-ttu-id="569f1-235">Es fácil toobe bloqueado fuera del firewall de hello debido ordenados toomis reglas.</span><span class="sxs-lookup"><span data-stu-id="569f1-235">It's easy toobe locked out of hello firewall due toomis-ordered rules.</span></span> <span data-ttu-id="569f1-236">Como mínimo, asegúrese de administración de Hola para firewall de hello propio siempre es regla de prioridad más alta absoluta Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-236">At a minimum, ensure hello management for hello firewall itself is always hello absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="569f1-237">Requisitos previos de las reglas</span><span class="sxs-lookup"><span data-stu-id="569f1-237">Rule Prerequisites</span></span>
<span data-ttu-id="569f1-238">Un requisito previo de firewall Hola Máquina Virtual de ejecución Hola son extremos públicos.</span><span class="sxs-lookup"><span data-stu-id="569f1-238">One prerequisite for hello Virtual Machine running hello firewall are public endpoints.</span></span> <span data-ttu-id="569f1-239">Para el tráfico de hello firewall tooprocess extremos públicos de hello adecuada deben estar abiertos.</span><span class="sxs-lookup"><span data-stu-id="569f1-239">For hello firewall tooprocess traffic hello appropriate public endpoints must be open.</span></span> <span data-ttu-id="569f1-240">Hay tres tipos de tráfico en este ejemplo; (1) administración tráfico toocontrol Hola firewall y las reglas de firewall, servidores de windows RDP (2) el tráfico toocontrol hello y tráfico de la aplicación (3).</span><span class="sxs-lookup"><span data-stu-id="569f1-240">There are three types of traffic in this example; 1) Management traffic toocontrol hello firewall and firewall rules, 2) RDP traffic toocontrol hello windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="569f1-241">Estos son tres columnas de tipos de tráfico de hello superior de Hola la mitad de la vista lógica de reglas de firewall de hello anteriores.</span><span class="sxs-lookup"><span data-stu-id="569f1-241">These are hello three columns of traffic types in hello upper half of logical view of hello firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="569f1-242">Un takeway clave aquí es tooremember que **todos los** tráfico procederá a través de firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-242">A key takeway here is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="569f1-243">Toohello de escritorio tooremote por lo que el servidor IIS01, aunque se encuentre en el servicio de nube de Front-End de Hola y de subred de Front-End de hello, tooaccess este servidor se va a necesitar tooRDP toohello firewall en 8014 de puerto y, a continuación, Permitir solicitud RDP de hello firewall tooroute Hola internamente toohello IIS01 el puerto de RDP.</span><span class="sxs-lookup"><span data-stu-id="569f1-243">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="569f1-244">Hola "Conectar" del portal de Azure botón no funcionará porque no hay ningún tooIIS01 de ruta de acceso directo de RDP (lo que puede ver el portal de hello).</span><span class="sxs-lookup"><span data-stu-id="569f1-244">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="569f1-245">Esto significa que todas las conexiones desde Hola internet estarán toohello servicio de seguridad y un puerto, p. ej. secscv001.cloudapp.net:xxxx (Hola de referencia por encima del diagrama para la asignación de hello del puerto externo y dirección IP interna y el puerto).</span><span class="sxs-lookup"><span data-stu-id="569f1-245">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference hello above diagram for hello mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="569f1-246">Un punto de conexión puede abrirse en tiempo de Hola de creación de máquinas virtuales o publicar compilación tal y como se hace en el script de ejemplo de Hola y se muestra a continuación en este fragmento de código (tenga en cuenta; cualquier elemento que comienza con un signo de dólar (p. ej.: $VMName[$i]) es una variable definida por el usuario desde un script de Hola en referencia de Hola sección de CE de este documento.</span><span class="sxs-lookup"><span data-stu-id="569f1-246">An endpoint can be opened either at hello time of VM creation or post build as is done in hello example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="569f1-247">Hola "$i" entre corchetes, [$i] representa número de la matriz de Hola de una VM específica en una matriz de máquinas virtuales):</span><span class="sxs-lookup"><span data-stu-id="569f1-247">hello “$i” in brackets, [$i], represents hello array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="569f1-248">Aunque no claramente que se muestra aquí debido toohello uso de las variables, pero los puntos de conexión son **sólo** abiertos en hello seguridad de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="569f1-248">Although not clearly shown here due toohello use of variables, but endpoints are **only** opened on hello Security Cloud Service.</span></span> <span data-ttu-id="569f1-249">Se trata de tooensure que se controla todo el tráfico entrante (enrutan, NAT tenía, quitarla) por firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-249">This is tooensure that all inbound traffic is handled (routed, NAT'd, dropped) by hello firewall.</span></span>

<span data-ttu-id="569f1-250">Un cliente de administración deberá toobe instalado en un servidor de seguridad de PC toomanage hello y crear configuraciones de hello necesarias.</span><span class="sxs-lookup"><span data-stu-id="569f1-250">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="569f1-251">Vea proveedor de documentación de su firewall (o en otro NVA) hello en cómo toomanage Hola dispositivo.</span><span class="sxs-lookup"><span data-stu-id="569f1-251">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="569f1-252">resto de Hola de esta sección y la siguiente sección hello, creación de reglas de Firewall, describirá configuración Hola de firewall de hello, a través del cliente de administración de proveedores de hello (es decir, no Hola portal de Azure o PowerShell).</span><span class="sxs-lookup"><span data-stu-id="569f1-252">hello remainder of this section and hello next section, Firewall Rules Creation, will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="569f1-253">Instrucciones para la descarga de cliente y conexión toohello Barracuda utilizado en este ejemplo pueden encontrarse aquí: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="569f1-253">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="569f1-254">Una vez iniciada sesión en firewall de hello pero antes de crear las reglas de firewall, hay dos clases de requisitos previos de objeto que pueden facilitar la creación de reglas de hello; Objetos de servicio y de red.</span><span class="sxs-lookup"><span data-stu-id="569f1-254">Once logged onto hello firewall but before creating firewall rules, there are two prerequisite object classes that can make creating hello rules easier; Network & Service objects.</span></span>

<span data-ttu-id="569f1-255">En este ejemplo, tres objetos de red con nombre deben ser definida (uno para la subred de front-end de Hola y subred de back-end de hello, también un objeto de red para la dirección IP de hello del servidor DNS de hello).</span><span class="sxs-lookup"><span data-stu-id="569f1-255">For this example, three named network objects should be defined (one for hello Frontend subnet and hello Backend subnet, also a network object for hello IP address of hello DNS server).</span></span> <span data-ttu-id="569f1-256">toocreate una red con nombre; a partir de panel de cliente de administración de dispositivo Barracuda NG hello, vaya la ficha de configuración de toohello, en la sección de configuración operativa hello, haga clic en el conjunto de reglas, a continuación, haga clic en "Redes" en el menú de objetos de servidor de seguridad de Hola y haga clic en nuevo en el menú Editar redes de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-256">toocreate a named network; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Networks” under hello Firewall Objects menu, then click New in hello Edit Networks menu.</span></span> <span data-ttu-id="569f1-257">objeto de red de Hello ahora se puede crear, mediante la adición de nombre de Hola y un prefijo de hello:</span><span class="sxs-lookup"><span data-stu-id="569f1-257">hello network object can now be created, by adding hello name and hello prefix:</span></span>

<span data-ttu-id="569f1-258">![Creación de un objeto de red front-end][3]</span><span class="sxs-lookup"><span data-stu-id="569f1-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="569f1-259">Esto creará una red con nombre para la subred de front-end de hello, se debe crear un objeto similar para así la subred de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-259">This will create a named network for hello FrontEnd subnet, a similar object should be created for hello BackEnd subnet as well.</span></span> <span data-ttu-id="569f1-260">Ahora subredes Hola pueden indicarse más fácilmente por nombre en las reglas de firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-260">Now hello subnets can be more easily referenced by name in hello firewall rules.</span></span>

<span data-ttu-id="569f1-261">Para hello objeto de servidor DNS:</span><span class="sxs-lookup"><span data-stu-id="569f1-261">For hello DNS Server Object:</span></span>

<span data-ttu-id="569f1-262">![Creación de un objeto de servidor DNS][4]</span><span class="sxs-lookup"><span data-stu-id="569f1-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="569f1-263">Esta referencia de dirección IP solo se utilizará en una regla DNS más adelante en el documento de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-263">This single IP address reference will be utilized in a DNS rule later in hello document.</span></span>

<span data-ttu-id="569f1-264">objetos de requisitos previos segundo Hola son objetos de servicios.</span><span class="sxs-lookup"><span data-stu-id="569f1-264">hello second prerequisite objects are Services objects.</span></span> <span data-ttu-id="569f1-265">Estos representan puertos de conexión RDP de Hola para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="569f1-265">These will represent hello RDP connection ports for each server.</span></span> <span data-ttu-id="569f1-266">Puesto que el objeto de servicio RDP existente de hello es el puerto RDP de toohello enlazados de forma predeterminada, 3389, nuevos servicios pueden crearse tooallow tráfico de puertos externos de hello (8014-8026).</span><span class="sxs-lookup"><span data-stu-id="569f1-266">Since hello existing RDP service object is bound toohello default RDP port, 3389, new Services can be created tooallow traffic from hello external ports (8014-8026).</span></span> <span data-ttu-id="569f1-267">Hola nuevo puertos también podrían agregarse toohello servicio RDP existente, pero para facilitar la demostración, se puede crear una regla individual para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="569f1-267">hello new ports could also be added toohello existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="569f1-268">toocreate una nueva regla RDP para un servidor; desde el panel de cliente de administración de dispositivo Barracuda NG hello, navegue toohello ficha de configuración, en hello configuración operativa sección haga clic en el conjunto de reglas, a continuación, haga clic en "Servicios" en hello menú de objetos de servidor de seguridad, desplácese hacia abajo de la lista de hello de servicios y seleccione Hola Servicio "RDP".</span><span class="sxs-lookup"><span data-stu-id="569f1-268">toocreate a new RDP rule for a server; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Services” under hello Firewall Objects menu, scroll down hello list of services and select hello “RDP” service.</span></span> <span data-ttu-id="569f1-269">Haga con el botón derecho y seleccione Copiar; después, haga clic con el botón derecho y seleccione Pegar.</span><span class="sxs-lookup"><span data-stu-id="569f1-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="569f1-270">Ahora hay un objeto de servicio RDP-Copy1 que se puede editar.</span><span class="sxs-lookup"><span data-stu-id="569f1-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="569f1-271">Haga clic en Copy1 RDP y seleccione Editar, Hola Editar objeto de servicio ventana se abrirá como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="569f1-271">Right-click RDP-Copy1 and select Edit, hello Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="569f1-272">![Copia de la regla predeterminada de RDP][5]</span><span class="sxs-lookup"><span data-stu-id="569f1-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="569f1-273">valores de Hello, a continuación, pueden ser editado toorepresent Hola servicio RDP para un servidor específico.</span><span class="sxs-lookup"><span data-stu-id="569f1-273">hello values can then be edited toorepresent hello RDP service for a specific server.</span></span> <span data-ttu-id="569f1-274">Para hello AppVM01 anteriormente predeterminado regla RDP debe ser modificada tooreflect un nuevo nombre de servicio, descripción, y utiliza el puerto de RDP externo en hello diagrama de la figura 8 (Nota: se cambian los puertos de Hola de hello predeterminada RDP 3389 toohello del puerto de externo que se va a utilizar para este servidor específico, en caso de hello de puerto externo de hello AppVM01 es 8025) hello servicio modificado se se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="569f1-274">For AppVM01 hello above default RDP rule should be modified tooreflect a new Service Name, Description, and external RDP Port used in hello Figure 8 diagram (Note: hello ports are changed from hello RDP default of 3389 toohello external port being used for this specific server, in hello case of AppVM01 hello external Port is 8025) hello modified service is shown below:</span></span>

<span data-ttu-id="569f1-275">![Regla de AppVM01][6]</span><span class="sxs-lookup"><span data-stu-id="569f1-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="569f1-276">Este proceso debe ser repetida toocreate servicios de RDP para hello restantes servidores; AppVM02, DNS01 y IIS01.</span><span class="sxs-lookup"><span data-stu-id="569f1-276">This process must be repeated toocreate RDP Services for hello remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="569f1-277">creación de Hello de estos servicios realizará creación de reglas de hello más sencillo y más obvio en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-277">hello creation of these Services will make hello Rule creation simpler and more obvious in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="569f1-278">Un servicio RDP para hello Firewall no es necesario por dos razones; firewall de hello (1) la primera máquina virtual es una imagen de basadas en Linux, por lo que se usarían SSH en el puerto 22 para la administración de máquinas virtuales en lugar de RDP y (2) el puerto 22 y otros dos puertos de administración se permiten en hello primera regla de administración se describe a continuación tooallow para la conectividad de administración.</span><span class="sxs-lookup"><span data-stu-id="569f1-278">An RDP service for hello Firewall is not needed for two reasons; 1) first hello firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in hello first management rule described below tooallow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="569f1-279">Creación de reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="569f1-279">Firewall Rules Creation</span></span>
<span data-ttu-id="569f1-280">En este ejemplo se usan tres tipos de reglas de firewall, todas ellas con iconos distintos:</span><span class="sxs-lookup"><span data-stu-id="569f1-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="569f1-281">una regla de redireccionamiento de la aplicación Hello: ![icono de redirigir la aplicación][7]</span><span class="sxs-lookup"><span data-stu-id="569f1-281">hello Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="569f1-282">regla de NAT de destino de Hello: ![icono de NAT de destino][8]</span><span class="sxs-lookup"><span data-stu-id="569f1-282">hello Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="569f1-283">regla de paso de Hello: ![pasar icono][9]</span><span class="sxs-lookup"><span data-stu-id="569f1-283">hello Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="569f1-284">Obtener más información sobre estas reglas puede encontrarse en el sitio web de hello Barracuda.</span><span class="sxs-lookup"><span data-stu-id="569f1-284">More information on these rules can be found at hello Barracuda web site.</span></span>

<span data-ttu-id="569f1-285">toocreate Hola siguiendo reglas (o comprobar las reglas existentes de forma predeterminada), a partir de panel de cliente de administración de dispositivo Barracuda NG hello, vaya la ficha de configuración de toohello, Hola configuración operativa sección, haga clic en el conjunto de reglas.</span><span class="sxs-lookup"><span data-stu-id="569f1-285">toocreate hello following rules (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="569f1-286">Llama a una cuadrícula, "Main reglas" mostrará Hola existente las reglas activas y desactivadas en este servidor de seguridad.</span><span class="sxs-lookup"><span data-stu-id="569f1-286">A grid called, “Main Rules” will show hello existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="569f1-287">En hello superior derecha de esta cuadrícula es una pequeña, de color verde "+" botón, haga clic en este toocreate una nueva regla (Nota: el firewall puede "bloquear" para los cambios, si ve un botón de marca "Bloqueo" y son no se puede toocreate o editar reglas, haga clic en este botón demasiado "desbloquear" Hola SAR de regla t y permitir la edición).</span><span class="sxs-lookup"><span data-stu-id="569f1-287">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello rule set and allow editing).</span></span> <span data-ttu-id="569f1-288">Si desea tooedit una regla existente, seleccione esa regla, haga clic en y seleccione Editar regla.</span><span class="sxs-lookup"><span data-stu-id="569f1-288">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="569f1-289">Una vez que las reglas se crea o modifica, se deben insertar toohello firewall y, a continuación, activar, si no es así regla Hola cambios no surtirán efecto.</span><span class="sxs-lookup"><span data-stu-id="569f1-289">Once your rules are created and/or modified, they must be pushed toohello firewall and then activated, if this is not done hello rule changes will not take effect.</span></span> <span data-ttu-id="569f1-290">proceso de activación e inserción de Hola se describe a continuación las descripciones de reglas de detalles de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-290">hello push and activation process is described below hello details rule descriptions.</span></span>

<span data-ttu-id="569f1-291">detalles de Hola de cada regla necesario toocomplete en este ejemplo se describe como sigue:</span><span class="sxs-lookup"><span data-stu-id="569f1-291">hello specifics of each rule required toocomplete this example are described as follows:</span></span>

* <span data-ttu-id="569f1-292">**Regla de administración de Firewall**: una regla de redireccionamiento de esta aplicación permite el tráfico toopass toohello los puertos de administración del dispositivo Hola red virtual, en este ejemplo un Barracuda NextGen Firewall.</span><span class="sxs-lookup"><span data-stu-id="569f1-292">**Firewall Management Rule**: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="569f1-293">puertos de administración de Hello estén 801, 807 y, opcionalmente, 22.</span><span class="sxs-lookup"><span data-stu-id="569f1-293">hello management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="569f1-294">puertos internos y externos de Hola se Hola iguales (es decir, ninguna traducción de puerto).</span><span class="sxs-lookup"><span data-stu-id="569f1-294">hello external and internal ports are hello same (i.e. no port translation).</span></span> <span data-ttu-id="569f1-295">SETUP-MGMT-ACCESS es una regla predeterminada y está habilitada de forma predeterminada (en Barracuda NextGen Firewall versión 6.1).</span><span class="sxs-lookup"><span data-stu-id="569f1-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="569f1-296">![Regla de administración de firewall][10]</span><span class="sxs-lookup"><span data-stu-id="569f1-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="569f1-297">Hello espacio de direcciones de origen en esta regla es cualquier, si hello se conocen los intervalos de direcciones IP de administración, lo que reduce este ámbito también reduciría puertos de administración de toohello superficie de ataque de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-297">hello source address space in this rule is Any, if hello management IP address ranges are known, reducing this scope would also reduce hello attack surface toohello management ports.</span></span>
> 
> 

* <span data-ttu-id="569f1-298">**Reglas de RDP**: reglas NAT de destino de estos le permitirá la administración del programa Hola a servidores individuales a través de RDP.</span><span class="sxs-lookup"><span data-stu-id="569f1-298">**RDP Rules**:  These Destination NAT rules will allow management of hello individual servers via RDP.</span></span>
  <span data-ttu-id="569f1-299">Hay cuatro toocreate crítico campos necesarios de esta regla:</span><span class="sxs-lookup"><span data-stu-id="569f1-299">There are four critical fields needed toocreate this rule:</span></span>
  
  1. <span data-ttu-id="569f1-300">Origen: tooallow RDP desde cualquier lugar, referencia de Hola "Cualquiera" se usa en el campo de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-300">Source – tooallow RDP from anywhere, hello reference “Any” is used in hello Source field.</span></span>
  2. <span data-ttu-id="569f1-301">Servicio: usar hello objeto adecuado de servicio creado anteriormente, en este caso "AppVM01 RDP", puertos externos Hola redirección la dirección IP local del servidor toohello y tooport 3386 (puerto RDP de hello predeterminado).</span><span class="sxs-lookup"><span data-stu-id="569f1-301">Service – use hello appropriate Service Object created earlier, in this case “AppVM01 RDP”, hello external ports redirect toohello servers local IP address and tooport 3386 (hello default RDP port).</span></span> <span data-ttu-id="569f1-302">Esta regla concreta es para tooAppVM01 de acceso RDP.</span><span class="sxs-lookup"><span data-stu-id="569f1-302">This specific rule is for RDP access tooAppVM01.</span></span>
  3. <span data-ttu-id="569f1-303">Destino: debe ser hello *puerto local en el servidor de seguridad de hello*, "DCHP 1 IP Local" o eth0 si usa direcciones IP estáticas.</span><span class="sxs-lookup"><span data-stu-id="569f1-303">Destination – should be hello *local port on hello firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="569f1-304">número ordinal de Hello (eth0, eth1, etcetera) puede ser diferente si el dispositivo de red tiene varias interfaces locales.</span><span class="sxs-lookup"><span data-stu-id="569f1-304">hello ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="569f1-305">Éste es el puerto de hello firewall Hola envía desde (pueden ser Hola igual como Hola puerto de recepción), destino enrutado real Hola se encuentre en el campo de la lista de destinos de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-305">This is hello port hello firewall is sending out from (may be hello same as hello receiving port), hello actual routed destination is in hello Target List field.</span></span>
  4. <span data-ttu-id="569f1-306">Redirección: esta sección explica el dispositivo virtual de Hola donde tooultimately redirigir este tráfico.</span><span class="sxs-lookup"><span data-stu-id="569f1-306">Redirection – this section tells hello virtual appliance where tooultimately redirect this traffic.</span></span> <span data-ttu-id="569f1-307">Hola la redirección más sencilla es tooplace Hola IP y puerto (opcional) en el campo de la lista de destinos de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-307">hello simplest redirection is tooplace hello IP and Port (optional) in hello Target List field.</span></span> <span data-ttu-id="569f1-308">Si ningún puerto es el puerto de destino de hello usado en la solicitud entrante de hello será usa (es decir, ninguna traducción), si no se designa un puerto de puerto de hello también será NAT junto con IP Hola se referiría.</span><span class="sxs-lookup"><span data-stu-id="569f1-308">If no port is used hello destination port on hello inbound request will be used (ie no translation), if a port is designated hello port will also be NAT’d along with hello IP address.</span></span>
     
     <span data-ttu-id="569f1-309">![Regla de RDP de firewall][11]</span><span class="sxs-lookup"><span data-stu-id="569f1-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="569f1-310">Un total de cuatro reglas RDP necesitará toobe creado:</span><span class="sxs-lookup"><span data-stu-id="569f1-310">A total of four RDP rules will need toobe created:</span></span> 
     
     | <span data-ttu-id="569f1-311">Nombre de la regla</span><span class="sxs-lookup"><span data-stu-id="569f1-311">Rule Name</span></span> | <span data-ttu-id="569f1-312">Server</span><span class="sxs-lookup"><span data-stu-id="569f1-312">Server</span></span> | <span data-ttu-id="569f1-313">Servicio</span><span class="sxs-lookup"><span data-stu-id="569f1-313">Service</span></span> | <span data-ttu-id="569f1-314">Lista de destinos</span><span class="sxs-lookup"><span data-stu-id="569f1-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="569f1-315">RDP a IIS01</span><span class="sxs-lookup"><span data-stu-id="569f1-315">RDP-to-IIS01</span></span> |<span data-ttu-id="569f1-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="569f1-316">IIS01</span></span> |<span data-ttu-id="569f1-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="569f1-317">IIS01 RDP</span></span> |<span data-ttu-id="569f1-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="569f1-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="569f1-319">RDP a DNS01</span><span class="sxs-lookup"><span data-stu-id="569f1-319">RDP-to-DNS01</span></span> |<span data-ttu-id="569f1-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="569f1-320">DNS01</span></span> |<span data-ttu-id="569f1-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="569f1-321">DNS01 RDP</span></span> |<span data-ttu-id="569f1-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="569f1-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="569f1-323">RDP a AppVM01</span><span class="sxs-lookup"><span data-stu-id="569f1-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="569f1-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="569f1-324">AppVM01</span></span> |<span data-ttu-id="569f1-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="569f1-325">AppVM01 RDP</span></span> |<span data-ttu-id="569f1-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="569f1-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="569f1-327">RDP a AppVM02</span><span class="sxs-lookup"><span data-stu-id="569f1-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="569f1-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="569f1-328">AppVM02</span></span> |<span data-ttu-id="569f1-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="569f1-329">AppVm02 RDP</span></span> |<span data-ttu-id="569f1-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="569f1-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="569f1-331">Restricción hacia abajo el ámbito de Hola de hello origen y campos de servicio se reducirá la superficie expuesta a ataques Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-331">Narrowing down hello scope of hello Source and Service fields will reduce hello attack surface.</span></span> <span data-ttu-id="569f1-332">ámbito de Hello más limitada que le permitirá funcionalidad debe utilizarse.</span><span class="sxs-lookup"><span data-stu-id="569f1-332">hello most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="569f1-333">**Las reglas de tráfico de aplicación**: hay dos reglas de tráfico de aplicaciones, Hola primero para el tráfico de web front-end de Hola y Hola en segundo lugar para el tráfico de back-end de hello (por ejemplo, la capa del toodata servidor web).</span><span class="sxs-lookup"><span data-stu-id="569f1-333">**Application Traffic Rules**: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="569f1-334">Estas reglas dependerá de arquitectura de red de hello (donde se colocan los servidores) y flujos de tráfico (el tráfico de Hola de qué dirección fluye y qué puertos se usan).</span><span class="sxs-lookup"><span data-stu-id="569f1-334">These rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="569f1-335">Se describe en primer lugar es la regla de front-end de hello para el tráfico web:</span><span class="sxs-lookup"><span data-stu-id="569f1-335">First discussed is hello front end rule for web traffic:</span></span>
  
    <span data-ttu-id="569f1-336">![Regla de Web de firewall][12]</span><span class="sxs-lookup"><span data-stu-id="569f1-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="569f1-337">Esta regla de NAT de destino permite que servidor de aplicaciones de hello aplicación real tráfico tooreach Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-337">This Destination NAT rule allows hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="569f1-338">Mientras hello otras reglas permiten para la seguridad, administración, etc., reglas de aplicación son los que permiten tooaccess de los usuarios o servicios externos Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="569f1-338">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="569f1-339">En este ejemplo, hay un único servidor web en el puerto 80, por lo tanto Hola única aplicación regla de firewall redirigirá el tráfico entrante toohello externo IP, dirección IP interna de servidores de web de toohello.</span><span class="sxs-lookup"><span data-stu-id="569f1-339">For this example, there is a single web server on port 80, thus hello single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span>
  
    <span data-ttu-id="569f1-340">**Tenga en cuenta**: que no hay ningún puerto asignado en el campo de la lista de destinos de Hola, por lo tanto hello entrante puerto 80 (o 443 para hello servicio seleccionado) se utilizará en la redirección de Hola Hola del servidor de web.</span><span class="sxs-lookup"><span data-stu-id="569f1-340">**Note**: that there is no port assigned in hello Target List field, thus hello inbound port 80 (or 443 for hello Service selected) will be used in hello redirection of hello web server.</span></span> <span data-ttu-id="569f1-341">Si el servidor web de hello está escuchando en un puerto diferente, por ejemplo, el puerto 8080, campo de la lista de destinos de hello podría ser tooallow too10.0.1.4:8080 actualizada para así la redirección de puertos de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-341">If hello web server is listening on a different port, for example port 8080, hello Target List field could be updated too10.0.1.4:8080 tooallow for hello Port redirection as well.</span></span>
  
    <span data-ttu-id="569f1-342">Hola es la siguiente regla de tráfico de aplicación Hola back-end regla tooallow hello Web tootalk toohello AppVM01 servidor (pero no AppVM02) a través de cualquier servicio:</span><span class="sxs-lookup"><span data-stu-id="569f1-342">hello next Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="569f1-343">![Regla de AppVM01 de firewall][13]</span><span class="sxs-lookup"><span data-stu-id="569f1-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="569f1-344">Esta regla de paso permite que cualquier servidor IIS en Hola de tooreach de subred de front-end de hello AppVM01 (dirección IP 10.0.2.5) en cualquier puerto, con los datos de tooaccess de protocolo necesarios para la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="569f1-344">This Pass rule allows any IIS server on hello Frontend subnet tooreach hello AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol tooaccess data needed by hello web application.</span></span>
  
    <span data-ttu-id="569f1-345">En esta captura de pantalla de un "\<explícita dest\>" se usa en toosignify de campo de destino de hello 10.0.2.5 como destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-345">In this screen shot an "\<explicit-dest\>" is used in hello Destination field toosignify 10.0.2.5 as hello destination.</span></span> <span data-ttu-id="569f1-346">Esto podría ser explícita denominada tal como se muestra, o un objeto de red (como ocurría en los requisitos previos de hello para el servidor DNS de hello).</span><span class="sxs-lookup"><span data-stu-id="569f1-346">This could be either explicit as shown or a named Network Object (as was done in hello prerequisites for hello DNS server).</span></span> <span data-ttu-id="569f1-347">Esto es toohello administrador del servidor de seguridad de hello ya se usará el método toowhich.</span><span class="sxs-lookup"><span data-stu-id="569f1-347">This is up toohello administrator of hello firewall as toowhich method will be used.</span></span> <span data-ttu-id="569f1-348">tooadd 10.0.2.5 como un Explict Desitnation, haga doble clic en la primera fila en blanco hello en \<explícita dest\> y escriba la dirección de hello en ventana hello que aparece.</span><span class="sxs-lookup"><span data-stu-id="569f1-348">tooadd 10.0.2.5 as an Explict Desitnation, double-click on hello first blank row under \<explicit-dest\> and enter hello address in hello window that pops up.</span></span>
  
    <span data-ttu-id="569f1-349">Con esta regla pasa, no se necesita ninguna NAT puesto que se trata el tráfico interno, por lo que Hola método de conexión puede establecerse demasiado "SNAT n".</span><span class="sxs-lookup"><span data-stu-id="569f1-349">With this Pass Rule, no NAT is needed since this is internal traffic, so hello Connection Method can be set too"No SNAT".</span></span>
  
    <span data-ttu-id="569f1-350">**Tenga en cuenta**: red de origen de hello en esta regla es cualquier recurso de subred de front-end de hello, si sólo habrá uno, o un número específico de servidores web, un objeto de red pudieron ser recursos creada toobe direcciones toothose IP exactas más específicas en lugar de subred de front-end de Hello completa.</span><span class="sxs-lookup"><span data-stu-id="569f1-350">**Note**: hello Source network in this rule is any resource on hello FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created toobe more specific toothose exact IP addresses instead of hello entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="569f1-351">Esta regla usa el servicio de Hola "Cualquiera" toomake toosetup más fácil de aplicación de ejemplo de Hola y usar, esto también le permitirá ICMPv4 (ping) en una sola regla.</span><span class="sxs-lookup"><span data-stu-id="569f1-351">This rule uses hello service “Any” toomake hello sample application easier toosetup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="569f1-352">Sin embargo, este no es el procedimiento recomendado.</span><span class="sxs-lookup"><span data-stu-id="569f1-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="569f1-353">Hola puertos y protocolos ("servicios") deben ser toohello limitados mínima posible que permite la superficie expuesta a ataques aplicación operación tooreduce Hola a través de este límite.</span><span class="sxs-lookup"><span data-stu-id="569f1-353">hello ports and protocols (“Services”) should be narrowed toohello minimum possible that allows application operation tooreduce hello attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="569f1-354">Aunque esta regla muestra una referencia explícita dest que se va a utilizar, debe utilizarse un enfoque coherente en toda la configuración del firewall Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout hello firewall configuration.</span></span> <span data-ttu-id="569f1-355">Se recomienda que Hola denominado objeto de red usarán en todo para facilitar la legibilidad y compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="569f1-355">It is recommended that hello named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="569f1-356">Hola explícita-dest es usado tooshow solo aquí un método alternativo de referencia y generalmente no se recomienda (especialmente en configuraciones complejas).</span><span class="sxs-lookup"><span data-stu-id="569f1-356">hello explicit-dest is used here only tooshow an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="569f1-357">**Regla de salida tooInternet**: pasar esta regla para permitir el tráfico de las redes de destino de origen red toopass toohello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="569f1-357">**Outbound tooInternet Rule**: This Pass rule will allow traffic from any Source network toopass toohello selected Destination networks.</span></span> <span data-ttu-id="569f1-358">Esta regla es una regla predeterminada ya vienen en firewall de Barracuda NextGen hello, pero está en un estado deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="569f1-358">This rule is a default rule usually already on hello Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="569f1-359">Haga doble clic en esta regla puede tener acceso a comandos de activar la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-359">Right-clicking on this rule can access hello Activate Rule command.</span></span> <span data-ttu-id="569f1-360">regla de Hola que se muestra aquí ha sido modificado tooadd Hola dos subredes locales que se crearon como referencias en la sección de requisitos previos de Hola de este atributo de origen de toohello de documento de esta regla.</span><span class="sxs-lookup"><span data-stu-id="569f1-360">hello rule shown here has been modified tooadd hello two local subnets that were created as references in hello prerequisite section of this document toohello Source attribute of this rule.</span></span>
  
    <span data-ttu-id="569f1-361">![Regla de salida de firewall][14]</span><span class="sxs-lookup"><span data-stu-id="569f1-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="569f1-362">**Regla de DNS**: pasar esta regla permite sólo DNS (el puerto 53) tráfico toopass toohello servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="569f1-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="569f1-363">Para este entorno que se bloquea la mayor parte del tráfico de hello front-end toohello back-end, esta regla permite específicamente DNS.</span><span class="sxs-lookup"><span data-stu-id="569f1-363">For this environment most traffic from hello FrontEnd toohello BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="569f1-364">![Regla de DNS de firewall][15]</span><span class="sxs-lookup"><span data-stu-id="569f1-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="569f1-365">**Tenga en cuenta**: en esta pantalla se incluye Hola instantánea método de conexión.</span><span class="sxs-lookup"><span data-stu-id="569f1-365">**Note**: In this screen shot hello Connection Method is included.</span></span> <span data-ttu-id="569f1-366">Dado que esta regla es para el tráfico interno de dirección IP de toointernal IP, no se requiere ninguna traducción, este Hola método de conexión se establece demasiado "No SNAT" para esta regla de paso.</span><span class="sxs-lookup"><span data-stu-id="569f1-366">Because this rule is for internal IP toointernal IP address traffic, no NATing is required, this hello Connection Method is set too“No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="569f1-367">**Subred tooSubnet regla**: pasar esta regla es una regla predeterminada que se ha activado y modificado tooallow cualquier servidor de hello volver Terminar server tooany de subred tooconnect en Hola subred de front-end.</span><span class="sxs-lookup"><span data-stu-id="569f1-367">**Subnet tooSubnet Rule**: This Pass rule is a default rule that has been activated and modified tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet.</span></span> <span data-ttu-id="569f1-368">Esta regla es el tráfico interno de todos los por lo que se puede establecer tooNo SNAT Hola método de conexión.</span><span class="sxs-lookup"><span data-stu-id="569f1-368">This rule is all internal traffic so hello Connection Method can be set tooNo SNAT.</span></span>
  
    <span data-ttu-id="569f1-369">![Regla entre redes virtuales de firewall][16]</span><span class="sxs-lookup"><span data-stu-id="569f1-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="569f1-370">**Tenga en cuenta**: Hola bidireccional casilla no está activada (ni está activada en la mayoría de las reglas), esto es significativo para esta regla ya que esto dificulta "uno direccional" de la regla, se puede iniciar una conexión de red de front-end del toohello Hola de subred de back-end, pero no Hola inversa.</span><span class="sxs-lookup"><span data-stu-id="569f1-370">**Note**: hello Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from hello back end subnet toohello front end network, but not hello reverse.</span></span> <span data-ttu-id="569f1-371">Si esa casilla se activa, esta regla permitiría el tráfico bidireccional lo que, desde la perspectiva de nuestro diagrama lógico, no es deseable.</span><span class="sxs-lookup"><span data-stu-id="569f1-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="569f1-372">**Denegar todas las reglas de tráfico**: siempre debería ser regla final de hello (en términos de prioridad) y, como por ejemplo, si un tráfico fluye se produce un error toomatch cualquiera de hello anterior reglas se eliminarán por esta regla.</span><span class="sxs-lookup"><span data-stu-id="569f1-372">**Deny All Traffic Rule**: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="569f1-373">Esta es una regla predeterminada y normalmente está activada; normalmente no se necesitan modificaciones.</span><span class="sxs-lookup"><span data-stu-id="569f1-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="569f1-374">![Regla de denegación de firewall][17]</span><span class="sxs-lookup"><span data-stu-id="569f1-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="569f1-375">Una vez que se crean todos Hola por encima de las reglas, es importante tooreview prioridad Hola el tráfico de tooensure de cada regla se permitirá o denegará según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="569f1-375">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="569f1-376">En este ejemplo, reglas de Hola están en orden de hello deben aparecer en hello cuadrícula principal de las reglas en hello Barracuda Management Client de reenvío.</span><span class="sxs-lookup"><span data-stu-id="569f1-376">For this example, hello rules are in hello order they should appear in hello Main Grid of forwarding rules in hello Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="569f1-377">Activación de reglas</span><span class="sxs-lookup"><span data-stu-id="569f1-377">Rule Activation</span></span>
<span data-ttu-id="569f1-378">Hola ruleset que se modificó la especificación de toohello de diagrama de la lógica de hello, debe ser Hola ruleset cargado toohello firewall y, a continuación, se activa.</span><span class="sxs-lookup"><span data-stu-id="569f1-378">With hello ruleset modified toohello specification of hello logic diagram, hello ruleset must be uploaded toohello firewall and then activated.</span></span>

<span data-ttu-id="569f1-379">![Activación de reglas de firewall][18]</span><span class="sxs-lookup"><span data-stu-id="569f1-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="569f1-380">En la esquina superior derecha de Hola de cliente de administración de hello son un clúster de botones.</span><span class="sxs-lookup"><span data-stu-id="569f1-380">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="569f1-381">Haga clic en firewall de Hola "enviar cambios" botón toosend Hola modificar reglas toohello, a continuación, haga clic en el botón de "Activar" Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-381">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="569f1-382">Con la activación de Hola de conjunto de reglas de firewall de hello esta compilación de entorno de ejemplo está completa.</span><span class="sxs-lookup"><span data-stu-id="569f1-382">With hello activation of hello firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="569f1-383">Escenarios de tráfico</span><span class="sxs-lookup"><span data-stu-id="569f1-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="569f1-384">Una clave takeway es tooremember que **todos los** tráfico procederá a través de firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-384">A key takeway is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="569f1-385">Toohello de escritorio tooremote por lo que el servidor IIS01, aunque se encuentre en el servicio de nube de Front-End de Hola y de subred de Front-End de hello, tooaccess este servidor se va a necesitar tooRDP toohello firewall en 8014 de puerto y, a continuación, Permitir solicitud RDP de hello firewall tooroute Hola internamente toohello IIS01 el puerto de RDP.</span><span class="sxs-lookup"><span data-stu-id="569f1-385">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="569f1-386">Hola "Conectar" del portal de Azure botón no funcionará porque no hay ningún tooIIS01 de ruta de acceso directo de RDP (lo que puede ver el portal de hello).</span><span class="sxs-lookup"><span data-stu-id="569f1-386">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="569f1-387">Esto significa que todas las conexiones desde Hola internet estarán toohello servicio de seguridad y un puerto, por ejemplo, secscv001.cloudapp.net:xxxx.</span><span class="sxs-lookup"><span data-stu-id="569f1-387">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="569f1-388">Para estos escenarios, debe ser Hola siguiendo las reglas de firewall en su lugar:</span><span class="sxs-lookup"><span data-stu-id="569f1-388">For these scenarios, hello following firewall rules should be in place:</span></span>

1. <span data-ttu-id="569f1-389">Administración del firewall</span><span class="sxs-lookup"><span data-stu-id="569f1-389">Firewall Management</span></span>
2. <span data-ttu-id="569f1-390">TooIIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="569f1-390">RDP tooIIS01</span></span>
3. <span data-ttu-id="569f1-391">TooDNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="569f1-391">RDP tooDNS01</span></span>
4. <span data-ttu-id="569f1-392">TooAppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="569f1-392">RDP tooAppVM01</span></span>
5. <span data-ttu-id="569f1-393">TooAppVM02 RDP</span><span class="sxs-lookup"><span data-stu-id="569f1-393">RDP tooAppVM02</span></span>
6. <span data-ttu-id="569f1-394">Toohello de tráfico de la aplicación Web</span><span class="sxs-lookup"><span data-stu-id="569f1-394">App Traffic toohello Web</span></span>
7. <span data-ttu-id="569f1-395">Tráfico de aplicación tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="569f1-395">App Traffic tooAppVM01</span></span>
8. <span data-ttu-id="569f1-396">Salida toohello Internet</span><span class="sxs-lookup"><span data-stu-id="569f1-396">Outbound toohello Internet</span></span>
9. <span data-ttu-id="569f1-397">TooDNS01 de front-end</span><span class="sxs-lookup"><span data-stu-id="569f1-397">Frontend tooDNS01</span></span>
10. <span data-ttu-id="569f1-398">Tráfico de subredes intra (back-end toofront final solamente)</span><span class="sxs-lookup"><span data-stu-id="569f1-398">Intra-Subnet Traffic (back end toofront end only)</span></span>
11. <span data-ttu-id="569f1-399">Denegar todo</span><span class="sxs-lookup"><span data-stu-id="569f1-399">Deny All</span></span>

<span data-ttu-id="569f1-400">conjunto de reglas de firewall real Hola probablemente tendrá muchas otras reglas en toothese adición, reglas de Hola en cualquier servidor de seguridad determinado también tendrá números de prioridad diferentes de los que se enumeran aquí Hola a.</span><span class="sxs-lookup"><span data-stu-id="569f1-400">hello actual firewall ruleset will most likely have many other rules in addition toothese, hello rules on any given firewall will also have different priority numbers than hello ones listed here.</span></span> <span data-ttu-id="569f1-401">Esta lista y números asociados son tooprovide relevancia entre simplemente estas once reglas y la prioridad relativa de hello entre ellos.</span><span class="sxs-lookup"><span data-stu-id="569f1-401">This list and associated numbers are tooprovide relevance between just these eleven rules and hello relative priority amongst them.</span></span> <span data-ttu-id="569f1-402">En otras palabras; en firewall de hello real, Hola "RDP tooIIS01" puede ser el número de regla 5, pero mientras está por debajo de la regla de "Administración de Firewall" hello y versiones posteriores de la regla de "RDP tooDNS01" hello podrían alinearse con intención de Hola de esta lista.</span><span class="sxs-lookup"><span data-stu-id="569f1-402">In other words; on hello actual firewall, hello “RDP tooIIS01” may be rule number 5, but as long as it’s below hello “Firewall Management” rule and above hello “RDP tooDNS01” rule it would align with hello intention of this list.</span></span> <span data-ttu-id="569f1-403">También le ayudará a lista de Hola Hola escenarios permitiendo brevedad; p. ej. “Regla de reenvío 9 (DNS)”.</span><span class="sxs-lookup"><span data-stu-id="569f1-403">hello list will also aid in hello below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="569f1-404">Para mayor brevedad, Hola cuatro reglas RDP será colectivamente el acrónimo, "Hola reglas RDP" al escenario de tráfico de hello es tooRDP no relacionado.</span><span class="sxs-lookup"><span data-stu-id="569f1-404">Also for brevity, hello four RDP rules will be collectively called, “hello RDP rules” when hello traffic scenario is unrelated tooRDP.</span></span>

<span data-ttu-id="569f1-405">Recuerde también que los grupos de seguridad de red están vigentes para el tráfico entrante de internet en hello front-end y back-end subredes.</span><span class="sxs-lookup"><span data-stu-id="569f1-405">Also recall that Network Security Groups are in-place for inbound internet traffic on hello Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="569f1-406">(Permitido) Internet tooWeb Server</span><span class="sxs-lookup"><span data-stu-id="569f1-406">(Allowed) Internet tooWeb Server</span></span>
1. <span data-ttu-id="569f1-407">El usuario de Internet solicita la página HTTP desde SecSvc001.CloudApp.Net (servicio en la nube accesible desde Internet).</span><span class="sxs-lookup"><span data-stu-id="569f1-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="569f1-408">Fases de tráfico del servicio de nube a través de un extremo abierto en la interfaz de toofirewall del puerto 80 en 10.0.0.4:80</span><span class="sxs-lookup"><span data-stu-id="569f1-408">Cloud service passes traffic through open endpoint on port 80 toofirewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="569f1-409">No hay NSG asignada subred tooSecurity, de modo que las reglas NSG de sistema permitir el tráfico toofirewall</span><span class="sxs-lookup"><span data-stu-id="569f1-409">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="569f1-410">Tráfico llega a dirección IP interna del servidor de seguridad de hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="569f1-410">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="569f1-411">El firewall comienza el procesamiento de las reglas:</span><span class="sxs-lookup"><span data-stu-id="569f1-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="569f1-412">No se aplican, mover toonext regla FW regla 1 (FW Mgmt)</span><span class="sxs-lookup"><span data-stu-id="569f1-412">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="569f1-413">Reglas de Firewall 2 y 5 (reglas de RDP) no se aplican, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="569f1-414">FW regla 6 (aplicación: Web) aplican, se permite el tráfico, firewall NAT too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="569f1-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it too10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="569f1-415">subred de front-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="569f1-415">hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="569f1-416">NSG de la regla 1 (bloque de Internet) no se aplica (este tráfico fue NAT estuviera firewall hello, por tanto, la dirección de origen de hello ahora es firewall de Hola que se encuentra en la subred de seguridad de Hola y visto por subred de front-end de hello tráfico NSG toobe "local" y, por tanto, se permite), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Frontend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="569f1-417">Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG</span><span class="sxs-lookup"><span data-stu-id="569f1-417">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="569f1-418">Iis01 escucha el tráfico de web, recibe esta solicitud y comienza a procesar la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-418">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
8. <span data-ttu-id="569f1-419">Iis01 intenta tooinitiates un tooAppVM01 de sesión FTP en la subred de back-end</span><span class="sxs-lookup"><span data-stu-id="569f1-419">IIS01 attempts tooinitiates an FTP session tooAppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="569f1-420">ruta UDR Hola de subred de front-end hace Hola firewall Hola de próximo salto</span><span class="sxs-lookup"><span data-stu-id="569f1-420">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
10. <span data-ttu-id="569f1-421">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="569f1-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="569f1-422">El firewall comienza el procesamiento de las reglas:</span><span class="sxs-lookup"><span data-stu-id="569f1-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="569f1-423">No se aplican, mover toonext regla FW regla 1 (FW Mgmt)</span><span class="sxs-lookup"><span data-stu-id="569f1-423">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="569f1-424">No se aplican reglas FW 2 y 5 (reglas de RDP), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="569f1-425">FW regla 6 (aplicación: Web) no se aplican, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-425">FW Rule 6 (App: Web) doesn’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="569f1-426">7 de la regla de FW (aplicación: back-end) se aplican, se permite el tráfico, firewall reenvía el tráfico too10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="569f1-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic too10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="569f1-427">subred de back-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="569f1-427">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="569f1-428">Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-428">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="569f1-429">Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG</span><span class="sxs-lookup"><span data-stu-id="569f1-429">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="569f1-430">AppVM01 recibe la solicitud de Hola e inicia la sesión de Hola y responde</span><span class="sxs-lookup"><span data-stu-id="569f1-430">AppVM01 receives hello request and initiates hello session and responds</span></span>
14. <span data-ttu-id="569f1-431">ruta UDR Hola de subred de back-end hace Hola firewall Hola de próximo salto</span><span class="sxs-lookup"><span data-stu-id="569f1-431">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
15. <span data-ttu-id="569f1-432">Puesto que no hay ninguna regla NSG saliente en hello respuesta de Hola de subred de back-end se permite</span><span class="sxs-lookup"><span data-stu-id="569f1-432">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
16. <span data-ttu-id="569f1-433">Dado que esto está devolviendo el tráfico en una sesión establecida Hola del firewall pasa servidor web de toohello de espera de respuesta hello (IIS01)</span><span class="sxs-lookup"><span data-stu-id="569f1-433">Because this is returning traffic on an established session hello firewall passes hello response back toohello web server (IIS01)</span></span>
17. <span data-ttu-id="569f1-434">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="569f1-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="569f1-435">Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-435">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="569f1-436">Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG</span><span class="sxs-lookup"><span data-stu-id="569f1-436">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="569f1-437">servidor IIS de Hola recibe respuesta Hola, completa la transacción de hello con AppVM01 y, a continuación, complete creación Hola respuesta HTTP, esta respuesta HTTP se envía toohello solicitante</span><span class="sxs-lookup"><span data-stu-id="569f1-437">hello IIS server receives hello response, completes hello transaction with AppVM01, and then completes building hello HTTP response, this HTTP response is sent toohello requestor</span></span>
19. <span data-ttu-id="569f1-438">Puesto que no hay ninguna regla NSG saliente en hello respuesta de Hola de subred de front-end está permitido</span><span class="sxs-lookup"><span data-stu-id="569f1-438">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
20. <span data-ttu-id="569f1-439">Hola firewall de Hola de aciertos de respuesta HTTP y porque se trata de hello respuesta tooan establecido sesión NAT se acepta por firewall de Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-439">hello HTTP response hits hello firewall, and because this is hello response tooan established NAT session is accepted by hello firewall</span></span>
21. <span data-ttu-id="569f1-440">firewall de Hello, a continuación, redirige Hola respuesta atrás toohello usuario de Internet</span><span class="sxs-lookup"><span data-stu-id="569f1-440">hello firewall then redirects hello response back toohello Internet User</span></span>
22. <span data-ttu-id="569f1-441">Puesto que no existen reglas de NSG salida ni saltos UDR de subred de front-end de Hola se permita la respuesta de Hola y Hola usuario de Internet recibe hello web página solicitada.</span><span class="sxs-lookup"><span data-stu-id="569f1-441">Since there are no outbound NSG rules or UDR hops on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-internet-rdp-toobackend"></a><span data-ttu-id="569f1-442">(Permitido) TooBackend de RDP de Internet</span><span class="sxs-lookup"><span data-stu-id="569f1-442">(Allowed) Internet RDP tooBackend</span></span>
1. <span data-ttu-id="569f1-443">Administrador del servidor en internet solicita tooAppVM01 de sesión RDP mediante SecSvc001.CloudApp.Net:8025, donde 8025 es número de puerto asignados al usuario de Hola de regla de firewall "RDP tooAppVM01" hello</span><span class="sxs-lookup"><span data-stu-id="569f1-443">Server Admin on internet requests RDP session tooAppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is hello user assigned port number for hello “RDP tooAppVM01” firewall rule</span></span>
2. <span data-ttu-id="569f1-444">servicio de nube de Hello pasa el tráfico a través del extremo abierto de hello en interfaz del puerto 8025 toofirewall 10.0.0.4:8025</span><span class="sxs-lookup"><span data-stu-id="569f1-444">hello cloud service passes traffic through hello open endpoint on port 8025 toofirewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="569f1-445">No hay NSG asignada subred tooSecurity, de modo que las reglas NSG de sistema permitir el tráfico toofirewall</span><span class="sxs-lookup"><span data-stu-id="569f1-445">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="569f1-446">El firewall comienza el procesamiento de las reglas:</span><span class="sxs-lookup"><span data-stu-id="569f1-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="569f1-447">No se aplican, mover toonext regla FW regla 1 (FW Mgmt)</span><span class="sxs-lookup"><span data-stu-id="569f1-447">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="569f1-448">No se aplica la regla FW 2 (RDP IIS), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-448">FW Rule 2 (RDP IIS) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="569f1-449">No se aplica la regla FW 3 (RDP DNS01), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-449">FW Rule 3 (RDP DNS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="569f1-450">Aplicar regla fw4 (RDP AppVM01), se permite el tráfico, firewall NAT se too10.0.2.5:3386 (puerto de RDP en AppVM01)</span><span class="sxs-lookup"><span data-stu-id="569f1-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it too10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="569f1-451">subred de back-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="569f1-451">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="569f1-452">NSG de la regla 1 (bloque de Internet) no se aplica (este tráfico fue NAT estuviera firewall hello, por tanto, la dirección de origen de hello ahora es firewall de Hola que se encuentra en la subred de seguridad de Hola y visto por subred de back-end de hello tráfico NSG toobe "local" y, por tanto, se permite), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Backend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="569f1-453">Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG</span><span class="sxs-lookup"><span data-stu-id="569f1-453">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="569f1-454">AppVM01 escucha el tráfico RDP y responde.</span><span class="sxs-lookup"><span data-stu-id="569f1-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="569f1-455">No hay reglas de grupo de seguridad de red de salida, se aplican las reglas predeterminadas y se permite el tráfico de retorno.</span><span class="sxs-lookup"><span data-stu-id="569f1-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="569f1-456">UDR enruta el tráfico saliente toohello firewall salto siguiente Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-456">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
9. <span data-ttu-id="569f1-457">Porque esto está devolviendo el tráfico en una sesión establecida Hola del firewall pasa usuario de internet de hello respuesta toohello atrás</span><span class="sxs-lookup"><span data-stu-id="569f1-457">Because this is returning traffic on an established session hello firewall passes hello response back toohello internet user</span></span>
10. <span data-ttu-id="569f1-458">La sesión RDP está habilitada.</span><span class="sxs-lookup"><span data-stu-id="569f1-458">RDP session is enabled</span></span>
11. <span data-ttu-id="569f1-459">AppVM01 solicita la contraseña del nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="569f1-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="569f1-460">(Permitido) Búsqueda de DNS del servidor web en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="569f1-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="569f1-461">Web necesidades de servidor, IIS01, fuente de distribución de datos en www.data.gov, pero necesita tooresolve Hola dirección.</span><span class="sxs-lookup"><span data-stu-id="569f1-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="569f1-462">Hola configuración de red para las listas de red virtual de hello DNS01 (10.0.2.4 de subred de back-end de hello) como servidor DNS principal de hello, IIS01 envía Hola DNS solicitud tooDNS01</span><span class="sxs-lookup"><span data-stu-id="569f1-462">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="569f1-463">UDR enruta el tráfico saliente toohello firewall salto siguiente Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-463">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
4. <span data-ttu-id="569f1-464">Ninguna regla NSG saliente está enlazado toohello subred de front-end, se permite el tráfico</span><span class="sxs-lookup"><span data-stu-id="569f1-464">No outbound NSG rules are bound toohello Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="569f1-465">El firewall comienza el procesamiento de las reglas:</span><span class="sxs-lookup"><span data-stu-id="569f1-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="569f1-466">No se aplican, mover toonext regla FW regla 1 (FW Mgmt)</span><span class="sxs-lookup"><span data-stu-id="569f1-466">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="569f1-467">No se aplican reglas FW 2 y 5 (reglas de RDP), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="569f1-468">No se aplicará la FW reglas 6 y 7 (reglas de aplicaciones), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-468">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="569f1-469">No se aplican, mover toonext regla FW regla 8 (tooInternet)</span><span class="sxs-lookup"><span data-stu-id="569f1-469">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="569f1-470">Aplicar FW regla 9 (DNS), se permite el tráfico, firewall reenvía el tráfico too10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="569f1-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic too10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="569f1-471">subred de back-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="569f1-471">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="569f1-472">Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-472">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="569f1-473">Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG</span><span class="sxs-lookup"><span data-stu-id="569f1-473">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="569f1-474">Servidor DNS recibe la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-474">DNS server receives hello request</span></span>
8. <span data-ttu-id="569f1-475">Servidor DNS no tiene dirección de hello en caché y pide un servidor DNS raíz en hello internet</span><span class="sxs-lookup"><span data-stu-id="569f1-475">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
9. <span data-ttu-id="569f1-476">UDR enruta el tráfico saliente toohello firewall salto siguiente Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-476">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
10. <span data-ttu-id="569f1-477">No hay reglas de grupo de seguridad de red de salida en la subred back-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="569f1-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="569f1-478">El firewall comienza el procesamiento de las reglas:</span><span class="sxs-lookup"><span data-stu-id="569f1-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="569f1-479">No se aplican, mover toonext regla FW regla 1 (FW Mgmt)</span><span class="sxs-lookup"><span data-stu-id="569f1-479">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="569f1-480">No se aplican reglas FW 2 y 5 (reglas de RDP), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="569f1-481">No se aplicará la FW reglas 6 y 7 (reglas de aplicaciones), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-481">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="569f1-482">Aplicar reglas de FW 8 (tooInternet), se permite el tráfico, sesión es SNAT out tooroot servidor DNS en Internet de Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-482">FW Rule 8 (tooInternet) does apply, traffic is allowed, session is SNAT out tooroot DNS server on hello Internet</span></span>
12. <span data-ttu-id="569f1-483">Responde el servidor DNS de Internet, ya que esta sesión se inició en firewall de hello, respuesta de hello acepta firewall Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-483">Internet DNS server responds, since this session was initiated from hello firewall, hello response is accepted by hello firewall</span></span>
13. <span data-ttu-id="569f1-484">Tal y como se trata de una sesión establecida, firewall de hello reenvía Hola respuesta toohello iniciar el servidor, DNS01</span><span class="sxs-lookup"><span data-stu-id="569f1-484">As this is an established session, hello firewall forwards hello response toohello initiating server, DNS01</span></span>
14. <span data-ttu-id="569f1-485">subred de back-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="569f1-485">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="569f1-486">Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-486">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="569f1-487">Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG</span><span class="sxs-lookup"><span data-stu-id="569f1-487">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="569f1-488">servidor DNS de Hello recibe y almacena en caché la respuesta de hello y, a continuación, responde tooIIS01 de espera de solicitud inicial toohello</span><span class="sxs-lookup"><span data-stu-id="569f1-488">hello DNS server receives and caches hello response, and then responds toohello initial request back tooIIS01</span></span>
16. <span data-ttu-id="569f1-489">ruta UDR Hola de subred de back-end hace Hola firewall Hola de próximo salto</span><span class="sxs-lookup"><span data-stu-id="569f1-489">hello UDR route on backend subnet makes hello firewall hello next hop</span></span>
17. <span data-ttu-id="569f1-490">No existe ninguna regla NSG saliente en la subred de back-end de hello, se permite el tráfico</span><span class="sxs-lookup"><span data-stu-id="569f1-490">No outbound NSG rules exist on hello Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="569f1-491">Se trata de una sesión establecida en firewall de hello, respuesta de Hola se reenvía por servidor IIS de hello firewall back-toohello</span><span class="sxs-lookup"><span data-stu-id="569f1-491">This is an established session on hello firewall, hello response is forwarded by hello firewall back toohello IIS server</span></span>
19. <span data-ttu-id="569f1-492">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="569f1-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="569f1-493">No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-493">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="569f1-494">Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico por lo que se permite el tráfico de Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-494">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
20. <span data-ttu-id="569f1-495">Iis01 recibe respuesta hello DNS01</span><span class="sxs-lookup"><span data-stu-id="569f1-495">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-backend-server-toofrontend-server"></a><span data-ttu-id="569f1-496">(Permitido) Servidor de tooFrontend de servidor back-end</span><span class="sxs-lookup"><span data-stu-id="569f1-496">(Allowed) Backend server tooFrontend server</span></span>
1. <span data-ttu-id="569f1-497">Un administrador ha iniciado sesión tooAppVM02 a través de RDP solicita un archivo directamente desde el servidor de IIS01 Hola a través del explorador de archivos de windows</span><span class="sxs-lookup"><span data-stu-id="569f1-497">An administrator logged on tooAppVM02 via RDP requests a file directly from hello IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="569f1-498">ruta UDR Hola de subred de back-end hace Hola firewall Hola de próximo salto</span><span class="sxs-lookup"><span data-stu-id="569f1-498">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
3. <span data-ttu-id="569f1-499">Puesto que no hay ninguna regla NSG saliente en hello respuesta de Hola de subred de back-end se permite</span><span class="sxs-lookup"><span data-stu-id="569f1-499">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
4. <span data-ttu-id="569f1-500">El firewall comienza el procesamiento de las reglas:</span><span class="sxs-lookup"><span data-stu-id="569f1-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="569f1-501">No se aplican, mover toonext regla FW regla 1 (FW Mgmt)</span><span class="sxs-lookup"><span data-stu-id="569f1-501">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="569f1-502">No se aplican reglas FW 2 y 5 (reglas de RDP), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="569f1-503">No se aplicará la FW reglas 6 y 7 (reglas de aplicaciones), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-503">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="569f1-504">No se aplican, mover toonext regla FW regla 8 (tooInternet)</span><span class="sxs-lookup"><span data-stu-id="569f1-504">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="569f1-505">No se aplica FW regla 9 (DNS), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-505">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="569f1-506">Aplicar FW regla 10 (Intra-subred), se permite el tráfico, firewall pasa el tráfico too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="569f1-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic too10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="569f1-507">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="569f1-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="569f1-508">Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-508">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="569f1-509">Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG</span><span class="sxs-lookup"><span data-stu-id="569f1-509">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="569f1-510">Suponiendo que autorización y la autenticación correcta, IIS01 acepta la solicitud de Hola y responde</span><span class="sxs-lookup"><span data-stu-id="569f1-510">Assuming proper authentication and authorization, IIS01 accepts hello request and responds</span></span>
7. <span data-ttu-id="569f1-511">ruta UDR Hola de subred de front-end hace Hola firewall Hola de próximo salto</span><span class="sxs-lookup"><span data-stu-id="569f1-511">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
8. <span data-ttu-id="569f1-512">Puesto que no hay ninguna regla NSG saliente en hello respuesta de Hola de subred de front-end está permitido</span><span class="sxs-lookup"><span data-stu-id="569f1-512">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
9. <span data-ttu-id="569f1-513">Tal y como se trata de una sesión existente en firewall de Hola se permita esta respuesta y firewall de hello devuelve Hola respuesta tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="569f1-513">As this is an existing session on hello firewall this response is allowed and hello firewall returns hello response tooAppVM02</span></span>
10. <span data-ttu-id="569f1-514">La subred back-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="569f1-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="569f1-515">Regla de NSG 1 (bloque de Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-515">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="569f1-516">Reglas de NSG predeterminada permitir el tráfico de toosubnet de subred, se permite el tráfico, detenga el procesamiento de la regla NSG</span><span class="sxs-lookup"><span data-stu-id="569f1-516">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="569f1-517">AppVM02 recibe respuesta Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-517">AppVM02 receives hello response</span></span>

#### <a name="denied-internet-direct-tooweb-server"></a><span data-ttu-id="569f1-518">(Denegado) TooWeb directo de Internet Server</span><span class="sxs-lookup"><span data-stu-id="569f1-518">(Denied) Internet direct tooWeb Server</span></span>
1. <span data-ttu-id="569f1-519">Usuario de Internet intenta tooaccess Hola servidor web, IIS01, a través de hello FrontEnd001.CloudApp.Net servicio</span><span class="sxs-lookup"><span data-stu-id="569f1-519">Internet user tries tooaccess hello web server, IIS01, through hello FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="569f1-520">Puesto que no hay ningún extremo abierto para el tráfico HTTP, esto no pasará a través de hello servicio en la nube y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="569f1-520">Since there are no endpoints open for HTTP traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="569f1-521">Si los puntos de conexión de hello estaban abiertos por algún motivo, hello NSG (bloque de Internet) en la subred de front-end de hello bloquearían este tráfico</span><span class="sxs-lookup"><span data-stu-id="569f1-521">If hello endpoints were open for some reason, hello NSG (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="569f1-522">Por último, ruta de UDR de subred de front-end de hello enviaría todo el tráfico saliente desde IIS01 toohello firewall como próximo salto de hello, firewall de hello sería y aparecen como tráfico asimétrico Quitar respuesta de salida de hello por lo tanto hay al menos tres capas independientes de defensa entre hello IIS01 e internet a través de su servicio de nube impedir el acceso no autorizado o inadecuado.</span><span class="sxs-lookup"><span data-stu-id="569f1-522">Finally, hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toobackend-server"></a><span data-ttu-id="569f1-523">(Denegado) Internet tooBackend Server</span><span class="sxs-lookup"><span data-stu-id="569f1-523">(Denied) Internet tooBackend Server</span></span>
1. <span data-ttu-id="569f1-524">Usuario de Internet intenta tooaccess un archivo en AppVM01 a través de hello BackEnd001.CloudApp.Net servicio</span><span class="sxs-lookup"><span data-stu-id="569f1-524">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="569f1-525">Dado que no hay ningún extremo abierto para el recurso compartido de archivos, esto no sucedería Hola servicio en la nube y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="569f1-525">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="569f1-526">Si los puntos de conexión de hello estaban abiertos por algún motivo, hello NSG (bloque de Internet) bloquearían este tráfico</span><span class="sxs-lookup"><span data-stu-id="569f1-526">If hello endpoints were open for some reason, hello NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="569f1-527">Por último, ruta de hello UDR enviaría todo el tráfico saliente desde AppVM01 toohello firewall como próximo salto de hello, firewall de hello sería y aparecen como tráfico asimétrico Quitar respuesta de salida de hello por lo tanto hay al menos tres capas independientes de defensa entre Hola AppVM01 e internet a través de su servicio de nube impedir el acceso no autorizado o inadecuado.</span><span class="sxs-lookup"><span data-stu-id="569f1-527">Finally, hello UDR route would send any outbound traffic from AppVM01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-toobackend-server"></a><span data-ttu-id="569f1-528">(Denegado) Front-end server tooBackend Server</span><span class="sxs-lookup"><span data-stu-id="569f1-528">(Denied) Frontend server tooBackend Server</span></span>
1. <span data-ttu-id="569f1-529">Se supone IIS01 se pone en peligro y se ejecuta el código malintencionado intente servidores de subred de back-end de tooscan Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-529">Assume IIS01 was compromised and is running malicious code trying tooscan hello Backend subnet servers.</span></span>
2. <span data-ttu-id="569f1-530">ruta de UDR de subred de front-end de Hello enviaría todo el tráfico saliente desde IIS01 toohello firewall salto siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-530">hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop.</span></span> <span data-ttu-id="569f1-531">Esto no es algo que puede ser modificado por hello en peligro la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="569f1-531">This is not something that can be altered by hello compromised VM.</span></span>
3. <span data-ttu-id="569f1-532">firewall de Hello procesaría tráfico hello, si se ha de solicitud de hello tooAppVM01 o servidor DNS de toohello para las búsquedas DNS que potencialmente se permite el tráfico por firewall de hello (vence tooFW reglas 7 y 9).</span><span class="sxs-lookup"><span data-stu-id="569f1-532">hello firewall would process hello traffic, if hello request was tooAppVM01, or toohello DNS server for DNS lookups that traffic could potentially be allowed by hello firewall (due tooFW Rules 7 and 9).</span></span> <span data-ttu-id="569f1-533">La regla de reenvío 11 bloquearía todo el tráfico restante (denegar todo).</span><span class="sxs-lookup"><span data-stu-id="569f1-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="569f1-534">Si la detección de amenazas avanzada se habilitó en firewall de hello (que no se trata en este documento, consulte Hola documentación del fabricante de su dispositivo de red específicas amenaza capacidades avanzadas), incluso el tráfico que se permitan hello básico de reglas de reenvío se describe en este documento puede evitarse si el tráfico de hello contenía firmas conocidas o patrones que se marca una regla avanzada amenaza.</span><span class="sxs-lookup"><span data-stu-id="569f1-534">If advanced threat detection was enabled on hello firewall (which is not covered in this document, see hello vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by hello basic forwarding rules discussed in this document could be prevented if hello traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="569f1-535">(Denegado) Búsqueda de DNS de Internet en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="569f1-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="569f1-536">Usuario de Internet intenta toolookup un registro DNS interno en DNS01 a través del servicio BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="569f1-536">Internet user tries toolookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="569f1-537">Dado que no hay ningún extremo abierto para el tráfico DNS, esto no pasará a través de hello servicio en la nube y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="569f1-537">Since there are no endpoints open for DNS traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="569f1-538">Si los puntos de conexión de hello estaban abiertos por algún motivo, la regla de NSG de hello (bloque de Internet) en la subred de front-end de hello bloquearían este tráfico</span><span class="sxs-lookup"><span data-stu-id="569f1-538">If hello endpoints were open for some reason, hello NSG rule (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="569f1-539">Por último, ruta UDR de subred de back-end de hello enviaría todo el tráfico saliente desde DNS01 toohello firewall como próximo salto de hello, firewall de hello sería y aparecen como tráfico asimétrico Quitar respuesta de salida de hello por lo tanto hay al menos tres capas independientes de defensa entre hello DNS01 e internet a través de su servicio de nube impedir el acceso no autorizado o inadecuado.</span><span class="sxs-lookup"><span data-stu-id="569f1-539">Finally, hello Backend subnet UDR route would send any outbound traffic from DNS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toosql-access-through-firewall"></a><span data-ttu-id="569f1-540">(Denegado) Acceso a tooSQL de Internet a través del Firewall</span><span class="sxs-lookup"><span data-stu-id="569f1-540">(Denied) Internet tooSQL access through Firewall</span></span>
1. <span data-ttu-id="569f1-541">El usuario de Internet solicita datos SQL desde SecSvc001.CloudApp.Net (servicio en la nube accesible desde Internet).</span><span class="sxs-lookup"><span data-stu-id="569f1-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="569f1-542">Dado que no hay ningún extremo abierto para SQL, esto no sucedería Hola servicio en la nube y no llegar a firewall de Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-542">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="569f1-543">Si los puntos de conexión SQL estaban abiertos por algún motivo, firewall de hello comenzaría procesamiento de reglas:</span><span class="sxs-lookup"><span data-stu-id="569f1-543">If SQL endpoints were open for some reason, hello firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="569f1-544">No se aplican, mover toonext regla FW regla 1 (FW Mgmt)</span><span class="sxs-lookup"><span data-stu-id="569f1-544">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="569f1-545">Reglas de Firewall 2 y 5 (reglas de RDP) no se aplican, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="569f1-546">No se aplicará la FW regla 6 y 7 (reglas de aplicación), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-546">FW Rule 6 & 7 (Application Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="569f1-547">No se aplican, mover toonext regla FW regla 8 (tooInternet)</span><span class="sxs-lookup"><span data-stu-id="569f1-547">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="569f1-548">No se aplica FW regla 9 (DNS), mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="569f1-548">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="569f1-549">No se aplican, mover toonext regla FW regla 10 (Intra-subred)</span><span class="sxs-lookup"><span data-stu-id="569f1-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move toonext rule</span></span>
   7. <span data-ttu-id="569f1-550">Se aplica la regla de reenvío 11 (denegar todo), se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="569f1-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="569f1-551">Referencias</span><span class="sxs-lookup"><span data-stu-id="569f1-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="569f1-552">Script principal y configuración de red</span><span class="sxs-lookup"><span data-stu-id="569f1-552">Main Script and Network Config</span></span>
<span data-ttu-id="569f1-553">Guardar Hola Script completo en un archivo de script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="569f1-553">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="569f1-554">Guardar configuración de red de hello en un archivo denominado "NetworkConf2.xml".</span><span class="sxs-lookup"><span data-stu-id="569f1-554">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="569f1-555">Modifique las variables definidas por el usuario de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="569f1-555">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="569f1-556">Ejecutar script de Hola, a continuación, siga anterior de instrucciones de instalación del regla de Firewall Hola.</span><span class="sxs-lookup"><span data-stu-id="569f1-556">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="569f1-557">Script completo</span><span class="sxs-lookup"><span data-stu-id="569f1-557">Full Script</span></span>
<span data-ttu-id="569f1-558">Este script superará en función de las variables definidas por el usuario de hello:</span><span class="sxs-lookup"><span data-stu-id="569f1-558">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="569f1-559">Conectar tooan suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="569f1-559">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="569f1-560">Creación de una cuenta de almacenamiento nueva</span><span class="sxs-lookup"><span data-stu-id="569f1-560">Create a new storage account</span></span>
3. <span data-ttu-id="569f1-561">Crear una red virtual nueva y tres subredes tal como se define en el archivo de configuración de red de Hola</span><span class="sxs-lookup"><span data-stu-id="569f1-561">Create a new VNet and three subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="569f1-562">Creación de cinco máquinas virtuales, un firewall y cuatro máquinas virtuales de servidor Windows</span><span class="sxs-lookup"><span data-stu-id="569f1-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="569f1-563">La configuración del enrutamiento definido por el usuario incluye:</span><span class="sxs-lookup"><span data-stu-id="569f1-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="569f1-564">Crear dos nuevas tablas de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="569f1-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="569f1-565">Agregar tablas de rutas toohello</span><span class="sxs-lookup"><span data-stu-id="569f1-565">Add routes toohello tables</span></span>
   3. <span data-ttu-id="569f1-566">Enlazar subredes tooappropriate de tablas</span><span class="sxs-lookup"><span data-stu-id="569f1-566">Bind tables tooappropriate subnets</span></span>
6. <span data-ttu-id="569f1-567">Habilitar el reenvío IP en hello NVA</span><span class="sxs-lookup"><span data-stu-id="569f1-567">Enable IP Forwarding on hello NVA</span></span>
7. <span data-ttu-id="569f1-568">Configuración del grupo de seguridad de red, incluido lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="569f1-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="569f1-569">Creación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="569f1-569">Creating a NSG</span></span>
   2. <span data-ttu-id="569f1-570">Adición de una regla</span><span class="sxs-lookup"><span data-stu-id="569f1-570">Adding a rule</span></span>
   3. <span data-ttu-id="569f1-571">Enlace hello NSG toohello las subredes correspondientes</span><span class="sxs-lookup"><span data-stu-id="569f1-571">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="569f1-572">Este script de PowerShell debe ejecutarse localmente en un equipo o servidor conectado a Internet.</span><span class="sxs-lookup"><span data-stu-id="569f1-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="569f1-573">Cuando se ejecuta este script, puede haber advertencias u otros mensajes informativos que se muestran en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="569f1-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="569f1-574">Solo los mensajes de error indicados en rojo son motivo de preocupación.</span><span class="sxs-lookup"><span data-stu-id="569f1-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="569f1-575">Archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="569f1-575">Network Config File</span></span>
<span data-ttu-id="569f1-576">Guarde este archivo xml con la ubicación actualizada y agregue Hola vínculo toothis toohello $NetworkConfigFile variable de archivos de script de Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="569f1-576">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a><span data-ttu-id="569f1-577">Scripts de aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="569f1-577">Sample Application Scripts</span></span>
<span data-ttu-id="569f1-578">Si desea tooinstall una aplicación de ejemplo para este y otros ejemplos de la red Perimetral, se aplicó en hello siguiente vínculo: [Script de aplicación de ejemplo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="569f1-578">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Red perimetral bidireccional con un dispositivo de red virtual, grupos de seguridad de red y enrutamiento definido por el usuario"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Vista lógica de hello las reglas de Firewall"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Creación de un objeto de red front-end"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Creación de un objeto de servidor DNS"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copia de la regla predeterminada de RDP"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Regla de AppVM01"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Icono de redirección de aplicación"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Icono de NAT de destino"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Icono de Paso"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Regla de administración de firewall"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Regla de RDP de firewall"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Regla web de firewall"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Regla de AppVM01 de firewall"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Regla de salida de firewall"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Regla de DNS de firewall"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Regla entre redes virtuales de firewall"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Regla de denegación de firewall"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Activación de reglas de firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
