---
title: aaaCreate un servicio confiable de Azure Service Fabric con C#
description: "Creación, implementación y depuración de una aplicación de servicio de confianza integrada en Azure Service Fabric, con Visual Studio."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="9d2d2-103">Creación de su primera aplicación de Reliable Services con estado de Service Fabric en C#</span><span class="sxs-lookup"><span data-stu-id="9d2d2-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="9d2d2-104">Obtenga información acerca de cómo toodeploy su primera aplicación de Service Fabric para .NET en Windows en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="9d2d2-105">Cuando haya terminado, tendrá un clúster local que se ejecuta con una aplicación de servicio de confianza.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d2d2-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9d2d2-106">Prerequisites</span></span>

<span data-ttu-id="9d2d2-107">Antes de comenzar, asegúrese de haber [configurado el entorno de desarrollo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9d2d2-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="9d2d2-108">Esto incluye la instalación de SDK del servicio de Fabric de Hola y 2017 de Visual Studio o 2015.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="9d2d2-109">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="9d2d2-109">Create hello application</span></span>

<span data-ttu-id="9d2d2-110">Inicie Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="9d2d2-111">Creación de un proyecto con `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="9d2d2-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="9d2d2-112">Hola **nuevo proyecto** cuadro de diálogo, elija **en la nube > aplicación de servicio de Fabric**.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="9d2d2-113">Nombre de la aplicación hello **MyApplication** y presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Cuadro de diálogo de proyecto nuevo en Visual Studio.][1]

<span data-ttu-id="9d2d2-115">Puede crear cualquier tipo de aplicación de Service Fabric del cuadro de diálogo siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="9d2d2-116">Para esta guía de inicio rápido, elija **Servicio con estado**.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="9d2d2-117">Nombre de servicio de hello **MyStatefulService** y presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Cuadro de diálogo de servicio nuevo en Visual Studio.][2]


<span data-ttu-id="9d2d2-119">Visual Studio crea el proyecto de aplicación de Hola y un proyecto de servicio con estado de Hola y mostrarlos en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![Explorador de soluciones después de la creación de una aplicación con el servicio con estado][3]

<span data-ttu-id="9d2d2-121">proyecto de aplicación Hola (**MyApplication**) no contiene ningún código directamente.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="9d2d2-122">En su lugar, hace referencia a un conjunto de proyectos de servicio.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="9d2d2-123">Además, contiene otros tres tipos de contenido:</span><span class="sxs-lookup"><span data-stu-id="9d2d2-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="9d2d2-124">**Perfiles de publicación**</span><span class="sxs-lookup"><span data-stu-id="9d2d2-124">**Publish profiles**</span></span>  
<span data-ttu-id="9d2d2-125">Perfiles para implementar entornos a toodifferent.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="9d2d2-126">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="9d2d2-126">**Scripts**</span></span>  
<span data-ttu-id="9d2d2-127">Script de PowerShell para implementar o actualizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="9d2d2-128">**Definición de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="9d2d2-128">**Application definition**</span></span>  
<span data-ttu-id="9d2d2-129">Incluye el archivo de ApplicationManifest.xml hello en *ApplicationPackageRoot* que describe la composición de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="9d2d2-130">Archivos de parámetros de las aplicaciones asociadas están bajo *ApplicationParameters*, que puede ser usado toospecify parámetros específicos del entorno.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="9d2d2-131">Perfil de publicación se seleccionan Visual Studio asociado de un archivo de parámetros de la aplicación que se especifica en Hola durante el entorno de implementación tooa específico.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="9d2d2-132">Para obtener información general del contenido de Hola Hola del proyecto del servicio, consulte [Introducción a servicios de confianza](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="9d2d2-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="9d2d2-133">Implementar y depurar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="9d2d2-133">Deploy and debug hello application</span></span>

<span data-ttu-id="9d2d2-134">Ahora que tiene una aplicación, ejecútela.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="9d2d2-135">En Visual Studio, presione `F5` toodeploy aplicación de hello para la depuración.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="9d2d2-136">Hola la primera vez que se ejecute e implementa aplicación de hello localmente, Visual Studio crea un clúster local para la depuración.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="9d2d2-137">Esto puede tardar algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-137">This may take some time.</span></span> <span data-ttu-id="9d2d2-138">estado de creación de clúster de Hola se muestra en la ventana de salida de Visual Studio de hello.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="9d2d2-139">Cuando esté listo clúster hello, obtendrá una notificación de aplicación Hola clúster local system bandeja manager incluido con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![Notificación de bandeja de sistema del clúster local][4]

<span data-ttu-id="9d2d2-141">Una vez empieza a aplicación Hola, Visual Studio muestra automáticamente hello **Visor de eventos de diagnóstico**, donde puede ver el resultado del seguimiento de los servicios.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Visor de eventos de diagnóstico][5]

<span data-ttu-id="9d2d2-143">Hello plantilla de servicio con estado usamos simplemente muestra un aumento de valor de contador en hello `RunAsync` método **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="9d2d2-144">Expanda una de hello toosee de eventos para obtener más detalles, incluido nodo Hola donde se está ejecutando código de hello.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="9d2d2-145">En este caso, es \_Node\_2, aunque puede que en su equipo sea otro.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Detalle del Visor de eventos de diagnóstico][6]

<span data-ttu-id="9d2d2-147">clúster local de Hello contiene cinco nodos hospedados en un único equipo.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="9d2d2-148">En un entorno de producción, cada nodo se hospeda en una máquina virtual o física distinta.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="9d2d2-149">pérdida de hello toosimulate de una máquina al llevar a cabo Hola Visual Studio del depurador en hello mismo tiempo, vamos a poner sin conexión uno de los nodos de hello en clúster local de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="9d2d2-150">Hola **el Explorador de soluciones** ventana, abra **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="9d2d2-151">Buscar hello `RunAsync` método y establezca un punto de interrupción en la primera línea del método hello de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![Punto de interrupción en el método RunAsync de servicio con estado][7]

<span data-ttu-id="9d2d2-153">Iniciar hello **Service Fabric Explorer** herramienta con el botón secundario en hello **Administrador de clústeres Local** aplicación de bandeja del sistema y elija **administrar clúster Local**.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Inicie el Explorador de Service Fabric desde Hola Administrador de clústeres Local][systray-launch-sfx]

<span data-ttu-id="9d2d2-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) ofrece una representación visual de un clúster.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="9d2d2-156">Incluye conjunto de Hola de las aplicaciones implementadas tooit y Hola de nodos físicos que lo componen.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="9d2d2-157">En el panel izquierdo de hello, expanda **clúster > nodos** y buscar Hola nodo donde se ejecuta el código.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="9d2d2-158">Haga clic en **acciones > desactivar (reiniciar)** toosimulate un reinicio del equipo.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![Detener un nodo en el Explorador de Service Fabric][sfx-stop-node]

<span data-ttu-id="9d2d2-160">En breve, debería ver el punto de interrupción alcanzado en Visual Studio como cálculo Hola que estabas haciendo perfectamente en un nodo conmuta por error tooanother.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="9d2d2-161">A continuación, devolver toohello Visor de eventos de diagnóstico y observe los mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="9d2d2-162">contador de Hello ha ido incremento, incluso si los eventos de hello realmente proceden de un nodo diferente.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![Visor de eventos de diagnóstico después de la conmutación por error][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="9d2d2-164">Limpiar el clúster local de hello (opcional)</span><span class="sxs-lookup"><span data-stu-id="9d2d2-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="9d2d2-165">Recuerde que este clúster local es real.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="9d2d2-166">Detener el depurador de hello quita la instancia de la aplicación y anula el registro de tipo de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="9d2d2-167">Sin embargo, el clúster de hello continúa toorun en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="9d2d2-168">Cuando esté listo toostop Hola local del clúster, hay un par de opciones.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="9d2d2-169">Mantener los datos de aplicación y de seguimiento</span><span class="sxs-lookup"><span data-stu-id="9d2d2-169">Keep application and trace data</span></span>

<span data-ttu-id="9d2d2-170">Apagar clúster Hola con el botón secundario en hello **Administrador de clústeres Local** aplicación de bandeja del sistema y, a continuación, elija **detener clúster Local**.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="9d2d2-171">Eliminar el clúster de Hola y todos los datos</span><span class="sxs-lookup"><span data-stu-id="9d2d2-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="9d2d2-172">Quitar clúster de hello con el botón secundario en hello **Administrador de clústeres Local** aplicación de bandeja del sistema y, a continuación, elija **quitar clúster Local**.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="9d2d2-173">Si elige esta opción, Visual Studio volverá a implementar Hola Hola de clúster siguiente tiempo de aplicación Hola a su ejecución.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="9d2d2-174">Elija esta opción si no tiene la intención de clúster local de toouse Hola durante algún tiempo o si necesita recursos tooreclaim.</span><span class="sxs-lookup"><span data-stu-id="9d2d2-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d2d2-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d2d2-175">Next steps</span></span>
<span data-ttu-id="9d2d2-176">Más información sobre [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9d2d2-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
