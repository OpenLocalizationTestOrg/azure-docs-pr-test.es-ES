---
title: aaaHost varios sitios con la puerta de enlace de aplicaciones de Azure | Documentos de Microsoft
description: "Esta página proporciona instrucciones tooconfigure una puerta de enlace de la aplicación de Azure existente para hospedar varias aplicaciones web en hello misma puerta de enlace con hello portal de Azure."
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
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="ca33b-103">Configuración de una puerta de enlace de aplicaciones existente para hospedar varias aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="ca33b-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca33b-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ca33b-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="ca33b-105">PowerShell del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="ca33b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="ca33b-106">Alojamiento de varios sitios permite toodeploy más de una aplicación web en hello misma puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ca33b-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="ca33b-107">Se basa en la presencia del encabezado de host en la solicitud HTTP entrante hello, toodetermine qué agente de escucha reciba tráfico.</span><span class="sxs-lookup"><span data-stu-id="ca33b-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="ca33b-108">agente de escucha de Hello, a continuación, dirige el grupo de back-end de tráfico tooappropriate como está configurado en la definición de las reglas de Hola de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="ca33b-109">En las aplicaciones web se ha habilitado SSL, puerta de enlace de aplicaciones se basa en hello indicación de nombre de servidor (SNI) extensión toochoose Hola correcto agente de escucha para el tráfico de web Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="ca33b-110">Un uso común de alojamiento de varios sitios es tooload equilibrar las solicitudes para grupos de servidor back-end de toodifferent de dominios de web diferente.</span><span class="sxs-lookup"><span data-stu-id="ca33b-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="ca33b-111">De igual forma varios subdominios de hello también se puede hospedar el dominio raíz del mismo en Hola misma puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ca33b-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="ca33b-112">Escenario</span><span class="sxs-lookup"><span data-stu-id="ca33b-112">Scenario</span></span>

<span data-ttu-id="ca33b-113">En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com y fabrikam.com con dos grupos de servidor back-end: contoso grupo de servidores y el grupo de servidores de fabrikam.</span><span class="sxs-lookup"><span data-stu-id="ca33b-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="ca33b-114">El programa de instalación similar podría ser subdominios toohost usado como app.contoso.com y blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ca33b-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![escenario multisitio][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="ca33b-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ca33b-116">Before you begin</span></span>

<span data-ttu-id="ca33b-117">Este escenario agrega la puerta de enlace de aplicaciones existentes de compatibilidad con varios sitios tooan.</span><span class="sxs-lookup"><span data-stu-id="ca33b-117">This scenario adds multi-site support tooan existing application gateway.</span></span> <span data-ttu-id="ca33b-118">toocomplete toobe disponibles tooconfigure es necesario este escenario, una puerta de enlace de la aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="ca33b-118">toocomplete this scenario, an existing application gateway needs toobe available tooconfigure.</span></span> <span data-ttu-id="ca33b-119">Visite [crear una puerta de enlace de la aplicación mediante el portal de hello](application-gateway-create-gateway-portal.md) toolearn cómo toocreate una puerta de enlace de aplicaciones básica en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-119">Visit [Create an application gateway by using hello portal](application-gateway-create-gateway-portal.md) toolearn how toocreate a basic application gateway in hello portal.</span></span>

<span data-ttu-id="ca33b-120">siguiente Hola es pasos de hello necesarios puerta de enlace de aplicaciones de tooupdate hello:</span><span class="sxs-lookup"><span data-stu-id="ca33b-120">hello following are hello steps needed tooupdate hello application gateway:</span></span>

1. <span data-ttu-id="ca33b-121">Crear grupos de back-end toouse para cada sitio.</span><span class="sxs-lookup"><span data-stu-id="ca33b-121">Create back-end pools toouse for each site.</span></span>
2. <span data-ttu-id="ca33b-122">Cree un agente de escucha para cada puerta de enlace de aplicaciones del sitio que lo admitirá.</span><span class="sxs-lookup"><span data-stu-id="ca33b-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="ca33b-123">Crear reglas toomap cada agente de escucha con hello adecuado back-end.</span><span class="sxs-lookup"><span data-stu-id="ca33b-123">Create rules toomap each listener with hello appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="ca33b-124">Requisitos</span><span class="sxs-lookup"><span data-stu-id="ca33b-124">Requirements</span></span>

