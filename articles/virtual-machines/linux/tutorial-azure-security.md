---
title: "máquinas virtuales de Azure del centro de seguridad y Linux del aaaAzure | Documentos de Microsoft"
description: "Obtenga información sobre la seguridad para máquinas virtuales Linux de Azure con Azure Security Center."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="acf87-103">Supervisión de la seguridad de máquinas virtuales con Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="acf87-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="acf87-104">Azure Security Center puede ayudarle a conocer mejor los procedimientos de seguridad de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="acf87-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="acf87-105">Security Center ofrece una supervisión integrada de la seguridad.</span><span class="sxs-lookup"><span data-stu-id="acf87-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="acf87-106">que puede detectar las amenazas que podrían pasar desapercibidas.</span><span class="sxs-lookup"><span data-stu-id="acf87-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="acf87-107">En este tutorial, aprenderá no solo a usar Azure Security Center, sino también a:</span><span class="sxs-lookup"><span data-stu-id="acf87-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="acf87-108">Configuración de una recolección de datos</span><span class="sxs-lookup"><span data-stu-id="acf87-108">Set up data collection</span></span>
> * <span data-ttu-id="acf87-109">Configurar directivas de seguridad</span><span class="sxs-lookup"><span data-stu-id="acf87-109">Set up security policies</span></span>
> * <span data-ttu-id="acf87-110">Ver y corregir problemas de estado de la configuración</span><span class="sxs-lookup"><span data-stu-id="acf87-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="acf87-111">Revisar las amenazas que se detecten</span><span class="sxs-lookup"><span data-stu-id="acf87-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="acf87-112">Introducción a Security Center</span><span class="sxs-lookup"><span data-stu-id="acf87-112">Security Center overview</span></span>

<span data-ttu-id="acf87-113">Security Center identifica posibles problemas de configuración de máquinas virtuales (VM) y amenazas de seguridad dirigidas.</span><span class="sxs-lookup"><span data-stu-id="acf87-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="acf87-114">Aquí se incluyen las máquinas virtuales que no tienen grupos de seguridad de red, los discos sin cifrar y ataques de RDP por fuerza bruta.</span><span class="sxs-lookup"><span data-stu-id="acf87-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="acf87-115">Hola información se muestra en el panel del centro de seguridad de hello en gráficos de fácil de leer.</span><span class="sxs-lookup"><span data-stu-id="acf87-115">hello information is shown on hello Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="acf87-116">tooaccess Hola panel del centro de seguridad, en hello portal de Azure, en el menú de hello, seleccione **centro de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="acf87-116">tooaccess hello Security Center dashboard, in hello Azure portal, on hello menu, select  **Security Center**.</span></span> <span data-ttu-id="acf87-117">En el panel de hello, puede ver el estado de seguridad de Hola de su entorno de Azure, buscar un recuento de las recomendaciones actuales y ver Hola el estado actual de las alertas de amenaza.</span><span class="sxs-lookup"><span data-stu-id="acf87-117">On hello dashboard, you can see hello security health of your Azure environment, find a count of current recommendations, and view hello current state of threat alerts.</span></span> <span data-ttu-id="acf87-118">Puede expandir cada toosee de alto nivel gráfico más detalle.</span><span class="sxs-lookup"><span data-stu-id="acf87-118">You can expand each high-level chart toosee more detail.</span></span>

