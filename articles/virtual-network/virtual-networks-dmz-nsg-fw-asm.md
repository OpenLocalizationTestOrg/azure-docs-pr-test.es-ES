---
title: "Ejemplo de red perimetral: Creación de una red perimetral para proteger las aplicaciones con un Firewall y grupos de seguridad de red | Microsoft Docs"
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
ms.openlocfilehash: cc0e8a3fa749eb2e6f65ef92c2d3cb404cfc8bc0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="example-2--build-a-dmz-to-protect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="81d77-103">Ejemplo 2: Creación de una red perimetral para proteger las aplicaciones con un Firewall y grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="81d77-103">Example 2 – Build a DMZ to protect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="81d77-104">[Volver a la página de procedimientos recomendados de límites de seguridad][HOME]</span><span class="sxs-lookup"><span data-stu-id="81d77-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="81d77-105">En este ejemplo se creará una red perimetral con un firewall, cuatro servidores Windows y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="81d77-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="81d77-106">También le guiará por cada uno de los comandos pertinentes para que comprenda mejor cada paso.</span><span class="sxs-lookup"><span data-stu-id="81d77-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="81d77-107">Hay también una sección llamada "Escenario de tráfico" para proporcionar información detallada paso a paso de cómo pasa el tráfico a través de los niveles de defensa de la red perimetral.</span><span class="sxs-lookup"><span data-stu-id="81d77-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="81d77-108">Por último, en la sección de referencias está el código completo e instrucciones para crear este entorno para probar y experimentar con diferentes escenarios.</span><span class="sxs-lookup"><span data-stu-id="81d77-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="81d77-109">![Entrada de la red Perimetral con NVA y NSG][1]</span><span class="sxs-lookup"><span data-stu-id="81d77-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="81d77-110">Descripción del entorno</span><span class="sxs-lookup"><span data-stu-id="81d77-110">Environment Description</span></span>
<span data-ttu-id="81d77-111">En este ejemplo hay una suscripción que contiene lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="81d77-111">In this example there is a subscription that contains the following:</span></span>

* <span data-ttu-id="81d77-112">Dos servicios en la nube: "FrontEnd001" y "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="81d77-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="81d77-113">Una red virtual, CorpNetwork, con dos subredes: FrontEnd y BackEnd</span><span class="sxs-lookup"><span data-stu-id="81d77-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="81d77-114">Un único grupo de seguridad de red que se aplica a ambas subredes</span><span class="sxs-lookup"><span data-stu-id="81d77-114">A single Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="81d77-115">Un dispositivo virtual de red, en este ejemplo un firewall Barracuda NextGen, conectado a la subred front-end</span><span class="sxs-lookup"><span data-stu-id="81d77-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected to the Frontend subnet</span></span>
* <span data-ttu-id="81d77-116">Un servidor Windows que representa un servidor de aplicaciones web ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="81d77-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="81d77-117">Dos servidores Windows que representan servidores back-end de aplicaciones (“AppVM01”, “AppVM02”)</span><span class="sxs-lookup"><span data-stu-id="81d77-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="81d77-118">Un servidor Windows que representa un servidor DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="81d77-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="81d77-119">Aunque este ejemplo usa un firewall Barracuda NextGen, muchos de los distintos dispositivos virtuales de red podrían usarse para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="81d77-119">Although this example uses a Barracuda NextGen Firewall, many of the different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="81d77-120">En la sección de referencias siguiente hay un script de PowerShell que compilará la mayor parte del entorno descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="81d77-120">In the references section below there is a PowerShell script that will build most of the environment described above.</span></span> <span data-ttu-id="81d77-121">Aunque la creación de las máquinas virtuales y las redes virtuales la realiza el script de ejemplo, no se describe en detalle en este documento.</span><span class="sxs-lookup"><span data-stu-id="81d77-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span>

<span data-ttu-id="81d77-122">Para crear el entorno, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="81d77-122">To build the environment:</span></span>

1. <span data-ttu-id="81d77-123">Guarde el archivo xml de configuración de red incluido en la sección de referencias (actualizado con nombres, ubicación y direcciones IP para que coincidan con el escenario dado).</span><span class="sxs-lookup"><span data-stu-id="81d77-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="81d77-124">Actualice las variables de usuario en el script para que coincida con el entorno en el que se va a ejecutar el script (suscripciones, nombres de servicio, etc.).</span><span class="sxs-lookup"><span data-stu-id="81d77-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="81d77-125">Ejecución del script en PowerShell</span><span class="sxs-lookup"><span data-stu-id="81d77-125">Execute the script in PowerShell</span></span>

<span data-ttu-id="81d77-126">**Nota**: la región indicada en el script de PowerShell debe coincidir con la región indicada en el archivo xml de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="81d77-126">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>

<span data-ttu-id="81d77-127">Cuando el script se ejecuta correctamente, se pueden realizar los siguientes pasos posteriores al script:</span><span class="sxs-lookup"><span data-stu-id="81d77-127">Once the script runs successfully the following post-script steps may be taken:</span></span>