* <span data-ttu-id="ca33b-125">**Grupo de servidores de back-end:** Hola lista de direcciones IP de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-125">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="ca33b-126">direcciones IP en Hello lista deben pertenecer o subred de red virtual toohello o deben ser una dirección IP pública/VIP.</span><span class="sxs-lookup"><span data-stu-id="ca33b-126">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="ca33b-127">También puede utilizarse el FQDN.</span><span class="sxs-lookup"><span data-stu-id="ca33b-127">FQDN can also be used.</span></span>
* <span data-ttu-id="ca33b-128">**Configuración del grupo de servidores back-end:** cada grupo tiene una configuración en la que se incluye el puerto, el protocolo y la afinidad basada en cookies.</span><span class="sxs-lookup"><span data-stu-id="ca33b-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="ca33b-129">Esta configuración está ligada tooa grupo y son servidores de tooall aplicados en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="ca33b-130">**Puerto front-end:** este puerto es Hola pública que se abre en la puerta de enlace de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-130">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="ca33b-131">Tráfico llega a este puerto y, a continuación, obtiene redirigido tooone de servidores de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-131">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="ca33b-132">**Agente de escucha:** agente de escucha de hello tiene un puerto front-end, un protocolo (Http o Https, estos valores distinguen mayúsculas de minúsculas) y el nombre del certificado SSL hello (si se descarga la configuración de SSL).</span><span class="sxs-lookup"><span data-stu-id="ca33b-132">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="ca33b-133">En el caso de las puertas de enlace de aplicaciones con sitios múltiples habilitados, también se agregan el nombre de host y los indicadores de SNI.</span><span class="sxs-lookup"><span data-stu-id="ca33b-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="ca33b-134">**Regla:** regla Hola enlaza el agente de escucha de hello, grupo de servidores de back-end de Hola y define qué tráfico de Hola de grupo de servidor back-end debe ser dirigido toowhen llega a un agente de escucha determinado.</span><span class="sxs-lookup"><span data-stu-id="ca33b-134">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="ca33b-135">Las reglas se procesan en orden de hello aparecen y se dirigirá el tráfico a través de la regla primera Hola que coincida con independientemente de especificidad.</span><span class="sxs-lookup"><span data-stu-id="ca33b-135">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="ca33b-136">Por ejemplo, si tiene una regla mediante un agente de escucha básico y una regla mediante una escucha de varios sitio ambos en hello misma regla de puerto, Hola con el agente de escucha de hello multisitio debe aparecer antes de la regla de hello con un agente de escucha básico de hello en orden para hello toofunction de regla de multisitio como se esperaba.</span><span class="sxs-lookup"><span data-stu-id="ca33b-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span> 
* <span data-ttu-id="ca33b-137">**Certificados:** cada agente de escucha requiere un certificado único, en este ejemplo se crean dos agentes de escucha para varios sitios.</span><span class="sxs-lookup"><span data-stu-id="ca33b-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="ca33b-138">Dos certificados .pfx y las contraseñas de Hola para ellos deben toobe creado.</span><span class="sxs-lookup"><span data-stu-id="ca33b-138">Two .pfx certificates and hello passwords for them need toobe created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="ca33b-139">Creación de grupos de back-end para cada sitio</span><span class="sxs-lookup"><span data-stu-id="ca33b-139">Create back-end pools for each site</span></span>

<span data-ttu-id="ca33b-140">Se necesita un grupo de back-end para cada sitio que va a admitir esa puerta de enlace de aplicaciones; en este caso se crearán dos, uno para contoso11.com y otro para fabrikam11.com.</span><span class="sxs-lookup"><span data-stu-id="ca33b-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="ca33b-141">Paso 1</span><span class="sxs-lookup"><span data-stu-id="ca33b-141">Step 1</span></span>

