---
title: "aaaApplication integración de puerta de enlace con el centro de seguridad de Azure | Documentos de Microsoft"
description: "Esta página proporciona información sobre cómo se integra Application Gateway en Azure Security Center."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="73f4a-103">Introducción a la integración entre Application Gateway y Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="73f4a-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="73f4a-104">Conozca más información acerca de cómo Application Gateway y Security Center le ayudan a proteger los recursos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="73f4a-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="73f4a-105">Servidor de aplicaciones web de aplicación puerta de enlace (WAFS) se integra con [centro de seguridad](../security-center/security-center-intro.md) tooprovide un tooprevent vista integrada, detectar y responder a las aplicaciones web de toothreats toounprotected en su entorno.</span><span class="sxs-lookup"><span data-stu-id="73f4a-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) tooprovide a seamless view tooprevent, detect and respond toothreats toounprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="73f4a-106">Información general</span><span class="sxs-lookup"><span data-stu-id="73f4a-106">Overview</span></span>

<span data-ttu-id="73f4a-107">El WAF de Application Gateway es una recomendación de Security Center para proteger las aplicaciones web frente a ataques y vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="73f4a-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="73f4a-108">Recursos de Web habilitado que no están protegidos por WAFS se muestran en el centro de seguridad de hello como recomendaciones de gravedad alta.</span><span class="sxs-lookup"><span data-stu-id="73f4a-108">Web enabled resources that are not protected by WAF show in hello security center as high severity recommendations.</span></span> <span data-ttu-id="73f4a-109">Recomendaciones para los firewalls de aplicación web se muestran en hello **Introducción** página, en **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="73f4a-109">Recommendations for web application firewalls are shown on hello **Overview** page, under **Applications**.</span></span>

![integración con security center][1]

<span data-ttu-id="73f4a-111">Al pulsar ninguna recomendación relacionada con el servidor de aplicaciones web, abre una nueva hoja muestra los detalles de saludo de la recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="73f4a-111">Clicking any recommendations regarding web application firewall opens a new blade showing hello details of hello recommendation.</span></span>

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a><span data-ttu-id="73f4a-112">Agregar un recurso web de aplicación firewall tooan existente</span><span class="sxs-lookup"><span data-stu-id="73f4a-112">Add a web application firewall tooan existing resource</span></span>

<span data-ttu-id="73f4a-113">Navegue demasiado**más servicios** > **seguridad e identidad** > **centro de seguridad** y en hello **centro de seguridad - información general**  hoja, haga clic en **aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="73f4a-113">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="73f4a-114">En hello **centro de seguridad - aplicaciones** hoja, tabla de hello contiene una lista de aplicaciones que el centro de seguridad ha detectado en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="73f4a-114">On hello **Security Center - Applications** blade, hello table contains a list of applications that Security Center detected in your subscription.</span></span>

![aplicaciones web][3]

<span data-ttu-id="73f4a-116">Al hacer clic en una aplicación web con un problema crítico, obtendrá hello **estado de seguridad de la aplicación** hoja.</span><span class="sxs-lookup"><span data-stu-id="73f4a-116">By clicking on a web application with a critical issue, you get hello **Application security health** blade.</span></span> <span data-ttu-id="73f4a-117">En la imagen de hello siguiente, Hola aplicación web que no está protegido por un servidor de seguridad de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="73f4a-117">In hello image below, hello web application that is not protected by a web application firewall.</span></span> 

![recursos web no protegidos][2]

<span data-ttu-id="73f4a-119">Haga clic en **agregar un servidor de seguridad de la aplicación web** en **recomendaciones** tooopen hello **agregar un servidor de seguridad de la aplicación Web** hoja.</span><span class="sxs-lookup"><span data-stu-id="73f4a-119">Click **Add a web application firewall** under **Recommendations** tooopen hello **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="73f4a-120">Si no tiene una puerta de enlace de la aplicación existente, o desea toocreate uno nuevo, haga clic en **crear nuevo** y en hello **crear un nuevo servidor de aplicaciones Web** hoja y haga clic en **Microsoft: Puerta de enlace de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="73f4a-120">If you do not have an existing Application Gateway, or want toocreate a new one, click **Create New** and on hello **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="73f4a-121">Esto le llevará a través de hello pasos toocreate una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="73f4a-121">This takes you through hello steps toocreate an application gateway.</span></span> <span data-ttu-id="73f4a-122">En este punto, la aplicación web se agrega como un recurso protegido y Security Center realiza un seguimiento para asegurarse de que este recurso está protegido por un firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="73f4a-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="73f4a-123">No se agrega como miembro del grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="73f4a-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="73f4a-124">Si ya tiene una instancia de Application Gateway, puede elegirla en **Usar solución existente**</span><span class="sxs-lookup"><span data-stu-id="73f4a-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![hoja de adición de firewall de aplicaciones web][4]

<span data-ttu-id="73f4a-126">Agregar que una puerta de enlace de web application tooan aplicación a través del centro de seguridad no agrega recursos Hola como un miembro del grupo back-end, debe hacerlo en el recurso de puerta de enlace de aplicación Hola directamente.</span><span class="sxs-lookup"><span data-stu-id="73f4a-126">Adding a web application tooan application gateway through Security Center does not add hello resource as a backend pool member, this must be done on hello application gateway resource directly.</span></span>

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a><span data-ttu-id="73f4a-127">Agregar un servidor de aplicaciones de web existente de recursos tooan</span><span class="sxs-lookup"><span data-stu-id="73f4a-127">Add a resource tooan existing web application firewall</span></span>

