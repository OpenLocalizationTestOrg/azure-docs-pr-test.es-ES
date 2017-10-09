---
title: "flujo de hello aaaTrace en una aplicación de servicios de nube con diagnósticos de Azure | Documentos de Microsoft"
description: "Agregar seguimiento mensajes tooan Azure toohelp la depuración de aplicaciones, medir el rendimiento, supervisión, análisis del tráfico y mucho más."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="b6d32-103">Flujo de Hola de seguimiento de una aplicación de servicios en la nube con diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="b6d32-103">Trace hello flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="b6d32-104">El seguimiento es una manera toomonitor Hola la ejecución de la aplicación mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="b6d32-104">Tracing is a way for you toomonitor hello execution of your application while it is running.</span></span> <span data-ttu-id="b6d32-105">Puede usar hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), y [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) clases toorecord información sobre los errores y ejecución de la aplicación en registros, archivos de texto u otros dispositivos para su análisis posterior.</span><span class="sxs-lookup"><span data-stu-id="b6d32-105">You can use hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes toorecord information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="b6d32-106">Para obtener más información acerca del seguimiento, consulte [Seguimiento e instrumentación de aplicaciones](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6d32-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="b6d32-107">Uso de las instrucciones de seguimiento y los modificadores de seguimiento</span><span class="sxs-lookup"><span data-stu-id="b6d32-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="b6d32-108">Seguimiento de implementar en la aplicación de servicios en la nube mediante la adición de hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello configuración de la aplicación y realizar llamadas tooSystem.Diagnostics.Trace o a System.Diagnostics.Debug en su código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b6d32-108">Implement tracing in your Cloud Services application by adding hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello application configuration and making calls tooSystem.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="b6d32-109">Utilizar el archivo de configuración de hello *app.config* para hello y roles de trabajo *web.config* para los roles web.</span><span class="sxs-lookup"><span data-stu-id="b6d32-109">Use hello configuration file *app.config* for worker roles and hello *web.config* for web roles.</span></span> <span data-ttu-id="b6d32-110">Cuando se crea un nuevo servicio hospedado mediante una plantilla de Visual Studio, diagnósticos de Azure se agrega automáticamente el proyecto toohello y hello DiagnosticMonitorTraceListener se agrega toohello el archivo de configuración adecuado para los roles de Hola que agregue.</span><span class="sxs-lookup"><span data-stu-id="b6d32-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added toohello project and hello DiagnosticMonitorTraceListener is added toohello appropriate configuration file for hello roles that you add.</span></span>

<span data-ttu-id="b6d32-111">Para obtener información sobre cómo colocar instrucciones de seguimiento, vea [Cómo: agregar instrucciones de seguimiento tooApplication código](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6d32-111">For information on placing trace statements, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="b6d32-112">Al colocar [modificadores de seguimiento](https://msdn.microsoft.com/library/3at424ac.aspx) en el código, puede controlar si se realiza el seguimiento y cuál es su alcance.</span><span class="sxs-lookup"><span data-stu-id="b6d32-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="b6d32-113">Esto le permite supervisar el estado de saludo de la aplicación en un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b6d32-113">This lets you monitor hello status of your application in a production environment.</span></span> <span data-ttu-id="b6d32-114">Esto es especialmente importante en una aplicación empresarial que usa varios componentes que se ejecutan en varios equipos.</span><span class="sxs-lookup"><span data-stu-id="b6d32-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="b6d32-115">Para obtener más información, consulte [Procedimientos: configuración de modificadores de seguimiento](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6d32-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-hello-trace-listener-in-an-azure-application"></a><span data-ttu-id="b6d32-116">Configurar el agente de escucha de seguimiento de hello en una aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="b6d32-116">Configure hello trace listener in an Azure application</span></span>
<span data-ttu-id="b6d32-117">Trace, Debug y TraceSource, deberá configurar "agentes de escucha" toocollect y mensajes de saludo de registro que se envían.</span><span class="sxs-lookup"><span data-stu-id="b6d32-117">Trace, Debug and TraceSource, require you set up "listeners" toocollect and record hello messages that are sent.</span></span> <span data-ttu-id="b6d32-118">Los agentes de escucha de recopilan, almacenan y enrutan los mensajes de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="b6d32-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="b6d32-119">Estos flujos dirigen Hola seguimiento salida tooan destino apropiado, como un registro, una ventana o un archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="b6d32-119">They direct hello tracing output tooan appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="b6d32-120">Diagnósticos de Azure usa hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) clase.</span><span class="sxs-lookup"><span data-stu-id="b6d32-120">Azure Diagnostics uses hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="b6d32-121">Antes de completar Hola siguiendo el procedimiento, debe inicializar Hola monitor de diagnóstico de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6d32-121">Before you complete hello following procedure, you must initialize hello Azure diagnostic monitor.</span></span> <span data-ttu-id="b6d32-122">toodo, vea [habilitar diagnósticos en Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b6d32-122">toodo this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="b6d32-123">Tenga en cuenta que si usa plantillas de Hola que se proporcionan con Visual Studio, Hola configuración de agente de escucha de Hola se agrega automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="b6d32-123">Note that if you use hello templates that are provided by Visual Studio, hello configuration of hello listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="b6d32-124">Incorporación de un agente de escucha de seguimiento</span><span class="sxs-lookup"><span data-stu-id="b6d32-124">Add a trace listener</span></span>
1. <span data-ttu-id="b6d32-125">Abra el archivo web.config o app.config de hello para el rol.</span><span class="sxs-lookup"><span data-stu-id="b6d32-125">Open hello web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="b6d32-126">Agregar Hola siguiente archivo de código toohello.</span><span class="sxs-lookup"><span data-stu-id="b6d32-126">Add hello following code toohello file.</span></span> <span data-ttu-id="b6d32-127">Cambiar Hola atributo toouse Hola versión número de versión Hola ensamblado que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="b6d32-127">Change hello Version attribute toouse hello version number of hello assembly you are referencing.</span></span> <span data-ttu-id="b6d32-128">versión del ensamblado Hello no necesariamente cambiar con cada versión del SDK de Azure a menos que haya actualizaciones tooit.</span><span class="sxs-lookup"><span data-stu-id="b6d32-128">hello assembly version does not necessarily change with each Azure SDK release unless there are updates tooit.</span></span>
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > <span data-ttu-id="b6d32-129">Asegúrese de que tiene un toohello de referencia de proyecto Microsoft.WindowsAzure.Diagnostics ensamblado.</span><span class="sxs-lookup"><span data-stu-id="b6d32-129">Make sure you have a project reference toohello Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="b6d32-130">Número de versión de actualización hello en xml de Hola por encima de la versión de Hola toomatch de hello al que hace referencia el ensamblado Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="b6d32-130">Update hello version number in hello xml above toomatch hello version of hello referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="b6d32-131">Guarde el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6d32-131">Save hello config file.</span></span>

<span data-ttu-id="b6d32-132">Para más información sobre los agentes de escucha, vea [Agentes de escucha de seguimiento](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6d32-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="b6d32-133">Después de completar el agente de escucha de hello pasos tooadd hello, puede agregar código de tooyour de instrucciones de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="b6d32-133">After you complete hello steps tooadd hello listener, you can add trace statements tooyour code.</span></span>

### <a name="tooadd-trace-statement-tooyour-code"></a><span data-ttu-id="b6d32-134">código de tooyour de instrucción de seguimiento tooadd</span><span class="sxs-lookup"><span data-stu-id="b6d32-134">tooadd trace statement tooyour code</span></span>
1. <span data-ttu-id="b6d32-135">Abra un archivo de origen para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b6d32-135">Open a source file for your application.</span></span> <span data-ttu-id="b6d32-136">Por ejemplo, hello <RoleName>archivo .cs para el rol de trabajo de Hola o web.</span><span class="sxs-lookup"><span data-stu-id="b6d32-136">For example, hello <RoleName>.cs file for hello worker role or web role.</span></span>
2. <span data-ttu-id="b6d32-137">Agregue Hola siguientes mediante la instrucción si ya no se ha agregado:</span><span class="sxs-lookup"><span data-stu-id="b6d32-137">Add hello following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="b6d32-138">Agregar instrucciones de seguimiento donde desea toocapture información sobre el estado de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b6d32-138">Add Trace statements where you want toocapture information about hello state of your application.</span></span> <span data-ttu-id="b6d32-139">Puede utilizar una variedad de salida de hello tooformat de métodos de hello instrucción de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="b6d32-139">You can use a variety of methods tooformat hello output of hello Trace statement.</span></span> <span data-ttu-id="b6d32-140">Para obtener más información, consulte [Cómo: agregar instrucciones de seguimiento tooApplication código](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6d32-140">For more information, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="b6d32-141">Guarde el archivo de código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6d32-141">Save hello source file.</span></span>

