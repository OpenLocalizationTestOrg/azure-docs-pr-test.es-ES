---
title: "datos de aaaCollect de CollectD en análisis de registros de OMS | Documentos de Microsoft"
description: "CollectD es un demonio de Linux de código abierto que recopila periódicamente datos de aplicaciones e información de nivel de sistema.  En este artículo se proporciona información sobre la recopilación de datos de CollectD en Log Analytics."
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
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="7b7f2-104">Recopilación de datos de CollectD en agentes de Linux en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7b7f2-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="7b7f2-105">[CollectD](https://collectd.org/) es un demonio de Linux de código abierto que recopila periódicamente métricas de rendimiento de aplicaciones e información de nivel de sistema.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="7b7f2-106">Aplicaciones de ejemplo incluyen hello Máquina Virtual Java (JVM), MySQL Server y Nginx.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="7b7f2-107">En este artículo se proporciona información sobre la recopilación de datos de rendimiento de CollectD en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="7b7f2-108">Puede encontrar una lista completa de los complementos disponibles en la [tabla de complementos](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="7b7f2-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Introducción a CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="7b7f2-110">Hello configuración CollectD siguiente se incluye en hello agente de OMS para Linux tooroute CollectD datos toohello agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="7b7f2-111">Además, si usa un versiones de collectD antes de 5.5 usar hello siguiente configuración en su lugar.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="7b7f2-112">configuración de Hello CollectD usa predeterminado de hello`write_http` toosend de complemento de los datos de rendimiento métrica a través del puerto 26000 tooOMS agente para Linux.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="7b7f2-113">Este puerto puede ser el puerto configurado tooa personalizado si es necesario.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="7b7f2-114">Hola agente de OMS para Linux también escucha en el puerto 26000 para las métricas de CollectD y, a continuación, convierte las métricas de esquema tooOMS.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="7b7f2-115">Hello aquí te mostramos hello agente de OMS para Linux configuración `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="7b7f2-116">Versiones admitidas</span><span class="sxs-lookup"><span data-stu-id="7b7f2-116">Versions supported</span></span>
- <span data-ttu-id="7b7f2-117">Log Analytics admite actualmente las versiones de CollectD 4.8 y superior.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="7b7f2-118">Para la recopilación de métricas de CollectD, se requiere el agente de OMS para Linux v1.1.0-217 o superior.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="7b7f2-119">Configuración</span><span class="sxs-lookup"><span data-stu-id="7b7f2-119">Configuration</span></span>
<span data-ttu-id="7b7f2-120">siguiente Hola es colección de tooconfigure de pasos básicos de los datos de CollectD de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="7b7f2-121">Configurar CollectD toosend datos toohello agente de OMS para Linux mediante el complemento de write_http Hola.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="7b7f2-122">Configurar hello agente de OMS para Linux toolisten para hello CollectD datos en el puerto adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="7b7f2-123">Reinicie CollectD y el agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="7b7f2-124">Configurar CollectD tooforward datos</span><span class="sxs-lookup"><span data-stu-id="7b7f2-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="7b7f2-125">tooroute CollectD datos toohello agente de OMS para Linux, `oms.conf` necesidades toobe agrega el directorio de configuración del tooCollectD.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="7b7f2-126">destino de Hola de este archivo depende de Hola de distribución de Linux de su equipo.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="7b7f2-127">Si su directorio de configuración de CollectD está ubicado en /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="7b7f2-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="7b7f2-128">Si su directorio de configuración de CollectD está ubicado en /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="7b7f2-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="7b7f2-129">Para las versiones de CollectD anteriores 5.5 tendrá etiquetas de hello toomodify en `oms.conf` como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="7b7f2-130">Copie el directorio de configuración de omsagent collectd.conf toohello deseado del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="7b7f2-131">Reinicie CollectD y agente de OMS para Linux con hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="7b7f2-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="7b7f2-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="7b7f2-133">Las métricas de CollectD tooLog conversión de esquema de análisis</span><span class="sxs-lookup"><span data-stu-id="7b7f2-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="7b7f2-134">toomaintain un modelo familiar entre las métricas de infraestructura que ya se han recopilado por el agente de OMS para Linux y Hola nuevas métricas recopilados por CollectD Hola después de la asignación de esquema se utiliza:</span><span class="sxs-lookup"><span data-stu-id="7b7f2-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="7b7f2-135">Campo de métrica de CollectD</span><span class="sxs-lookup"><span data-stu-id="7b7f2-135">CollectD Metric field</span></span> | <span data-ttu-id="7b7f2-136">Campo de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7b7f2-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="7b7f2-137">host</span><span class="sxs-lookup"><span data-stu-id="7b7f2-137">host</span></span> | <span data-ttu-id="7b7f2-138">Equipo</span><span class="sxs-lookup"><span data-stu-id="7b7f2-138">Computer</span></span> |
| <span data-ttu-id="7b7f2-139">complemento</span><span class="sxs-lookup"><span data-stu-id="7b7f2-139">plugin</span></span> | <span data-ttu-id="7b7f2-140">None</span><span class="sxs-lookup"><span data-stu-id="7b7f2-140">None</span></span> |
| <span data-ttu-id="7b7f2-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="7b7f2-141">plugin_instance</span></span> | <span data-ttu-id="7b7f2-142">Nombre de instancia</span><span class="sxs-lookup"><span data-stu-id="7b7f2-142">Instance Name</span></span><br><span data-ttu-id="7b7f2-143">Si **plugin_instance** es *null*, entonces InstanceName ="*_Total*".</span><span class="sxs-lookup"><span data-stu-id="7b7f2-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="7b7f2-144">type</span><span class="sxs-lookup"><span data-stu-id="7b7f2-144">type</span></span> | <span data-ttu-id="7b7f2-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="7b7f2-145">ObjectName</span></span> |
| <span data-ttu-id="7b7f2-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="7b7f2-146">type_instance</span></span> | <span data-ttu-id="7b7f2-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="7b7f2-147">CounterName</span></span><br><span data-ttu-id="7b7f2-148">Si **type_instance** es *null*, entonces CounterName=**en blanco**.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="7b7f2-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="7b7f2-149">dsnames[]</span></span> | <span data-ttu-id="7b7f2-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="7b7f2-150">CounterName</span></span> |
| <span data-ttu-id="7b7f2-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="7b7f2-151">dstypes</span></span> | <span data-ttu-id="7b7f2-152">None</span><span class="sxs-lookup"><span data-stu-id="7b7f2-152">None</span></span> |
| <span data-ttu-id="7b7f2-153">values[]</span><span class="sxs-lookup"><span data-stu-id="7b7f2-153">values[]</span></span> | <span data-ttu-id="7b7f2-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="7b7f2-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7b7f2-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b7f2-155">Next steps</span></span>
* <span data-ttu-id="7b7f2-156">Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="7b7f2-157">Use [campos personalizados](log-analytics-custom-fields.md) tooparse datos de registros de syslog en campos individuales.</span><span class="sxs-lookup"><span data-stu-id="7b7f2-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