1. <span data-ttu-id="81d77-128">Configure las reglas de firewall, esto se trata en la sección siguiente denominada Reglas de firewall.</span><span class="sxs-lookup"><span data-stu-id="81d77-128">Set up the firewall rules, this is covered in the section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="81d77-129">Opcionalmente, en la sección de referencias hay dos scripts para configurar el servidor web y el servidor de aplicaciones con una aplicación web sencilla para permitir las pruebas con esta configuración de red perimetral.</span><span class="sxs-lookup"><span data-stu-id="81d77-129">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="81d77-130">La siguiente sección explica la mayor parte de las instrucciones de scripts relativas a los grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="81d77-130">The next section explains most of the scripts statements relative to Network Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="81d77-131">Grupos de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="81d77-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="81d77-132">En este ejemplo, se crea un grupo de grupos de seguridad de red y después se carga con seis reglas.</span><span class="sxs-lookup"><span data-stu-id="81d77-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="81d77-133">Por lo general, debe crear primero las reglas específicas de "Permitir" y, por último, las reglas de "Denegar" más genéricas.</span><span class="sxs-lookup"><span data-stu-id="81d77-133">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="81d77-134">La prioridad asignada indica qué reglas se evalúan primero.</span><span class="sxs-lookup"><span data-stu-id="81d77-134">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="81d77-135">Una vez que se encuentra el tráfico para aplicar a una regla específica, no se evalúa ninguna otra regla.</span><span class="sxs-lookup"><span data-stu-id="81d77-135">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="81d77-136">Se pueden aplicar reglas de grupo de seguridad de red en cualquier dirección, entrante o saliente (desde la perspectiva de la subred).</span><span class="sxs-lookup"><span data-stu-id="81d77-136">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
> 
> 

<span data-ttu-id="81d77-137">De forma declarativa, se compilan las reglas siguientes para el tráfico entrante:</span><span class="sxs-lookup"><span data-stu-id="81d77-137">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="81d77-138">Se permite el tráfico DNS interno (puerto 53)</span><span class="sxs-lookup"><span data-stu-id="81d77-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="81d77-139">Se permite el tráfico RDP (puerto 3389) desde Internet a cualquier máquina virtual</span><span class="sxs-lookup"><span data-stu-id="81d77-139">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="81d77-140">Se permite el tráfico HTTP (puerto 80) desde Internet a NVA (firewall)</span><span class="sxs-lookup"><span data-stu-id="81d77-140">HTTP traffic (port 80) from the Internet to the NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="81d77-141">Se permite cualquier tráfico (todos los puertos) desde IIS01 a AppVM1.</span><span class="sxs-lookup"><span data-stu-id="81d77-141">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="81d77-142">Se deniega todo el tráfico (todos los puertos) desde Internet a toda la red virtual (ambas subredes).</span><span class="sxs-lookup"><span data-stu-id="81d77-142">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="81d77-143">Se deniega todo el tráfico (todos los puertos) desde la subred front-end a la subred back-end.</span><span class="sxs-lookup"><span data-stu-id="81d77-143">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="81d77-144">Con estas reglas enlazadas a cada subred, si una solicitud HTTP era entrante desde Internet al servidor web, se aplicarían ambas reglas, la 3 (permitir) y la 5 (denegar), pero como la regla 3 tiene mayor prioridad, solo se aplicaría esa y la regla 5 no entraría en juego.</span><span class="sxs-lookup"><span data-stu-id="81d77-144">With these rules bound to each subnet, if a HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="81d77-145">Por lo tanto, se permitiría la solicitud HTTP al firewall.</span><span class="sxs-lookup"><span data-stu-id="81d77-145">Thus the HTTP request would be allowed to the firewall.</span></span> <span data-ttu-id="81d77-146">Si ese mismo tráfico estaba intentando ponerse en contacto con el servidor DNS01, se aplicaría primero la regla 5 (denegar) y no se permitiría que el tráfico pase al servidor.</span><span class="sxs-lookup"><span data-stu-id="81d77-146">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="81d77-147">La regla 6 (denegar) impide que la subred front-end se comunique con la subred back-end (excepto el tráfico permitido en las reglas 1 y 4) y esto protege la red back-end en el caso de que un atacante ponga en peligro la aplicación web en el front-end, y el atacante tendría acceso limitado a la red back-end "protegida" (solo a los recursos expuestos en el servidor AppVM01).</span><span class="sxs-lookup"><span data-stu-id="81d77-147">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="81d77-148">Hay una regla de salida predeterminada que permite el tráfico saliente a Internet.</span><span class="sxs-lookup"><span data-stu-id="81d77-148">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="81d77-149">En este ejemplo, permitimos el tráfico saliente y no modificamos las reglas de salida.</span><span class="sxs-lookup"><span data-stu-id="81d77-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="81d77-150">Para bloquear el tráfico en ambas direcciones, es necesario el enrutamiento definido por el usuario, que se explora en otro ejemplo que se puede encontrar en el [documento de límites de seguridad principales][HOME].</span><span class="sxs-lookup"><span data-stu-id="81d77-150">To lock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in the [main security boundary document][HOME].</span></span>

