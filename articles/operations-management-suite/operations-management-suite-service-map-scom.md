---
title: "Integración de Service Map con System Center Operations Manager | Microsoft Docs"
description: "Mapa de servicio es una solución de Operations Management Suite que detecta automáticamente los componentes de la aplicación en sistemas Windows y Linux y asigna la comunicación entre servicios. En este artículo se aborda el uso de Mapa de servicio para crear automáticamente diagramas de aplicaciones distribuidas en Operations Manager."
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
ms.openlocfilehash: a7dbe54ffb4daa941c19b51ba263dd3d23b7a98b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="7cbdf-104">Integración de Mapa de servicio con System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="7cbdf-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="7cbdf-105">Esta característica está en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="7cbdf-106">Mapa de servicio de Operations Management Suite detecta automáticamente los componentes de la aplicación en sistemas Windows y Linux y asigna la comunicación entre los servicios.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="7cbdf-107">Mapa de servicio permite ver los servidores a medida que piensa en ellos, como los sistemas interconectados que ofrecen servicios críticos.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-107">Service Map allows you to view your servers the way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="7cbdf-108">Mapa de servicio muestra las conexiones entre servidores, procesos y puertos en cualquier arquitectura conectada TCP sin una configuración necesaria que sea distinta a la instalación de un agente.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides the installation of an agent.</span></span> <span data-ttu-id="7cbdf-109">Para más detalles, consulte la [documentación de Mapa de servicio](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="7cbdf-109">For more information, see the [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="7cbdf-110">Con esta integración entre Mapa de servicio y System Center Operations Manager, puede crear automáticamente diagramas de aplicaciones distribuidas en Operations Manager basados en mapas de dependencia dinámica de Mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cbdf-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7cbdf-111">Prerequisites</span></span>
* <span data-ttu-id="7cbdf-112">Un grupo de administración de Operations Manager que administra un conjunto de servidores.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="7cbdf-113">Un área de trabajo de Operations Management Suite con la solución Mapa de servicio habilitada.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-113">An Operations Management Suite workspace with the Service Map solution enabled.</span></span>
* <span data-ttu-id="7cbdf-114">Un conjunto de servidores (al menos uno) que se administren desde Operations Manager y envíen datos a Mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-114">A set of servers (at least one) that are being managed by Operations Manager and sending data to Service Map.</span></span> <span data-ttu-id="7cbdf-115">Se admiten los servidores de Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="7cbdf-116">Una entidad de servicio con acceso a la suscripción de Azure asociada al área de trabajo de Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-116">A service principal with access to the Azure subscription that is associated with the Operations Management Suite workspace.</span></span> <span data-ttu-id="7cbdf-117">Para más información, vaya a [Create a service principal](#creating-a-service-principal) (Creación de una entidad de servicio).</span><span class="sxs-lookup"><span data-stu-id="7cbdf-117">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-the-service-map-management-pack"></a><span data-ttu-id="7cbdf-118">Instalación del módulo de administración de Mapa de servicio</span><span class="sxs-lookup"><span data-stu-id="7cbdf-118">Install the Service Map management pack</span></span>
<span data-ttu-id="7cbdf-119">La integración entre Operations Manager y Mapa de servicio se habilita al importar el paquete de módulos de administración de Microsoft.SystemCenter.ServiceMap (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="7cbdf-119">You enable the integration between Operations Manager and Service Map by importing the Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="7cbdf-120">El paquete contiene los siguientes módulos de administración:</span><span class="sxs-lookup"><span data-stu-id="7cbdf-120">The bundle contains the following management packs:</span></span>
* <span data-ttu-id="7cbdf-121">Microsoft Service Map Application Views</span><span class="sxs-lookup"><span data-stu-id="7cbdf-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="7cbdf-122">Microsoft System Center Service Map Internal</span><span class="sxs-lookup"><span data-stu-id="7cbdf-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="7cbdf-123">Microsoft System Center Service Map Overrides</span><span class="sxs-lookup"><span data-stu-id="7cbdf-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="7cbdf-124">Microsoft System Center Service Map</span><span class="sxs-lookup"><span data-stu-id="7cbdf-124">Microsoft System Center Service Map</span></span>

## <a name="configure-the-service-map-integration"></a><span data-ttu-id="7cbdf-125">Configuración de la integración de Mapa de servicio</span><span class="sxs-lookup"><span data-stu-id="7cbdf-125">Configure the Service Map integration</span></span>
<span data-ttu-id="7cbdf-126">Después de instalar el módulo de administración de **Mapa de servicio**, habrá un nuevo nodo, Mapa de servicio, en **Operations Management Suite**, en el panel de **Administración**.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-126">After you install the Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in the **Administration** pane.</span></span> 

<span data-ttu-id="7cbdf-127">Para configurar la integración de Mapa de servicio, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7cbdf-127">To configure Service Map integration, do the following:</span></span>

1. <span data-ttu-id="7cbdf-128">Para abrir el asistente para configuración, en el panel de **información general de Mapa de servicio**, haga clic en **Agregar área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-128">To open the configuration wizard, in the **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Panel de información general de Mapa de servicio](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="7cbdf-130">En la ventana **Configuración de la conexión**, escriba el identificador o el nombre del inquilino, el identificador de la aplicación (también conocido como nombre de usuario o identificador de cliente) y la contraseña de la entidad de servicio; a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-130">In the **Connection Configuration** window, enter the tenant name or ID, application ID (also known as the username or clientID), and password of the service principal, and then click **Next**.</span></span> <span data-ttu-id="7cbdf-131">Para más información, vaya a [Create a service principal](#creating-a-service-principal) (Creación de una entidad de servicio).</span><span class="sxs-lookup"><span data-stu-id="7cbdf-131">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

    ![Ventana de configuración de la conexión](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="7cbdf-133">En la ventana de **selección de suscripción**, seleccione la suscripción de Azure, el grupo de recursos de Azure (el que contiene el área de trabajo de Operations Management Suite) y el área de trabajo de Operations Management Suite; a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-133">In the **Subscription Selection** window, select the Azure subscription, Azure resource group (the one that contains the Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Área de trabajo de configuración de Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="7cbdf-135">En la ventana **Selección de Grupo de máquinas**, elija los grupos de máquinas de Service Map que desea sincronizar con Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-135">In the **Machine Group Selection** window, you choose which Service Map Machine Groups you want to sync to Operations Manager.</span></span> <span data-ttu-id="7cbdf-136">Haga clic en **Agregar o quitar Grupos de máquinas**, seleccione los grupos de la lista de **Grupos de máquinas disponibles** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-136">Click **Add/Remove Machine Groups**, choose groups from the list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="7cbdf-137">Cuando haya terminado la selección de grupos, haga clic en **Aceptar** para finalizar.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-137">When you are finished selecting groups, click **Ok** to finish.</span></span>
    
    ![Configuración de grupos de máquinas de Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="7cbdf-139">En la ventana **Selección de servidor**, se puede configurar el grupo de servidores de Mapa de servicio con los servidores que desea sincronizar entre Operations Manager y Mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-139">In the **Server Selection** window, you configure the Service Map Servers Group with the servers that you want to sync between Operations Manager and Service Map.</span></span> <span data-ttu-id="7cbdf-140">Haga clic en **Agregar o quitar servidores**.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="7cbdf-141">Para que la integración genere un diagrama de aplicación distribuida para un servidor, el servidor debe cumplir lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7cbdf-141">For the integration to build a distributed application diagram for a server, the server must be:</span></span>

    * <span data-ttu-id="7cbdf-142">Administrado por Operations Manager</span><span class="sxs-lookup"><span data-stu-id="7cbdf-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="7cbdf-143">Administrado por Service Map</span><span class="sxs-lookup"><span data-stu-id="7cbdf-143">Managed by Service Map</span></span>
    * <span data-ttu-id="7cbdf-144">Aparece en el grupo de servidores de Service Map</span><span class="sxs-lookup"><span data-stu-id="7cbdf-144">Listed in the Service Map Servers Group</span></span>

    ![Grupo de configuración de Operations Manager](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="7cbdf-146">Opcional: seleccione el grupo de recursos del servidor de administración para comunicarse con Operations Management Suite y haga clic en **Agregar área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-146">Optional: Select the Management Server resource pool to communicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Grupo de recursos de configuración de Operations Manager](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="7cbdf-148">Es posible que el proceso de configuración y registro del área de trabajo de Operations Management Suite tarde un minuto.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-148">It might take a minute to configure and register the Operations Management Suite workspace.</span></span> <span data-ttu-id="7cbdf-149">Una vez configurado, Operations Manager inicia la primera sincronización de Mapa de servicio desde Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-149">After it is configured, Operations Manager initiates the first Service Map sync from Operations Management Suite.</span></span>

    ![Grupo de recursos de configuración de Operations Manager](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="7cbdf-151">Supervisión del Mapa de servicio</span><span class="sxs-lookup"><span data-stu-id="7cbdf-151">Monitor Service Map</span></span>
<span data-ttu-id="7cbdf-152">Después de conectar el área de trabajo de Operations Management Suite, una nueva carpeta (Mapa de servicio) aparece en el panel **Supervisión** de la consola de Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-152">After the Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in the **Monitoring** pane of the Operations Manager console.</span></span>

![Panel de supervisión de Operations Manager](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="7cbdf-154">La carpeta de Service Map tiene cuatro nodos:</span><span class="sxs-lookup"><span data-stu-id="7cbdf-154">The Service Map folder has four nodes:</span></span>
* <span data-ttu-id="7cbdf-155">**Alertas activas**: muestra todas las alertas activas sobre la comunicación entre Operations Manager y Service Map.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-155">**Active Alerts**: Lists all the active alerts about the communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="7cbdf-156">Observe que estas alertas no son alertas de Operations Management Suite sincronizadas con Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-156">Note that these alerts are not Operations Management Suite alerts being synced to Operations Manager.</span></span> 

* <span data-ttu-id="7cbdf-157">**Servidores**: muestra los servidores supervisados que se han configurado para la sincronización con Mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-157">**Servers**: Lists the monitored servers that are configured to sync from Service Map.</span></span>

    ![Panel de servidores de supervisión de Operations Manager](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="7cbdf-159">**Vistas de dependencia de grupo de máquinas**: muestra todos los grupos de máquinas que se sincronizan desde Service Map.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="7cbdf-160">Puede hacer clic en cualquier grupo para ver su diagrama de aplicaciones distribuidas.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-160">You can click any group to view its distributed application diagram.</span></span>

    ![Diagrama de aplicaciones distribuidas de Operations Manager](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="7cbdf-162">**Vistas de la dependencia de servidor**: muestra todos los servidores que se sincronizan desde Mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="7cbdf-163">Puede hacer clic en cualquier servidor para ver su diagrama de aplicaciones distribuidas.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-163">You can click any server to view its distributed application diagram.</span></span>

    ![Diagrama de aplicaciones distribuidas de Operations Manager](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-the-workspace"></a><span data-ttu-id="7cbdf-165">Edición o eliminación del área de trabajo</span><span class="sxs-lookup"><span data-stu-id="7cbdf-165">Edit or delete the workspace</span></span>
<span data-ttu-id="7cbdf-166">Puede editar o eliminar el área de trabajo configurada desde el panel de **información general de Mapa de servicio** (panel **Administración** > **Operations Management Suite** > **Mapa de servicio**).</span><span class="sxs-lookup"><span data-stu-id="7cbdf-166">You can edit or delete the configured workspace through the **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="7cbdf-167">Puede configurar solo un área de trabajo de Operations Management Suite por ahora.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![Panel de edición de área de trabajo de Operations Manager](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="7cbdf-169">Configuración de reglas e invalidaciones</span><span class="sxs-lookup"><span data-stu-id="7cbdf-169">Configure rules and overrides</span></span>
<span data-ttu-id="7cbdf-170">Se crea una regla, _Microsoft.SystemCenter.ServiceMapImport.Rule_, para capturar información periódicamente de Mapa de servicio.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created to periodically fetch information from Service Map.</span></span> <span data-ttu-id="7cbdf-171">Para cambiar los intervalos de sincronización, puede configurar las invalidaciones de la regla (panel **Creación** > **Reglas** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="7cbdf-171">To change sync timings, you can configure overrides of the rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![Ventana de propiedades de invalidaciones de Operations Manager](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="7cbdf-173">**Enabled**: sirve para habilitar o deshabilitar las actualizaciones automáticas.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="7cbdf-174">**IntervalMinutes**: restablece el tiempo entre actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-174">**IntervalMinutes**: Reset the time between updates.</span></span> <span data-ttu-id="7cbdf-175">El intervalo predeterminado es de una hora.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-175">The default interval is one hour.</span></span> <span data-ttu-id="7cbdf-176">Si desea sincronizar asignaciones de servidor con más frecuencia, puede cambiar el valor.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-176">If you want to sync server maps more frequently, you can change the value.</span></span>
* <span data-ttu-id="7cbdf-177">**TimeoutSeconds**: restablece el período de tiempo antes de que se agote el tiempo de espera de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-177">**TimeoutSeconds**: Reset the length of time before the request times out.</span></span> 
* <span data-ttu-id="7cbdf-178">**TimeWindowMinutes**: restablece el período de tiempo para consultar datos.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-178">**TimeWindowMinutes**: Reset the time window for querying data.</span></span> <span data-ttu-id="7cbdf-179">El valor predeterminado es de 60 minutos.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-179">Default is a 60-minute window.</span></span> <span data-ttu-id="7cbdf-180">El valor máximo permitido por Mapa de servicio es de 60 minutos.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-180">The maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="7cbdf-181">Problemas conocidos y limitaciones</span><span class="sxs-lookup"><span data-stu-id="7cbdf-181">Known issues and limitations</span></span>

<span data-ttu-id="7cbdf-182">El diseño actual presenta los problemas y limitaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="7cbdf-182">The current design presents the following issues and limitations:</span></span>
* <span data-ttu-id="7cbdf-183">Puede conectarse a una sola área de trabajo de Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-183">You can only connect to a single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="7cbdf-184">Aunque puede agregar servidores manualmente al grupo de servidores de Service Map desde el panel **Creación**, las asignaciones para esos servidores no se sincronizan inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-184">Although you can add servers to the Service Map Servers Group manually through the **Authoring** pane, the maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="7cbdf-185">Se sincronizarán desde Service Map durante el siguiente ciclo de sincronización.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-185">They will be synced from Service Map during the next sync cycle.</span></span>
* <span data-ttu-id="7cbdf-186">Si realiza cambios en los diagramas de aplicación distribuida creados por el módulo de administración, es probable que se sobrescriban esos cambios en la próxima sincronización con Service Map.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-186">If you make any changes to the Distributed Application Diagrams created by the management pack, those changes will likely be overwritten on the next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="7cbdf-187">Creación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="7cbdf-187">Create a service principal</span></span>
<span data-ttu-id="7cbdf-188">Para obtener documentación oficial de Azure acerca de cómo crear una entidad de servicio, consulte:</span><span class="sxs-lookup"><span data-stu-id="7cbdf-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="7cbdf-189">Uso de Azure PowerShell para crear una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="7cbdf-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="7cbdf-190">Uso de la CLI de Azure para crear a una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="7cbdf-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* <span data-ttu-id="7cbdf-191">[Create a service principal by using the Azure portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal) (Uso de Azure Portal para crear una entidad de servicio)</span><span class="sxs-lookup"><span data-stu-id="7cbdf-191">[Create a service principal by using the Azure portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)</span></span>

### <a name="feedback"></a><span data-ttu-id="7cbdf-192">Comentarios</span><span class="sxs-lookup"><span data-stu-id="7cbdf-192">Feedback</span></span>
<span data-ttu-id="7cbdf-193">¿Quiere hacernos llegar algún comentario acerca de Mapa de servicio o esta documentación?</span><span class="sxs-lookup"><span data-stu-id="7cbdf-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="7cbdf-194">Visite nuestra [página Voz del usuario](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), donde puede sugerir características o votar sugerencias existentes.</span><span class="sxs-lookup"><span data-stu-id="7cbdf-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
