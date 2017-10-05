---
title: "Introducción a Azure Security Center | Microsoft Docs"
description: "Obtenga información sobre el Centro de seguridad de Azure, sus capacidades clave y cómo funciona."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 8951167213da6ab5341c1ca420353ec625ef5424
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-security-center"></a><span data-ttu-id="3c1bb-103">Introducción al Centro de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="3c1bb-103">Introduction to Azure Security Center</span></span>
<span data-ttu-id="3c1bb-104">Obtenga información sobre el Centro de seguridad de Azure, sus capacidades clave y cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-104">Learn about Azure Security Center, its key capabilities, and how it works.</span></span>

> [!NOTE]
> <span data-ttu-id="3c1bb-105">Desde primeros de junio de 2017, Security Center usará Microsoft Monitoring Agent para recopilar y almacenar datos.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-105">Beginning in early June 2017, Security Center will use the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="3c1bb-106">Consulte [Migración de la plataforma de Azure Security Center](security-center-platform-migration.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) to learn more.</span></span> <span data-ttu-id="3c1bb-107">La información de este artículo representa la funcionalidad de Security Center después de la transición a Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-107">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>
>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="3c1bb-108">¿Qué es el Centro de seguridad de Azure?</span><span class="sxs-lookup"><span data-stu-id="3c1bb-108">What is Azure Security Center?</span></span>
 <span data-ttu-id="3c1bb-109">El Centro de seguridad ayuda a evitar, detectar y responder a amenazas con más visibilidad y control de la seguridad en los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-109">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="3c1bb-110">Proporciona administración de directivas y supervisión de la seguridad integrada en las suscripciones de Azure, ayuda a detectar las amenazas que podrían pasar desapercibidas y funciona con un amplio ecosistema de soluciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-110">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="3c1bb-111">Principales capacidades</span><span class="sxs-lookup"><span data-stu-id="3c1bb-111">Key capabilities</span></span>
 <span data-ttu-id="3c1bb-112">El Centro de seguridad ofrece las funcionalidades sencillas y eficaces de prevención, detección y respuesta ante amenazas integradas en Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-112">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in to Azure.</span></span> <span data-ttu-id="3c1bb-113">Principales capacidades:</span><span class="sxs-lookup"><span data-stu-id="3c1bb-113">Key capabilities are:</span></span>

