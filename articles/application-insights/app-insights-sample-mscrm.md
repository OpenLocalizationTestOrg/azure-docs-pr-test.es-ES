---
title: "aaaMicrosoft Dynamics CRM y visión de la aplicación de Azure | Documentos de Microsoft"
description: "Obtenga la telemetría de Microsoft Dynamics CRM Online con Application Insights. Tutorial sobre configuración, obtención de datos, visualización y exportación."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="c68c2-104">Tutorial: Habilitar la telemetría para Microsoft Dynamics CRM Online con Application Insights</span><span class="sxs-lookup"><span data-stu-id="c68c2-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="c68c2-105">Este artículo muestra cómo los datos de telemetría tooget de [Microsoft Dynamics CRM Online](https://www.dynamics.com/) con [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="c68c2-105">This article shows you how tooget telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="c68c2-106">Usaremos el proceso completo de Hola de agregar la aplicación de tooyour de secuencias de comandos de Application Insights, captura de datos y visualización de datos.</span><span class="sxs-lookup"><span data-stu-id="c68c2-106">We’ll walk through hello complete process of adding Application Insights script tooyour application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="c68c2-107">[Examinar la solución de ejemplo de Hola](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="c68c2-107">[Browse hello sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a><span data-ttu-id="c68c2-108">Agregar Application Insights toonew o instancia de CRM Online existente</span><span class="sxs-lookup"><span data-stu-id="c68c2-108">Add Application Insights toonew or existing CRM Online instance</span></span>
<span data-ttu-id="c68c2-109">toomonitor su aplicación, agregar una aplicación de tooyour Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="c68c2-109">toomonitor your application, you add an Application Insights SDK tooyour application.</span></span> <span data-ttu-id="c68c2-110">Hola SDK envía telemetría toohello [portal de Application Insights](https://portal.azure.com), donde puede usar nuestro análisis eficaces y herramientas de diagnóstico, o exportar hello toostorage de datos.</span><span class="sxs-lookup"><span data-stu-id="c68c2-110">hello SDK sends telemetry toohello [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export hello data toostorage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="c68c2-111">Creación de un recurso de Application Insights en Azure</span><span class="sxs-lookup"><span data-stu-id="c68c2-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="c68c2-112">Obtenga una [cuenta en Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="c68c2-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="c68c2-113">Inicio de sesión en hello [portal de Azure](https://portal.azure.com) y agregar un nuevo recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c68c2-113">Sign into hello [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="c68c2-114">Aquí es donde se procesarán y mostrarán los datos.</span><span class="sxs-lookup"><span data-stu-id="c68c2-114">This is where your data will be processed and displayed.</span></span>
   
    ![Haga clic en +, Servicios para desarrolladores, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="c68c2-116">Elija ASP.NET como tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="c68c2-116">Choose ASP.NET as hello application type.</span></span>
3. <span data-ttu-id="c68c2-117">Abra la página de introducción de Hola y abra "supervisar y diagnosticar el lado del cliente".</span><span class="sxs-lookup"><span data-stu-id="c68c2-117">Open hello Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Fragmento de código para inserción en la página web](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="c68c2-119">**Mantenga abierta la página de códigos de hello** mientras Hola siguiente paso en otra ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="c68c2-119">**Keep hello code page open** while you do hello next step in another browser window.</span></span> <span data-ttu-id="c68c2-120">Código de hello, deberá pronto.</span><span class="sxs-lookup"><span data-stu-id="c68c2-120">You'll need hello code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="c68c2-121">Creación de un recurso web de JavaScript en Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="c68c2-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="c68c2-122">Abra la instancia de CRM Online e inicie sesión con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="c68c2-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="c68c2-123">Abra Microsoft Dynamics CRM configuración, las personalizaciones, personalizar Hola sistema</span><span class="sxs-lookup"><span data-stu-id="c68c2-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize hello System</span></span>
   
    ![Configuración de Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Configuración > Personalizaciones](./media/app-insights-sample-mscrm/05.png)

    ![Personalizar la opción de sistema de Hola](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="c68c2-127">Cree un recurso de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c68c2-127">Create a JavaScript resource.</span></span>
   
    ![Cuadro de diálogo de nuevo recurso web](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="c68c2-129">Asígnele un nombre, seleccione **Script (JScript)** y Hola Abrir editor de texto.</span><span class="sxs-lookup"><span data-stu-id="c68c2-129">Give it a name, select **Script (JScript)** and open hello text editor.</span></span>
   
    ![Editor de texto hello abierto](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="c68c2-131">Copie el código de hello de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c68c2-131">Copy hello code from Application Insights.</span></span> <span data-ttu-id="c68c2-132">Mientras se copiaban que las etiquetas de script de tooignore seguro.</span><span class="sxs-lookup"><span data-stu-id="c68c2-132">While copying make sure tooignore script tags.</span></span> <span data-ttu-id="c68c2-133">Consulte la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="c68c2-133">Refer below screenshot:</span></span>
   
    ![Establecer la clave de instrumentación](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="c68c2-135">código de Hello incluye la clave de instrumentación de Hola que identifica el recurso de información de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c68c2-135">hello code includes hello instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="c68c2-136">Guarde y publique.</span><span class="sxs-lookup"><span data-stu-id="c68c2-136">Save and publish.</span></span>
   
    ![Guardar y publicar](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="c68c2-138">Formularios de instrumentos</span><span class="sxs-lookup"><span data-stu-id="c68c2-138">Instrument Forms</span></span>
1. <span data-ttu-id="c68c2-139">En Microsoft CRM Online, abra el formulario de la cuenta de hello</span><span class="sxs-lookup"><span data-stu-id="c68c2-139">In Microsoft CRM Online, open hello Account form</span></span>
   
    ![Formulario de la cuenta](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="c68c2-141">Abra el formulario de hello propiedades</span><span class="sxs-lookup"><span data-stu-id="c68c2-141">Open hello form Properties</span></span>
   
    ![Propiedades del formulario](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="c68c2-143">Agregar Hola recurso web de JavaScript que ha creado</span><span class="sxs-lookup"><span data-stu-id="c68c2-143">Add hello JavaScript web resource that you created</span></span>
   
    ![Menú Agregar](./media/app-insights-sample-mscrm/13.png)
   
    ![Agregar recurso web de Hola](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="c68c2-146">Guarde y publique las personalizaciones de formulario.</span><span class="sxs-lookup"><span data-stu-id="c68c2-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="c68c2-147">Métricas capturadas</span><span class="sxs-lookup"><span data-stu-id="c68c2-147">Metrics captured</span></span>
<span data-ttu-id="c68c2-148">Ha configurado una captura de telemetría del formulario de Hola.</span><span class="sxs-lookup"><span data-stu-id="c68c2-148">You have now set up telemetry capture for hello form.</span></span> <span data-ttu-id="c68c2-149">Cada vez que se utiliza, se enviará datos tooyour recursos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c68c2-149">Whenever it is used, data will be sent tooyour Application Insights resource.</span></span>

<span data-ttu-id="c68c2-150">Estos son ejemplos de datos de Hola que verá.</span><span class="sxs-lookup"><span data-stu-id="c68c2-150">Here are samples of hello data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="c68c2-151">Estado de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c68c2-151">Application health</span></span>
![Ejemplo de tiempo de carga de página](./media/app-insights-sample-mscrm/15.png)

![Ejemplo de gráfico de vistas de página](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="c68c2-154">Excepciones de explorador:</span><span class="sxs-lookup"><span data-stu-id="c68c2-154">Browser exceptions:</span></span>

![Gráfico de excepciones de explorador](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="c68c2-156">Haga clic en hello gráfico tooget más detalle:</span><span class="sxs-lookup"><span data-stu-id="c68c2-156">Click hello chart tooget more detail:</span></span>

![Lista de excepciones](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="c68c2-158">Uso</span><span class="sxs-lookup"><span data-stu-id="c68c2-158">Usage</span></span>
![Sesiones, usuarios y vistas de página](./media/app-insights-sample-mscrm/19.png)

![Gráficos de sesión](./media/app-insights-sample-mscrm/20.png)

![Versiones de explorador](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="c68c2-162">Exploradores</span><span class="sxs-lookup"><span data-stu-id="c68c2-162">Browsers</span></span>
![Desglose de tiempo de carga de página](./media/app-insights-sample-mscrm/22.png)

![Recuento de sesiones por versión de explorador](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="c68c2-165">Geolocalización</span><span class="sxs-lookup"><span data-stu-id="c68c2-165">Geolocation</span></span>
![Recuento de sesiones por país](./media/app-insights-sample-mscrm/24.png)

![Sesiones y usuarios por país](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="c68c2-168">Solicitud de la vista de página interior</span><span class="sxs-lookup"><span data-stu-id="c68c2-168">Inside page view request</span></span>
![Resumen de vistas de página](./media/app-insights-sample-mscrm/26.png)

![Buscar en eventos de vista de página](./media/app-insights-sample-mscrm/27.png)

![Vistas de página similares](./media/app-insights-sample-mscrm/28.png)

![Propiedades de la vista de página](./media/app-insights-sample-mscrm/29.png)

![Páginas por sesión](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="c68c2-174">Código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="c68c2-174">Sample code</span></span>
<span data-ttu-id="c68c2-175">[Examinar el código de ejemplo de Hola](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="c68c2-175">[Browse hello sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="c68c2-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="c68c2-176">Power BI</span></span>
<span data-ttu-id="c68c2-177">Puede hacer un análisis más profundo incluso si se [exportar Hola datos tooMicrosoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="c68c2-177">You can do even deeper analysis if you [export hello data tooMicrosoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="c68c2-178">Solución de ejemplo de Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="c68c2-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="c68c2-179">[Esta es la solución de ejemplo de Hola implementada en Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="c68c2-179">[Here is hello sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="c68c2-180">Más información</span><span class="sxs-lookup"><span data-stu-id="c68c2-180">Learn more</span></span>
* [<span data-ttu-id="c68c2-181">¿Qué es Application Insights?</span><span class="sxs-lookup"><span data-stu-id="c68c2-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="c68c2-182">Application Insights para páginas web</span><span class="sxs-lookup"><span data-stu-id="c68c2-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="c68c2-183">Más ejemplos y tutoriales</span><span class="sxs-lookup"><span data-stu-id="c68c2-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
