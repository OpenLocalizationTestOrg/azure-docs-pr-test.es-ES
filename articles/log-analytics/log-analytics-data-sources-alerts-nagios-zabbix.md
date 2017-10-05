---
title: "Recopilación de alertas de Nagios y Zabbix en Log Analytics de OMS | Microsoft Docs"
description: "Nagios y Zabbix son herramientas de supervisión de código abierto. Con estas herramientas, puede recopilar alertas en Log Analytics con el fin de analizarlas, y también alertas de otros orígenes.  En este artículo se describe cómo configurar al agente de OMS para Linux para recopilar alertas de estos sistemas."
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
ms.openlocfilehash: 0b64c32e1031e704d50aab0b38eaea41e27d134b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="0f4dd-105">Recopilación de alertas de Nagios y Zabbix en Log Analytics desde el agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="0f4dd-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="0f4dd-106">[Nagios](https://www.nagios.org/) y [Zabbix](http://www.zabbix.com/) son herramientas de supervisión de código abierto.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="0f4dd-107">Con estas herramientas, puede recopilar alertas en Log Analytics con el fin de analizarlas, y [también alertas de otros orígenes](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="0f4dd-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="0f4dd-108">En este artículo se describe cómo configurar al agente de OMS para Linux para recopilar alertas de estos sistemas.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="0f4dd-109">Configuración de la recopilación de alertas</span><span class="sxs-lookup"><span data-stu-id="0f4dd-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="0f4dd-110">Configuración de la recopilación de alertas de Nagios</span><span class="sxs-lookup"><span data-stu-id="0f4dd-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="0f4dd-111">Realice los pasos siguientes en el servidor Nagios para recopilar alertas.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-111">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="0f4dd-112">Conceda al usuario acceso de lectura de **omsagent** al archivo de registro de Nagios (es decir, `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="0f4dd-112">Grant the user **omsagent** read access to the Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="0f4dd-113">Suponiendo que el archivo nagios.log es propiedad del grupo `nagios`, puede agregar al usuario **omsagent** al grupo **nagios**.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-113">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span></span> 

    <span data-ttu-id="0f4dd-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="0f4dd-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="0f4dd-115">Modifique el archivo de configuración en (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="0f4dd-115">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="0f4dd-116">Asegúrese de que las entradas siguientes están presentes y no comentadas:</span><span class="sxs-lookup"><span data-stu-id="0f4dd-116">Ensure the following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path to point to your nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="0f4dd-117">Reinicio del demonio de omsagent</span><span class="sxs-lookup"><span data-stu-id="0f4dd-117">Restart the omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="0f4dd-118">Configuración de la recopilación de alertas de Zabbix</span><span class="sxs-lookup"><span data-stu-id="0f4dd-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="0f4dd-119">Para recopilar alertas de un servidor de Zabbix, debe especificar un usuario y una contraseña en *texto sin formato*.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-119">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="0f4dd-120">Aunque esto no es lo idóneo, se recomienda que cree el usuario y conceda permisos solo de supervisión.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-120">This is not ideal, but we recommend that you create the user and grant permissions to monitor onlu.</span></span>

<span data-ttu-id="0f4dd-121">Realice los pasos siguientes en el servidor Nagios para recopilar alertas.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-121">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="0f4dd-122">Modifique el archivo de configuración en (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="0f4dd-122">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="0f4dd-123">Asegúrese de que las entradas siguientes están presentes y no tienen comentarios:</span><span class="sxs-lookup"><span data-stu-id="0f4dd-123">Ensure the following entries are present and not commented out.</span></span>  <span data-ttu-id="0f4dd-124">Cambie el nombre de usuario y la contraseña por los valores de su entorno de Zabbix.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-124">Change the user name and password to values for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="0f4dd-125">Reinicio del demonio de omsagent</span><span class="sxs-lookup"><span data-stu-id="0f4dd-125">Restart the omsagent daemon</span></span>

    <span data-ttu-id="0f4dd-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="0f4dd-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="0f4dd-127">Registros de alerta</span><span class="sxs-lookup"><span data-stu-id="0f4dd-127">Alert records</span></span>
<span data-ttu-id="0f4dd-128">Puede recuperar registros de alertas de Nagios y Zabbix con [búsquedas de registros](log-analytics-log-searches.md) en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="0f4dd-129">Registros de alertas de Nagios</span><span class="sxs-lookup"><span data-stu-id="0f4dd-129">Nagios Alert records</span></span>

<span data-ttu-id="0f4dd-130">Los registros de alertas recopilados por Nagios tienen como **tipo** una **alerta** y como **SourceSystem****Nagios**.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="0f4dd-131">Tienen las propiedades de la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-131">They have the properties in the following table.</span></span>

| <span data-ttu-id="0f4dd-132">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0f4dd-132">Property</span></span> | <span data-ttu-id="0f4dd-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="0f4dd-133">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0f4dd-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="0f4dd-134">Type</span></span> |<span data-ttu-id="0f4dd-135">*Alerta*</span><span class="sxs-lookup"><span data-stu-id="0f4dd-135">*Alert*</span></span> |
| <span data-ttu-id="0f4dd-136">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="0f4dd-136">SourceSystem</span></span> |<span data-ttu-id="0f4dd-137">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="0f4dd-137">*Nagios*</span></span> |
| <span data-ttu-id="0f4dd-138">AlertName</span><span class="sxs-lookup"><span data-stu-id="0f4dd-138">AlertName</span></span> |<span data-ttu-id="0f4dd-139">Nombre de la alerta</span><span class="sxs-lookup"><span data-stu-id="0f4dd-139">Name of the alert.</span></span> |
| <span data-ttu-id="0f4dd-140">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="0f4dd-140">AlertDescription</span></span> | <span data-ttu-id="0f4dd-141">Descripción de la alerta</span><span class="sxs-lookup"><span data-stu-id="0f4dd-141">Description of the alert.</span></span> |
| <span data-ttu-id="0f4dd-142">AlertState</span><span class="sxs-lookup"><span data-stu-id="0f4dd-142">AlertState</span></span> | <span data-ttu-id="0f4dd-143">Estado del servicio o host.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-143">Status of the service or host.</span></span><br><br><span data-ttu-id="0f4dd-144">OK</span><span class="sxs-lookup"><span data-stu-id="0f4dd-144">OK</span></span><br><span data-ttu-id="0f4dd-145">ADVERTENCIA</span><span class="sxs-lookup"><span data-stu-id="0f4dd-145">WARNING</span></span><br><span data-ttu-id="0f4dd-146">ARRIBA</span><span class="sxs-lookup"><span data-stu-id="0f4dd-146">UP</span></span><br><span data-ttu-id="0f4dd-147">ABAJO</span><span class="sxs-lookup"><span data-stu-id="0f4dd-147">DOWN</span></span> |
| <span data-ttu-id="0f4dd-148">HostName</span><span class="sxs-lookup"><span data-stu-id="0f4dd-148">HostName</span></span> | <span data-ttu-id="0f4dd-149">Nombre del host que creó la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-149">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="0f4dd-150">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="0f4dd-150">PriorityNumber</span></span> | <span data-ttu-id="0f4dd-151">Nivel de prioridad de la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-151">Priority level of the alert.</span></span> |
| <span data-ttu-id="0f4dd-152">StateType</span><span class="sxs-lookup"><span data-stu-id="0f4dd-152">StateType</span></span> | <span data-ttu-id="0f4dd-153">El tipo de estado de la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-153">The type of state of the alert.</span></span><br><br><span data-ttu-id="0f4dd-154">SOFT: problema que no se ha vuelto a comprobar.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-154">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="0f4dd-155">HARD: problema que se ha vuelto a comprobar un número de veces especificado.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-155">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="0f4dd-156">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="0f4dd-156">TimeGenerated</span></span> |<span data-ttu-id="0f4dd-157">Fecha y hora en que se creó la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-157">Date and time the alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="0f4dd-158">Registros de alertas de Zabbix</span><span class="sxs-lookup"><span data-stu-id="0f4dd-158">Zabbix alert records</span></span>
<span data-ttu-id="0f4dd-159">Los registros de alertas recopilados por Zabbix tienen como **tipo** una **alerta** y como **SourceSystem****Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="0f4dd-160">Tienen las propiedades de la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-160">They have the properties in the following table.</span></span>

| <span data-ttu-id="0f4dd-161">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0f4dd-161">Property</span></span> | <span data-ttu-id="0f4dd-162">Descripción</span><span class="sxs-lookup"><span data-stu-id="0f4dd-162">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0f4dd-163">Tipo</span><span class="sxs-lookup"><span data-stu-id="0f4dd-163">Type</span></span> |<span data-ttu-id="0f4dd-164">*Alerta*</span><span class="sxs-lookup"><span data-stu-id="0f4dd-164">*Alert*</span></span> |
| <span data-ttu-id="0f4dd-165">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="0f4dd-165">SourceSystem</span></span> |<span data-ttu-id="0f4dd-166">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="0f4dd-166">*Zabbix*</span></span> |
| <span data-ttu-id="0f4dd-167">AlertName</span><span class="sxs-lookup"><span data-stu-id="0f4dd-167">AlertName</span></span> | <span data-ttu-id="0f4dd-168">Nombre de la alerta</span><span class="sxs-lookup"><span data-stu-id="0f4dd-168">Name of the alert.</span></span> |
| <span data-ttu-id="0f4dd-169">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="0f4dd-169">AlertPriority</span></span> | <span data-ttu-id="0f4dd-170">Gravedad de la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-170">Severity of the alert.</span></span><br><br><span data-ttu-id="0f4dd-171">no clasificada</span><span class="sxs-lookup"><span data-stu-id="0f4dd-171">not classified</span></span><br><span data-ttu-id="0f4dd-172">informativo</span><span class="sxs-lookup"><span data-stu-id="0f4dd-172">information</span></span><br><span data-ttu-id="0f4dd-173">Warning (Advertencia)</span><span class="sxs-lookup"><span data-stu-id="0f4dd-173">warning</span></span><br><span data-ttu-id="0f4dd-174">average</span><span class="sxs-lookup"><span data-stu-id="0f4dd-174">average</span></span><br><span data-ttu-id="0f4dd-175">alta</span><span class="sxs-lookup"><span data-stu-id="0f4dd-175">high</span></span><br><span data-ttu-id="0f4dd-176">desastre</span><span class="sxs-lookup"><span data-stu-id="0f4dd-176">disaster</span></span>  |
| <span data-ttu-id="0f4dd-177">AlertState</span><span class="sxs-lookup"><span data-stu-id="0f4dd-177">AlertState</span></span> | <span data-ttu-id="0f4dd-178">Estado de la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-178">State of the alert.</span></span><br><br><span data-ttu-id="0f4dd-179">0: el estado está actualizado.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-179">0 - State is up to date.</span></span><br><span data-ttu-id="0f4dd-180">1: el estado es desconocido.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-180">1 - State is unknown.</span></span>  |
| <span data-ttu-id="0f4dd-181">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="0f4dd-181">AlertTypeNumber</span></span> | <span data-ttu-id="0f4dd-182">Especifica si la alerta puede generar varios eventos de problema.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-182">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="0f4dd-183">0: el estado está actualizado.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-183">0 - State is up to date.</span></span><br><span data-ttu-id="0f4dd-184">1: el estado es desconocido.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-184">1 - State is unknown.</span></span>    |
| <span data-ttu-id="0f4dd-185">Comentarios</span><span class="sxs-lookup"><span data-stu-id="0f4dd-185">Comments</span></span> | <span data-ttu-id="0f4dd-186">Comentarios adicionales de la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-186">Additional comments for alert.</span></span> |
| <span data-ttu-id="0f4dd-187">HostName</span><span class="sxs-lookup"><span data-stu-id="0f4dd-187">HostName</span></span> | <span data-ttu-id="0f4dd-188">Nombre del host que creó la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-188">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="0f4dd-189">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="0f4dd-189">PriorityNumber</span></span> | <span data-ttu-id="0f4dd-190">Valor que indica la gravedad de la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-190">Value indicating severity of the alert.</span></span><br><br><span data-ttu-id="0f4dd-191">0: no clasificada</span><span class="sxs-lookup"><span data-stu-id="0f4dd-191">0 - not classified</span></span><br><span data-ttu-id="0f4dd-192">1: información</span><span class="sxs-lookup"><span data-stu-id="0f4dd-192">1 - information</span></span><br><span data-ttu-id="0f4dd-193">2: advertencia</span><span class="sxs-lookup"><span data-stu-id="0f4dd-193">2 - warning</span></span><br><span data-ttu-id="0f4dd-194">3: promedio</span><span class="sxs-lookup"><span data-stu-id="0f4dd-194">3 - average</span></span><br><span data-ttu-id="0f4dd-195">4: alta</span><span class="sxs-lookup"><span data-stu-id="0f4dd-195">4 - high</span></span><br><span data-ttu-id="0f4dd-196">5: desastre</span><span class="sxs-lookup"><span data-stu-id="0f4dd-196">5 - disaster</span></span> |
| <span data-ttu-id="0f4dd-197">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="0f4dd-197">TimeGenerated</span></span> |<span data-ttu-id="0f4dd-198">Fecha y hora en que se creó la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-198">Date and time the alert was created.</span></span> |
| <span data-ttu-id="0f4dd-199">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="0f4dd-199">TimeLastModified</span></span> |<span data-ttu-id="0f4dd-200">Fecha y hora en que se cambió por última vez el estado de la alerta.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-200">Date and time the state of the alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="0f4dd-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f4dd-201">Next steps</span></span>
* <span data-ttu-id="0f4dd-202">Más información sobre las [alertas](log-analytics-alerts.md) en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="0f4dd-203">Obtenga información acerca de las [búsquedas de registros](log-analytics-log-searches.md) para analizar los datos recopilados de las soluciones y los orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="0f4dd-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
