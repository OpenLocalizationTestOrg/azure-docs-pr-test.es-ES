---
title: "integración de aaaSCOM con Application Insights | Documentos de Microsoft"
description: "Si es usuario de SCOM, supervise el rendimiento y diagnostique problemas con Application Insights. Paneles integrales, alertas inteligentes, eficaces herramientas de diagnóstico y consultas de análisis."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="e74c9-104">Supervisión del rendimiento de la aplicación con Application Insights para SCOM</span><span class="sxs-lookup"><span data-stu-id="e74c9-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="e74c9-105">Si usa System Center Operations Manager (SCOM) toomanage los servidores, puede supervisar el rendimiento y diagnosticar problemas de rendimiento con la Ayuda de Hola de [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="e74c9-105">If you use System Center Operations Manager (SCOM) toomanage your servers, you can monitor performance and diagnose performance issues with hello help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="e74c9-106">Application Insights supervisa solicitudes entrantes de la aplicación web, llamadas SQL y REST salientes, excepciones y seguimientos de registros.</span><span class="sxs-lookup"><span data-stu-id="e74c9-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="e74c9-107">Proporciona paneles con gráficos de métricas y alertas inteligentes, así como una eficaz búsqueda de diagnóstico y consultas analíticas sobre esta telemetría.</span><span class="sxs-lookup"><span data-stu-id="e74c9-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="e74c9-108">Puede activar la supervisión de Application Insights mediante un módulo de administración de SCOM.</span><span class="sxs-lookup"><span data-stu-id="e74c9-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e74c9-109">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="e74c9-109">Before you start</span></span>
<span data-ttu-id="e74c9-110">Condiciones:</span><span class="sxs-lookup"><span data-stu-id="e74c9-110">We assume:</span></span>

