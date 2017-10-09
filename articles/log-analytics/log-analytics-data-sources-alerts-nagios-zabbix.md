---
title: "las alertas de Nagios y Zabbix aaaCollect en análisis de registros de OMS | Documentos de Microsoft"
description: "Nagios y Zabbix son herramientas de supervisión de código abierto. Puede recopilar alertas de estas herramientas en el análisis de registros en orden tooanalyze ellos junto con las alertas de otros orígenes.  Este artículo describe cómo tooconfigure hello agente de OMS para Linux toocollect alertas desde estos sistemas."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="1d287-105">Recopilación de alertas de Nagios y Zabbix en Log Analytics desde el agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="1d287-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="1d287-106">[Nagios](https://www.nagios.org/) y [Zabbix](http://www.zabbix.com/) son herramientas de supervisión de código abierto.</span><span class="sxs-lookup"><span data-stu-id="1d287-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="1d287-107">Puede recopilar las alertas de estas herramientas en análisis de registros en orden tooanalyze junto con [alertas procedentes de otros orígenes](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1d287-107">You can collect alerts from these tools into Log Analytics in order tooanalyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="1d287-108">Este artículo describe cómo tooconfigure hello agente de OMS para Linux toocollect alertas desde estos sistemas.</span><span class="sxs-lookup"><span data-stu-id="1d287-108">This article describes how tooconfigure hello OMS Agent for Linux toocollect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="1d287-109">Configuración de la recopilación de alertas</span><span class="sxs-lookup"><span data-stu-id="1d287-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="1d287-110">Configuración de la recopilación de alertas de Nagios</span><span class="sxs-lookup"><span data-stu-id="1d287-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="1d287-111">Realizar Hola seguir pasos de alertas de hello Nagios server toocollect.</span><span class="sxs-lookup"><span data-stu-id="1d287-111">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="1d287-112">Usuario de hello GRANT **omsagent** archivo de registro de acceso de lectura toohello Nagios (es decir, `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="1d287-112">Grant hello user **omsagent** read access toohello Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="1d287-113">Suponiendo que el archivo de hello nagios.log es propiedad de grupo hello `nagios`, puede agregar el usuario hello **omsagent** toohello **nagios** grupo.</span><span class="sxs-lookup"><span data-stu-id="1d287-113">Assuming hello nagios.log file is owned by hello group `nagios`, you can add hello user **omsagent** toohello **nagios** group.</span></span> 

    <span data-ttu-id="1d287-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="1d287-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="1d287-115">Modificar el archivo de configuración de hello en (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="1d287-115">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="1d287-116">Asegúrese de hello siguiendo las entradas está presentes y no comentadas:</span><span class="sxs-lookup"><span data-stu-id="1d287-116">Ensure hello following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="1d287-117">Reiniciar el demonio omsagent Hola</span><span class="sxs-lookup"><span data-stu-id="1d287-117">Restart hello omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="1d287-118">Configuración de la recopilación de alertas de Zabbix</span><span class="sxs-lookup"><span data-stu-id="1d287-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="1d287-119">toocollect las alertas de un servidor Zabbix, deberá toospecify un usuario y una contraseña en *borre el texto*.</span><span class="sxs-lookup"><span data-stu-id="1d287-119">toocollect alerts from a Zabbix server, you need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="1d287-120">Esto no es lo ideal, pero se recomienda que cree el usuario de Hola y conceder permisos toomonitor onlu.</span><span class="sxs-lookup"><span data-stu-id="1d287-120">This is not ideal, but we recommend that you create hello user and grant permissions toomonitor onlu.</span></span>

<span data-ttu-id="1d287-121">Realizar Hola seguir pasos de alertas de hello Nagios server toocollect.</span><span class="sxs-lookup"><span data-stu-id="1d287-121">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="1d287-122">Modificar el archivo de configuración de hello en (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="1d287-122">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="1d287-123">Asegúrese de hello siguiendo las entradas está presentes y no comentado.  Cambiar toovalues de nombre y la contraseña del usuario de hello para el entorno de Zabbix.</span><span class="sxs-lookup"><span data-stu-id="1d287-123">Ensure hello following entries are present and not commented out.  Change hello user name and password toovalues for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="1d287-124">Reiniciar el demonio omsagent Hola</span><span class="sxs-lookup"><span data-stu-id="1d287-124">Restart hello omsagent daemon</span></span>

    <span data-ttu-id="1d287-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="1d287-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="1d287-126">Registros de alerta</span><span class="sxs-lookup"><span data-stu-id="1d287-126">Alert records</span></span>
<span data-ttu-id="1d287-127">Puede recuperar registros de alertas de Nagios y Zabbix con [búsquedas de registros](log-analytics-log-searches.md) en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1d287-127">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="1d287-128">Registros de alertas de Nagios</span><span class="sxs-lookup"><span data-stu-id="1d287-128">Nagios Alert records</span></span>

<span data-ttu-id="1d287-129">Los registros de alertas recopilados por Nagios tienen como **tipo** una **alerta** y como **SourceSystem****Nagios**.</span><span class="sxs-lookup"><span data-stu-id="1d287-129">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="1d287-130">Tienen propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="1d287-130">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="1d287-131">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1d287-131">Property</span></span> | <span data-ttu-id="1d287-132">Descripción</span><span class="sxs-lookup"><span data-stu-id="1d287-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d287-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="1d287-133">Type</span></span> |<span data-ttu-id="1d287-134">*Alerta*</span><span class="sxs-lookup"><span data-stu-id="1d287-134">*Alert*</span></span> |
| <span data-ttu-id="1d287-135">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1d287-135">SourceSystem</span></span> |<span data-ttu-id="1d287-136">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="1d287-136">*Nagios*</span></span> |
| <span data-ttu-id="1d287-137">AlertName</span><span class="sxs-lookup"><span data-stu-id="1d287-137">AlertName</span></span> |<span data-ttu-id="1d287-138">Nombre de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d287-138">Name of hello alert.</span></span> |
| <span data-ttu-id="1d287-139">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="1d287-139">AlertDescription</span></span> | <span data-ttu-id="1d287-140">Descripción de la alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d287-140">Description of hello alert.</span></span> |
| <span data-ttu-id="1d287-141">AlertState</span><span class="sxs-lookup"><span data-stu-id="1d287-141">AlertState</span></span> | <span data-ttu-id="1d287-142">Estado del servicio de Hola o host.</span><span class="sxs-lookup"><span data-stu-id="1d287-142">Status of hello service or host.</span></span><br><br><span data-ttu-id="1d287-143">OK</span><span class="sxs-lookup"><span data-stu-id="1d287-143">OK</span></span><br><span data-ttu-id="1d287-144">ADVERTENCIA</span><span class="sxs-lookup"><span data-stu-id="1d287-144">WARNING</span></span><br><span data-ttu-id="1d287-145">ARRIBA</span><span class="sxs-lookup"><span data-stu-id="1d287-145">UP</span></span><br><span data-ttu-id="1d287-146">ABAJO</span><span class="sxs-lookup"><span data-stu-id="1d287-146">DOWN</span></span> |
| <span data-ttu-id="1d287-147">HostName</span><span class="sxs-lookup"><span data-stu-id="1d287-147">HostName</span></span> | <span data-ttu-id="1d287-148">Nombre del host de Hola que creó Hola alerta.</span><span class="sxs-lookup"><span data-stu-id="1d287-148">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="1d287-149">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="1d287-149">PriorityNumber</span></span> | <span data-ttu-id="1d287-150">Nivel de prioridad de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d287-150">Priority level of hello alert.</span></span> |
| <span data-ttu-id="1d287-151">StateType</span><span class="sxs-lookup"><span data-stu-id="1d287-151">StateType</span></span> | <span data-ttu-id="1d287-152">tipo de Hola de estado de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d287-152">hello type of state of hello alert.</span></span><br><br><span data-ttu-id="1d287-153">SOFT: problema que no se ha vuelto a comprobar.</span><span class="sxs-lookup"><span data-stu-id="1d287-153">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="1d287-154">HARD: problema que se ha vuelto a comprobar un número de veces especificado.</span><span class="sxs-lookup"><span data-stu-id="1d287-154">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="1d287-155">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="1d287-155">TimeGenerated</span></span> |<span data-ttu-id="1d287-156">Se creó la alerta de Hola de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="1d287-156">Date and time hello alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="1d287-157">Registros de alertas de Zabbix</span><span class="sxs-lookup"><span data-stu-id="1d287-157">Zabbix alert records</span></span>
<span data-ttu-id="1d287-158">Los registros de alertas recopilados por Zabbix tienen como **tipo** una **alerta** y como **SourceSystem****Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="1d287-158">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="1d287-159">Tienen propiedades de hello en hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="1d287-159">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="1d287-160">Propiedad</span><span class="sxs-lookup"><span data-stu-id="1d287-160">Property</span></span> | <span data-ttu-id="1d287-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="1d287-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d287-162">Tipo</span><span class="sxs-lookup"><span data-stu-id="1d287-162">Type</span></span> |<span data-ttu-id="1d287-163">*Alerta*</span><span class="sxs-lookup"><span data-stu-id="1d287-163">*Alert*</span></span> |
| <span data-ttu-id="1d287-164">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1d287-164">SourceSystem</span></span> |<span data-ttu-id="1d287-165">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="1d287-165">*Zabbix*</span></span> |
| <span data-ttu-id="1d287-166">AlertName</span><span class="sxs-lookup"><span data-stu-id="1d287-166">AlertName</span></span> | <span data-ttu-id="1d287-167">Nombre de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d287-167">Name of hello alert.</span></span> |
| <span data-ttu-id="1d287-168">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="1d287-168">AlertPriority</span></span> | <span data-ttu-id="1d287-169">Gravedad de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d287-169">Severity of hello alert.</span></span><br><br><span data-ttu-id="1d287-170">no clasificada</span><span class="sxs-lookup"><span data-stu-id="1d287-170">not classified</span></span><br><span data-ttu-id="1d287-171">informativo</span><span class="sxs-lookup"><span data-stu-id="1d287-171">information</span></span><br><span data-ttu-id="1d287-172">Warning (Advertencia)</span><span class="sxs-lookup"><span data-stu-id="1d287-172">warning</span></span><br><span data-ttu-id="1d287-173">average</span><span class="sxs-lookup"><span data-stu-id="1d287-173">average</span></span><br><span data-ttu-id="1d287-174">alta</span><span class="sxs-lookup"><span data-stu-id="1d287-174">high</span></span><br><span data-ttu-id="1d287-175">desastre</span><span class="sxs-lookup"><span data-stu-id="1d287-175">disaster</span></span>  |
| <span data-ttu-id="1d287-176">AlertState</span><span class="sxs-lookup"><span data-stu-id="1d287-176">AlertState</span></span> | <span data-ttu-id="1d287-177">Estado de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d287-177">State of hello alert.</span></span><br><br><span data-ttu-id="1d287-178">0 - estado está activo toodate.</span><span class="sxs-lookup"><span data-stu-id="1d287-178">0 - State is up toodate.</span></span><br><span data-ttu-id="1d287-179">1: el estado es desconocido.</span><span class="sxs-lookup"><span data-stu-id="1d287-179">1 - State is unknown.</span></span>  |
| <span data-ttu-id="1d287-180">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="1d287-180">AlertTypeNumber</span></span> | <span data-ttu-id="1d287-181">Especifica si la alerta puede generar varios eventos de problema.</span><span class="sxs-lookup"><span data-stu-id="1d287-181">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="1d287-182">0 - estado está activo toodate.</span><span class="sxs-lookup"><span data-stu-id="1d287-182">0 - State is up toodate.</span></span><br><span data-ttu-id="1d287-183">1: el estado es desconocido.</span><span class="sxs-lookup"><span data-stu-id="1d287-183">1 - State is unknown.</span></span>    |
| <span data-ttu-id="1d287-184">Comentarios</span><span class="sxs-lookup"><span data-stu-id="1d287-184">Comments</span></span> | <span data-ttu-id="1d287-185">Comentarios adicionales de la alerta.</span><span class="sxs-lookup"><span data-stu-id="1d287-185">Additional comments for alert.</span></span> |
| <span data-ttu-id="1d287-186">HostName</span><span class="sxs-lookup"><span data-stu-id="1d287-186">HostName</span></span> | <span data-ttu-id="1d287-187">Nombre del host de Hola que creó Hola alerta.</span><span class="sxs-lookup"><span data-stu-id="1d287-187">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="1d287-188">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="1d287-188">PriorityNumber</span></span> | <span data-ttu-id="1d287-189">Valor que indica la gravedad de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d287-189">Value indicating severity of hello alert.</span></span><br><br><span data-ttu-id="1d287-190">0: no clasificada</span><span class="sxs-lookup"><span data-stu-id="1d287-190">0 - not classified</span></span><br><span data-ttu-id="1d287-191">1: información</span><span class="sxs-lookup"><span data-stu-id="1d287-191">1 - information</span></span><br><span data-ttu-id="1d287-192">2: advertencia</span><span class="sxs-lookup"><span data-stu-id="1d287-192">2 - warning</span></span><br><span data-ttu-id="1d287-193">3: promedio</span><span class="sxs-lookup"><span data-stu-id="1d287-193">3 - average</span></span><br><span data-ttu-id="1d287-194">4: alta</span><span class="sxs-lookup"><span data-stu-id="1d287-194">4 - high</span></span><br><span data-ttu-id="1d287-195">5: desastre</span><span class="sxs-lookup"><span data-stu-id="1d287-195">5 - disaster</span></span> |
| <span data-ttu-id="1d287-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="1d287-196">TimeGenerated</span></span> |<span data-ttu-id="1d287-197">Se creó la alerta de Hola de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="1d287-197">Date and time hello alert was created.</span></span> |
| <span data-ttu-id="1d287-198">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="1d287-198">TimeLastModified</span></span> |<span data-ttu-id="1d287-199">Estado de Hola de fecha y hora de alerta de Hola se cambió por última vez.</span><span class="sxs-lookup"><span data-stu-id="1d287-199">Date and time hello state of hello alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="1d287-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d287-200">Next steps</span></span>
* <span data-ttu-id="1d287-201">Más información sobre las [alertas](log-analytics-alerts.md) en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1d287-201">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="1d287-202">Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.</span><span class="sxs-lookup"><span data-stu-id="1d287-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
