---
title: "aaaCreate de reglas de una puerta de enlace de la aplicación mediante el enrutamiento de direcciones URL - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Esta página proporcionan instrucciones toocreate, configure una puerta de enlace de la aplicación de Azure mediante las reglas de enrutamiento de direcciones URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="c0f35-103">Creación de una puerta de enlace de aplicaciones mediante enrutamiento basado en rutas de acceso con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c0f35-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0f35-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c0f35-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="c0f35-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c0f35-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="c0f35-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c0f35-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="c0f35-107">Enrutamiento basado en la ruta de acceso de direcciones URL permite tooassociate rutas basándose en la ruta de acceso de dirección URL de Hola de una solicitud Http.</span><span class="sxs-lookup"><span data-stu-id="c0f35-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="c0f35-108">Comprueba si hay un grupo de back-end de ruta tooa configurado para dirección URL de hello presentado en Application Gateway hello y envía toohello de tráfico de red de hello definido grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="c0f35-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="c0f35-109">Un uso común de enrutamiento basado en la dirección URL es tooload equilibrar las solicitudes para grupos de servidor back-end de toodifferent de diferentes tipos de contenido.</span><span class="sxs-lookup"><span data-stu-id="c0f35-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="c0f35-110">Enrutamiento basado en dirección URL, presenta una puerta de enlace de tooapplication de tipo de regla nueva.</span><span class="sxs-lookup"><span data-stu-id="c0f35-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="c0f35-111">Application Gateway tiene dos tipos de reglas: básicas y PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="c0f35-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="c0f35-112">Tipo de regla básica proporciona servicio round robin para hello back-end grupos al PathBasedRouting además de la distribución competitiva tooround, también tiene modelo de ruta de acceso de dirección URL de solicitud de hello en cuenta al elegir grupo back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-112">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="c0f35-113">Escenario</span><span class="sxs-lookup"><span data-stu-id="c0f35-113">Scenario</span></span>

<span data-ttu-id="c0f35-114">En el siguiente ejemplo de Hola, puerta de enlace de aplicaciones está atendiendo a tráfico para contoso.com con dos grupos de servidor back-end: un grupo de servidor predeterminado y un grupo de servidores de la imagen.</span><span class="sxs-lookup"><span data-stu-id="c0f35-114">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="c0f35-115">Las solicitudes para http://contoso.com/image * son enruta el grupo de servidores de tooimage (imagesBackendPool), si hello no coincide con el patrón de ruta de acceso, se selecciona un grupo de servidores de forma predeterminada (appGatewayBackendPool).</span><span class="sxs-lookup"><span data-stu-id="c0f35-115">Requests for http://contoso.com/image* are routed tooimage server pool (imagesBackendPool), if hello path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![ruta de dirección URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a><span data-ttu-id="c0f35-117">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="c0f35-117">Log in tooAzure</span></span>

<span data-ttu-id="c0f35-118">Abra hello **Microsoft Azure Command Prompt**e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="c0f35-118">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="c0f35-119">También puede usar `az login` sin el modificador de hello para el inicio de sesión de dispositivo que requiere proporcionar un código en aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="c0f35-119">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="c0f35-120">Una vez que escriba Hola anterior ejemplo, se proporciona un código.</span><span class="sxs-lookup"><span data-stu-id="c0f35-120">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="c0f35-121">Navegue toohttps://aka.ms/devicelogin en un proceso de inicio de sesión de explorador toocontinue Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-121">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd que muestra el inicio de sesión de dispositivos][1]

<span data-ttu-id="c0f35-123">En el Explorador de hello, escriba el código de hello que ha recibido.</span><span class="sxs-lookup"><span data-stu-id="c0f35-123">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="c0f35-124">Está página de inicio de sesión tooa redirigida.</span><span class="sxs-lookup"><span data-stu-id="c0f35-124">You are redirected tooa sign-in page.</span></span>

![código de tooenter de explorador][2]

<span data-ttu-id="c0f35-126">Una vez que se ha especificado el código de hello ha iniciado sesión, cierre Hola explorador toocontinue con el escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-126">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![ha iniciado sesión correctamente][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a><span data-ttu-id="c0f35-128">Agregar una regla basada en la ruta de acceso tooan aplicación puerta de enlace existente</span><span class="sxs-lookup"><span data-stu-id="c0f35-128">Add a path-based rule tooan existing application gateway</span></span>

<span data-ttu-id="c0f35-129">Cree una puerta de enlace de aplicaciones con una regla de ruta definida.</span><span class="sxs-lookup"><span data-stu-id="c0f35-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="c0f35-130">Creación de un nuevo grupo de back-end</span><span class="sxs-lookup"><span data-stu-id="c0f35-130">Create a new back-end pool</span></span>

