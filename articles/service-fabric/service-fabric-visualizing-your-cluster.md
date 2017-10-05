---
title: "Visualización del clúster mediante el Explorador de Service Fabric | Microsoft Docs"
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
ms.openlocfilehash: 789793a7f50170188d688881a9178546c3074018
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="c42e9-103">Visualización del clúster mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c42e9-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="c42e9-104">El Explorador de Service Fabric es una herramienta web para inspeccionar y administrar aplicaciones y nodos en un clúster de Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c42e9-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="c42e9-105">El Explorador de Service Fabric se hospeda directamente en el clúster para que siempre esté disponible, independientemente de dónde se ejecuta el clúster.</span><span class="sxs-lookup"><span data-stu-id="c42e9-105">Service Fabric Explorer is hosted directly within the cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="c42e9-106">Tutorial en vídeo</span><span class="sxs-lookup"><span data-stu-id="c42e9-106">Video tutorial</span></span>

<span data-ttu-id="c42e9-107">Para información sobre cómo usar Service Fabric Explorer, vea el siguiente vídeo de Microsoft Virtual Academy:</span><span class="sxs-lookup"><span data-stu-id="c42e9-107">To learn how to use Service Fabric Explorer, watch the following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-to-service-fabric-explorer"></a><span data-ttu-id="c42e9-108">Conexión al Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c42e9-108">Connect to Service Fabric Explorer</span></span>
<span data-ttu-id="c42e9-109">Si ha seguido las instrucciones para [preparar el entorno de desarrollo](service-fabric-get-started.md), puede iniciar el Explorador de Service Fabric en el clúster local en http://localhost:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="c42e9-109">If you have followed the instructions to [prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating to http://localhost:19080/Explorer.</span></span>

## <a name="understand-the-service-fabric-explorer-layout"></a><span data-ttu-id="c42e9-110">Información sobre el diseño del Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c42e9-110">Understand the Service Fabric Explorer layout</span></span>
<span data-ttu-id="c42e9-111">Puede desplazarse por el Explorador de Service Fabric desde el árbol situado a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="c42e9-111">You can navigate through Service Fabric Explorer by using the tree on the left.</span></span> <span data-ttu-id="c42e9-112">En la raíz del árbol, el panel del clúster proporciona información general del clúster, incluido un resumen de la aplicación y del estado del nodo.</span><span class="sxs-lookup"><span data-stu-id="c42e9-112">At the root of the tree, the cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Panel de clúster del Explorador de Service Fabric][sfx-cluster-dashboard]

### <a name="view-the-clusters-layout"></a><span data-ttu-id="c42e9-114">Visualización del diseño del clúster</span><span class="sxs-lookup"><span data-stu-id="c42e9-114">View the cluster's layout</span></span>
<span data-ttu-id="c42e9-115">Los nodos de un clúster de Service Fabric se colocan en una cuadrícula bidimensional de dominios de error y dominios de actualización.</span><span class="sxs-lookup"><span data-stu-id="c42e9-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="c42e9-116">Esta colocación garantiza que las aplicaciones permanecen disponibles en presencia de errores de hardware y actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c42e9-116">This placement ensures that your applications remain available in the presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="c42e9-117">Puede ver cómo se dispone el clúster actual mediante el mapa del clúster.</span><span class="sxs-lookup"><span data-stu-id="c42e9-117">You can view how the current cluster is laid out by using the cluster map.</span></span>

![Mapa de clúster del Explorador de Service Fabric][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="c42e9-119">Visualización de aplicaciones y servicios</span><span class="sxs-lookup"><span data-stu-id="c42e9-119">View applications and services</span></span>
<span data-ttu-id="c42e9-120">El clúster contiene dos subárboles: uno para las aplicaciones y otro para los nodos.</span><span class="sxs-lookup"><span data-stu-id="c42e9-120">The cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="c42e9-121">Puede usar la vista de aplicaciones para navegar por la jerarquía lógica de Service Fabric: aplicaciones, servicios, particiones y réplicas.</span><span class="sxs-lookup"><span data-stu-id="c42e9-121">You can use the application view to navigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="c42e9-122">En el ejemplo siguiente, la aplicación **MyApp** se compone de dos servicios: **MyStatefulService** y **WebService**.</span><span class="sxs-lookup"><span data-stu-id="c42e9-122">In the example below, the application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="c42e9-123">Como **MyStatefulService** es un servicio con estado, incluye una partición con una réplica principal y dos réplicas secundarias.</span><span class="sxs-lookup"><span data-stu-id="c42e9-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="c42e9-124">Por el contrario, el servicio WebSvcService no tiene estado y contiene una única instancia.</span><span class="sxs-lookup"><span data-stu-id="c42e9-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Vista de aplicación del explorador de Service Fabric][sfx-application-tree]

