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
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>Recopilación de alertas de Nagios y Zabbix en Log Analytics desde el agente de OMS para Linux 
[Nagios](https://www.nagios.org/) y [Zabbix](http://www.zabbix.com/) son herramientas de supervisión de código abierto.  Puede recopilar las alertas de estas herramientas en análisis de registros en orden tooanalyze junto con [alertas procedentes de otros orígenes](log-analytics-alerts.md).  Este artículo describe cómo tooconfigure hello agente de OMS para Linux toocollect alertas desde estos sistemas.
 
## <a name="configure-alert-collection"></a>Configuración de la recopilación de alertas

### <a name="configuring-nagios-alert-collection"></a>Configuración de la recopilación de alertas de Nagios
Realizar Hola seguir pasos de alertas de hello Nagios server toocollect.

1. Usuario de hello GRANT **omsagent** archivo de registro de acceso de lectura toohello Nagios (es decir, `/var/log/nagios/nagios.log`). Suponiendo que el archivo de hello nagios.log es propiedad de grupo hello `nagios`, puede agregar el usuario hello **omsagent** toohello **nagios** grupo. 

    sudo usermod -a -G nagios omsagent

2.  Modificar el archivo de configuración de hello en (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Asegúrese de hello siguiendo las entradas está presentes y no comentadas:  

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

3. Reiniciar el demonio omsagent Hola

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>Configuración de la recopilación de alertas de Zabbix
toocollect las alertas de un servidor Zabbix, deberá toospecify un usuario y una contraseña en *borre el texto*. Esto no es lo ideal, pero se recomienda que cree el usuario de Hola y conceder permisos toomonitor onlu.

Realizar Hola seguir pasos de alertas de hello Nagios server toocollect.

1. Modificar el archivo de configuración de hello en (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Asegúrese de hello siguiendo las entradas está presentes y no comentado.  Cambiar toovalues de nombre y la contraseña del usuario de hello para el entorno de Zabbix.

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. Reiniciar el demonio omsagent Hola

    sudo sh /opt/microsoft/omsagent/bin/service_control restart


## <a name="alert-records"></a>Registros de alerta
Puede recuperar registros de alertas de Nagios y Zabbix con [búsquedas de registros](log-analytics-log-searches.md) en Log Analytics.

### <a name="nagios-alert-records"></a>Registros de alertas de Nagios

Los registros de alertas recopilados por Nagios tienen como **tipo** una **alerta** y como **SourceSystem****Nagios**.  Tienen propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| Tipo |*Alerta* |
| SourceSystem |*Nagios* |
| AlertName |Nombre de alerta de Hola. |
| AlertDescription | Descripción de la alerta de Hola. |
| AlertState | Estado del servicio de Hola o host.<br><br>OK<br>ADVERTENCIA<br>ARRIBA<br>ABAJO |
| HostName | Nombre del host de Hola que creó Hola alerta. |
| PriorityNumber | Nivel de prioridad de alerta de Hola. |
| StateType | tipo de Hola de estado de alerta de Hola.<br><br>SOFT: problema que no se ha vuelto a comprobar.<br>HARD: problema que se ha vuelto a comprobar un número de veces especificado.  |
| TimeGenerated |Se creó la alerta de Hola de fecha y hora. |


### <a name="zabbix-alert-records"></a>Registros de alertas de Zabbix
Los registros de alertas recopilados por Zabbix tienen como **tipo** una **alerta** y como **SourceSystem****Zabbix**.  Tienen propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| Tipo |*Alerta* |
| SourceSystem |*Zabbix* |
| AlertName | Nombre de alerta de Hola. |
| AlertPriority | Gravedad de alerta de Hola.<br><br>no clasificada<br>informativo<br>Warning (Advertencia)<br>average<br>alta<br>desastre  |
| AlertState | Estado de alerta de Hola.<br><br>0 - estado está activo toodate.<br>1: el estado es desconocido.  |
| AlertTypeNumber | Especifica si la alerta puede generar varios eventos de problema.<br><br>0 - estado está activo toodate.<br>1: el estado es desconocido.    |
| Comentarios | Comentarios adicionales de la alerta. |
| HostName | Nombre del host de Hola que creó Hola alerta. |
| PriorityNumber | Valor que indica la gravedad de alerta de Hola.<br><br>0: no clasificada<br>1: información<br>2: advertencia<br>3: promedio<br>4: alta<br>5: desastre |
| TimeGenerated |Se creó la alerta de Hola de fecha y hora. |
| TimeLastModified |Estado de Hola de fecha y hora de alerta de Hola se cambió por última vez. |


## <a name="next-steps"></a>Pasos siguientes
* Más información sobre las [alertas](log-analytics-alerts.md) en Log Analytics.
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones. 
