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
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>Recopilar orígenes de datos JSON con hello agente de OMS para Linux en análisis de registros
Orígenes de datos JSON se pueden recopilar en análisis de registros mediante Hola agente de OMS para Linux.  Estos orígenes de datos personalizados pueden ser scripts simples que devuelven JSON, como [curl](https://curl.haxx.se/) o uno de los más de [300 complementos de FluentD](http://www.fluentd.org/plugins/all). Este artículo describe configuración de hello necesaria para esta recopilación de datos.

> [!NOTE]
> El agente de OMS para Linux v1.1.0-217+ es necesario para los datos JSON personalizados.

## <a name="configuration"></a>Configuración

### <a name="configure-input-plugin"></a>Configuración del complemento de entrada

agregar datos JSON de toocollect en análisis de registros, `oms.api.` toohello inicio de una etiqueta de FluentD en un complemento de entrada.

Por ejemplo, el siguiente es un archivo de configuración independiente `exec-json.conf` en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.  Esto utiliza hello FluentD complemento `exec` toorun un comando curl cada 30 segundos.  complemento de salida JSON de hello recopila la salida de Hello de este comando.

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
agregado en el archivo de configuración de Hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` requerirá toohave cambiar su propiedad con el siguiente comando de Hola.

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>Configuración del complemento de salida 
Agregar Hola siguiente salida complemento Configuración toohello principal configuración en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` o según lo coloca en un archivo de configuración independiente`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

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

### <a name="restart-oms-agent-for-linux"></a>Reinicio del agente de OMS para Linux
Reinicie Hola agente de OMS para Linux servicio con el siguiente comando de Hola.

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>Salida
se recopilarán datos de Hello en análisis de registros con un tipo de registro de `<FLUENTD_TAG>_CL`.

Por ejemplo, Hola etiqueta personalizada `tag oms.api.tomcat` en análisis de registros con un tipo de registro de `tomcat_CL`.  Puede recuperar todos los registros de este tipo con hello después de la búsqueda de registros.

    Type=tomcat_CL

Se admiten datos JSON anidados, pero se indexan en función del campo principal. Por ejemplo, se devuelve Hola después datos JSON en una búsqueda de análisis de registros como `tag_s : "[{ "a":"1", "b":"2" }]`.

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones. 
 