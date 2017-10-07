---
title: aaaManage las alertas de seguridad en el centro de seguridad de Azure | Documentos de Microsoft
description: Este documento le ayuda a toouse Azure Security Center capacidades toomanage y responde toosecurity alertas.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a><span data-ttu-id="92399-103">Administrar y responder a alertas de toosecurity en el centro de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="92399-103">Managing and responding toosecurity alerts in Azure Security Center</span></span>
<span data-ttu-id="92399-104">Este documento le ayuda a usar Azure Security Center toomanage y responder toosecurity alertas.</span><span class="sxs-lookup"><span data-stu-id="92399-104">This document helps you use Azure Security Center toomanage and respond toosecurity alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="92399-105">detecciones de tooenable avanzada, tooAzure actualización estándar de centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="92399-105">tooenable advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="92399-106">Hay disponible una versión de evaluación gratuita de 60 días.</span><span class="sxs-lookup"><span data-stu-id="92399-106">A free 60-day trial is available.</span></span> <span data-ttu-id="92399-107">tooupgrade, seleccione nivel de precios en hello [directiva de seguridad](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="92399-107">tooupgrade, select Pricing Tier in hello [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="92399-108">Vea [precios de Azure Security Center](security-center-pricing.md) toolearn más.</span><span class="sxs-lookup"><span data-stu-id="92399-108">See [Azure Security Center pricing](security-center-pricing.md) toolearn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="92399-109">¿Qué son las alertas de seguridad?</span><span class="sxs-lookup"><span data-stu-id="92399-109">What are security alerts?</span></span>
<span data-ttu-id="92399-110">Centro de seguridad automáticamente recopila, analiza y se integra datos de registro de los recursos de Azure, red de hello, soluciones de socios comerciales, así como soluciones de protección firewall y de punto de conexión, toodetect reales amenazas conectadas y reducir los falsos positivos.</span><span class="sxs-lookup"><span data-stu-id="92399-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="92399-111">Se muestra una lista de alertas de seguridad con prioridades en el centro de seguridad junto con hello información que necesita tooquickly investigar el problema de Hola y recomendaciones sobre cómo tooremediate un ataque.</span><span class="sxs-lookup"><span data-stu-id="92399-111">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem and recommendations for how tooremediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="92399-112">Para más información acerca de cómo actúan las funcionalidades de detección de Security Center, consulte [Funcionalidades de detección de Azure Security Center](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="92399-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="92399-113">Administración de alertas de seguridad</span><span class="sxs-lookup"><span data-stu-id="92399-113">Managing security alerts</span></span>
<span data-ttu-id="92399-114">Puede revisar las alertas actuales examinando hello **alertas de seguridad** icono.</span><span class="sxs-lookup"><span data-stu-id="92399-114">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="92399-115">Abra el Portal de Azure y siga estos pasos hello toosee más detalles sobre cada alerta:</span><span class="sxs-lookup"><span data-stu-id="92399-115">Open Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="92399-116">En el panel del centro de seguridad de hello, verá hello **alertas de seguridad** icono.</span><span class="sxs-lookup"><span data-stu-id="92399-116">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Icono Alertas de seguridad en Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="92399-118">Haga clic en Hola mosaico tooopen Hola **alertas de seguridad** hoja que contiene información más detallada acerca de hello alertas tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="92399-118">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts as shown below.</span></span>

   ![hoja de alertas de seguridad de Hello en el centro de seguridad](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="92399-120">En la parte inferior de Hola de esta hoja son los detalles de Hola para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="92399-120">In hello bottom part of this blade are hello details for each alert.</span></span> <span data-ttu-id="92399-121">toosort, haga clic en la columna de Hola que desea toosort por.</span><span class="sxs-lookup"><span data-stu-id="92399-121">toosort, click hello column that you want toosort by.</span></span> <span data-ttu-id="92399-122">definición de Hola para cada columna se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="92399-122">hello definition for each column is given below:</span></span>

* <span data-ttu-id="92399-123">**Descripción**: una breve explicación de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="92399-123">**Description**: A brief explanation of hello alert.</span></span>
* <span data-ttu-id="92399-124">**Recuento**: una lista de todas las alertas de este tipo específico que se han detectado en un día concreto.</span><span class="sxs-lookup"><span data-stu-id="92399-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="92399-125">**Detectado por**: Hola servicio que era responsable de activar la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="92399-125">**Detected by**: hello service that was responsible for triggering hello alert.</span></span>
* <span data-ttu-id="92399-126">**Fecha**: Hola fecha ese evento Hola se ha producido.</span><span class="sxs-lookup"><span data-stu-id="92399-126">**Date**: hello date that hello event occurred.</span></span>
* <span data-ttu-id="92399-127">**Estado**: Hola estado actual de esa alerta.</span><span class="sxs-lookup"><span data-stu-id="92399-127">**State**: hello current state for that alert.</span></span> <span data-ttu-id="92399-128">Existen dos tipos de servicios:</span><span class="sxs-lookup"><span data-stu-id="92399-128">There are two types of states:</span></span>
  * <span data-ttu-id="92399-129">**Active**: se detectó la alerta de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="92399-129">**Active**: hello security alert has been detected.</span></span>
* <span data-ttu-id="92399-130">**Gravedad**: nivel de gravedad de hello, que puede ser alta, Media o baja.</span><span class="sxs-lookup"><span data-stu-id="92399-130">**Severity**: hello severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="92399-131">Filtrado de alertas</span><span class="sxs-lookup"><span data-stu-id="92399-131">Filtering alerts</span></span>
<span data-ttu-id="92399-132">Puede filtrar alertas en función de la fecha, el estado y la gravedad.</span><span class="sxs-lookup"><span data-stu-id="92399-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="92399-133">Filtrar las alertas puede ser útil para escenarios donde es necesario ámbito de hello toonarrow de presentación de las alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="92399-133">Filtering alerts can be useful for scenarios where you need toonarrow hello scope of security alerts show.</span></span> <span data-ttu-id="92399-134">Por ejemplo, puede que también desee tooaddress alertas de seguridad que se produzcan en hello últimas 24 horas dado que se está investigando una posible infracción en sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="92399-134">For example, you might you want tooaddress security alerts that occurred in hello last 24 hours because you are investigating a potential breach in hello system.</span></span>

1. <span data-ttu-id="92399-135">Haga clic en **filtro** en hello **alertas de seguridad** hoja.</span><span class="sxs-lookup"><span data-stu-id="92399-135">Click **Filter** on hello **Security Alerts** blade.</span></span> <span data-ttu-id="92399-136">Hola **filtro** abre la hoja y seleccione valores de fecha, el estado y la gravedad de hello desea toosee.</span><span class="sxs-lookup"><span data-stu-id="92399-136">hello **Filter** blade opens and you select hello date, state, and severity values you wish toosee.</span></span>

    ![Filtrado de alertas en Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a><span data-ttu-id="92399-138">Responder toosecurity alertas</span><span class="sxs-lookup"><span data-stu-id="92399-138">Respond toosecurity alerts</span></span>
<span data-ttu-id="92399-139">Seleccione un toolearn de alerta de seguridad más información acerca de los eventos de Hola que desencadenó la alerta de Hola y qué, si existe, los pasos necesitan tootake tooremediate un ataque.</span><span class="sxs-lookup"><span data-stu-id="92399-139">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="92399-140">Las alertas de seguridad se agrupan según el tipo y la fecha.</span><span class="sxs-lookup"><span data-stu-id="92399-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="92399-141">Al hacer clic en una alerta de seguridad se abrirá una hoja que contiene una lista de alertas de hello agrupado.</span><span class="sxs-lookup"><span data-stu-id="92399-141">Clicking a security alert will open a blade containing a list of hello grouped alerts.</span></span>

![Responder toosecurity alertas en el centro de seguridad de Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="92399-143">En este caso, las alertas de Hola que se han activado consulte toosuspicious actividad de protocolo de escritorio remoto (RDP).</span><span class="sxs-lookup"><span data-stu-id="92399-143">In this case, hello alerts that were triggered refer toosuspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="92399-144">Hola primera columna muestra qué recursos atacados; en segundo lugar, Hello muestra cuántas veces se atacadas recursos Hola; Hola tercero muestra el tiempo de Hola de ataque de hello; Hola cuarto muestra el estado de alerta de hello; y Hola quinto muestra gravedad Hola de ataque de Hola.</span><span class="sxs-lookup"><span data-stu-id="92399-144">hello first column shows which resources were attacked; hello second shows how many times hello resource was attacked; hello third shows hello time of hello attack; hello fourth shows state of hello alert; and hello fifth shows hello severity of hello attack.</span></span> <span data-ttu-id="92399-145">Después de revisar esta información, haga clic en recurso de Hola que estaba atacada y se abrirá una nueva hoja.</span><span class="sxs-lookup"><span data-stu-id="92399-145">After reviewing this information, click hello resource that was attacked and a new blade will open.</span></span>

![Sugerencias para qué toodo sobre la seguridad de las alertas en el centro de seguridad de Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="92399-147">Hola **descripción** campo de esta hoja encontrará más detalles sobre este evento.</span><span class="sxs-lookup"><span data-stu-id="92399-147">In hello **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="92399-148">Estos detalles adicionales proporcionan una visión general de qué Hola desencadenadas seguridad alerta, Hola recurso de destino, cuando Hola procede del origen de dirección IP y recomendaciones sobre cómo tooremediate.</span><span class="sxs-lookup"><span data-stu-id="92399-148">These additional details offer insight into what triggered hello security alert, hello target resource, when applicable hello source IP address, and recommendations about how tooremediate.</span></span>  <span data-ttu-id="92399-149">En algunos casos, dirección IP de origen de Hola se vaciará (no disponible) porque no todos los registros de eventos de seguridad de Windows incluyen la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="92399-149">In some instances, hello source IP address will be empty (not available) because not all Windows security events logs include hello IP address.</span></span>

<span data-ttu-id="92399-150">corrección de Hello sugerido por centro de seguridad variará alerta de seguridad toohello correspondiente.</span><span class="sxs-lookup"><span data-stu-id="92399-150">hello remediation suggested by Security Center will vary according toohello security alert.</span></span> <span data-ttu-id="92399-151">En algunos casos, puede que tenga toouse otro tooimplement las capacidades de Azure Hola recomendada corrección.</span><span class="sxs-lookup"><span data-stu-id="92399-151">In some cases, you may have toouse other Azure capabilities tooimplement hello recommended remediation.</span></span> <span data-ttu-id="92399-152">Por ejemplo, Hola corrección para este tipo de ataque es la dirección IP de tooblacklist Hola que genera este tipo de ataque mediante el uso de un [ACL de red](../virtual-network/virtual-networks-acl.md) o un [grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md) regla.</span><span class="sxs-lookup"><span data-stu-id="92399-152">For example, hello remediation for this attack is tooblacklist hello IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="92399-153">Para obtener más información acerca de diferentes tipos de alertas de hello, lea [alertas de seguridad por tipo de Azure Security Center](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="92399-153">For more information on hello different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="92399-154">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="92399-154">See also</span></span>
<span data-ttu-id="92399-155">En este documento, se habrá aprendido cómo tooconfigure las directivas de seguridad en el centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="92399-155">In this document, you learned how tooconfigure security policies in Security Center.</span></span> <span data-ttu-id="92399-156">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="92399-156">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="92399-157">Control de incidentes de seguridad en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="92399-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="92399-158">Funcionalidades de detección de Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="92399-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="92399-159">Guía de planeamiento y operaciones de Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="92399-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="92399-160">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="92399-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="92399-161">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="92399-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
