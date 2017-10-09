---
title: estado de hello aaaMonitor de recursos de red CDN de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor Hola mantenimiento de los recursos de red CDN de Azure mediante el mantenimiento de recursos de Azure."
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
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a><span data-ttu-id="79e3e-103">Supervisar el estado de Hola de recursos de red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="79e3e-103">Monitor hello health of Azure CDN resources</span></span>
  
<span data-ttu-id="79e3e-104">El estado de los recursos de la red CDN de Azure es un subconjunto de [Estado de los recursos de Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79e3e-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="79e3e-105">Puede utilizar Mantenimiento de hello toomonitor Azure recursos de mantenimiento de recursos de red CDN y problemas de tootroubleshoot las instrucciones de recepción.</span><span class="sxs-lookup"><span data-stu-id="79e3e-105">You can use Azure resource health toomonitor hello health of CDN resources and receive actionable guidance tootroubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="79e3e-106">Mantenimiento de recursos de red CDN de Azure actualmente solo las cuentas para el estado de Hola de entrega de CDN global y funciones de API.</span><span class="sxs-lookup"><span data-stu-id="79e3e-106">Azure CDN resource health only currently accounts for hello health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="79e3e-107">El estado de los recursos de la red CDN de Azure no comprueba los puntos de conexión individuales de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="79e3e-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="79e3e-108">señales de Hello esa fuente mantenimiento de recursos de red CDN de Azure pueden ser up too15 minutos.</span><span class="sxs-lookup"><span data-stu-id="79e3e-108">hello signals that feed Azure CDN resource health may be up too15 minutes delayed.</span></span>

## <a name="how-toofind-azure-cdn-resource-health"></a><span data-ttu-id="79e3e-109">¿Cómo toofind mantenimiento de recursos de red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="79e3e-109">How toofind Azure CDN resource health</span></span>

1. <span data-ttu-id="79e3e-110">Hola [portal de Azure](https://portal.azure.com), examinar el perfil de CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="79e3e-110">In hello [Azure portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>

2. <span data-ttu-id="79e3e-111">Haga clic en hello **configuración** botón.</span><span class="sxs-lookup"><span data-stu-id="79e3e-111">Click hello **Settings** button.</span></span>

    ![Botón Configuración](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="79e3e-113">En *Soporte y solución de problemas*, haga clic en **Estado de los recursos**.</span><span class="sxs-lookup"><span data-stu-id="79e3e-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![Estado de los recursos de la red CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="79e3e-115">También puede encontrar recursos de red CDN enumerados en hello *estado de los recursos* el icono Servicios hello *ayuda y soporte técnico* hoja.</span><span class="sxs-lookup"><span data-stu-id="79e3e-115">You can also find CDN resources listed in hello *Resource health* tile in hello *Help + support* blade.</span></span>  <span data-ttu-id="79e3e-116">¿Puede obtener demasiado rápidamente*ayuda y soporte técnico* haciendo clic en hello en un círculo **?**</span><span class="sxs-lookup"><span data-stu-id="79e3e-116">You can quickly get too*Help + support* by clicking hello circled **?**</span></span> <span data-ttu-id="79e3e-117">en hello esquina superior derecha del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="79e3e-117">in hello upper right corner of hello portal.</span></span>
>
> ![Ayuda y soporte técnico](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="79e3e-119">Mensajes específicos de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="79e3e-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="79e3e-120">Mantenimiento de recursos de red CDN de Estados tooAzure relacionado se encuentra por debajo.</span><span class="sxs-lookup"><span data-stu-id="79e3e-120">Statuses related tooAzure CDN resource health can be found below.</span></span>

|<span data-ttu-id="79e3e-121">Message</span><span class="sxs-lookup"><span data-stu-id="79e3e-121">Message</span></span> | <span data-ttu-id="79e3e-122">Acción recomendada</span><span class="sxs-lookup"><span data-stu-id="79e3e-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="79e3e-123">Es posible que haya detenido, quitado o configurado de forma incorrecta uno o más de los puntos de conexión de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="79e3e-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="79e3e-124">Es posible que haya detenido, quitado o configurado de forma incorrecta uno o más de los puntos de conexión de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="79e3e-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="79e3e-125">Lo sentimos, el servicio de administración de red CDN Hola no está disponible actualmente</span><span class="sxs-lookup"><span data-stu-id="79e3e-125">We are sorry, hello CDN management service is currently unavailable</span></span> | <span data-ttu-id="79e3e-126">Vuelva aquí para las actualizaciones de estado; comprobar Si el problema persiste después de hello espera el tiempo de resolución, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="79e3e-126">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
|<span data-ttu-id="79e3e-127">Es posible que los puntos de conexión de la red CDN se vean afectados por problemas continuos con algunos de nuestros proveedores de redes CDN.</span><span class="sxs-lookup"><span data-stu-id="79e3e-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="79e3e-128">Vuelva aquí para las actualizaciones de estado; comprobar Usar toolearn de herramienta de solución de problemas de hello cómo tootest su origen y el punto de conexión de red CDN; Si el problema persiste después de hello espera el tiempo de resolución, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="79e3e-128">Check back here for status updates; Use hello Troubleshoot tool toolearn how tootest your origin and CDN endpoint; If your problem persists after hello expected resolution time, contact support.</span></span> |
|<span data-ttu-id="79e3e-129">Los cambios de configuración en los puntos de conexión de la red CDN están experimentando retrasos en la propagación.</span><span class="sxs-lookup"><span data-stu-id="79e3e-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="79e3e-130">Vuelva aquí para las actualizaciones de estado; comprobar Si los cambios de configuración no se ha propagado completamente en el tiempo de espera de hello, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="79e3e-130">Check back here for status updates; If your configuration changes are not fully propagated in hello expected time, contact support.</span></span>|
|<span data-ttu-id="79e3e-131">Lo sentimos, que estamos sufriendo problemas el cargar portal complementario de Hola</span><span class="sxs-lookup"><span data-stu-id="79e3e-131">We're sorry, we are experiencing issues loading hello supplemental portal</span></span> | <span data-ttu-id="79e3e-132">Vuelva aquí para las actualizaciones de estado; comprobar Si el problema persiste después de hello espera el tiempo de resolución, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="79e3e-132">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
<span data-ttu-id="79e3e-133">Tenemos problemas con algunos de nuestros proveedores de red CDN.</span><span class="sxs-lookup"><span data-stu-id="79e3e-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="79e3e-134">Vuelva aquí para las actualizaciones de estado; comprobar Si el problema persiste después de hello espera el tiempo de resolución, póngase en contacto con el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="79e3e-134">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="79e3e-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79e3e-135">Next steps</span></span>

- [<span data-ttu-id="79e3e-136">Información general sobre el estado de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="79e3e-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="79e3e-137">Solución de problemas de la compresión en la red CDN</span><span class="sxs-lookup"><span data-stu-id="79e3e-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="79e3e-138">Solución de problemas de errores 404</span><span class="sxs-lookup"><span data-stu-id="79e3e-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)