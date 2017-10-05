---
title: Hospedaje de varios sitios con Azure Application Gateway | Microsoft Docs
description: "En esta página se proporcionan instrucciones para configurar una puerta de enlace de aplicaciones de Azure para hospedar varias aplicaciones web en la misma puerta de enlace con Azure Portal."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 84bd62ae17b7f7ba4cd815ef1f9880679607ebce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="ebd9d-103">Configuración de una puerta de enlace de aplicaciones existente para hospedar varias aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="ebd9d-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ebd9d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ebd9d-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="ebd9d-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ebd9d-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="ebd9d-106">El hospedaje de varios sitios permite implementar más de una aplicación web en la misma puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="ebd9d-107">Se basa en la presencia de un encabezado host en la solicitud HTTP entrante para determinar el agente de escucha que recibe el tráfico.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="ebd9d-108">Luego, dicho agente dirige el tráfico al grupo de back-end adecuado, el configurado en la definición de las reglas de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="ebd9d-109">En las aplicaciones web con SSL habilitado, la puerta de enlace de aplicaciones depende de la extensión de la indicación de nombre de servidor (SNI) para elegir el agente de escucha correcto para el tráfico web.En las aplicaciones web con SSL habilitado, Application Gateway depende de la extensión de la indicación de nombre de servidor (SNI) para elegir el agente de escucha correcto para el tráfico web.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="ebd9d-110">Un uso común del hospedaje de varios sitios es el equilibrio de carga de las solicitudes de diferentes dominios web entre diferentes grupos de servidores de back-end.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="ebd9d-111">De forma similar, varios subdominios del mismo dominio raíz también se pueden hospedar en la misma puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="ebd9d-112">Escenario</span><span class="sxs-lookup"><span data-stu-id="ebd9d-112">Scenario</span></span>

