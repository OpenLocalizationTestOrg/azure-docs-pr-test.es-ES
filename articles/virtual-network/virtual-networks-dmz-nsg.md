---
title: 'aaaAzure DMZ ejemplo: crear una red Perimetral Simple con NSG | Documentos de Microsoft'
description: "Creación de una red perimetral con grupos de seguridad de red"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="abced-103">Ejemplo 1: Crear una red perimetral simple mediante NSG con una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abced-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="abced-104">[Devolver toohello página de prácticas recomendadas de seguridad límite][HOME]</span><span class="sxs-lookup"><span data-stu-id="abced-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="abced-105">Plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="abced-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="abced-106">Clásico: PowerShell</span><span class="sxs-lookup"><span data-stu-id="abced-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="abced-107">En este ejemplo se crea una red perimetral primitiva con cuatro servidores Windows y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="abced-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="abced-108">En este ejemplo se describe cada uno de hello plantilla relevante secciones tooprovide una comprensión más profunda de cada paso.</span><span class="sxs-lookup"><span data-stu-id="abced-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="abced-109">También hay un tooprovide de sección de escenario de tráfico obtener información detallada sobre paso a paso cómo se realiza el tráfico a través de niveles de Hola de defensa en hello red Perimetral.</span><span class="sxs-lookup"><span data-stu-id="abced-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="abced-110">Por último, en la sección de referencias de hello es toobuild de código y las instrucciones de la plantilla completa de Hola este entorno tootest y experimentar con diferentes escenarios.</span><span class="sxs-lookup"><span data-stu-id="abced-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="abced-111">![Red perimetral de entrada con grupo de seguridad de red][1]</span><span class="sxs-lookup"><span data-stu-id="abced-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="abced-112">Descripción del entorno</span><span class="sxs-lookup"><span data-stu-id="abced-112">Environment description</span></span>
<span data-ttu-id="abced-113">En este ejemplo, una suscripción contiene Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="abced-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="abced-114">Un único grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="abced-114">A single resource group</span></span>
* <span data-ttu-id="abced-115">Una red virtual con dos subredes (FrontEnd y BackEnd)</span><span class="sxs-lookup"><span data-stu-id="abced-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="abced-116">Un grupo de seguridad de red que está aplicada tooboth subredes</span><span class="sxs-lookup"><span data-stu-id="abced-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="abced-117">Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="abced-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="abced-118">Dos servidores Windows que representan servidores back-end de aplicaciones ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="abced-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="abced-119">Un servidor Windows que representa un servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="abced-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="abced-120">Una dirección IP pública asociada con el servidor de web de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="abced-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="abced-121">En la sección de referencias de hello, hay una plantilla de Azure Resource Manager tooan de vínculo que se basa el entorno de hello descrita en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="abced-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="abced-122">Hola de crear las máquinas virtuales y redes virtuales, aunque se realiza mediante la plantilla de ejemplo de Hola, se describen detalladamente en este documento.</span><span class="sxs-lookup"><span data-stu-id="abced-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="abced-123">**toobuild este entorno** (las instrucciones detalladas están en la sección de referencias de Hola de este documento);</span><span class="sxs-lookup"><span data-stu-id="abced-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="abced-124">Implementar Hola plantilla del Administrador de recursos de Azure en: [plantillas de inicio rápido de Azure][Template]</span><span class="sxs-lookup"><span data-stu-id="abced-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="abced-125">Instalar la aplicación de ejemplo de Hola en: [Script de aplicación de ejemplo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="abced-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="abced-126">servidores de back-end de tooRDP tooany en este caso, el servidor IIS de Hola se utiliza como un "cuadro salto".</span><span class="sxs-lookup"><span data-stu-id="abced-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="abced-127">Primer servidor RDP toohello IIS y, a continuación, desde el servidor de hello IIS Server RDP toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="abced-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="abced-128">Asimismo, una IP pública se puede asociar con cada servidor NIC para facilitar la conexión RDP.</span><span class="sxs-lookup"><span data-stu-id="abced-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="abced-129">Hello secciones siguientes proporcionan una descripción detallada de hello grupo de seguridad de red y su funcionamiento en este ejemplo recorriendo líneas claves de hello plantilla del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="abced-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="abced-130">Grupos de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="abced-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="abced-131">En este ejemplo, se crea un grupo de seguridad de red y se cargan después seis reglas.</span><span class="sxs-lookup"><span data-stu-id="abced-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="abced-132">Por lo general, debe crear primero las reglas específicas de "Permitir" y, a continuación, Hola reglas más genéricas de "Denegar" última.</span><span class="sxs-lookup"><span data-stu-id="abced-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="abced-133">Hola tenga asignada la prioridad determina qué reglas se evalúan primero.</span><span class="sxs-lookup"><span data-stu-id="abced-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="abced-134">Una vez que el tráfico se encuentra la regla específica de tooapply tooa, no se evalúa ninguna otra regla.</span><span class="sxs-lookup"><span data-stu-id="abced-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="abced-135">Se pueden aplicar reglas NSG en la vista en hello dirección entrante o saliente (desde la perspectiva de Hola de subred de hello).</span><span class="sxs-lookup"><span data-stu-id="abced-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="abced-136">Mediante declaración, se regeneran Hola siguiendo las reglas para el tráfico entrante:</span><span class="sxs-lookup"><span data-stu-id="abced-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="abced-137">Se permite el tráfico DNS interno (puerto 53)</span><span class="sxs-lookup"><span data-stu-id="abced-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="abced-138">Se permite el tráfico RDP (puerto 3389) de hello Internet tooany VM</span><span class="sxs-lookup"><span data-stu-id="abced-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="abced-139">Se permite el tráfico HTTP (puerto 80) del servidor de hello Internet tooweb (IIS01)</span><span class="sxs-lookup"><span data-stu-id="abced-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="abced-140">Se permite cualquier tráfico (todos los puertos) del IIS01 tooAppVM1</span><span class="sxs-lookup"><span data-stu-id="abced-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="abced-141">Todo (todos los puertos) el tráfico de hello Internet toohello se deniega todo red virtual (tanto en las subredes)</span><span class="sxs-lookup"><span data-stu-id="abced-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="abced-142">Se deniega todo (todos los puertos) el tráfico de subred de back-end de hello front-end subred toohello</span><span class="sxs-lookup"><span data-stu-id="abced-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="abced-143">Con estas subredes de enlazado tooeach reglas, si una solicitud HTTP es entrante desde el servidor web de hello Internet toohello, ambas reglas 3 (permitir) y 5 (denegar) aplicaría, pero dado que la regla 3 tiene mayor prioridad solo aplicaría y regla 5 podría no entran en juego.</span><span class="sxs-lookup"><span data-stu-id="abced-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="abced-144">Por lo tanto solicitud HTTP de hello podría permitirse a toohello servidor de web.</span><span class="sxs-lookup"><span data-stu-id="abced-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="abced-145">Si ese mismo tráfico estaba intentando server DNS01 de tooreach hello, regla 5 (Deny) sería Hola primera hello y tooapply el tráfico no estarían permitido a toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="abced-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="abced-146">Regla 6 (Deny) bloques de subred de front-end de Hola de hablar de subred de back-end de toohello (excepto el tráfico permitido en las reglas 1 y 4), este conjunto de reglas protege la red de back-end de hello en caso de que una aplicación atacante pone en peligro hello web en hello front-end, el atacante de hello sería ha limitado toohello acceso back-end "protegido" red (solo tooresources expuesta en el servidor de hello AppVM01).</span><span class="sxs-lookup"><span data-stu-id="abced-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="abced-147">Hay una regla de salida predeterminada que permite el tráfico de salida toohello internet.</span><span class="sxs-lookup"><span data-stu-id="abced-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="abced-148">En este ejemplo, permitimos el tráfico saliente y no modificamos las reglas de salida.</span><span class="sxs-lookup"><span data-stu-id="abced-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="abced-149">tooapply tootraffic de directiva de seguridad en ambas direcciones, enrutamiento de definido por usuario es obligatorio y se explora en "Ejemplo 3" en hello [página de prácticas recomendadas de seguridad límite][HOME].</span><span class="sxs-lookup"><span data-stu-id="abced-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="abced-150">Cada regla se explica con más detalle a continuación:</span><span class="sxs-lookup"><span data-stu-id="abced-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="abced-151">Un recurso de grupo de seguridad de red debe ser toohold instancias Hola reglas:</span><span class="sxs-lookup"><span data-stu-id="abced-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="abced-152">la primera regla en este ejemplo de Hola permite el tráfico DNS entre todos los servidores DNS de toohello redes internas de subred de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="abced-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="abced-153">regla de Hello tiene algunos parámetros importantes:</span><span class="sxs-lookup"><span data-stu-id="abced-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="abced-154">"destinationAddressPrefix" - reglas pueden usar un tipo especial de prefijo de dirección denominado "Etiqueta predeterminada", estas etiquetas son identificadores proporcionados por el sistema que permiten una tooaddress fácilmente una categoría mayor de prefijos de dirección.</span><span class="sxs-lookup"><span data-stu-id="abced-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="abced-155">Esta regla usa Hola etiqueta predeterminado "Internet" toosignify cualquiera de las direcciones fuera Hola red virtual.</span><span class="sxs-lookup"><span data-stu-id="abced-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="abced-156">Otras etiquetas de prefijo son VirtualNetwork y AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="abced-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="abced-157">"Direction" indica en qué dirección del flujo de tráfico esta entrada surte efecto.</span><span class="sxs-lookup"><span data-stu-id="abced-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="abced-158">dirección de Hello es desde la perspectiva de Hola de subred de Hola o una máquina Virtual (en función de donde está enlazado este GSN).</span><span class="sxs-lookup"><span data-stu-id="abced-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="abced-159">Por lo tanto si dirección es "Inbound" y está accediendo al tráfico de subred de Hola, Hola regla se aplicará y tráfico que sale de la subred de hello no se verían afectado por esta regla.</span><span class="sxs-lookup"><span data-stu-id="abced-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="abced-160">"Priority" establece el orden de hello en el que se evalúa un flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="abced-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="abced-161">Hola inferior Hola número Hola Hola prioridad.</span><span class="sxs-lookup"><span data-stu-id="abced-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="abced-162">Cuando una regla aplica tooa flujo de tráfico específico, no se procesa ninguna otra regla.</span><span class="sxs-lookup"><span data-stu-id="abced-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="abced-163">Por tanto, si una regla con prioridad 1 permite el tráfico y una regla con prioridad 2 deniega el tráfico y ambas reglas aplican tootraffic, ¿se permite el tráfico de hello tooflow (puesto regla 1 no tenía una prioridad más alta entra en vigor y no se aplica ninguna otra regla).</span><span class="sxs-lookup"><span data-stu-id="abced-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="abced-164">"Access" indica si se bloquea ("Deny") o se permite ("Allow") el tráfico al que afecta esta regla.</span><span class="sxs-lookup"><span data-stu-id="abced-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="abced-165">Esta regla permite tooflow de tráfico RDP de hello internet toohello el puerto RDP en cualquier servidor de hello enlazado subred.</span><span class="sxs-lookup"><span data-stu-id="abced-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="abced-166">Esta regla permite que servidor de web de hello toohit de tráfico de internet entrante.</span><span class="sxs-lookup"><span data-stu-id="abced-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="abced-167">Esta regla no cambia el comportamiento de enrutamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="abced-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="abced-168">regla de Hello solo permite el tráfico destinado a IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="abced-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="abced-169">Por lo tanto si el tráfico de Internet Hola tenía el servidor de web de hello como su destino de esta regla se permitirlo y detener el procesamiento de más reglas.</span><span class="sxs-lookup"><span data-stu-id="abced-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="abced-170">(En la regla de hello con prioridad 140 todos los demás tráfico entrante de internet se bloquea).</span><span class="sxs-lookup"><span data-stu-id="abced-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="abced-171">Si sólo está procesando el tráfico HTTP, esta regla podría ser más restringido tooonly Permitir destino puerto 80.</span><span class="sxs-lookup"><span data-stu-id="abced-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="abced-172">Esta regla permite toopass de tráfico desde el servidor de hello IIS01 toohello AppVM01 server, una regla posterior bloquea todo el tráfico de otros tooBackend front-end.</span><span class="sxs-lookup"><span data-stu-id="abced-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="abced-173">tooimprove esta regla, si se conoce el puerto de Hola que debe agregarse.</span><span class="sxs-lookup"><span data-stu-id="abced-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="abced-174">Por ejemplo, si el servidor IIS de hello está alcanzando solo SQL Server en AppVM01, intervalo de puertos de destino de hello debe cambiarse de "*" (Any) too1433 (Hola puerto de SQL) lo que permite una menor superficie expuesta a ataques entrantes en AppVM01 debe alguna vez verse comprometida la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="abced-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="abced-175">Esta regla deniega el tráfico de los servidores de tooany de internet de hello en red Hola.</span><span class="sxs-lookup"><span data-stu-id="abced-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="abced-176">Con las reglas de hello en prioridad 110 y 120, el efecto de hello es tooallow solo internet tráfico toohello firewall de entrada y puertos RDP en servidores y todo lo demás bloquea.</span><span class="sxs-lookup"><span data-stu-id="abced-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="abced-177">Esta regla es la regla de notificaciones de "error" tooblock todos los flujos inesperados.</span><span class="sxs-lookup"><span data-stu-id="abced-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="abced-178">regla de final de Hello deniega el tráfico de subred de back-end de hello front-end subred toohello.</span><span class="sxs-lookup"><span data-stu-id="abced-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="abced-179">Puesto que esta regla es una regla de sola entrada, se permite el tráfico inverso (de hello back-end toohello front-end).</span><span class="sxs-lookup"><span data-stu-id="abced-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="abced-180">Escenarios de tráfico</span><span class="sxs-lookup"><span data-stu-id="abced-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="abced-181">(*Permitido*) servidor de Internet tooweb</span><span class="sxs-lookup"><span data-stu-id="abced-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="abced-182">Un usuario de internet solicita una página HTTP desde la dirección IP pública de Hola de hello que NIC asociada con hello IIS01 NIC</span><span class="sxs-lookup"><span data-stu-id="abced-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="abced-183">dirección IP pública de Hello pasa tráfico toohello red virtual hacia IIS01 (servidor web de hello)</span><span class="sxs-lookup"><span data-stu-id="abced-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="abced-184">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="abced-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="abced-185">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="abced-186">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="abced-187">Aplicar NSG regla 3 (tooIIS01 Internet), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="abced-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="abced-188">Tráfico alcanza el dirección IP interna del servidor web de hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="abced-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="abced-189">Iis01 escucha el tráfico de web, recibe esta solicitud y comienza a procesar la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="abced-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="abced-190">Iis01 pide Hola SQL Server en AppVM01 información</span><span class="sxs-lookup"><span data-stu-id="abced-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="abced-191">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="abced-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="abced-192">subred de back-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="abced-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="abced-193">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="abced-194">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="abced-195">Regla de NSG 3 (tooFirewall Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="abced-196">Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="abced-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="abced-197">AppVM01 recibe Hola consulta SQL y responde</span><span class="sxs-lookup"><span data-stu-id="abced-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="abced-198">Dado que no hay ninguna regla de salida en la subred de back-end de hello, se permite la respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="abced-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="abced-199">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="abced-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="abced-200">No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola</span><span class="sxs-lookup"><span data-stu-id="abced-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="abced-201">Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="abced-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="abced-202">servidor IIS de Hello recibe la respuesta SQL de Hola y completa respuesta HTTP de Hola y envía toohello solicitante</span><span class="sxs-lookup"><span data-stu-id="abced-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="abced-203">Dado que no hay ninguna regla de salida en la subred de front-end de hello, se permite la respuesta de Hola y Hola usuario de Internet recibe hello web página solicitada.</span><span class="sxs-lookup"><span data-stu-id="abced-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="abced-204">(*Permitido*) servidor de tooIIS RDP</span><span class="sxs-lookup"><span data-stu-id="abced-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="abced-205">Un administrador del servidor en internet solicita un tooIIS01 de sesión RDP en la dirección IP pública de Hola de hello que NIC asociada con hello NIC IIS01 (se puede encontrar esta dirección IP pública a través de hello Portal o PowerShell)</span><span class="sxs-lookup"><span data-stu-id="abced-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="abced-206">dirección IP pública de Hello pasa tráfico toohello red virtual hacia IIS01 (servidor web de hello)</span><span class="sxs-lookup"><span data-stu-id="abced-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="abced-207">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="abced-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="abced-208">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="abced-209">Se aplica la regla 2 (RDP) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="abced-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="abced-210">No hay reglas de salida, se aplican las reglas predeterminadas y se permite el tráfico de retorno.</span><span class="sxs-lookup"><span data-stu-id="abced-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="abced-211">La sesión RDP está habilitada.</span><span class="sxs-lookup"><span data-stu-id="abced-211">RDP session is enabled</span></span>
6. <span data-ttu-id="abced-212">Mensajes de iis01 Hola nombre de usuario y contraseña</span><span class="sxs-lookup"><span data-stu-id="abced-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="abced-213">servidores de back-end de tooRDP tooany en este caso, el servidor IIS de Hola se utiliza como un "cuadro salto".</span><span class="sxs-lookup"><span data-stu-id="abced-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="abced-214">Primer servidor RDP toohello IIS y, a continuación, desde el servidor de hello IIS Server RDP toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="abced-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="abced-215">(*Permitido*) Búsqueda de DNS del servidor web en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="abced-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="abced-216">Web necesidades de servidor, IIS01, fuente de distribución de datos en www.data.gov, pero necesita tooresolve Hola dirección.</span><span class="sxs-lookup"><span data-stu-id="abced-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="abced-217">Hola configuración de red para las listas de red virtual de hello DNS01 (10.0.2.4 de subred de back-end de hello) como servidor DNS principal de hello, IIS01 envía Hola DNS solicitud tooDNS01</span><span class="sxs-lookup"><span data-stu-id="abced-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="abced-218">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="abced-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="abced-219">La subred back-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="abced-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="abced-220">Se aplica la regla 1 (DNS) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="abced-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="abced-221">Servidor DNS recibe la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="abced-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="abced-222">Servidor DNS no tiene dirección de hello en caché y pide un servidor DNS raíz en hello internet</span><span class="sxs-lookup"><span data-stu-id="abced-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="abced-223">No hay reglas de salida en la subred back-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="abced-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="abced-224">Se responde el servidor DNS de Internet, ya que esta sesión se ha iniciado internamente, se permite la respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="abced-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="abced-225">Servidor DNS almacena en caché la respuesta de Hola y responde tooIIS01 de espera de solicitud inicial toohello</span><span class="sxs-lookup"><span data-stu-id="abced-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="abced-226">No hay reglas de salida en la subred back-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="abced-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="abced-227">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="abced-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="abced-228">No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola</span><span class="sxs-lookup"><span data-stu-id="abced-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="abced-229">Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico por lo que se permite el tráfico de Hola</span><span class="sxs-lookup"><span data-stu-id="abced-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="abced-230">Iis01 recibe respuesta hello DNS01</span><span class="sxs-lookup"><span data-stu-id="abced-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="abced-231">(*Permitido*) Archivo de acceso del servidor web en AppVM01</span><span class="sxs-lookup"><span data-stu-id="abced-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="abced-232">IIS01 solicita un archivo en AppVM01</span><span class="sxs-lookup"><span data-stu-id="abced-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="abced-233">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="abced-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="abced-234">subred de back-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="abced-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="abced-235">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="abced-236">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="abced-237">Regla de NSG 3 (tooIIS01 Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="abced-238">Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="abced-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="abced-239">AppVM01 recibe la solicitud de Hola y responde con el archivo (suponiendo que se autoriza el acceso)</span><span class="sxs-lookup"><span data-stu-id="abced-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="abced-240">Dado que no hay ninguna regla de salida en la subred de back-end de hello, se permite la respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="abced-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="abced-241">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="abced-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="abced-242">No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola</span><span class="sxs-lookup"><span data-stu-id="abced-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="abced-243">Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="abced-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="abced-244">servidor IIS de Hello recibe el archivo hello</span><span class="sxs-lookup"><span data-stu-id="abced-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="abced-245">(*Denegado*) toobackend RDP</span><span class="sxs-lookup"><span data-stu-id="abced-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="abced-246">Un usuario de internet intenta tooRDP tooserver AppVM01</span><span class="sxs-lookup"><span data-stu-id="abced-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="abced-247">Dado que no hay ninguna dirección IP pública asociada a esta NIC de servidores, este tráfico nunca escribiría Hola red virtual y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="abced-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="abced-248">Sin embargo, si se habilitó una dirección IP pública por algún motivo, la regla de NSG 2 (RDP) permitiría este tráfico.</span><span class="sxs-lookup"><span data-stu-id="abced-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="abced-249">servidores de back-end de tooRDP tooany en este caso, el servidor IIS de Hola se utiliza como un "cuadro salto".</span><span class="sxs-lookup"><span data-stu-id="abced-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="abced-250">Primer servidor RDP toohello IIS y, a continuación, desde el servidor de hello IIS Server RDP toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="abced-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="abced-251">(*Denegado*) servidor de Web toobackend</span><span class="sxs-lookup"><span data-stu-id="abced-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="abced-252">Un usuario de internet trata de un archivo en AppVM01 tooaccess</span><span class="sxs-lookup"><span data-stu-id="abced-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="abced-253">Dado que no hay ninguna dirección IP pública asociada a esta NIC de servidores, este tráfico nunca escribiría Hola red virtual y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="abced-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="abced-254">Si ha habilitado una dirección IP pública por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico</span><span class="sxs-lookup"><span data-stu-id="abced-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="abced-255">(*Denegado*) Búsqueda de DNS web en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="abced-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="abced-256">Un usuario de internet intenta toolook un registro de DNS interna en DNS01</span><span class="sxs-lookup"><span data-stu-id="abced-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="abced-257">Dado que no hay ninguna dirección IP pública asociada a esta NIC de servidores, este tráfico nunca escribiría Hola red virtual y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="abced-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="abced-258">Si ha habilitado una dirección IP pública por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico (Nota: 1 de la regla (DNS) no aplicaría porque Hola solicita la dirección de origen es Hola internet y de la regla 1 solo se aplica toohello red virtual local como origen de hello)</span><span class="sxs-lookup"><span data-stu-id="abced-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="abced-259">(*Denegado*) el acceso a SQL en el servidor web de Hola</span><span class="sxs-lookup"><span data-stu-id="abced-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="abced-260">Un usuario de Internet solicita datos SQL de IIS01</span><span class="sxs-lookup"><span data-stu-id="abced-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="abced-261">Dado que no hay ninguna dirección IP pública asociada a esta NIC de servidores, este tráfico nunca escribiría Hola red virtual y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="abced-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="abced-262">Si ha habilitado una dirección IP pública por algún motivo, subred de front-end de hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="abced-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="abced-263">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="abced-264">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="abced-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="abced-265">Aplicar NSG regla 3 (tooIIS01 Internet), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="abced-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="abced-266">Tráfico alcanza el dirección IP interna de hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="abced-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="abced-267">Iis01 no está escuchando en el puerto 1433, por lo que no hay ninguna solicitud de toohello de respuesta</span><span class="sxs-lookup"><span data-stu-id="abced-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="abced-268">Conclusión</span><span class="sxs-lookup"><span data-stu-id="abced-268">Conclusion</span></span>
<span data-ttu-id="abced-269">En este ejemplo es una forma relativamente simple y sencillo de aislar la subred de back-end de Hola de tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="abced-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="abced-270">Puede encontrar más ejemplos y una descripción general de los límites de seguridad de red [aquí][HOME].</span><span class="sxs-lookup"><span data-stu-id="abced-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="abced-271">Referencias</span><span class="sxs-lookup"><span data-stu-id="abced-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="abced-272">Plantilla del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="abced-272">Azure Resource Manager template</span></span>
<span data-ttu-id="abced-273">Este ejemplo usa una plantilla predefinida de administrador de recursos de Azure en un repositorio de GitHub mantenido por Microsoft y abra toohello Comunidad.</span><span class="sxs-lookup"><span data-stu-id="abced-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="abced-274">Esta plantilla puede implementarse sin desviarse para extraerla de GitHub, o descarga y modifica toofit sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="abced-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="abced-275">plantilla principal de Hello es en el archivo hello denominado "azuredeploy.json."</span><span class="sxs-lookup"><span data-stu-id="abced-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="abced-276">Esta plantilla puede enviarse a través de PowerShell o CLI (con el archivo de asociados "azuredeploy.parameters.json" hello) toodeploy esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="abced-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="abced-277">Opino que hello más fácil es forma toouse Hola botón "Implementar tooAzure" en la página de README.md hello en GitHub.</span><span class="sxs-lookup"><span data-stu-id="abced-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="abced-278">plantilla de hello toodeploy que se basa en este ejemplo de GitHub y Hola portal de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="abced-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="abced-279">Desde un explorador, navegue toohello [plantilla][Template]</span><span class="sxs-lookup"><span data-stu-id="abced-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="abced-280">Haga clic en botón de "Implementar tooAzure" hello (u Hola "Visualizar" botón toosee una representación gráfica de esta plantilla)</span><span class="sxs-lookup"><span data-stu-id="abced-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="abced-281">Escriba Hola cuenta de almacenamiento, el nombre de usuario y la contraseña en la hoja de parámetros de hello, a continuación, haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="abced-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="abced-282">Cree un grupo de recursos para esta implementación (puede usar uno existente, pero se recomienda una nueva contraseña para obtener los mejores resultados).</span><span class="sxs-lookup"><span data-stu-id="abced-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="abced-283">Si es necesario, cambiar la configuración de suscripción y la ubicación de hello para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="abced-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="abced-284">Haga clic en **revisar los términos legales**, lea los términos de Hola y haga clic en **compra** tooagree.</span><span class="sxs-lookup"><span data-stu-id="abced-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="abced-285">Haga clic en **crear** implementación de hello toobegin de esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="abced-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="abced-286">Una vez finalizada correctamente la implementación hello, navegue toohello que creará el grupo de recursos para esta implementación toosee Hola los recursos configurados dentro.</span><span class="sxs-lookup"><span data-stu-id="abced-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="abced-287">Esta plantilla permite a solo servidor RDP toohello IIS01 (Buscar Hola IP pública para IIS01 en hello Portal).</span><span class="sxs-lookup"><span data-stu-id="abced-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="abced-288">servidores de back-end de tooRDP tooany en este caso, el servidor IIS de Hola se utiliza como un "cuadro salto".</span><span class="sxs-lookup"><span data-stu-id="abced-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="abced-289">Primer servidor RDP toohello IIS y, a continuación, desde el servidor de hello IIS Server RDP toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="abced-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="abced-290">tooremove esta implementación, Hola eliminar grupo de recursos y todos los recursos secundarios también se eliminarán.</span><span class="sxs-lookup"><span data-stu-id="abced-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="abced-291">Scripts de aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="abced-291">Sample application scripts</span></span>
<span data-ttu-id="abced-292">Una vez que la plantilla de Hola se ejecuta correctamente, puede configurar hello web y servidor de aplicaciones con una tooallow de aplicación web simple pruebas con esta configuración de red Perimetral.</span><span class="sxs-lookup"><span data-stu-id="abced-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="abced-293">tooinstall una aplicación de ejemplo para este y otros ejemplos de la red Perimetral, se aplicó en hello siguiente vínculo: [Script de aplicación de ejemplo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="abced-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="abced-294">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abced-294">Next steps</span></span>

* <span data-ttu-id="abced-295">Implementar este ejemplo</span><span class="sxs-lookup"><span data-stu-id="abced-295">Deploy this example</span></span>
* <span data-ttu-id="abced-296">Compilar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="abced-296">Build hello sample application</span></span>
* <span data-ttu-id="abced-297">Probar los flujos de tráfico distintos a través de esta red perimetral</span><span class="sxs-lookup"><span data-stu-id="abced-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Red perimetral de entrada con grupo de seguridad de red"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md