---
title: aaaHandling las alertas de seguridad en el centro de seguridad de Azure | Documentos de Microsoft
description: Este documento le ayuda a incidentes de seguridad de toohandle capacidades de toouse centro de seguridad de Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="8d0bf-103">Control de incidentes de seguridad en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8d0bf-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="8d0bf-104">Clasificación e investigación de alertas de seguridad pueden llevar mucho tiempo para los analistas de seguridad más cualificados incluso hello y para muchos es tooeven difícil saber dónde toobegin.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-104">Triaging and investigating security alerts can be time consuming for even hello most skilled security analysts, and for many it is hard tooeven know where toobegin.</span></span> <span data-ttu-id="8d0bf-105">Mediante el uso de [análisis](security-center-detection-capabilities.md) tooconnect información de hello entre distintos [alertas de seguridad](security-center-managing-and-responding-alerts.md), centro de seguridad puede proporcionar una vista única de una campaña de ataque y todas las de hello relacionadas alertas: también puede comprender rápidamente qué atacante de hello acciones tardó y qué recursos se vieron afectados.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-105">By using [analytics](security-center-detection-capabilities.md) tooconnect hello information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of hello related alerts – you can quickly understand what actions hello attacker took and what resources were impacted.</span></span>

<span data-ttu-id="8d0bf-106">Este documento describe cómo toouse seguridad avisarle capacidad en el centro de seguridad tooassist control de incidentes de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-106">This document discusses how toouse security alert capability in Security Center tooassist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="8d0bf-107">¿Qué es un incidente de seguridad?</span><span class="sxs-lookup"><span data-stu-id="8d0bf-107">What is a security incident?</span></span>
<span data-ttu-id="8d0bf-108">En Security Center, un incidente de seguridad es la suma de todas las alertas de un recurso que se alinean con patrones de [cadenas de eliminación](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) .</span><span class="sxs-lookup"><span data-stu-id="8d0bf-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="8d0bf-109">Incidentes aparecen en hello [alertas de seguridad](security-center-managing-and-responding-alerts.md) mosaico y hoja.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-109">Incidents appear in hello [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="8d0bf-110">Un incidente revelará lista Hola de alertas relacionadas, lo que permite tooobtain obtener más información sobre cada repetición.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-110">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="8d0bf-111">Administración de incidentes de seguridad</span><span class="sxs-lookup"><span data-stu-id="8d0bf-111">Managing security incidents</span></span>
<span data-ttu-id="8d0bf-112">Puede revisar los incidentes de seguridad actual examinando el icono de alertas de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-112">You can review your current security incidents by looking at hello security alerts tile.</span></span> <span data-ttu-id="8d0bf-113">Acceso Hola Portal de Azure y siga estos pasos hello toosee más detalles sobre cada incidente de seguridad:</span><span class="sxs-lookup"><span data-stu-id="8d0bf-113">Access hello Azure Portal and follow hello steps below toosee more details about each security incident:</span></span>

1. <span data-ttu-id="8d0bf-114">En el panel del centro de seguridad de hello, verá hello **alertas de seguridad** icono.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-114">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Icono Alertas de seguridad en Security Center](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="8d0bf-116">Haga clic en este icono tooexpand, y si se detecta un incidente de seguridad, aparecerá en el gráfico de alertas de seguridad de hello tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="8d0bf-116">Click on this tile tooexpand it and if a security incident is detected, it will appear under hello security alerts graph as shown  below:</span></span>

    ![Incidente de seguridad](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="8d0bf-118">Observe que la descripción de incidentes de seguridad de hello tiene un icono diferente en comparación con las alertas de tooother.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-118">Notice that hello security incident description has a different icon compared tooother alerts.</span></span> <span data-ttu-id="8d0bf-119">Haga clic en ella tooview más detalles sobre este incidente.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-119">Click on it tooview more details about this incident.</span></span>

    ![Incidente de seguridad](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="8d0bf-121">En hello **incidente** hoja verá más detalles sobre este incidente de seguridad, que incluye su descripción completa, su gravedad (que en este caso es alta), su estado actual (en este caso sigue siendo *activo*, lo cual implica usuario hello no ha tomado un tooit de acción: puede hacerlo haciendo clic en incidente Hola Hola **alertas de seguridad** hoja), Hola atacadas recursos (en este caso *VM1*) Hola pasos de corrección de incidente de hello y, en el panel inferior de hello tiene alertas de Hola que se incluyeron en este incidente.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-121">On hello **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies hello user hasn't taken an action tooit - this can be done by right clicking on hello incident in hello **Security alerts** blade), hello attacked resource (in this case *VM1*), hello remediation steps for hello incident, and in hello bottom pane you have hello alerts that were included in this incident.</span></span> <span data-ttu-id="8d0bf-122">Si desea obtener más información sobre cada alerta tooobtain, simplemente haga clic en él y otra hoja se abrirá, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="8d0bf-122">If you want tooobtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![Incidente de seguridad](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="8d0bf-124">información de Hello en esta hoja variará alerta de toohello correspondiente.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-124">hello information on this blade will vary according toohello alert.</span></span> <span data-ttu-id="8d0bf-125">Lectura [toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) para obtener más información acerca de cómo toomanage estas alertas.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-125">Read [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how toomanage these alerts.</span></span> <span data-ttu-id="8d0bf-126">Algunas consideraciones importantes con respecto a esta funcionalidad son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="8d0bf-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="8d0bf-127">Un nuevo filtro le permite toocustomize que su tooIncident vista únicamente, las alertas sólo, o ambos.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-127">A new filter enables you toocustomize your view tooIncident only, Alerts only, or both.</span></span>
* <span data-ttu-id="8d0bf-128">Hola misma alerta puede existir como parte de un incidente (si procede), así como toobe visible como una alerta independiente.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-128">hello same alert can exist as part of an Incident (if applicable), as well as toobe visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="8d0bf-129">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="8d0bf-129">See also</span></span>
<span data-ttu-id="8d0bf-130">En este documento, aprendió cómo toouse Hola capacidad de incidentes de seguridad en el centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-130">In this document, you learned how toouse hello security incident capability in Security Center.</span></span> <span data-ttu-id="8d0bf-131">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8d0bf-131">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="8d0bf-132">Administrar y responder a alertas de toosecurity en el centro de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="8d0bf-132">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="8d0bf-133">Funcionalidades de detección de Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8d0bf-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="8d0bf-134">Guía de planeamiento y operaciones de Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8d0bf-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="8d0bf-135">Administrar y responder a alertas de toosecurity en el centro de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="8d0bf-135">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="8d0bf-136">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md)--buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="8d0bf-137">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre entradas de blog sobre el cumplimiento y la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0bf-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
