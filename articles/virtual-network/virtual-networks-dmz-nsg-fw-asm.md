---
title: 'aaaDMZ ejemplo: crear una red Perimetral tooprotect aplicaciones con un Firewall y los NSG | Documentos de Microsoft'
description: "Creación de una red perimetral con un firewall y grupos de seguridad de red (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="ca580-103">Ejemplo 2: crear una red Perimetral tooprotect aplicaciones con un Firewall y los NSG</span><span class="sxs-lookup"><span data-stu-id="ca580-103">Example 2 – Build a DMZ tooprotect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="ca580-104">[Devolver toohello página de prácticas recomendadas de seguridad límite][HOME]</span><span class="sxs-lookup"><span data-stu-id="ca580-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="ca580-105">En este ejemplo se creará una red perimetral con un firewall, cuatro servidores Windows y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="ca580-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="ca580-106">También guiará a través de cada uno de los tooprovide de comandos pertinentes de hello una comprensión más profunda de cada paso.</span><span class="sxs-lookup"><span data-stu-id="ca580-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="ca580-107">También hay un escenario de tráfico sección tooprovide una detallada paso a paso cómo tráfico pasa a través de las capas de defensa en Hola Hola red Perimetral.</span><span class="sxs-lookup"><span data-stu-id="ca580-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="ca580-108">Por último, en la sección de referencias de hello es código completo de Hola e instrucción toobuild este entorno tootest y experimentar con diferentes escenarios.</span><span class="sxs-lookup"><span data-stu-id="ca580-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="ca580-109">![Entrada de la red Perimetral con NVA y NSG][1]</span><span class="sxs-lookup"><span data-stu-id="ca580-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="ca580-110">Descripción del entorno</span><span class="sxs-lookup"><span data-stu-id="ca580-110">Environment Description</span></span>
<span data-ttu-id="ca580-111">En este ejemplo hay una suscripción que contiene Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca580-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="ca580-112">Dos servicios en la nube: "FrontEnd001" y "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="ca580-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="ca580-113">Una red virtual, CorpNetwork, con dos subredes: FrontEnd y BackEnd</span><span class="sxs-lookup"><span data-stu-id="ca580-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="ca580-114">Un único grupo de seguridad de red que está aplicada tooboth subredes</span><span class="sxs-lookup"><span data-stu-id="ca580-114">A single Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="ca580-115">Un dispositivo de red virtual, en este ejemplo, un NextGen Firewall Barracuda, conectado toohello subred de front-end</span><span class="sxs-lookup"><span data-stu-id="ca580-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected toohello Frontend subnet</span></span>
* <span data-ttu-id="ca580-116">Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="ca580-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="ca580-117">Dos servidores Windows que representan servidores back-end de aplicaciones (“AppVM01”, “AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="ca580-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="ca580-118">Un servidor Windows que representa un servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="ca580-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="ca580-119">Aunque en este ejemplo usa un NextGen Firewall Barracuda, muchos de los diferentes dispositivos de red Virtual podría utilizarse para este ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-119">Although this example uses a Barracuda NextGen Firewall, many of hello different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="ca580-120">En la sección de referencias de Hola a continuación hay un script de PowerShell que se compilará la mayor parte del entorno de Hola que se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ca580-120">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="ca580-121">Hola de crear las máquinas virtuales y redes virtuales, aunque se realizan mediante el script de ejemplo de Hola, no se describen en detalle en este documento.</span><span class="sxs-lookup"><span data-stu-id="ca580-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="ca580-122">entorno de Hola toobuild:</span><span class="sxs-lookup"><span data-stu-id="ca580-122">toobuild hello environment:</span></span>

1. <span data-ttu-id="ca580-123">Guardar archivo de xml de configuración Hola red incluido en la sección de referencias de hello (actualizada con nombres, la ubicación y el escenario de hello dada de toomatch de direcciones IP)</span><span class="sxs-lookup"><span data-stu-id="ca580-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="ca580-124">Variables de usuario de actualización hello en hello toomatch Hola entorno Hola de script es toobe ejecutarán (suscripciones, los nombres de servicio, etcetera)</span><span class="sxs-lookup"><span data-stu-id="ca580-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="ca580-125">Ejecutar script de Hola en PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca580-125">Execute hello script in PowerShell</span></span>

