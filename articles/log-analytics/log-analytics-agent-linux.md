---
title: aaaConnect su tooOperations de equipos Linux Management Suite (OMS) | Documentos de Microsoft
description: "Este artículo describe cómo tooconnect los equipos Linux se hospedan en Azure, otros en la nube o tooOMS local mediante Hola agente de OMS para Linux."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>Conectar su tooOperations de equipos Linux Management Suite (OMS) 

Con Microsoft Operations Management Suite (OMS), puede recopilar y actuar en los datos generados desde equipos Linux y soluciones de contenedor como Docker, que residen en el centro de datos local como servidores físicos o máquinas virtuales, máquinas virtuales en un servicio hospedado en la nube como Amazon Web Services (AWS) o Microsoft Azure. También puede usar soluciones de administración disponibles en OMS como seguimiento de cambios, los cambios de configuración tooidentify, y tooproactively de las actualizaciones de software de administración de actualizaciones toomanage administrar Hola del ciclo de vida de las máquinas virtuales de Linux. 

Hello agente de OMS para Linux se comunica saliente con el servicio OMS hello en el puerto TCP 443, y si el equipo de Hola conecta toocommunicate de servidor proxy o firewall tooa mediante Hola Internet, revise [configurar agente de Hola para su uso con un proxy HTTP servidor o puerta de enlace de OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand cambia la configuración deberá toobe aplicado.  Si se está supervisando el equipo de hello con System Center 2016 - Operations Manager u Operations Manager 2012 R2, puede ser de host múltiple con datos de toocollect del servicio OMS de Hola y el servicio de toohello hacia delante y supervisarse por Operations Manager.  Equipos de Linux supervisados por un grupo de administración de Operations Manager se integra con OMS no reciben la configuración de orígenes de datos y reenviar los datos a través del grupo de administración de Hola recopilan.  agente de OMS Hello no puede ser toomore tooreport configurado a un área de trabajo.  

Si las directivas de seguridad de TI no permitir que los equipos en su toohello de tooconnect de la red Internet, agente de hello puede ser información de configuración de tooreceive de tooconnect configurado toohello puerta de enlace de OMS y enviar los datos recopilados según solución hello que tiene habilitado. Para obtener más información y pasos acerca de cómo tooconfigure su toocommunicate agente Linux de OMS a través de un servicio de OMS toohello de puerta de enlace de OMS, consulte [conectar tooOMS de equipos con hello puerta de enlace de OMS](log-analytics-oms-gateway.md).  

Hello siguiente diagrama muestra conexión Hola entre los equipos administrados con agente de Linux de Hola y OMS, incluidos los puertos y la dirección de Hola.

![diagrama de comunicación de agente directo con OMS](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>Requisitos del sistema
Antes de comenzar, revise Hola después tooverify detalles cumplen los requisitos previos de Hola.

### <a name="supported-linux-operating-systems"></a>Sistemas operativos Linux compatibles
Hola siguiendo las distribuciones de Linux es compatibles oficialmente.  Sin embargo, también puede ejecutar Hola agente de OMS para Linux en otras distribuciones que no aparece.

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5, 6 y 7 (x86/x64)
* Oracle Linux 5, 6 y 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 y 7 (x86/x64)
* Debian GNU/Linux 6, 7 y 8 (x86/x64)
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)
* SUSE Linux Enterprise Server 11 y 12 (x86/x64)

### <a name="network"></a>Red
información de Hello debajo de proxy de Hola de lista e información de configuración de firewall necesitan para hello toocommunicate de agente de Linux con OMS. Tráfico es saliente desde el servicio OMS de toohello de red. 

|Recurso del agente| Puertos |  
|------|---------|  
|*.ods.opinsights.azure.com | Puerto 443|   
|*.oms.opinsights.azure.com | Puerto 443|   
|*.blob.core.windows.net/ | Puerto 443|   
|*.azure-automation.net | Puerto 443|  

### <a name="package-requirements"></a>Requisitos de paquete

 **Paquetes necesarios**   | **Descripción**   | **Versión mínima**
--------------------- | --------------------- | -------------------
Glibc | Biblioteca GNU C   | 2.5-12 
Openssl | Bibliotecas OpenSSL | 0.9.8E o 1.0
Curl | Cliente web de cURL | 7.15.5
Python ctypes | | 
PAM | Módulos de autenticación conectables | 

> [!NOTE]
>  Rsyslog o syslog-ng es necesario toocollect mensajes de syslog. demonio de syslog de Hello predeterminado en la versión 5 de Red Hat Enterprise Linux, CentOS y Oracle Linux (sysklog) no se admite para la recopilación de eventos de syslog. toocollect datos de syslog de esta versión de las distribuciones, Hola rsyslog daemon debe estar instalado y configurado tooreplace sysklog, 

agente de Hello incluye varios paquetes. archivo de la versión Hello contiene Hola después de paquetes, disponibles mediante la agrupación de shell Hola ejecución con `--extract`:

**Paquete** | **Versión** | **Descripción**
----------- | ----------- | --------------
omsagent | 1.4.0 | Hola agente de Operations Management Suite para Linux
omsconfig | 1.1.1 | Agente de configuración para hello agente de OMS
omi | 1.2.0 | Infraestructura de administración abierta (OMI), un servidor de CIM ligero
scx | 1.6.3 | Proveedores de CIM OMI para métricas de rendimiento del sistema operativo
apache-cimprov | 1.0.1 | Proveedor de supervisión de rendimiento de servidor HTTP de Apache para OMI. Se instala si se detecta un servidor HTTP de Apache.
mysql-cimprov | 1.0.1 | Proveedor de supervisión de rendimiento de servidor MySQL Server para OMI. Se instala si se detecta un servidor MySQL/MariaDB.
docker-cimprov | 1.0.0 | Proveedor de Docker para OMI. Se instala si se detecta Docker.

### <a name="compatibility-with-system-center-operations-manager"></a>Compatibilidad con System Center Operations Manager
Hola agente de OMS para Linux comparte archivos binarios del agente con el agente de System Center Operations Manager de Hola. Si instala Hola agente de OMS para Linux en un sistema administrado por Operations Manager, Hola paquetes OMI y SCX versión más reciente de hello equipo tooa. En esta versión, Hola OMS y System Center 2016 - agentes de Operations Manager/Operations Manager 2012 R2 para Linux son compatibles. 

> [!NOTE]
> System Center 2012 SP1 y versiones anteriores no son actualmente compatibles con hello agente de OMS para Linux.<br>
> Si Hola agente de OMS para Linux es equipo tooa instalada que actualmente no está supervisado por Operations Manager y, a continuación, desea toomonitor equipo de hello con Operations Manager, debe modificar hello [configuración de OMI](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) anterior equipo de hello toodiscovering. **Este paso es *no* necesario si el agente de Operations Manager Hola está instalado antes de hello agente de OMS para Linux.**

### <a name="system-configuration-changes"></a>Cambios en la configuración del sistema
Después de instalar Hola agente de OMS para los paquetes de Linux, hello siguientes cambios de configuración adicionales de todo el sistema se aplican. Estos artefactos se quitan cuando se desinstala el paquete de hello omsagent.

* Se crea un usuario sin privilegios llamado: `omsagent` . Se trata de hello cuenta hello omsagent daemon se ejecuta como.
* Se crea un archivo "include" de sudoers en /etc/sudoers.d/omsagent. Esto autoriza a omsagent toorestart Hola syslog y omsagent daemons. Si no se admiten directivas "incluir" de sudo en la versión de Hola instalada de sudo, estas entradas se escriben demasiado/etcetera/sudoers.
* configuración de syslog de Hello es tooforward modificado un subconjunto de agente de toohello de eventos. Para obtener más información, vea hello **configurar la recopilación de datos** sección más adelante

### <a name="upgrade-from-a-previous-release"></a>Actualización desde una versión anterior
La actualización desde versiones anteriores a 1.0.0-47 se admite en esta versión. Instalación de hello con hello `--upgrade` comando actualiza todos los componentes de la versión más reciente de hello agente toohello.

## <a name="installing-hello-agent"></a>Instalar agente de Hola

Esta sección describe cómo tooinstall Hola agente de OMS para Linux con un bunndle, que contiene Debian y RPM paquetes para cada uno de los componentes del agente Hola.  Se puede instalar directamente o extraer paquetes individuales de tooretrieve Hola.  

En primer lugar debe el Id. de área de trabajo OMS y la clave, que puede encontrar al cambiar toohello [portal clásico de OMS](https://mms.microsoft.com).  En hello **información general sobre** página desde la selección de menú superior de hello **configuración**y, a continuación, navegue demasiado**servidores conectados de Sources\Linux**.  Puede ver Hola valor toohello de **Id. de área de trabajo** y **Primary Key**.  Copie y pegue ambos valores en el editor que prefiera.    

1. Hola de descarga más reciente [agente de OMS para Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) o [agente de OMS para Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) desde GitHub.  
2. Transferencia de hello paquete adecuado (x86 o x x64) tooyour equipo Linux mediante scp o sftp.
3. Agrupación de Hola de instalación mediante el uso de hello `--install` o `--upgrade` argumento. 

    > [!NOTE]
    > Si se instalan todos los paquetes existentes como si ya está instalado el agente de System Center Operations Manager de Hola para Linux, use hello `--upgrade` argumento. tooconnect tooOperations Management Suite durante la instalación, proporcione hello `-w <WorkspaceID>` y `-s <Shared Key>` parámetros.


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall e incorporar directamente
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>paquete de agente de hello tooupgrade
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>área de trabajo de tooa incorporado en la nube de US Government y tooinstall
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>Configurar el agente de Hola para su uso con un servidor proxy HTTP o la puerta de enlace de OMS
Hola agente de OMS para Linux es compatible con la comunicación a través de un servidor proxy HTTP o HTTPS o el servicio de puerta de enlace de OMS toohello OMS.  Se admite la autenticación anónima y básica (nombre de usuario/contraseña).  

### <a name="proxy-configuration"></a>Configuración de proxy
valor de configuración de proxy de Hello tiene Hola según la sintaxis:

`[protocol://][user:password@]proxyhost[:port]`

Propiedad|Descripción
-|-
Protocol|http o https
user|Nombre de usuario opcional para la autenticación de proxy
contraseña|Contraseña opcional para la autenticación de proxy
proxyhost|Dirección o el FQDN de hello proxy server/OMS puerta de enlace
puerto|Número de puerto opcional para hello proxy server/OMS puerta de enlace

Por ejemplo: `http://user01:password@proxy01.contoso.com:8080`

servidor proxy de Hello puede especificarse durante la instalación o modificando el archivo de configuración de hello proxy.conf después de la instalación.   

### <a name="specify-proxy-configuration-during-installation"></a>Especificación de la configuración de proxy durante la instalación
Hola `-p` o `--proxy` toouse de configuración de proxy de Hola que especifica el argumento para el paquete de instalación de hello omsagent. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>Definir configuración de proxy de hello en un archivo
configuración de proxy de Hola se puede establecer en archivos de hello `/etc/opt/microsoft/omsagent/proxy.conf` y `/etc/opt/microsoft/omsagent/conf/proxy.conf `. archivos de Hola se pueden crear o editar directamente, pero sus permisos deben ser usuario de omiuser de hello toogrant actualizada permiso de lectura en los archivos de saludo. Por ejemplo:
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>Quitando a la configuración de proxy de Hola
tooremove una configuración de proxy definida previamente y revertir toodirect conectividad, quite el archivo de hello proxy.conf:
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Incorporación con Operations Management Suite
Si un identificador de área de trabajo y la clave no se proporcionaron durante la instalación del paquete de hello, el agente de hello debe estar registrada posteriormente con Operations Management Suite.

### <a name="onboarding-using-hello-command-line"></a>Incorporación mediante la línea de comandos de Hola
Ejecute hello omsadmin.sh comando proporcionando el Id. de área de trabajo de Hola y de clave para el área de trabajo. Este comando debe ejecutarse como raíz (con elevación sudo):
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>Incorporación mediante un archivo
1.  Crear archivo hello `/etc/omsagent-onboard.conf`. archivo Hello debe ser de lectura y escritura para la raíz.
`sudo vi /etc/omsagent-onboard.conf`
2.  Inserte Hola después de líneas en el archivo de hello con su Id. de área de trabajo y la clave compartida:

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  Siguiente ejecución Hola comando tooOnboard tooOMS:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  se elimina el archivo Hello en incorporar correctamente.

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>Habilitar hello agente de OMS para Linux tooreport tooSystem Center Operations Manager
Realizar Hola siguiendo los pasos tooconfigure Hola agente de OMS para el grupo de administración de System Center Operations Manager de Linux tooreport tooa.  

1. Editar archivo hello`/etc/opt/omi/conf/omiserver.conf`
2. Asegúrese de que Hola línea que comienza con **httpsport =** define Hola puerto 1270. Por ejemplo: `httpsport=1270`
3. Reinicie el servidor de OMI de hello:`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>Registros del agente
Hola registros de hello agente de OMS para Linux se encuentran en: `/var/opt/microsoft/omsagent/<workspace id>/log/` Hola registros de programa de hello omsconfig (configuración del agente) se encuentran en: `/var/opt/microsoft/omsconfig/log/` los registros de componentes OMI y SCX hello (que proporcionan datos de métricas de rendimiento) se pueden encontrar en:`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>Configuración de rotación de registros##
configuración de rotación de registros de Hola de omsagent puede encontrarse en:`/etc/logrotate.d/omsagent-<workspace id>`

valores predeterminados de Hello son: 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>Hola Desinstalar agente de OMS para Linux
Hello paquetes de agente se pueden desinstalar ejecución archivo .sh del paquete Hola con hello `--purge` argumento, que quita completamente el agente de Hola y su configuración del equipo de Hola.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>Solución de problemas

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>Problema: No se puede tooconnect a través de proxy tooOMS

#### <a name="probable-causes"></a>Causas probables
* proxy de Hello especificado durante la incorporación era incorrecta
* Hola extremos de servicio de OMS no son whitelistested en su centro de datos 

#### <a name="resolutions"></a>Soluciones
1. Reonboard toohello servicio de OMS con hello agente de OMS para Linux mediante el uso de hello siguiente comando con la opción de hello `-v` habilitado. Esto permite que un resultado detallado del agente de hello conexión a través de proxy de hello toohello servicio de OMS. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Revise la sección de hello [agente de Hola de configuración para su uso con un proxy HTTP server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify ha configurado correctamente Hola toocommunicate de agente a través de un servidor proxy.    
* Comprueba que la Hola después de los puntos de conexión de servicio de OMS están en la lista blanca:

    |Recurso del agente| Puertos |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Puerto 443|   
    |*.oms.opinsights.azure.com | Puerto 443|   
    |ods.systemcenteradvisor.com | Puerto 443|   
    |*.blob.core.windows.net/ | Puerto 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>Problema: Recibir un error 403 al tratar de tooonboard

#### <a name="probable-causes"></a>Causas probables
* La fecha y la hora son incorrectas en el servidor Linux 
* El identificador y la clave de área de trabajo usados son incorrectos

#### <a name="resolution"></a>Resolución

1. Comprobar tiempo de hello en el servidor Linux con fecha de comando Hola. Si es hora de hello +/-15 minutos de la hora actual, incorporación produce un error. toocorrect esta actualización Hola fecha y/o la zona horaria del servidor Linux. 
2. Compruebe que ha instalado Hola versión más reciente del programa Hola a agente de OMS para Linux.  versión más reciente de Hello ahora le notifica si el sesgo horario está causando el error de incorporación de Hola.
3. Reonboard usando correcto Id. de área de trabajo y la clave de área de trabajo siguiendo las instrucciones de instalación de hello anteriormente en este tema.

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>Problema: Vea un error 404 y 500 en el archivo de registro de hello justo después de la incorporación
Se trata de un problema conocido que se produce con la primera carga de datos de Linux en un área de trabajo de OMS. Esto no afecta a los datos que se envían ni a la experiencia del servicio.

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>Problema: No aparece ningún dato en el portal de OMS Hola

#### <a name="probable-causes"></a>Causas probables

- Error de servicio de OMS de incorporación toohello
- Toohello de conexión que se bloquea el servicio de OMS
- Se está haciendo la copia de seguridad de los datos del agente OMS para Linux

#### <a name="resolutions"></a>Soluciones
1. Comprobar si Hola de incorporación OMS servicio tuvo éxito comprobando si existe hello siguiente archivo:`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Reonboard con hello `omsadmin.sh` instrucciones de línea de comandos
3. Si utiliza a un proxy, consulte pasos de resolución de proxy toohello proporcionados anteriormente.
4. En algunos casos, cuando Hola agente de OMS para Linux no puede comunicarse con servicio de OMS, Hola datos en el agente de hello están el tamaño de búfer lleno de toohello en cola, que es de 50 MB. Hola agente de OMS para Linux debe reiniciarse ejecutando el siguiente comando de hello: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Este problema se ha corregido en la versión 1.1.0-28 y posteriores del agente.
> 