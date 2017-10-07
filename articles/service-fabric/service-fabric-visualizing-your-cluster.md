---
title: "aaaVisualizing su clúster mediante el Explorador de Service Fabric | Documentos de Microsoft"
description: "El Explorador de Service Fabric es una herramienta basada en web para inspeccionar y administrar aplicaciones y nodos en la nube en un clúster de Service Fabric de Microsoft Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="87d24-103">Visualización del clúster mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="87d24-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="87d24-104">El Explorador de Service Fabric es una herramienta web para inspeccionar y administrar aplicaciones y nodos en un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="87d24-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="87d24-105">Explorador de Service Fabric se hospeda directamente en clúster de hello, por lo que siempre está disponible, independientemente de donde se está ejecutando el clúster.</span><span class="sxs-lookup"><span data-stu-id="87d24-105">Service Fabric Explorer is hosted directly within hello cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="87d24-106">Tutorial en vídeo</span><span class="sxs-lookup"><span data-stu-id="87d24-106">Video tutorial</span></span>

<span data-ttu-id="87d24-107">toolearn cómo ver toouse Service Fabric Explorer Hola después de vídeo Microsoft Virtual Academy:</span><span class="sxs-lookup"><span data-stu-id="87d24-107">toolearn how toouse Service Fabric Explorer, watch hello following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a><span data-ttu-id="87d24-108">Conectar tooService Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="87d24-108">Connect tooService Fabric Explorer</span></span>
<span data-ttu-id="87d24-109">Si ha seguido las instrucciones de hello demasiado[preparar el entorno de desarrollo](service-fabric-get-started.md), puede iniciar el Explorador de Service Fabric en el clúster local desplazándose toohttp://localhost:19080 / explorador.</span><span class="sxs-lookup"><span data-stu-id="87d24-109">If you have followed hello instructions too[prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating toohttp://localhost:19080/Explorer.</span></span>

