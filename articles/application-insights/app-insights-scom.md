---
title: "Integración de SCOM con Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 9c205465981fabdbb696cdc44f765532bbb992b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="c49f8-104">Supervisión del rendimiento de la aplicación con Application Insights para SCOM</span><span class="sxs-lookup"><span data-stu-id="c49f8-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="c49f8-105">Si usa System Center Operations Manager (SCOM) para administrar los servidores, puede supervisar el rendimiento y diagnosticar problemas de rendimiento con la ayuda de [Azure Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="c49f8-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="c49f8-106">Application Insights supervisa solicitudes entrantes de la aplicación web, llamadas SQL y REST salientes, excepciones y seguimientos de registros.</span><span class="sxs-lookup"><span data-stu-id="c49f8-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="c49f8-107">Proporciona paneles con gráficos de métricas y alertas inteligentes, así como una eficaz búsqueda de diagnóstico y consultas analíticas sobre esta telemetría.</span><span class="sxs-lookup"><span data-stu-id="c49f8-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="c49f8-108">Puede activar la supervisión de Application Insights mediante un módulo de administración de SCOM.</span><span class="sxs-lookup"><span data-stu-id="c49f8-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c49f8-109">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="c49f8-109">Before you start</span></span>
<span data-ttu-id="c49f8-110">Condiciones:</span><span class="sxs-lookup"><span data-stu-id="c49f8-110">We assume:</span></span>

* <span data-ttu-id="c49f8-111">Está familiarizado con SCOM y usa SCOM 2012 R2 o 2016 para administrar los servidores web de IIS.</span><span class="sxs-lookup"><span data-stu-id="c49f8-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span></span>
* <span data-ttu-id="c49f8-112">Ya ha instalado los servidores de una aplicación web que desea supervisar con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c49f8-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span></span>
* <span data-ttu-id="c49f8-113">La versión de framework de la aplicación es .NET 4.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c49f8-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="c49f8-114">Tiene acceso a una suscripción en [Microsoft Azure](https://azure.com) y puede iniciar sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c49f8-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c49f8-115">Su organización puede tener una suscripción y puede agregar su cuenta de Microsoft a ella.</span><span class="sxs-lookup"><span data-stu-id="c49f8-115">Your organization may have a subscription, and can add your Microsoft account to it.</span></span>

<span data-ttu-id="c49f8-116">(El equipo de desarrollo puede generar el [SDK de Application Insights](app-insights-asp-net.md) en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c49f8-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span></span> <span data-ttu-id="c49f8-117">Esta instrumentación en tiempo de compilación les proporciona mayor flexibilidad al escribir una telemetría personalizada.</span><span class="sxs-lookup"><span data-stu-id="c49f8-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="c49f8-118">Sin embargo, no importa: puede seguir los pasos descritos aquí, con o sin el SDK integrado).</span><span class="sxs-lookup"><span data-stu-id="c49f8-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="c49f8-119">(Una vez) Instalación del módulo de administración de Application Insights</span><span class="sxs-lookup"><span data-stu-id="c49f8-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="c49f8-120">En el equipo donde se ejecuta Operations Manager:</span><span class="sxs-lookup"><span data-stu-id="c49f8-120">On the machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="c49f8-121">Desinstale cualquier versión anterior del paquete de administración:</span><span class="sxs-lookup"><span data-stu-id="c49f8-121">Uninstall any old version of the management pack:</span></span>
   1. <span data-ttu-id="c49f8-122">En Operations Manager, abra Administración, Módulos de administración.</span><span class="sxs-lookup"><span data-stu-id="c49f8-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="c49f8-123">Elimine la versión anterior.</span><span class="sxs-lookup"><span data-stu-id="c49f8-123">Delete the old version.</span></span>
2. <span data-ttu-id="c49f8-124">Descargue e instale el módulo de administración desde el catálogo.</span><span class="sxs-lookup"><span data-stu-id="c49f8-124">Download and install the management pack from the catalog.</span></span>
3. <span data-ttu-id="c49f8-125">Reinicie Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="c49f8-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="c49f8-126">Creación de un módulo de administración</span><span class="sxs-lookup"><span data-stu-id="c49f8-126">Create a management pack</span></span>
1. <span data-ttu-id="c49f8-127">En Operations Manager, abra **Creación**, **.NET... con Application Insights**, **Asistente para agregar monitores** y vuelva a elegir **.NET... con Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="c49f8-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="c49f8-128">Asigne un nombre a la configuración de acuerdo con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c49f8-128">Name the configuration after your app.</span></span> <span data-ttu-id="c49f8-129">(Tiene que instrumentar una aplicación cada vez).</span><span class="sxs-lookup"><span data-stu-id="c49f8-129">(You have to instrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="c49f8-130">En la misma página del asistente, cree un módulo de administración, o bien seleccione un módulo que creó anteriormente para Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c49f8-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="c49f8-131">(El [módulo de administración](https://technet.microsoft.com/library/cc974491.aspx) de Application Insights es una plantilla, a partir de la cual se crea una instancia.</span><span class="sxs-lookup"><span data-stu-id="c49f8-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="c49f8-132">Puede reutilizar la misma instancia más adelante).</span><span class="sxs-lookup"><span data-stu-id="c49f8-132">You can reuse the same instance later.)</span></span>

    ![En la pestaña Propiedades generales, escriba el nombre de la aplicación.](./media/app-insights-scom/040.png)

1. <span data-ttu-id="c49f8-136">Elija una aplicación que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="c49f8-136">Choose one app that you want to monitor.</span></span> <span data-ttu-id="c49f8-137">La característica de búsqueda busca entre las aplicaciones instaladas en los servidores.</span><span class="sxs-lookup"><span data-stu-id="c49f8-137">The search feature searches among apps installed on your servers.</span></span>
   
    ![En la pestaña What to Monitor (Qué supervisar), haga clic en Agregar, escriba parte del nombre de la aplicación, haga clic en Buscar, seleccione la aplicación y haga clic en Agregar y Aceptar.](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="c49f8-139">El campo opcional Ámbito de supervisión puede utilizarse para especificar un subconjunto de los servidores, si no desea supervisar la aplicación en todos los servidores.</span><span class="sxs-lookup"><span data-stu-id="c49f8-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span></span>
2. <span data-ttu-id="c49f8-140">En la siguiente página del asistente, debe proporcionar las credenciales para iniciar sesión en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c49f8-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span></span>
   
    <span data-ttu-id="c49f8-141">En esta página, elija el recurso de Application Insights donde desea que los datos de telemetría se analicen y muestren.</span><span class="sxs-lookup"><span data-stu-id="c49f8-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="c49f8-142">Si la aplicación se configuró para Application Insights durante el desarrollo, seleccione el recurso existente.</span><span class="sxs-lookup"><span data-stu-id="c49f8-142">If the application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="c49f8-143">De lo contrario, cree un recurso con un nombre que corresponda a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c49f8-143">Otherwise, create a new resource named for the app.</span></span> <span data-ttu-id="c49f8-144">Si hay otras aplicaciones que son componentes del mismo sistema, colóquelas en el mismo grupo de recursos, para que el acceso a los datos a la telemetría sea más fácil de administrar.</span><span class="sxs-lookup"><span data-stu-id="c49f8-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span></span>
     
     <span data-ttu-id="c49f8-145">Puede cambiar estas opciones aquí.</span><span class="sxs-lookup"><span data-stu-id="c49f8-145">You can change these settings later.</span></span>
     
     ![En la pestaña de configuración de Application Insights, haga clic en 'Iniciar sesión' y proporcione las credenciales de la cuenta de Microsoft para Azure.](./media/app-insights-scom/060.png)
3. <span data-ttu-id="c49f8-148">Realice los pasos del asistente.</span><span class="sxs-lookup"><span data-stu-id="c49f8-148">Complete the wizard.</span></span>
   
    ![Click Create](./media/app-insights-scom/070.png)

<span data-ttu-id="c49f8-150">Repita este procedimiento para cada aplicación que desee supervisar.</span><span class="sxs-lookup"><span data-stu-id="c49f8-150">Repeat this procedure for each app that you want to monitor.</span></span>

<span data-ttu-id="c49f8-151">Si necesita cambiar la configuración más adelante, vuelva a abrir las propiedades del monitor en la ventana Creación.</span><span class="sxs-lookup"><span data-stu-id="c49f8-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span></span>

![En Creación, seleccione .NET Application Performance Monitoring (Supervisión del rendimiento de la aplicación de .NET) con Application Insights, seleccione al monitor y haga clic en Propiedades.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="c49f8-153">Comprobación de la supervisión</span><span class="sxs-lookup"><span data-stu-id="c49f8-153">Verify monitoring</span></span>
<span data-ttu-id="c49f8-154">El monitor que ha instalado busca la aplicación en todos los servidores.</span><span class="sxs-lookup"><span data-stu-id="c49f8-154">The monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="c49f8-155">Cuando encuentra la aplicación, configura el Monitor de estado de Application Insights ahí para supervisarla.</span><span class="sxs-lookup"><span data-stu-id="c49f8-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span></span> <span data-ttu-id="c49f8-156">Si es necesario, instala primero el Monitor de estado en el servidor.</span><span class="sxs-lookup"><span data-stu-id="c49f8-156">If necessary, it first installs Status Monitor on the server.</span></span>

<span data-ttu-id="c49f8-157">Puede comprobar qué instancias de la aplicación ha encontrado:</span><span class="sxs-lookup"><span data-stu-id="c49f8-157">You can verify which instances of the app it has found:</span></span>

![En Supervisión, abra Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="c49f8-159">Visualización de la telemetría en Application Insights</span><span class="sxs-lookup"><span data-stu-id="c49f8-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="c49f8-160">En el [Portal de Azure](https://portal.azure.com), busque el recurso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c49f8-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span></span> <span data-ttu-id="c49f8-161">[Verá gráficos que muestran la telemetría](app-insights-dashboards.md) de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="c49f8-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="c49f8-162">(Si aún no ha aparecido en la página principal, haga clic en Live Metrics Stream).</span><span class="sxs-lookup"><span data-stu-id="c49f8-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c49f8-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c49f8-163">Next steps</span></span>
* <span data-ttu-id="c49f8-164">[Configuración de un panel](app-insights-dashboards.md) para reunir los gráficos más importantes que supervisan esta y otras aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c49f8-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="c49f8-165">Más información sobre las métricas</span><span class="sxs-lookup"><span data-stu-id="c49f8-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="c49f8-166">Configuración de alertas</span><span class="sxs-lookup"><span data-stu-id="c49f8-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="c49f8-167">Diagnóstico de problemas de rendimiento</span><span class="sxs-lookup"><span data-stu-id="c49f8-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="c49f8-168">Consultas de Analytics eficaces</span><span class="sxs-lookup"><span data-stu-id="c49f8-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="c49f8-169">Pruebas web de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="c49f8-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