<span data-ttu-id="c0f35-131">Configuración de puerta de enlace de aplicaciones **imagesBackendPool** para tráfico con equilibrio de carga de red de hello en grupo back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-131">Configure application gateway setting **imagesBackendPool** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="c0f35-132">En este ejemplo, configurará la configuración de otro grupo back-end para nuevos grupos de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-132">In this example, you configure different back-end pool settings for hello new back-end pool.</span></span> <span data-ttu-id="c0f35-133">Cada grupo de back-end puede tener su propia configuración de grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="c0f35-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="c0f35-134">Configuración de HTTP de back-end se usa por miembros del grupo de reglas tooroute tráfico toohello correcta back-end.</span><span class="sxs-lookup"><span data-stu-id="c0f35-134">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="c0f35-135">Esto determina el protocolo de Hola y el puerto que se usa al enviar tráfico toohello los miembros del grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="c0f35-135">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="c0f35-136">Configuración de HTTP de back-end de hello también dependen de las sesiones basado en cookies.</span><span class="sxs-lookup"><span data-stu-id="c0f35-136">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="c0f35-137">Si está habilitada, la afinidad de sesión basado en cookies envía tráfico toohello mismo back-end como solicitudes anteriores para cada paquete.</span><span class="sxs-lookup"><span data-stu-id="c0f35-137">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="c0f35-138">Creación de un nuevo puerto de front-end</span><span class="sxs-lookup"><span data-stu-id="c0f35-138">Create a new front-end port</span></span>

<span data-ttu-id="c0f35-139">Configurar puerto front-end de Hola para una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0f35-139">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="c0f35-140">objeto de configuración de puerto front-end de Hello utiliza un agente de escucha toodefine qué puerto de escucha de puerta de enlace de aplicación hello para el tráfico en el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-140">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="c0f35-141">Creación de un nuevo agente de escucha</span><span class="sxs-lookup"><span data-stu-id="c0f35-141">Create a new listener</span></span>

<span data-ttu-id="c0f35-142">Configurar el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-142">Configure hello listener.</span></span> <span data-ttu-id="c0f35-143">Este paso configura el agente de escucha de hello para la dirección IP pública hello y utiliza el puerto tooreceive tráfico de red entrante.</span><span class="sxs-lookup"><span data-stu-id="c0f35-143">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="c0f35-144">Hola siguiente ejemplo toma la configuración de IP de front-end de hello configurado previamente, la configuración de puerto front-end y un protocolo (http o https) y configura el agente de escucha de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-144">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="c0f35-145">En este ejemplo, el agente de escucha de hello escucha tooHTTP tráfico en el puerto 82 dirección IP pública Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c0f35-145">In this example, hello listener listens tooHTTP traffic on port 82 on hello public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a><span data-ttu-id="c0f35-146">Crear mapa de ruta de acceso de dirección Url de Hola</span><span class="sxs-lookup"><span data-stu-id="c0f35-146">Create hello Url path map</span></span>

<span data-ttu-id="c0f35-147">Configurar rutas de acceso de regla de dirección URL para grupos de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-147">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="c0f35-148">Este paso configura Hola ruta de acceso relativa utilizado por asignación para hello toodefine aplicación puerta de enlace entre la ruta de acceso de dirección URL y qué grupo back-end se asigna el tráfico entrante toohandle Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-148">This step configures hello relative path used by application gateway toodefine hello mapping between URL path and which back-end pool is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0f35-149">Cada ruta de acceso debe comenzar con / hello solo lugar y un "\*" está permitida, está al final de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0f35-149">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="c0f35-150">Algunos ejemplos válidos son /xyz, /xyz* o /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="c0f35-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="c0f35-151">Hello cadena fed buscador de coincidencias de ruta de acceso de toohello no incluye cualquier texto después de hello primero "?" o "#" y los caracteres no se permiten.</span><span class="sxs-lookup"><span data-stu-id="c0f35-151">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="c0f35-152">Hello en el ejemplo siguiente se crea una regla de "/ imágenes / *" ruta de acceso de enrutamiento de tráfico tooback-end "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="c0f35-152">hello following example creates one rule for "/images/*" path routing traffic tooback-end "imagesBackendPool."</span></span> <span data-ttu-id="c0f35-153">Esta regla garantiza que el tráfico para cada conjunto de direcciones URL es toohello enrutado back-end.</span><span class="sxs-lookup"><span data-stu-id="c0f35-153">This rule ensures that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="c0f35-154">Por ejemplo, va demasiado http://adatum.com/images/figure1.jpg "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="c0f35-154">For example, http://adatum.com/images/figure1.jpg goes too"imagesBackendPool."</span></span> <span data-ttu-id="c0f35-155">Si la ruta de acceso de hello no coincide con ninguna de las reglas de ruta de acceso definida previamente hello, configuración del mapa de ruta de acceso de regla de hello también configura un grupo de direcciones de back-end de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c0f35-155">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="c0f35-156">Por ejemplo, http://adatum.com/shoppingcart/test.html va toopool1 tal y como se define como grupo predeterminado de hello para el tráfico no coincidente.</span><span class="sxs-lookup"><span data-stu-id="c0f35-156">For example, http://adatum.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a><span data-ttu-id="c0f35-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0f35-157">Next steps</span></span>

<span data-ttu-id="c0f35-158">Si desea toolearn sobre la descarga de capa de Sockets seguros (SSL), consulte [configurar una puerta de enlace de la aplicación para la descarga SSL](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c0f35-158">If you want toolearn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
