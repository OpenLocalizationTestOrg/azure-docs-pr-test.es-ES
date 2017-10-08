---
title: 'aaaCreate basada en una ruta de acceso de regla: puerta de enlace de aplicaciones de Azure: Portal de Azure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toocreate una regla basada en la ruta de acceso para una puerta de enlace de la aplicación mediante el uso de Hola portal"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a><span data-ttu-id="f2079-103">Crear una regla basada en la ruta de acceso para una puerta de enlace de la aplicación mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="f2079-103">Create a Path-based rule for an application gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2079-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f2079-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="f2079-105">PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2079-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="f2079-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f2079-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="f2079-107">Enrutamiento basado en la ruta de acceso de direcciones URL permite tooassociate rutas basándose en la ruta de acceso de dirección URL de saludo de solicitud Http.</span><span class="sxs-lookup"><span data-stu-id="f2079-107">URL Path-based routing enables you tooassociate routes based on hello URL path of Http request.</span></span> <span data-ttu-id="f2079-108">Comprueba si hay un grupo de back-end de ruta tooa configurado para la dirección URL de hello mencionada en hello Application Gateway y envía toohello de tráfico de red de hello definido grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="f2079-108">It checks if there is a route tooa back-end pool configured for hello URL listed in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="f2079-109">Un uso común de enrutamiento basado en la dirección URL es tooload equilibrar las solicitudes para grupos de servidor back-end de toodifferent de diferentes tipos de contenido.</span><span class="sxs-lookup"><span data-stu-id="f2079-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="f2079-110">Enrutamiento basado en dirección URL, presenta una puerta de enlace de tooapplication de tipo de regla nueva.</span><span class="sxs-lookup"><span data-stu-id="f2079-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="f2079-111">Application Gateway tiene dos tipos de reglas: básicas y basadas en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="f2079-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="f2079-112">tipo de regla básica de Hola, proporciona round robin servicio back-end de Hola grupos mientras las reglas basadas en la ruta de acceso de distribución Round robin de tooround Además, también tiene modelo de ruta de acceso de dirección URL de solicitud de hello en cuenta al elegir grupo back-end adecuados de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2079-112">hello basic rule type, provides round-robin service for hello back-end pools while path-based rules in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="f2079-113">Escenario</span><span class="sxs-lookup"><span data-stu-id="f2079-113">Scenario</span></span>

