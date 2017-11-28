---
title: "Creación de un servicio de confianza de Azure Service Fabric con C#"
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
ms.openlocfilehash: f93298e6483fd8c9dfda835964aeebd1a430af69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="3b137-103">Creación de su primera aplicación de Reliable Services con estado de Service Fabric en C#</span><span class="sxs-lookup"><span data-stu-id="3b137-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="3b137-104">Aprenda a implementar su primera aplicación de Service Fabric para .NET en Windows en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="3b137-104">Learn how to deploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="3b137-105">Cuando haya terminado, tendrá un clúster local que se ejecuta con una aplicación de servicio de confianza.</span><span class="sxs-lookup"><span data-stu-id="3b137-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b137-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3b137-106">Prerequisites</span></span>

<span data-ttu-id="3b137-107">Antes de comenzar, asegúrese de haber [configurado el entorno de desarrollo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b137-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="3b137-108">Esto incluye la instalación del SDK de Service Fabric SDK y Visual Studio 2017 o 2015.</span><span class="sxs-lookup"><span data-stu-id="3b137-108">This includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="3b137-109">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3b137-109">Create the application</span></span>

<span data-ttu-id="3b137-110">Inicie Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="3b137-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="3b137-111">Creación de un proyecto con `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="3b137-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="3b137-112">En el cuadro de diálogo **Nuevo proyecto**, elija **Nube > Aplicación de Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="3b137-112">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="3b137-113">Asigne el nombre **MyApplication** a la aplicación y presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3b137-113">Name the application **MyApplication** and press **OK**.</span></span>

   
![Cuadro de diálogo de proyecto nuevo en Visual Studio.][1]

<span data-ttu-id="3b137-115">Puede crear cualquier tipo de aplicación de Service Fabric en el cuadro de diálogo siguiente.</span><span class="sxs-lookup"><span data-stu-id="3b137-115">You can create any type of Service Fabric application from the next dialog.</span></span> <span data-ttu-id="3b137-116">Para esta guía de inicio rápido, elija **Servicio con estado**.</span><span class="sxs-lookup"><span data-stu-id="3b137-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="3b137-117">Asigne el nombre **MyStatefulService** al servicio y presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3b137-117">Name the service **MyStatefulService** and press **OK**.</span></span>

![Cuadro de diálogo de servicio nuevo en Visual Studio.][2]


<span data-ttu-id="3b137-119">Visual Studio crea el proyecto de aplicación y el proyecto de servicio con estado y los muestra en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="3b137-119">Visual Studio creates the application project and the stateful service project and displays them in Solution Explorer.</span></span>

![Explorador de soluciones después de la creación de una aplicación con el servicio con estado][3]

<span data-ttu-id="3b137-121">El proyecto de aplicación (**MyApplication**) no contiene código directamente.</span><span class="sxs-lookup"><span data-stu-id="3b137-121">The application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="3b137-122">En su lugar, hace referencia a un conjunto de proyectos de servicio.</span><span class="sxs-lookup"><span data-stu-id="3b137-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="3b137-123">Además, contiene otros tres tipos de contenido:</span><span class="sxs-lookup"><span data-stu-id="3b137-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="3b137-124">**Perfiles de publicación**</span><span class="sxs-lookup"><span data-stu-id="3b137-124">**Publish profiles**</span></span>  
<span data-ttu-id="3b137-125">Perfiles para la implementación en entornos diferentes.</span><span class="sxs-lookup"><span data-stu-id="3b137-125">Profiles for deploying to different environments.</span></span>

* <span data-ttu-id="3b137-126">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="3b137-126">**Scripts**</span></span>  
<span data-ttu-id="3b137-127">Script de PowerShell para implementar o actualizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b137-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="3b137-128">**Definición de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="3b137-128">**Application definition**</span></span>  
<span data-ttu-id="3b137-129">Incluye el archivo ApplicationManifest.xml en *ApplicationPackageRoot* que describe la composición de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b137-129">Includes the ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="3b137-130">Los archivos de parámetros de aplicación asociados están en *ApplicationParameters* y se pueden utilizar para especificar parámetros específicos del entorno.</span><span class="sxs-lookup"><span data-stu-id="3b137-130">Associated application parameter files are under *ApplicationParameters*, which can be used to specify environment-specific parameters.</span></span> <span data-ttu-id="3b137-131">Visual Studio seleccionará un archivo de parámetros de aplicación que se especificó en el perfil de publicación asociado durante la implementación en un entorno concreto.</span><span class="sxs-lookup"><span data-stu-id="3b137-131">Visual Studio selects an application parameter file that's specified in the associated publish profile during deployment to a specific environment.</span></span>
    
<span data-ttu-id="3b137-132">Para obtener información general del contenido del proyecto de servicio, consulte [Introducción a Reliable Services de Microsoft Azure Service Fabric](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="3b137-132">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-the-application"></a><span data-ttu-id="3b137-133">Implemente la aplicación y depúrela</span><span class="sxs-lookup"><span data-stu-id="3b137-133">Deploy and debug the application</span></span>

<span data-ttu-id="3b137-134">Ahora que tiene una aplicación, ejecútela.</span><span class="sxs-lookup"><span data-stu-id="3b137-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="3b137-135">Presione `F5` en Visual Studio para implementar la aplicación, con el fin de depurarla.</span><span class="sxs-lookup"><span data-stu-id="3b137-135">In Visual Studio, press `F5` to deploy the application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="3b137-136">La primera vez que ejecute e implemente la aplicación localmente, Visual Studio creará un clúster local para la depuración.</span><span class="sxs-lookup"><span data-stu-id="3b137-136">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="3b137-137">Esto puede tardar algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="3b137-137">This may take some time.</span></span> <span data-ttu-id="3b137-138">El estado de creación del clúster se muestra en la ventana de salida de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3b137-138">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="3b137-139">Cuando el clúster esté listo, recibirá una notificación de la aplicación de administración de la bandeja de sistema del clúster local que se incluye con el SDK.</span><span class="sxs-lookup"><span data-stu-id="3b137-139">When the cluster is ready, you get a notification from the local cluster system tray manager application included with the SDK.</span></span>
   
![Notificación de bandeja de sistema del clúster local][4]

<span data-ttu-id="3b137-141">Cuando se inicia la aplicación, Visual Studio muestra automáticamente el **visor de eventos de diagnóstico**, donde se pueden ver los resultados del seguimiento del servicio.</span><span class="sxs-lookup"><span data-stu-id="3b137-141">Once the application starts, Visual Studio automatically brings up the **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Visor de eventos de diagnóstico][5]

<span data-ttu-id="3b137-143">La plantilla del servicio con estado que se utilizó muestra simplemente un valor del contador, que se incrementa en el método `RunAsync` de **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="3b137-143">The stateful service template we used simply shows a counter value incrementing in the `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="3b137-144">Expanda uno de los eventos para ver más detalles, incluido el nodo en que se ejecuta el código.</span><span class="sxs-lookup"><span data-stu-id="3b137-144">Expand one of the events to see more details, including the node where the code is running.</span></span> <span data-ttu-id="3b137-145">En este caso, es \_Node\_2, aunque puede que en su equipo sea otro.</span><span class="sxs-lookup"><span data-stu-id="3b137-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Detalle del Visor de eventos de diagnóstico][6]

<span data-ttu-id="3b137-147">El clúster local contiene cinco nodos que se hospedan en una sola máquina.</span><span class="sxs-lookup"><span data-stu-id="3b137-147">The local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="3b137-148">En un entorno de producción, cada nodo se hospeda en una máquina virtual o física distinta.</span><span class="sxs-lookup"><span data-stu-id="3b137-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="3b137-149">Para simular la pérdida de una máquina mientras se ejecuta el depurador de Visual Studio, vamos a desactivar uno de los nodos del clúster local.</span><span class="sxs-lookup"><span data-stu-id="3b137-149">To simulate the loss of a machine while exercising the Visual Studio debugger at the same time, let's take down one of the nodes on the local cluster.</span></span>

<span data-ttu-id="3b137-150">En la ventana del **Explorador de soluciones**, abra **MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="3b137-150">In the **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="3b137-151">Buscar el método `RunAsync` y establezca un punto de interrupción en la primera línea del método.</span><span class="sxs-lookup"><span data-stu-id="3b137-151">Find the `RunAsync` method and set a breakpoint on the first line of the method.</span></span>

![Punto de interrupción en el método RunAsync de servicio con estado][7]

<span data-ttu-id="3b137-153">Para iniciar la herramienta **Service Fabric Explorer**, haga clic con el botón derecho en la aplicación de la bandeja del sistema de la instancia de **Cluster Manager local** y elija **Manage Local Cluster** (Administrar clúster local).</span><span class="sxs-lookup"><span data-stu-id="3b137-153">Launch the **Service Fabric Explorer** tool by right-clicking on the **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Inicie el Explorador de Service Fabric desde el Administrador de clústeres locales][systray-launch-sfx]

<span data-ttu-id="3b137-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) ofrece una representación visual de un clúster.</span><span class="sxs-lookup"><span data-stu-id="3b137-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="3b137-156">Incluye el conjunto de las aplicaciones implementadas en él y el conjunto de nodos físicos que lo componen.</span><span class="sxs-lookup"><span data-stu-id="3b137-156">It includes the set of applications deployed to it and the set of physical nodes that make it up.</span></span>

<span data-ttu-id="3b137-157">En el panel izquierdo, expanda **Clúster > Nodos** y busque el nodo en que se ejecuta el código.</span><span class="sxs-lookup"><span data-stu-id="3b137-157">In the left pane, expand **Cluster > Nodes** and find the node where your code is running.</span></span>

<span data-ttu-id="3b137-158">Haga clic en **Acciones > Desactivar (reiniciar)** para simular un reinicio de la máquina.</span><span class="sxs-lookup"><span data-stu-id="3b137-158">Click **Actions > Deactivate (Restart)** to simulate a machine restarting.</span></span>

![Detener un nodo en el Explorador de Service Fabric][sfx-stop-node]

<span data-ttu-id="3b137-160">Momentáneamente, debería ver que se alcanza el punto de interrupción en Visual Studio cuando el cálculo hacía perfectamente en un nodo se conmuta por error a otro.</span><span class="sxs-lookup"><span data-stu-id="3b137-160">Momentarily, you should see your breakpoint hit in Visual Studio as the computation you were doing on one node seamlessly fails over to another.</span></span>


<span data-ttu-id="3b137-161">A continuación, vuelva al Visor de eventos de diagnóstico y observe los mensajes.</span><span class="sxs-lookup"><span data-stu-id="3b137-161">Next, return to the Diagnostic Events Viewer and observe the messages.</span></span> <span data-ttu-id="3b137-162">El contador no ha dejado de incrementarse, aunque los eventos proceden de otro nodo.</span><span class="sxs-lookup"><span data-stu-id="3b137-162">The counter has continued incrementing, even though the events are actually coming from a different node.</span></span>

![Visor de eventos de diagnóstico después de la conmutación por error][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-the-local-cluster-optional"></a><span data-ttu-id="3b137-164">Limpieza del clúster local (opcional)</span><span class="sxs-lookup"><span data-stu-id="3b137-164">Cleaning up the local cluster (optional)</span></span>

<span data-ttu-id="3b137-165">Recuerde que este clúster local es real.</span><span class="sxs-lookup"><span data-stu-id="3b137-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="3b137-166">La detención del depurador elimina la instancia de la aplicación y anula el registro del tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b137-166">Stopping the debugger removes your application instance and unregisters the application type.</span></span> <span data-ttu-id="3b137-167">No obstante, el clúster se sigue ejecutando en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="3b137-167">However, the cluster continues to run in the background.</span></span> <span data-ttu-id="3b137-168">Una vez que está listo para detener el clúster local, hay un par de opciones.</span><span class="sxs-lookup"><span data-stu-id="3b137-168">When you're ready to stop the local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="3b137-169">Mantener los datos de aplicación y de seguimiento</span><span class="sxs-lookup"><span data-stu-id="3b137-169">Keep application and trace data</span></span>

<span data-ttu-id="3b137-170">Cierre el clúster haciendo clic con el botón derecho en la aplicación de la bandeja del sistema de la instancia de **Cluster Manager local** y seleccione **Stop Local Cluster** (Detener clúster local).</span><span class="sxs-lookup"><span data-stu-id="3b137-170">Shut down the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-the-cluster-and-all-data"></a><span data-ttu-id="3b137-171">Eliminar el clúster y todos los datos</span><span class="sxs-lookup"><span data-stu-id="3b137-171">Delete the cluster and all data</span></span>

<span data-ttu-id="3b137-172">Elimine el clúster haciendo clic con el botón derecho en la aplicación de la bandeja del sistema de la instancia de **Cluster Manager local** y seleccione **Remove Local Cluster** (Quitar clúster local).</span><span class="sxs-lookup"><span data-stu-id="3b137-172">Remove the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="3b137-173">Si elige esta opción, Visual Studio volverá a implementar el clúster la próxima vez que ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3b137-173">If you choose this option, Visual Studio will redeploy the cluster the next time your run the application.</span></span> <span data-ttu-id="3b137-174">Elija esta opción solo si no tiene intención de utilizar el clúster local durante algún tiempo o si necesita reclamar recursos.</span><span class="sxs-lookup"><span data-stu-id="3b137-174">Choose this option if you don't intend to use the local cluster for some time or if you need to reclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b137-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b137-175">Next steps</span></span>
<span data-ttu-id="3b137-176">Más información sobre [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3b137-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
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
