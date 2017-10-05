---
title: "Seguimiento del flujo en una aplicación de Cloud Services con Diagnósticos de Azure | Microsoft Docs"
description: "Agregar mensajes de seguimiento a una aplicación de Azure para facilitar la depuración, medición del rendimiento, supervisión, análisis del tráfico y mucho más."
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
ms.openlocfilehash: 35b4a4270846c54a1ca760e803ef7adba60cf03b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="trace-the-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="6866d-103">Seguimiento del flujo en una aplicación de servicios en la nube con Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="6866d-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="6866d-104">El seguimiento es una manera de supervisar la ejecución de la aplicación mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="6866d-104">Tracing is a way for you to monitor the execution of your application while it is running.</span></span> <span data-ttu-id="6866d-105">Puede usar las clases [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx) y [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) para registrar información sobre errores y ejecución de la aplicaciones en registros, archivos de texto u otros dispositivos para su análisis posterior.</span><span class="sxs-lookup"><span data-stu-id="6866d-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="6866d-106">Para obtener más información acerca del seguimiento, consulte [Seguimiento e instrumentación de aplicaciones](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="6866d-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="6866d-107">Uso de las instrucciones de seguimiento y los modificadores de seguimiento</span><span class="sxs-lookup"><span data-stu-id="6866d-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="6866d-108">Implemente el seguimiento en la aplicación de servicios en la nube al agregar [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) a la configuración de la aplicación y realizar llamadas a System.Diagnostics.Trace o a System.Diagnostics.Debug en el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6866d-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="6866d-109">Use el archivo de configuración *app.config* para los roles de trabajo y *web.config* para los roles web.</span><span class="sxs-lookup"><span data-stu-id="6866d-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span></span> <span data-ttu-id="6866d-110">Cuando se crea un nuevo servicio hospedado mediante una plantilla de Visual Studio, Diagnósticos de Azure se agrega automáticamente al proyecto y DiagnosticMonitorTraceListener se agrega al archivo de configuración adecuado para los roles que se añadan.</span><span class="sxs-lookup"><span data-stu-id="6866d-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span></span>

<span data-ttu-id="6866d-111">Para obtener información sobre cómo colocar instrucciones de seguimiento, consulte [Procedimientos: incorporación de instrucciones de seguimiento al código de aplicación](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="6866d-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="6866d-112">Al colocar [modificadores de seguimiento](https://msdn.microsoft.com/library/3at424ac.aspx) en el código, puede controlar si se realiza el seguimiento y cuál es su alcance.</span><span class="sxs-lookup"><span data-stu-id="6866d-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="6866d-113">Con ello puede supervisar el estado de la aplicación en un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6866d-113">This lets you monitor the status of your application in a production environment.</span></span> <span data-ttu-id="6866d-114">Esto es especialmente importante en una aplicación empresarial que usa varios componentes que se ejecutan en varios equipos.</span><span class="sxs-lookup"><span data-stu-id="6866d-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="6866d-115">Para obtener más información, consulte [Procedimientos: configuración de modificadores de seguimiento](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="6866d-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-the-trace-listener-in-an-azure-application"></a><span data-ttu-id="6866d-116">Configuración de la escucha de seguimiento en una aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="6866d-116">Configure the trace listener in an Azure application</span></span>
<span data-ttu-id="6866d-117">Tendrá que configurar "agentes de escucha" para Trace, Debug y TraceSource, para recopilar y registrar los mensajes que se envían.</span><span class="sxs-lookup"><span data-stu-id="6866d-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span></span> <span data-ttu-id="6866d-118">Los agentes de escucha de recopilan, almacenan y enrutan los mensajes de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="6866d-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="6866d-119">Estos dirigen los resultados del seguimiento a un destino apropiado, como un registro, una ventana o un archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="6866d-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="6866d-120">Diagnósticos de Azure usa la clase [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6866d-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="6866d-121">Antes de completar el siguiente procedimiento, tiene que inicializar el monitor de diagnóstico de Azure.</span><span class="sxs-lookup"><span data-stu-id="6866d-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span></span> <span data-ttu-id="6866d-122">Para ello, consulte [Habilitación de diagnósticos en Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6866d-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="6866d-123">Tenga en cuenta que si usa las plantillas proporcionadas por Visual Studio, la configuración del agente de escucha se agrega automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6866d-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="6866d-124">Incorporación de un agente de escucha de seguimiento</span><span class="sxs-lookup"><span data-stu-id="6866d-124">Add a trace listener</span></span>
1. <span data-ttu-id="6866d-125">Abra el archivo web.config o app.config para su rol.</span><span class="sxs-lookup"><span data-stu-id="6866d-125">Open the web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="6866d-126">Agregue el siguiente código al archivo.</span><span class="sxs-lookup"><span data-stu-id="6866d-126">Add the following code to the file.</span></span> <span data-ttu-id="6866d-127">Cambie el atributo Version para usar el número de versión del ensamblado al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="6866d-127">Change the Version attribute to use the version number of the assembly you are referencing.</span></span> <span data-ttu-id="6866d-128">La versión de ensamblado no cambia necesariamente con cada versión del SDK de Azure, a menos que haya actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="6866d-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span></span>
   
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
   > <span data-ttu-id="6866d-129">Asegúrese de que tiene una referencia de proyecto al ensamblado Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="6866d-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="6866d-130">Actualice el número de versión en el xml anterior para que coincida con la versión del ensamblado de Microsoft.WindowsAzure.Diagnostics al que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="6866d-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="6866d-131">Guarde el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="6866d-131">Save the config file.</span></span>

<span data-ttu-id="6866d-132">Para más información sobre los agentes de escucha, vea [Agentes de escucha de seguimiento](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="6866d-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="6866d-133">Después de completar los pasos para agregar el agente de escucha, puede agregar instrucciones de seguimiento al código.</span><span class="sxs-lookup"><span data-stu-id="6866d-133">After you complete the steps to add the listener, you can add trace statements to your code.</span></span>

### <a name="to-add-trace-statement-to-your-code"></a><span data-ttu-id="6866d-134">Para agregar instrucciones de seguimiento al código</span><span class="sxs-lookup"><span data-stu-id="6866d-134">To add trace statement to your code</span></span>
1. <span data-ttu-id="6866d-135">Abra un archivo de origen para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6866d-135">Open a source file for your application.</span></span> <span data-ttu-id="6866d-136">Por ejemplo, el archivo <RoleName>.cs para el rol de trabajo o el rol web.</span><span class="sxs-lookup"><span data-stu-id="6866d-136">For example, the <RoleName>.cs file for the worker role or web role.</span></span>
2. <span data-ttu-id="6866d-137">Agregue la siguiente instrucción using si no se agregó ya:</span><span class="sxs-lookup"><span data-stu-id="6866d-137">Add the following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="6866d-138">Agregue instrucciones de seguimiento en donde desee capturar información sobre el estado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6866d-138">Add Trace statements where you want to capture information about the state of your application.</span></span> <span data-ttu-id="6866d-139">Puede usar diversos métodos para dar formato al resultado de la instrucción de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="6866d-139">You can use a variety of methods to format the output of the Trace statement.</span></span> <span data-ttu-id="6866d-140">Para información, vea [Procedimientos: adición de instrucciones de seguimiento al código de aplicación](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="6866d-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="6866d-141">Guarde el archivo de origen.</span><span class="sxs-lookup"><span data-stu-id="6866d-141">Save the source file.</span></span>