## <a name="understand-hello-service-fabric-explorer-layout"></a><span data-ttu-id="87d24-110">Entender el diseño del explorador de Service Fabric Hola</span><span class="sxs-lookup"><span data-stu-id="87d24-110">Understand hello Service Fabric Explorer layout</span></span>
<span data-ttu-id="87d24-111">Puede navegar a través del explorador de Service Fabric mediante árbol Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="87d24-111">You can navigate through Service Fabric Explorer by using hello tree on hello left.</span></span> <span data-ttu-id="87d24-112">En raíz de Hola de árbol de hello, panel de clúster de hello proporciona información general del clúster, incluido un resumen de la aplicación y el estado de nodo.</span><span class="sxs-lookup"><span data-stu-id="87d24-112">At hello root of hello tree, hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Panel de clúster del Explorador de Service Fabric][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a><span data-ttu-id="87d24-114">Ver el diseño del clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="87d24-114">View hello cluster's layout</span></span>
<span data-ttu-id="87d24-115">Los nodos de un clúster de Service Fabric se colocan en una cuadrícula bidimensional de dominios de error y dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="87d24-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="87d24-116">Esta ubicación se asegura de que las aplicaciones siguen estando disponibles en presencia de Hola de errores de hardware y las actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="87d24-116">This placement ensures that your applications remain available in hello presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="87d24-117">Puede ver cómo se diseña el clúster actual hello mediante el mapa de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-117">You can view how hello current cluster is laid out by using hello cluster map.</span></span>

![Mapa de clúster del Explorador de Service Fabric][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="87d24-119">Visualización de aplicaciones y servicios</span><span class="sxs-lookup"><span data-stu-id="87d24-119">View applications and services</span></span>
<span data-ttu-id="87d24-120">clúster de Hello contiene dos subárboles: uno para las aplicaciones y otro para los nodos.</span><span class="sxs-lookup"><span data-stu-id="87d24-120">hello cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="87d24-121">Puede utilizar toonavigate de vista de aplicación Hola a través de la jerarquía lógica de Service Fabric: las aplicaciones, servicios, particiones y réplicas.</span><span class="sxs-lookup"><span data-stu-id="87d24-121">You can use hello application view toonavigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="87d24-122">En el siguiente ejemplo de Hola, Hola aplicación **MyApp** consta de dos servicios, **MyStatefulService** y **WebService**.</span><span class="sxs-lookup"><span data-stu-id="87d24-122">In hello example below, hello application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="87d24-123">Como **MyStatefulService** es un servicio con estado, incluye una partición con una réplica principal y dos réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="87d24-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="87d24-124">Por el contrario, el servicio WebSvcService no tiene estado y contiene una única instancia.</span><span class="sxs-lookup"><span data-stu-id="87d24-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Vista de aplicación del explorador de Service Fabric][sfx-application-tree]

<span data-ttu-id="87d24-126">En cada nivel del árbol de hello, panel principal hello muestra la información pertinente sobre elemento Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-126">At each level of hello tree, hello main pane shows pertinent information about hello item.</span></span> <span data-ttu-id="87d24-127">Por ejemplo, puede ver el estado de mantenimiento de Hola y la versión para un servicio determinado.</span><span class="sxs-lookup"><span data-stu-id="87d24-127">For example, you can see hello health status and version for a particular service.</span></span>

![Panel Essentials del explorador de Service Fabric][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a><span data-ttu-id="87d24-129">Ver los nodos del clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="87d24-129">View hello cluster's nodes</span></span>
<span data-ttu-id="87d24-130">vista de nodo de Hello muestra el diseño físico de Hola de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-130">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="87d24-131">Para un nodo determinado, puede comprobar qué aplicaciones tienen el código implementado en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="87d24-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="87d24-132">Más específicamente, puede ver qué réplicas están en ejecución.</span><span class="sxs-lookup"><span data-stu-id="87d24-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="87d24-133">Acciones</span><span class="sxs-lookup"><span data-stu-id="87d24-133">Actions</span></span>
<span data-ttu-id="87d24-134">Explorador de Service Fabric ofrece una forma rápida tooinvoke acciones en nodos, aplicaciones y servicios en el clúster.</span><span class="sxs-lookup"><span data-stu-id="87d24-134">Service Fabric Explorer offers a quick way tooinvoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="87d24-135">Por ejemplo, toodelete una instancia de la aplicación, elija aplicación hello de árbol de Hola Hola izquierda y, a continuación, elija **acciones** > **eliminar una aplicación**.</span><span class="sxs-lookup"><span data-stu-id="87d24-135">For example, toodelete an application instance, choose hello application from hello tree on hello left, and then choose **Actions** > **Delete Application**.</span></span>

![Eliminación de una aplicación en el explorador de Service Fabric][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="87d24-137">Puede realizar Hola mismas acciones, haga clic en siguiente tooeach elemento de hello puntos suspensivos.</span><span class="sxs-lookup"><span data-stu-id="87d24-137">You can perform hello same actions by clicking hello ellipsis next tooeach element.</span></span>
>
>

<span data-ttu-id="87d24-138">Hello tabla siguiente enumeran las acciones de hello disponibles para cada entidad:</span><span class="sxs-lookup"><span data-stu-id="87d24-138">hello following table lists hello actions available for each entity:</span></span>

| <span data-ttu-id="87d24-139">**Entidad**</span><span class="sxs-lookup"><span data-stu-id="87d24-139">**Entity**</span></span> | <span data-ttu-id="87d24-140">**Acción**</span><span class="sxs-lookup"><span data-stu-id="87d24-140">**Action**</span></span> | <span data-ttu-id="87d24-141">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="87d24-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87d24-142">Tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="87d24-142">Application type</span></span> |<span data-ttu-id="87d24-143">Tipo de anulación de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="87d24-143">Unprovision type</span></span> |<span data-ttu-id="87d24-144">Quita el paquete de aplicación Hola del clúster de hello almacén de imágenes.</span><span class="sxs-lookup"><span data-stu-id="87d24-144">Removes hello application package from hello cluster's image store.</span></span> <span data-ttu-id="87d24-145">Requiere que todas las aplicaciones de ese toobe tipo quitado primero.</span><span class="sxs-lookup"><span data-stu-id="87d24-145">Requires all applications of that type toobe removed first.</span></span> |
| <span data-ttu-id="87d24-146">Application</span><span class="sxs-lookup"><span data-stu-id="87d24-146">Application</span></span> |<span data-ttu-id="87d24-147">Eliminar aplicación</span><span class="sxs-lookup"><span data-stu-id="87d24-147">Delete Application</span></span> |<span data-ttu-id="87d24-148">Eliminar aplicación hello, incluidos todos sus servicios y su estado (si existe).</span><span class="sxs-lookup"><span data-stu-id="87d24-148">Delete hello application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="87d24-149">Servicio</span><span class="sxs-lookup"><span data-stu-id="87d24-149">Service</span></span> |<span data-ttu-id="87d24-150">Eliminar servicio</span><span class="sxs-lookup"><span data-stu-id="87d24-150">Delete Service</span></span> |<span data-ttu-id="87d24-151">Eliminar servicio hello y su estado (si existe).</span><span class="sxs-lookup"><span data-stu-id="87d24-151">Delete hello service and its state (if any).</span></span> |
| <span data-ttu-id="87d24-152">Nodo</span><span class="sxs-lookup"><span data-stu-id="87d24-152">Node</span></span> |<span data-ttu-id="87d24-153">Activar</span><span class="sxs-lookup"><span data-stu-id="87d24-153">Activate</span></span> |<span data-ttu-id="87d24-154">Activación del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-154">Activate hello node.</span></span> |
| <span data-ttu-id="87d24-155">Nodo</span><span class="sxs-lookup"><span data-stu-id="87d24-155">Node</span></span> | <span data-ttu-id="87d24-156">Desactivar (pausa)</span><span class="sxs-lookup"><span data-stu-id="87d24-156">Deactivate (pause)</span></span> | <span data-ttu-id="87d24-157">Pausar el nodo de hello en su estado actual.</span><span class="sxs-lookup"><span data-stu-id="87d24-157">Pause hello node in its current state.</span></span> <span data-ttu-id="87d24-158">Servicios seguirán toorun pero Service Fabric no proactivamente mover nada en o desactivar, a menos que sea necesario tooprevent una interrupción o incoherencia en los datos.</span><span class="sxs-lookup"><span data-stu-id="87d24-158">Services continue toorun but Service Fabric does not proactively move anything onto or off it unless it is required tooprevent an outage or data inconsistency.</span></span> <span data-ttu-id="87d24-159">Esta acción es tooenable normalmente se usan los servicios en un tooensure de nodo específico que no se mueven durante la inspección de depuración.</span><span class="sxs-lookup"><span data-stu-id="87d24-159">This action is typically used tooenable debugging services on a specific node tooensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="87d24-160">Nodo</span><span class="sxs-lookup"><span data-stu-id="87d24-160">Node</span></span> | <span data-ttu-id="87d24-161">Desactivar (reiniciar)</span><span class="sxs-lookup"><span data-stu-id="87d24-161">Deactivate (restart)</span></span> | <span data-ttu-id="87d24-162">Saque todos los servicios de la memoria de un nodo y cierre los servicios persistentes de forma segura.</span><span class="sxs-lookup"><span data-stu-id="87d24-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="87d24-163">Se utiliza normalmente cuando los procesos de host de Hola o máquina necesidad toobe reinicia.</span><span class="sxs-lookup"><span data-stu-id="87d24-163">Typically used when hello host processes or machine need toobe restarted.</span></span> | |
| <span data-ttu-id="87d24-164">Nodo</span><span class="sxs-lookup"><span data-stu-id="87d24-164">Node</span></span> | <span data-ttu-id="87d24-165">Desactivar (quitar datos)</span><span class="sxs-lookup"><span data-stu-id="87d24-165">Deactivate (remove data)</span></span> | <span data-ttu-id="87d24-166">Cerrar todos los servicios que se ejecutan en el nodo de hello después de la creación de réplicas de reserva suficiente.</span><span class="sxs-lookup"><span data-stu-id="87d24-166">Safely close all services running on hello node after building sufficient spare replicas.</span></span> <span data-ttu-id="87d24-167">Se utiliza normalmente cuando un nodo (o al menos su almacenamiento) se está sacando permanentemente de circulación.</span><span class="sxs-lookup"><span data-stu-id="87d24-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="87d24-168">Nodo</span><span class="sxs-lookup"><span data-stu-id="87d24-168">Node</span></span> | <span data-ttu-id="87d24-169">Quitar el estado del nodo</span><span class="sxs-lookup"><span data-stu-id="87d24-169">Remove node state</span></span> | <span data-ttu-id="87d24-170">Quitar información de réplicas de un nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-170">Remove knowledge of a node's replicas from hello cluster.</span></span> <span data-ttu-id="87d24-171">Se utiliza normalmente cuando un nodo con error ya se considera irrecuperable.</span><span class="sxs-lookup"><span data-stu-id="87d24-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="87d24-172">Nodo</span><span class="sxs-lookup"><span data-stu-id="87d24-172">Node</span></span> | <span data-ttu-id="87d24-173">Reiniciar</span><span class="sxs-lookup"><span data-stu-id="87d24-173">Restart</span></span> | <span data-ttu-id="87d24-174">Simular un error de nodo, reinicie el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-174">Simulate a node failure by restarting hello node.</span></span> <span data-ttu-id="87d24-175">Puede encontrar más información [aquí](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="87d24-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="87d24-176">Puesto que muchas acciones son destructivas, es posible que más frecuentes tooconfirm su intención antes de que finalice la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-176">Since many actions are destructive, you may be asked tooconfirm your intent before hello action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="87d24-177">Todas las acciones que pueden realizarse a través del explorador de Service Fabric también pueden realizarse a través de PowerShell o una API de REST, tooenable automatización.</span><span class="sxs-lookup"><span data-stu-id="87d24-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, tooenable automation.</span></span>
>
>

<span data-ttu-id="87d24-178">También puede utilizar instancias de la aplicación de explorador de Service Fabric toocreate para un tipo de aplicación determinada y la versión.</span><span class="sxs-lookup"><span data-stu-id="87d24-178">You can also use Service Fabric Explorer toocreate application instances for a given application type and version.</span></span> <span data-ttu-id="87d24-179">Elija el tipo de aplicación de hello en la vista de árbol de hello, haga clic en hello **crear instancia de aplicación** versión toohello siguiente vínculo que se desea en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-179">Choose hello application type in hello tree view, then click hello **Create app instance** link next toohello version you'd like in hello right pane.</span></span>

![Creación de una instancia de aplicación en Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="87d24-181">En la actualidad, no se pueden parametrizar las instancias de aplicaciones creadas mediante Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="87d24-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="87d24-182">Se crean utilizando los valores de parámetros predeterminados.</span><span class="sxs-lookup"><span data-stu-id="87d24-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a><span data-ttu-id="87d24-183">Conectar el clúster de tejido de servicio remoto tooa</span><span class="sxs-lookup"><span data-stu-id="87d24-183">Connect tooa remote Service Fabric cluster</span></span>
<span data-ttu-id="87d24-184">Si conoce el punto de conexión del clúster de Hola y tiene los permisos necesarios pueden tener acceso a Service Fabric Explorer desde cualquier explorador.</span><span class="sxs-lookup"><span data-stu-id="87d24-184">If you know hello cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="87d24-185">Esto es porque el Explorador de Service Fabric es simplemente otro servicio que se ejecuta en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="87d24-185">This is because Service Fabric Explorer is just another service that runs in hello cluster.</span></span>

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="87d24-186">Detectar extremo de Service Fabric Explorer Hola para un clúster remoto</span><span class="sxs-lookup"><span data-stu-id="87d24-186">Discover hello Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="87d24-187">tooreach Service Fabric Explorer para un clúster determinado, seleccione el explorador para:</span><span class="sxs-lookup"><span data-stu-id="87d24-187">tooreach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="87d24-188">http://&lt;su-punto-de-conexión-de-clúster&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="87d24-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="87d24-189">Para los clústeres de Azure, dirección URL completa de hello también está disponible en el panel de essentials de clúster Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="87d24-189">For Azure clusters, hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="87d24-190">Conectar el clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="87d24-190">Connect tooa secure cluster</span></span>
<span data-ttu-id="87d24-191">Puede controlar el clúster de Service Fabric de tooyour de cliente acceso con certificados o usar Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="87d24-191">You can control client access tooyour Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="87d24-192">Si intentas tooconnect tooService Fabric Explorer en un clúster de seguro, a continuación, dependiendo de la configuración del clúster de hello podrá ser toopresent requiere un certificado de cliente o inicie sesión con AAD.</span><span class="sxs-lookup"><span data-stu-id="87d24-192">If you attempt tooconnect tooService Fabric Explorer on a secure cluster, then depending on hello cluster's configuration you'll be required toopresent a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87d24-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="87d24-193">Next steps</span></span>
* [<span data-ttu-id="87d24-194">Información general sobre Testability</span><span class="sxs-lookup"><span data-stu-id="87d24-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="87d24-195">Administración de aplicaciones de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="87d24-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="87d24-196">Implementación de aplicaciones de Service Fabric con PowerShell</span><span class="sxs-lookup"><span data-stu-id="87d24-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
