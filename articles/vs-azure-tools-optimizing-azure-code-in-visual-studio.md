---
title: "aaaOptimizing código de Azure en Visual Studio | Documentos de Microsoft"
description: "Obtenga información sobre cómo las herramientas de optimización del código de Azure en Visual Studio ayudan a que el código sea más sólido y tenga un mejor rendimiento."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="e27d1-103">Optimización del código de Azure</span><span class="sxs-lookup"><span data-stu-id="e27d1-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="e27d1-104">Al programar aplicaciones que usan Microsoft Azure, hay algunas prácticas de codificación que debe seguir toohelp evitar problemas con la escalabilidad de la aplicación, el comportamiento y el rendimiento en un entorno de nube.</span><span class="sxs-lookup"><span data-stu-id="e27d1-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow toohelp avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="e27d1-105">Microsoft proporciona una herramienta de análisis de código de Azure que reconoce e identifica varios de los problemas que se suelen encontrar y ayuda a resolverlos.</span><span class="sxs-lookup"><span data-stu-id="e27d1-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="e27d1-106">Puede descargar la herramienta de hello en Visual Studio a través de NuGet.</span><span class="sxs-lookup"><span data-stu-id="e27d1-106">You can download hello tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="e27d1-107">Reglas de análisis de código de Azure</span><span class="sxs-lookup"><span data-stu-id="e27d1-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="e27d1-108">herramienta de análisis de código de Azure de Hello usa Hola siguiendo reglas tooautomatically marca el código de Azure cuando encuentra problemas conocidos que influyen en el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="e27d1-108">hello Azure Code Analysis tool uses hello following rules tooautomatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="e27d1-109">Los problemas detectados aparecen como advertencias o errores del compilador.</span><span class="sxs-lookup"><span data-stu-id="e27d1-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="e27d1-110">Código correcciones o sugerencias tooresolve Hola advertencia o error a menudo se proporcionan a través de un icono de bombilla.</span><span class="sxs-lookup"><span data-stu-id="e27d1-110">Code fixes or suggestions tooresolve hello warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="e27d1-111">Evite usar el modo de estado de sesión predeterminado (en proceso)</span><span class="sxs-lookup"><span data-stu-id="e27d1-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-112">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-112">ID</span></span>
<span data-ttu-id="e27d1-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="e27d1-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-114">Descripción</span><span class="sxs-lookup"><span data-stu-id="e27d1-114">Description</span></span>
<span data-ttu-id="e27d1-115">Si utiliza modo de estado de sesión (en proceso) de hello predeterminado para las aplicaciones de nube, puede perder el estado de sesión.</span><span class="sxs-lookup"><span data-stu-id="e27d1-115">If you use hello default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="e27d1-116">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-117">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-117">Reason</span></span>
<span data-ttu-id="e27d1-118">De forma predeterminada, el modo de estado de sesión de hello especificado en el archivo web.config de hello está en proceso.</span><span class="sxs-lookup"><span data-stu-id="e27d1-118">By default, hello session state mode specified in hello web.config file is in-process.</span></span> <span data-ttu-id="e27d1-119">Además, si ninguna entrada especificada en el archivo de configuración de hello, el modo de estado de sesión de hello predeterminado tooin-process.</span><span class="sxs-lookup"><span data-stu-id="e27d1-119">Also, if no entry specified in hello configuration file, hello Session State mode defaults tooin-process.</span></span> <span data-ttu-id="e27d1-120">Hola modo en proceso almacena el estado de sesión en la memoria en el servidor web de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-120">hello in-process mode stores session state in memory on hello web server.</span></span> <span data-ttu-id="e27d1-121">Cuando se reinicia una instancia o una nueva instancia se utiliza para el equilibrio de carga o compatibilidad de conmutación por error, estado de sesión de hello almacenado en memoria en el servidor web de hello no se guarda.</span><span class="sxs-lookup"><span data-stu-id="e27d1-121">When an instance is restarted or a new instance is used for load balancing or failover support, hello session state stored in memory on hello web server isn’t saved.</span></span> <span data-ttu-id="e27d1-122">Esta situación impide que la aplicación hello sea escalable en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-122">This situation prevents hello application from being scalable on hello cloud.</span></span>

