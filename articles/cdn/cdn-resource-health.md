---
title: "Supervisión del estado de los recursos de una red CDN de Azure | Microsoft Docs"
description: "Obtenga información sobre cómo supervisar el estado de los recursos de una red CDN de Azure con Estado de los recursos de Azure."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="8cde1-103">Supervisión del estado de los recursos de una red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="8cde1-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="8cde1-104">El estado de los recursos de la red CDN de Azure es un subconjunto de [Estado de los recursos de Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8cde1-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="8cde1-105">Puede usar Estado de los recursos de Azure para supervisar el estado de los recursos de una red CDN y recibir instrucciones procesables para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="8cde1-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="8cde1-106">El estado de los recursos de la red CDN de Azure solo tiene en cuenta el estado de la entrega de la red CDN global y las funciones de la API.</span><span class="sxs-lookup"><span data-stu-id="8cde1-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="8cde1-107">El estado de los recursos de la red CDN de Azure no comprueba los puntos de conexión individuales de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="8cde1-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="8cde1-108">Las señales que recibe el estado de los recursos de la red CDN de Azure pueden retrasarse hasta 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="8cde1-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="8cde1-109">Buscar el estado de los recursos de una red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="8cde1-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="8cde1-110">En [Azure Portal](https://portal.azure.com), vaya a su perfil de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="8cde1-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="8cde1-111">Haga clic en el botón **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="8cde1-111">Click the **Settings** button.</span></span>

    ![Botón Configuración](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="8cde1-113">En *Soporte y solución de problemas*, haga clic en **Estado de los recursos**.</span><span class="sxs-lookup"><span data-stu-id="8cde1-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Estado de los recursos de la red CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="8cde1-115">También encontrará los recursos de la red CDN en el icono *Estado de los recursos* de la hoja *Ayuda y soporte técnico*.</span><span class="sxs-lookup"><span data-stu-id="8cde1-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="8cde1-116">Para acceder rápidamente a *Ayuda y soporte técnico*, haga clic en el círculo con un signo de interrogación (**?**)</span><span class="sxs-lookup"><span data-stu-id="8cde1-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="8cde1-117">en la esquina superior derecha del portal.</span><span class="sxs-lookup"><span data-stu-id="8cde1-117">in the upper right corner of the portal.</span></span>
>
> ![Ayuda y soporte técnico](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="8cde1-119">Mensajes específicos de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="8cde1-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="8cde1-120">Los estados relacionados con el estado de los recursos de una red CDN de Azure se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="8cde1-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="8cde1-121">Message</span><span class="sxs-lookup"><span data-stu-id="8cde1-121">Message</span></span> | <span data-ttu-id="8cde1-122">Acción recomendada</span><span class="sxs-lookup"><span data-stu-id="8cde1-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="8cde1-123">Es posible que haya detenido, quitado o configurado de forma incorrecta uno o más de los puntos de conexión de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="8cde1-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="8cde1-124">Es posible que haya detenido, quitado o configurado de forma incorrecta uno o más de los puntos de conexión de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="8cde1-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="8cde1-125">El servicio de administración de la red CDN no está disponible en estos momentos.</span><span class="sxs-lookup"><span data-stu-id="8cde1-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="8cde1-126">Vuelva aquí para ver actualizaciones de estado. Si el problema persiste después del tiempo de resolución esperado, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="8cde1-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="8cde1-127">Es posible que los puntos de conexión de la red CDN se vean afectados por problemas continuos con algunos de nuestros proveedores de redes CDN.</span><span class="sxs-lookup"><span data-stu-id="8cde1-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="8cde1-128">Vuelva aquí para ver actualizaciones de estado. Use la herramienta de solución de problemas para obtener información sobre cómo probar el origen y el punto de conexión de la red CDN. Si el problema persiste después del tiempo de resolución esperado, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="8cde1-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="8cde1-129">Los cambios de configuración en los puntos de conexión de la red CDN están experimentando retrasos en la propagación.</span><span class="sxs-lookup"><span data-stu-id="8cde1-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="8cde1-130">Vuelva aquí para ver actualizaciones de estado. Si los cambios de configuración no se propagan por completo en el tiempo esperado, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="8cde1-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="8cde1-131">Tenemos problemas al cargar el portal complementario.</span><span class="sxs-lookup"><span data-stu-id="8cde1-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="8cde1-132">Vuelva aquí para ver actualizaciones de estado. Si el problema persiste después del tiempo de resolución esperado, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="8cde1-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="8cde1-133">Tenemos problemas con algunos de nuestros proveedores de red CDN.</span><span class="sxs-lookup"><span data-stu-id="8cde1-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="8cde1-134">Vuelva aquí para ver actualizaciones de estado. Si el problema persiste después del tiempo de resolución esperado, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="8cde1-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8cde1-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8cde1-135">Next steps</span></span>

- [<span data-ttu-id="8cde1-136">Información general sobre el estado de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="8cde1-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="8cde1-137">Solución de problemas de la compresión en la red CDN</span><span class="sxs-lookup"><span data-stu-id="8cde1-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="8cde1-138">Solución de problemas de errores 404</span><span class="sxs-lookup"><span data-stu-id="8cde1-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)