<span data-ttu-id="81d77-151">Las reglas del grupo de seguridad de red tratadas anteriormente son muy similares a las reglas del grupo de seguridad de red del [Ejemplo 1: Creación de una red perimetral simple con grupos de seguridad de red][Example1].</span><span class="sxs-lookup"><span data-stu-id="81d77-151">The above discussed NSG rules are very similar to the NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="81d77-152">Revise la descripción del grupo de seguridad de red en ese documento para una visión detallada de cada regla del grupo de seguridad de red y sus atributos.</span><span class="sxs-lookup"><span data-stu-id="81d77-152">Please review the NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="81d77-153">Reglas de firewall</span><span class="sxs-lookup"><span data-stu-id="81d77-153">Firewall Rules</span></span>
<span data-ttu-id="81d77-154">Deberá instalarse un cliente de administración en el equipo para administrar el firewall y crear las configuraciones necesarias.</span><span class="sxs-lookup"><span data-stu-id="81d77-154">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span></span> <span data-ttu-id="81d77-155">Consulte la documentación del proveedor de su firewall (o de otro dispositivo virtual de red) acerca de cómo administrar el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="81d77-155">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span></span> <span data-ttu-id="81d77-156">El resto de esta sección describe la configuración del mismo firewall, a través del cliente de administración de proveedores (es decir, no el Portal de Azure o PowerShell).</span><span class="sxs-lookup"><span data-stu-id="81d77-156">The remainder of this section will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span></span>

<span data-ttu-id="81d77-157">Puede encontrar instrucciones para descargar el cliente y conectarse al firewall Barracuda usado en este ejemplo aquí: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="81d77-157">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="81d77-158">En el firewall, deberán crearse reglas de reenvío.</span><span class="sxs-lookup"><span data-stu-id="81d77-158">On the firewall, forwarding rules will need to be created.</span></span> <span data-ttu-id="81d77-159">Como en este ejemplo solo se enruta el tráfico entrante de Internet al firewall y después al servidor web, únicamente se necesita un regla NAT de reenvío.</span><span class="sxs-lookup"><span data-stu-id="81d77-159">Since this example only routes internet traffic in-bound to the firewall and then to the web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="81d77-160">En el firewall de Barracuda NextGen usado en este ejemplo, la regla sería una regla NAT de destino ("Dst NAT") para pasar este tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-160">On the Barracuda NextGen Firewall used in this example the rule would be a Destination NAT rule (“Dst NAT”) to pass this traffic.</span></span>

<span data-ttu-id="81d77-161">Para crear la siguiente regla (o comprobar las reglas predeterminadas existentes), a partir del panel de cliente de Barracuda NG Admin, vaya a la pestaña de configuración, en la sección de configuración funcional, y haga clic en el conjunto de reglas.</span><span class="sxs-lookup"><span data-stu-id="81d77-161">To create the following rule (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="81d77-162">Una cuadrícula denominada "Main rules" (Reglas principales) mostrará las reglas activas existentes y las desactivadas en el firewall.</span><span class="sxs-lookup"><span data-stu-id="81d77-162">A grid called, “Main Rules” will show the existing active and deactivated rules on the firewall.</span></span> <span data-ttu-id="81d77-163">En la esquina superior derecha de esta cuadrícula hay un pequeño botón "+" de color verde; haga clic aquí para crear una nueva regla (Nota: el firewall puede estar "bloqueado" para los cambios; si ve un botón marcado con "Lock" (Bloquear) y no puede crear o editar reglas, haga clic en este botón para "desbloquear" el conjunto de reglas y permitir la modificación).</span><span class="sxs-lookup"><span data-stu-id="81d77-163">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the ruleset and allow editing).</span></span> <span data-ttu-id="81d77-164">Si quiere modificar una regla existente, seleccione esa regla, haga clic con el botón derecho y seleccione Edit Rule (Editar regla).</span><span class="sxs-lookup"><span data-stu-id="81d77-164">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="81d77-165">Cree una nueva regla y asígnele un nombre, como "WebTraffic".</span><span class="sxs-lookup"><span data-stu-id="81d77-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="81d77-166">El icono de regla de NAT de destino tiene el siguiente aspecto: ![icono de NAT de destino][2]</span><span class="sxs-lookup"><span data-stu-id="81d77-166">The Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="81d77-167">La regla debe tener un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="81d77-167">The rule itself would look something like this:</span></span>

<span data-ttu-id="81d77-168">![Regla de Firewall][3]</span><span class="sxs-lookup"><span data-stu-id="81d77-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="81d77-169">Aquí cualquier dirección entrante que alcanza el firewall que intenta llegar a HTTP (puerto 80 o 443 para HTTPS) se enviará fuera de interfaz de "DHCP1 Local IP" del firewall y se redirigirá al servidor web con la dirección IP de 10.0.1.5.</span><span class="sxs-lookup"><span data-stu-id="81d77-169">Here any inbound address that hits the Firewall trying to reach HTTP (port 80 or 443 for HTTPS) will be sent out the Firewall’s “DHCP1 Local IP” interface and redirected to the Web Server with the IP Address of 10.0.1.5.</span></span> <span data-ttu-id="81d77-170">Puesto que el tráfico entra en el puerto 80 y se dirige al servidor web en el puerto 80, no se necesita ningún cambio de puerto.</span><span class="sxs-lookup"><span data-stu-id="81d77-170">Since the traffic is coming in on port 80 and going to the web server on port 80 no port change was needed.</span></span> <span data-ttu-id="81d77-171">Sin embargo, la lista de destino podría haber sido 10.0.1.5:8080 si nuestro servidor web escucha en el puerto 8080, convirtiendo, por tanto, el puerto de entrada 80 del firewall en el puerto 8080 de entrada del servidor web.</span><span class="sxs-lookup"><span data-stu-id="81d77-171">However, the Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating the inbound port 80 on the firewall to inbound port 8080 on the web server.</span></span>