| <span data-ttu-id="3c1bb-114">Fase</span><span class="sxs-lookup"><span data-stu-id="3c1bb-114">Stage</span></span> | <span data-ttu-id="3c1bb-115">Capacidad</span><span class="sxs-lookup"><span data-stu-id="3c1bb-115">Capability</span></span> |
| --- | --- |
| <span data-ttu-id="3c1bb-116">Prevención</span><span class="sxs-lookup"><span data-stu-id="3c1bb-116">Prevent</span></span> |<span data-ttu-id="3c1bb-117">Supervisa el estado de seguridad de los recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="3c1bb-117">Monitors the security state of your Azure resources</span></span> |
| <span data-ttu-id="3c1bb-118">Prevención</span><span class="sxs-lookup"><span data-stu-id="3c1bb-118">Prevent</span></span> | <span data-ttu-id="3c1bb-119">Define las directivas de las suscripciones de Azure en función de los requisitos de seguridad de la compañía, los tipos de aplicaciones utilizados y la confidencialidad de los datos.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-119">Defines policies for your Azure subscriptions based on your company’s security requirements, the types of applications that you use, and the sensitivity of your data</span></span> |
| <span data-ttu-id="3c1bb-120">Prevención</span><span class="sxs-lookup"><span data-stu-id="3c1bb-120">Prevent</span></span> | <span data-ttu-id="3c1bb-121">Usa recomendaciones de seguridad controladas por directivas para guiar a los propietarios de los servicios a través del proceso de implementación de los controles necesarios</span><span class="sxs-lookup"><span data-stu-id="3c1bb-121">Uses policy-driven security recommendations to guide service owners through the process of implementing needed controls</span></span> |
| <span data-ttu-id="3c1bb-122">Prevención</span><span class="sxs-lookup"><span data-stu-id="3c1bb-122">Prevent</span></span> | <span data-ttu-id="3c1bb-123">Implementa rápidamente servicios y dispositivos de seguridad de Microsoft y asociados</span><span class="sxs-lookup"><span data-stu-id="3c1bb-123">Rapidly deploys security services and appliances from Microsoft and partners</span></span> |
| <span data-ttu-id="3c1bb-124">Detección</span><span class="sxs-lookup"><span data-stu-id="3c1bb-124">Detect</span></span> |<span data-ttu-id="3c1bb-125">Recopila y analiza automáticamente los datos de seguridad de los recursos de Azure, la red y las soluciones de asociados como firewalls y programas antimalware</span><span class="sxs-lookup"><span data-stu-id="3c1bb-125">Automatically collects and analyzes security data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls</span></span> |
| <span data-ttu-id="3c1bb-126">Detección</span><span class="sxs-lookup"><span data-stu-id="3c1bb-126">Detect</span></span> | <span data-ttu-id="3c1bb-127">Utiliza la inteligencia de amenazas globales de los productos y servicios de Microsoft, Microsoft Digital Crimes Unit (DCU), Microsoft Security Response Center (MSRC) y fuentes externas.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-127">Uses global threat intelligence from Microsoft products and services, the Microsoft Digital Crimes Unit (DCU), the Microsoft Security Response Center (MSRC), and external feeds</span></span> |
| <span data-ttu-id="3c1bb-128">Detección</span><span class="sxs-lookup"><span data-stu-id="3c1bb-128">Detect</span></span> | <span data-ttu-id="3c1bb-129">Aplica análisis avanzados, incluido el aprendizaje automático y el análisis de comportamientos</span><span class="sxs-lookup"><span data-stu-id="3c1bb-129">Applies advanced analytics, including machine learning and behavioral analysis</span></span> |
| <span data-ttu-id="3c1bb-130">Respuesta</span><span class="sxs-lookup"><span data-stu-id="3c1bb-130">Respond</span></span> |<span data-ttu-id="3c1bb-131">Proporciona seguridad prioritaria ante incidentes y alertas</span><span class="sxs-lookup"><span data-stu-id="3c1bb-131">Provides prioritized security incidents/alerts</span></span> |
| <span data-ttu-id="3c1bb-132">Respuesta</span><span class="sxs-lookup"><span data-stu-id="3c1bb-132">Respond</span></span> | <span data-ttu-id="3c1bb-133">Proporciona información sobre el origen del ataque y los recursos afectados</span><span class="sxs-lookup"><span data-stu-id="3c1bb-133">Offers insights into the source of the attack and impacted resources</span></span> |
| <span data-ttu-id="3c1bb-134">Respuesta</span><span class="sxs-lookup"><span data-stu-id="3c1bb-134">Respond</span></span> | <span data-ttu-id="3c1bb-135">Sugiere formas de detener el ataque actual y de ayudar a impedir ataques futuros</span><span class="sxs-lookup"><span data-stu-id="3c1bb-135">Suggests ways to stop the current attack and help prevent future attacks</span></span> |

## <a name="introductory-walkthrough"></a><span data-ttu-id="3c1bb-136">Tutorial de introducción</span><span class="sxs-lookup"><span data-stu-id="3c1bb-136">Introductory walkthrough</span></span>

