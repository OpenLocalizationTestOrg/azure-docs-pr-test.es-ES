---
title: "aaaConnecting la solución de auditoría y seguridad productos toohello seguridad Operations Management Suite (OMS) | Documentos de Microsoft"
description: "Este documento le ayuda a tooconnect su tooOperations de productos de seguridad, seguridad del conjunto de administración y solución de auditoría con formato de eventos común."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a>Conectar la solución de auditoría y seguridad productos toohello seguridad Operations Management Suite (OMS) 
Este documento le ayuda a conectar sus productos de seguridad en hello seguridad de OMS y solución de auditoría. se admite Hola siguientes orígenes:

- Eventos de formato de evento común (CEF)
- Eventos de Cisco ASA


## <a name="what-is-cef"></a>¿Qué es el formato de evento común (CEF)?
Formato de evento comunes (CEF) es un formato estándar del sector sobre mensajes de Syslog, utilizado por muchos proveedores tooallow evento interoperabilidad de la seguridad entre varias plataformas distintas. Solución de auditoría y seguridad de OMS admiten la ingesta de datos con los productos de seguridad CEF, lo que permite tooconnect con seguridad de OMS. 

Al conectar su tooOMS de origen de datos, son tootake puede aprovechar Hola siguiendo las capacidades que forman parte de esta plataforma:

- Búsqueda y correlación
- Auditoría
- Alerta
- Información sobre amenazas
- Problemas importantes

## <a name="collection-of-security-solution-logs"></a>Colección de registros de soluciones de seguridad

Seguridad de OMS admite la recopilación de registros utilizando CEF sobre Syslogs y registros [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/). En este ejemplo, el origen de hello (equipo que genera registros de hello) es un equipo de Linux que se ejecuta el demonio syslog-ng y destino de hello es seguridad de OMS. tareas de equipo Linux tooprepare Hola que necesitará hello tooperform siguientes:

- Descargar Hola agente de OMS para Linux, versión 1.2.0-25 o una versión posterior.
- Siga la sección de hello **Guía de instalación rápida** de [este artículo](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall y el área de trabajo de hello incorporar agente tooyour.

Normalmente, el agente de hello está instalado en un equipo diferente de hello uno en los registros de Hola se generan. Equipo de agente de reenvío Hola registros toohello normalmente requerirá Hola pasos:

- Configurar Hola registro producto/máquina tooforward Hola eventos necesarios toohello demonio syslog (rsyslog o syslog-ng) en el equipo del agente de Hola.
- Habilitar el demonio de syslog hello en los mensajes de Hola agente máquina tooreceive desde un sistema remoto.

En el equipo de agente de hello, eventos de hello necesitan toobe enviado desde el puerto UDP 25226 del toolocal de demonio de syslog Hola. agente de Hello está realizando escuchas para los eventos entrantes en este puerto. Hola te mostramos un ejemplo de configuración para enviar todos los eventos de hello local system toohello agent (puede modificar Hola configuración toofit la configuración regional):

1. Ventana de terminal de hello abierta y vaya toohello directorio */etc/syslog-ng /* 
2. Crear un nuevo archivo *omsagent.conf de configuración de seguridad* y agregue Hola siguen contenido: OMS_facility = local4
    
    filter f_local4_oms { facility(local4); };

    destination security_oms { tcp("127.0.0.1" port(25226)); };

    log { source(src); filter(f_local4_oms); destination(security_oms); };
    
3. Descargar archivo hello *security_events.conf* y colóquelo en */etc/opt/microsoft/omsagent/conf/omsagent.d/* en el equipo del agente de OMS de Hola.
4. Escriba comando hello debajo de demonio de syslog de Hola toorestart: *para syslog-ng ejecutar:*
    
    ```
    sudo service rsyslog restart
    ```

    *Para la ejecución de rsyslog:*
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. Escriba el comando de hello debajo de hello toorestart agente de OMS:

    *Para la ejecución de syslog-ng:*
    
    ```
    sudo service omsagent restart
    ```

    *Para la ejecución de rsyslog:*
    
    ```
    systemctl restart omsagent
    ```
6. Escriba el siguiente comando de Hola y revise hello tooconfirm de resultado que no hay ningún error en el registro del agente de OMS de hello:

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a>Revisión de eventos de seguridad recopilados

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

Una vez hello configuración finalizado, eventos de seguridad de hello iniciará toobe ingerida por la seguridad de OMS. toovisualize esos eventos, abra Hola búsqueda de registros, escriba el comando de hello *tipo = CommonSecurityLog* en Hola campo de búsqueda y presione ENTRAR. Hello en el ejemplo siguiente se muestra resultado de hello de este comando, tenga en cuenta que en este caso seguridad OMS ya ingestión registros de seguridad en varios proveedores:
   
![Evaluación de línea base de Seguridad y auditoría de OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

Puede refinar la búsqueda de un proveedor único, por ejemplo, toovisualize registra Cisco en línea, escriba: *tipo = CommonSecurityLog DeviceVendor = Cisco*. Hola "CommonSecurityLog" tiene predefinidos los campos para cualquier encabezado CEF incluidos extensios básica de hello, mientras otra extensión, ya sea "Custom Extension" o no es así, se insertará en el campo "AdditionalExtensions". Puede usar campos de tooget dedicado de característica de campos personalizados de Hola de él. 

### <a name="accessing-computers-missing-baseline-assessment"></a>Acceso a equipos sin evaluación de línea base
OMS admite el perfil de línea de base de miembro de dominio de hello en Windows Server 2008 R2 hasta tooWindows Server 2012 R2. La línea base de Windows Server 2016 todavía no está finalizada y se agregará en cuanto se publique. Todos los demás sistemas operativos analizados a través de evaluación de línea de base de seguridad de OMS y auditoría aparecen bajo hello **equipos falta la evaluación de la línea de base** sección.

## <a name="see-also"></a>Otras referencias
En este documento, se habrá aprendido cómo tooconnect su tooOMS de solución CEF. toolearn más información acerca de la seguridad de OMS, consulte Hola siguientes artículos:

* [Información general de Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Supervisión y responde tooSecurity alertas en Operations Management Suite solución de seguridad y auditoría](oms-security-responding-alerts.md)
* [Supervisión de los recursos en la solución Seguridad y auditoría de Operations Management Suite](oms-security-monitoring-resources.md)