<span data-ttu-id="81d77-172">También se debe indicar un método de conexión, para el que regla de destino desde Internet, "Dynamic SNAT", sea la más adecuada.</span><span class="sxs-lookup"><span data-stu-id="81d77-172">A Connection Method should also be signified, for the Destination Rule from the Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="81d77-173">Aunque se creó una regla, es importante que su prioridad se establezca correctamente.</span><span class="sxs-lookup"><span data-stu-id="81d77-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="81d77-174">Si esta nueva regla se encuentra en la parte inferior de la cuadrícula de todas las reglas en el firewall (debajo de la regla "BLOCKALL"), nunca se activará.</span><span class="sxs-lookup"><span data-stu-id="81d77-174">If in the grid of all rules on the firewall this new rule is on the bottom (below the "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="81d77-175">Asegúrese de que la regla recién creada para el tráfico web está encima de la regla BLOCKALL.</span><span class="sxs-lookup"><span data-stu-id="81d77-175">Ensure the newly created rule for web traffic is above the BLOCKALL rule.</span></span>

<span data-ttu-id="81d77-176">Una vez que se crea la regla, debe insertarse en el firewall y, después, activarse, pues en caso contrario el cambio de regla no tendrá efecto.</span><span class="sxs-lookup"><span data-stu-id="81d77-176">Once the rule is created, it must be pushed to the firewall and then activated, if this is not done the rule change will not take effect.</span></span> <span data-ttu-id="81d77-177">En la siguiente sección se describe el proceso de activación y de inserción.</span><span class="sxs-lookup"><span data-stu-id="81d77-177">The push and activation process is described in the next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="81d77-178">Activación de reglas</span><span class="sxs-lookup"><span data-stu-id="81d77-178">Rule Activation</span></span>
<span data-ttu-id="81d77-179">Con el conjunto de reglas modificado para agregar esta regla, el conjunto de reglas debe cargarse en el firewall y activarse.</span><span class="sxs-lookup"><span data-stu-id="81d77-179">With the ruleset modified to add this rule, the ruleset must be uploaded to the firewall and activated.</span></span>

<span data-ttu-id="81d77-180">![Activación de reglas de firewall][4]</span><span class="sxs-lookup"><span data-stu-id="81d77-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="81d77-181">En la esquina superior derecha del cliente de administración hay un grupo de botones.</span><span class="sxs-lookup"><span data-stu-id="81d77-181">In the upper right hand corner of the management client are a cluster of buttons.</span></span> <span data-ttu-id="81d77-182">Haga clic en el botón "Send Changes" (Enviar cambios) para enviar las reglas modificadas al firewall y, después, haga clic en el botón "Activate" (Activar).</span><span class="sxs-lookup"><span data-stu-id="81d77-182">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span></span>

