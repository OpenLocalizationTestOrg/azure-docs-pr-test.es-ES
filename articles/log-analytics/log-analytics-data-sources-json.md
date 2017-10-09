---
title: "aaaCollecting datos personalizados de JSON en análisis de registros de OMS | Documentos de Microsoft"
description: "Orígenes de datos JSON se pueden recopilar en análisis de registros mediante Hola agente de OMS para Linux.  Estos orígenes de datos personalizados pueden ser scripts simples que devuelven JSON, como curl o uno de los más de 300 complementos de FluentD. Este artículo describe configuración de hello necesaria para esta recopilación de datos."
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
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="88f22-105">Recopilar orígenes de datos JSON con hello agente de OMS para Linux en análisis de registros</span><span class="sxs-lookup"><span data-stu-id="88f22-105">Collecting custom JSON data sources with hello OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="88f22-106">Orígenes de datos JSON se pueden recopilar en análisis de registros mediante Hola agente de OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="88f22-106">Custom JSON data sources can be collected into Log Analytics using hello OMS Agent for Linux.</span></span>  <span data-ttu-id="88f22-107">Estos orígenes de datos personalizados pueden ser scripts simples que devuelven JSON, como [curl](https://curl.haxx.se/) o uno de los más de [300 complementos de FluentD](http://www.fluentd.org/plugins/all).</span><span class="sxs-lookup"><span data-stu-id="88f22-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="88f22-108">Este artículo describe configuración de hello necesaria para esta recopilación de datos.</span><span class="sxs-lookup"><span data-stu-id="88f22-108">This article describes hello configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="88f22-109">El agente de OMS para Linux v1.1.0-217+ es necesario para los datos JSON personalizados.</span><span class="sxs-lookup"><span data-stu-id="88f22-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="88f22-110">Configuración</span><span class="sxs-lookup"><span data-stu-id="88f22-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="88f22-111">Configuración del complemento de entrada</span><span class="sxs-lookup"><span data-stu-id="88f22-111">Configure input plugin</span></span>

<span data-ttu-id="88f22-112">agregar datos JSON de toocollect en análisis de registros, `oms.api.` toohello inicio de una etiqueta de FluentD en un complemento de entrada.</span><span class="sxs-lookup"><span data-stu-id="88f22-112">toocollect JSON data in Log Analytics, add `oms.api.` toohello start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="88f22-113">Por ejemplo, el siguiente es un archivo de configuración independiente `exec-json.conf` en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span><span class="sxs-lookup"><span data-stu-id="88f22-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="88f22-114">Esto utiliza hello FluentD complemento `exec` toorun un comando curl cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="88f22-114">This uses hello FluentD plugin `exec` toorun a curl command every 30 seconds.</span></span>  <span data-ttu-id="88f22-115">complemento de salida JSON de hello recopila la salida de Hello de este comando.</span><span class="sxs-lookup"><span data-stu-id="88f22-115">hello output from this command is collected by hello JSON output plugin.</span></span>

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
<span data-ttu-id="88f22-116">agregado en el archivo de configuración de Hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` requerirá toohave cambiar su propiedad con el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="88f22-116">hello configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require toohave its ownership changed with hello following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="88f22-117">Configuración del complemento de salida</span><span class="sxs-lookup"><span data-stu-id="88f22-117">Configure output plugin</span></span> 
<span data-ttu-id="88f22-118">Agregar Hola siguiente salida complemento Configuración toohello principal configuración en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` o según lo coloca en un archivo de configuración independiente`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span><span class="sxs-lookup"><span data-stu-id="88f22-118">Add hello following output plugin configuration toohello main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

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

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="88f22-119">Reinicio del agente de OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="88f22-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="88f22-120">Reinicie Hola agente de OMS para Linux servicio con el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="88f22-120">Restart hello OMS Agent for Linux service with hello following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="88f22-121">Salida</span><span class="sxs-lookup"><span data-stu-id="88f22-121">Output</span></span>
<span data-ttu-id="88f22-122">se recopilarán datos de Hello en análisis de registros con un tipo de registro de `<FLUENTD_TAG>_CL`.</span><span class="sxs-lookup"><span data-stu-id="88f22-122">hello data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="88f22-123">Por ejemplo, Hola etiqueta personalizada `tag oms.api.tomcat` en análisis de registros con un tipo de registro de `tomcat_CL`.</span><span class="sxs-lookup"><span data-stu-id="88f22-123">For example, hello custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="88f22-124">Puede recuperar todos los registros de este tipo con hello después de la búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="88f22-124">You could retrieve all records of this type with hello following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="88f22-125">Se admiten datos JSON anidados, pero se indexan en función del campo principal.</span><span class="sxs-lookup"><span data-stu-id="88f22-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="88f22-126">Por ejemplo, se devuelve Hola después datos JSON en una búsqueda de análisis de registros como `tag_s : "[{ "a":"1", "b":"2" }]`.</span><span class="sxs-lookup"><span data-stu-id="88f22-126">For example, hello following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="88f22-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="88f22-127">Next steps</span></span>
* <span data-ttu-id="88f22-128">Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.</span><span class="sxs-lookup"><span data-stu-id="88f22-128">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
 