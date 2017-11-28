---
title: 'aaaAzure DMZ ejemplo: crear una red Perimetral Simple con NSG | Documentos de Microsoft'
description: "Creación de una red perimetral con grupos de seguridad de red"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="05588-103">Ejemplo 1: crear una red perimetral simple mediante grupos de seguridad de red con PowerShell clásico</span><span class="sxs-lookup"><span data-stu-id="05588-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="05588-104">[Devolver toohello página de prácticas recomendadas de seguridad límite][HOME]</span><span class="sxs-lookup"><span data-stu-id="05588-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="05588-105">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05588-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="05588-106">Clásico: PowerShell</span><span class="sxs-lookup"><span data-stu-id="05588-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="05588-107">En este ejemplo se crea una red perimetral primitiva con cuatro servidores Windows y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="05588-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="05588-108">Este ejemplo describe cada uno de los tooprovide de comandos de PowerShell relevante de hello una comprensión más profunda de cada paso.</span><span class="sxs-lookup"><span data-stu-id="05588-108">This example describes each of hello relevant PowerShell commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="05588-109">También hay un escenario de tráfico sección tooprovide una detallada paso a paso cómo tráfico pasa a través de las capas de defensa en Hola Hola red Perimetral.</span><span class="sxs-lookup"><span data-stu-id="05588-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="05588-110">Por último, en la sección de referencias de hello es código completo de Hola e instrucción toobuild este entorno tootest y experimentar con diferentes escenarios.</span><span class="sxs-lookup"><span data-stu-id="05588-110">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="05588-111">![Red perimetral de entrada con grupo de seguridad de red][1]</span><span class="sxs-lookup"><span data-stu-id="05588-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="05588-112">Descripción del entorno</span><span class="sxs-lookup"><span data-stu-id="05588-112">Environment description</span></span>
<span data-ttu-id="05588-113">En este ejemplo, una suscripción contiene Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="05588-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="05588-114">Dos servicios en la nube: "FrontEnd001" y "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="05588-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="05588-115">Una red virtual, “CorpNetwork”, con dos subredes, “FrontEnd” y “BackEnd”</span><span class="sxs-lookup"><span data-stu-id="05588-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="05588-116">Un grupo de seguridad de red que está aplicada tooboth subredes</span><span class="sxs-lookup"><span data-stu-id="05588-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="05588-117">Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="05588-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="05588-118">Dos servidores Windows que representan servidores back-end de aplicaciones ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="05588-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="05588-119">Un servidor Windows que representa un servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="05588-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="05588-120">En la sección de referencias de hello, hay una secuencia de comandos de PowerShell que se basa la mayor parte del entorno de hello descrita en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="05588-120">In hello references section, there is a PowerShell script that builds most of hello environment described in this example.</span></span> <span data-ttu-id="05588-121">Hola de crear las máquinas virtuales y redes virtuales, aunque se realizan mediante el script de ejemplo de Hola, no se describen en detalle en este documento.</span><span class="sxs-lookup"><span data-stu-id="05588-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="05588-122">entorno de hello toobuild;</span><span class="sxs-lookup"><span data-stu-id="05588-122">toobuild hello environment;</span></span>

1. <span data-ttu-id="05588-123">Guardar archivo de xml de configuración Hola red incluido en la sección de referencias de hello (actualizada con nombres, la ubicación y el escenario de hello dada de toomatch de direcciones IP)</span><span class="sxs-lookup"><span data-stu-id="05588-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="05588-124">Variables de usuario de actualización hello en hello toomatch Hola entorno Hola de script es toobe ejecutarán (suscripciones, los nombres de servicio, etcetera.)</span><span class="sxs-lookup"><span data-stu-id="05588-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="05588-125">Ejecutar script de Hola en PowerShell</span><span class="sxs-lookup"><span data-stu-id="05588-125">Execute hello script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="05588-126">región Hola indicado en el script de PowerShell de Hola debe coincidir con la región Hola indicado en el archivo de xml de configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="05588-126">hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>
>
>

