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
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>Recopilación de datos de CollectD en agentes de Linux en Log Analytics
[CollectD](https://collectd.org/) es un demonio de Linux de código abierto que recopila periódicamente métricas de rendimiento de aplicaciones e información de nivel de sistema. Aplicaciones de ejemplo incluyen hello Máquina Virtual Java (JVM), MySQL Server y Nginx. En este artículo se proporciona información sobre la recopilación de datos de rendimiento de CollectD en Log Analytics.

Puede encontrar una lista completa de los complementos disponibles en la [tabla de complementos](https://collectd.org/wiki/index.php/Table_of_Plugins).

![Introducción a CollectD](media/log-analytics-data-sources-collectd/overview.png)

Hello configuración CollectD siguiente se incluye en hello agente de OMS para Linux tooroute CollectD datos toohello agente de OMS para Linux.

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

Además, si usa un versiones de collectD antes de 5.5 usar hello siguiente configuración en su lugar.

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

configuración de Hello CollectD usa predeterminado de hello`write_http` toosend de complemento de los datos de rendimiento métrica a través del puerto 26000 tooOMS agente para Linux. 

> [!NOTE]
> Este puerto puede ser el puerto configurado tooa personalizado si es necesario.

Hola agente de OMS para Linux también escucha en el puerto 26000 para las métricas de CollectD y, a continuación, convierte las métricas de esquema tooOMS. Hello aquí te mostramos hello agente de OMS para Linux configuración `collectd.conf`.

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>Versiones admitidas
- Log Analytics admite actualmente las versiones de CollectD 4.8 y superior.
- Para la recopilación de métricas de CollectD, se requiere el agente de OMS para Linux v1.1.0-217 o superior.


## <a name="configuration"></a>Configuración
siguiente Hola es colección de tooconfigure de pasos básicos de los datos de CollectD de análisis de registros.

1. Configurar CollectD toosend datos toohello agente de OMS para Linux mediante el complemento de write_http Hola.  
2. Configurar hello agente de OMS para Linux toolisten para hello CollectD datos en el puerto adecuado de Hola.
3. Reinicie CollectD y el agente de OMS para Linux.

### <a name="configure-collectd-tooforward-data"></a>Configurar CollectD tooforward datos 

1. tooroute CollectD datos toohello agente de OMS para Linux, `oms.conf` necesidades toobe agrega el directorio de configuración del tooCollectD. destino de Hola de este archivo depende de Hola de distribución de Linux de su equipo.

    Si su directorio de configuración de CollectD está ubicado en /etc/collectd.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    Si su directorio de configuración de CollectD está ubicado en /etc/collectd/collectd.conf.d/:

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >Para las versiones de CollectD anteriores 5.5 tendrá etiquetas de hello toomodify en `oms.conf` como se indicó anteriormente.
    >

2. Copie el directorio de configuración de omsagent collectd.conf toohello deseado del área de trabajo.

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. Reinicie CollectD y agente de OMS para Linux con hello siga los comandos.

    sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>Las métricas de CollectD tooLog conversión de esquema de análisis
toomaintain un modelo familiar entre las métricas de infraestructura que ya se han recopilado por el agente de OMS para Linux y Hola nuevas métricas recopilados por CollectD Hola después de la asignación de esquema se utiliza:

| Campo de métrica de CollectD | Campo de Log Analytics |
|:--|:--|
| host | Equipo |
| complemento | None |
| plugin_instance | Nombre de instancia<br>Si **plugin_instance** es *null*, entonces InstanceName ="*_Total*". |
| type | ObjectName |
| type_instance | CounterName<br>Si **type_instance** es *null*, entonces CounterName=**en blanco**. |
| dsnames[] | CounterName |
| dstypes | None |
| values[] | CounterValue |

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones. 
* Use [campos personalizados](log-analytics-custom-fields.md) tooparse datos de registros de syslog en campos individuales.

