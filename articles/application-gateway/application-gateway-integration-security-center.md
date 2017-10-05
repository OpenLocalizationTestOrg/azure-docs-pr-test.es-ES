---
title: "Integración de Application Gateway con Azure Security Center | Microsoft Docs"
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
ms.openlocfilehash: 737cdff3140be68cf9d6d396b470dd09c65c52f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="ad817-103">Introducción a la integración entre Application Gateway y Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="ad817-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="ad817-104">Conozca más información acerca de cómo Application Gateway y Security Center le ayudan a proteger los recursos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ad817-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="ad817-105">El firewall de la aplicación web (WAF) de Application Gateway se integra con [Security Center](../security-center/security-center-intro.md) para proporcionar una vista integrada que evite, detecte y responda a las amenazas a las aplicaciones web no protegidas de su entorno.</span><span class="sxs-lookup"><span data-stu-id="ad817-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="ad817-106">Información general</span><span class="sxs-lookup"><span data-stu-id="ad817-106">Overview</span></span>

<span data-ttu-id="ad817-107">El WAF de Application Gateway es una recomendación de Security Center para proteger las aplicaciones web frente a ataques y vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="ad817-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="ad817-108">Los recursos con conexión que no están protegidos con WAF aparecen en Security Center como recomendaciones de gravedad alta.</span><span class="sxs-lookup"><span data-stu-id="ad817-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="ad817-109">Las recomendaciones para los firewalls de aplicaciones web aparecen en la página **Introducción**, en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ad817-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![integración con security center][1]

<span data-ttu-id="ad817-111">Al hacer clic en las recomendaciones sobre el firewall de aplicación web se abre una nueva hoja que muestra los detalles de la recomendación.</span><span class="sxs-lookup"><span data-stu-id="ad817-111">Clicking any recommendations regarding web application firewall opens a new blade showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="ad817-112">Adición del firewall de aplicaciones web a un recurso existente</span><span class="sxs-lookup"><span data-stu-id="ad817-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="ad817-113">Vaya a **Más servicios** > **Seguridad e identidad** > **Security Center** y en la hoja **Security Center - Información general**, haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="ad817-113">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="ad817-114">En la hoja **Security Center - Aplicaciones**, la tabla contiene una lista de las aplicaciones que Security Center ha detectado en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="ad817-114">On the **Security Center - Applications** blade, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![aplicaciones web][3]

<span data-ttu-id="ad817-116">Al hacer clic en una aplicación web con un problema crítico, aparecerá la hoja **Estado de seguridad de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="ad817-116">By clicking on a web application with a critical issue, you get the **Application security health** blade.</span></span> <span data-ttu-id="ad817-117">En la imagen siguiente, se ve la aplicación web que no está protegida por un firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="ad817-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![recursos web no protegidos][2]

<span data-ttu-id="ad817-119">Haga clic en **Agregar un firewall de aplicaciones web** en **Recomendaciones** para que se abra la hoja **Agregar un firewall de aplicaciones web**.</span><span class="sxs-lookup"><span data-stu-id="ad817-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="ad817-120">Si no tiene una instancia de Application Gateway existente o quiere crear una nueva, haga clic en **Crear nuevo** y en la hoja **Create a new Web Application Firewall** (Crear un nuevo firewall de aplicaciones web) y haga clic en **Microsoft - Application Gateway**.</span><span class="sxs-lookup"><span data-stu-id="ad817-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on the **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="ad817-121">Esto le guiará por los pasos para crear una instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ad817-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="ad817-122">En este punto, la aplicación web se agrega como un recurso protegido y Security Center realiza un seguimiento para asegurarse de que este recurso está protegido por un firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="ad817-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="ad817-123">No se agrega como miembro del grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="ad817-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="ad817-124">Si ya tiene una instancia de Application Gateway, puede elegirla en **Usar solución existente**</span><span class="sxs-lookup"><span data-stu-id="ad817-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![hoja de adición de firewall de aplicaciones web][4]