<span data-ttu-id="05588-127">Una vez que se ejecuta correctamente adicional el script de Hola pasos opcionales pueden tener, en la sección de referencias de hello son dos de las secuencias de comandos tooset seguridad hello web y servidor de aplicaciones con una tooallow de aplicación web simple pruebas con esta configuración de red Perimetral.</span><span class="sxs-lookup"><span data-stu-id="05588-127">Once hello script runs successfully additional optional steps may be taken, in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="05588-128">Hello secciones siguientes proporcionan una descripción detallada de los grupos de seguridad de red y cómo funcionan en este ejemplo recorriendo líneas de clave de secuencia de comandos de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="05588-128">hello following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of hello PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="05588-129">Grupos de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="05588-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="05588-130">En este ejemplo, se crea un grupo de seguridad de red y se cargan después seis reglas.</span><span class="sxs-lookup"><span data-stu-id="05588-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="05588-131">Por lo general, debe crear primero las reglas específicas de "Permitir" y, a continuación, Hola reglas más genéricas de "Denegar" última.</span><span class="sxs-lookup"><span data-stu-id="05588-131">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="05588-132">Hola tenga asignada la prioridad determina qué reglas se evalúan primero.</span><span class="sxs-lookup"><span data-stu-id="05588-132">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="05588-133">Una vez que el tráfico se encuentra la regla específica de tooapply tooa, no se evalúa ninguna otra regla.</span><span class="sxs-lookup"><span data-stu-id="05588-133">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="05588-134">Se pueden aplicar reglas NSG en la vista en hello dirección entrante o saliente (desde la perspectiva de Hola de subred de hello).</span><span class="sxs-lookup"><span data-stu-id="05588-134">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="05588-135">Mediante declaración, se regeneran Hola siguiendo las reglas para el tráfico entrante:</span><span class="sxs-lookup"><span data-stu-id="05588-135">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="05588-136">Se permite el tráfico DNS interno (puerto 53)</span><span class="sxs-lookup"><span data-stu-id="05588-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="05588-137">Se permite el tráfico RDP (puerto 3389) de hello Internet tooany VM</span><span class="sxs-lookup"><span data-stu-id="05588-137">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="05588-138">Se permite el tráfico HTTP (puerto 80) del servidor de hello Internet tooweb (IIS01)</span><span class="sxs-lookup"><span data-stu-id="05588-138">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="05588-139">Se permite cualquier tráfico (todos los puertos) del IIS01 tooAppVM1</span><span class="sxs-lookup"><span data-stu-id="05588-139">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="05588-140">Todo (todos los puertos) el tráfico de hello Internet toohello se deniega todo red virtual (tanto en las subredes)</span><span class="sxs-lookup"><span data-stu-id="05588-140">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="05588-141">Se deniega todo (todos los puertos) el tráfico de subred de back-end de hello front-end subred toohello</span><span class="sxs-lookup"><span data-stu-id="05588-141">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="05588-142">Con estas subredes de enlazado tooeach reglas, si una solicitud HTTP es entrante desde el servidor web de hello Internet toohello, ambas reglas 3 (permitir) y 5 (denegar) aplicaría, pero dado que la regla 3 tiene mayor prioridad solo aplicaría y regla 5 podría no entran en juego.</span><span class="sxs-lookup"><span data-stu-id="05588-142">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="05588-143">Por lo tanto solicitud HTTP de hello podría permitirse a toohello servidor de web.</span><span class="sxs-lookup"><span data-stu-id="05588-143">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="05588-144">Si ese mismo tráfico estaba intentando server DNS01 de tooreach hello, regla 5 (Deny) sería Hola primera hello y tooapply el tráfico no estarían permitido a toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="05588-144">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="05588-145">Regla 6 (Deny) bloques de subred de front-end de Hola de hablar de subred de back-end de toohello (excepto el tráfico permitido en las reglas 1 y 4), este conjunto de reglas protege la red de back-end de hello en caso de que una aplicación atacante pone en peligro hello web en hello front-end, el atacante de hello sería ha limitado toohello acceso back-end "protegido" red (solo tooresources expuesta en el servidor de hello AppVM01).</span><span class="sxs-lookup"><span data-stu-id="05588-145">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="05588-146">Hay una regla de salida predeterminada que permite el tráfico de salida toohello internet.</span><span class="sxs-lookup"><span data-stu-id="05588-146">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="05588-147">En este ejemplo, permitimos el tráfico saliente y no modificamos las reglas de salida.</span><span class="sxs-lookup"><span data-stu-id="05588-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="05588-148">toolock hacia abajo el tráfico en ambas direcciones, enrutamiento de definido por usuario es obligatorio y se explora en "Ejemplo 3" en hello [página de prácticas recomendadas de seguridad límite][HOME].</span><span class="sxs-lookup"><span data-stu-id="05588-148">toolock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="05588-149">Cada regla se explica con más detalle como sigue (**Nota**: cualquier elemento de hello sigue el principio de la lista con un signo de dólar (por ejemplo: $NSGName) es una variable definida por el usuario desde un script de Hola en la sección de referencia de Hola de este documento):</span><span class="sxs-lookup"><span data-stu-id="05588-149">Each rule is discussed in more detail as follows (**Note**: any item in hello following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="05588-150">En primer lugar un grupo de seguridad de red debe compilarse reglas de Hola toohold:</span><span class="sxs-lookup"><span data-stu-id="05588-150">First a Network Security Group must be built toohold hello rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="05588-151">la primera regla en este ejemplo de Hola permite el tráfico DNS entre todos los servidores DNS de toohello redes internas de subred de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="05588-151">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="05588-152">regla de Hello tiene algunos parámetros importantes:</span><span class="sxs-lookup"><span data-stu-id="05588-152">hello rule has some important parameters:</span></span>
   
   * <span data-ttu-id="05588-153">"Type" indica en qué dirección del flujo de tráfico esta entrada surte efecto.</span><span class="sxs-lookup"><span data-stu-id="05588-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="05588-154">dirección de Hello es desde la perspectiva de Hola de subred de Hola o una máquina Virtual (en función de donde está enlazado este GSN).</span><span class="sxs-lookup"><span data-stu-id="05588-154">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="05588-155">Por lo tanto si tipo es "Inbound" y está accediendo al tráfico de subred de Hola, Hola regla se aplicará y tráfico que sale de la subred de hello no se verían afectado por esta regla.</span><span class="sxs-lookup"><span data-stu-id="05588-155">Thus if Type is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="05588-156">"Priority" establece el orden de hello en el que se evalúa un flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="05588-156">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="05588-157">Hola inferior Hola número Hola Hola prioridad.</span><span class="sxs-lookup"><span data-stu-id="05588-157">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="05588-158">Cuando una regla aplica tooa flujo de tráfico específico, no se procesa ninguna otra regla.</span><span class="sxs-lookup"><span data-stu-id="05588-158">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="05588-159">Por tanto, si una regla con prioridad 1 permite el tráfico y una regla con prioridad 2 deniega el tráfico y ambas reglas aplican tootraffic, ¿se permite el tráfico de hello tooflow (puesto regla 1 no tenía una prioridad más alta entra en vigor y no se aplica ninguna otra regla).</span><span class="sxs-lookup"><span data-stu-id="05588-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="05588-160">"Action" indica si se bloquea o se permite el tráfico al que afecta esta regla.</span><span class="sxs-lookup"><span data-stu-id="05588-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="05588-161">Esta regla permite tooflow de tráfico RDP de hello internet toohello el puerto RDP en cualquier servidor de hello enlazado subred.</span><span class="sxs-lookup"><span data-stu-id="05588-161">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> <span data-ttu-id="05588-162">Esta regla usa dos tipos especiales de prefijos de dirección: "VIRTUAL_NETWORK" e "INTERNET".</span><span class="sxs-lookup"><span data-stu-id="05588-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="05588-163">Estas etiquetas son un tooaddress fácilmente una categoría mayor de prefijos de dirección.</span><span class="sxs-lookup"><span data-stu-id="05588-163">These tags are an easy way tooaddress a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="05588-164">Esta regla permite que servidor de web de hello toohit de tráfico de internet entrante.</span><span class="sxs-lookup"><span data-stu-id="05588-164">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="05588-165">Esta regla no cambia el comportamiento de enrutamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="05588-165">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="05588-166">regla de Hello solo permite el tráfico destinado a IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="05588-166">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="05588-167">Por lo tanto si el tráfico de Internet Hola tenía el servidor de web de hello como su destino de esta regla se permitirlo y detener el procesamiento de más reglas.</span><span class="sxs-lookup"><span data-stu-id="05588-167">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="05588-168">(En la regla de hello con prioridad 140 todos los demás tráfico entrante de internet se bloquea).</span><span class="sxs-lookup"><span data-stu-id="05588-168">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="05588-169">Si sólo está procesando el tráfico HTTP, esta regla podría ser más restringido tooonly Permitir destino puerto 80.</span><span class="sxs-lookup"><span data-stu-id="05588-169">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="05588-170">Esta regla permite toopass de tráfico desde el servidor de hello IIS01 toohello AppVM01 server, una regla posterior bloquea todo el tráfico de otros tooBackend front-end.</span><span class="sxs-lookup"><span data-stu-id="05588-170">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="05588-171">tooimprove esta regla, si se conoce el puerto de Hola que debe agregarse.</span><span class="sxs-lookup"><span data-stu-id="05588-171">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="05588-172">Por ejemplo, si el servidor IIS de hello está alcanzando solo SQL Server en AppVM01, intervalo de puertos de destino de hello debe cambiarse de "*" (Any) too1433 (Hola puerto de SQL) lo que permite una menor superficie expuesta a ataques entrantes en AppVM01 debe alguna vez verse comprometida la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="05588-172">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="05588-173">Esta regla deniega el tráfico de los servidores de tooany de internet de hello en red Hola.</span><span class="sxs-lookup"><span data-stu-id="05588-173">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="05588-174">Con las reglas de hello en prioridad 110 y 120, el efecto de hello es tooallow solo internet tráfico toohello firewall de entrada y puertos RDP en servidores y todo lo demás bloquea.</span><span class="sxs-lookup"><span data-stu-id="05588-174">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="05588-175">Esta regla es la regla de notificaciones de "error" tooblock todos los flujos inesperados.</span><span class="sxs-lookup"><span data-stu-id="05588-175">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="05588-176">regla de final de Hello deniega el tráfico de subred de back-end de hello front-end subred toohello.</span><span class="sxs-lookup"><span data-stu-id="05588-176">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="05588-177">Puesto que esta regla es una regla de sola entrada, se permite el tráfico inverso (de hello back-end toohello front-end).</span><span class="sxs-lookup"><span data-stu-id="05588-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="05588-178">Escenarios de tráfico</span><span class="sxs-lookup"><span data-stu-id="05588-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="05588-179">(*Permitido*) servidor de Internet tooweb</span><span class="sxs-lookup"><span data-stu-id="05588-179">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="05588-180">Un usuario de Internet solicita una página HTTP desde FrontEnd001.CloudApp.Net (servicio en la nube accesible desde Internet).</span><span class="sxs-lookup"><span data-stu-id="05588-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="05588-181">En la nube tráfico del servicio pasa a través de un extremo abierto en el puerto 80 hacia IIS01 (servidor web de hello)</span><span class="sxs-lookup"><span data-stu-id="05588-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="05588-182">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="05588-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="05588-183">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-183">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="05588-184">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-184">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="05588-185">Aplicar NSG regla 3 (tooIIS01 Internet), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="05588-185">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="05588-186">Tráfico alcanza el dirección IP interna del servidor web de hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="05588-186">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="05588-187">Iis01 escucha el tráfico de web, recibe esta solicitud y comienza a procesar la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="05588-187">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="05588-188">Iis01 pide Hola SQL Server en AppVM01 información</span><span class="sxs-lookup"><span data-stu-id="05588-188">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="05588-189">Puesto que no hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="05588-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="05588-190">subred de back-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="05588-190">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="05588-191">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-191">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="05588-192">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-192">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="05588-193">Regla de NSG 3 (tooFirewall Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-193">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="05588-194">Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="05588-194">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="05588-195">AppVM01 recibe Hola consulta SQL y responde</span><span class="sxs-lookup"><span data-stu-id="05588-195">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="05588-196">Dado que no hay ninguna regla de salida en la subred de back-end de hello, se permite la respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="05588-196">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="05588-197">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="05588-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="05588-198">No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola</span><span class="sxs-lookup"><span data-stu-id="05588-198">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="05588-199">Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="05588-199">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="05588-200">servidor IIS de Hello recibe la respuesta SQL de Hola y completa respuesta HTTP de Hola y envía toohello solicitante</span><span class="sxs-lookup"><span data-stu-id="05588-200">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
13. <span data-ttu-id="05588-201">Dado que no hay ninguna regla de salida en la subred de front-end de Hola Hola se permita respuesta y hello internet usuario recibe hello web página solicitada.</span><span class="sxs-lookup"><span data-stu-id="05588-201">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="05588-202">(*Permitido*) toobackend RDP</span><span class="sxs-lookup"><span data-stu-id="05588-202">(*Allowed*) RDP toobackend</span></span>
1. <span data-ttu-id="05588-203">Administrador del servidor en internet solicita tooAppVM01 de sesión RDP en BackEnd001.CloudApp.Net:xxxxx donde xxxxx es el número de puerto de hello asignada aleatoriamente para tooAppVM01 RDP (puerto Hola asignado se puede encontrar en el portal de Azure de Hola o a través de PowerShell)</span><span class="sxs-lookup"><span data-stu-id="05588-203">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="05588-204">La subred back-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="05588-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="05588-205">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-205">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="05588-206">Se aplica la regla 2 (RDP) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="05588-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="05588-207">No hay reglas de salida, se aplican las reglas predeterminadas y se permite el tráfico de retorno.</span><span class="sxs-lookup"><span data-stu-id="05588-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="05588-208">La sesión RDP está habilitada.</span><span class="sxs-lookup"><span data-stu-id="05588-208">RDP session is enabled</span></span>
5. <span data-ttu-id="05588-209">Mensajes de AppVM01 Hola nombre de usuario y contraseña</span><span class="sxs-lookup"><span data-stu-id="05588-209">AppVM01 prompts for hello user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="05588-210">(*Permitido*) Búsqueda de DNS del servidor web en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="05588-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="05588-211">Web necesidades de servidor, IIS01, fuente de distribución de datos en www.data.gov, pero necesita tooresolve Hola dirección.</span><span class="sxs-lookup"><span data-stu-id="05588-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="05588-212">Hola configuración de red para las listas de red virtual de hello DNS01 (10.0.2.4 de subred de back-end de hello) como servidor DNS principal de hello, IIS01 envía Hola DNS solicitud tooDNS01</span><span class="sxs-lookup"><span data-stu-id="05588-212">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="05588-213">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="05588-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="05588-214">La subred back-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="05588-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="05588-215">Se aplica la regla 1 (DNS) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="05588-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="05588-216">Servidor DNS recibe la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="05588-216">DNS server receives hello request</span></span>
6. <span data-ttu-id="05588-217">Servidor DNS no tiene dirección de hello en caché y pide un servidor DNS raíz en hello internet</span><span class="sxs-lookup"><span data-stu-id="05588-217">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="05588-218">No hay reglas de salida en la subred back-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="05588-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="05588-219">Se responde el servidor DNS de Internet, ya que esta sesión se ha iniciado internamente, se permite la respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="05588-219">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="05588-220">Servidor DNS almacena en caché la respuesta de Hola y responde tooIIS01 de espera de solicitud inicial toohello</span><span class="sxs-lookup"><span data-stu-id="05588-220">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="05588-221">No hay reglas de salida en la subred back-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="05588-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="05588-222">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="05588-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="05588-223">No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola</span><span class="sxs-lookup"><span data-stu-id="05588-223">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="05588-224">Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico por lo que se permite el tráfico de Hola</span><span class="sxs-lookup"><span data-stu-id="05588-224">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="05588-225">Iis01 recibe respuesta hello DNS01</span><span class="sxs-lookup"><span data-stu-id="05588-225">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="05588-226">(*Permitido*) Archivo de acceso del servidor web en AppVM01</span><span class="sxs-lookup"><span data-stu-id="05588-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="05588-227">IIS01 solicita un archivo en AppVM01</span><span class="sxs-lookup"><span data-stu-id="05588-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="05588-228">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="05588-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="05588-229">subred de back-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="05588-229">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="05588-230">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-230">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="05588-231">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-231">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="05588-232">Regla de NSG 3 (tooIIS01 Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-232">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="05588-233">Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="05588-233">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="05588-234">AppVM01 recibe la solicitud de Hola y responde con el archivo (suponiendo que se autoriza el acceso)</span><span class="sxs-lookup"><span data-stu-id="05588-234">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="05588-235">Dado que no hay ninguna regla de salida en la subred de back-end de hello, se permite la respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="05588-235">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="05588-236">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="05588-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="05588-237">No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola</span><span class="sxs-lookup"><span data-stu-id="05588-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="05588-238">Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="05588-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="05588-239">servidor IIS de Hello recibe el archivo hello</span><span class="sxs-lookup"><span data-stu-id="05588-239">hello IIS server receives hello file</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="05588-240">(*Denegado*) servidor de Web toobackend</span><span class="sxs-lookup"><span data-stu-id="05588-240">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="05588-241">Tooaccess un archivo en AppVM01 a través de hello BackEnd001.CloudApp.Net servicio trata de un usuario de internet</span><span class="sxs-lookup"><span data-stu-id="05588-241">An internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="05588-242">Dado que no hay ningún extremo abierto para el recurso compartido de archivos, este tráfico no pasaría Hola servicio en la nube y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="05588-242">Since there are no endpoints open for file share, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="05588-243">Si los puntos de conexión de hello estaban abiertos por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico</span><span class="sxs-lookup"><span data-stu-id="05588-243">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="05588-244">(*Denegado*) Búsqueda de DNS web en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="05588-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="05588-245">Un usuario de internet intenta toolook un registro de DNS interna en DNS01 a través de hello BackEnd001.CloudApp.Net servicio</span><span class="sxs-lookup"><span data-stu-id="05588-245">An internet user tries toolook up an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="05588-246">Dado que no hay ningún extremo abierto para DNS, este tráfico no pasaría Hola servicio en la nube y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="05588-246">Since there are no endpoints open for DNS, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="05588-247">Si los puntos de conexión de hello estaban abiertos por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico (Nota: esa regla 1 (DNS) no se aplicarían por dos motivos, primera dirección de origen de hello es Hola internet, esta regla solo aplica toohello red virtual local como Hola de origen, también Esta regla es una regla de permiso, por lo que nunca podría denegar el tráfico)</span><span class="sxs-lookup"><span data-stu-id="05588-247">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="05588-248">(*Denegado*) Web tooSQL acceso a través del firewall</span><span class="sxs-lookup"><span data-stu-id="05588-248">(*Denied*) Web tooSQL access through firewall</span></span>
1. <span data-ttu-id="05588-249">Un usuario de Internet solicita los datos SQL desde FrontEnd001.CloudApp.Net (servicio en la nube accesible desde Internet).</span><span class="sxs-lookup"><span data-stu-id="05588-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="05588-250">Dado que no hay ningún extremo abierto para SQL, este tráfico no pasaría Hola servicio en la nube y no llegar a firewall de Hola</span><span class="sxs-lookup"><span data-stu-id="05588-250">Since there are no endpoints open for SQL, this traffic would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="05588-251">Si los puntos de conexión estaban abiertos por algún motivo, subred de front-end de hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="05588-251">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="05588-252">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-252">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="05588-253">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="05588-253">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="05588-254">Aplicar NSG regla 3 (tooIIS01 Internet), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="05588-254">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="05588-255">Tráfico alcanza el dirección IP interna de hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="05588-255">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="05588-256">Iis01 no está escuchando en el puerto 1433, por lo que no hay ninguna solicitud de toohello de respuesta</span><span class="sxs-lookup"><span data-stu-id="05588-256">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="05588-257">Conclusión</span><span class="sxs-lookup"><span data-stu-id="05588-257">Conclusion</span></span>
<span data-ttu-id="05588-258">En este ejemplo es una forma relativamente simple y sencillo de aislar la subred de back-end de Hola de tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="05588-258">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="05588-259">Puede encontrar más ejemplos y una descripción general de los límites de seguridad de red [aquí][HOME].</span><span class="sxs-lookup"><span data-stu-id="05588-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="05588-260">Referencias</span><span class="sxs-lookup"><span data-stu-id="05588-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="05588-261">Script principal y configuración de red</span><span class="sxs-lookup"><span data-stu-id="05588-261">Main script and network config</span></span>
<span data-ttu-id="05588-262">Guardar Hola Script completo en un archivo de script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05588-262">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="05588-263">Guardar Hola configuración de red en un archivo denominado "NetworkConf1.xml."</span><span class="sxs-lookup"><span data-stu-id="05588-263">Save hello Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="05588-264">Modificar variables definidas por el usuario de hello como script de Hola necesarios y que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="05588-264">Modify hello user-defined variables as needed and run hello script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="05588-265">Script completo</span><span class="sxs-lookup"><span data-stu-id="05588-265">Full script</span></span>
<span data-ttu-id="05588-266">Esta secuencia de comandos mostrarán, en función de variables definidas por el usuario de hello;</span><span class="sxs-lookup"><span data-stu-id="05588-266">This script will, based on hello user-defined variables;</span></span>

1. <span data-ttu-id="05588-267">Conectar tooan suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="05588-267">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="05588-268">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="05588-268">Create a storage account</span></span>
3. <span data-ttu-id="05588-269">Crear una red virtual y dos subredes tal como se define en el archivo de configuración de red de Hola</span><span class="sxs-lookup"><span data-stu-id="05588-269">Create a VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="05588-270">Creación de cuatro máquinas virtuales de Windows Server</span><span class="sxs-lookup"><span data-stu-id="05588-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="05588-271">Configuración del grupo de seguridad de red, incluido lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="05588-271">Configure NSG including:</span></span>
   * <span data-ttu-id="05588-272">Creación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="05588-272">Creating an NSG</span></span>
   * <span data-ttu-id="05588-273">Rellenado con reglas</span><span class="sxs-lookup"><span data-stu-id="05588-273">Populating it with rules</span></span>
   * <span data-ttu-id="05588-274">Enlace hello NSG toohello las subredes correspondientes</span><span class="sxs-lookup"><span data-stu-id="05588-274">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="05588-275">Este script de PowerShell debe ejecutarse localmente en un equipo o servidor conectado a Internet.</span><span class="sxs-lookup"><span data-stu-id="05588-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05588-276">Cuando se ejecuta este script, puede haber advertencias u otros mensajes informativos que se muestran en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05588-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="05588-277">Solo los mensajes de error indicados en rojo son motivo de preocupación.</span><span class="sxs-lookup"><span data-stu-id="05588-277">Only error messages in red are cause for concern.</span></span>
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

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

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="05588-278">Archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="05588-278">Network config file</span></span>
<span data-ttu-id="05588-279">Guarde este archivo xml con la ubicación actualizada y agregue variable de hello link toothis archivo toohello $NetworkConfigFile Hola anterior secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="05588-279">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello preceding script.</span></span>

```XML
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
```

#### <a name="sample-application-scripts"></a><span data-ttu-id="05588-280">Scripts de aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="05588-280">Sample application scripts</span></span>
<span data-ttu-id="05588-281">Si desea tooinstall una aplicación de ejemplo para este y otros ejemplos de la red Perimetral, se aplicó en hello siguiente vínculo: [Script de aplicación de ejemplo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="05588-281">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="05588-282">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05588-282">Next steps</span></span>
* <span data-ttu-id="05588-283">Actualice y guarde el archivo XML.</span><span class="sxs-lookup"><span data-stu-id="05588-283">Update and save XML file</span></span>
* <span data-ttu-id="05588-284">Ejecute hello PowerShell script toobuild Hola entorno</span><span class="sxs-lookup"><span data-stu-id="05588-284">Run hello PowerShell script toobuild hello environment</span></span>
* <span data-ttu-id="05588-285">Instalar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="05588-285">Install hello sample application</span></span>
* <span data-ttu-id="05588-286">Probar los flujos de tráfico distintos a través de esta red perimetral</span><span class="sxs-lookup"><span data-stu-id="05588-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Red perimetral de entrada con grupo de seguridad de red"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

