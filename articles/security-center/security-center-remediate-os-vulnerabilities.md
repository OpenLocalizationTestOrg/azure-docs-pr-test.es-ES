---
title: vulnerabilidades de aaaRemediate sistema operativo en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** SO corregir vulnerabilidades **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="f2a3c-103">Corrección de vulnerabilidades del SO en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f2a3c-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="f2a3c-104">Centro de seguridad de Azure diariamente analiza el sistema de operativo (SO) de máquina virtual (VM) para las configuraciones que pudieron realizar Hola VM cambios de configuración sean más vulnerable de tooattack y recomienda tooaddress estas vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make hello VM more vulnerable tooattack and recommends configuration changes tooaddress these vulnerabilities.</span></span> <span data-ttu-id="f2a3c-105">Centro de seguridad, se recomienda que resolver vulnerabilidades cuando la configuración del sistema operativo de la máquina virtual no coincide con hello reglas de configuración recomendada.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match hello recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="f2a3c-106">Para obtener más información sobre configuraciones específicas de Hola que se está supervisando, vea hello [lista de reglas de configuración recomendada](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="f2a3c-106">For more information on hello specific configurations being monitored, see hello [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="f2a3c-107">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="f2a3c-107">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="f2a3c-108">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="f2a3c-109">Este documento no es una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="f2a3c-110">Hola **recomendaciones** hoja, seleccione **vulnerabilidades de sistema operativo corregir**.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-110">In hello **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="f2a3c-111">![Corrección de vulnerabilidades del SO][1]</span><span class="sxs-lookup"><span data-stu-id="f2a3c-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="f2a3c-112">Hola **vulnerabilidades de sistema operativo corregir** hoja se abre y muestra las máquinas virtuales con las configuraciones de sistema operativo que no coincide con hello reglas de configuración recomendada.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-112">hello **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match hello recommended configuration rules.</span></span>  <span data-ttu-id="f2a3c-113">Para cada máquina virtual, hoja de hello identifica:</span><span class="sxs-lookup"><span data-stu-id="f2a3c-113">For each VM, hello blade identifies:</span></span>

   * <span data-ttu-id="f2a3c-114">**No se pudo reglas** --hello número de reglas que Hola configuración del sistema operativo de la máquina virtual con error.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-114">**FAILED RULES** -- hello number of rules that hello VM's OS configuration failed.</span></span>
   * <span data-ttu-id="f2a3c-115">**HORA del último RECORRIDO** : fecha de Hola y tiempo que el centro de seguridad última vez la configuración del sistema operativo de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-115">**LAST SCAN TIME** -- hello date and time that Security Center last scanned hello VM’s OS configuration.</span></span>
   * <span data-ttu-id="f2a3c-116">**ESTADO** : Hola estado actual de vulnerabilidades de hello:</span><span class="sxs-lookup"><span data-stu-id="f2a3c-116">**STATE** -- hello current state of hello vulnerability:</span></span>

     * <span data-ttu-id="f2a3c-117">Abierta: vulnerabilidades de hello no se ha solucionado aún</span><span class="sxs-lookup"><span data-stu-id="f2a3c-117">Open: hello vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="f2a3c-118">En curso: Una vulnerabilidad de saludo se está aplicando actualmente, no se requiere ninguna acción por parte del usuario</span><span class="sxs-lookup"><span data-stu-id="f2a3c-118">In Progress: hello vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="f2a3c-119">Resolver: vulnerabilidades de hello ya se ha solucionado (cuando se ha resuelto el problema de hello, entrada Hola está atenuado)</span><span class="sxs-lookup"><span data-stu-id="f2a3c-119">Resolved: hello vulnerability was already addressed (when hello issue has been resolved, hello entry is grayed out)</span></span>
   * <span data-ttu-id="f2a3c-120">**GRAVEDAD** --todas las vulnerabilidades se establecen tooa gravedad baja, lo que significa que debe llevar a cabo una vulnerabilidad, pero no requiere atención inmediata.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-120">**SEVERITY** -- All vulnerabilities are set tooa severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="f2a3c-121">Seleccione una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-121">Select a VM.</span></span> <span data-ttu-id="f2a3c-122">Una hoja para VM se abre y muestra las reglas de Hola que han producido un error.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-122">A blade for that VM opens and displays hello rules that have failed.</span></span>
   <span data-ttu-id="f2a3c-123">![Reglas de configuración con error][2]</span><span class="sxs-lookup"><span data-stu-id="f2a3c-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="f2a3c-124">Seleccione una regla.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-124">Select a rule.</span></span> <span data-ttu-id="f2a3c-125">En este ejemplo, seleccionamos **La contraseña debe cumplir los requisitos de complejidad**.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="f2a3c-126">Una hoja abre el impacto de hello y regla de hello no se pudo que describe.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-126">A blade opens describing hello failed rule and hello impact.</span></span> <span data-ttu-id="f2a3c-127">Revise los detalles de Hola y tenga en cuenta cómo se aplican las configuraciones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-127">Review hello details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="f2a3c-128">![Descripción de la regla de error de Hola][3]</span><span class="sxs-lookup"><span data-stu-id="f2a3c-128">![Description for hello failed rule][3]</span></span>

  <span data-ttu-id="f2a3c-129">Centro de seguridad utiliza identificadores únicos de tooassign Common Configuration Enumeration (CCE) para las reglas de configuración.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-129">Security Center uses Common Configuration Enumeration (CCE) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="f2a3c-130">Hola siguiente información se proporciona en esta hoja:</span><span class="sxs-lookup"><span data-stu-id="f2a3c-130">hello following information is provided on this blade:</span></span>

  - <span data-ttu-id="f2a3c-131">NOMBRE: nombre de la regla.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="f2a3c-132">GRAVEDAD: valor de gravedad de CCE, que puede ser Crítico, Importante o Advertencia.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="f2a3c-133">CCIED--Identificador único CCE para regla de Hola</span><span class="sxs-lookup"><span data-stu-id="f2a3c-133">CCIED -- CCE unique identifier for hello rule</span></span>
  - <span data-ttu-id="f2a3c-134">DESCRIPCIÓN: descripción de la regla.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="f2a3c-135">VULNERABILIDAD: explicación de la vulnerabilidad o el riesgo si no se aplica la regla.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="f2a3c-136">IMPACTO: impacto de negocio cuando se aplica la regla.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="f2a3c-137">VALOR esperado: Valor que se esperaba al centro de seguridad analiza la configuración de sistema operativo de la máquina virtual con la regla de Hola</span><span class="sxs-lookup"><span data-stu-id="f2a3c-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="f2a3c-138">OPERACIÓN de regla: Operación utilizada por el centro de seguridad durante el análisis de la configuración del sistema operativo de la máquina virtual con la regla de Hola de reglas</span><span class="sxs-lookup"><span data-stu-id="f2a3c-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="f2a3c-139">VALOR real: Valor devuelto después del análisis de la configuración del sistema operativo de la máquina virtual con la regla de Hola</span><span class="sxs-lookup"><span data-stu-id="f2a3c-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="f2a3c-140">RESULTADO DE LA EVALUACIÓN: resultado del análisis, que puede ser Sin errores o Con errores.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="f2a3c-141">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="f2a3c-141">See also</span></span>
<span data-ttu-id="f2a3c-142">En este artículo se ha explicado cómo tooimplement Hola centro de seguridad recomendación "corregir SO vulnerabilidades."</span><span class="sxs-lookup"><span data-stu-id="f2a3c-142">This article showed you how tooimplement hello Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="f2a3c-143">Puede revisar el conjunto de Hola de reglas de configuración de [aquí](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="f2a3c-143">You can review hello set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="f2a3c-144">Centro de seguridad utiliza identificadores únicos de tooassign CCE (enumeración de configuración común) para las reglas de configuración.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-144">Security Center uses CCE (Common Configuration Enumeration) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="f2a3c-145">Visite hello [CCE](https://nvd.nist.gov/cce/index.cfm) sitio para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-145">Visit hello [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="f2a3c-146">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f2a3c-146">toolearn more about Security Center, see hello following resources:</span></span>

* <span data-ttu-id="f2a3c-147">[Plataformas compatibles con Azure Security Center](security-center-os-coverage.md): proporciona una lista de máquinas virtuales Windows y Linux compatibles.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="f2a3c-148">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) -Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f2a3c-149">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f2a3c-150">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) -Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="f2a3c-151">[Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) -Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-151">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="f2a3c-152">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) -Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="f2a3c-153">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) -buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="f2a3c-154">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a3c-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