<span data-ttu-id="c42e9-126">En cada nivel del árbol, el panel principal muestra la información pertinente sobre el elemento.</span><span class="sxs-lookup"><span data-stu-id="c42e9-126">At each level of the tree, the main pane shows pertinent information about the item.</span></span> <span data-ttu-id="c42e9-127">Por ejemplo, puede ver el estado de mantenimiento y la versión para un servicio determinado.</span><span class="sxs-lookup"><span data-stu-id="c42e9-127">For example, you can see the health status and version for a particular service.</span></span>

![Panel Essentials del explorador de Service Fabric][sfx-service-essentials]

### <a name="view-the-clusters-nodes"></a><span data-ttu-id="c42e9-129">Visualización de los nodos del clúster</span><span class="sxs-lookup"><span data-stu-id="c42e9-129">View the cluster's nodes</span></span>
<span data-ttu-id="c42e9-130">En la vista de nodos se muestra el diseño físico del clúster.</span><span class="sxs-lookup"><span data-stu-id="c42e9-130">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="c42e9-131">Para un nodo determinado, puede comprobar qué aplicaciones tienen el código implementado en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="c42e9-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="c42e9-132">Más específicamente, puede ver qué réplicas están en ejecución.</span><span class="sxs-lookup"><span data-stu-id="c42e9-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="c42e9-133">Acciones</span><span class="sxs-lookup"><span data-stu-id="c42e9-133">Actions</span></span>
<span data-ttu-id="c42e9-134">El explorador de Service Fabric ofrece una forma rápida de invocar acciones en nodos, aplicaciones y servicios dentro del clúster.</span><span class="sxs-lookup"><span data-stu-id="c42e9-134">Service Fabric Explorer offers a quick way to invoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="c42e9-135">Por ejemplo, para eliminar una instancia de la aplicación, elija la aplicación en el árbol de la izquierda y, luego, elija **Acciones** > **Eliminar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="c42e9-135">For example, to delete an application instance, choose the application from the tree on the left, and then choose **Actions** > **Delete Application**.</span></span>