* <span data-ttu-id="e74c9-111">Está familiarizado con SCOM y uso de SCOM 2012 R2 o toomanage 2016 IIS servidores web.</span><span class="sxs-lookup"><span data-stu-id="e74c9-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 toomanage your IIS web servers.</span></span>
* <span data-ttu-id="e74c9-112">Ya ha instalado en los servidores de una aplicación web que desea que toomonitor con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e74c9-112">You have already installed on your servers a web application that you want toomonitor with Application Insights.</span></span>
* <span data-ttu-id="e74c9-113">La versión de framework de la aplicación es .NET 4.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e74c9-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="e74c9-114">Tener acceso tooa suscripción en [Microsoft Azure](https://azure.com) y puede iniciar sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e74c9-114">You have access tooa subscription in [Microsoft Azure](https://azure.com) and can sign in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e74c9-115">Su organización puede tener una suscripción y puede agregar su tooit de cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e74c9-115">Your organization may have a subscription, and can add your Microsoft account tooit.</span></span>

<span data-ttu-id="e74c9-116">(equipo de desarrollo de hello podría aumentar hello [Application Insights SDK](app-insights-asp-net.md) en la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="e74c9-116">(hello development team might build hello [Application Insights SDK](app-insights-asp-net.md) into hello web app.</span></span> <span data-ttu-id="e74c9-117">Esta instrumentación en tiempo de compilación les proporciona mayor flexibilidad al escribir una telemetría personalizada.</span><span class="sxs-lookup"><span data-stu-id="e74c9-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="e74c9-118">Sin embargo, no importa: puede seguir los pasos de hello descritos aquí con o sin Hola SDK integrado.)</span><span class="sxs-lookup"><span data-stu-id="e74c9-118">However, it doesn't matter: you can follow hello steps described here either with or without hello SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="e74c9-119">(Una vez) Instalación del módulo de administración de Application Insights</span><span class="sxs-lookup"><span data-stu-id="e74c9-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="e74c9-120">En el equipo de Hola donde se ejecuta Operations Manager:</span><span class="sxs-lookup"><span data-stu-id="e74c9-120">On hello machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="e74c9-121">Desinstale cualquier versión anterior del módulo de administración de hello:</span><span class="sxs-lookup"><span data-stu-id="e74c9-121">Uninstall any old version of hello management pack:</span></span>
   1. <span data-ttu-id="e74c9-122">En Operations Manager, abra Administración, Módulos de administración.</span><span class="sxs-lookup"><span data-stu-id="e74c9-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="e74c9-123">Eliminar la versión anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74c9-123">Delete hello old version.</span></span>
2. <span data-ttu-id="e74c9-124">Descargue e instale el módulo de administración de Hola desde el catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74c9-124">Download and install hello management pack from hello catalog.</span></span>
3. <span data-ttu-id="e74c9-125">Reinicie Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="e74c9-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="e74c9-126">Creación de un módulo de administración</span><span class="sxs-lookup"><span data-stu-id="e74c9-126">Create a management pack</span></span>
1. <span data-ttu-id="e74c9-127">En Operations Manager, abra **Creación**, **.NET... con Application Insights**, **Asistente para agregar monitores** y vuelva a elegir **.NET... con Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="e74c9-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="e74c9-128">Configuración de hello nombre después de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e74c9-128">Name hello configuration after your app.</span></span> <span data-ttu-id="e74c9-129">(Tiene tooinstrument una aplicación en un momento.)</span><span class="sxs-lookup"><span data-stu-id="e74c9-129">(You have tooinstrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="e74c9-130">En Hola misma página del asistente, cree una nueva administración de módulo, o seleccione un paquete que creó anteriormente para Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e74c9-130">On hello same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="e74c9-131">(Hola Application Insights [módulo de administración](https://technet.microsoft.com/library/cc974491.aspx) es una plantilla, desde el que se crea una instancia.</span><span class="sxs-lookup"><span data-stu-id="e74c9-131">(hello Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="e74c9-132">Puede reutilizar Hola misma instancia posteriormente.)</span><span class="sxs-lookup"><span data-stu-id="e74c9-132">You can reuse hello same instance later.)</span></span>

    ![En la ficha Propiedades generales de hello, escriba el nombre de Hola de aplicación hello.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="e74c9-136">Elija una aplicación que desea toomonitor.</span><span class="sxs-lookup"><span data-stu-id="e74c9-136">Choose one app that you want toomonitor.</span></span> <span data-ttu-id="e74c9-137">característica de búsqueda de Hello busca entre aplicaciones instaladas en los servidores.</span><span class="sxs-lookup"><span data-stu-id="e74c9-137">hello search feature searches among apps installed on your servers.</span></span>
   
    ![En la ficha tooMonitor, haga clic en Agregar, escriba parte del nombre de la aplicación hello, haga clic en Buscar, elija aplicación hello y, a continuación, agregar, en Aceptar.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="e74c9-139">campo de ámbito de supervisión opcional Hola puede ser usado toospecify un subconjunto de los servidores, si no desea toomonitor Hola aplicación en todos los servidores.</span><span class="sxs-lookup"><span data-stu-id="e74c9-139">hello optional Monitoring scope field can be used toospecify a subset of your servers, if you don't want toomonitor hello app in all servers.</span></span>
2. <span data-ttu-id="e74c9-140">En la siguiente página del asistente hello, primero debe proporcionar su toosign de credenciales en tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e74c9-140">On hello next wizard page, you must first provide your credentials toosign in tooMicrosoft Azure.</span></span>
   
    <span data-ttu-id="e74c9-141">En esta página, elija recursos de Application Insights Hola donde desea toobe de datos de telemetría de hello analiza y muestra.</span><span class="sxs-lookup"><span data-stu-id="e74c9-141">On this page, you choose hello Application Insights resource where you want hello telemetry data toobe analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="e74c9-142">Si la aplicación hello se configuró para Application Insights durante el desarrollo, seleccione el recurso existente.</span><span class="sxs-lookup"><span data-stu-id="e74c9-142">If hello application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="e74c9-143">En caso contrario, cree un nuevo recurso con el nombre de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e74c9-143">Otherwise, create a new resource named for hello app.</span></span> <span data-ttu-id="e74c9-144">Si no hay otras aplicaciones que son componentes de hello mismo sistema, colóquelos en hello mismo grupo de recursos, toomake acceso toohello telemetría más fácil toomanage.</span><span class="sxs-lookup"><span data-stu-id="e74c9-144">If there are other apps that are components of hello same system, put them in hello same resource group, toomake access toohello telemetry easier toomanage.</span></span>
     
     <span data-ttu-id="e74c9-145">Puede cambiar estas opciones aquí.</span><span class="sxs-lookup"><span data-stu-id="e74c9-145">You can change these settings later.</span></span>
     
     ![En la pestaña de configuración de Application Insights, haga clic en 'Iniciar sesión' y proporcione las credenciales de la cuenta de Microsoft para Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="e74c9-148">Asistente de hello completa.</span><span class="sxs-lookup"><span data-stu-id="e74c9-148">Complete hello wizard.</span></span>
   
    ![Click Create](./media/app-insights-scom/070.png)

<span data-ttu-id="e74c9-150">Repita este procedimiento para cada aplicación que desea que se toomonitor.</span><span class="sxs-lookup"><span data-stu-id="e74c9-150">Repeat this procedure for each app that you want toomonitor.</span></span>

<span data-ttu-id="e74c9-151">Si necesita una configuración toochange más adelante, vuelva a abrir propiedades de Hola de hello supervisar desde la ventana de creación de hello.</span><span class="sxs-lookup"><span data-stu-id="e74c9-151">If you need toochange settings later, re-open hello properties of hello monitor from hello Authoring window.</span></span>

![En Creación, seleccione .NET Application Performance Monitoring (Supervisión del rendimiento de la aplicación de .NET) con Application Insights, seleccione al monitor y haga clic en Propiedades.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="e74c9-153">Comprobación de la supervisión</span><span class="sxs-lookup"><span data-stu-id="e74c9-153">Verify monitoring</span></span>
<span data-ttu-id="e74c9-154">monitor de Hola que ha instalado busca la aplicación en todos los servidores.</span><span class="sxs-lookup"><span data-stu-id="e74c9-154">hello monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="e74c9-155">Donde encuentra la aplicación hello, que configura la aplicación hello de Monitor de estado de aplicación visión toomonitor.</span><span class="sxs-lookup"><span data-stu-id="e74c9-155">Where it finds hello app, it configures Application Insights Status Monitor toomonitor hello app.</span></span> <span data-ttu-id="e74c9-156">Si es necesario, instala primero el Monitor de estado en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74c9-156">If necessary, it first installs Status Monitor on hello server.</span></span>

<span data-ttu-id="e74c9-157">También puede comprobar qué instancias de aplicación hello que ha encontrado:</span><span class="sxs-lookup"><span data-stu-id="e74c9-157">You can verify which instances of hello app it has found:</span></span>

![En Supervisión, abra Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="e74c9-159">Visualización de la telemetría en Application Insights</span><span class="sxs-lookup"><span data-stu-id="e74c9-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="e74c9-160">Hola [portal de Azure](https://portal.azure.com), examinar toohello recursos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e74c9-160">In hello [Azure portal](https://portal.azure.com), browse toohello resource for your app.</span></span> <span data-ttu-id="e74c9-161">[Verá gráficos que muestran la telemetría](app-insights-dashboards.md) de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="e74c9-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="e74c9-162">(Si lo no ha aparecido en la página principal de hello todavía, haga clic en secuencia en directo de métricas).</span><span class="sxs-lookup"><span data-stu-id="e74c9-162">(If it hasn't shown up on hello main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e74c9-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e74c9-163">Next steps</span></span>
* <span data-ttu-id="e74c9-164">[Configurar un panel](app-insights-dashboards.md) gráficos más importantes de toobring Hola juntos esta y otras aplicaciones de supervisión.</span><span class="sxs-lookup"><span data-stu-id="e74c9-164">[Set up a dashboard](app-insights-dashboards.md) toobring together hello most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="e74c9-165">Más información sobre las métricas</span><span class="sxs-lookup"><span data-stu-id="e74c9-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="e74c9-166">Configuración de alertas</span><span class="sxs-lookup"><span data-stu-id="e74c9-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="e74c9-167">Diagnóstico de problemas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="e74c9-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="e74c9-168">Consultas de Analytics eficaces</span><span class="sxs-lookup"><span data-stu-id="e74c9-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="e74c9-169">Pruebas web de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="e74c9-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

