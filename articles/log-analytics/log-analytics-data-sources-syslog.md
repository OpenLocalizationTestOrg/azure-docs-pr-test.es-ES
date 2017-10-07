---
title: aaaCollect y analizar los mensajes de Syslog en OMS Log Analytics | Documentos de Microsoft
description: "Syslog es un protocolo de registro de eventos que es común tooLinux. Este artículo describe cómo tooconfigure colección de mensajes de Syslog en análisis de registros y detalles de los registros de hello crean en el repositorio de OMS Hola."
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
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a>Orígenes de datos de Syslog en Log Analytics
Syslog es un protocolo de registro de eventos que es común tooLinux.  Las aplicaciones enviará los mensajes que pueden almacenados en el equipo local de Hola o entregar a tooa Syslog recopilador.  Cuando se instala el agente de OMS para Linux hello, configura el agente de toohello de hello local Syslog daemon tooforward mensajes.  agente de Hello, a continuación, envía tooLog de mensaje de Hola análisis donde se crea un registro correspondiente en el repositorio OMS Hola.  

> [!NOTE]
> Análisis de registros es compatible con la colección de mensajes enviados por rsyslog o syslog-ng, donde rsyslog es el demonio de hello predeterminado. demonio de syslog de Hello predeterminado en la versión 5 de Red Hat Enterprise Linux, CentOS y Oracle Linux (sysklog) no se admite para la recopilación de eventos de syslog. Hola toocollect datos de syslog de esta versión de las distribuciones, [demonio rsyslog](http://rsyslog.com) debe estar instalado y configurado tooreplace sysklog.
>
>

![Recopilación de Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a>Configuración de Syslog
Hola agente de OMS para Linux solo recopilará eventos con instalaciones de Hola y niveles de gravedad que se especifican en su configuración.  Puede configurar Syslog a través del portal de OMS de Hola o mediante la administración de archivos de configuración en los agentes de Linux.

### <a name="configure-syslog-in-hello-oms-portal"></a>Configurar Syslog en portal de OMS Hola
Configurar Syslog desde hello [menú datos de configuración de análisis de registro](log-analytics-data-sources.md#configuring-data-sources).  Esta configuración se entrega el archivo de configuración de toohello en cada agente de Linux.

Para agregar un nuevo recurso, escriba su nombre y haga clic en **+**.  Para cada instalación, se recopilarán sólo los mensajes con una gravedad de hello seleccionado.  Comprobar los niveles de gravedad de Hola para hello equipamiento que desea toocollect.  No puede proporcionar los criterios adicionales toofilter mensajes.

![Configuración de Syslog](media/log-analytics-data-sources-syslog/configure.png)

De forma predeterminada, todos los cambios de configuración se insertan automáticamente agentes tooall.  Si desea tooconfigure Syslog manualmente en cada agente de Linux, a continuación, desactive la casilla de hello *aplicar la siguiente máquinas de Linux de configuración toomy*.

### <a name="configure-syslog-on-linux-agent"></a>Configuración de Syslog en agente de Linux
Cuando Hola [agente de OMS se instala en un cliente Linux](log-analytics-linux-agents.md), instala un archivo de configuración de syslog predeterminada que define la función hello y gravedad de hello los mensajes que se recopilan.  Puede modificar este archivo de configuración de hello toochange.  archivo de configuración de Hello es diferente según Hola Syslog demonio que Hola cliente se ha instalado.

> [!NOTE]
> Si modifica la configuración de syslog hello, debe reiniciar el demonio de syslog Hola Hola cambios tootake efecto.
>
>

#### <a name="rsyslog"></a>rsyslog
Hello archivo de configuración para rsyslog se encuentra en **/etc/rsyslog.d/95-omsagent.conf**.  A continuación se muestra su contenido predeterminado.  Aquí reúnen los mensajes de syslog enviados del agente local Hola para todas las instalaciones con un nivel de advertencia o superior.

    kern.warning       @127.0.0.1:25224
    user.warning       @127.0.0.1:25224
    daemon.warning     @127.0.0.1:25224
    auth.warning       @127.0.0.1:25224
    syslog.warning     @127.0.0.1:25224
    uucp.warning       @127.0.0.1:25224
    authpriv.warning   @127.0.0.1:25224
    ftp.warning        @127.0.0.1:25224
    cron.warning       @127.0.0.1:25224
    local0.warning     @127.0.0.1:25224
    local1.warning     @127.0.0.1:25224
    local2.warning     @127.0.0.1:25224
    local3.warning     @127.0.0.1:25224
    local4.warning     @127.0.0.1:25224
    local5.warning     @127.0.0.1:25224
    local6.warning     @127.0.0.1:25224
    local7.warning     @127.0.0.1:25224

Puede quitar una instalación mediante la eliminación de su sección del archivo de configuración de Hola.  Puede limitar los niveles de gravedad de Hola que se recopilan para una instalación determinada mediante la modificación de la entrada de dicha instalación.  Por ejemplo, instalaciones de usuario de toolimit hello toomessages con una gravedad de error o superior modificaría esa línea de toohello de archivo de configuración de hello siguientes:

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a>syslog-ng
archivo de configuración de Hola de syslog-ng es la ubicación en **/etc/syslog-ng/syslog-ng.conf**.  A continuación se muestra su contenido predeterminado.  Aquí reúnen enviados desde el agente local Hola para todas las utilidades y todos los niveles de gravedad de mensajes de syslog.   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

Puede quitar una instalación mediante la eliminación de su sección del archivo de configuración de Hola.  Puede limitar los niveles de gravedad de Hola que se recopilan para una instalación determinada quitándolos de la lista.  Por ejemplo, toolimit Hola usuario facility toojust mensajes de alerta y críticos, lo haría para modificar esa sección de toohello de archivo de configuración de hello siguientes:

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a>Recopilación de datos de puertos de Syslog adicionales
agente de OMS Hola escucha los mensajes de Syslog en cliente local de hello en el puerto 25224.  Cuando se instala el agente de hello, se aplica una configuración de syslog predeterminada y se encuentra en hello ubicación siguiente:

* Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`
* Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`

Puede cambiar el número de puerto de hello mediante la creación de dos archivos de configuración: un archivo de configuración de FluentD y un archivo ng de rsyslog o syslog según ha instalado el demonio de Syslog de Hola.  

* el archivo de configuración de Hello FluentD debe ser un nuevo archivo que se encuentra en: `/etc/opt/microsoft/omsagent/conf/omsagent.d` y reemplace el valor de Hola Hola **puerto** entrada con el número de puerto personalizado.

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* Para rsyslog, debe crear un nuevo archivo de configuración que se encuentra en: `/etc/rsyslog.d/` y reemplace Hola valor % SYSLOG_PORT % con el número de puerto personalizado.  

    > [!NOTE]
    > Si modifica este valor en el archivo de configuración de hello `95-omsagent.conf`, se sobrescribirá al agente de Hola aplica una configuración predeterminada.
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* Hello syslog-ng config debe modificarse mediante la copia de configuración de ejemplo de Hola se muestra a continuación y agregar Hola configuración modificada personalizada toohello final del archivo de configuración de syslog ng.conf Hola ubicado en `/etc/syslog-ng/`.  Hacer **no** utilizar la etiqueta predeterminada de hello **% WORKSPACE_ID % _oms** o **% WORKSPACE_ID_OMS**, definir un personalizado etiqueta toohelp distinguir los cambios.  

    > [!NOTE]
    > Si modifica los valores predeterminados de hello en el archivo de configuración de hello, se sobrescribirán cuando el agente de hello aplica una configuración predeterminada.
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

Después de completar los cambios de hello, Hola Syslog y Hola debe toobe reiniciar tooensure Hola configuración cambios surten efecto el servicio de agente OMS.   

## <a name="syslog-record-properties"></a>Propiedades de registros de Syslog
Registros de syslog tienen un tipo de **Syslog** y que tienen propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| Equipo |Equipo que Hola eventos se recopilaron de. |
| Facility |Define la parte de hello del sistema de Hola que generó el mensaje de bienvenida. |
| HostIP |Dirección IP del sistema Hola enviando mensaje de saludo. |
| HostName |Nombre del sistema de hello enviando mensaje de saludo. |
| SeverityLevel |Nivel de gravedad del evento de Hola. |
| SyslogMessage |Texto del mensaje de bienvenida. |
| ProcessID |Identificador del proceso de Hola que generó el mensaje de bienvenida. |
| EventTime |Fecha y hora en que Hola eventos generó un error. |

## <a name="log-queries-with-syslog-records"></a>Consultas de registro con registros de Syslog
Hello tabla siguiente proporciona diferentes ejemplos de consultas de registro que recuperar registros de Syslog.

| Consultar | Descripción |
|:--- |:--- |
| Type=Syslog |Todos los registros de Syslog. |
| Type=Syslog SeverityLevel=error |Todos los registros de Syslog con gravedad de error. |
| Type=Syslog &#124; measure count() by Computer |Número de registros de Syslog por equipo. |
| Type=Syslog &#124; measure count() by Facility |Número de registros de Syslog por recurso. |

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de las consultas cambiaría toohello siguiente.

> | Consultar | Descripción |
|:--- |:--- |
| syslog |Todos los registros de Syslog. |
| Syslog &#124; where SeverityLevel == "error" |Todos los registros de Syslog con gravedad de error. |
| Syslog &#124; summarize AggregatedValue = count() by Computer |Número de registros de Syslog por equipo. |
| Syslog &#124; summarize AggregatedValue = count() by Facility |Número de registros de Syslog por recurso. |

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.
* Use [campos personalizados](log-analytics-custom-fields.md) tooparse datos de registros de syslog en campos individuales.
* [Configurar los agentes de Linux](log-analytics-linux-agents.md) toocollect otros tipos de datos.