<span data-ttu-id="81d77-183">Con la activación del conjunto de reglas de firewall finaliza la compilación del entorno de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="81d77-183">With the activation of the firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="81d77-184">Opcionalmente, se pueden ejecutar los scripts posteriores a la compilación en la sección de referencias para agregar una aplicación a este entorno para probar los escenarios de tráfico siguientes.</span><span class="sxs-lookup"><span data-stu-id="81d77-184">Optionally, the post build scripts in the References section can be run to add an application to this environment to test the below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81d77-185">Es esencial tener en cuenta que no alcanzará el servidor web directamente.</span><span class="sxs-lookup"><span data-stu-id="81d77-185">It is critical to realize that you will not hit the web server directly.</span></span> <span data-ttu-id="81d77-186">Cuando un explorador solicita una página HTTP desde FrontEnd001.CloudApp.Net, el extremo HTTP (puerto 80) traslada este tráfico al firewall, no al servidor web.</span><span class="sxs-lookup"><span data-stu-id="81d77-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, the HTTP endpoint (port 80) passes this traffic to the firewall not the web server.</span></span> <span data-ttu-id="81d77-187">El firewall, según la regla creada anteriormente, envía varios NAT que solicitan al servidor web.</span><span class="sxs-lookup"><span data-stu-id="81d77-187">The firewall then, according to the rule created above, NATs that request to the Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="81d77-188">Escenarios de tráfico</span><span class="sxs-lookup"><span data-stu-id="81d77-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-to-web-server-through-firewall"></a><span data-ttu-id="81d77-189">(Permitido) Servidor web a web a través de firewall</span><span class="sxs-lookup"><span data-stu-id="81d77-189">(Allowed) Web to Web Server through Firewall</span></span>
1. <span data-ttu-id="81d77-190">El usuario de Internet solicita la página HTTP desde FrontEnd001.CloudApp.Net (servicio en la nube accesible desde Internet).</span><span class="sxs-lookup"><span data-stu-id="81d77-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="81d77-191">El servicio en la nube pasa el tráfico por un extremo abierto en el puerto 80 hacia la interfaz local del firewall en 10.0.1.4:80.</span><span class="sxs-lookup"><span data-stu-id="81d77-191">Cloud service passes traffic through open endpoint on port 80 to firewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="81d77-192">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="81d77-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="81d77-193">No se aplica la regla 1 (DNS) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="81d77-194">No se aplica la regla 2 (DNS) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="81d77-195">Se aplica la regla 3 (Internet a firewall) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="81d77-195">NSG Rule 3 (Internet to Firewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="81d77-196">El tráfico llega a dirección IP interna del firewall (10.0.1.4).</span><span class="sxs-lookup"><span data-stu-id="81d77-196">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="81d77-197">La regla de reenvío de firewall que ve esto es el tráfico del puerto 80, lo redirige al servidor web IIS01.</span><span class="sxs-lookup"><span data-stu-id="81d77-197">Firewall forwarding rule see this is port 80 traffic, redirects it to the web server IIS01</span></span>
6. <span data-ttu-id="81d77-198">IIS01 escucha el tráfico web, recibe esta solicitud y comienza a procesarla.</span><span class="sxs-lookup"><span data-stu-id="81d77-198">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
7. <span data-ttu-id="81d77-199">IIS01 pide información al servidor SQL Server en AppVM01</span><span class="sxs-lookup"><span data-stu-id="81d77-199">IIS01 asks the SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="81d77-200">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="81d77-201">La subred back-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="81d77-201">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="81d77-202">No se aplica la regla 1 (DNS) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-202">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="81d77-203">No se aplica la regla 2 (DNS) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-203">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="81d77-204">No se aplica la regla 3 (Internet a firewall) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-204">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="81d77-205">No se aplica la regla 4 (IIS01 a AppVM01) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="81d77-205">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="81d77-206">AppVM01 recibe la consulta SQL y responde.</span><span class="sxs-lookup"><span data-stu-id="81d77-206">AppVM01 receives the SQL Query and responds</span></span>
11. <span data-ttu-id="81d77-207">Como no hay ninguna regla de salida en la subred back-end, se permite la respuesta.</span><span class="sxs-lookup"><span data-stu-id="81d77-207">Since there are no outbound rules on the Backend subnet the response is allowed</span></span>
12. <span data-ttu-id="81d77-208">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="81d77-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="81d77-209">No hay ninguna regla de grupo de seguridad de red que se aplique al tráfico de entrada desde la subred back-end a la subred front-end, por lo que no se aplica ninguna de las reglas de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="81d77-209">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="81d77-210">La regla del sistema predeterminada que permite el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-210">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
13. <span data-ttu-id="81d77-211">El servidor IIS recibe la respuesta SQL y completa la respuesta HTTP y la envía al solicitante.</span><span class="sxs-lookup"><span data-stu-id="81d77-211">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
14. <span data-ttu-id="81d77-212">Como es una sesión NAT del firewall, el destino de respuesta (inicialmente) es para el firewall.</span><span class="sxs-lookup"><span data-stu-id="81d77-212">Since this is a NAT session from the firewall, the response destination (initially) is for the Firewall</span></span>
15. <span data-ttu-id="81d77-213">El firewall recibe la respuesta del servidor web y lo reenvía al usuario de Internet.</span><span class="sxs-lookup"><span data-stu-id="81d77-213">The firewall receives the response from the Web Server and forwards back to the Internet User</span></span>
16. <span data-ttu-id="81d77-214">Puesto que no hay reglas de salida en la subred front-end, se permite la respuesta y el usuario de Internet recibe la página web solicitada.</span><span class="sxs-lookup"><span data-stu-id="81d77-214">Since there are no outbound rules on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="81d77-215">(Permitido) RDP a back-end</span><span class="sxs-lookup"><span data-stu-id="81d77-215">(Allowed) RDP to Backend</span></span>
1. <span data-ttu-id="81d77-216">El administrador del servidor en Internet solicita la sesión RDP para AppVM01 en BackEnd001.CloudApp.Net:xxxxx donde xxxxx es el número de puerto asignado de forma aleatoria para RDP a AppVM01 (el puerto asignado puede encontrarse en el Portal de Azure o a través de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="81d77-216">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="81d77-217">Como el firewall solo está escuchando en la dirección FrontEnd001.CloudApp.Net, no participa en este flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-217">Since the Firewall is only listening on the FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="81d77-218">La subred back-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="81d77-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="81d77-219">No se aplica la regla 1 (DNS) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-219">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="81d77-220">Se aplica la regla 2 (RDP) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="81d77-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="81d77-221">No hay reglas de salida, se aplican las reglas predeterminadas y se permite el tráfico de retorno.</span><span class="sxs-lookup"><span data-stu-id="81d77-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="81d77-222">La sesión RDP está habilitada.</span><span class="sxs-lookup"><span data-stu-id="81d77-222">RDP session is enabled</span></span>
6. <span data-ttu-id="81d77-223">AppVM01 solicita la contraseña del nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="81d77-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="81d77-224">(Permitido) Búsqueda de DNS del servidor web en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="81d77-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="81d77-225">El servidor web, IIS01, necesita una fuente de datos en www.data.gov, pero debe resolver la dirección.</span><span class="sxs-lookup"><span data-stu-id="81d77-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="81d77-226">La configuración de red de la red virtual incluye DNS01 (10.0.2.4 en la subred back-end) como servidor DNS principal, IIS01 envía la solicitud DNS a DNS01.</span><span class="sxs-lookup"><span data-stu-id="81d77-226">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="81d77-227">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="81d77-228">La subred back-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="81d77-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="81d77-229">Se aplica la regla 1 (DNS) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="81d77-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="81d77-230">El servidor DNS recibe la solicitud.</span><span class="sxs-lookup"><span data-stu-id="81d77-230">DNS server receives the request</span></span>
6. <span data-ttu-id="81d77-231">El servidor DNS no tiene la dirección en caché y solicita un servidor DNS raíz en Internet.</span><span class="sxs-lookup"><span data-stu-id="81d77-231">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="81d77-232">No hay reglas de salida en la subred back-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="81d77-233">El servidor DNS de Internet responde, puesto que esta sesión se inició internamente, se permite la respuesta.</span><span class="sxs-lookup"><span data-stu-id="81d77-233">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="81d77-234">El servidor DNS almacena en caché la respuesta y responde a la solicitud inicial a IIS01.</span><span class="sxs-lookup"><span data-stu-id="81d77-234">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="81d77-235">No hay reglas de salida en la subred back-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="81d77-236">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="81d77-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="81d77-237">No hay ninguna regla de grupo de seguridad de red que se aplique al tráfico de entrada desde la subred back-end a la subred front-end, por lo que no se aplica ninguna de las reglas de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="81d77-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="81d77-238">La regla del sistema predeterminada que permite el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="81d77-239">IIS01 recibe la respuesta de DNS01.</span><span class="sxs-lookup"><span data-stu-id="81d77-239">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="81d77-240">(Permitido) Archivo de acceso del servidor web en AppVM01</span><span class="sxs-lookup"><span data-stu-id="81d77-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="81d77-241">IIS01 solicita un archivo en AppVM01</span><span class="sxs-lookup"><span data-stu-id="81d77-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="81d77-242">No hay reglas de salida en la subred front-end, se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="81d77-243">La subred back-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="81d77-243">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="81d77-244">No se aplica la regla 1 (DNS) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-244">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="81d77-245">No se aplica la regla 2 (DNS) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-245">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="81d77-246">No se aplica la regla 3 (Internet a firewall) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-246">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="81d77-247">No se aplica la regla 4 (IIS01 a AppVM01) de grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="81d77-247">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="81d77-248">AppVM01 recibe la solicitud y responde con el archivo (suponiendo que se autoriza el acceso).</span><span class="sxs-lookup"><span data-stu-id="81d77-248">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="81d77-249">Como no hay ninguna regla de salida en la subred back-end, se permite la respuesta.</span><span class="sxs-lookup"><span data-stu-id="81d77-249">Since there are no outbound rules on the Backend subnet the response is allowed</span></span>
6. <span data-ttu-id="81d77-250">La subred front-end comienza el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="81d77-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="81d77-251">No hay ninguna regla de grupo de seguridad de red que se aplique al tráfico de entrada desde la subred back-end a la subred front-end, por lo que no se aplica ninguna de las reglas de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="81d77-251">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="81d77-252">La regla del sistema predeterminada que permite el tráfico entre subredes permitiría este tráfico, por lo que se permite el tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-252">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="81d77-253">El servidor IIS recibe el archivo.</span><span class="sxs-lookup"><span data-stu-id="81d77-253">The IIS server receives the file</span></span>

#### <a name="denied-web-direct-to-web-server"></a><span data-ttu-id="81d77-254">(Denegado) Web directo al servidor web</span><span class="sxs-lookup"><span data-stu-id="81d77-254">(Denied) Web direct to Web Server</span></span>
<span data-ttu-id="81d77-255">Dado que el servidor web, IIS01 y el firewall se encuentran en el mismo servicio en la nube, comparten la misma dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="81d77-255">Since the Web Server, IIS01, and the Firewall are in the same Cloud Service they share the same public facing IP address.</span></span> <span data-ttu-id="81d77-256">Por lo tanto todo el tráfico HTTP se dirigirá al firewall.</span><span class="sxs-lookup"><span data-stu-id="81d77-256">Thus any HTTP traffic would be directed to the firewall.</span></span> <span data-ttu-id="81d77-257">Aunque la solicitud se atendió correctamente, no puede ir directamente al servidor web y, pasa primero, como está previsto, a través del firewall.</span><span class="sxs-lookup"><span data-stu-id="81d77-257">While the request would be successfully served, it cannot go directly to the Web Server, it passed, as designed, through the Firewall first.</span></span> <span data-ttu-id="81d77-258">Consulte el primer escenario de esta sección para ver el flujo de tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-258">See the first Scenario in this section for the traffic flow.</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="81d77-259">(Denegado) Web a servidor back-end</span><span class="sxs-lookup"><span data-stu-id="81d77-259">(Denied) Web to Backend Server</span></span>
1. <span data-ttu-id="81d77-260">El usuario de Internet intenta acceder a un archivo en AppVM01 a través del servicio BackEnd001.CloudApp.Net.</span><span class="sxs-lookup"><span data-stu-id="81d77-260">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="81d77-261">Puesto que no hay ningún extremo abierto para el uso compartido de archivos, no pasaría por el servicio en la nube y no llegaría al servidor.</span><span class="sxs-lookup"><span data-stu-id="81d77-261">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="81d77-262">Si hubiera extremos abiertos por alguna razón, la regla 5 (Internet a la red virtual) de grupo de seguridad de red bloquearía este tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-262">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="81d77-263">(Denegado) Búsqueda de DNS web en el servidor DNS</span><span class="sxs-lookup"><span data-stu-id="81d77-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="81d77-264">El usuario de Internet intenta buscar un registro DNS interno en DNS01 a través del servicio BackEnd001.CloudApp.Net.</span><span class="sxs-lookup"><span data-stu-id="81d77-264">Internet user tries to lookup an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="81d77-265">Puesto que no hay ningún extremo abierto para DNS, no pasaría por el servicio en la nube y no llegaría al servidor.</span><span class="sxs-lookup"><span data-stu-id="81d77-265">Since there are no endpoints open for DNS, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="81d77-266">Si hubiera extremos abiertos por alguna razón, la regla 5 (Internet a red virtual) de grupo de seguridad de red bloquearía este tráfico. (Nota: esa regla 1 (DNS) no se aplicaría por dos motivos; en primer lugar, la dirección de origen es Internet, esta regla solo se aplica a la red virtual local como origen. También se trata una regla de permiso, por lo que nunca denegaría tráfico).</span><span class="sxs-lookup"><span data-stu-id="81d77-266">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="81d77-267">(Denegado) Web a acceso SQL a través de firewall</span><span class="sxs-lookup"><span data-stu-id="81d77-267">(Denied) Web to SQL access through Firewall</span></span>
1. <span data-ttu-id="81d77-268">El usuario de Internet solicita los datos SQL desde FrontEnd001.CloudApp.Net (servicio en la nube accesible desde Internet).</span><span class="sxs-lookup"><span data-stu-id="81d77-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="81d77-269">Puesto que no hay ningún extremo abierto para SQL, no pasaría por el servicio en la nube y no llegaría al firewall.</span><span class="sxs-lookup"><span data-stu-id="81d77-269">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="81d77-270">Si hubiera extremos abiertos por alguna razón, la subred front-end comenzaría el procesamiento de las reglas de entrada:</span><span class="sxs-lookup"><span data-stu-id="81d77-270">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="81d77-271">No se aplica la regla 1 (DNS) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-271">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="81d77-272">No se aplica la regla 2 (DNS) de grupo de seguridad de red, pasar a la regla siguiente.</span><span class="sxs-lookup"><span data-stu-id="81d77-272">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="81d77-273">Se aplica la regla 2 (Internet a firewall) del grupo de seguridad de red, se permite el tráfico, detener el procesamiento de las reglas.</span><span class="sxs-lookup"><span data-stu-id="81d77-273">NSG Rule 2 (Internet to Firewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="81d77-274">El tráfico llega a dirección IP interna del firewall (10.0.1.4).</span><span class="sxs-lookup"><span data-stu-id="81d77-274">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="81d77-275">El firewall no tiene ninguna regla de reenvío para SQL y descarta el tráfico.</span><span class="sxs-lookup"><span data-stu-id="81d77-275">Firewall has no forwarding rules for SQL and drops the traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="81d77-276">Conclusión</span><span class="sxs-lookup"><span data-stu-id="81d77-276">Conclusion</span></span>
<span data-ttu-id="81d77-277">Se trata de una manera relativamente sencilla de proteger la aplicación con un firewall y de aislar la subred back-end del tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="81d77-277">This is a relatively straight forward way of protecting your application with a firewall and isolating the back end subnet from inbound traffic.</span></span>

<span data-ttu-id="81d77-278">Puede encontrar más ejemplos y una descripción general de los límites de seguridad de red [aquí][HOME].</span><span class="sxs-lookup"><span data-stu-id="81d77-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="81d77-279">Referencias</span><span class="sxs-lookup"><span data-stu-id="81d77-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="81d77-280">Script principal y configuración de red</span><span class="sxs-lookup"><span data-stu-id="81d77-280">Main Script and Network Config</span></span>
<span data-ttu-id="81d77-281">Guarde el script completo en un archivo de script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81d77-281">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="81d77-282">Guarde la configuración de red en un archivo llamado "NetworkConf2.xml".</span><span class="sxs-lookup"><span data-stu-id="81d77-282">Save the Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="81d77-283">Modifique las variables definidas por el usuario que sean necesarias.</span><span class="sxs-lookup"><span data-stu-id="81d77-283">Modify the user defined variables as needed.</span></span> <span data-ttu-id="81d77-284">Ejecute el script y siga las instrucciones de configuración de reglas de firewall anteriores.</span><span class="sxs-lookup"><span data-stu-id="81d77-284">Run the script, then follow the Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="81d77-285">Script completo</span><span class="sxs-lookup"><span data-stu-id="81d77-285">Full Script</span></span>
<span data-ttu-id="81d77-286">En función de las variables definidas por el usuario, este script realizará las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="81d77-286">This script will, based on the user defined variables:</span></span>

1. <span data-ttu-id="81d77-287">Conexión a una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="81d77-287">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="81d77-288">Creación de una cuenta de almacenamiento nueva</span><span class="sxs-lookup"><span data-stu-id="81d77-288">Create a new storage account</span></span>
3. <span data-ttu-id="81d77-289">Creación de una red virtual nueva y dos subredes, como se define en el archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="81d77-289">Create a new VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="81d77-290">Creación de cuatro máquinas virtuales de servidor Windows</span><span class="sxs-lookup"><span data-stu-id="81d77-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="81d77-291">Configuración del grupo de seguridad de red, incluido lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="81d77-291">Configure NSG including:</span></span>
   * <span data-ttu-id="81d77-292">Creación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="81d77-292">Creating a NSG</span></span>
   * <span data-ttu-id="81d77-293">Rellenado con reglas</span><span class="sxs-lookup"><span data-stu-id="81d77-293">Populating it with rules</span></span>
   * <span data-ttu-id="81d77-294">Enlace del grupo de seguridad de red a las subredes adecuadas</span><span class="sxs-lookup"><span data-stu-id="81d77-294">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="81d77-295">Este script de PowerShell debe ejecutarse localmente en un equipo o servidor conectado a Internet.</span><span class="sxs-lookup"><span data-stu-id="81d77-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81d77-296">Cuando se ejecuta este script, puede haber advertencias u otros mensajes informativos que se muestran en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81d77-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="81d77-297">Solo los mensajes de error indicados en rojo son motivo de preocupación.</span><span class="sxs-lookup"><span data-stu-id="81d77-297">Only error messages in red are cause for concern.</span></span>
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
       - One server on the FrontEnd Subnet (plus the NVA on the FrontEnd subnet)
       - Three Servers on the BackEnd Subnet
       - Network Security Groups to allow/deny traffic patterns as declared

      Before running script, ensure the network configuration file is created in
      the directory referenced by $NetworkConfigFile variable (or update the
      variable to reflect the path and file name of the config file being used).

     .Notes
      Security requirements are different for each use case and can be addressed in a
      myriad of ways. Please be sure that any sensitive data or applications are behind
      the appropriate layer(s) of protection. This script serves as an example of some
      of the techniques that can be used, but should not be used for all scenarios. You
      are responsible to assess your security needs and the appropriate protections
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
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes to reflect your subscription and services
      # Invalid options will fail in the validation section

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
        # Note: To ensure proper NSG Rule creation later in this script:
        #       - The Web Server must be VM 1
        #       - The AppVM1 Server must be VM 2
        #       - The DNS server must be VM 4
        #
        #       Otherwise the NSG rules in the last section of this
        #       script will need to be changed to match the modified
        #       VM array numbers ($i) so the NSG Rule IP addresses
        #       are aligned to the associated VM IP addresses.

        # VM 0 - The Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - The Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - The First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - The Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - The DNS Server
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

      # Update Subscription Pointer to New Storage Account
        Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation varible is correct and the netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see the above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

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
                # Set up all the EndPoints we'll need once we're up and running
                # Note: Web traffic goes through the firewall, so we'll need to set up a HTTP endpoint.
                #       Also, the firewall will be redirecting web traffic to a new IP and Port in a
                #       forwarding rule, so the HTTP endpoint here will have the same public and local
                #       port and the firewall will do the NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when the appliance is created.
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
        Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

      # Build the NSG
        Write-Host "Building the NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) to $($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 140 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
            -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
            -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
            -Protocol *

        # Assign the NSG to the Subnets
            Write-Host "Binding the NSG to both subnets" -ForegroundColor Cyan
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on the IIS Server)
      # Install Backend resource (Run Post-Build Script on the AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="81d77-298">Archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="81d77-298">Network Config File</span></span>
<span data-ttu-id="81d77-299">Guarde este archivo xml con la ubicación actualizada y agregue el vínculo a este archivo a la variable $NetworkConfigFile en el script anterior.</span><span class="sxs-lookup"><span data-stu-id="81d77-299">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="81d77-300">Scripts de aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="81d77-300">Sample Application Scripts</span></span>
<span data-ttu-id="81d77-301">Si desea instalar una aplicación de ejemplo para este y otros ejemplos de red perimetral, hay una en el siguiente vínculo: [Script de aplicación de ejemplo][SampleApp].</span><span class="sxs-lookup"><span data-stu-id="81d77-301">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
<span data-ttu-id="81d77-302">[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Red perimetral de entrada con grupo de seguridad de red"</span><span class="sxs-lookup"><span data-stu-id="81d77-302">[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Inbound DMZ with NSG"</span></span>
<span data-ttu-id="81d77-303">[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Icono de NAT de destino"</span><span class="sxs-lookup"><span data-stu-id="81d77-303">[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Destination NAT Icon"</span></span>
<span data-ttu-id="81d77-304">[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Regla de firewall"</span><span class="sxs-lookup"><span data-stu-id="81d77-304">[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Firewall Rule"</span></span>
<span data-ttu-id="81d77-305">[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Activación de reglas de firewall"</span><span class="sxs-lookup"><span data-stu-id="81d77-305">[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Firewall Rule Activation"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