<span data-ttu-id="73f4a-128">Navegue demasiado**más servicios** > **seguridad e identidad** > **centro de seguridad** y en hello **centro de seguridad - información general**  hoja, haga clic en **soluciones de asociados**.</span><span class="sxs-lookup"><span data-stu-id="73f4a-128">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="73f4a-129">Puertas de enlace de aplicación compatible con el centro de seguridad existentes se muestran en hello **soluciones de socios** hoja.</span><span class="sxs-lookup"><span data-stu-id="73f4a-129">Existing Security Center aware application gateways show in hello **Partner Solutions** blade.</span></span>

![soluciones de asociados][7]

<span data-ttu-id="73f4a-131">Haga clic en **aplicación vínculo** tooopen hello **aplicaciones de vínculo** hoja, aquí se proporcionan aplicaciones existentes de hello opciones tooselect.</span><span class="sxs-lookup"><span data-stu-id="73f4a-131">Click **Link app** tooopen hello **Link Applications** blade, here you are given hello options tooselect existing applications.</span></span> <span data-ttu-id="73f4a-132">Elija Hola aplicaciones tooprotect y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="73f4a-132">Choose hello applications tooprotect and click **OK**.</span></span> <span data-ttu-id="73f4a-133">Este método no agrega grupo hello web aplicación toohello back-end de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="73f4a-133">This does not add hello web application toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="73f4a-134">Recursos de Hola se establece como un recurso protegido para que el centro de seguridad puede realizar un seguimiento.</span><span class="sxs-lookup"><span data-stu-id="73f4a-134">This sets hello resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="73f4a-135">recurso de hello tooadd como un miembro del grupo back-end, esto debe hacerse en puerta de enlace de aplicación Hola, desde la hoja actual de hello puede hacer clic **consola de solución** toobe realizada toohello de recursos de puerta de enlace de aplicación donde puede agregar web Hola grupo de aplicaciones toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="73f4a-135">tooadd hello resource as a backend pool member, this must be done on hello application gateway, from hello current blade you can click **Solution console** toobe taken toohello application gateway resource where you can add hello web application toohello backend pool.</span></span>

![aplicaciones de soluciones de asociados][6]

## <a name="finalize-configuration"></a><span data-ttu-id="73f4a-137">Finalización de la configuración</span><span class="sxs-lookup"><span data-stu-id="73f4a-137">Finalize configuration</span></span>

<span data-ttu-id="73f4a-138">Las aplicaciones de las pistas del centro de seguridad agregan tooan puerta de enlace de aplicaciones como un recurso protegido.</span><span class="sxs-lookup"><span data-stu-id="73f4a-138">Security Center tracks applications added tooan application gateway as a protected resource.</span></span>  <span data-ttu-id="73f4a-139">Supervisa el estado de Hola de este recurso y se asegura de que está protegida por una puerta de enlace de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="73f4a-139">It monitors hello health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="73f4a-140">Hola siguiente paso es tooadd Hola privada IP, IP pública o NIC de su grupo de back-end de toohello de máquina virtual de puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="73f4a-140">hello next step is tooadd hello private IP, public IP, or NIC of your virtual machine toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="73f4a-141">Hasta que esto se hace una recomendación adicional de **finalizar la protección de la aplicación** se muestra hasta que se agregan recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="73f4a-141">Until this is done an additional recommendation of **Finalize application protection** is shown until hello resource is added.</span></span>

![hoja de adición de firewall de aplicaciones web][5]

## <a name="security-alerts"></a><span data-ttu-id="73f4a-143">Alertas de seguridad</span><span class="sxs-lookup"><span data-stu-id="73f4a-143">Security Alerts</span></span>

<span data-ttu-id="73f4a-144">En el centro de seguridad desplazarse demasiado**detección** > **alertas de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="73f4a-144">Within Security Center navigate too**DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="73f4a-145">Aquí encontrará las alertas de WAF para las instancias de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="73f4a-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="73f4a-146">Las alertas se desglosan según las reglas de WAF.</span><span class="sxs-lookup"><span data-stu-id="73f4a-146">Alerts are broken down by WAF rule.</span></span>

![alertas de seguridad][8]

<span data-ttu-id="73f4a-148">Si hace clic en una regla proporcionará una lista de alertas para esa regla de WAF específica.</span><span class="sxs-lookup"><span data-stu-id="73f4a-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="73f4a-149">Cada alerta muestra detalles adicionales acerca de cómo buscar Hola.</span><span class="sxs-lookup"><span data-stu-id="73f4a-149">Each alert shows additional details on hello finding.</span></span> <span data-ttu-id="73f4a-150">detalles de Hello proporcionan una puerta de enlace de aplicaciones de toohello de vínculo.</span><span class="sxs-lookup"><span data-stu-id="73f4a-150">hello details provide a link toohello application gateway.</span></span>
 
![detalles de alertas][9]

## <a name="next-steps"></a><span data-ttu-id="73f4a-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="73f4a-152">Next steps</span></span>

<span data-ttu-id="73f4a-153">toolearn cómo tooenable firewall de aplicación web en una puerta de enlace de aplicación existente, visite [crear o actualizar una puerta de enlace de aplicaciones de Azure con firewall de aplicación web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="73f4a-153">toolearn how tooenable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png