![Eliminación de una aplicación en el explorador de Service Fabric][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="c42e9-137">Puede realizar las mismas acciones haciendo clic en los puntos suspensivos situados junto a cada elemento.</span><span class="sxs-lookup"><span data-stu-id="c42e9-137">You can perform the same actions by clicking the ellipsis next to each element.</span></span>
>
>

<span data-ttu-id="c42e9-138">En la tabla siguiente se enumeran las acciones disponibles para cada entidad:</span><span class="sxs-lookup"><span data-stu-id="c42e9-138">The following table lists the actions available for each entity:</span></span>

| <span data-ttu-id="c42e9-139">**Entidad**</span><span class="sxs-lookup"><span data-stu-id="c42e9-139">**Entity**</span></span> | <span data-ttu-id="c42e9-140">**Acción**</span><span class="sxs-lookup"><span data-stu-id="c42e9-140">**Action**</span></span> | <span data-ttu-id="c42e9-141">**Descripción**</span><span class="sxs-lookup"><span data-stu-id="c42e9-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c42e9-142">Tipo de aplicación</span><span class="sxs-lookup"><span data-stu-id="c42e9-142">Application type</span></span> |<span data-ttu-id="c42e9-143">Tipo de anulación de aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="c42e9-143">Unprovision type</span></span> |<span data-ttu-id="c42e9-144">Quita el paquete de aplicación del almacén de imágenes del clúster.</span><span class="sxs-lookup"><span data-stu-id="c42e9-144">Removes the application package from the cluster's image store.</span></span> <span data-ttu-id="c42e9-145">Requiere que todas las aplicaciones de ese tipo se quiten en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="c42e9-145">Requires all applications of that type to be removed first.</span></span> |
| <span data-ttu-id="c42e9-146">Application</span><span class="sxs-lookup"><span data-stu-id="c42e9-146">Application</span></span> |<span data-ttu-id="c42e9-147">Eliminar aplicación</span><span class="sxs-lookup"><span data-stu-id="c42e9-147">Delete Application</span></span> |<span data-ttu-id="c42e9-148">Elimine la aplicación, incluidos todos sus servicios y su estado (si hubiera).</span><span class="sxs-lookup"><span data-stu-id="c42e9-148">Delete the application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="c42e9-149">Servicio</span><span class="sxs-lookup"><span data-stu-id="c42e9-149">Service</span></span> |<span data-ttu-id="c42e9-150">Eliminar servicio</span><span class="sxs-lookup"><span data-stu-id="c42e9-150">Delete Service</span></span> |<span data-ttu-id="c42e9-151">Elimine el servicio y su estado (si hubiera).</span><span class="sxs-lookup"><span data-stu-id="c42e9-151">Delete the service and its state (if any).</span></span> |
| <span data-ttu-id="c42e9-152">Nodo</span><span class="sxs-lookup"><span data-stu-id="c42e9-152">Node</span></span> |<span data-ttu-id="c42e9-153">Activar</span><span class="sxs-lookup"><span data-stu-id="c42e9-153">Activate</span></span> |<span data-ttu-id="c42e9-154">Active el nodo.</span><span class="sxs-lookup"><span data-stu-id="c42e9-154">Activate the node.</span></span> |
| <span data-ttu-id="c42e9-155">Nodo</span><span class="sxs-lookup"><span data-stu-id="c42e9-155">Node</span></span> | <span data-ttu-id="c42e9-156">Desactivar (pausa)</span><span class="sxs-lookup"><span data-stu-id="c42e9-156">Deactivate (pause)</span></span> | <span data-ttu-id="c42e9-157">Pause el nodo en su estado actual.</span><span class="sxs-lookup"><span data-stu-id="c42e9-157">Pause the node in its current state.</span></span> <span data-ttu-id="c42e9-158">Los servicios siguen ejecutándose, pero Service Fabric no introduce ni saca nada proactivamente, a menos que se requiera para prevenir una interrupción o una incoherencia de datos.</span><span class="sxs-lookup"><span data-stu-id="c42e9-158">Services continue to run but Service Fabric does not proactively move anything onto or off it unless it is required to prevent an outage or data inconsistency.</span></span> <span data-ttu-id="c42e9-159">Esta acción se utiliza normalmente para habilitar los servicios de depuración en un nodo específico para asegurarse de que no se mueven durante la inspección.</span><span class="sxs-lookup"><span data-stu-id="c42e9-159">This action is typically used to enable debugging services on a specific node to ensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="c42e9-160">Nodo</span><span class="sxs-lookup"><span data-stu-id="c42e9-160">Node</span></span> | <span data-ttu-id="c42e9-161">Desactivar (reiniciar)</span><span class="sxs-lookup"><span data-stu-id="c42e9-161">Deactivate (restart)</span></span> | <span data-ttu-id="c42e9-162">Saque todos los servicios de la memoria de un nodo y cierre los servicios persistentes de forma segura.</span><span class="sxs-lookup"><span data-stu-id="c42e9-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="c42e9-163">Suele usarse cuando es necesario reiniciar los procesos de host o el equipo.</span><span class="sxs-lookup"><span data-stu-id="c42e9-163">Typically used when the host processes or machine need to be restarted.</span></span> | |
| <span data-ttu-id="c42e9-164">Nodo</span><span class="sxs-lookup"><span data-stu-id="c42e9-164">Node</span></span> | <span data-ttu-id="c42e9-165">Desactivar (quitar datos)</span><span class="sxs-lookup"><span data-stu-id="c42e9-165">Deactivate (remove data)</span></span> | <span data-ttu-id="c42e9-166">Cierre todos los servicios que se ejecutan en el nodo después de la creación de suficientes réplicas de reserva con seguridad.</span><span class="sxs-lookup"><span data-stu-id="c42e9-166">Safely close all services running on the node after building sufficient spare replicas.</span></span> <span data-ttu-id="c42e9-167">Se utiliza normalmente cuando un nodo (o al menos su almacenamiento) se está sacando permanentemente de circulación.</span><span class="sxs-lookup"><span data-stu-id="c42e9-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="c42e9-168">Nodo</span><span class="sxs-lookup"><span data-stu-id="c42e9-168">Node</span></span> | <span data-ttu-id="c42e9-169">Quitar el estado del nodo</span><span class="sxs-lookup"><span data-stu-id="c42e9-169">Remove node state</span></span> | <span data-ttu-id="c42e9-170">Quite información de las réplicas de un nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="c42e9-170">Remove knowledge of a node's replicas from the cluster.</span></span> <span data-ttu-id="c42e9-171">Se utiliza normalmente cuando un nodo con error ya se considera irrecuperable.</span><span class="sxs-lookup"><span data-stu-id="c42e9-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="c42e9-172">Nodo</span><span class="sxs-lookup"><span data-stu-id="c42e9-172">Node</span></span> | <span data-ttu-id="c42e9-173">Reiniciar</span><span class="sxs-lookup"><span data-stu-id="c42e9-173">Restart</span></span> | <span data-ttu-id="c42e9-174">Reinicie el nodo para simular un error de nodo.</span><span class="sxs-lookup"><span data-stu-id="c42e9-174">Simulate a node failure by restarting the node.</span></span> <span data-ttu-id="c42e9-175">Puede encontrar más información [aquí](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="c42e9-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="c42e9-176">Como muchas acciones son destructivas, le pediremos que confirme su intención antes de que finalice la acción.</span><span class="sxs-lookup"><span data-stu-id="c42e9-176">Since many actions are destructive, you may be asked to confirm your intent before the action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="c42e9-177">Todas las acciones que pueden realizarse a través del Explorador de Service Fabric también pueden realizarse a través de PowerShell o una API de REST, para habilitar la automatización.</span><span class="sxs-lookup"><span data-stu-id="c42e9-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, to enable automation.</span></span>
>
>

<span data-ttu-id="c42e9-178">También puede utilizar el Service Fabric Explorer a fin de crear instancias de aplicaciones para un tipo de aplicación y versión.</span><span class="sxs-lookup"><span data-stu-id="c42e9-178">You can also use Service Fabric Explorer to create application instances for a given application type and version.</span></span> <span data-ttu-id="c42e9-179">Elija el tipo de aplicación en la vista de árbol y, luego, haga clic en el vínculo **Create app instance** (Crear instancia de aplicación) situado junto a la versión que desee en el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="c42e9-179">Choose the application type in the tree view, then click the **Create app instance** link next to the version you'd like in the right pane.</span></span>

![Creación de una instancia de aplicación en Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="c42e9-181">En la actualidad, no se pueden parametrizar las instancias de aplicaciones creadas mediante Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="c42e9-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="c42e9-182">Se crean utilizando los valores de parámetros predeterminados.</span><span class="sxs-lookup"><span data-stu-id="c42e9-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-to-a-remote-service-fabric-cluster"></a><span data-ttu-id="c42e9-183">Conexión a un clúster de Service Fabric remoto</span><span class="sxs-lookup"><span data-stu-id="c42e9-183">Connect to a remote Service Fabric cluster</span></span>
<span data-ttu-id="c42e9-184">Si conoce el punto de conexión del clúster y tiene los permisos suficientes, puede tener acceso a Service Fabric Explorer desde cualquier explorador.</span><span class="sxs-lookup"><span data-stu-id="c42e9-184">If you know the cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="c42e9-185">Esto se debe a que Service Fabric Explorer no es más que otro servicio que se ejecuta en el clúster.</span><span class="sxs-lookup"><span data-stu-id="c42e9-185">This is because Service Fabric Explorer is just another service that runs in the cluster.</span></span>

### <a name="discover-the-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="c42e9-186">Detección del punto de conexión del Explorador de Service Fabric para un clúster remoto</span><span class="sxs-lookup"><span data-stu-id="c42e9-186">Discover the Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="c42e9-187">Si desea tener acceso a Service Fabric Explorer para un clúster determinado, dirija el explorador a:</span><span class="sxs-lookup"><span data-stu-id="c42e9-187">To reach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="c42e9-188">http://&lt;su-punto-de-conexión-de-clúster&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="c42e9-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="c42e9-189">En el caso de clústeres de Azure, la dirección URL completa también está disponible en el panel de elementos esenciales del clúster de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c42e9-189">For Azure clusters, the full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="c42e9-190">Conexión a un clúster seguro</span><span class="sxs-lookup"><span data-stu-id="c42e9-190">Connect to a secure cluster</span></span>
<span data-ttu-id="c42e9-191">Puede controlar el acceso de cliente a su clúster de Service Fabric con certificados o mediante Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="c42e9-191">You can control client access to your Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="c42e9-192">Si intenta conectarse a Service Fabric Explorer en un clúster seguro, se le pedirá presentar un certificado de cliente o iniciar sesión con AAD, según la configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="c42e9-192">If you attempt to connect to Service Fabric Explorer on a secure cluster, then depending on the cluster's configuration you'll be required to present a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c42e9-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c42e9-193">Next steps</span></span>
* [<span data-ttu-id="c42e9-194">Información general sobre Testability</span><span class="sxs-lookup"><span data-stu-id="c42e9-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="c42e9-195">Administración de aplicaciones de Service Fabric en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c42e9-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="c42e9-196">Implementación de aplicaciones de Service Fabric con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c42e9-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