![Panel de Security Center](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="acf87-120">Centro de seguridad va más allá de las recomendaciones del tooprovide de detección de datos para los problemas que detecta.</span><span class="sxs-lookup"><span data-stu-id="acf87-120">Security Center goes beyond data discovery tooprovide recommendations for issues that it detects.</span></span> <span data-ttu-id="acf87-121">Por ejemplo, si se implementa una máquina virtual sin un grupo de seguridad de red conectado, Security Center mostrará una recomendación con los pasos que se pueden dar para aplicarla.</span><span class="sxs-lookup"><span data-stu-id="acf87-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="acf87-122">Obtener la corrección automatizada sin dejar el contexto de hello del centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="acf87-122">You get automated remediation without leaving hello context of Security Center.</span></span>  

![Recomendaciones](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="acf87-124">Configuración de una recolección de datos</span><span class="sxs-lookup"><span data-stu-id="acf87-124">Set up data collection</span></span>

<span data-ttu-id="acf87-125">Antes de que pueda obtener visibilidad en las configuraciones de seguridad de máquina virtual, deberá tooset la recopilación de datos del centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="acf87-125">Before you can get visibility into VM security configurations, you need tooset up Security Center data collection.</span></span> <span data-ttu-id="acf87-126">Esto implica activar la recopilación de datos y crear una cuenta de almacenamiento de Azure toohold recopilan datos.</span><span class="sxs-lookup"><span data-stu-id="acf87-126">This involves turning on data collection and creating an Azure storage account toohold collected data.</span></span> 

1. <span data-ttu-id="acf87-127">En el panel del centro de seguridad de hello, haga clic en **directiva de seguridad**y, a continuación, seleccione la suscripción.</span><span class="sxs-lookup"><span data-stu-id="acf87-127">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="acf87-128">En **Recopilación de datos**, seleccione **Activado**.</span><span class="sxs-lookup"><span data-stu-id="acf87-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="acf87-129">Seleccione una cuenta de almacenamiento, toocreate **elegir una cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="acf87-129">toocreate a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="acf87-130">Después, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="acf87-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="acf87-131">En hello **directiva de seguridad** hoja, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="acf87-131">On hello **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="acf87-132">agente de recopilación de datos de Hello centro de seguridad se instala en todas las máquinas virtuales y empiece la recopilación de datos.</span><span class="sxs-lookup"><span data-stu-id="acf87-132">hello Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="acf87-133">Configuración de una directiva de seguridad</span><span class="sxs-lookup"><span data-stu-id="acf87-133">Set up a security policy</span></span>

<span data-ttu-id="acf87-134">Las directivas de seguridad son elementos de Hola de toodefine usado para el que el centro de seguridad recopila los datos y hace recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="acf87-134">Security policies are used toodefine hello items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="acf87-135">Puede aplicar toodifferent conjuntos de directivas de seguridad diferentes de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="acf87-135">You can apply different security policies toodifferent sets of Azure resources.</span></span> <span data-ttu-id="acf87-136">Aunque de forma predeterminada los recursos de Azure se evalúan con respecto a todos los elementos de la directiva, es posible desactivar elementos individuales de la directiva tanto para todos los recursos de Azure como para un solo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="acf87-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="acf87-137">Para más información acerca de las directivas de seguridad de Security Center, consulte [Establecimiento de directivas de seguridad en Azure Security Center](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="acf87-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="acf87-138">tooset una directiva de seguridad para todos los recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="acf87-138">tooset up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="acf87-139">En el panel del centro de seguridad de hello, seleccione **directiva de seguridad**y, a continuación, seleccione la suscripción.</span><span class="sxs-lookup"><span data-stu-id="acf87-139">On hello Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="acf87-140">Seleccione **Prevention policy** (Directiva de prevención).</span><span class="sxs-lookup"><span data-stu-id="acf87-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="acf87-141">Activar o desactivar elementos de directiva que desea tooapply tooall recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="acf87-141">Turn on or turn off policy items that you want tooapply tooall Azure resources.</span></span>
4. <span data-ttu-id="acf87-142">Cuando haya terminado de seleccionar la configuración, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="acf87-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="acf87-143">En hello **directiva de seguridad** hoja, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="acf87-143">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="acf87-144">tooset una directiva para un grupo de recursos específico:</span><span class="sxs-lookup"><span data-stu-id="acf87-144">tooset up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="acf87-145">En el panel del centro de seguridad de hello, seleccione **directiva de seguridad**y, a continuación, seleccione un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="acf87-145">On hello Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="acf87-146">Seleccione **Prevention policy** (Directiva de prevención).</span><span class="sxs-lookup"><span data-stu-id="acf87-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="acf87-147">Activar o desactivar elementos de directiva que desea que el grupo de recursos de tooapply toohello.</span><span class="sxs-lookup"><span data-stu-id="acf87-147">Turn on or turn off policy items that you want tooapply toohello resource group.</span></span>
4. <span data-ttu-id="acf87-148">En **INHERITANCE** (HERENCIA), seleccione **Unique** (Único).</span><span class="sxs-lookup"><span data-stu-id="acf87-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="acf87-149">Cuando haya terminado de seleccionar la configuración, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="acf87-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="acf87-150">En hello **directiva de seguridad** hoja, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="acf87-150">On hello **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="acf87-151">En esta página también se puede desactivar la recopilación de datos de un grupo de recursos concreto.</span><span class="sxs-lookup"><span data-stu-id="acf87-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="acf87-152">En el siguiente ejemplo de Hola, se ha creado una directiva única para un grupo de recursos denominado *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="acf87-152">In hello following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="acf87-153">En esta directiva, se han desactivado las recomendaciones tanto para el cifrado de disco como para el Firewall de aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="acf87-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Directiva única](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="acf87-155">Visualización del estado de configuración de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="acf87-155">View VM configuration health</span></span>

<span data-ttu-id="acf87-156">Después de que ha activado la recopilación de datos y establecer una directiva de seguridad, el centro de seguridad empieza a las recomendaciones y tooprovide alertas.</span><span class="sxs-lookup"><span data-stu-id="acf87-156">After you've turned on data collection and set a security policy, Security Center begins tooprovide alerts and recommendations.</span></span> <span data-ttu-id="acf87-157">Tal y como se implementan máquinas virtuales, se instala el agente de recopilación de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="acf87-157">As VMs are deployed, hello data collection agent is installed.</span></span> <span data-ttu-id="acf87-158">Centro de seguridad, a continuación, se rellena con datos de hello nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="acf87-158">Security Center is then populated with data for hello new VMs.</span></span> <span data-ttu-id="acf87-159">Para obtener información detallada acerca del estado de configuración de las máquinas virtuales, consulte [Protección de las máquinas virtuales en Azure Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="acf87-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="acf87-160">Tal y como se recopilan los datos, se agrega el estado de los recursos Hola para cada máquina virtual y los recursos relacionados de Azure.</span><span class="sxs-lookup"><span data-stu-id="acf87-160">As data is collected, hello resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="acf87-161">se muestra información de Hello en un gráfico de fácil de leer.</span><span class="sxs-lookup"><span data-stu-id="acf87-161">hello information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="acf87-162">estado de los recursos tooview:</span><span class="sxs-lookup"><span data-stu-id="acf87-162">tooview resource health:</span></span>

1.  <span data-ttu-id="acf87-163">En el panel del centro de seguridad de hello, en **estado de seguridad del recurso**, seleccione **proceso**.</span><span class="sxs-lookup"><span data-stu-id="acf87-163">On hello Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="acf87-164">En hello **proceso** hoja, seleccione **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="acf87-164">On hello **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="acf87-165">Esta vista proporciona un resumen del estado de configuración de Hola para todas las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="acf87-165">This view provides a summary of hello configuration status for all your VMs.</span></span>

![Estado de Compute](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="acf87-167">toosee todas las recomendaciones para una máquina virtual, seleccione Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="acf87-167">toosee all recommendations for a VM, select hello VM.</span></span> <span data-ttu-id="acf87-168">Recomendaciones y la corrección se tratan con más detalle en la siguiente sección de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="acf87-168">Recommendations and remediation are covered in more detail in hello next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="acf87-169">Corrección de los problemas de configuración</span><span class="sxs-lookup"><span data-stu-id="acf87-169">Remediate configuration issues</span></span>

<span data-ttu-id="acf87-170">Después de que el centro de seguridad comience toopopulate con datos de configuración, las recomendaciones se realizan en función de directiva de seguridad de hello que configurar.</span><span class="sxs-lookup"><span data-stu-id="acf87-170">After Security Center begins toopopulate with configuration data, recommendations are made based on hello security policy you set up.</span></span> <span data-ttu-id="acf87-171">Por ejemplo, si se configuró una máquina virtual sin un grupo de seguridad de red asociados, una actuación toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="acf87-171">For instance, if a VM was set up without an associated network security group, a recommendation is made toocreate one.</span></span> 

<span data-ttu-id="acf87-172">toosee una lista de todas las recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="acf87-172">toosee a list of all recommendations:</span></span> 

1. <span data-ttu-id="acf87-173">En el panel del centro de seguridad de hello, seleccione **recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="acf87-173">On hello Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="acf87-174">Seleccione una recomendación concreta.</span><span class="sxs-lookup"><span data-stu-id="acf87-174">Select a specific recommendation.</span></span> <span data-ttu-id="acf87-175">Aparece una lista de todos los recursos para el que se aplica la recomendación de Hola.</span><span class="sxs-lookup"><span data-stu-id="acf87-175">A list of all resources for which hello recommendation applies appears.</span></span>
3. <span data-ttu-id="acf87-176">tooapply una recomendación, seleccione un recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="acf87-176">tooapply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="acf87-177">Siga las instrucciones de Hola de pasos de corrección.</span><span class="sxs-lookup"><span data-stu-id="acf87-177">Follow hello instructions for remediation steps.</span></span> 

<span data-ttu-id="acf87-178">En muchos casos, el centro de seguridad proporciona procesables pasos que puede seguir una recomendación tooaddress sin abandonar el centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="acf87-178">In many cases, Security Center provides actionable steps you can take tooaddress a recommendation without leaving Security Center.</span></span> <span data-ttu-id="acf87-179">En el siguiente ejemplo de Hola, centro de seguridad detecta un grupo de seguridad de red que tenga una regla de entrada sin restricciones.</span><span class="sxs-lookup"><span data-stu-id="acf87-179">In hello following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="acf87-180">En la página de la recomendación de hello, puede seleccionar hello **editar reglas de entrada** botón.</span><span class="sxs-lookup"><span data-stu-id="acf87-180">On hello recommendation page, you can select hello **Edit inbound rules** button.</span></span> <span data-ttu-id="acf87-181">aparece en la interfaz de usuario que es necesario toomodify Hola regla Hola.</span><span class="sxs-lookup"><span data-stu-id="acf87-181">hello UI that is needed toomodify hello rule appears.</span></span> 

![Recomendaciones](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="acf87-183">A medida que se corrigen las recomendaciones, se marcan como resueltas.</span><span class="sxs-lookup"><span data-stu-id="acf87-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="acf87-184">Visualización de amenazas detectadas</span><span class="sxs-lookup"><span data-stu-id="acf87-184">View detected threats</span></span>

<span data-ttu-id="acf87-185">Además, tooresource recomendaciones para la configuración, el centro de seguridad muestra las alertas de detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="acf87-185">In addition tooresource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="acf87-186">característica de alertas de seguridad de Hello agrega los datos recopilados de cada máquina virtual, registros de red de Azure y socios conectados soluciones toodetect amenazas de seguridad en recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="acf87-186">hello security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions toodetect security threats against Azure resources.</span></span> <span data-ttu-id="acf87-187">Para más información acerca de las funcionalidades de detección de amenazas de Security Center, consulte [Funcionalidades de detección de Azure Security Center](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="acf87-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="acf87-188">característica de alertas de seguridad de Hello requiere precios toobe capa aumentado desde el centro de seguridad de hello *libre* demasiado*estándar*.</span><span class="sxs-lookup"><span data-stu-id="acf87-188">hello security alerts feature requires hello Security Center pricing tier toobe increased from *Free* too*Standard*.</span></span> <span data-ttu-id="acf87-189">30 días **evaluación gratuita** está disponible cuando se mueve toothis mayor nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="acf87-189">A 30-day **free trial** is available when you move toothis higher pricing tier.</span></span> 

<span data-ttu-id="acf87-190">nivel de precios de Hola toochange:</span><span class="sxs-lookup"><span data-stu-id="acf87-190">toochange hello pricing tier:</span></span>  

1. <span data-ttu-id="acf87-191">En el panel del centro de seguridad de hello, haga clic en **directiva de seguridad**y, a continuación, seleccione la suscripción.</span><span class="sxs-lookup"><span data-stu-id="acf87-191">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="acf87-192">Seleccione **Plan de tarifa**.</span><span class="sxs-lookup"><span data-stu-id="acf87-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="acf87-193">Seleccione el nuevo nivel de hello y, a continuación, seleccione **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="acf87-193">Select hello new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="acf87-194">En hello **directiva de seguridad** hoja, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="acf87-194">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="acf87-195">Después de cambiar nivel de precios de hello, gráfico de alertas de seguridad de hello comienza toopopulate cuando se detectan amenazas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="acf87-195">After you've changed hello pricing tier, hello security alerts graph begins toopopulate as security threats are detected.</span></span>

![Alertas de seguridad](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="acf87-197">Seleccione un alerta tooview la información.</span><span class="sxs-lookup"><span data-stu-id="acf87-197">Select an alert tooview information.</span></span> <span data-ttu-id="acf87-198">Por ejemplo, puede ver una descripción de la amenaza de hello, hora de detección de hello, todos los intentos de amenaza y Hola corrección recomendada.</span><span class="sxs-lookup"><span data-stu-id="acf87-198">For example, you can see a description of hello threat, hello detection time, all threat attempts, and hello recommended remediation.</span></span> <span data-ttu-id="acf87-199">En el siguiente ejemplo de Hola, se detectó un ataque por fuerza bruta RDP con 294 intentos fallidos de RDP.</span><span class="sxs-lookup"><span data-stu-id="acf87-199">In hello following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="acf87-200">Se proporciona una corrección recomendada.</span><span class="sxs-lookup"><span data-stu-id="acf87-200">A recommended resolution is provided.</span></span>

![Ataque de RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="acf87-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="acf87-202">Next steps</span></span>
<span data-ttu-id="acf87-203">En este tutorial, configurará Azure Security Center y, luego, revisó las máquinas virtuales de Security Center.</span><span class="sxs-lookup"><span data-stu-id="acf87-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="acf87-204">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="acf87-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="acf87-205">Configuración de una recolección de datos</span><span class="sxs-lookup"><span data-stu-id="acf87-205">Set up data collection</span></span>
> * <span data-ttu-id="acf87-206">Configurar directivas de seguridad</span><span class="sxs-lookup"><span data-stu-id="acf87-206">Set up security policies</span></span>
> * <span data-ttu-id="acf87-207">Ver y corregir problemas de estado de la configuración</span><span class="sxs-lookup"><span data-stu-id="acf87-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="acf87-208">Revisar las amenazas que se detecten</span><span class="sxs-lookup"><span data-stu-id="acf87-208">Review detected threats</span></span>

<span data-ttu-id="acf87-209">Avance toohello siguiente tutorial toolearn más acerca de cómo crear un CD de elemento de configuración de canalización con Jenkins, GitHub y Docker.</span><span class="sxs-lookup"><span data-stu-id="acf87-209">Advance toohello next tutorial toolearn more about creating a CI/CD pipeline with Jenkins, GitHub, and Docker.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="acf87-210">Creación de una infraestructura de CI/CD con Jenkins, GitHub y Docker</span><span class="sxs-lookup"><span data-stu-id="acf87-210">Create CI/CD infrastructure with Jenkins, GitHub, and Docker</span></span>](tutorial-jenkins-github-docker-cicd.md)