<span data-ttu-id="ca33b-142">Navegue tooan la puerta de enlace de aplicación existente en hello portal de Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ca33b-142">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="ca33b-143">Seleccione **Grupos de back-end** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ca33b-143">Select **Backend pools** and click **Add**</span></span>

![adición de grupos de back-end][7]

### <a name="step-2"></a><span data-ttu-id="ca33b-145">Paso 2</span><span class="sxs-lookup"><span data-stu-id="ca33b-145">Step 2</span></span>

<span data-ttu-id="ca33b-146">Rellene la información de hello para el grupo de back-end de hello **pool1**, agregar direcciones ip de Hola o FQDN para servidores de back-end de Hola y haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="ca33b-146">Fill in hello information for hello back-end pool **pool1**, adding hello ip addresses or FQDNs for hello back-end servers and click **OK**</span></span>

![configuración del grupo de back-end grupo1][8]

### <a name="step-3"></a><span data-ttu-id="ca33b-148">Paso 3</span><span class="sxs-lookup"><span data-stu-id="ca33b-148">Step 3</span></span>

<span data-ttu-id="ca33b-149">En la hoja de grupos de back-end de hello haga clic en **agregar** tooadd un grupo back-end adicional **pool2**, agregar direcciones ip de Hola o FQDN para servidores de back-end de Hola y haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="ca33b-149">On hello backend-pools blade click **Add** tooadd an additional back-end pool **pool2**, adding hello ip addresses or FQDNS for hello back-end servers and click **OK**</span></span>

