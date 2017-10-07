---
title: "solución de supervisión en el análisis de registros aaaVMware | Documentos de Microsoft"
description: "Obtenga información sobre cómo Hola solución de supervisión de VMware puede ayudar a administrar registros y supervisar los hosts de ESXi."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a>Solución de supervisión de VMware (versión preliminar)de Log Analytics

![Símbolo de VMware](./media/log-analytics-vmware/vmware-symbol.png)

Hola solución de supervisión de VMware en el análisis de registros es una solución que le ayudará a crear un registro centralizado y un nuevo enfoque de supervisión para los registros de VMware de gran tamaño. Este artículo describe cómo solucionar problemas, capturar y administrar hosts de ESXi hello en una sola ubicación con soluciones de Hola. Con la solución de hello, puede ver datos detallados para todos los hosts de ESXi en una sola ubicación. Puede ver los recuentos de eventos superior, el estado y las tendencias de los hosts de máquina virtual y ESXi proporcionados a través de los registros de host ESXi Hola. Puede solucionar errores viendo y buscando registros de host ESXi centralizados, además de crear alertas basadas en consultas de búsqueda de registros.

solución de Hello utiliza funcionalidad de syslog nativo de hello ESXi toopush datos tooa objetivo de host de máquina virtual, que tiene el agente de OMS. Sin embargo, solución de hello no escribe archivos en syslog en destino Hola máquina virtual. agente de OMS Hola abre el puerto 1514 y escucha toothis. Después de recibir datos de hello, agente de OMS Hola traslada los datos de hello en OMS.

## <a name="installing-and-configuring-hello-solution"></a>Instalar y configurar soluciones de Hola
Usar hello después tooinstall de información y configurar soluciones de Hola.

* Agregar Hola VMware supervisión solución tooyour se describe el área de trabajo OMS mediante el proceso de hello en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).

#### <a name="supported-vmware-esxi-hosts"></a>Hosts ESXi de VMware compatibles
Hosts ESXi de vSphere 5.5 y 6.0