> [!NOTE]
> <span data-ttu-id="3c1bb-137">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-137">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="3c1bb-138">Este documento no es una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-138">This document is not a step-by-step guide.</span></span>
>
>

 <span data-ttu-id="3c1bb-139">Se accede al Centro de seguridad desde el [Portal de Azure](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="3c1bb-139">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="3c1bb-140">[Inicie sesión en el portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3c1bb-140">[Sign in to the portal](https://portal.azure.com).</span></span> <span data-ttu-id="3c1bb-141">En el menú principal del portal, desplácese hasta la opción **Security Center** o seleccione el icono **Security Center** que ancló anteriormente al panel del portal.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-141">Under the main portal menu, scroll to the **Security Center** option or select the **Security Center** tile that you previously pinned to the portal dashboard.</span></span>

![Icono Seguridad en el Portal de Azure][1]

<span data-ttu-id="3c1bb-143">En el Centro de seguridad, puede establecer directivas de seguridad, supervisar configuraciones de seguridad y ver alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-143">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span></span>

### <a name="security-policies"></a><span data-ttu-id="3c1bb-144">Directivas de seguridad</span><span class="sxs-lookup"><span data-stu-id="3c1bb-144">Security policies</span></span>
<span data-ttu-id="3c1bb-145">Puede definir directivas para las suscripciones de Azure según los requisitos de seguridad de la compañía.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-145">You can define policies for your Azure subscriptions according to your company's security requirements.</span></span> <span data-ttu-id="3c1bb-146">También puede personalizarlas según los tipos de aplicaciones que use o la confidencialidad de los datos en cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-146">You can also tailor them to the types of applications you're using or to the sensitivity of the data in each subscription.</span></span> <span data-ttu-id="3c1bb-147">Por ejemplo, es posible que los recursos usados para el desarrollo o las pruebas tengan requisitos de seguridad distintos a los empleados para las aplicaciones de producción.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-147">For example, resources used for development or testing may have different security requirements than those used for production applications.</span></span> <span data-ttu-id="3c1bb-148">Del mismo modo, es posible que las aplicaciones con datos regulados como PII requieran un mayor nivel de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-148">Likewise, applications with regulated data like PII may require a higher level of security.</span></span>

> [!NOTE]
> <span data-ttu-id="3c1bb-149">Para modificar una directiva de seguridad, debe ser administrador de seguridad o el propietario/colaborador de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-149">To modify a security policy, you must be a Security Administrator or the subscription's Owner or Contributor.</span></span> <span data-ttu-id="3c1bb-150">Consulte [Permisos en Azure Security Center](security-center-permissions.md) para obtener más información sobre los roles y las acciones permitidas en Security Center.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-150">To learn more about roles and allowed actions in Security Center, see [Permissions in Azure Security Center](security-center-permissions.md).</span></span>
>
>

<span data-ttu-id="3c1bb-151">En la hoja **Security Center**, seleccione el icono **Directiva** para obtener una lista de las suscripciones y los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-151">On the **Security Center** blade, select the **Policy** tile for a list of your subscriptions and resource groups.</span></span>   

![Hoja de centro de seguridad][2]

<span data-ttu-id="3c1bb-153">En la hoja **Directiva de seguridad**, seleccione una suscripción para ver los detalles de la directiva.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-153">On the **Security policy** blade, select a subscription to view the policy details.</span></span>

<span data-ttu-id="3c1bb-154">**Recopilación de datos** habilita la recopilación de datos en una directiva de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-154">**Data collection** enables data collection for a security policy.</span></span> <span data-ttu-id="3c1bb-155">Con la habilitación se consigue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3c1bb-155">Enabling provides:</span></span>

* <span data-ttu-id="3c1bb-156">Examen diario de todas las máquinas virtuales (VM) admitidas para las recomendaciones y la supervisión de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-156">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span></span>
* <span data-ttu-id="3c1bb-157">Colección de eventos de seguridad para el análisis y la detección de amenazas.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-157">Collection of security events for analysis and threat detection.</span></span>

> [!NOTE]
> <span data-ttu-id="3c1bb-158">Recopilación de datos se configura en el nivel de suscripción.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-158">Data collection is configured at the subscription level.</span></span>
>
>

<span data-ttu-id="3c1bb-159">Seleccione **Directiva de prevención** para abrir la hoja **Directiva de prevención**.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-159">Select **Prevention policy** to open the **Prevention policy** blade.</span></span> <span data-ttu-id="3c1bb-160">**Mostrar recomendaciones para** permite elegir los controles de seguridad que desea supervisar y las recomendaciones que desea ver según las necesidades de seguridad de los recursos de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-160">**Show recommendations for** lets you choose the security controls that you want to monitor and the recommendations that you want to see based on the security needs of the resources within the subscription.</span></span>

### <a name="security-recommendations"></a><span data-ttu-id="3c1bb-161">Recomendaciones de seguridad</span><span class="sxs-lookup"><span data-stu-id="3c1bb-161">Security recommendations</span></span>
 <span data-ttu-id="3c1bb-162">El Centro de seguridad analiza el estado de seguridad de los recursos de Azure para identificar posibles vulnerabilidades de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-162">Security Center analyzes the security state of your Azure resources to identify potential security vulnerabilities.</span></span> <span data-ttu-id="3c1bb-163">Una lista de recomendaciones le guiará por el proceso de configuración de los controles necesarios.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-163">A list of recommendations guides you through the process of configuring needed controls.</span></span> <span data-ttu-id="3c1bb-164">Algunos ejemplos son:</span><span class="sxs-lookup"><span data-stu-id="3c1bb-164">Examples include:</span></span>

* <span data-ttu-id="3c1bb-165">Aprovisionamiento de antimalware para ayudar a identificar y eliminar el software malintencionado.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-165">Provisioning antimalware to help identify and remove malicious software</span></span>
* <span data-ttu-id="3c1bb-166">Configuración de reglas y grupos de seguridad de red para controlar el tráfico a las VM</span><span class="sxs-lookup"><span data-stu-id="3c1bb-166">Configuring network security groups and rules to control traffic to VMs</span></span>
* <span data-ttu-id="3c1bb-167">Aprovisionamiento de firewalls de aplicaciones web para ayudar a defenderse contra ataques dirigidos a las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-167">Provisioning of web application firewalls to help defend against attacks that target your web applications</span></span>
* <span data-ttu-id="3c1bb-168">Implementación de actualizaciones del sistema que faltan.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-168">Deploying missing system updates</span></span>
* <span data-ttu-id="3c1bb-169">Resolución de las configuraciones de sistema operativo que no coinciden con las líneas base recomendadas.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-169">Addressing OS configurations that do not match the recommended baselines</span></span>

<span data-ttu-id="3c1bb-170">Haga clic en el icono **Recomendaciones** para obtener una lista de recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-170">Click the **Recommendations** tile for a list of recommendations.</span></span> <span data-ttu-id="3c1bb-171">Haga clic en cada recomendación para ver más información o para tomar medidas para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-171">Click each recommendation to view additional information or to take action to resolve the issue.</span></span>

![Recomendaciones de seguridad en el Centro de seguridad de Azure][5]

### <a name="security-state-of-azure-resources"></a><span data-ttu-id="3c1bb-173">Estado de seguridad de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="3c1bb-173">Security state of Azure resources</span></span>
<span data-ttu-id="3c1bb-174">En la sección **Prevención** del panel se muestra la posición de seguridad general del entorno por tipo de recurso, lo que incluye máquinas virtuales, aplicaciones web y otros recursos.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-174">The **Prevention** section of the dashboard shows the overall security posture of the environment by resource type, including VMs, web applications, and other resources.</span></span>   

<span data-ttu-id="3c1bb-175">Seleccione un tipo de recurso en **Prevención** para ver más información, incluida una lista de las posibles vulnerabilidades de seguridad que se hayan identificado.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-175">Select a resource type under **Prevention** to view more information, including a list of any potential security vulnerabilities that have been identified.</span></span> <span data-ttu-id="3c1bb-176">(En el siguiente ejemplo, se selecciona la opción **Compute**).</span><span class="sxs-lookup"><span data-stu-id="3c1bb-176">(**Compute** is selected in the example below.)</span></span>

![Icono Estado de los recursos][6]

### <a name="security-alerts"></a><span data-ttu-id="3c1bb-178">Alertas de seguridad</span><span class="sxs-lookup"><span data-stu-id="3c1bb-178">Security alerts</span></span>
 <span data-ttu-id="3c1bb-179">El Centro de seguridad recopila, analiza e integra automáticamente los datos de registro de los recursos de Azure, la red y soluciones de asociados como firewalls y programas antimalware.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-179">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls.</span></span> <span data-ttu-id="3c1bb-180">Cuando se detecten amenazas, se creará una alerta de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-180">When threats are detected, a security alert is created.</span></span> <span data-ttu-id="3c1bb-181">Como ejemplos se incluye la detección de:</span><span class="sxs-lookup"><span data-stu-id="3c1bb-181">Examples include detection of:</span></span>

* <span data-ttu-id="3c1bb-182">VM en peligro que se comunican con direcciones IP malintencionadas conocidas</span><span class="sxs-lookup"><span data-stu-id="3c1bb-182">Compromised VMs communicating with known malicious IP addresses</span></span>
* <span data-ttu-id="3c1bb-183">Malware avanzado detectado mediante la generación de informes de errores de Windows.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-183">Advanced malware detected by using Windows error reporting</span></span>
* <span data-ttu-id="3c1bb-184">Ataques de fuerza bruta contra VM</span><span class="sxs-lookup"><span data-stu-id="3c1bb-184">Brute force attacks against VMs</span></span>
* <span data-ttu-id="3c1bb-185">Alertas de seguridad de programas antimalware y firewalls integrados</span><span class="sxs-lookup"><span data-stu-id="3c1bb-185">Security alerts from integrated antimalware programs and firewalls</span></span>

<span data-ttu-id="3c1bb-186">Al hacer clic en el icono **Alertas de seguridad** se muestra una lista de alertas por prioridad.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-186">Clicking the **Security alerts** tile displays a list of prioritized alerts.</span></span>

![Alertas de seguridad][7]

<span data-ttu-id="3c1bb-188">Al seleccionar una alerta, se muestra más información sobre el ataque y sugerencias para resolverlo.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-188">Selecting an alert shows more information about the attack and suggestions for how to remediate it.</span></span>

![Detalles de alertas de seguridad][8]

### <a name="partner-solutions"></a><span data-ttu-id="3c1bb-190">Soluciones de socios</span><span class="sxs-lookup"><span data-stu-id="3c1bb-190">Partner solutions</span></span>
<span data-ttu-id="3c1bb-191">El icono de **Soluciones de asociados** permite supervisar de un solo vistazo el estado de seguridad de las soluciones de asociados integradas en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-191">The **Partner solutions** tile lets you monitor at a glance the security state of your partner solutions integrated with your Azure subscription.</span></span> <span data-ttu-id="3c1bb-192">Security Center muestra las alertas procedentes de las soluciones.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-192">Security Center displays alerts coming from the solutions.</span></span>

<span data-ttu-id="3c1bb-193">Seleccione el icono **Soluciones de asociados** .</span><span class="sxs-lookup"><span data-stu-id="3c1bb-193">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="3c1bb-194">Se muestra una hoja con una lista de todas las soluciones de asociados conectadas.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-194">A blade opens displaying a list of all connected partner solutions.</span></span>

![Soluciones de socios][9]

## <a name="get-started"></a><span data-ttu-id="3c1bb-196">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="3c1bb-196">Get started</span></span>
<span data-ttu-id="3c1bb-197">Para empezar a trabajar con el Centro de seguridad, necesita una suscripción a Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-197">To get started with Security Center, you need a subscription to Microsoft Azure.</span></span> <span data-ttu-id="3c1bb-198">El Centro de seguridad se habilita con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-198">Security Center is enabled with your Azure subscription.</span></span> <span data-ttu-id="3c1bb-199">Si no tiene una suscripción, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c1bb-199">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

 <span data-ttu-id="3c1bb-200">Se accede al Centro de seguridad desde el [Portal de Azure](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="3c1bb-200">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="3c1bb-201">Para obtener más información, consulte la [documentación del portal](https://azure.microsoft.com/documentation/services/azure-portal/) .</span><span class="sxs-lookup"><span data-stu-id="3c1bb-201">See the [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) to learn more.</span></span>

<span data-ttu-id="3c1bb-202">[Introducción a Azure Security Center](security-center-get-started.md) le guía rápidamente por los componentes de administración de directivas y supervisión de seguridad de Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-202">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through the security-monitoring and policy-management components of Security Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c1bb-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c1bb-203">Next steps</span></span>
<span data-ttu-id="3c1bb-204">En este documento, se ha presentado el Centro de seguridad, sus funcionalidades clave y cómo empezar a usarlo.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-204">In this document, you were introduced to Security Center, its key capabilities, and how to get started.</span></span> <span data-ttu-id="3c1bb-205">Para obtener más información, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="3c1bb-205">To learn more, see the following resources:</span></span>

* <span data-ttu-id="3c1bb-206">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md) : aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-206">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="3c1bb-207">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que lo ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-207">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="3c1bb-208">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md) : obtenga información sobre cómo supervisar el estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-208">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="3c1bb-209">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md) : obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-209">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="3c1bb-210">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md) : aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-210">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="3c1bb-211">[Seguridad de datos de Azure Security Center](security-center-data-security.md): aprenda cómo se administran y protegen los datos en Security Center.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-211">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="3c1bb-212">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md) : encuentre las preguntas más frecuentes sobre el uso del servicio.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-212">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="3c1bb-213">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenga las últimas noticias e información sobre la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="3c1bb-213">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