<span data-ttu-id="ebd9d-113">En el siguiente ejemplo, la puerta de enlace de aplicaciones sirve el tráfico a contoso.com y a fabrikam.com con dos grupos de servidores back-end: el grupo de servidores de contoso y el grupo de servidores de fabrikam.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="ebd9d-114">Se puede usar una configuración similar para hospedar subdominios como app.contoso.com y blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![escenario multisitio][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="ebd9d-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ebd9d-116">Before you begin</span></span>

<span data-ttu-id="ebd9d-117">Este escenario agrega compatibilidad multisitio a una puerta de enlace de aplicaciones existente.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-117">This scenario adds multi-site support to an existing application gateway.</span></span> <span data-ttu-id="ebd9d-118">Para completar este escenario debe estar disponible para su configuración una puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-118">To complete this scenario, an existing application gateway needs to be available to configure.</span></span> <span data-ttu-id="ebd9d-119">Visite [Creación de una puerta de enlace de aplicaciones mediante el portal](application-gateway-create-gateway-portal.md) para aprender a crear una puerta de enlace de aplicaciones básica en el portal.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span></span>

<span data-ttu-id="ebd9d-120">A continuación se muestran los pasos necesarios para actualizar una puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="ebd9d-120">The following are the steps needed to update the application gateway:</span></span>

1. <span data-ttu-id="ebd9d-121">Cree grupos de back-end para cada sitio.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-121">Create back-end pools to use for each site.</span></span>
2. <span data-ttu-id="ebd9d-122">Cree un agente de escucha para cada puerta de enlace de aplicaciones del sitio que lo admitirá.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="ebd9d-123">Cree reglas para asignar cada agente de escucha al back-end apropiado.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-123">Create rules to map each listener with the appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="ebd9d-124">Requisitos</span><span class="sxs-lookup"><span data-stu-id="ebd9d-124">Requirements</span></span>

* <span data-ttu-id="ebd9d-125">**Grupo de servidores back-end** : lista de direcciones IP de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="ebd9d-126">Las direcciones IP que se enumeran deben pertenecer a la subred de la red virtual o ser una IP/VIP pública.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="ebd9d-127">También puede utilizarse el FQDN.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-127">FQDN can also be used.</span></span>
* <span data-ttu-id="ebd9d-128">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="ebd9d-129">Estos valores están vinculados a un grupo y se aplican a todos los servidores del grupo.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="ebd9d-130">**Puerto front-end:** este puerto es el puerto público que se abre en la puerta de enlace de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="ebd9d-131">El tráfico llega a este puerto y después se redirige a uno de los servidores back-end.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="ebd9d-132">**Agente de escucha** : tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL (si se configura la descarga de SSL).</span><span class="sxs-lookup"><span data-stu-id="ebd9d-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="ebd9d-133">En el caso de las puertas de enlace de aplicaciones con sitios múltiples habilitados, también se agregan el nombre de host y los indicadores de SNI.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="ebd9d-134">**Regla:** enlaza el agente de escucha y el grupo de servidores back-end, y define a qué grupo de servidores back-end se debe redireccionar el tráfico que llegue a un agente de escucha concreto.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="ebd9d-135">Las reglas se procesan en el orden en que aparecen y el tráfico se dirige a través de la primera regla que coincida independientemente de la especificidad.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="ebd9d-136">Por ejemplo, si tiene una regla que usa un agente de escucha básico y una regla que usa un agente de escucha multisitio en el mismo puerto, la regla con el agente de escucha multisitio debe aparecer antes que la regla con el agente de escucha básico para que la regla multisitio funcione según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 
* <span data-ttu-id="ebd9d-137">**Certificados:** cada agente de escucha requiere un certificado único, en este ejemplo se crean dos agentes de escucha para varios sitios.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="ebd9d-138">Deben crearse dos certificados .pfx y las contraseñas para ellos.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-138">Two .pfx certificates and the passwords for them need to be created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="ebd9d-139">Creación de grupos de back-end para cada sitio</span><span class="sxs-lookup"><span data-stu-id="ebd9d-139">Create back-end pools for each site</span></span>

<span data-ttu-id="ebd9d-140">Se necesita un grupo de back-end para cada sitio que va a admitir esa puerta de enlace de aplicaciones; en este caso se crearán dos, uno para contoso11.com y otro para fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="ebd9d-141">Paso 1</span><span class="sxs-lookup"><span data-stu-id="ebd9d-141">Step 1</span></span>

<span data-ttu-id="ebd9d-142">Vaya a una puerta de enlace de aplicaciones existente en Azure Portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ebd9d-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="ebd9d-143">Seleccione **Grupos de back-end** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-143">Select **Backend pools** and click **Add**</span></span>

![adición de grupos de back-end][7]

### <a name="step-2"></a><span data-ttu-id="ebd9d-145">Paso 2</span><span class="sxs-lookup"><span data-stu-id="ebd9d-145">Step 2</span></span>

<span data-ttu-id="ebd9d-146">Rellene la información para el grupo de back-end **grupo1**, agregue las direcciones IP o nombres completos para los servidores back-end y haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="ebd9d-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span></span>

![configuración del grupo de back-end grupo1][8]

### <a name="step-3"></a><span data-ttu-id="ebd9d-148">Paso 3</span><span class="sxs-lookup"><span data-stu-id="ebd9d-148">Step 3</span></span>

<span data-ttu-id="ebd9d-149">En la hoja de grupos de back-end, haga clic en **Agregar** para agregar el grupo de back-end adicional **pool2**, agregando la direcciones IP o nombres completos para los servidores back-end y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span></span>

![configuración del grupo de back-end grupo2][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="ebd9d-151">Creación de agentes de escucha para cada back-end</span><span class="sxs-lookup"><span data-stu-id="ebd9d-151">Create listeners for each back-end</span></span>

<span data-ttu-id="ebd9d-152">Application Gateway se basa en los encabezados de host HTTP 1.1 para hospedar más de un sitio web en la misma dirección IP pública y en el mismo puerto.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="ebd9d-153">El agente de escucha básico creado en el portal no contiene esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-153">The basic listener created in the portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="ebd9d-154">Paso 1</span><span class="sxs-lookup"><span data-stu-id="ebd9d-154">Step 1</span></span>

<span data-ttu-id="ebd9d-155">Haga clic en **Agentes de escucha** en la puerta de enlace de aplicaciones y haga clic en **Multisitio** para agregar el primer agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span></span>

![hoja de información general de los agentes de escucha][1]

### <a name="step-2"></a><span data-ttu-id="ebd9d-157">Paso 2</span><span class="sxs-lookup"><span data-stu-id="ebd9d-157">Step 2</span></span>

<span data-ttu-id="ebd9d-158">Rellene la información del agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-158">Fill out the information for the listener.</span></span> <span data-ttu-id="ebd9d-159">En este ejemplo se configura la terminación SSL y se crea un nuevo puerto de front-end.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="ebd9d-160">Cargue el certificado .pfx que se usará para la terminación SSL.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-160">Upload the .pfx certificate to be used for SSL termination.</span></span> <span data-ttu-id="ebd9d-161">La única diferencia de esta hoja en comparación con la hoja del agente de escucha básica estándar es el nombre de host.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span>

![hoja de propiedades del agente de escucha][2]

### <a name="step-3"></a><span data-ttu-id="ebd9d-163">Paso 3</span><span class="sxs-lookup"><span data-stu-id="ebd9d-163">Step 3</span></span>

<span data-ttu-id="ebd9d-164">Haga clic en **Multisitio** y cree otro agente de escucha, tal como se describe en el paso anterior para el segundo sitio.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span></span> <span data-ttu-id="ebd9d-165">Asegúrese de utilizar un certificado diferente para el segundo agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-165">Make sure to use a different certificate for the second listener.</span></span> <span data-ttu-id="ebd9d-166">La única diferencia de esta hoja en comparación con la hoja del agente de escucha básica estándar es el nombre de host.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span> <span data-ttu-id="ebd9d-167">Rellene la información del agente de escucha y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-167">Fill out the information for the listener and click **OK**.</span></span>

![hoja de propiedades del agente de escucha][3]

> [!NOTE]
> <span data-ttu-id="ebd9d-169">La creación de agentes de escucha en Azure Portal para la puerta de enlace de aplicaciones es una tarea de larga duración; puede tardar algún tiempo en crear los dos agentes de escucha en este escenario.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-169">Creation of listeners in the Azure portal for application gateway is a long running task, it may take some time to create the two listeners in this scenario.</span></span> <span data-ttu-id="ebd9d-170">Cuando finalice, los agentes de escucha se muestran en el portal, tal como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="ebd9d-170">When complete the listeners show in the portal as seen in the following image:</span></span>

![información general del agente de escucha][4]

## <a name="create-rules-to-map-listeners-to-backend-pools"></a><span data-ttu-id="ebd9d-172">Creación de reglas para asignar agentes de escucha a grupos de back-end</span><span class="sxs-lookup"><span data-stu-id="ebd9d-172">Create rules to map listeners to backend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="ebd9d-173">Paso 1</span><span class="sxs-lookup"><span data-stu-id="ebd9d-173">Step 1</span></span>

<span data-ttu-id="ebd9d-174">Vaya a una puerta de enlace de aplicaciones existente en Azure Portal (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ebd9d-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="ebd9d-175">Seleccione **Reglas** y elija la regla predeterminada existente **Regla1** y haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="ebd9d-176">Paso 2</span><span class="sxs-lookup"><span data-stu-id="ebd9d-176">Step 2</span></span>

<span data-ttu-id="ebd9d-177">Rellene la hoja de reglas, tal como se muestra en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-177">Fill out the rules blade as seen in the following image.</span></span> <span data-ttu-id="ebd9d-178">Elija el primer agente de escucha y el primer grupo y haga clic en **Guardar** cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-178">Choosing the first listener and first pool and clicking **Save** when complete.</span></span>

![edición de una regla existente][6]

### <a name="step-3"></a><span data-ttu-id="ebd9d-180">Paso 3</span><span class="sxs-lookup"><span data-stu-id="ebd9d-180">Step 3</span></span>

<span data-ttu-id="ebd9d-181">Haga clic en **Regla básica** para crear la segunda regla.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-181">Click **Basic rule** to create the second rule.</span></span> <span data-ttu-id="ebd9d-182">Rellene el formulario con el segundo agente de escucha y el segundo grupo de back-end, y haga clic en **Aceptar** para guardarlo.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span></span>

![adición de una hoja de reglas básicas][10]

<span data-ttu-id="ebd9d-184">Este escenario completa la configuración de una puerta de enlace de aplicaciones existentes con compatibilidad multisitio a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ebd9d-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebd9d-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ebd9d-185">Next steps</span></span>

<span data-ttu-id="ebd9d-186">Aprenda a proteger sitios web con [Firewall de aplicaciones web de Application Gateway (versión preliminar)](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ebd9d-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
