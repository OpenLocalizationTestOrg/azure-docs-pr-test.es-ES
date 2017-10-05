---
title: "Recopilación de datos JSON personalizados en Log Analytics de OMS | Microsoft Docs"
description: "Los orígenes de datos JSON personalizados se pueden recopilar en Log Analytics mediante el agente de OMS para Linux.  Estos orígenes de datos personalizados pueden ser scripts simples que devuelven JSON, como curl o uno de los más de 300 complementos de FluentD. En este artículo se describe la configuración necesaria para esta recopilación de datos."
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
ms.openlocfilehash: 800ee1269556e7c2d56fbbf2b497c10509b5c78c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="collecting-custom-json-data-sources-with-the-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="78953-105">Recopilación de orígenes de datos JSON personalizados con el agente de OMS para Linux en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="78953-105">Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="78953-106">Los orígenes de datos JSON personalizados se pueden recopilar en Log Analytics mediante el agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="78953-106">Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.</span></span>  <span data-ttu-id="78953-107">Estos orígenes de datos personalizados pueden ser scripts simples que devuelven JSON, como [curl](https://curl.haxx.se/) o uno de los más de [300 complementos de FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="78953-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="78953-108">En este artículo se describe la configuración necesaria para esta recopilación de datos.</span><span class="sxs-lookup"><span data-stu-id="78953-108">This article describes the configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="78953-109">El agente de OMS para Linux v1.1.0-217+ es necesario para los datos JSON personalizados.</span><span class="sxs-lookup"><span data-stu-id="78953-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="78953-110">Configuración</span><span class="sxs-lookup"><span data-stu-id="78953-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="78953-111">Configuración del complemento de entrada</span><span class="sxs-lookup"><span data-stu-id="78953-111">Configure input plugin</span></span>

<span data-ttu-id="78953-112">Para recopilar datos JSON en Log Analytics, agregue `oms.api.` al principio de una etiqueta de FluentD en un complemento de entrada.</span><span class="sxs-lookup"><span data-stu-id="78953-112">To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="78953-113">Por ejemplo, el siguiente es un archivo de configuración independiente `exec-json.conf` en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="78953-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="78953-114">Este archivo usa el complemento `exec` de FuentD para ejecutar un comando de curl cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="78953-114">This uses the FluentD plugin `exec` to run a curl command every 30 seconds.</span></span>  <span data-ttu-id="78953-115">La salida de este comando se recopila mediante el complemento de salida JSON.</span><span class="sxs-lookup"><span data-stu-id="78953-115">The output from this command is collected by the JSON output plugin.</span></span>

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
<span data-ttu-id="78953-116">Será necesario cambiar la propiedad del archivo de configuración agregado bajo `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="78953-116">The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="78953-117">Configuración del complemento de salida</span><span class="sxs-lookup"><span data-stu-id="78953-117">Configure output plugin</span></span> 
<span data-ttu-id="78953-118">Agregue la siguiente configuración de complemento de salida a la configuración principal en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` o como un archivo de configuración independiente colocado en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="78953-118">Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="78953-119">Reinicio del agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="78953-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="78953-120">Reinicie el servicio de agente de OMS para Linux con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="78953-120">Restart the OMS Agent for Linux service with the following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="78953-121">Salida</span><span class="sxs-lookup"><span data-stu-id="78953-121">Output</span></span>
<span data-ttu-id="78953-122">Los datos se recopilarán en Log Analytics con un tipo de registro de `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="78953-122">The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="78953-123">Por ejemplo, la etiqueta personalizada `tag oms.api.tomcat` en Log Analytics con un tipo de registro de `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="78953-123">For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="78953-124">Podría recuperar todos los registros de este tipo con la siguiente búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="78953-124">You could retrieve all records of this type with the following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="78953-125">Se admiten datos JSON anidados, pero se indexan en función del campo principal.</span><span class="sxs-lookup"><span data-stu-id="78953-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="78953-126">Por ejemplo, se devuelven los siguientes datos JSON desde Log Analytics como `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="78953-126">For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="78953-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78953-127">Next steps</span></span>
* <span data-ttu-id="78953-128">Obtenga información sobre las [búsquedas de registros](log-analytics-log-searches.md) para analizar los datos recopilados desde soluciones y orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="78953-128">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
 