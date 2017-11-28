---
title: "aaaService integración con el mapa con System Center Operations Manager | Documentos de Microsoft"
description: "Mapa de servicio es una solución de Operations Management Suite que detecta automáticamente los componentes de la aplicación en Windows y mapas y sistemas Linux Hola comunicación entre los servicios. Este artículo describe el uso de mapa de servicio tooautomatically crear diagramas de aplicación distribuida en Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="66bf4-104">Integración de Mapa de servicio con System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="66bf4-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="66bf4-105">Esta característica está en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="66bf4-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="66bf4-106">Mapa de servicio de Operations Management Suite detecta los componentes de la aplicación en los sistemas Windows y Linux y comunicación de hello entre los servicios se asigna automáticamente.</span><span class="sxs-lookup"><span data-stu-id="66bf4-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="66bf4-107">Mapa de servicio le permite tooview el camino de Hola de servidores que pensar en ellos, como sistemas interconectados que ofrecen servicios críticos.</span><span class="sxs-lookup"><span data-stu-id="66bf4-107">Service Map allows you tooview your servers hello way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="66bf4-108">Mapa de servicio muestra las conexiones entre servidores, los procesos y los puertos a través de cualquier arquitectura conectado de TCP, sin ninguna configuración necesaria además de la instalación de Hola de un agente.</span><span class="sxs-lookup"><span data-stu-id="66bf4-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides hello installation of an agent.</span></span> <span data-ttu-id="66bf4-109">Para obtener más información, vea hello [documentación del mapa de servicio](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="66bf4-109">For more information, see hello [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="66bf4-110">Con esta integración entre System Center Operations Manager y el mapa de servicio, puede crear automáticamente diagramas de aplicación distribuida en Operations Manager que se basan en los mapas de dependencia dinámica hello en mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="66bf4-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on hello dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66bf4-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="66bf4-111">Prerequisites</span></span>
* <span data-ttu-id="66bf4-112">Un grupo de administración de Operations Manager que administra un conjunto de servidores.</span><span class="sxs-lookup"><span data-stu-id="66bf4-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="66bf4-113">Un área de trabajo de Operations Management Suite con hello solución de mapa de servicio habilitada.</span><span class="sxs-lookup"><span data-stu-id="66bf4-113">An Operations Management Suite workspace with hello Service Map solution enabled.</span></span>
* <span data-ttu-id="66bf4-114">Un conjunto de servidores (al menos uno) que se está administrando mediante Operations Manager y enviar datos tooService mapa.</span><span class="sxs-lookup"><span data-stu-id="66bf4-114">A set of servers (at least one) that are being managed by Operations Manager and sending data tooService Map.</span></span> <span data-ttu-id="66bf4-115">Se admiten los servidores de Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="66bf4-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="66bf4-116">Una entidad de servicio con acceso toohello suscripción de Azure que está asociado con el área de trabajo de hello Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="66bf4-116">A service principal with access toohello Azure subscription that is associated with hello Operations Management Suite workspace.</span></span> <span data-ttu-id="66bf4-117">Para obtener más información, consulte demasiado[crear una entidad de servicio](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="66bf4-117">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-hello-service-map-management-pack"></a><span data-ttu-id="66bf4-118">Instalar el módulo de administración de hello mapa de servicio</span><span class="sxs-lookup"><span data-stu-id="66bf4-118">Install hello Service Map management pack</span></span>
<span data-ttu-id="66bf4-119">Habilitar la integración de hello entre Operations Manager y mapa de servicio mediante la importación de paquete de módulos de administración de hello Microsoft.SystemCenter.ServiceMap (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="66bf4-119">You enable hello integration between Operations Manager and Service Map by importing hello Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="66bf4-120">agrupación de Hello contiene Hola después de módulos de administración:</span><span class="sxs-lookup"><span data-stu-id="66bf4-120">hello bundle contains hello following management packs:</span></span>
* <span data-ttu-id="66bf4-121">Microsoft Service Map Application Views</span><span class="sxs-lookup"><span data-stu-id="66bf4-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="66bf4-122">Microsoft System Center Service Map Internal</span><span class="sxs-lookup"><span data-stu-id="66bf4-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="66bf4-123">Microsoft System Center Service Map Overrides</span><span class="sxs-lookup"><span data-stu-id="66bf4-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="66bf4-124">Microsoft System Center Service Map</span><span class="sxs-lookup"><span data-stu-id="66bf4-124">Microsoft System Center Service Map</span></span>

## <a name="configure-hello-service-map-integration"></a><span data-ttu-id="66bf4-125">Configurar la integración del mapa de servicio Hola</span><span class="sxs-lookup"><span data-stu-id="66bf4-125">Configure hello Service Map integration</span></span>
<span data-ttu-id="66bf4-126">Después de instalar el módulo de administración de hello mapa de servicio, un nuevo nodo, **Service Map**, se muestra bajo **Operations Management Suite** en hello **administración** panel.</span><span class="sxs-lookup"><span data-stu-id="66bf4-126">After you install hello Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in hello **Administration** pane.</span></span> 

<span data-ttu-id="66bf4-127">tooconfigure integración con el mapa de servicio, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="66bf4-127">tooconfigure Service Map integration, do hello following:</span></span>

1. <span data-ttu-id="66bf4-128">Asistente de configuración de hello tooopen, Hola **Introducción al servicio de mapa** panel, haga clic en **Agregar área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="66bf4-128">tooopen hello configuration wizard, in hello **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Panel de información general de Mapa de servicio](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="66bf4-130">Hola **configuración de la conexión** ventana, escriba el nombre del inquilino de Hola o ID, Id. de aplicación (también conocido como nombre de usuario de Hola o clientID) y contraseña de entidad de servicio de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="66bf4-130">In hello **Connection Configuration** window, enter hello tenant name or ID, application ID (also known as hello username or clientID), and password of hello service principal, and then click **Next**.</span></span> <span data-ttu-id="66bf4-131">Para obtener más información, consulte demasiado[crear una entidad de servicio](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="66bf4-131">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

    ![ventana de configuración de la conexión de Hello](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="66bf4-133">Hola **selección de suscripción** ventana, seleccione Hola suscripción de Azure, el grupo de recursos de Azure (Hola uno que contiene el área de trabajo de hello Operations Management Suite) y área de trabajo de Operations Management Suite y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="66bf4-133">In hello **Subscription Selection** window, select hello Azure subscription, Azure resource group (hello one that contains hello Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Hola área de trabajo de configuración de Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="66bf4-135">Hola **selección de grupo de la máquina** ventana, decide qué grupos de máquinas de mapa de servicio que desee toosync tooOperations Manager.</span><span class="sxs-lookup"><span data-stu-id="66bf4-135">In hello **Machine Group Selection** window, you choose which Service Map Machine Groups you want toosync tooOperations Manager.</span></span> <span data-ttu-id="66bf4-136">Haga clic en **agregar o quitar grupos de máquinas**, seleccione los grupos de lista de Hola de **grupos disponibles de máquina**y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="66bf4-136">Click **Add/Remove Machine Groups**, choose groups from hello list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="66bf4-137">Cuando haya terminado la selección de grupos, haga clic en **Aceptar** toofinish.</span><span class="sxs-lookup"><span data-stu-id="66bf4-137">When you are finished selecting groups, click **Ok** toofinish.</span></span>
    
    ![Hola grupos de máquina de configuración de Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="66bf4-139">Hola **selección de servidor** ventana, se puede configurar Hola grupo de servidores de mapa de servicio con servidores de Hola que desea toosync entre Operations Manager y mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="66bf4-139">In hello **Server Selection** window, you configure hello Service Map Servers Group with hello servers that you want toosync between Operations Manager and Service Map.</span></span> <span data-ttu-id="66bf4-140">Haga clic en **Agregar o quitar servidores**.</span><span class="sxs-lookup"><span data-stu-id="66bf4-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="66bf4-141">Para toobuild de integración de hello un diagrama de la aplicación distribuida para un servidor, debe ser servidor hello:</span><span class="sxs-lookup"><span data-stu-id="66bf4-141">For hello integration toobuild a distributed application diagram for a server, hello server must be:</span></span>

    * <span data-ttu-id="66bf4-142">Administrado por Operations Manager</span><span class="sxs-lookup"><span data-stu-id="66bf4-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="66bf4-143">Administrado por Service Map</span><span class="sxs-lookup"><span data-stu-id="66bf4-143">Managed by Service Map</span></span>
    * <span data-ttu-id="66bf4-144">Aparecen en hello grupo de servidores de mapa de servicio</span><span class="sxs-lookup"><span data-stu-id="66bf4-144">Listed in hello Service Map Servers Group</span></span>

    ![Hola grupo de configuración de Operations Manager](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="66bf4-146">Opcional: Seleccione toocommunicate de grupo de recursos de servidor de administración de hello con Operations Management Suite y, a continuación, haga clic en **Agregar área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="66bf4-146">Optional: Select hello Management Server resource pool toocommunicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Hola grupo de recursos de configuración de Operations Manager](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="66bf4-148">Podría tardar un minuto tooconfigure y registrar el área de trabajo de hello Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="66bf4-148">It might take a minute tooconfigure and register hello Operations Management Suite workspace.</span></span> <span data-ttu-id="66bf4-149">Una vez configurado, Operations Manager inicia la primera sincronización de mapa de servicio Hola de Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="66bf4-149">After it is configured, Operations Manager initiates hello first Service Map sync from Operations Management Suite.</span></span>

    ![Hola grupo de recursos de configuración de Operations Manager](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="66bf4-151">Supervisión del Mapa de servicio</span><span class="sxs-lookup"><span data-stu-id="66bf4-151">Monitor Service Map</span></span>
<span data-ttu-id="66bf4-152">Después de conecta el área de trabajo de hello Operations Management Suite, una nueva carpeta, mapa de servicio, se muestra en hello **supervisión** panel de consola de Operations Manager Hola.</span><span class="sxs-lookup"><span data-stu-id="66bf4-152">After hello Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in hello **Monitoring** pane of hello Operations Manager console.</span></span>

![panel de supervisión de Operations Manager de Hola](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="66bf4-154">carpeta de mapa de servicio de Hello consta de cuatro nodos:</span><span class="sxs-lookup"><span data-stu-id="66bf4-154">hello Service Map folder has four nodes:</span></span>
* <span data-ttu-id="66bf4-155">**Alertas activas**: enumera todas las alertas activas de hello acerca de la comunicación de hello entre Operations Manager y mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="66bf4-155">**Active Alerts**: Lists all hello active alerts about hello communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="66bf4-156">Tenga en cuenta que estas alertas no son están sincronizados tooOperations Administrador de alertas de Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="66bf4-156">Note that these alerts are not Operations Management Suite alerts being synced tooOperations Manager.</span></span> 

* <span data-ttu-id="66bf4-157">**Servidores**: enumera los servidores de hello supervisado que están configuran toosync de mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="66bf4-157">**Servers**: Lists hello monitored servers that are configured toosync from Service Map.</span></span>

    ![panel de servidores de supervisión de Operations Manager Hola](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="66bf4-159">**Vistas de dependencia de grupo de máquinas**: muestra todos los grupos de máquinas que se sincronizan desde Service Map.</span><span class="sxs-lookup"><span data-stu-id="66bf4-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="66bf4-160">Puede hacer clic en cualquier grupo tooview su diagrama de aplicaciones distribuidas.</span><span class="sxs-lookup"><span data-stu-id="66bf4-160">You can click any group tooview its distributed application diagram.</span></span>

    ![diagrama de aplicaciones distribuidas de Operations Manager de Hola](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="66bf4-162">**Vistas de la dependencia de servidor**: muestra todos los servidores que se sincronizan desde Mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="66bf4-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="66bf4-163">Puede hacer clic en cualquier servidor tooview su diagrama de aplicaciones distribuidas.</span><span class="sxs-lookup"><span data-stu-id="66bf4-163">You can click any server tooview its distributed application diagram.</span></span>

    ![diagrama de aplicaciones distribuidas de Operations Manager de Hola](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a><span data-ttu-id="66bf4-165">Editar o eliminar área de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="66bf4-165">Edit or delete hello workspace</span></span>
<span data-ttu-id="66bf4-166">Puede editar o eliminar área de trabajo de hello configurado a través de hello **Introducción al servicio de mapa** panel (**administración** panel > **Operations Management Suite**  >  **Mapa de servicio**).</span><span class="sxs-lookup"><span data-stu-id="66bf4-166">You can edit or delete hello configured workspace through hello **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="66bf4-167">Puede configurar solo un área de trabajo de Operations Management Suite por ahora.</span><span class="sxs-lookup"><span data-stu-id="66bf4-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![panel de área de trabajo de Operations Manager editar Hola](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="66bf4-169">Configuración de reglas e invalidaciones</span><span class="sxs-lookup"><span data-stu-id="66bf4-169">Configure rules and overrides</span></span>
<span data-ttu-id="66bf4-170">Una regla, _Microsoft.SystemCenter.ServiceMapImport.Rule_, se crea información de captura tooperiodically de mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="66bf4-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created tooperiodically fetch information from Service Map.</span></span> <span data-ttu-id="66bf4-171">intervalos de sincronización de toochange, puede configurar las invalidaciones de regla de hello (**Authoring** panel > **reglas** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="66bf4-171">toochange sync timings, you can configure overrides of hello rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![ventana de propiedades de Hello invalidaciones de Operations Manager](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="66bf4-173">**Enabled**: sirve para habilitar o deshabilitar las actualizaciones automáticas.</span><span class="sxs-lookup"><span data-stu-id="66bf4-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="66bf4-174">**IntervalMinutes**: restablecer Hola tiempo que transcurre entre las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="66bf4-174">**IntervalMinutes**: Reset hello time between updates.</span></span> <span data-ttu-id="66bf4-175">intervalo de saludo predeterminado es una hora.</span><span class="sxs-lookup"><span data-stu-id="66bf4-175">hello default interval is one hour.</span></span> <span data-ttu-id="66bf4-176">Si desea toosync server mapas con más frecuencia, puede cambiar el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="66bf4-176">If you want toosync server maps more frequently, you can change hello value.</span></span>
* <span data-ttu-id="66bf4-177">**Tiempos de espera**: restablecer la longitud de Hola de tiempo antes de que agota el tiempo de espera de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="66bf4-177">**TimeoutSeconds**: Reset hello length of time before hello request times out.</span></span> 
* <span data-ttu-id="66bf4-178">**TimeWindowMinutes**: ventana de tiempo de restablecimiento de Hola para consultar datos.</span><span class="sxs-lookup"><span data-stu-id="66bf4-178">**TimeWindowMinutes**: Reset hello time window for querying data.</span></span> <span data-ttu-id="66bf4-179">El valor predeterminado es de 60 minutos.</span><span class="sxs-lookup"><span data-stu-id="66bf4-179">Default is a 60-minute window.</span></span> <span data-ttu-id="66bf4-180">valor máximo de Hello permitido por el mapa de servicio es 60 minutos.</span><span class="sxs-lookup"><span data-stu-id="66bf4-180">hello maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="66bf4-181">Problemas conocidos y limitaciones</span><span class="sxs-lookup"><span data-stu-id="66bf4-181">Known issues and limitations</span></span>

<span data-ttu-id="66bf4-182">diseño actual Hello presenta siguiente Hola problemas y limitaciones:</span><span class="sxs-lookup"><span data-stu-id="66bf4-182">hello current design presents hello following issues and limitations:</span></span>
* <span data-ttu-id="66bf4-183">Sólo se puede conectar el área de trabajo de tooa único Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="66bf4-183">You can only connect tooa single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="66bf4-184">Aunque es posible agregar servidores toohello grupo de servidores de mapa de servicio manualmente a través de hello **Authoring** panel, mapas de Hola para esos servidores no se sincronizan inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="66bf4-184">Although you can add servers toohello Service Map Servers Group manually through hello **Authoring** pane, hello maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="66bf4-185">Se sincronizarán de mapa de servicio durante el siguiente ciclo de sincronización de Hola.</span><span class="sxs-lookup"><span data-stu-id="66bf4-185">They will be synced from Service Map during hello next sync cycle.</span></span>
* <span data-ttu-id="66bf4-186">Si realiza cambios toohello distribuidas aplicación diagramas creados por el módulo de administración de hello, esos cambios se sobrescribirán probablemente en la próxima sincronización de hello con mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="66bf4-186">If you make any changes toohello Distributed Application Diagrams created by hello management pack, those changes will likely be overwritten on hello next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="66bf4-187">Creación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="66bf4-187">Create a service principal</span></span>
<span data-ttu-id="66bf4-188">Para obtener documentación oficial de Azure acerca de cómo crear una entidad de servicio, consulte:</span><span class="sxs-lookup"><span data-stu-id="66bf4-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="66bf4-189">Uso de Azure PowerShell para crear una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="66bf4-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="66bf4-190">Uso de la CLI de Azure para crear a una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="66bf4-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="66bf4-191">Crear a una entidad de servicio mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="66bf4-191">Create a service principal by using hello Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="66bf4-192">Comentarios</span><span class="sxs-lookup"><span data-stu-id="66bf4-192">Feedback</span></span>
<span data-ttu-id="66bf4-193">¿Quiere hacernos llegar algún comentario acerca de Mapa de servicio o esta documentación?</span><span class="sxs-lookup"><span data-stu-id="66bf4-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="66bf4-194">Visite nuestra [página Voz del usuario](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), donde puede sugerir características o votar sugerencias existentes.</span><span class="sxs-lookup"><span data-stu-id="66bf4-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
