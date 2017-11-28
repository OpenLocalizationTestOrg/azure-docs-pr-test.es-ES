---
title: "aaaSet de un clúster de Azure Service Fabric | Documentos de Microsoft"
description: "Inicio rápido: creación de un clúster de Windows o Linux Service Fabric en Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="65824-103">Creación del primer clúster de Service Fabric en Azure</span><span class="sxs-lookup"><span data-stu-id="65824-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="65824-104">Un [clúster de Service Fabric](service-fabric-deploy-anywhere.md) es un conjunto de máquinas físicas o virtuales conectadas a la red, en las que se implementan y administran los microservicios.</span><span class="sxs-lookup"><span data-stu-id="65824-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="65824-105">Este inicio rápido le ayuda a un clúster de cinco nodos, que se ejecuta en Windows o Linux, a través de hello toocreate [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) o [portal de Azure](http://portal.azure.com) en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="65824-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="65824-106">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="65824-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="65824-107">Usar hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="65824-107">Use hello Azure portal</span></span>

<span data-ttu-id="65824-108">Inicie sesión en toohello portal de Azure en [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="65824-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="65824-109">Crear clúster Hola</span><span class="sxs-lookup"><span data-stu-id="65824-109">Create hello cluster</span></span>

1. <span data-ttu-id="65824-110">Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="65824-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="65824-111">Seleccione **proceso** de hello **nuevo** hoja y, a continuación, seleccione **clúster de Service Fabric** de hello **proceso** hoja.</span><span class="sxs-lookup"><span data-stu-id="65824-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="65824-112">Rellene Hola Service Fabric **Fundamentos** formulario.</span><span class="sxs-lookup"><span data-stu-id="65824-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="65824-113">Para **sistema operativo**, seleccione la versión de Hola de Windows o Linux que desea Hola toorun de nodos de clúster.</span><span class="sxs-lookup"><span data-stu-id="65824-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="65824-114">nombre de usuario de Hello y una contraseña escritos aquí es toolog usado en la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="65824-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="65824-115">En **Grupo de recursos**, cree uno.</span><span class="sxs-lookup"><span data-stu-id="65824-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="65824-116">Un grupo de recursos es un contenedor lógico en el que se administran y crean los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="65824-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="65824-117">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="65824-117">When complete, click **OK**.</span></span>

    ![Salida de instalación de clúster][cluster-setup-basics]

4. <span data-ttu-id="65824-119">Rellene hello **configuración de clúster** formulario.</span><span class="sxs-lookup"><span data-stu-id="65824-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="65824-120">En **Número de tipos de nodos**, escriba "1".</span><span class="sxs-lookup"><span data-stu-id="65824-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="65824-121">Seleccione **1 (principal) del tipo de nodo** y rellene hello **configuración de tipo de nodo** formulario.</span><span class="sxs-lookup"><span data-stu-id="65824-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="65824-122">Escriba un nombre de tipo de nodo y establezca hello [el nivel de durabilidad](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) demasiado "bronce".</span><span class="sxs-lookup"><span data-stu-id="65824-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="65824-123">Seleccione un tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65824-123">Select a VM size.</span></span>

    <span data-ttu-id="65824-124">Tipos de nodos definen tamaño de máquina virtual de hello, número de máquinas virtuales, los puntos de conexión personalizadas, y otras opciones de Hola máquinas virtuales de ese tipo.</span><span class="sxs-lookup"><span data-stu-id="65824-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="65824-125">Cada tipo de nodo definido se configura como un conjunto de escala de máquina virtual independiente, que es usado toodeploy y máquinas virtuales administradas como un conjunto.</span><span class="sxs-lookup"><span data-stu-id="65824-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="65824-126">Cada tipo de nodo se puede escalar o reducir verticalmente de forma independiente. Cada uno tiene diferentes conjuntos de puertos abiertos y puede tener distintas métricas de capacidad.</span><span class="sxs-lookup"><span data-stu-id="65824-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="65824-127">Hola primera o principal, tipo de nodo es donde los servicios del sistema de Service Fabric se hospedan y deben tener cinco o más máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="65824-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="65824-128">En cualquier implementación de producción, el [planeamiento de capacidad](service-fabric-cluster-capacity.md) es un paso importante.</span><span class="sxs-lookup"><span data-stu-id="65824-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="65824-129">Para este inicio rápido, sin embargo, no está ejecutando aplicaciones así que seleccione un tamaño de máquina virtual *DS1_v2 Estándar*.</span><span class="sxs-lookup"><span data-stu-id="65824-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="65824-130">Seleccione "Silver" para hello [nivel de confiabilidad](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) y una escala de la máquina virtual inicial establece capacidad de 5.</span><span class="sxs-lookup"><span data-stu-id="65824-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="65824-131">Extremos personalizados abrirán puertos en el equilibrador de carga de Azure de Hola para que puedan conectarse con aplicaciones que se ejecutan en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="65824-132">Escriba "80, 8172" tooopen los puertos 80 y 8172.</span><span class="sxs-lookup"><span data-stu-id="65824-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="65824-133">¿Comprobar hello **configurar opciones avanzadas** box, que se utiliza para personalizar los extremos de la administración de TCP o HTTP, intervalos de puertos de la aplicación, [las restricciones de posición](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), y [capacidad propiedades](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="65824-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="65824-134">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="65824-134">Select **OK**.</span></span>

6. <span data-ttu-id="65824-135">Hola **configuración de clúster** formulario, establezca **diagnósticos** demasiado**en**.</span><span class="sxs-lookup"><span data-stu-id="65824-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="65824-136">Para este tutorial rápido, no es necesario tooenter cualquier [tejido establecer](service-fabric-cluster-fabric-settings.md) propiedades.</span><span class="sxs-lookup"><span data-stu-id="65824-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="65824-137">En **versión de Fabric**, seleccione **automática** actualizar el modo de modo que Microsoft actualiza automáticamente la versión Hola de código de fabric Hola ejecuta Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="65824-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="65824-138">Establecer el modo de hello demasiado**Manual** si desea demasiado[elegir una versión compatible](service-fabric-cluster-upgrade.md) tooupgrade a.</span><span class="sxs-lookup"><span data-stu-id="65824-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![Configuración del tipo de nodo][node-type-config]

    <span data-ttu-id="65824-140">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="65824-140">Select **OK**.</span></span>

7. <span data-ttu-id="65824-141">Rellene hello **seguridad** formulario.</span><span class="sxs-lookup"><span data-stu-id="65824-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="65824-142">Para este inicio rápido seleccione **No seguro**.</span><span class="sxs-lookup"><span data-stu-id="65824-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="65824-143">Es muy recomendable un clúster segura para las cargas de trabajo de producción, de toocreate sin embargo, dado que cualquiera puede conectarse tooan clúster y realizar operaciones de administración de forma anónima.</span><span class="sxs-lookup"><span data-stu-id="65824-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="65824-144">Los certificados se utilizan en toosecure de autenticación y cifrado de Service Fabric tooprovide diversos aspectos de un clúster y sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="65824-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="65824-145">Para más información sobre el modo en que se usan los certificados en Service Fabric, consulte los [Escenarios de seguridad de los clústeres de Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="65824-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="65824-146">autenticación de usuario de tooenable mediante Azure Active Directory o tooset los certificados de seguridad de la aplicación, [crear un clúster desde una plantilla de administrador de recursos](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="65824-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="65824-147">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="65824-147">Select **OK**.</span></span>

8. <span data-ttu-id="65824-148">Resumen de hello de revisión.</span><span class="sxs-lookup"><span data-stu-id="65824-148">Review hello summary.</span></span>  <span data-ttu-id="65824-149">Si desea que toodownload una plantilla de administrador de recursos compilada a partir de la configuración de Hola que escribió, seleccione **descargar la plantilla y los parámetros**.</span><span class="sxs-lookup"><span data-stu-id="65824-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="65824-150">Seleccione **crear** clúster de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="65824-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="65824-151">Puede ver el progreso de la creación de hello en las notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="65824-152">(Haga clic en el icono de campana"hello" cerca de la barra de estado de hello en la parte superior de hello derecha de la pantalla). Si hace clic en **Pin tooStartboard** al crear el clúster de hello, consulte **implementación de clúster de Service Fabric** anclado toohello **iniciar** panel.</span><span class="sxs-lookup"><span data-stu-id="65824-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="65824-153">Visualización del estado del clúster</span><span class="sxs-lookup"><span data-stu-id="65824-153">View cluster status</span></span>
<span data-ttu-id="65824-154">Una vez creado el clúster, puede inspeccionar el clúster en hello **Introducción** hoja en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="65824-155">Ahora puede ver detalles de hello del clúster en panel de hello, incluidos extremo público del clúster de Hola y un explorador de Fabric tooService de vínculo.</span><span class="sxs-lookup"><span data-stu-id="65824-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![Estado del clúster][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="65824-157">Visualizar el clúster de hello mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="65824-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="65824-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) es una buena herramienta para visualizar el clúster y administrar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="65824-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="65824-159">Explorador de Service Fabric es un servicio que se ejecuta en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="65824-160">Acceder a él mediante un explorador web, haga clic en hello **Service Fabric Explorer** vínculo de clúster de hello **Introducción** página del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="65824-161">También puede especificar direcciones de hello directamente en el Explorador de hello: [http://quickstartcluster.westus.cloudapp.azure.com:19080/explorador](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="65824-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="65824-162">panel de clúster de Hello proporciona una visión general del clúster, incluido un resumen de la aplicación y el estado de nodo.</span><span class="sxs-lookup"><span data-stu-id="65824-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="65824-163">vista de nodo de Hello muestra el diseño físico de Hola de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="65824-164">Para un nodo determinado, puede comprobar qué aplicaciones tienen el código implementado en ese nodo.</span><span class="sxs-lookup"><span data-stu-id="65824-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="65824-166">Conectar el clúster toohello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="65824-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="65824-167">Compruebe que ese clúster Hola se está ejecutando al conectar con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65824-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="65824-168">Hello ServiceFabric PowerShell se instala con hello [SDK del servicio de Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="65824-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="65824-169">Hola [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establece un clúster de toohello de conexión.</span><span class="sxs-lookup"><span data-stu-id="65824-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="65824-170">Vea [clúster segura de conectar tooa](service-fabric-connect-to-secure-cluster.md) para obtener ejemplos de conexión de tooa de clúster.</span><span class="sxs-lookup"><span data-stu-id="65824-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="65824-171">Después de la conexión de toohello de clúster, use hello [ServiceFabricNode Get](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay una lista de nodos en la información de clúster y el estado de Hola para cada nodo.</span><span class="sxs-lookup"><span data-stu-id="65824-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="65824-172">**HealthState** debe ser *OK* para cada nodo.</span><span class="sxs-lookup"><span data-stu-id="65824-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a><span data-ttu-id="65824-173">Quitar clúster Hola</span><span class="sxs-lookup"><span data-stu-id="65824-173">Remove hello cluster</span></span>
<span data-ttu-id="65824-174">Además propio recurso de clúster toohello, un clúster de Service Fabric se compone de otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="65824-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="65824-175">Por lo que toocompletely eliminar un clúster de Service Fabric debe toodelete que todos Hola recursos que está formada.</span><span class="sxs-lookup"><span data-stu-id="65824-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="65824-176">clúster de Hola de manera más sencilla de Hello toodelete y todos los recursos de Hola que consume es grupo de recursos de toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="65824-177">Para otro toodelete formas un clúster o toodelete recursos Hola algunas (aunque no todos) en un grupo de recursos, consulte [eliminar un clúster](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="65824-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="65824-178">Eliminar un grupo de recursos en hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="65824-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="65824-179">Navegar por clúster de Service Fabric toohello desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="65824-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="65824-180">Haga clic en hello **grupo de recursos** nombre de página de hello clúster essentials.</span><span class="sxs-lookup"><span data-stu-id="65824-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="65824-181">Hola **Essentials de grupo de recursos** página, haga clic en **eliminar el grupo de recursos** y siga las instrucciones de hello en dicha eliminación de página toocomplete Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="65824-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="65824-182">![Eliminar grupo de recursos de Hola][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="65824-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="65824-183">Usar Powershell de Azure toodeploy un clúster segura</span><span class="sxs-lookup"><span data-stu-id="65824-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="65824-184">Descargar hello [Azure Powershell versión 4.0 o posterior del módulo](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) en su equipo.</span><span class="sxs-lookup"><span data-stu-id="65824-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="65824-185">Abra una ventana de Windows PowerShell, Hola de ejecución siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="65824-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="65824-186">Debería aparecer un resultado similar toohello.</span><span class="sxs-lookup"><span data-stu-id="65824-186">You should see an output similar toohello following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="65824-188">TooAzure de inicio de sesión y seleccione hello toowhich de suscripción que desea toocreate Hola clúster</span><span class="sxs-lookup"><span data-stu-id="65824-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="65824-189">Hola ejecución sigue toonow comando crea un clúster seguro.</span><span class="sxs-lookup"><span data-stu-id="65824-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="65824-190">No olvide parámetros de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="65824-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="65824-191">comando Hello puede durar entre 10 minutos too30 minutos toocomplete, al final de Hola de ella, debe obtener un siguiente toohello similar de salida.</span><span class="sxs-lookup"><span data-stu-id="65824-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="65824-192">salida de Hello tiene información sobre el certificado de hello, hello KeyVault donde se cargaron en, y Hola carpeta local donde se copia el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="65824-194">Copiar el resultado completo de Hola y guarde el archivo de texto de tooa como necesitamos toorefer tooit.</span><span class="sxs-lookup"><span data-stu-id="65824-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="65824-195">Tome nota de hello siguiendo la información de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="65824-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="65824-196">**CertificateSavedLocalPath**: c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="65824-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="65824-197">**CertificateThumbprint**: C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="65824-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="65824-198">**ManagementEndpoint**: https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="65824-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="65824-199">**ClientConnectionEndpointPort**: 19000</span><span class="sxs-lookup"><span data-stu-id="65824-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="65824-200">Instalar certificado de hello en el equipo local</span><span class="sxs-lookup"><span data-stu-id="65824-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="65824-201">clúster de toohello tooconnect, necesita tooinstall Hola certificado en almacén de hello Personal del usuario actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="65824-202">Ejecute hello después de PowerShell</span><span class="sxs-lookup"><span data-stu-id="65824-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="65824-203">Ya estás listo tooconnect tooyour segura clúster.</span><span class="sxs-lookup"><span data-stu-id="65824-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="65824-204">Conectar el clúster segura tooa</span><span class="sxs-lookup"><span data-stu-id="65824-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="65824-205">Ejecute hello siguiente comando PowerShell tooconnect tooa segura clúster.</span><span class="sxs-lookup"><span data-stu-id="65824-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="65824-206">Detalles del certificado Hola deben coincidir con un certificado que se usa tooset clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="65824-207">Hola siguiendo el ejemplo se muestra hello parámetros completed:</span><span class="sxs-lookup"><span data-stu-id="65824-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="65824-208">Ejecute hello después toocheck de comando que está conectado y Hola clúster es correcto.</span><span class="sxs-lookup"><span data-stu-id="65824-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="65824-209">Publicar su clúster de tooyour aplicaciones desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="65824-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="65824-210">Ahora que ha configurado un clúster de Azure, puede publicar su tooit de aplicaciones desde Visual Studio por hello siguiente [publicar tooan clúster](service-fabric-publish-app-remote-cluster.md) documento.</span><span class="sxs-lookup"><span data-stu-id="65824-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="65824-211">Quitar clúster Hola</span><span class="sxs-lookup"><span data-stu-id="65824-211">Remove hello cluster</span></span>
<span data-ttu-id="65824-212">Además propio recurso de clúster toohello, un clúster se compone de otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="65824-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="65824-213">clúster de Hola de manera más sencilla de Hello toodelete y todos los recursos de Hola que consume es grupo de recursos de toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="65824-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="65824-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65824-214">Next steps</span></span>
<span data-ttu-id="65824-215">Ahora que ha configurado un clúster de desarrollo, prueba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="65824-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="65824-216">Crear un clúster seguro en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="65824-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="65824-217">Crear un clúster a partir de una plantilla</span><span class="sxs-lookup"><span data-stu-id="65824-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* <span data-ttu-id="65824-218">[Implemente aplicaciones mediante PowerShell](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="65824-218">[Deploy apps using PowerShell](service-fabric-deploy-remove-applications.md)</span></span>


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