<span data-ttu-id="ca580-126">**Tenga en cuenta**: región Hola indicado en el script de PowerShell de hello debe coincidir con la región Hola indicado en el archivo de xml de configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-126">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="ca580-127">Una vez que el script de Hola se ejecuta correctamente puede tener Hola siguiendo los pasos posteriores a la secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="ca580-127">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="ca580-128">Configurar reglas de firewall de hello, este tema se trata en la sección de hello siguiente titulada: las reglas de Firewall.</span><span class="sxs-lookup"><span data-stu-id="ca580-128">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="ca580-129">Opcionalmente, en la sección de referencias de hello son dos tooset de secuencias de comandos de hello web y servidor de aplicaciones con una tooallow de aplicación web simple pruebas con esta configuración de red Perimetral.</span><span class="sxs-lookup"><span data-stu-id="ca580-129">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="ca580-130">Hola próxima sección explica la mayoría de las secuencias de comandos de hello instrucciones relativa tooNetwork grupos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ca580-130">hello next section explains most of hello scripts statements relative tooNetwork Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="ca580-131">Grupos de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="ca580-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="ca580-132">En este ejemplo, se crea un grupo de grupos de seguridad de red y después se carga con seis reglas.</span><span class="sxs-lookup"><span data-stu-id="ca580-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="ca580-133">Por lo general, debe crear primero las reglas específicas de "Permitir" y, a continuación, Hola reglas más genéricas de "Denegar" última.</span><span class="sxs-lookup"><span data-stu-id="ca580-133">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="ca580-134">Hola tenga asignada la prioridad determina qué reglas se evalúan primero.</span><span class="sxs-lookup"><span data-stu-id="ca580-134">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="ca580-135">Una vez que el tráfico se encuentra la regla específica de tooapply tooa, no se evalúa ninguna otra regla.</span><span class="sxs-lookup"><span data-stu-id="ca580-135">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="ca580-136">Se pueden aplicar reglas NSG en la vista en hello dirección entrante o saliente (desde la perspectiva de Hola de subred de hello).</span><span class="sxs-lookup"><span data-stu-id="ca580-136">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="ca580-137">Mediante declaración, se regeneran Hola siguiendo las reglas para el tráfico entrante:</span><span class="sxs-lookup"><span data-stu-id="ca580-137">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="ca580-138">Se permite el tráfico DNS interno (puerto 53)</span><span class="sxs-lookup"><span data-stu-id="ca580-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="ca580-139">Se permite el tráfico RDP (puerto 3389) de hello Internet tooany VM</span><span class="sxs-lookup"><span data-stu-id="ca580-139">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="ca580-140">Se permite el tráfico HTTP (puerto 80) de hello Internet toohello NVA (firewall)</span><span class="sxs-lookup"><span data-stu-id="ca580-140">HTTP traffic (port 80) from hello Internet toohello NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="ca580-141">Se permite cualquier tráfico (todos los puertos) del IIS01 tooAppVM1</span><span class="sxs-lookup"><span data-stu-id="ca580-141">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="ca580-142">Todo (todos los puertos) el tráfico de hello Internet toohello se deniega todo red virtual (tanto en las subredes)</span><span class="sxs-lookup"><span data-stu-id="ca580-142">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="ca580-143">Se deniega todo (todos los puertos) el tráfico de subred de back-end de hello front-end subred toohello</span><span class="sxs-lookup"><span data-stu-id="ca580-143">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="ca580-144">Con estas subredes de enlazado tooeach reglas, si una solicitud HTTP es entrante desde el servidor web de hello Internet toohello, ambas reglas 3 (permitir) y 5 (denegar) aplicaría, pero dado que la regla 3 tiene mayor prioridad solo aplicaría y regla 5 podría no entran en juego.</span><span class="sxs-lookup"><span data-stu-id="ca580-144">With these rules bound tooeach subnet, if a HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="ca580-145">Por lo tanto solicitud Hola HTTP podría permitirse toohello firewall.</span><span class="sxs-lookup"><span data-stu-id="ca580-145">Thus hello HTTP request would be allowed toohello firewall.</span></span> <span data-ttu-id="ca580-146">Si ese mismo tráfico estaba intentando server DNS01 de tooreach hello, regla 5 (Deny) sería Hola primera hello y tooapply el tráfico no estarían permitido a toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="ca580-146">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="ca580-147">Regla 6 (Deny) bloques Hola front-end de subred hablando de la subred de back-end de toohello (excepto el tráfico permitido en las reglas 1 y 4), esto protege la red de back-end de hello en caso de que un atacante pone en peligro hello web aplicación en hello front-end, tendría atacante Hola acceso limitado toohello back-end "protegido" red (solo tooresources expuesta en el servidor de hello AppVM01).</span><span class="sxs-lookup"><span data-stu-id="ca580-147">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="ca580-148">Hay una regla de salida predeterminada que permite el tráfico de salida toohello internet.</span><span class="sxs-lookup"><span data-stu-id="ca580-148">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="ca580-149">En este ejemplo, permitimos el tráfico saliente y no modificamos las reglas de salida.</span><span class="sxs-lookup"><span data-stu-id="ca580-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="ca580-150">toolock hacia abajo el tráfico en ambas direcciones, enrutamiento de definido por usuario es obligatorio, esto se explora en otro ejemplo que puede encontrar en hello [documento de límite de seguridad principal][HOME].</span><span class="sxs-lookup"><span data-stu-id="ca580-150">toolock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in hello [main security boundary document][HOME].</span></span>