<span data-ttu-id="e27d1-123">El estado de sesión ASP.NET es compatible con distintas opciones de almacenamiento para los datos de estado de sesión: InProc, StateServer, SQLServer, personalizado y desactivado.</span><span class="sxs-lookup"><span data-stu-id="e27d1-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="e27d1-124">Se recomienda que utilice datos toohost en modo personalizado en un almacén de estado de sesión externo, como [proveedor de estado de sesión de Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="e27d1-124">It’s recommended that you use Custom mode toohost data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-125">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-125">Solution</span></span>
<span data-ttu-id="e27d1-126">Una solución recomendada es toostore el estado de sesión en un servicio de caché administrado.</span><span class="sxs-lookup"><span data-stu-id="e27d1-126">One recommended solution is toostore session state on a managed cache service.</span></span> <span data-ttu-id="e27d1-127">Obtenga información acerca de cómo toouse [proveedor de estado de sesión de Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore el estado de sesión.</span><span class="sxs-lookup"><span data-stu-id="e27d1-127">Learn how toouse [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore your session state.</span></span> <span data-ttu-id="e27d1-128">Se puede también sesión de almacén de estado en otro lugares tooensure que su aplicación sea escalable en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-128">You can also store session state in other places tooensure your application is scalable on hello cloud.</span></span> <span data-ttu-id="e27d1-129">más información acerca de soluciones alternativas, lea toolearn [modos de estado de sesión](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="e27d1-129">toolearn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="e27d1-130">El método de ejecución no debe ser asincrónico</span><span class="sxs-lookup"><span data-stu-id="e27d1-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-131">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-131">ID</span></span>
<span data-ttu-id="e27d1-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="e27d1-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="e27d1-133">Description</span></span>
<span data-ttu-id="e27d1-134">Crear métodos asincrónicos (como [await](https://msdn.microsoft.com/library/hh156528.aspx)) fuera de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método y, a continuación, llaman a los métodos asincrónicos Hola de [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call hello async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="e27d1-135">Declarar hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) hace que el método asincrónico trabajo Hola rol tooenter un bucle de reinicio.</span><span class="sxs-lookup"><span data-stu-id="e27d1-135">Declaring hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes hello worker role tooenter a restart loop.</span></span>

<span data-ttu-id="e27d1-136">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-137">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-137">Reason</span></span>
<span data-ttu-id="e27d1-138">Llamar a métodos asincrónicos desde hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método provoca el rol de trabajo Hola de toorecycle en tiempo de ejecución de servicio en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-138">Calling async methods inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello cloud service runtime toorecycle hello worker role.</span></span> <span data-ttu-id="e27d1-139">Cuando se inicia un rol de trabajo, toda la ejecución del programa tiene lugar dentro de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="e27d1-139">When a worker role starts, all program execution takes place inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="e27d1-140">Hola existente [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método provoca trabajo hello toorestart de rol.</span><span class="sxs-lookup"><span data-stu-id="e27d1-140">Exiting hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello worker role toorestart.</span></span> <span data-ttu-id="e27d1-141">Cuando en tiempo de ejecución del rol de trabajo de hello alcanza el método asincrónico de hello, distribuye todas las operaciones después de método asincrónico de hello y, a continuación, se devuelve.</span><span class="sxs-lookup"><span data-stu-id="e27d1-141">When hello worker role runtime hits hello async method, it dispatches all operations after hello async method and then returns.</span></span> <span data-ttu-id="e27d1-142">Esto hace que el trabajo de hello tooexit de rol de hello [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método y reiniciar.</span><span class="sxs-lookup"><span data-stu-id="e27d1-142">This causes hello worker role tooexit from hello [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="e27d1-143">En la siguiente iteración de Hola de ejecución, rol de trabajo de hello aciertos de nuevo al método asincrónico hello y se reinicia, haciendo que al trabajo de hello toorecycle de rol también se vuelve.</span><span class="sxs-lookup"><span data-stu-id="e27d1-143">In hello next iteration of execution, hello worker role hits hello async method again and restarts, causing hello worker role toorecycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-144">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-144">Solution</span></span>
<span data-ttu-id="e27d1-145">Coloque todas las operaciones asincrónicas fuera hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="e27d1-145">Place all async operations outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="e27d1-146">A continuación, llame al método asincrónico de hello refactorizado desde dentro de hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método, por ejemplo, .wait de Coredispatcher ().</span><span class="sxs-lookup"><span data-stu-id="e27d1-146">Then, call hello refactored async method from inside hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="e27d1-147">herramienta de análisis de código de Azure de Hello puede ayudarle a solucionar este problema.</span><span class="sxs-lookup"><span data-stu-id="e27d1-147">hello Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="e27d1-148">Hola siguiente fragmento de código muestra hello código para solucionar el problema:</span><span class="sxs-lookup"><span data-stu-id="e27d1-148">hello following code snippet demonstrates hello code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="e27d1-149">Use la autenticación con firma de acceso compartido de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="e27d1-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-150">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-150">ID</span></span>
<span data-ttu-id="e27d1-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="e27d1-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-152">Description</span><span class="sxs-lookup"><span data-stu-id="e27d1-152">Description</span></span>
<span data-ttu-id="e27d1-153">Use SAS (firma de acceso compartido) para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="e27d1-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="e27d1-154">El servicio de control de acceso (ACS) se está desusando para la autenticación de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="e27d1-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="e27d1-155">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-156">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-156">Reason</span></span>
<span data-ttu-id="e27d1-157">Para mejorar la seguridad, Azure Active Directory está sustituyendo la autenticación ACS por la autenticación SAS.</span><span class="sxs-lookup"><span data-stu-id="e27d1-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="e27d1-158">Vea [Azure Active Directory es Hola futuras de ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) para obtener información sobre el plan de transición de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-158">See [Azure Active Directory is hello future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on hello transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-159">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-159">Solution</span></span>
<span data-ttu-id="e27d1-160">Use la autenticación SAS en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e27d1-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="e27d1-161">Hola de ejemplo siguiente muestra cómo toouse una existente tooaccess de token de SAS un servicio de bus de espacio de nombres o entidad.</span><span class="sxs-lookup"><span data-stu-id="e27d1-161">hello following example shows how toouse an existing SAS token tooaccess a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="e27d1-162">Vea Hola siguientes temas para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e27d1-162">See hello following topics for more information.</span></span>

* <span data-ttu-id="e27d1-163">Para obtener información general, consulte [Autenticación con firma de acceso compartido en Bus de servicio](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="e27d1-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="e27d1-164">¿Cómo toouse autenticación de firma de acceso compartido con Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="e27d1-164">How toouse Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="e27d1-165">Para ver un proyecto de ejemplo, consulte [Using Shared Access Signature (SAS) authentication with ServiceBus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="e27d1-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a><span data-ttu-id="e27d1-166">Considere el uso de "bucle de recepción" OnMessage método tooavoid</span><span class="sxs-lookup"><span data-stu-id="e27d1-166">Consider using OnMessage method tooavoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-167">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-167">ID</span></span>
<span data-ttu-id="e27d1-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="e27d1-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="e27d1-169">Description</span></span>
<span data-ttu-id="e27d1-170">tooavoid en un "bucle de recepción," hello llamada **OnMessage** método es la mejor solución para recibir los mensajes de Hola que realiza la llamada **recepción** método.</span><span class="sxs-lookup"><span data-stu-id="e27d1-170">tooavoid going into a "receive loop," calling hello **OnMessage** method is a better solution for receiving messages than calling hello **Receive** method.</span></span> <span data-ttu-id="e27d1-171">Sin embargo, si tiene que utilizar hello **recepción** (método) y especificar un tiempo de espera de servidor no predeterminada, asegúrese de que el tiempo de espera del servidor de hello es superior a un minuto.</span><span class="sxs-lookup"><span data-stu-id="e27d1-171">However, if you must use hello **Receive** method, and you specify a non-default server wait time, make sure hello server wait time is more than one minute.</span></span>

<span data-ttu-id="e27d1-172">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-173">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-173">Reason</span></span>
<span data-ttu-id="e27d1-174">Al llamar a **OnMessage**, cliente hello inicia un suministro de mensajes interno que sondea constantemente Hola cola o suscripción.</span><span class="sxs-lookup"><span data-stu-id="e27d1-174">When calling **OnMessage**, hello client starts an internal message pump that constantly polls hello queue or subscription.</span></span> <span data-ttu-id="e27d1-175">Este suministro de mensajes contiene un bucle infinito que emite una llamada tooreceive mensajes.</span><span class="sxs-lookup"><span data-stu-id="e27d1-175">This message pump contains an infinite loop that issues a call tooreceive messages.</span></span> <span data-ttu-id="e27d1-176">Si se agota el tiempo llamada hello, emite una llamada nueva.</span><span class="sxs-lookup"><span data-stu-id="e27d1-176">If hello call times out, it issues a new call.</span></span> <span data-ttu-id="e27d1-177">intervalo de tiempo de espera de saludo viene determinado por el valor de Hola de hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) propiedad de hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)que se está utilizando.</span><span class="sxs-lookup"><span data-stu-id="e27d1-177">hello timeout interval is determined by hello value of hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="e27d1-178">Hola ventaja de usar **OnMessage** en comparación con demasiado**recepción** es que los usuarios no tengan toomanually sondear en busca de mensajes, controlar excepciones, procesar varios mensajes en paralelo y completar Hola mensajes.</span><span class="sxs-lookup"><span data-stu-id="e27d1-178">hello advantage of using **OnMessage** compared too**Receive** is that users don’t have toomanually poll for messages, handle exceptions, process multiple messages in parallel, and complete hello messages.</span></span>

<span data-ttu-id="e27d1-179">Si se llama a **recepción** sin utilizar su valor predeterminado, ser seguro hello *ServerWaitTime* valor es superior a un minuto.</span><span class="sxs-lookup"><span data-stu-id="e27d1-179">If you call **Receive** without using its default value, be sure hello *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="e27d1-180">Establecer *ServerWaitTime* toomore a un minuto evita que el servidor de Hola se agota el tiempo de esperar a recibir mensajes de bienvenida totalmente.</span><span class="sxs-lookup"><span data-stu-id="e27d1-180">Setting *ServerWaitTime* toomore than one minute prevents hello server from timing out before hello message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-181">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-181">Solution</span></span>
<span data-ttu-id="e27d1-182">Vea Hola siguiendo los ejemplos de código para usos recomendados.</span><span class="sxs-lookup"><span data-stu-id="e27d1-182">Please see hello following code examples for recommended usages.</span></span> <span data-ttu-id="e27d1-183">Para obtener más detalles, consulte [Método QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) y [Método QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="e27d1-184">rendimiento de hello tooimprove de hello infraestructura de mensajería de Azure, vea el modelo de diseño de hello [manual de mensajería asincrónica](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-184">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="e27d1-185">Hello siguiente es un ejemplo del uso de **OnMessage** tooreceive mensajes.</span><span class="sxs-lookup"><span data-stu-id="e27d1-185">hello following is an example of using **OnMessage** tooreceive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

<span data-ttu-id="e27d1-186">Hello siguiente es un ejemplo del uso de **recepción** con servidor de saludo predeterminado de tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="e27d1-186">hello following is an example of using **Receive** with hello default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="e27d1-187">Hello siguiente es un ejemplo del uso de **recepción** con un servidor de tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="e27d1-187">hello following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="e27d1-188">Considere usar los métodos asincrónicos de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="e27d1-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-189">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-189">ID</span></span>
<span data-ttu-id="e27d1-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="e27d1-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-191">Descripción</span><span class="sxs-lookup"><span data-stu-id="e27d1-191">Description</span></span>
<span data-ttu-id="e27d1-192">Utilice el rendimiento de tooimprove de métodos de Bus de servicio asincrónica con mensajería asíncrona.</span><span class="sxs-lookup"><span data-stu-id="e27d1-192">Use asynchronous Service Bus methods tooimprove performance with brokered messaging.</span></span>

<span data-ttu-id="e27d1-193">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-194">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-194">Reason</span></span>
<span data-ttu-id="e27d1-195">Usar métodos asincrónicos permite la simultaneidad de programas de aplicación porque ejecutar cada llamada no bloquea el subproceso principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block hello main thread.</span></span> <span data-ttu-id="e27d1-196">Cuando se usan los métodos de mensajería de Bus de servicio, realizar una operación (enviar, recibir, eliminar, etc.) lleva tiempo.</span><span class="sxs-lookup"><span data-stu-id="e27d1-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="e27d1-197">Este tiempo incluye el procesamiento de Hola de operación de Hola por hello servicio de Bus de servicio en la latencia de toohello de adición de solicitud de Hola y respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-197">This time includes hello processing of hello operation by hello Service Bus service in addition toohello latency of hello request and hello reply.</span></span> <span data-ttu-id="e27d1-198">número de hello tooincrease de operaciones por tiempo, las operaciones deberán ejecutarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="e27d1-198">tooincrease hello number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="e27d1-199">Para obtener más información, consulte demasiado[prácticas recomendadas para rendimiento mejoras utilizando Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-199">For more information please refer too[Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-200">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-200">Solution</span></span>
<span data-ttu-id="e27d1-201">Vea [clase QueueClient (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) para obtener información acerca de cómo toouse Hola recomienda método asincrónico.</span><span class="sxs-lookup"><span data-stu-id="e27d1-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how toouse hello recommended asynchronous method.</span></span>

<span data-ttu-id="e27d1-202">rendimiento de hello tooimprove de hello infraestructura de mensajería de Azure, vea el modelo de diseño de hello [manual de mensajería asincrónica](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-202">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="e27d1-203">Considere crear particiones de temas y colas de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="e27d1-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-204">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-204">ID</span></span>
<span data-ttu-id="e27d1-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="e27d1-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-206">Description</span><span class="sxs-lookup"><span data-stu-id="e27d1-206">Description</span></span>
<span data-ttu-id="e27d1-207">Partición de temas y colas de Bus de servicio para mejorar el rendimiento de la mensajería de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="e27d1-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="e27d1-208">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-209">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-209">Reason</span></span>
<span data-ttu-id="e27d1-210">La partición de temas y colas de Bus de servicio aumenta la disponibilidad de rendimiento y el servicio de rendimiento porque hello el rendimiento global de una cola o tema particionado es ya no está limitado por hello rendimiento de un solo agente de mensajes o almacén de mensajería.</span><span class="sxs-lookup"><span data-stu-id="e27d1-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="e27d1-211">Además, una interrupción temporal de un almacén de mensajería no hace que una cola o tema particionado deje de estar disponible.</span><span class="sxs-lookup"><span data-stu-id="e27d1-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="e27d1-212">Para obtener más información, consulte [Particionamiento de entidades de mensajería](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-213">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-213">Solution</span></span>
<span data-ttu-id="e27d1-214">Hola código fragmento siguiente muestra cómo toopartition entidades de mensajería.</span><span class="sxs-lookup"><span data-stu-id="e27d1-214">hello following code snippet shows how toopartition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="e27d1-215">Para obtener más información, vea [temas y colas de Bus de servicio con particiones | Blog de Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) y extraer del repositorio hello [cola con particiones de Microsoft Azure Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e27d1-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out hello [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="e27d1-216">No establezca SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="e27d1-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-217">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-217">ID</span></span>
<span data-ttu-id="e27d1-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="e27d1-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-219">Descripción</span><span class="sxs-lookup"><span data-stu-id="e27d1-219">Description</span></span>
<span data-ttu-id="e27d1-220">Debe evitar el uso de SharedAccessStartTimeset toohello tooimmediately iniciar Hola directiva de acceso compartido de hora actual.</span><span class="sxs-lookup"><span data-stu-id="e27d1-220">You should avoid using SharedAccessStartTimeset toohello current time tooimmediately start hello Shared Access policy.</span></span> <span data-ttu-id="e27d1-221">Solo necesita tooset esta propiedad si desea que Directiva de acceso compartido de hello toostart en un momento posterior.</span><span class="sxs-lookup"><span data-stu-id="e27d1-221">You only need tooset this property if you want toostart hello Shared Access policy at a later time.</span></span>

<span data-ttu-id="e27d1-222">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-223">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-223">Reason</span></span>
<span data-ttu-id="e27d1-224">La sincronización de relojes provoca una ligera diferencia de tiempo entre los centros de datos.</span><span class="sxs-lookup"><span data-stu-id="e27d1-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="e27d1-225">Por ejemplo, puede pensar hora de inicio de Hola de configuración de una directiva SAS de almacenamiento como hello hora actual mediante el uso de DateTime.Now o un método similar hará que efecto de hello SAS directiva tootake inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="e27d1-225">For example, you would logically think setting hello start time of a storage SAS policy as hello current time by using DateTime.Now or a similar method will cause hello SAS policy tootake effect immediately.</span></span> <span data-ttu-id="e27d1-226">Sin embargo, Hola ligera diferencia de tiempo entre los centros de datos puede causar problemas con este ya que algunas veces de centro de datos pueden ser ligeramente posteriores a la hora de inicio de hello, mientras que otros pueden ir adelantados.</span><span class="sxs-lookup"><span data-stu-id="e27d1-226">However, hello slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than hello start time, while others ahead of it.</span></span> <span data-ttu-id="e27d1-227">Como resultado, Hola directiva SAS puede expirar rápidamente (o incluso inmediatamente) si se establece demasiado corta duración de la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-227">As a result, hello SAS policy can expire quickly (or even immediately) if hello policy lifetime is set too short.</span></span>

<span data-ttu-id="e27d1-228">Para obtener instrucciones sobre cómo utilizar la firma de acceso compartido en almacenamiento de Azure, vea [tabla Introducción a SAS (firma de acceso compartido), colas SAS y actualización tooBlob SAS - Blog del equipo de almacenamiento de Microsoft Azure - Blogs de MSDN de inicio - sitio](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-229">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-229">Solution</span></span>
<span data-ttu-id="e27d1-230">Quite la instrucción de Hola que establece la hora de inicio de Hola de directiva de acceso de hello compartido.</span><span class="sxs-lookup"><span data-stu-id="e27d1-230">Remove hello statement that sets hello start time of hello shared access policy.</span></span> <span data-ttu-id="e27d1-231">herramienta de análisis de código de Azure de Hello proporciona una corrección para este problema.</span><span class="sxs-lookup"><span data-stu-id="e27d1-231">hello Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="e27d1-232">Para obtener más información sobre la administración de seguridad, vea el modelo de diseño de hello [patrón de clave Valet](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-232">For more information on security management, please see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="e27d1-233">Hola siguiente fragmento de código muestra hello código para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="e27d1-233">hello following code snippet demonstrates hello code fix for this issue.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="e27d1-234">El tiempo de expiración de la directiva de acceso compartido debe ser superior a cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="e27d1-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-235">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-235">ID</span></span>
<span data-ttu-id="e27d1-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="e27d1-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-237">Descripción</span><span class="sxs-lookup"><span data-stu-id="e27d1-237">Description</span></span>
<span data-ttu-id="e27d1-238">Puede haber hasta cinco minutos de diferencia en los relojes entre los centros de datos en diferentes ubicaciones debido a condición de tooa conocida como "desplazamiento del reloj."</span><span class="sxs-lookup"><span data-stu-id="e27d1-238">There can be as much as a five minute difference in clocks among datacenters at different locations due tooa condition known as "clock skew."</span></span> <span data-ttu-id="e27d1-239">token de directiva SAS tooprevent Hola expiren antes de lo planeado, establezca toobe de tiempo de expiración de hello más de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="e27d1-239">tooprevent hello SAS policy token from expiring earlier than planned, set hello expiry time toobe more than five minutes.</span></span>

<span data-ttu-id="e27d1-240">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-241">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-241">Reason</span></span>
<span data-ttu-id="e27d1-242">Los centros de datos en diferentes ubicaciones alrededor de Hola a todos para sincronizar una señal de reloj.</span><span class="sxs-lookup"><span data-stu-id="e27d1-242">Datacenters at different locations around hello world synchronize by a clock signal.</span></span> <span data-ttu-id="e27d1-243">Dado que requiere tiempo para las ubicaciones de toodifferent de tootravel de señal de reloj, puede haber una variación de tiempo entre los centros de datos en distintas ubicaciones geográficas aunque supuestamente todo está sincronizado.</span><span class="sxs-lookup"><span data-stu-id="e27d1-243">Because it takes time for clock signal tootravel toodifferent locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="e27d1-244">Esta diferencia de tiempo puede afectar al acceso compartido directiva inicio tiempo y la expiración de intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="e27d1-244">This time difference can affect hello Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="e27d1-245">Por lo tanto, tooensure directiva de acceso compartido surte efecto inmediatamente, sin especificar hora de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-245">Therefore, tooensure Shared Access policy takes effect immediately, don’t specify hello start time.</span></span> <span data-ttu-id="e27d1-246">Además, asegúrese de tiempo de expiración de hello es mayor que el tiempo de espera de 5 minutos tooprevent temprano.</span><span class="sxs-lookup"><span data-stu-id="e27d1-246">In addition, make sure hello expiration time is more than 5 minutes tooprevent early timeout.</span></span>

<span data-ttu-id="e27d1-247">Para obtener más información acerca del uso de firma de acceso compartido en almacenamiento de Azure, consulte [tabla Introducción a SAS (firma de acceso compartido), colas SAS y actualización tooBlob SAS - Blog del equipo de almacenamiento de Microsoft Azure - Blogs de MSDN de inicio - sitio](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-248">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-248">Solution</span></span>
<span data-ttu-id="e27d1-249">Para obtener más información sobre la administración de seguridad, vea el modelo de diseño de hello [patrón de clave Valet](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-249">For more information on security management, see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="e27d1-250">Hola aquí te mostramos un ejemplo de no especificar una hora de inicio de la directiva de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="e27d1-250">hello following is an example of not specifying a Shared Access policy start time.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="e27d1-251">Hola aquí te mostramos un ejemplo de especificar una hora de inicio de la directiva de acceso compartido con una duración de expiración de la directiva superior a cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="e27d1-251">hello following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="e27d1-252">Para obtener más información, consulte [Crear y usar una firma de acceso compartido](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="e27d1-253">Use CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="e27d1-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-254">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-254">ID</span></span>
<span data-ttu-id="e27d1-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="e27d1-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-256">Descripción</span><span class="sxs-lookup"><span data-stu-id="e27d1-256">Description</span></span>
<span data-ttu-id="e27d1-257">Con hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) clase para los proyectos como sitio Web de Azure y servicios móviles de Azure no presentan problemas de tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="e27d1-257">Using hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="e27d1-258">Como práctica recomendada, sin embargo, es una nube de buena idea toouse[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) como una manera unificada de administración de configuraciones para todas las aplicaciones de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="e27d1-258">As a best practice, however, it's a good idea toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="e27d1-259">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-260">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-260">Reason</span></span>
<span data-ttu-id="e27d1-261">CloudConfigurationManager lee el entorno de aplicación de hello configuración archivo toohello adecuado.</span><span class="sxs-lookup"><span data-stu-id="e27d1-261">CloudConfigurationManager reads hello configuration file appropriate toohello application environment.</span></span>

[<span data-ttu-id="e27d1-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="e27d1-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="e27d1-263">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-263">Solution</span></span>
<span data-ttu-id="e27d1-264">Refactorizar el saludo de toouse código [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-264">Refactor your code toouse hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="e27d1-265">Herramienta de análisis de código de Azure de hello proporciona un código para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="e27d1-265">A code fix for this issue is provided by hello Azure Code Analysis tool.</span></span>

<span data-ttu-id="e27d1-266">Hola siguiente fragmento de código muestra hello código para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="e27d1-266">hello following code snippet demonstrates hello code fix for this issue.</span></span> <span data-ttu-id="e27d1-267">Sustituya</span><span class="sxs-lookup"><span data-stu-id="e27d1-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="e27d1-268">por</span><span class="sxs-lookup"><span data-stu-id="e27d1-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="e27d1-269">Este es un ejemplo de cómo toostore Hola de configuración en un archivo App.config o Web.config.</span><span class="sxs-lookup"><span data-stu-id="e27d1-269">Here's an example of how toostore hello configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="e27d1-270">Agregue Hola configuración toohello appSettings sección Hola del archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="e27d1-270">Add hello settings toohello appSettings section of hello configuration file.</span></span> <span data-ttu-id="e27d1-271">Hola aquí te mostramos archivo Web.config de hello para el ejemplo de código anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-271">hello following is hello Web.config file for hello previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="e27d1-272">Evite usar cadenas de conexión codificadas de forma rígida</span><span class="sxs-lookup"><span data-stu-id="e27d1-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-273">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-273">ID</span></span>
<span data-ttu-id="e27d1-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="e27d1-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-275">Descripción</span><span class="sxs-lookup"><span data-stu-id="e27d1-275">Description</span></span>
<span data-ttu-id="e27d1-276">Si utiliza cadenas de conexión codificadas de forma rígida y necesita tooupdate usarlas más adelante, podrá tiene código fuente de toomake cambios tooyour y vuelva a compilar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e27d1-276">If you use hard-coded connection strings and you need tooupdate them later, you’ll have toomake changes tooyour source code and recompile hello application.</span></span> <span data-ttu-id="e27d1-277">Sin embargo, si almacena las cadenas de conexión en un archivo de configuración, puede cambiarlos más adelante simplemente actualizando el archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating hello configuration file.</span></span>

<span data-ttu-id="e27d1-278">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-279">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-279">Reason</span></span>
<span data-ttu-id="e27d1-280">Codificar las cadenas de conexión es una práctica incorrecta porque presenta problemas cuando las cadenas de conexión necesitan toobe cambiar rápidamente.</span><span class="sxs-lookup"><span data-stu-id="e27d1-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need toobe changed quickly.</span></span> <span data-ttu-id="e27d1-281">Además, si el proyecto de hello necesita toobe activado toosource control, las cadenas de conexión codificadas de forma rígida introducen vulnerabilidades de seguridad, puesto que las cadenas de hello pueden verse en el código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-281">In addition, if hello project needs toobe checked in toosource control, hard-coded connection strings introduce security vulnerabilities since hello strings can be viewed in hello source code.</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-282">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-282">Solution</span></span>
<span data-ttu-id="e27d1-283">Almacenar cadenas de conexión en archivos de configuración de Hola o entornos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e27d1-283">Store connection strings in hello configuration files or Azure environments.</span></span>

* <span data-ttu-id="e27d1-284">Para aplicaciones independientes, utilice la configuración de la cadena de conexión de app.config toostore.</span><span class="sxs-lookup"><span data-stu-id="e27d1-284">For standalone applications, use app.config toostore connection string settings.</span></span>
* <span data-ttu-id="e27d1-285">Para las aplicaciones web hospedadas en IIS, utilice las cadenas de conexión de web.config toostore.</span><span class="sxs-lookup"><span data-stu-id="e27d1-285">For IIS-hosted web applications, use web.config toostore connection strings.</span></span>
* <span data-ttu-id="e27d1-286">Para las aplicaciones ASP.NET vNext, use configuration.json toostore las cadenas de conexión.</span><span class="sxs-lookup"><span data-stu-id="e27d1-286">For ASP.NET vNext applications, use configuration.json toostore connection strings.</span></span>

<span data-ttu-id="e27d1-287">Para obtener información sobre el uso de archivos de configuración como web.config o app.config, consulte [Directrices de configuración web de ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="e27d1-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="e27d1-288">Para obtener información sobre cómo funcionan las variables de entorno de Azure, consulte [Sitios web Microsoft Azure: cómo funcionan las cadenas de aplicaciones y las cadenas de conexión](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="e27d1-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="e27d1-289">Para obtener información sobre cómo almacenar la cadena de conexión en el control de código fuente, consulte [Evitar colocar información confidencial, como cadenas de conexión, en archivos que se almacenan en el repositorio de código fuente.](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)</span><span class="sxs-lookup"><span data-stu-id="e27d1-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="e27d1-290">Uso del archivo de configuración de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e27d1-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-291">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-291">ID</span></span>
<span data-ttu-id="e27d1-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="e27d1-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-293">Descripción</span><span class="sxs-lookup"><span data-stu-id="e27d1-293">Description</span></span>
<span data-ttu-id="e27d1-294">En lugar de configurar la configuración de diagnóstico en el código como mediante el uso de Hola Microsoft.WindowsAzure.Diagnostics API de programación, debe configurar la configuración de diagnóstico en el archivo diagnostics.wadcfg de hello.</span><span class="sxs-lookup"><span data-stu-id="e27d1-294">Instead of configuring diagnostics settings in your code such as by using hello Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in hello diagnostics.wadcfg file.</span></span> <span data-ttu-id="e27d1-295">(O bien, diagnostics.wadcfgx si usa Azure SDK 2.5).</span><span class="sxs-lookup"><span data-stu-id="e27d1-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="e27d1-296">Al hacerlo, puede cambiar la configuración de diagnóstico sin tener toorecompile el código.</span><span class="sxs-lookup"><span data-stu-id="e27d1-296">By doing this, you can change diagnostics settings without having toorecompile your code.</span></span>

<span data-ttu-id="e27d1-297">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-298">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-298">Reason</span></span>
<span data-ttu-id="e27d1-299">Antes de Azure SDK 2.5 (que usa el diagnóstico de Azure 1.3), diagnósticos de Azure (WAD) puede configurarse mediante varios métodos diferentes: agregar toohello blob de configuración en el almacenamiento, utilizando código imperativo, configuración declarativa u Hola default configuración.</span><span class="sxs-lookup"><span data-stu-id="e27d1-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it toohello configuration blob in storage, by using imperative code, declarative configuration, or hello default configuration.</span></span> <span data-ttu-id="e27d1-300">Sin embargo, Hola preferida forma tooconfigure diagnósticos son toouse un archivo de configuración XML (diagnostics.wadcfg o diagnositcs.wadcfgx para 2.5 SDK y versiones posteriores) en el proyecto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-300">However, hello preferred way tooconfigure diagnostics is toouse an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in hello application project.</span></span> <span data-ttu-id="e27d1-301">En este enfoque, archivo diagnostics.wadcfg de hello completamente define la configuración de Hola y se puede actualizar y volver a implementar con total.</span><span class="sxs-lookup"><span data-stu-id="e27d1-301">In this approach, hello diagnostics.wadcfg file completely defines hello configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="e27d1-302">Combina el uso de Hola Hola diagnostics.wadcfg del archivo de configuración con hello métodos de programación de establecimiento de configuraciones mediante el uso de hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)o [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) las clases pueden provocar tooconfusion.</span><span class="sxs-lookup"><span data-stu-id="e27d1-302">Mixing hello use of hello diagnostics.wadcfg configuration file with hello programmatic methods of setting configurations by using hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead tooconfusion.</span></span> <span data-ttu-id="e27d1-303">Consulte [Inicializar o cambiar la configuración de Diagnósticos de Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e27d1-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="e27d1-304">A partir de WAD 1.3 (incluido con Azure SDK 2.5), ya no es diagnósticos de posibles toouse código tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="e27d1-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible toouse code tooconfigure diagnostics.</span></span> <span data-ttu-id="e27d1-305">Como resultado, solo puede proporcionar configuración de hello al aplicar o actualizar la extensión de diagnósticos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-305">As a result, you can only provide hello configuration when applying or updating hello diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-306">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-306">Solution</span></span>
<span data-ttu-id="e27d1-307">Utilice Hola diagnósticos configuración diseñador toomove configuración de diagnóstico toohello archivo configuración de diagnósticos (diagnositcs.wadcfg o diagnositcs.wadcfgx para 2.5 SDK y versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="e27d1-307">Use hello diagnostics configuration designer toomove diagnostic settings toohello diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="e27d1-308">También se recomienda que instale [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) y usar la característica de diagnóstico más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use hello latest diagnostics feature.</span></span>

1. <span data-ttu-id="e27d1-309">En hello menú contextual Hola rol que desea tooconfigure, elija Propiedades y, a continuación, elija la ficha de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-309">On hello shortcut menu for hello role that you want tooconfigure, choose Properties, and then choose hello Configuration tab.</span></span>
2. <span data-ttu-id="e27d1-310">Hola **diagnósticos** sección, asegúrese de que ese hello **habilitar diagnósticos** casilla está activada.</span><span class="sxs-lookup"><span data-stu-id="e27d1-310">In hello **Diagnostics** section, make sure that hello **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="e27d1-311">Elija hello **configurar** botón.</span><span class="sxs-lookup"><span data-stu-id="e27d1-311">Choose hello **Configure** button.</span></span>

   ![Obtener acceso a la opción de habilitar diagnósticos de Hola](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="e27d1-313">Consulte [Configuración de los diagnósticos para los servicios en la nube y las máquinas virtuales de Azure](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e27d1-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="e27d1-314">Evite declarar objetos DbContext como estáticos</span><span class="sxs-lookup"><span data-stu-id="e27d1-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="e27d1-315">ID</span><span class="sxs-lookup"><span data-stu-id="e27d1-315">ID</span></span>
<span data-ttu-id="e27d1-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="e27d1-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="e27d1-317">Descripción</span><span class="sxs-lookup"><span data-stu-id="e27d1-317">Description</span></span>
<span data-ttu-id="e27d1-318">memoria de toosave, evite declarar objetos DBContext como estáticos.</span><span class="sxs-lookup"><span data-stu-id="e27d1-318">toosave memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="e27d1-319">Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e27d1-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e27d1-320">Motivo</span><span class="sxs-lookup"><span data-stu-id="e27d1-320">Reason</span></span>
<span data-ttu-id="e27d1-321">Objetos de DBContext contienen Hola resultados de la consulta de cada llamada.</span><span class="sxs-lookup"><span data-stu-id="e27d1-321">DBContext objects hold hello query results from each call.</span></span> <span data-ttu-id="e27d1-322">Los objetos estáticos de DBContext no se eliminan hasta que se descarga el dominio de aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e27d1-322">Static DBContext objects are not disposed until hello application domain is unloaded.</span></span> <span data-ttu-id="e27d1-323">Por lo tanto, un objeto DBContext estático puede consumir grandes cantidades de memoria.</span><span class="sxs-lookup"><span data-stu-id="e27d1-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="e27d1-324">Solución</span><span class="sxs-lookup"><span data-stu-id="e27d1-324">Solution</span></span>
<span data-ttu-id="e27d1-325">Declare DBContext como un campo de instancia variable o no estático, úselo para una tarea y, luego, deje que se elimine después de usarlo.</span><span class="sxs-lookup"><span data-stu-id="e27d1-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="e27d1-326">Hola después de la clase de controlador MVC de ejemplo muestra cómo toouse Hola objeto DBContext.</span><span class="sxs-lookup"><span data-stu-id="e27d1-326">hello following example MVC controller class shows how toouse hello DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="e27d1-327">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e27d1-327">Next steps</span></span>
<span data-ttu-id="e27d1-328">toolearn más información acerca de optimización y solución de problemas de aplicaciones de Azure, consulte [solucionar problemas de una aplicación web en el servicio de aplicaciones de Azure con Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="e27d1-328">toolearn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