<span data-ttu-id="f2079-114">Hello escenario siguiente va a crear una regla basada en la ruta de acceso en una puerta de enlace de la aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="f2079-114">hello following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="f2079-115">Hello escenario se supone que ya ha seguido los pasos de hello demasiado[crear una puerta de enlace de la aplicación](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f2079-115">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![ruta de dirección URL][scenario]

## <span data-ttu-id="f2079-117"><a name="createrule"></a>Crear regla basada en ruta de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="f2079-117"><a name="createrule"></a>Create hello Path-based rule</span></span>

<span data-ttu-id="f2079-118">Una regla basada en la ruta de acceso requiere su propio agente de escucha, antes de crear la regla de hello ser tooverify seguro de que tiene un agente de escucha disponible toouse.</span><span class="sxs-lookup"><span data-stu-id="f2079-118">A Path-based rule requires its own listener, before creating hello rule be sure tooverify you have an available listener toouse.</span></span>

### <a name="step-1"></a><span data-ttu-id="f2079-119">Paso 1</span><span class="sxs-lookup"><span data-stu-id="f2079-119">Step 1</span></span>

<span data-ttu-id="f2079-120">Navegue toohello [portal de Azure](http://portal.azure.com) y seleccione una puerta de enlace de la aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="f2079-120">Navigate toohello [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="f2079-121">Haga clic en **Reglas**</span><span class="sxs-lookup"><span data-stu-id="f2079-121">Click **Rules**</span></span>

![Introducción a Application Gateway][1]

### <a name="step-2"></a><span data-ttu-id="f2079-123">Paso 2</span><span class="sxs-lookup"><span data-stu-id="f2079-123">Step 2</span></span>

<span data-ttu-id="f2079-124">Haga clic en **basado en la ruta de acceso** botón tooadd una nueva regla de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="f2079-124">Click **Path-based** button tooadd a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="f2079-125">Paso 3</span><span class="sxs-lookup"><span data-stu-id="f2079-125">Step 3</span></span>

<span data-ttu-id="f2079-126">Hola **Agregar regla de ruta de acceso-based** hoja tiene dos secciones.</span><span class="sxs-lookup"><span data-stu-id="f2079-126">hello **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="f2079-127">Hola primera sección es donde se definen el agente de escucha de hello, el nombre de Hola de regla de Hola y la configuración de ruta de acceso predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2079-127">hello first section is where you defined hello listener, hello name of hello rule and hello default path settings.</span></span> <span data-ttu-id="f2079-128">configuración de ruta de acceso predeterminada de Hello es para las rutas que no entran en la ruta de hello personalizado basado en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="f2079-128">hello default path settings are for routes that do not fall under hello custom path-based route.</span></span> <span data-ttu-id="f2079-129">Hola segunda sección de hello **Agregar regla de ruta de acceso-based** hoja es donde se definen reglas basadas en la ruta de acceso de Hola por sí mismos.</span><span class="sxs-lookup"><span data-stu-id="f2079-129">hello second section of hello **Add path-based rule** blade is where you define hello path-based rules themselves.</span></span>

<span data-ttu-id="f2079-130">**Configuración básica**</span><span class="sxs-lookup"><span data-stu-id="f2079-130">**Basic Settings**</span></span>

* <span data-ttu-id="f2079-131">**Nombre de** -este valor es una regla de toohello nombre descriptivo que sea accesible en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2079-131">**Name** - This value is a friendly name toohello rule that is accessible in hello portal.</span></span>
* <span data-ttu-id="f2079-132">**Agente de escucha** -este valor es el agente de escucha de Hola que se usa para la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2079-132">**Listener** - This value is hello listener that is used for hello rule.</span></span>
* <span data-ttu-id="f2079-133">**Predeterminado grupo back-end** -esta configuración es Hola que define toobe de back-end de hello utilizado para la regla predeterminada de Hola</span><span class="sxs-lookup"><span data-stu-id="f2079-133">**Default backend pool** - This setting is hello setting that defines hello back-end toobe used for hello default rule</span></span>
* <span data-ttu-id="f2079-134">**Configuración predeterminada de HTTP** -esta configuración es Hola que define toobe de configuración de hello HTTP utilizado para la regla predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2079-134">**Default HTTP settings** - This setting is hello setting that defines hello HTTP settings toobe used for hello default rule.</span></span>

<span data-ttu-id="f2079-135">**Reglas basadas en ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="f2079-135">**Path-based rules**</span></span>

* <span data-ttu-id="f2079-136">**Nombre de** -este valor es una regla basada en toopath de nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="f2079-136">**Name** - This value is a friendly name toopath-based rule.</span></span>
* <span data-ttu-id="f2079-137">**Las rutas de acceso** -esta opción define Hola ruta Hola regla busca al reenviar tráfico</span><span class="sxs-lookup"><span data-stu-id="f2079-137">**Paths** - This setting defines hello path hello rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="f2079-138">**Grupo back-end** -esta configuración es Hola que define hello toobe de back-end usado para regla de Hola</span><span class="sxs-lookup"><span data-stu-id="f2079-138">**Backend Pool** - This setting is hello setting that defines hello back-end toobe used for hello rule</span></span>
* <span data-ttu-id="f2079-139">**Configuración de HTTP** -esta configuración es Hola que define toobe de configuración de hello HTTP utilizado para regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2079-139">**HTTP setting** - This setting is hello setting that defines hello HTTP settings toobe used for hello rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2079-140">Rutas de acceso: lista de Hola de toomatch de patrones de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="f2079-140">Paths: hello list of path patterns toomatch.</span></span> <span data-ttu-id="f2079-141">Cada uno de ellos debe comenzar con / hello solo lugar y un "\*" se permite es Hola final.</span><span class="sxs-lookup"><span data-stu-id="f2079-141">Each must start with / and hello only place a "\*" is allowed is at hello end.</span></span> <span data-ttu-id="f2079-142">Algunos ejemplos válidos son /xyz, /xyz* o /xyz/*.</span><span class="sxs-lookup"><span data-stu-id="f2079-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Agregar hoja de regla basada en ruta de acceso con información completada][2]

<span data-ttu-id="f2079-144">Agregar una regla basada en la ruta de acceso tooan puerta de enlace de aplicaciones existente es un proceso sencillo a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2079-144">Adding a path-based rule tooan existing application gateway is an easy process through hello portal.</span></span> <span data-ttu-id="f2079-145">Una vez creada una regla basada en la ruta de acceso, puede ser editado tooadd de reglas adicionales.</span><span class="sxs-lookup"><span data-stu-id="f2079-145">After a path-based rule has been created, it can be edited tooadd additional rules.</span></span> 

![agregar reglas basadas en ruta de acceso adicionales][3]

<span data-ttu-id="f2079-147">Este paso configura una regla basada en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="f2079-147">This step configures a path-based route.</span></span> <span data-ttu-id="f2079-148">Es importante toounderstand que las solicitudes no vuelven a escribirse, como las solicitudes procedan de puerta de enlace de aplicación inspecciona solicitud hello y basic en hello url patrón envía Hola solicitud toohello adecuado back-end.</span><span class="sxs-lookup"><span data-stu-id="f2079-148">It is important toounderstand that requests are not rewritten, as requests come in application gateway inspects hello request and basic on hello url pattern sends hello request toohello appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2079-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f2079-149">Next steps</span></span>

<span data-ttu-id="f2079-150">toolearn tooconfigure la descarga de SSL con la puerta de enlace de aplicaciones de Azure, vea [configurar la descarga de SSL](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f2079-150">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