<span data-ttu-id="ad817-126">La adición de una aplicación web a una instancia de Application Gateway a través de Security Center no agrega el recurso como miembro del grupo de back-end. Esto se debe hacer directamente en el recurso de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ad817-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member, this must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="ad817-127">Adición de un recurso a un firewall de aplicaciones web existente</span><span class="sxs-lookup"><span data-stu-id="ad817-127">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="ad817-128">Vaya a **Más servicios** > **Seguridad e identidad** > **Security Center** y en la hoja **Security Center - Información general**, haga clic en **Soluciones de asociados**.</span><span class="sxs-lookup"><span data-stu-id="ad817-128">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="ad817-129">Las instancias de Application Gateway existentes reconocidas en Security Center aparecen en la hoja **Soluciones de asociados**.</span><span class="sxs-lookup"><span data-stu-id="ad817-129">Existing Security Center aware application gateways show in the **Partner Solutions** blade.</span></span>

![soluciones de asociados][7]

<span data-ttu-id="ad817-131">Haga clic en **Vincular aplicación** para abrir la hoja **Vincular aplicaciones**. Aquí se proporcionan las opciones para seleccionar las aplicaciones existentes.</span><span class="sxs-lookup"><span data-stu-id="ad817-131">Click **Link app** to open the **Link Applications** blade, here you are given the options to select existing applications.</span></span> <span data-ttu-id="ad817-132">Elija las aplicaciones que desea proteger y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ad817-132">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="ad817-133">Este procedimiento no agregará la aplicación web al grupo de back-end de la instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ad817-133">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="ad817-134">Esto establece los recursos como recursos protegidos, por lo que Security Center puede realizar un seguimiento de ellos.</span><span class="sxs-lookup"><span data-stu-id="ad817-134">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="ad817-135">Para agregar el recurso como un miembro del grupo de back-end, debe hacerlo en la instancia de Application Gateway. En la hoja actual puede hacer clic en **Consola de soluciones** para ir al recurso de Application Gateway donde podrá agregar la aplicación web al grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="ad817-135">To add the resource as a backend pool member, this must be done on the application gateway, from the current blade you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![aplicaciones de soluciones de asociados][6]

## <a name="finalize-configuration"></a><span data-ttu-id="ad817-137">Finalización de la configuración</span><span class="sxs-lookup"><span data-stu-id="ad817-137">Finalize configuration</span></span>

<span data-ttu-id="ad817-138">Security Center realiza un seguimiento de las aplicaciones agregadas a una instancia de Application Gateway como recursos protegidos.</span><span class="sxs-lookup"><span data-stu-id="ad817-138">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="ad817-139">Supervisa el estado de este recurso y se asegura de que está protegido mediante una instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ad817-139">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="ad817-140">El siguiente paso consiste en agregar la dirección IP privada, la dirección IP pública o el NIC de la máquina virtual al grupo de back-end de la instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ad817-140">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="ad817-141">Hasta que esto se hace, aparece una recomendación adicional de **Finalizar protección de la aplicación** hasta que se agrega el recurso.</span><span class="sxs-lookup"><span data-stu-id="ad817-141">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![hoja de adición de firewall de aplicaciones web][5]

## <a name="security-alerts"></a><span data-ttu-id="ad817-143">Alertas de seguridad</span><span class="sxs-lookup"><span data-stu-id="ad817-143">Security Alerts</span></span>

<span data-ttu-id="ad817-144">En Security Center, vaya a **DETECCIÓN** > **Alertas de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="ad817-144">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="ad817-145">Aquí encontrará las alertas de WAF para las instancias de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ad817-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="ad817-146">Las alertas se desglosan según las reglas de WAF.</span><span class="sxs-lookup"><span data-stu-id="ad817-146">Alerts are broken down by WAF rule.</span></span>

![alertas de seguridad][8]

<span data-ttu-id="ad817-148">Si hace clic en una regla proporcionará una lista de alertas para esa regla de WAF específica.</span><span class="sxs-lookup"><span data-stu-id="ad817-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="ad817-149">Cada alerta muestra detalles adicionales sobre la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="ad817-149">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="ad817-150">Los detalles de proporcionan un vínculo a la instancia de Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ad817-150">The details provide a link to the application gateway.</span></span>
 
![detalles de alertas][9]

## <a name="next-steps"></a><span data-ttu-id="ad817-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad817-152">Next steps</span></span>

<span data-ttu-id="ad817-153">Para aprender a habilitar un firewall de aplicaciones web en una instancia existente de Application Gateway, visite [Creación o actualización de una instancia de Azure Application Gateway con el firewall de aplicaciones web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="ad817-153">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png