#### <a name="prepare-a-linux-server"></a>Preparación de servidores Linux
Crear un tooreceive VM del sistema operativo Linux todos los datos de syslog desde hosts de ESXi Hola. Hola [agente Linux de OMS](log-analytics-linux-agents.md) es el punto de recopilación de Hola para todos los datos de syslog de host ESXi. Puede usar varios ESXi hosts tooforward registros tooa único servidor Linux, como en el siguiente ejemplo de Hola.  

   ![Flujo de Syslog](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a>Configuración de recopilaciones de Syslog
1. Configure el reenvío de Syslog en vSphere. Para obtener información detallada toohelp configurar el reenvío de syslog, consulte [configuración de syslog en ESXi 5.x y 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322). Vaya demasiado**configuración del Host ESXi** > **Software** > **configuración avanzada** > **Syslog**.
   ![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)  
2. Hola *Syslog.global.logHost* , a continuación, agregue el número de puerto de hello y servidor Linux *1514*. Por ejemplo, `tcp://hostname:1514` o `tcp://123.456.789.101:1514`.
3. Abra firewall de host ESXi Hola de syslog. **ESXi Host Configuration (Configuración de hosts ESXi)** > **Software** > **Security Profile (Perfil de seguridad)** > **Firewall** y abra **Properties (Propiedades)**.  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. Compruebe Hola vSphere consola tooverify que ese syslog está configurado correctamente. Confirmar en hello ESXI hospedar ese puerto **1514** está configurado.
5. Descargue e instale Hola agente de OMS para Linux en el servidor Linux de Hola. Para obtener más información, vea hello [documentación para agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux).
6. Después de instala el agente de OMS para Linux de Hola, vaya toohello /etc/opt/microsoft/omsagent/sysconf/omsagent.d directorio y copia hello vmware_esxi.conf archivo toohello /etc/opt/microsoft/omsagent/conf/omsagent.d y Hola Hola propietario/grupo de cambios permisos de archivo hello y. Por ejemplo:

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. Reinicie Hola agente de OMS para Linux mediante la ejecución de `sudo /opt/microsoft/omsagent/bin/service_control restart`.
8. Probar la conectividad de hello entre servidor Linux de Hola y host ESXi de hello mediante el uso de hello `nc` comando hello ESXi Host. Por ejemplo:

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. Hola Portal de OMS, realizar una búsqueda de registros para `Type=VMware_CL`. Cuando OMS recopila los datos de syslog de hello, conserva el formato de syslog Hola. En el portal de hello, se capturan algunos campos específicos, como *Hostname* y *ProcessName*.  

    ![type](./media/log-analytics-vmware/type.png)  

    Si los resultados de búsqueda de registros de vista son similares imagen toohello anterior, está configurado el panel de solución de supervisión de VMware de OMS de Hola de toouse.  

## <a name="vmware-data-collection-details"></a>Detalles de la colección de datos de VMware
Hola solución de supervisión de VMware recopila diversos datos de registro y métricas de rendimiento de los hosts de ESXi mediante Hola agentes de OMS para Linux que se ha habilitado.

Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos.

| plataforma | Agente de OMS para Linux | Agente de SCOM | Azure Storage | ¿Se necesita SCOM? | Datos del agente de SCOM enviados a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- |
| Linux |&#8226; |  |  |  |  |Cada 3 minutos |

Hello en la tabla siguiente muestra ejemplos de campos de datos recopilados por hello solución de supervisión de VMware:

| Nombre del campo | Descripción |
| --- | --- |
| Device_s |Dispositivos de almacenamiento de VMware |
| ESXIFailure_s |Tipos de error |
| EventTime_t |Hora en la que se produjo el evento |
| HostName_s |Nombre de host ESXi |
| Operation_s |Creación o eliminación de máquinas virtuales |
| ProcessName_s |Nombre del evento |
| ResourceId_s |nombre de host de VMware Hola |
| ResourceLocation_s |VMware |
| ResourceName_s |VMware |
| ResourceType_s |Hyper-V |
| SCSIStatus_s |Estado de SCSI de VMware |
| SyslogMessage_s |Datos de syslog |
| UserName_s |Usuario que creó o eliminó la máquina virtual |
| VMName_s |Nombre de la máquina virtual |
| Equipo |Equipo host |
| TimeGenerated |se generan datos en tiempo de Hola |
| DataCenter_s |Centro de datos de VMware |
| StorageLatency_s |Latencia de almacenamiento (ms) |

## <a name="vmware-monitoring-solution-overview"></a>Información general de la solución de supervisión de VMware
aparece el icono de VMware de Hola Hola portal de OMS. Proporciona una visión general de los errores. Al hacer clic en el icono de hello, vaya a una vista de panel.

![Icono](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a>Navegue a vista de panel de Hola
Hola **VMware** vista de panel, los módulos están organizados por:

* Número de estados de error
* Hosts principales por números de eventos
* Números de eventos principales
* Actividades de máquina virtual
* Eventos de disco de host ESXi

![solution1](./media/log-analytics-vmware/solutionview1-1.png)

![solution2](./media/log-analytics-vmware/solutionview1-2.png)

Haga clic en cualquier panel de búsqueda de análisis de registros que muestra información detallada específica de la hoja de hello tooopen de hoja.

Desde aquí, puede editar toomodify de consulta de búsqueda de Hola para un elemento específico. Para obtener un tutorial sobre aspectos básicos de hello de la búsqueda de OMS, visite hello [tutorial de búsqueda de registros OMS.](log-analytics-log-searches.md)

#### <a name="find-esxi-host-events"></a>Búsqueda de eventos de hosts ESXi
Un único host ESXi genera varios registros en función de sus procesos. Hola solución de supervisión de VMware centraliza ellos y resume los recuentos de eventos de Hola. Esta vista centralizada ayudar a comprender qué host ESXi tiene un gran volumen de eventos y qué eventos ocurren con más frecuencia en su entorno.

![event](./media/log-analytics-vmware/events.png)

Puede obtener más detalles haciendo clic en un host ESXi o un tipo de evento.

Al hacer clic en un nombre de host ESXi, verá la información de ese host ESXi. Si desea toonarrow resultados con el tipo de evento de hello, agregue `“ProcessName_s=EVENT TYPE”` en la consulta de búsqueda. Puede seleccionar **ProcessName** en filtro de búsqueda de Hola. Limita información Hola.

![Detalles](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a>Búsqueda de actividades de máquina virtual que usan numerosos recursos
Una máquina virtual se puede crear y eliminar en cualquier host ESXi. Es útil para un administrador tooidentify cuántas máquinas virtuales que crea un host ESXi. Que a su vez, ayuda a planear la capacidad y rendimiento de toounderstand. Es fundamental realizar un seguimiento de los eventos de actividad de máquina virtual al administrar el entorno.

![Detalles](./media/log-analytics-vmware/vmactivities1.png)

Si desea que el host ESXi adicional de toosee datos de creación de la máquina virtual, haga clic en un nombre de host ESXi.

![Detalles](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a>Consultas de búsqueda comunes
solución de Hello incluye otras consultas útiles que pueden ayudarle a administrar los hosts de ESXi, por ejemplo, el espacio de almacenamiento alta, latencia de almacenamiento y de errores de ruta de acceso.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Consultas](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a>Guardado de consultas
Guardar consultas de búsqueda es una característica estándar de OMS que puede ayudarlo a sacar utilidad de las consultas encontradas. Después de crear una consulta que encuentre útil, puede guardarlo si hace clic hello **favoritos**. Una consulta guardada permite fácilmente reutilizarla más adelante desde hello [Mi panel](log-analytics-dashboards.md) página donde puede crear sus propios paneles personalizados.

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a>Creación de alertas a partir de las consultas
Después de crear las consultas, es recomendable toouse Hola consultas tooalert cuando se producen eventos específicos. Vea [alertas en los análisis de registros](log-analytics-alerts.md) para obtener información acerca de cómo toocreate alertas. Para obtener ejemplos de consultas y otros ejemplos de consulta de las alertas, vea hello [VMware Monitor mediante el análisis de registros de OMS](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) entrada de blog.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a>¿Qué necesito toodo en configuración del host ESXi Hola? ¿Qué impacto tendrá en mi entorno actual?
solución de Hello utiliza mecanismo de reenvío de Syslog de Host ESXi nativo Hola. No es necesario ningún software adicional de Microsoft en hello Host ESXi toocapture Hola registros. Debe tener un entorno existente de tooyour de bajo impacto. Sin embargo, deberá tooset syslog reenvío, que es la funcionalidad ESXI.

### <a name="do-i-need-toorestart-my-esxi-host"></a>¿Es necesario toorestart mi host ESXi?
No. Este proceso no requiere reiniciar. A veces, vSphere no actualiza correctamente Hola syslog. En tal caso, inicie sesión en el host de ESXi toohello y volver a cargar Hola syslog. De nuevo, no es necesario toorestart host de hello, por lo que este proceso no interrumpen el funcionamiento tooyour entorno.

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a>¿Puedo aumentar o disminuir el volumen de Hola de los datos de registro enviados tooOMS?
Sí, puede. Puede usar la configuración del nivel de registro de Host ESXi hello en vSphere. Recopilación de registros se basa en hello *información* nivel. Por lo tanto, si desea tooaudit VM creación o eliminación, necesita hello tookeep *información* nivel hostd. Para obtener más información, vea hello [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a>¿Por qué no proporciona Hostd tooOMS de datos? El registro se debe establecer tooinfo.
Se produjo un error de host ESXi de marca de tiempo de hello syslog. Para obtener más información, vea hello [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202). Después de aplicar la solución de hello, Hostd debe funcionando con normalidad.

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a>¿Puedo tener ESXi varios hosts tooa de datos de syslog de reenvío único VM con omsagent?
Sí. Puede tener varios ESXi hosts reenvío tooa único VM con omsagent.

### <a name="why-dont-i-see-data-flowing-into-oms"></a>¿Por qué no veo los datos que se transmiten a OMS?
Puede haber varios motivos:

* host de ESXi Hola correctamente no inserta datos toohello VM ejecución omsagent. tootest, realizar Hola pasos:

  1. tooconfirm, inicie sesión en toohello ESXi host utilizando ssh y ejecute el siguiente comando de hello:`nc -z ipaddressofVM 1514`

      Si esto no es correcta, configuración de vSphere Hola configuración avanzada son probablemente no se corregirá. Vea [configurar la recopilación de syslog](#configure-syslog-collection) para obtener información sobre cómo hospedar tooset seguridad Hola ESXi para el reenvío de syslog.
  2. Si la conectividad de puerto syslog es correcta, pero aún no verá ningún dato, a continuación, volver a cargar syslog hello en el host ESXi de hello mediante ssh hello toorun siguiente comando:` esxcli system syslog reload`
* Hola VM con el agente de OMS no está configurado correctamente. tootest, realizar Hola pasos:

  1. OMS escucha toohello puerto 1514 e inserta datos en OMS. tooverify que esté abierto, ejecute el siguiente comando de hello:`netstat -a | grep 1514`
  2. Debería ver el puerto `1514/tcp` abierto. Si no lo hace, compruebe que omsagent Hola está instalado correctamente. Si no ve la información del puerto hello, puerto de syslog de hello no está abierto en hello máquina virtual.

     1. Compruebe que Hola se ejecuta el agente de OMS mediante `ps -ef | grep oms`. Si no se está ejecutando, iniciar el proceso de hello, ejecute el comando de Hola` sudo /opt/microsoft/omsagent/bin/service_control start`
     2. Abra hello `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` archivo.

         Compruebe que usuario adecuada de Hola y configuración de grupo es válido, al igual que:`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`

         Si el archivo hello no existe u Hola de usuario y configuración de grupo es incorrecto, tomar medidas correctivas por [preparar un servidor Linux](#prepare-a-linux-server).

## <a name="next-steps"></a>Pasos siguientes
* Use [búsquedas de registros](log-analytics-log-searches.md) en análisis de registros tooview obtener datos de host de VMware.
* [Cree sus propios paneles](log-analytics-dashboards.md) que muestren datos de hosts de VMware.
* [Cree alertas](log-analytics-alerts.md) cuando se produzcan eventos específicos de hosts de VMware.