![configuración del grupo de back-end grupo2][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="ca33b-151">Creación de agentes de escucha para cada back-end</span><span class="sxs-lookup"><span data-stu-id="ca33b-151">Create listeners for each back-end</span></span>

<span data-ttu-id="ca33b-152">Puerta de enlace de aplicaciones se basa en HTTP 1.1 toohost de encabezados de host, más de un sitio Web en Hola la misma dirección IP pública y el puerto.</span><span class="sxs-lookup"><span data-stu-id="ca33b-152">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="ca33b-153">escucha básica Hello creada en portal de hello no contiene esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="ca33b-153">hello basic listener created in hello portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="ca33b-154">Paso 1</span><span class="sxs-lookup"><span data-stu-id="ca33b-154">Step 1</span></span>

<span data-ttu-id="ca33b-155">Haga clic en **los agentes de escucha** Hola puerta de enlace de aplicación existente y haga clic en **multisitio** primer agente de escucha de tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-155">Click **Listeners** on hello existing application gateway and click **Multi-site** tooadd hello first listener.</span></span>

![hoja de información general de los agentes de escucha][1]

### <a name="step-2"></a><span data-ttu-id="ca33b-157">Paso 2</span><span class="sxs-lookup"><span data-stu-id="ca33b-157">Step 2</span></span>

<span data-ttu-id="ca33b-158">Rellene la información de hello para el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-158">Fill out hello information for hello listener.</span></span> <span data-ttu-id="ca33b-159">En este ejemplo se configura la terminación SSL y se crea un nuevo puerto de front-end.</span><span class="sxs-lookup"><span data-stu-id="ca33b-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="ca33b-160">Cargar toobe de certificado .pfx Hola utilizado para la terminación SSL.</span><span class="sxs-lookup"><span data-stu-id="ca33b-160">Upload hello .pfx certificate toobe used for SSL termination.</span></span> <span data-ttu-id="ca33b-161">Hola única diferencia en esta hoja de agente de escucha básico estándar toohello hoja en comparación con es el nombre de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-161">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span>

![hoja de propiedades del agente de escucha][2]

### <a name="step-3"></a><span data-ttu-id="ca33b-163">Paso 3</span><span class="sxs-lookup"><span data-stu-id="ca33b-163">Step 3</span></span>

<span data-ttu-id="ca33b-164">Haga clic en **multisitio** y crear otro agente de escucha tal como se describe en el paso anterior de Hola para otro sitio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-164">Click **Multi-site** and create another listener as described in hello previous step for hello second site.</span></span> <span data-ttu-id="ca33b-165">Asegúrese de toouse seguro de un certificado diferente para el agente de escucha de segundo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-165">Make sure toouse a different certificate for hello second listener.</span></span> <span data-ttu-id="ca33b-166">Hola única diferencia en esta hoja de agente de escucha básico estándar toohello hoja en comparación con es el nombre de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-166">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span> <span data-ttu-id="ca33b-167">Rellene la información de hello para el agente de escucha de Hola y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ca33b-167">Fill out hello information for hello listener and click **OK**.</span></span>

![hoja de propiedades del agente de escucha][3]

> [!NOTE]
> <span data-ttu-id="ca33b-169">La creación de agentes de escucha de hello portal de Azure para puerta de enlace de aplicaciones es una tarea de ejecución prolongada, podría tardar algunos Hola de toocreate tiempo dos agentes de escucha en este escenario.</span><span class="sxs-lookup"><span data-stu-id="ca33b-169">Creation of listeners in hello Azure portal for application gateway is a long running task, it may take some time toocreate hello two listeners in this scenario.</span></span> <span data-ttu-id="ca33b-170">Cuando los agentes de escucha de hello completa se muestran en el portal de hello tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="ca33b-170">When complete hello listeners show in hello portal as seen in hello following image:</span></span>

![información general del agente de escucha][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a><span data-ttu-id="ca33b-172">Crear reglas de grupos de toobackend de agentes de escucha de toomap</span><span class="sxs-lookup"><span data-stu-id="ca33b-172">Create rules toomap listeners toobackend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="ca33b-173">Paso 1</span><span class="sxs-lookup"><span data-stu-id="ca33b-173">Step 1</span></span>

<span data-ttu-id="ca33b-174">Navegue tooan la puerta de enlace de aplicación existente en hello portal de Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ca33b-174">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="ca33b-175">Seleccione **reglas** y elija la regla predeterminada existente de hello **rule1** y haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="ca33b-175">Select **Rules** and choose hello existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="ca33b-176">Paso 2</span><span class="sxs-lookup"><span data-stu-id="ca33b-176">Step 2</span></span>

<span data-ttu-id="ca33b-177">Rellene la hoja de reglas de Hola tal como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="ca33b-177">Fill out hello rules blade as seen in hello following image.</span></span> <span data-ttu-id="ca33b-178">Elegir el primer agente de escucha de Hola y el primer grupo y haga clic en **guardar** cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="ca33b-178">Choosing hello first listener and first pool and clicking **Save** when complete.</span></span>

![edición de una regla existente][6]

### <a name="step-3"></a><span data-ttu-id="ca33b-180">Paso 3</span><span class="sxs-lookup"><span data-stu-id="ca33b-180">Step 3</span></span>

<span data-ttu-id="ca33b-181">Haga clic en **reglas básicas** segunda regla de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="ca33b-181">Click **Basic rule** toocreate hello second rule.</span></span> <span data-ttu-id="ca33b-182">Rellene el formulario de hello con hello segundo agente de escucha y el segundo grupo back-end y haga clic en **Aceptar** toosave.</span><span class="sxs-lookup"><span data-stu-id="ca33b-182">Fill out hello form with hello second listener and second backend pool and click **OK** toosave.</span></span>

![adición de una hoja de reglas básicas][10]

<span data-ttu-id="ca33b-184">Este escenario completa la configuración de una puerta de enlace de aplicaciones existentes con soporte para varios sitio a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ca33b-184">This scenario completes configuring an existing application gateway with multi-site support through hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca33b-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca33b-185">Next steps</span></span>

<span data-ttu-id="ca33b-186">Obtenga información acerca de cómo tooprotect sus sitios Web con [puerta de enlace de aplicaciones - servidor de aplicaciones Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ca33b-186">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

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