<span data-ttu-id="ca580-151">las reglas NSG de Hello anterior descrito son reglas NSG toohello muy similares en [ejemplo 1: crear una red Perimetral Simple con NSG][Example1].</span><span class="sxs-lookup"><span data-stu-id="ca580-151">hello above discussed NSG rules are very similar toohello NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="ca580-152">Revise hello NSG descripción en ese documento para una visión detallada de cada regla NSG y sus atributos.</span><span class="sxs-lookup"><span data-stu-id="ca580-152">Please review hello NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="ca580-153">Reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="ca580-153">Firewall Rules</span></span>
<span data-ttu-id="ca580-154">Un cliente de administración deberá toobe instalado en un servidor de seguridad de PC toomanage hello y crear configuraciones de hello necesarias.</span><span class="sxs-lookup"><span data-stu-id="ca580-154">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="ca580-155">Vea proveedor de documentación de su firewall (o en otro NVA) hello en cómo toomanage Hola dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ca580-155">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="ca580-156">resto Hola de esta sección describe la configuración Hola de firewall de hello, a través del cliente de administración de proveedores de hello (es decir, no Hola portal de Azure o PowerShell).</span><span class="sxs-lookup"><span data-stu-id="ca580-156">hello remainder of this section will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="ca580-157">Instrucciones para la descarga de cliente y conexión toohello Barracuda utilizado en este ejemplo pueden encontrarse aquí: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="ca580-157">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="ca580-158">En firewall de hello, las reglas de reenvío debe toobe creado.</span><span class="sxs-lookup"><span data-stu-id="ca580-158">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="ca580-159">Dado que este ejemplo solo enruta el tráfico de entrada toohello firewall de internet y, a continuación, el servidor de web de toohello, se necesita reenvío solo una regla NAT.</span><span class="sxs-lookup"><span data-stu-id="ca580-159">Since this example only routes internet traffic in-bound toohello firewall and then toohello web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="ca580-160">En hello Barracuda NextGen Firewall utilizado en este Hola ejemplo regla sería una NAT de destino de regla "(Dst" NAT) toopass este tráfico.</span><span class="sxs-lookup"><span data-stu-id="ca580-160">On hello Barracuda NextGen Firewall used in this example hello rule would be a Destination NAT rule (“Dst NAT”) toopass this traffic.</span></span>

<span data-ttu-id="ca580-161">siguiente de hello toocreate regla (o comprobar las reglas existentes de forma predeterminada), a partir de panel de cliente de administración de dispositivo Barracuda NG hello, vaya la ficha de configuración de toohello, Hola configuración operativa sección, haga clic en el conjunto de reglas.</span><span class="sxs-lookup"><span data-stu-id="ca580-161">toocreate hello following rule (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="ca580-162">Llama a una cuadrícula, "Main reglas" mostrará Hola existente las reglas activas y desactivadas en firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-162">A grid called, “Main Rules” will show hello existing active and deactivated rules on hello firewall.</span></span> <span data-ttu-id="ca580-163">En hello superior derecha de esta cuadrícula es una pequeña, de color verde "+" botón, haga clic en este toocreate una nueva regla (Nota: el firewall puede "bloquear" para los cambios, si ve un botón de marca "Bloquear" y son no se puede toocreate o editar las reglas, haga clic en este botón demasiado "desbloquear" hello conjunto de reglas y permitir la edición).</span><span class="sxs-lookup"><span data-stu-id="ca580-163">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello ruleset and allow editing).</span></span> <span data-ttu-id="ca580-164">Si desea tooedit una regla existente, seleccione esa regla, haga clic en y seleccione Editar regla.</span><span class="sxs-lookup"><span data-stu-id="ca580-164">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="ca580-165">Cree una nueva regla y asígnele un nombre, como "WebTraffic".</span><span class="sxs-lookup"><span data-stu-id="ca580-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="ca580-166">icono de regla de NAT de destino de Hello tiene el siguiente aspecto: ![icono de NAT de destino][2]</span><span class="sxs-lookup"><span data-stu-id="ca580-166">hello Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="ca580-167">regla de Hello propio sería algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="ca580-167">hello rule itself would look something like this:</span></span>

<span data-ttu-id="ca580-168">![Regla de Firewall][3]</span><span class="sxs-lookup"><span data-stu-id="ca580-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="ca580-169">Aquí cualquier dirección entrante que aciertos Hola Firewall intentar tooreach HTTP (puerto 80 o 443 para HTTPS) se enviarán Hola interfaz "DHCP1 Local IP" del Firewall y redirigida toohello servidor Web con la dirección IP de 10.0.1.5 Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-169">Here any inbound address that hits hello Firewall trying tooreach HTTP (port 80 or 443 for HTTPS) will be sent out hello Firewall’s “DHCP1 Local IP” interface and redirected toohello Web Server with hello IP Address of 10.0.1.5.</span></span> <span data-ttu-id="ca580-170">Dado que el tráfico de hello próximas novedades en el puerto 80 en y en curso toohello web en el puerto 80 no se necesita ningún cambio de puerto.</span><span class="sxs-lookup"><span data-stu-id="ca580-170">Since hello traffic is coming in on port 80 and going toohello web server on port 80 no port change was needed.</span></span> <span data-ttu-id="ca580-171">Sin embargo, Hola lista de destino podrían haber resultado 10.0.1.5:8080 si el servidor Web escucha en el puerto 8080, por tanto, traducir Hola entrante del puerto 80 en hello firewall tooinbound puerto 8080 Hola servidor web.</span><span class="sxs-lookup"><span data-stu-id="ca580-171">However, hello Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating hello inbound port 80 on hello firewall tooinbound port 8080 on hello web server.</span></span>

<span data-ttu-id="ca580-172">Un método de conexión debe también ser indicado, para hello la regla de destino de hello Internet, "Dinámica SNAT" es el más adecuado.</span><span class="sxs-lookup"><span data-stu-id="ca580-172">A Connection Method should also be signified, for hello Destination Rule from hello Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="ca580-173">Aunque se creó una regla, es importante que su prioridad se establezca correctamente.</span><span class="sxs-lookup"><span data-stu-id="ca580-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="ca580-174">Si en la cuadrícula de Hola de todas las reglas de firewall de hello que esta nueva regla se encuentra en parte inferior de hello (debajo de la regla de "BLOCKALL" hello) nunca se entran en juego.</span><span class="sxs-lookup"><span data-stu-id="ca580-174">If in hello grid of all rules on hello firewall this new rule is on hello bottom (below hello "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="ca580-175">Asegúrese de regla Hola recién creada para el tráfico web está por encima de la regla BLOCKALL Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-175">Ensure hello newly created rule for web traffic is above hello BLOCKALL rule.</span></span>

<span data-ttu-id="ca580-176">Una vez que se crea la regla de hello, debe insertar toohello firewall y, a continuación, activar, si no es así regla Hola cambios no surtirán efecto.</span><span class="sxs-lookup"><span data-stu-id="ca580-176">Once hello rule is created, it must be pushed toohello firewall and then activated, if this is not done hello rule change will not take effect.</span></span> <span data-ttu-id="ca580-177">proceso de activación e inserción de Hola se describe en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-177">hello push and activation process is described in hello next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="ca580-178">Activación de reglas</span><span class="sxs-lookup"><span data-stu-id="ca580-178">Rule Activation</span></span>
<span data-ttu-id="ca580-179">Con hello ruleset modifica tooadd esta regla, debe ser Hola ruleset cargado toohello firewall y activado.</span><span class="sxs-lookup"><span data-stu-id="ca580-179">With hello ruleset modified tooadd this rule, hello ruleset must be uploaded toohello firewall and activated.</span></span>

<span data-ttu-id="ca580-180">![Activación de reglas de firewall][4]</span><span class="sxs-lookup"><span data-stu-id="ca580-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="ca580-181">En la esquina superior derecha de Hola de cliente de administración de hello son un clúster de botones.</span><span class="sxs-lookup"><span data-stu-id="ca580-181">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="ca580-182">Haga clic en firewall de Hola "enviar cambios" botón toosend Hola modificar reglas toohello, a continuación, haga clic en el botón de "Activar" Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-182">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="ca580-183">Con la activación de Hola de conjunto de reglas de firewall de hello esta compilación de entorno de ejemplo está completa.</span><span class="sxs-lookup"><span data-stu-id="ca580-183">With hello activation of hello firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="ca580-184">Si lo desea, scripts de compilación de post Hola Hola referencias sección puede ser ejecutan tooadd una aplicación toothis entorno tootest hello por debajo de los escenarios de tráfico.</span><span class="sxs-lookup"><span data-stu-id="ca580-184">Optionally, hello post build scripts in hello References section can be run tooadd an application toothis environment tootest hello below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca580-185">Es toorealize crítico que no alcanzará a servidor web de hello directamente.</span><span class="sxs-lookup"><span data-stu-id="ca580-185">It is critical toorealize that you will not hit hello web server directly.</span></span> <span data-ttu-id="ca580-186">Cuando un explorador solicita una página HTTP desde FrontEnd001.CloudApp.Net, pasadas de hello HTTP (puerto 80) del punto de conexión no Hola este tráfico toohello firewall del servidor web.</span><span class="sxs-lookup"><span data-stu-id="ca580-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, hello HTTP endpoint (port 80) passes this traffic toohello firewall not hello web server.</span></span> <span data-ttu-id="ca580-187">Hola firewall a continuación, según la regla de toohello creado anteriormente, NAT que solicitan toohello servidor Web.</span><span class="sxs-lookup"><span data-stu-id="ca580-187">hello firewall then, according toohello rule created above, NATs that request toohello Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="ca580-188">Escenarios de tráfico</span><span class="sxs-lookup"><span data-stu-id="ca580-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-tooweb-server-through-firewall"></a><span data-ttu-id="ca580-189">(Permitido) TooWeb Web Server a través del Firewall</span><span class="sxs-lookup"><span data-stu-id="ca580-189">(Allowed) Web tooWeb Server through Firewall</span></span>
1. <span data-ttu-id="ca580-190">El usuario de Internet solicita la página HTTP desde FrontEnd001.CloudApp.Net (servicio en la nube accesible desde Internet).</span><span class="sxs-lookup"><span data-stu-id="ca580-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="ca580-191">Fases de tráfico del servicio de nube a través de un extremo abierto en la interfaz local de toofirewall el puerto 80 en 10.0.1.4:80</span><span class="sxs-lookup"><span data-stu-id="ca580-191">Cloud service passes traffic through open endpoint on port 80 toofirewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="ca580-192">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="ca580-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ca580-193">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ca580-194">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="ca580-195">Aplicar NSG regla 3 (tooFirewall Internet), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="ca580-195">NSG Rule 3 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="ca580-196">Tráfico llega a dirección IP interna del servidor de seguridad de hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="ca580-196">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="ca580-197">Regla de reenvío de Firewall vea esto es tráfico en el puerto 80, se redirige el servidor web de toohello IIS01</span><span class="sxs-lookup"><span data-stu-id="ca580-197">Firewall forwarding rule see this is port 80 traffic, redirects it toohello web server IIS01</span></span>
6. <span data-ttu-id="ca580-198">Iis01 escucha el tráfico de web, recibe esta solicitud y comienza a procesar la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="ca580-198">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
7. <span data-ttu-id="ca580-199">Iis01 pide Hola SQL Server en AppVM01 información</span><span class="sxs-lookup"><span data-stu-id="ca580-199">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="ca580-200">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="ca580-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="ca580-201">subred de back-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="ca580-201">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ca580-202">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-202">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ca580-203">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-203">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="ca580-204">Regla de NSG 3 (tooFirewall Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-204">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="ca580-205">Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="ca580-205">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="ca580-206">AppVM01 recibe Hola consulta SQL y responde</span><span class="sxs-lookup"><span data-stu-id="ca580-206">AppVM01 receives hello SQL Query and responds</span></span>
11. <span data-ttu-id="ca580-207">Puesto que no hay ninguna regla de salida en hello respuesta de Hola de subred de back-end se permite</span><span class="sxs-lookup"><span data-stu-id="ca580-207">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
12. <span data-ttu-id="ca580-208">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="ca580-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ca580-209">No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola</span><span class="sxs-lookup"><span data-stu-id="ca580-209">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="ca580-210">Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-210">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
13. <span data-ttu-id="ca580-211">servidor IIS de Hello recibe la respuesta SQL de Hola y completa respuesta HTTP de Hola y envía toohello solicitante</span><span class="sxs-lookup"><span data-stu-id="ca580-211">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
14. <span data-ttu-id="ca580-212">Puesto que se trata de una sesión NAT de firewall de hello, destino de la respuesta de hello (inicialmente) es para hello Firewall</span><span class="sxs-lookup"><span data-stu-id="ca580-212">Since this is a NAT session from hello firewall, hello response destination (initially) is for hello Firewall</span></span>
15. <span data-ttu-id="ca580-213">firewall de Hello recibe respuesta Hola Hola servidor Web y reenvía toohello back-usuario de Internet</span><span class="sxs-lookup"><span data-stu-id="ca580-213">hello firewall receives hello response from hello Web Server and forwards back toohello Internet User</span></span>
16. <span data-ttu-id="ca580-214">Dado que hay no se permite ninguna regla de salida en respuesta de Hola de subred de front-end de Hola y Hola usuario de Internet recibe hello web página solicitada.</span><span class="sxs-lookup"><span data-stu-id="ca580-214">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="ca580-215">(Permitido) TooBackend RDP</span><span class="sxs-lookup"><span data-stu-id="ca580-215">(Allowed) RDP tooBackend</span></span>
1. <span data-ttu-id="ca580-216">Administrador del servidor en internet solicita tooAppVM01 de sesión RDP en BackEnd001.CloudApp.Net:xxxxx donde xxxxx es el número de puerto de hello asignada aleatoriamente para tooAppVM01 RDP (puerto Hola asignado se puede encontrar en hello Portal de Azure o a través de PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ca580-216">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="ca580-217">Desde Hola que Firewall sólo está escuchando en hello FrontEnd001.CloudApp.Net dirección no está implicado en este flujo de tráfico</span><span class="sxs-lookup"><span data-stu-id="ca580-217">Since hello Firewall is only listening on hello FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="ca580-218">La subred back-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="ca580-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ca580-219">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-219">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ca580-220">Se aplica la regla 2 (RDP) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="ca580-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="ca580-221">No hay reglas de salida, se aplican las reglas predeterminadas y se permite el tráfico de retorno.</span><span class="sxs-lookup"><span data-stu-id="ca580-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="ca580-222">La sesión RDP está habilitada.</span><span class="sxs-lookup"><span data-stu-id="ca580-222">RDP session is enabled</span></span>
6. <span data-ttu-id="ca580-223">AppVM01 solicita la contraseña del nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="ca580-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="ca580-224">(Permitido) Búsqueda de DNS del servidor web en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="ca580-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="ca580-225">Web necesidades de servidor, IIS01, fuente de distribución de datos en www.data.gov, pero necesita tooresolve Hola dirección.</span><span class="sxs-lookup"><span data-stu-id="ca580-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="ca580-226">Hola configuración de red para las listas de red virtual de hello DNS01 (10.0.2.4 de subred de back-end de hello) como servidor DNS principal de hello, IIS01 envía Hola DNS solicitud tooDNS01</span><span class="sxs-lookup"><span data-stu-id="ca580-226">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="ca580-227">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="ca580-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="ca580-228">La subred back-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="ca580-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ca580-229">Se aplica la regla 1 (DNS) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="ca580-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="ca580-230">Servidor DNS recibe la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="ca580-230">DNS server receives hello request</span></span>
6. <span data-ttu-id="ca580-231">Servidor DNS no tiene dirección de hello en caché y pide un servidor DNS raíz en hello internet</span><span class="sxs-lookup"><span data-stu-id="ca580-231">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="ca580-232">No hay reglas de salida en la subred back-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="ca580-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="ca580-233">Se responde el servidor DNS de Internet, ya que esta sesión se ha iniciado internamente, se permite la respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="ca580-233">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="ca580-234">Servidor DNS almacena en caché la respuesta de Hola y responde tooIIS01 de espera de solicitud inicial toohello</span><span class="sxs-lookup"><span data-stu-id="ca580-234">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="ca580-235">No hay reglas de salida en la subred back-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="ca580-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="ca580-236">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="ca580-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ca580-237">No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola</span><span class="sxs-lookup"><span data-stu-id="ca580-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="ca580-238">Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico por lo que se permite el tráfico de Hola</span><span class="sxs-lookup"><span data-stu-id="ca580-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="ca580-239">Iis01 recibe respuesta hello DNS01</span><span class="sxs-lookup"><span data-stu-id="ca580-239">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="ca580-240">(Permitido) Archivo de acceso del servidor web en AppVM01</span><span class="sxs-lookup"><span data-stu-id="ca580-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="ca580-241">IIS01 solicita un archivo en AppVM01</span><span class="sxs-lookup"><span data-stu-id="ca580-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="ca580-242">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="ca580-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="ca580-243">subred de back-end de Hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="ca580-243">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ca580-244">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-244">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ca580-245">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-245">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="ca580-246">Regla de NSG 3 (tooFirewall Internet) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-246">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="ca580-247">Aplicar NSG regla 4 (IIS01 tooAppVM01), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="ca580-247">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="ca580-248">AppVM01 recibe la solicitud de Hola y responde con el archivo (suponiendo que se autoriza el acceso)</span><span class="sxs-lookup"><span data-stu-id="ca580-248">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="ca580-249">Puesto que no hay ninguna regla de salida en hello respuesta de Hola de subred de back-end se permite</span><span class="sxs-lookup"><span data-stu-id="ca580-249">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
6. <span data-ttu-id="ca580-250">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="ca580-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ca580-251">No hay ninguna regla NSG que se aplica tooInbound tráfico de subred de front-end del toohello Hola de subred de back-end, por lo que no se aplica ninguno de reglas NSG Hola</span><span class="sxs-lookup"><span data-stu-id="ca580-251">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="ca580-252">Hola regla predeterminada del sistema permitiendo el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-252">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="ca580-253">servidor IIS de Hello recibe el archivo hello</span><span class="sxs-lookup"><span data-stu-id="ca580-253">hello IIS server receives hello file</span></span>

#### <a name="denied-web-direct-tooweb-server"></a><span data-ttu-id="ca580-254">(Denegado) TooWeb directo de Web Server</span><span class="sxs-lookup"><span data-stu-id="ca580-254">(Denied) Web direct tooWeb Server</span></span>
<span data-ttu-id="ca580-255">Desde hello Firewall, IIS01 y Hola servidor Web están en hello mismo servicio en la nube comparten Hola misma dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="ca580-255">Since hello Web Server, IIS01, and hello Firewall are in hello same Cloud Service they share hello same public facing IP address.</span></span> <span data-ttu-id="ca580-256">Por lo tanto se dirigirá todo el tráfico HTTP toohello firewall.</span><span class="sxs-lookup"><span data-stu-id="ca580-256">Thus any HTTP traffic would be directed toohello firewall.</span></span> <span data-ttu-id="ca580-257">Mientras que resultará usar correctamente la solicitud de hello, no se puede ir directamente a toohello servidor Web, pasa, según lo previsto, a través de Hola de Firewall en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="ca580-257">While hello request would be successfully served, it cannot go directly toohello Web Server, it passed, as designed, through hello Firewall first.</span></span> <span data-ttu-id="ca580-258">Vea Hola primer escenario de esta sección para el flujo de tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-258">See hello first Scenario in this section for hello traffic flow.</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="ca580-259">(Denegado) TooBackend Web Server</span><span class="sxs-lookup"><span data-stu-id="ca580-259">(Denied) Web tooBackend Server</span></span>
1. <span data-ttu-id="ca580-260">Usuario de Internet intenta tooaccess un archivo en AppVM01 a través de hello BackEnd001.CloudApp.Net servicio</span><span class="sxs-lookup"><span data-stu-id="ca580-260">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="ca580-261">Dado que no hay ningún extremo abierto para el recurso compartido de archivos, esto no sucedería Hola servicio en la nube y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="ca580-261">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="ca580-262">Si los puntos de conexión de hello estaban abiertos por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico</span><span class="sxs-lookup"><span data-stu-id="ca580-262">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="ca580-263">(Denegado) Búsqueda de DNS web en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="ca580-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="ca580-264">Usuario de Internet intenta toolookup un registro DNS interno en DNS01 a través de hello BackEnd001.CloudApp.Net servicio</span><span class="sxs-lookup"><span data-stu-id="ca580-264">Internet user tries toolookup an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="ca580-265">Dado que no hay ningún extremo abierto para DNS, esto no pasaría Hola servicio en la nube y no llegar a servidor hello</span><span class="sxs-lookup"><span data-stu-id="ca580-265">Since there are no endpoints open for DNS, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="ca580-266">Si los puntos de conexión de hello estaban abiertos por algún motivo, la regla de NSG 5 (Internet tooVNet) bloquearían este tráfico (Nota: esa regla 1 (DNS) no se aplicarían por dos motivos, primera dirección de origen de hello es Hola internet, esta regla solo aplica toohello red virtual local como Hola de origen, también se trata de una regla de permiso, por lo que nunca podría denegar el tráfico)</span><span class="sxs-lookup"><span data-stu-id="ca580-266">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="ca580-267">(Denegado) Acceso Web de tooSQL a través del Firewall</span><span class="sxs-lookup"><span data-stu-id="ca580-267">(Denied) Web tooSQL access through Firewall</span></span>
1. <span data-ttu-id="ca580-268">El usuario de Internet solicita los datos SQL desde FrontEnd001.CloudApp.Net (servicio en la nube accesible desde Internet).</span><span class="sxs-lookup"><span data-stu-id="ca580-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="ca580-269">Dado que no hay ningún extremo abierto para SQL, esto no sucedería Hola servicio en la nube y no llegar a firewall de Hola</span><span class="sxs-lookup"><span data-stu-id="ca580-269">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="ca580-270">Si los puntos de conexión estaban abiertos por algún motivo, subred de front-end de hello comienza el procesamiento de la regla de entrada:</span><span class="sxs-lookup"><span data-stu-id="ca580-270">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ca580-271">1 de la regla de NSG (DNS) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-271">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ca580-272">2 de la regla de NSG (RDP) no se aplica, mover toonext regla</span><span class="sxs-lookup"><span data-stu-id="ca580-272">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="ca580-273">Aplicar NSG regla 2 (tooFirewall Internet), el tráfico es el procesamiento de reglas permitidas, detenga</span><span class="sxs-lookup"><span data-stu-id="ca580-273">NSG Rule 2 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="ca580-274">Tráfico llega a dirección IP interna del servidor de seguridad de hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="ca580-274">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="ca580-275">Servidor de seguridad no tiene ninguna regla de reenvío para SQL y quita Hola tráfico</span><span class="sxs-lookup"><span data-stu-id="ca580-275">Firewall has no forwarding rules for SQL and drops hello traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="ca580-276">Conclusión</span><span class="sxs-lookup"><span data-stu-id="ca580-276">Conclusion</span></span>
<span data-ttu-id="ca580-277">Se trata de una manera relativamente sencillo de protección de su aplicación con un firewall y el aislamiento de la subred de back-end de Hola de tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="ca580-277">This is a relatively straight forward way of protecting your application with a firewall and isolating hello back end subnet from inbound traffic.</span></span>

<span data-ttu-id="ca580-278">Puede encontrar más ejemplos y una descripción general de los límites de seguridad de red [aquí][HOME].</span><span class="sxs-lookup"><span data-stu-id="ca580-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="ca580-279">Referencias</span><span class="sxs-lookup"><span data-stu-id="ca580-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="ca580-280">Script principal y configuración de red</span><span class="sxs-lookup"><span data-stu-id="ca580-280">Main Script and Network Config</span></span>
<span data-ttu-id="ca580-281">Guardar Hola Script completo en un archivo de script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca580-281">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="ca580-282">Guardar configuración de red de hello en un archivo denominado "NetworkConf2.xml".</span><span class="sxs-lookup"><span data-stu-id="ca580-282">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="ca580-283">Modifique las variables definidas por el usuario de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ca580-283">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="ca580-284">Ejecutar script de Hola, a continuación, siga anterior de instrucciones de instalación del regla de Firewall Hola.</span><span class="sxs-lookup"><span data-stu-id="ca580-284">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="ca580-285">Script completo</span><span class="sxs-lookup"><span data-stu-id="ca580-285">Full Script</span></span>
<span data-ttu-id="ca580-286">Este script superará en función de las variables definidas por el usuario de hello:</span><span class="sxs-lookup"><span data-stu-id="ca580-286">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="ca580-287">Conectar tooan suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="ca580-287">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="ca580-288">Creación de una cuenta de almacenamiento nueva</span><span class="sxs-lookup"><span data-stu-id="ca580-288">Create a new storage account</span></span>
3. <span data-ttu-id="ca580-289">Crear una red virtual nueva y dos subredes tal como se define en el archivo de configuración de red de Hola</span><span class="sxs-lookup"><span data-stu-id="ca580-289">Create a new VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="ca580-290">Creación de cuatro máquinas virtuales de servidor Windows</span><span class="sxs-lookup"><span data-stu-id="ca580-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="ca580-291">Configuración del grupo de seguridad de red, incluido lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ca580-291">Configure NSG including:</span></span>
   * <span data-ttu-id="ca580-292">Creación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="ca580-292">Creating a NSG</span></span>
   * <span data-ttu-id="ca580-293">Rellenado con reglas</span><span class="sxs-lookup"><span data-stu-id="ca580-293">Populating it with rules</span></span>
   * <span data-ttu-id="ca580-294">Enlace hello NSG toohello las subredes correspondientes</span><span class="sxs-lookup"><span data-stu-id="ca580-294">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="ca580-295">Este script de PowerShell debe ejecutarse localmente en un equipo o servidor conectado a Internet.</span><span class="sxs-lookup"><span data-stu-id="ca580-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca580-296">Cuando se ejecuta este script, puede haber advertencias u otros mensajes informativos que se muestran en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca580-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="ca580-297">Solo los mensajes de error indicados en rojo son motivo de preocupación.</span><span class="sxs-lookup"><span data-stu-id="ca580-297">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

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
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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


#### <a name="network-config-file"></a><span data-ttu-id="ca580-298">Archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="ca580-298">Network Config File</span></span>
<span data-ttu-id="ca580-299">Guarde este archivo xml con la ubicación actualizada y agregue Hola vínculo toothis toohello $NetworkConfigFile variable de archivos de script de Hola anterior.</span><span class="sxs-lookup"><span data-stu-id="ca580-299">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="ca580-300">Scripts de aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ca580-300">Sample Application Scripts</span></span>
<span data-ttu-id="ca580-301">Si desea tooinstall una aplicación de ejemplo para este y otros ejemplos de la red Perimetral, se aplicó en hello siguiente vínculo: [Script de aplicación de ejemplo][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="ca580-301">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Red perimetral de entrada con grupo de seguridad de red"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Icono de NAT de destino"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Regla de firewall"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Activación de reglas de firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
