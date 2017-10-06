---
title: "aaaUse contadores de rendimiento de diagnósticos de Azure | Documentos de Microsoft"
description: "Utilice los contadores de rendimiento en los servicios de nube de Azure o los cuellos de botella toofind de máquina virtual y optimizar el rendimiento."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="60db7-103">Creación y uso de contadores de rendimiento en una aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="60db7-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="60db7-104">Este artículo describen las ventajas de Hola de y cómo los contadores de rendimiento de tooput en su aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="60db7-104">This article describes hello benefits of and how tooput performance counters into your Azure application.</span></span> <span data-ttu-id="60db7-105">Puede usar datos toocollect, encontrar cuellos de botella y ajustar el rendimiento del sistema y de aplicación.</span><span class="sxs-lookup"><span data-stu-id="60db7-105">You can use them toocollect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="60db7-106">Contadores de rendimiento disponibles para Windows Server, IIS y ASP.NET también se pueden recopilar y utilizan mantenimiento de hello toodetermine de los roles web de Azure, roles de trabajo y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="60db7-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used toodetermine hello health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="60db7-107">Además, puede crear y usar contadores de rendimiento personalizados.</span><span class="sxs-lookup"><span data-stu-id="60db7-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="60db7-108">Puede examinar los datos del contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="60db7-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="60db7-109">Directamente en el host de la aplicación hello con la herramienta Monitor de rendimiento de hello acceder mediante Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="60db7-109">Directly on hello application host with hello Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="60db7-110">Con el uso de System Center Operations Manager Hola el módulo de administración de Azure</span><span class="sxs-lookup"><span data-stu-id="60db7-110">With System Center Operations Manager using hello Azure Management Pack</span></span>
3. <span data-ttu-id="60db7-111">Con otras herramientas de supervisión que tienen acceso a Hola datos de diagnóstico transfieren tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60db7-111">With other monitoring tools that access hello diagnostic data transferred tooAzure storage.</span></span> <span data-ttu-id="60db7-112">Consulte [Guardar y ver datos de diagnóstico en el almacenamiento de Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="60db7-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="60db7-113">Para obtener más información acerca de cómo supervisar el rendimiento de saludo de la aplicación Hola [portal de Azure](http://portal.azure.com/), consulte [cómo los servicios de nube tooMonitor](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="60db7-113">For more information on monitoring hello performance of your application in hello [Azure portal](http://portal.azure.com/), see [How tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="60db7-114">Para obtener instrucciones detalladas sobre cómo crear un registro y seguimiento de la estrategia y usar diagnósticos y otros problemas de tootroubleshoot técnicas adicionales y optimizar aplicaciones de Azure, consulte [prácticas recomendadas para el desarrollo de Azure Aplicaciones](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="60db7-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques tootroubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="60db7-115">Habilitación de la supervisión de contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="60db7-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="60db7-116">Los contadores de rendimiento no están habilitados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="60db7-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="60db7-117">La aplicación o una tarea de inicio debe modificar diagnósticos de forma predeterminada Hola contadores de rendimiento de específicos de Hola de agente configuración tooinclude que desea toomonitor para cada instancia de rol.</span><span class="sxs-lookup"><span data-stu-id="60db7-117">Your application or a startup task must modify hello default diagnostics agent configuration tooinclude hello specific performance counters that you wish toomonitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="60db7-118">Contadores de rendimiento disponibles para Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="60db7-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="60db7-119">Azure proporciona un subconjunto de los contadores de rendimiento de hello disponibles para Windows Server, IIS y Hola pila ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="60db7-119">Azure provides a subset of hello performance counters available for Windows Server, IIS and hello ASP.NET stack.</span></span> <span data-ttu-id="60db7-120">Hello tabla siguiente enumeran algunos de los contadores de rendimiento de Hola de especial interés para las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="60db7-120">hello following table lists some of hello performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="60db7-121">Categoría de contador: Objeto (instancia)</span><span class="sxs-lookup"><span data-stu-id="60db7-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="60db7-122">Nombre del contador</span><span class="sxs-lookup"><span data-stu-id="60db7-122">Counter Name</span></span> | <span data-ttu-id="60db7-123">Referencia</span><span class="sxs-lookup"><span data-stu-id="60db7-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60db7-124">Excepciones de .NET CLR (*Global*)</span><span class="sxs-lookup"><span data-stu-id="60db7-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="60db7-125">Nº de excepciones producidas por segundo</span><span class="sxs-lookup"><span data-stu-id="60db7-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="60db7-126">Contadores de rendimiento de excepciones</span><span class="sxs-lookup"><span data-stu-id="60db7-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="60db7-127">Memoria de .NET CLR (*Global*)</span><span class="sxs-lookup"><span data-stu-id="60db7-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="60db7-128">% de tiempo del GC</span><span class="sxs-lookup"><span data-stu-id="60db7-128">% Time in GC</span></span> |<span data-ttu-id="60db7-129">Contadores de rendimiento de memoria</span><span class="sxs-lookup"><span data-stu-id="60db7-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="60db7-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-130">ASP.NET</span></span> |<span data-ttu-id="60db7-131">Reinicios de la aplicación</span><span class="sxs-lookup"><span data-stu-id="60db7-131">Application Restarts</span></span> |<span data-ttu-id="60db7-132">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-133">ASP.NET</span></span> |<span data-ttu-id="60db7-134">Tiempo de ejecución de solicitud</span><span class="sxs-lookup"><span data-stu-id="60db7-134">Request Execution Time</span></span> |<span data-ttu-id="60db7-135">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-136">ASP.NET</span></span> |<span data-ttu-id="60db7-137">Solicitudes desconectadas</span><span class="sxs-lookup"><span data-stu-id="60db7-137">Requests Disconnected</span></span> |<span data-ttu-id="60db7-138">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-139">ASP.NET</span></span> |<span data-ttu-id="60db7-140">Reinicios del proceso de trabajo</span><span class="sxs-lookup"><span data-stu-id="60db7-140">Worker Process Restarts</span></span> |<span data-ttu-id="60db7-141">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-142">Aplicaciones ASP.NET(**Total**)</span><span class="sxs-lookup"><span data-stu-id="60db7-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="60db7-143">Total de solicitudes</span><span class="sxs-lookup"><span data-stu-id="60db7-143">Requests Total</span></span> |<span data-ttu-id="60db7-144">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-145">Aplicaciones ASP.NET(**Total**)</span><span class="sxs-lookup"><span data-stu-id="60db7-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="60db7-146">Solicitudes por segundo</span><span class="sxs-lookup"><span data-stu-id="60db7-146">Requests/Sec</span></span> |<span data-ttu-id="60db7-147">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="60db7-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="60db7-149">Tiempo de ejecución de solicitud</span><span class="sxs-lookup"><span data-stu-id="60db7-149">Request Execution Time</span></span> |<span data-ttu-id="60db7-150">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="60db7-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="60db7-152">Tiempo de espera de la solicitud</span><span class="sxs-lookup"><span data-stu-id="60db7-152">Request Wait Time</span></span> |<span data-ttu-id="60db7-153">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="60db7-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="60db7-155">Solicitudes actuales</span><span class="sxs-lookup"><span data-stu-id="60db7-155">Requests Current</span></span> |<span data-ttu-id="60db7-156">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="60db7-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="60db7-158">Solicitudes en cola</span><span class="sxs-lookup"><span data-stu-id="60db7-158">Requests Queued</span></span> |<span data-ttu-id="60db7-159">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="60db7-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="60db7-161">Solicitudes rechazadas</span><span class="sxs-lookup"><span data-stu-id="60db7-161">Requests Rejected</span></span> |<span data-ttu-id="60db7-162">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-163">Memoria</span><span class="sxs-lookup"><span data-stu-id="60db7-163">Memory</span></span> |<span data-ttu-id="60db7-164">MB disponibles</span><span class="sxs-lookup"><span data-stu-id="60db7-164">Available MBytes</span></span> |<span data-ttu-id="60db7-165">Contadores de rendimiento de memoria</span><span class="sxs-lookup"><span data-stu-id="60db7-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="60db7-166">Memoria</span><span class="sxs-lookup"><span data-stu-id="60db7-166">Memory</span></span> |<span data-ttu-id="60db7-167">Bytes confirmados</span><span class="sxs-lookup"><span data-stu-id="60db7-167">Committed Bytes</span></span> |<span data-ttu-id="60db7-168">Contadores de rendimiento de memoria</span><span class="sxs-lookup"><span data-stu-id="60db7-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="60db7-169">Processor(_Total)</span><span class="sxs-lookup"><span data-stu-id="60db7-169">Processor(_Total)</span></span> |<span data-ttu-id="60db7-170">% de tiempo de procesador</span><span class="sxs-lookup"><span data-stu-id="60db7-170">% Processor Time</span></span> |<span data-ttu-id="60db7-171">Contadores de rendimiento para ASP.NET</span><span class="sxs-lookup"><span data-stu-id="60db7-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="60db7-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="60db7-172">TCPv4</span></span> |<span data-ttu-id="60db7-173">Errores de conexión</span><span class="sxs-lookup"><span data-stu-id="60db7-173">Connection Failures</span></span> |<span data-ttu-id="60db7-174">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="60db7-174">TCP Object</span></span> |
| <span data-ttu-id="60db7-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="60db7-175">TCPv4</span></span> |<span data-ttu-id="60db7-176">Conexiones establecidas</span><span class="sxs-lookup"><span data-stu-id="60db7-176">Connections Established</span></span> |<span data-ttu-id="60db7-177">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="60db7-177">TCP Object</span></span> |
| <span data-ttu-id="60db7-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="60db7-178">TCPv4</span></span> |<span data-ttu-id="60db7-179">Restablecimiento de conexiones</span><span class="sxs-lookup"><span data-stu-id="60db7-179">Connections Reset</span></span> |<span data-ttu-id="60db7-180">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="60db7-180">TCP Object</span></span> |
| <span data-ttu-id="60db7-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="60db7-181">TCPv4</span></span> |<span data-ttu-id="60db7-182">Segmentos enviados por segundo</span><span class="sxs-lookup"><span data-stu-id="60db7-182">Segments Sent/sec</span></span> |<span data-ttu-id="60db7-183">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="60db7-183">TCP Object</span></span> |
| <span data-ttu-id="60db7-184">Interfaz de red(*)</span><span class="sxs-lookup"><span data-stu-id="60db7-184">Network Interface(*)</span></span> |<span data-ttu-id="60db7-185">Bytes recibidos por segundo</span><span class="sxs-lookup"><span data-stu-id="60db7-185">Bytes Received/sec</span></span> |<span data-ttu-id="60db7-186">Objeto de interfaz de red</span><span class="sxs-lookup"><span data-stu-id="60db7-186">Network Interface Object</span></span> |
| <span data-ttu-id="60db7-187">Interfaz de red(*)</span><span class="sxs-lookup"><span data-stu-id="60db7-187">Network Interface(*)</span></span> |<span data-ttu-id="60db7-188">Bytes enviados por segundo</span><span class="sxs-lookup"><span data-stu-id="60db7-188">Bytes Sent/sec</span></span> |<span data-ttu-id="60db7-189">Objeto de interfaz de red</span><span class="sxs-lookup"><span data-stu-id="60db7-189">Network Interface Object</span></span> |
| <span data-ttu-id="60db7-190">Interfaz de red (Adaptador de red de bus de máquina virtual de Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="60db7-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="60db7-191">Bytes recibidos por segundo</span><span class="sxs-lookup"><span data-stu-id="60db7-191">Bytes Received/sec</span></span> |<span data-ttu-id="60db7-192">Objeto de interfaz de red</span><span class="sxs-lookup"><span data-stu-id="60db7-192">Network Interface Object</span></span> |
| <span data-ttu-id="60db7-193">Interfaz de red (Adaptador de red de bus de máquina virtual de Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="60db7-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="60db7-194">Bytes enviados por segundo</span><span class="sxs-lookup"><span data-stu-id="60db7-194">Bytes Sent/sec</span></span> |<span data-ttu-id="60db7-195">Objeto de interfaz de red</span><span class="sxs-lookup"><span data-stu-id="60db7-195">Network Interface Object</span></span> |
| <span data-ttu-id="60db7-196">Interfaz de red (Adaptador de red de bus de máquina virtual de Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="60db7-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="60db7-197">Bytes totales por segundo</span><span class="sxs-lookup"><span data-stu-id="60db7-197">Bytes Total/sec</span></span> |<span data-ttu-id="60db7-198">Objeto de interfaz de red</span><span class="sxs-lookup"><span data-stu-id="60db7-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a><span data-ttu-id="60db7-199">Crear y agregar la aplicación de tooyour de contadores de rendimiento personalizados</span><span class="sxs-lookup"><span data-stu-id="60db7-199">Create and add custom performance counters tooyour application</span></span>
<span data-ttu-id="60db7-200">Azure tiene toocreate de soporte técnico y modificar contadores de rendimiento personalizados para roles web y roles de trabajo.</span><span class="sxs-lookup"><span data-stu-id="60db7-200">Azure has support toocreate and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="60db7-201">contadores de Hola pueden ser usado tootrack y monitor específica de la aplicación el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="60db7-201">hello counters may be used tootrack and monitor application-specific behavior.</span></span> <span data-ttu-id="60db7-202">Puede crear y eliminar categorías y especificadores de contadores de rendimiento personalizados desde una tarea de inicio, un rol web o un rol de trabajo con permisos elevados.</span><span class="sxs-lookup"><span data-stu-id="60db7-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="60db7-203">Código que realiza cambios en los contadores de rendimiento toocustom debe tener un elevado toorun de permisos.</span><span class="sxs-lookup"><span data-stu-id="60db7-203">Code that makes changes toocustom performance counters must have elevated permissions toorun.</span></span> <span data-ttu-id="60db7-204">Si el código de hello está en un rol web o el rol de trabajo, rol Hola debe incluir la etiqueta hello <Runtime executionContext="elevated" /> Hola ServiceDefinition.csdef de archivos para hello rol tooinitialize correctamente.</span><span class="sxs-lookup"><span data-stu-id="60db7-204">If hello code is in a web role or worker role, hello role must include hello tag <Runtime executionContext="elevated" /> in hello ServiceDefinition.csdef file for hello role tooinitialize properly.</span></span>
>
>

<span data-ttu-id="60db7-205">Puede enviar rendimiento personalizados contador datos tooAzure almacenamiento mediante el agente de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="60db7-205">You can send custom performance counter data tooAzure storage using hello diagnostics agent.</span></span>

<span data-ttu-id="60db7-206">hello que Azure procesa genera datos de contador de rendimiento estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="60db7-206">hello standard performance counter data is generated by hello Azure processes.</span></span> <span data-ttu-id="60db7-207">La aplicación para el rol web o de trabajo debe crear los datos de contadores de rendimiento personalizados.</span><span class="sxs-lookup"><span data-stu-id="60db7-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="60db7-208">Vea [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) para obtener información sobre tipos de Hola de datos que pueden almacenarse en contadores de rendimiento personalizados.</span><span class="sxs-lookup"><span data-stu-id="60db7-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on hello types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="60db7-209">Consulte el [ejemplo PerformanceCounters](http://code.msdn.microsoft.com/azure/) para obtener un ejemplo que crea y establece datos de contadores de rendimiento personalizados en un rol web.</span><span class="sxs-lookup"><span data-stu-id="60db7-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="60db7-210">Almacenamiento y visualización de datos de contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="60db7-210">Store and view performance counter data</span></span>
<span data-ttu-id="60db7-211">Azure almacena en caché los datos de contadores de rendimiento junto con otra información de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="60db7-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="60db7-212">Estos datos están disponibles para la supervisión remota mientras se está ejecutando la instancia de rol de hello con acceso de escritorio remoto tooview herramientas como el Monitor de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="60db7-212">This data is available for remote monitoring while hello role instance is running using remote desktop access tooview tools such as Performance Monitor.</span></span> <span data-ttu-id="60db7-213">toopersist Hola fuera de la instancia de rol de hello, agente de diagnóstico de hello debe transferencia de datos de almacenamiento de hello datos tooAzure.</span><span class="sxs-lookup"><span data-stu-id="60db7-213">toopersist hello data outside of hello role instance, hello diagnostics agent must transfer hello data tooAzure storage.</span></span> <span data-ttu-id="60db7-214">límite de tamaño de Hola de datos del contador de rendimiento de hello en caché se puede configurar en el agente de diagnóstico de hello, o puede ser configurado toobe parte de un límite compartido para todos los datos de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="60db7-214">hello size limit of hello cached performance counter data can be configured in hello diagnostics agent, or it may be configured toobe part of a shared limit for all hello diagnostic data.</span></span> <span data-ttu-id="60db7-215">Para obtener más información acerca de cómo establecer el tamaño del búfer de hello, consulte [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) y [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="60db7-215">For more information about setting hello buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="60db7-216">Vea [almacenar y ver datos de diagnóstico en almacenamiento de Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para obtener información general de configuración de la cuenta de almacenamiento tooa de hello diagnósticos agente tootransfer datos.</span><span class="sxs-lookup"><span data-stu-id="60db7-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up hello diagnostics agent tootransfer data tooa storage account.</span></span>

<span data-ttu-id="60db7-217">Cada instancia de contador de rendimiento configurada se registra a una velocidad de muestreo especificada y se transfieren datos de hello muestreada toohello cuenta de almacenamiento mediante una solicitud de transferencia programada o una solicitud de transferencia a petición.</span><span class="sxs-lookup"><span data-stu-id="60db7-217">Each configured performance counter instance is recorded at a specified sampling rate, and hello sampled data is transferred toohello storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="60db7-218">Se pueden programar transferencias automáticas una vez por minuto.</span><span class="sxs-lookup"><span data-stu-id="60db7-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="60db7-219">Datos del contador de rendimiento transferidos por el agente de diagnóstico de Hola se almacenan en una tabla, WADPerformanceCountersTable, en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="60db7-219">Performance counter data transferred by hello diagnostics agent is stored in a table, WADPerformanceCountersTable, in hello storage account.</span></span> <span data-ttu-id="60db7-220">Se puede acceder a esta tabla y se puede consultar con métodos de API de Almacenamiento de Azure estándar.</span><span class="sxs-lookup"><span data-stu-id="60db7-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="60db7-221">Vea [ejemplo de PerformanceCounters de Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) para obtener un ejemplo de consulta y mostrar los datos del contador de rendimiento de la tabla de WADPerformanceCountersTable Hola.</span><span class="sxs-lookup"><span data-stu-id="60db7-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from hello WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="60db7-222">Dependiendo de la frecuencia de transferencia de agente de diagnóstico de Hola y latencia de la cola, hello datos de contadores de rendimiento más reciente en la cuenta de almacenamiento de hello pueden ser obsoletos varios minutos.</span><span class="sxs-lookup"><span data-stu-id="60db7-222">Depending on hello diagnostics agent transfer frequency and queue latency, hello most recent performance counter data in hello storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="60db7-223">Habilitación de contadores de rendimiento mediante el archivo de configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="60db7-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="60db7-224">Usar hello siguiendo los contadores de rendimiento de tooenable del procedimiento en su aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="60db7-224">Use hello following procedure tooenable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60db7-225">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="60db7-225">Prerequisites</span></span>
<span data-ttu-id="60db7-226">En esta sección se da por supuesto que se haya importado el monitor de diagnóstico de hello en la aplicación y que se han agregado Hola diagnósticos configuración archivo tooyour solución de Visual Studio (diagnostics.wadcfg en SDK 2.4 y por debajo o diagnostics.wadcfgx en SDK 2.5 y versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="60db7-226">This section assumes that you have imported hello Diagnostics monitor into your application and added hello diagnostics configuration file tooyour Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="60db7-227">Consulte los pasos 1 y 2 en [Habilitación de diagnósticos en Azure Cloud Services y en Virtual Machines](cloud-services-dotnet-diagnostics.md)para más información.</span><span class="sxs-lookup"><span data-stu-id="60db7-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="60db7-228">Paso 1: Recopilación y almacenamiento de datos de contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="60db7-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="60db7-229">Después de haber agregado diagnósticos Hola archivo tooyour solución de Visual Studio, puede configurar la recopilación de Hola y el almacenamiento de datos del contador de rendimiento en una aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="60db7-229">After you have added hello diagnostics file tooyour Visual Studio solution, you can configure hello collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="60db7-230">Esto se realiza mediante la adición de archivo de diagnóstico de toohello de contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="60db7-230">This is done by adding performance counters toohello diagnostics file.</span></span> <span data-ttu-id="60db7-231">Datos de diagnóstico, incluidos los contadores de rendimiento, se recopilan primero en la instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="60db7-231">Diagnostics data, including performance counters, is first collected on hello instance.</span></span> <span data-ttu-id="60db7-232">datos de Hello están persistente toohello WADPerformanceCountersTable tabla Hola servicio tabla de Azure, por lo que tendrá que también necesita toospecify Hola cuenta de almacenamiento en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="60db7-232">hello data is then persisted toohello WADPerformanceCountersTable table in hello Azure Table service, so you will also need toospecify hello storage account in your application.</span></span> <span data-ttu-id="60db7-233">Si va a probar la aplicación localmente en hello emulador de proceso, también puede almacenar datos de diagnóstico localmente en hello emulador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60db7-233">If you're testing your application locally in hello Compute Emulator, you can also store diagnostics data locally in hello Storage Emulator.</span></span> <span data-ttu-id="60db7-234">Antes de almacenar datos de diagnóstico, debe ir primero toohello [portal de Azure](http://portal.azure.com/) y crear una cuenta de almacenamiento clásico.</span><span class="sxs-lookup"><span data-stu-id="60db7-234">Before you store diagnostics data, you must first go toohello [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="60db7-235">Una práctica recomendada es toolocate su cuenta de almacenamiento en Hola la misma ubicación geográfica que la aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="60db7-235">A best practice is toolocate your storage account in hello same geo-location as your Azure application.</span></span> <span data-ttu-id="60db7-236">Por mantener Hola cuenta de aplicación y el almacenamiento de Azure están en Hola misma ubicación geográfica, evitar pagar costos externos de ancho de banda y reducir la latencia.</span><span class="sxs-lookup"><span data-stu-id="60db7-236">By keeping hello Azure application and storage account are in hello same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-toohello-diagnostics-file"></a><span data-ttu-id="60db7-237">Agregar archivo de diagnóstico de toohello de contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="60db7-237">Add performance counters toohello diagnostics file</span></span>
<span data-ttu-id="60db7-238">Hay muchos contadores que puede usar.</span><span class="sxs-lookup"><span data-stu-id="60db7-238">There are many counters you can use.</span></span> <span data-ttu-id="60db7-239">Hello en el ejemplo siguiente se muestra varios contadores de rendimiento que se recomiendan para web y la supervisión del rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="60db7-239">hello following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="60db7-240">Abrir el archivo de diagnóstico de hello (diagnostics.wadcfg en SDK 2.4 y anteriores o diagnostics.wadcfgx en SDK 2.5 y versiones posteriores) y agregue Hola siguiente toohello DiagnosticMonitorConfiguration elemento:</span><span class="sxs-lookup"><span data-stu-id="60db7-240">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="60db7-241">atributo de bufferQuotaInMB Hello, que especifica la cantidad máxima de Hola de almacenamiento del sistema de archivos que está disponible para el tipo de colección de datos de hello (registros de Azure, los registros de IIS, etcetera).</span><span class="sxs-lookup"><span data-stu-id="60db7-241">hello bufferQuotaInMB attribute, which specifies hello maximum amount of file system storage that is available for hello data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="60db7-242">Hola predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="60db7-242">hello default is 0.</span></span> <span data-ttu-id="60db7-243">Cuando se alcanza la cuota de hello, se eliminan datos más antiguos de Hola a medida que se agregan nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="60db7-243">When hello quota is reached, hello oldest data is deleted as new data is added.</span></span> <span data-ttu-id="60db7-244">suma de Hola de todas las propiedades de hello bufferQuotaInMB debe ser mayor que valor Hola del atributo de OverallQuotaInMB Hola.</span><span class="sxs-lookup"><span data-stu-id="60db7-244">hello sum of all hello bufferQuotaInMB properties must be greater than hello value of hello OverallQuotaInMB attribute.</span></span> <span data-ttu-id="60db7-245">Para obtener una explicación más detallada de determinar la cantidad de almacenamiento que se necesitará para Hola de recopilación de datos de diagnóstico, vea Hola sección de instalación de WAD de [prácticas recomendadas para desarrollar aplicaciones de Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="60db7-245">For a more detailed discussion of determining how much storage will be required for hello collection of diagnostics data, see hello Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="60db7-246">atributo de scheduledTransferPeriod Hello, que especifica el intervalo de saludo entre las transferencias programadas de datos, se redondea hacia arriba toohello más cercano de minuto.</span><span class="sxs-lookup"><span data-stu-id="60db7-246">hello scheduledTransferPeriod attribute, which specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span> <span data-ttu-id="60db7-247">Hola en los ejemplos siguientes, se establece tooPT30M (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="60db7-247">In hello following examples, it is set tooPT30M (30 minutes).</span></span> <span data-ttu-id="60db7-248">Hola transferencia tooa período pequeño valor de configuración, como 1 minuto, afectará negativamente al rendimiento de su aplicación en producción, pero puede ser útil para ver los diagnósticos rápidamente cuando se prueban.</span><span class="sxs-lookup"><span data-stu-id="60db7-248">Setting hello transfer period tooa small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="60db7-249">período de transferencia programada de Hello debe ser lo suficientemente pequeño como tooensure que los datos de diagnóstico no se sobrescribe en la instancia de hello, pero lo suficientemente grande como para que no afectará al rendimiento de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="60db7-249">hello scheduled transfer period should be small enough tooensure that diagnostic data is not overwritten on hello instance, but large enough that it will not impact hello performance of your application.</span></span>

<span data-ttu-id="60db7-250">atributo de Hello counterSpecifier especifica toocollect de contador de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="60db7-250">hello counterSpecifier attribute specifies hello performance counter toocollect.</span></span> <span data-ttu-id="60db7-251">atributo de Hello sampleRate especifica tasa de hello en el que el contador de rendimiento de hello debe realizarse el muestreo, en este caso 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="60db7-251">hello sampleRate attribute specifies hello rate at which hello performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="60db7-252">Cuando haya agregado los contadores de rendimiento de Hola que desea toocollect, guarde el archivo de diagnóstico de toohello de cambios.</span><span class="sxs-lookup"><span data-stu-id="60db7-252">Once you've added hello performance counters that you want toocollect, save your changes toohello diagnostics file.</span></span> <span data-ttu-id="60db7-253">A continuación, debe cuenta de almacenamiento de hello toospecify que se almacenarán los datos de diagnóstico de saludo.</span><span class="sxs-lookup"><span data-stu-id="60db7-253">Next, you need toospecify hello storage account that hello diagnostics data will be persisted to.</span></span>

### <a name="specify-hello-storage-account"></a><span data-ttu-id="60db7-254">Especifique la cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="60db7-254">Specify hello storage account</span></span>
<span data-ttu-id="60db7-255">toopersist su tooyour de información de diagnóstico almacenamiento de Azure de la cuenta, debe especificar una cadena de conexión en el archivo de configuración (ServiceConfiguration.cscfg) de servicio.</span><span class="sxs-lookup"><span data-stu-id="60db7-255">toopersist your diagnostics information tooyour Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="60db7-256">Para Azure SDK 2.5, puede especificarse Hola cuenta de almacenamiento en archivo de hello diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="60db7-256">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="60db7-257">Estas instrucciones aplican solo tooAzure SDK 2.4 y versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="60db7-257">These instructions only apply tooAzure SDK 2.4 and below.</span></span> <span data-ttu-id="60db7-258">Para Azure SDK 2.5, puede especificarse Hola cuenta de almacenamiento en archivo de hello diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="60db7-258">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="60db7-259">cadenas de conexión de Hola tooset:</span><span class="sxs-lookup"><span data-stu-id="60db7-259">tooset hello connection strings:</span></span>

1. <span data-ttu-id="60db7-260">Abra el archivo de ServiceConfiguration.Cloud.cscfg de Hola con su editor de texto que prefiera y la cadena de conexión de Hola de conjunto para el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60db7-260">Open hello ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set hello connection string for your storage.</span></span> <span data-ttu-id="60db7-261">Hola *AccountName* y *AccountKey* valores se encuentran en hello portal de Azure en el panel de cuenta de almacenamiento de hello, bajo las teclas de acceso.</span><span class="sxs-lookup"><span data-stu-id="60db7-261">hello *AccountName* and *AccountKey* values are found in hello Azure portal in hello storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="60db7-262">Guarde el archivo de ServiceConfiguration.Cloud.cscfg Hola.</span><span class="sxs-lookup"><span data-stu-id="60db7-262">Save hello ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="60db7-263">Abra el archivo ServiceConfiguration.Local.cscfg de hello y compruebe que UseDevelopmentStorage esté establecido tootrue.</span><span class="sxs-lookup"><span data-stu-id="60db7-263">Open hello ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set tootrue.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="60db7-264">Ahora que se establecen las cadenas de conexión de hello, la aplicación conservará la cuenta de almacenamiento de tooyour de datos de diagnóstico cuando se implementa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="60db7-264">Now that hello connection strings are set, your application will persist diagnostics data tooyour storage account when your application is deployed.</span></span>
4. <span data-ttu-id="60db7-265">Guarde y compile el proyecto y, a continuación, implemente la aplicación.</span><span class="sxs-lookup"><span data-stu-id="60db7-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="60db7-266">Paso 2 (opcional): Creación de contadores de rendimiento personalizados</span><span class="sxs-lookup"><span data-stu-id="60db7-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="60db7-267">Además toohello había definido previamente los contadores de rendimiento, puede agregar que su propio rendimiento personalizados contadores toomonitor roles de web o de trabajo.</span><span class="sxs-lookup"><span data-stu-id="60db7-267">In addition toohello pre-defined performance counters, you can add your own custom performance counters toomonitor web or worker roles.</span></span> <span data-ttu-id="60db7-268">Contadores de rendimiento personalizados pueden comportamientos de específica de la aplicación tootrack y monitor de uso y se puede crear o eliminar en una tarea de inicio, el rol web o el rol de trabajo con permisos elevados.</span><span class="sxs-lookup"><span data-stu-id="60db7-268">Custom performance counters may be used tootrack and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="60db7-269">agente de diagnóstico de Azure Hola actualiza Hola configuración contador de rendimiento desde el archivo .wadcfg de hello un minuto después de iniciar.</span><span class="sxs-lookup"><span data-stu-id="60db7-269">hello Azure diagnostics agent refreshes hello performance counter configuration from hello .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="60db7-270">Si debe crear contadores de rendimiento personalizados en hello OnStart (método) y sus tareas de inicio tarden más de un minuto tooexecute, los contadores de rendimiento personalizados no se habrá creados cuando trate de agente de diagnóstico de Azure de hello tooload ellos.</span><span class="sxs-lookup"><span data-stu-id="60db7-270">If you create custom performance counters in hello OnStart method and your startup tasks take longer than one minute tooexecute, your custom performance counters will not have been created when hello Azure Diagnostics agent tries tooload them.</span></span>  <span data-ttu-id="60db7-271">En este escenario, verá que Azure Diagnostics captura correctamente todos los datos de diagnóstico, excepto los contadores de rendimiento personalizados.</span><span class="sxs-lookup"><span data-stu-id="60db7-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="60db7-272">tooresolve este problema, cree Hola contadores de rendimiento en una tarea de inicio o mover algunas de la tarea de inicio funcionan toohello OnStart (método) después de crear contadores de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="60db7-272">tooresolve this issue, create hello performance counters in a startup task or move some of your startup task work toohello OnStart method after creating hello performance counters.</span></span>

<span data-ttu-id="60db7-273">Lleve a cabo Hola siguiendo los pasos toocreate un rendimiento personalizado simple contador denominado "\MyCustomCounterCategory\MyButton1Counter":</span><span class="sxs-lookup"><span data-stu-id="60db7-273">Perform hello following steps toocreate a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="60db7-274">Abra el archivo de definición de servicio de hello (CSDEF) para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="60db7-274">Open hello service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="60db7-275">Agregue Hola elemento toohello WebRole o WorkerRole elemento tooallow ejecución con privilegios elevados:</span><span class="sxs-lookup"><span data-stu-id="60db7-275">Add hello Runtime element toohello WebRole or WorkerRole element tooallow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="60db7-276">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="60db7-276">Save hello file.</span></span>
4. <span data-ttu-id="60db7-277">Abrir el archivo de diagnóstico de hello (diagnostics.wadcfg en SDK 2.4 y anteriores o diagnostics.wadcfgx en SDK 2.5 y versiones posteriores) y agregue Hola después toohello DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="60db7-277">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="60db7-278">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="60db7-278">Save hello file.</span></span>
6. <span data-ttu-id="60db7-279">Crear categoría de contador de rendimiento personalizados de hello en hello OnStart (método) de su rol, antes de invocar base. OnStart.</span><span class="sxs-lookup"><span data-stu-id="60db7-279">Create hello custom performance counter category in hello OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="60db7-280">Hello ejemplo C# siguiente crea una categoría personalizada, si aún no existe:</span><span class="sxs-lookup"><span data-stu-id="60db7-280">hello following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="60db7-281">Actualizar los contadores de hello dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="60db7-281">Update hello counters within your application.</span></span> <span data-ttu-id="60db7-282">Hola de ejemplo siguiente actualiza un contador de rendimiento personalizado en eventos Button1_Click:</span><span class="sxs-lookup"><span data-stu-id="60db7-282">hello following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="60db7-283">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="60db7-283">Save hello file.</span></span>  

<span data-ttu-id="60db7-284">Monitor de diagnóstico de Azure de hello ahora recopilará datos de contador de rendimiento personalizados.</span><span class="sxs-lookup"><span data-stu-id="60db7-284">Custom performance counter data will now be collected by hello Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="60db7-285">Paso 3: Consulta de datos de contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="60db7-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="60db7-286">Una vez que la aplicación se implementa y ejecuta, se iniciará el monitor de diagnóstico de hello recopilar contadores de rendimiento y conservar ese almacenamiento tooAzure de datos.</span><span class="sxs-lookup"><span data-stu-id="60db7-286">Once your application is deployed and running, hello Diagnostics monitor will begin collecting performance counters and persisting that data tooAzure storage.</span></span> <span data-ttu-id="60db7-287">Usar herramientas como el Explorador de servidores en Visual Studio, [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), o [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) de Cerebrata tooview Hola contadores de rendimiento de datos en hello Tabla WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="60db7-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata tooview hello performance counters data in hello WADPerformanceCountersTable table.</span></span> <span data-ttu-id="60db7-288">Puede consultar mediante programación Hola tabla servicio mediante [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), o [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="60db7-288">You can also programmatically query hello Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="60db7-289">Hola siguiente ejemplo de C# muestra una consulta básica contra la tabla de WADPerformanceCountersTable Hola y guarda el archivo CSV tooa de hello diagnósticos datos.</span><span class="sxs-lookup"><span data-stu-id="60db7-289">hello following C# example shows a basic query against hello WADPerformanceCountersTable table and saves hello diagnostics data tooa CSV file.</span></span> <span data-ttu-id="60db7-290">Una vez que los contadores de rendimiento de Hola se guardan el archivo CSV de tooa, puede usar Hola capacidades de Microsoft Excel o algún otro dato de hello toovisualize de herramienta de creación de gráficos.</span><span class="sxs-lookup"><span data-stu-id="60db7-290">Once hello performance counters are saved tooa CSV file, you can use hello graphing capabilities in Microsoft Excel or some other tool toovisualize hello data.</span></span> <span data-ttu-id="60db7-291">Ser seguro tooadd un tooMicrosoft.WindowsAzure.Storage.dll de referencia, que se incluye en hello Azure SDK para .NET de octubre de 2012 y versiones posterior.</span><span class="sxs-lookup"><span data-stu-id="60db7-291">Be sure tooadd a reference tooMicrosoft.WindowsAzure.Storage.dll, which is included in hello Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="60db7-292">ensamblado de Hello es directorio de programa Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ % toohello instalado.</span><span class="sxs-lookup"><span data-stu-id="60db7-292">hello assembly is installed toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="60db7-293">Las entidades asignan objetos tooC # mediante una clase personalizada derivada de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="60db7-293">Entities map tooC# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="60db7-294">Hello código siguiente define una clase de entidad que representa un contador de rendimiento en hello **WADPerformanceCountersTable** tabla.</span><span class="sxs-lookup"><span data-stu-id="60db7-294">hello following code defines an entity class that represents a performance counter in hello **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="60db7-295">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="60db7-295">Next Steps</span></span>
[<span data-ttu-id="60db7-296">Ver más artículos sobre Diagnósticos de Azure</span><span class="sxs-lookup"><span data-stu-id="60db7-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
