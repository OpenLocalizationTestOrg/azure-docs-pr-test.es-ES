---
title: "Administración de alertas de seguridad en Azure Security Center | Microsoft Docs"
description: Este documento le ayuda a usar las capacidades del Centro de seguridad de Azure para administrar y responder a las alertas de seguridad.
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
ms.openlocfilehash: 56fcfbfdbe15749132ba6a27861142fd564063c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="managing-and-responding-to-security-alerts-in-azure-security-center"></a><span data-ttu-id="adbef-103">Administración y respuesta a las alertas de seguridad en el Centro de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="adbef-103">Managing and responding to security alerts in Azure Security Center</span></span>
<span data-ttu-id="adbef-104">Este documento le ayuda a usar Azure Security Center para administrar las alertas de seguridad y responder a ellas.</span><span class="sxs-lookup"><span data-stu-id="adbef-104">This document helps you use Azure Security Center to manage and respond to security alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="adbef-105">Para habilitar las detecciones avanzadas, actualice a la versión estándar de Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="adbef-105">To enable advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="adbef-106">Hay disponible una versión de evaluación gratuita de 60 días.</span><span class="sxs-lookup"><span data-stu-id="adbef-106">A free 60-day trial is available.</span></span> <span data-ttu-id="adbef-107">Para realizar la actualización, seleccione el plan de tarifa en la [directiva de seguridad](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="adbef-107">To upgrade, select Pricing Tier in the [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="adbef-108">Consulte [Precios de Azure Security Center](security-center-pricing.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="adbef-108">See [Azure Security Center pricing](security-center-pricing.md) to learn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="adbef-109">¿Qué son las alertas de seguridad?</span><span class="sxs-lookup"><span data-stu-id="adbef-109">What are security alerts?</span></span>
<span data-ttu-id="adbef-110">Security Center recopila, analiza e integra automáticamente los datos de registro de los recursos de Azure, la red y las soluciones de asociados conectados, como firewalls y soluciones de protección de puntos de conexión, para detectar amenazas reales y reducir los falsos positivos.</span><span class="sxs-lookup"><span data-stu-id="adbef-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives.</span></span> <span data-ttu-id="adbef-111">En Security Center, se muestra una lista de alertas de seguridad prioritarias, junto con la información que necesita para investigar rápidamente y recomendaciones para corregir un ataque.</span><span class="sxs-lookup"><span data-stu-id="adbef-111">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="adbef-112">Para más información acerca de cómo actúan las funcionalidades de detección de Security Center, consulte [Funcionalidades de detección de Azure Security Center](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="adbef-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="adbef-113">Administración de alertas de seguridad</span><span class="sxs-lookup"><span data-stu-id="adbef-113">Managing security alerts</span></span>
<span data-ttu-id="adbef-114">Puede revisar las alertas actuales en el icono **Alertas de seguridad** .</span><span class="sxs-lookup"><span data-stu-id="adbef-114">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="adbef-115">Abra el Portal de Azure y siga los pasos siguientes para ver más detalles sobre cada alerta:</span><span class="sxs-lookup"><span data-stu-id="adbef-115">Open Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="adbef-116">En el panel Security Center, verá el icono **Alertas de seguridad** .</span><span class="sxs-lookup"><span data-stu-id="adbef-116">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Icono Alertas de seguridad en Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="adbef-118">Haga clic en el icono para abrir la hoja **Alertas de seguridad** , que contiene más detalles acerca de las alertas, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="adbef-118">Click the tile to open the **Security alerts** blade that contains more details about the alerts as shown below.</span></span>

   ![La hoja Alertas de seguridad en Azure Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="adbef-120">En la parte inferior de esta hoja aparecen los detalles de cada alerta.</span><span class="sxs-lookup"><span data-stu-id="adbef-120">In the bottom part of this blade are the details for each alert.</span></span> <span data-ttu-id="adbef-121">Para ordenar, haga clic en la columna que desea ordenar.</span><span class="sxs-lookup"><span data-stu-id="adbef-121">To sort, click the column that you want to sort by.</span></span> <span data-ttu-id="adbef-122">A continuación se muestra la definición de cada columna:</span><span class="sxs-lookup"><span data-stu-id="adbef-122">The definition for each column is given below:</span></span>

* <span data-ttu-id="adbef-123">**Descripción**: una breve explicación de la alerta.</span><span class="sxs-lookup"><span data-stu-id="adbef-123">**Description**: A brief explanation of the alert.</span></span>
* <span data-ttu-id="adbef-124">**Recuento**: una lista de todas las alertas de este tipo específico que se han detectado en un día concreto.</span><span class="sxs-lookup"><span data-stu-id="adbef-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="adbef-125">**Detectado por**: el servicio responsable de desencadenar la alerta.</span><span class="sxs-lookup"><span data-stu-id="adbef-125">**Detected by**: The service that was responsible for triggering the alert.</span></span>
* <span data-ttu-id="adbef-126">**Fecha**: la fecha en que se ha producido el evento.</span><span class="sxs-lookup"><span data-stu-id="adbef-126">**Date**: The date that the event occurred.</span></span>
* <span data-ttu-id="adbef-127">**Estado**: el estado actual de esa alerta.</span><span class="sxs-lookup"><span data-stu-id="adbef-127">**State**: The current state for that alert.</span></span> <span data-ttu-id="adbef-128">Existen dos tipos de servicios:</span><span class="sxs-lookup"><span data-stu-id="adbef-128">There are two types of states:</span></span>
  * <span data-ttu-id="adbef-129">**Activa**: se ha detectado la alerta de seguridad.</span><span class="sxs-lookup"><span data-stu-id="adbef-129">**Active**: The security alert has been detected.</span></span>
* <span data-ttu-id="adbef-130">**Gravedad**: el nivel de gravedad, que puede ser alto, medio o bajo.</span><span class="sxs-lookup"><span data-stu-id="adbef-130">**Severity**: The severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="adbef-131">Filtrado de alertas</span><span class="sxs-lookup"><span data-stu-id="adbef-131">Filtering alerts</span></span>
<span data-ttu-id="adbef-132">Puede filtrar alertas en función de la fecha, el estado y la gravedad.</span><span class="sxs-lookup"><span data-stu-id="adbef-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="adbef-133">Puede resultar útil filtrar las alertas en aquellos escenarios en que necesite restringir el ámbito de las alertas de seguridad que se muestran.</span><span class="sxs-lookup"><span data-stu-id="adbef-133">Filtering alerts can be useful for scenarios where you need to narrow the scope of security alerts show.</span></span> <span data-ttu-id="adbef-134">Por ejemplo, podría comprobar las alertas de seguridad que se produjeron en las 24 horas anteriores, ya que se está investigando una posible brecha en el sistema.</span><span class="sxs-lookup"><span data-stu-id="adbef-134">For example, you might you want to address security alerts that occurred in the last 24 hours because you are investigating a potential breach in the system.</span></span>

1. <span data-ttu-id="adbef-135">Haga clic en **Filtro** en la hoja **Alertas de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="adbef-135">Click **Filter** on the **Security Alerts** blade.</span></span> <span data-ttu-id="adbef-136">Se abre la hoja **Filtro** , donde podrá seleccionar los valores de fecha, estado y gravedad que desee ver.</span><span class="sxs-lookup"><span data-stu-id="adbef-136">The **Filter** blade opens and you select the date, state, and severity values you wish to see.</span></span>

    ![Filtrado de alertas en Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-to-security-alerts"></a><span data-ttu-id="adbef-138">Responder a alertas de seguridad</span><span class="sxs-lookup"><span data-stu-id="adbef-138">Respond to security alerts</span></span>
<span data-ttu-id="adbef-139">Seleccione una alerta de seguridad para ver más información sobre el evento o los eventos que la desencadenaron y, si existen, los pasos que debe seguir para corregir un ataque.</span><span class="sxs-lookup"><span data-stu-id="adbef-139">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="adbef-140">Las alertas de seguridad se agrupan según el tipo y la fecha.</span><span class="sxs-lookup"><span data-stu-id="adbef-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="adbef-141">Haga clic en una alerta de seguridad y se abrirá una hoja que contiene una lista de las alertas agrupadas.</span><span class="sxs-lookup"><span data-stu-id="adbef-141">Clicking a security alert will open a blade containing a list of the grouped alerts.</span></span>

![Responder a alertas de seguridad en el Centro de seguridad de Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="adbef-143">En este caso, las alertas desencadenadas hacen referencia a las actividades sospechosas del Protocolo de escritorio remoto (RDP).</span><span class="sxs-lookup"><span data-stu-id="adbef-143">In this case, the alerts that were triggered refer to suspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="adbef-144">En la primera columna se muestran los recursos atacados, en la segunda, las veces que el recurso fue atacado, en la tercera, la hora en la que se produjo el ataque, en la cuarta, el estado de la alerta y, en la quinta, la gravedad del ataque.</span><span class="sxs-lookup"><span data-stu-id="adbef-144">The first column shows which resources were attacked; the second shows how many times the resource was attacked; the third shows the time of the attack; the fourth shows state of the alert; and the fifth shows the severity of the attack.</span></span> <span data-ttu-id="adbef-145">Después de revisar esta información, haga clic en el recurso atacado y se abrirá una nueva hoja.</span><span class="sxs-lookup"><span data-stu-id="adbef-145">After reviewing this information, click the resource that was attacked and a new blade will open.</span></span>

![Sugerencias sobre qué hacer con las alertas de seguridad en el Centro de seguridad de Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="adbef-147">En el campo **Descripción** de esta hoja encontrará más detalles sobre este evento.</span><span class="sxs-lookup"><span data-stu-id="adbef-147">In the **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="adbef-148">Estos detalles adicionales ofrecen información detallada sobre lo que activó la alerta de seguridad, el recurso de destino, la dirección IP de origen si corresponde, y recomendaciones sobre cómo corregirla.</span><span class="sxs-lookup"><span data-stu-id="adbef-148">These additional details offer insight into what triggered the security alert, the target resource, when applicable the source IP address, and recommendations about how to remediate.</span></span>  <span data-ttu-id="adbef-149">En algunos casos, la dirección IP de origen estará vacía (no disponible) porque no todos los registros de eventos de seguridad de Windows incluyen la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="adbef-149">In some instances, the source IP address will be empty (not available) because not all Windows security events logs include the IP address.</span></span>

<span data-ttu-id="adbef-150">La corrección sugerida por el Centro de seguridad variará según la alerta de seguridad.</span><span class="sxs-lookup"><span data-stu-id="adbef-150">The remediation suggested by Security Center will vary according to the security alert.</span></span> <span data-ttu-id="adbef-151">En algunos casos, tendrá que utilizar otras capacidades de Azure para implementar la corrección recomendada.</span><span class="sxs-lookup"><span data-stu-id="adbef-151">In some cases, you may have to use other Azure capabilities to implement the recommended remediation.</span></span> <span data-ttu-id="adbef-152">Por ejemplo, la solución para este ataque consiste en colocar la dirección IP que lo está generando en la lista negra mediante una [ACL de red](../virtual-network/virtual-networks-acl.md) o una regla de [grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="adbef-152">For example, the remediation for this attack is to blacklist the IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="adbef-153">Para más información sobre los distintos tipos de alertas, consulte [Alertas de seguridad por tipo en Azure Security Center](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="adbef-153">For more information on the different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="adbef-154">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="adbef-154">See also</span></span>
<span data-ttu-id="adbef-155">En este documento ha aprendido a configurar directivas de seguridad en el Centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="adbef-155">In this document, you learned how to configure security policies in Security Center.</span></span> <span data-ttu-id="adbef-156">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="adbef-156">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="adbef-157">Control de incidentes de seguridad en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="adbef-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="adbef-158">Funcionalidades de detección de Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="adbef-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="adbef-159">Guía de planeamiento y operaciones de Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="adbef-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="adbef-160">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md) : encuentre las preguntas más frecuentes sobre el uso del servicio.</span><span class="sxs-lookup"><span data-stu-id="adbef-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="adbef-161">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="adbef-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
