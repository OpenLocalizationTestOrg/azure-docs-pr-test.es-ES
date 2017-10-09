---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a>Conectar su tooLog de equipos Linux análisis
El uso de Log Analytics permite recopilar y actuar sobre los datos generados en equipos Linux. Agregar datos recopilados de Linux tooOMS permite toomanage sistemas de Linux y soluciones de contenedor como Docker, independientemente de dónde estén ubicados los equipos, prácticamente en cualquier lugar. Orígenes de datos pueden residir en su centro de datos local como servidores físicos, equipos virtuales en un servicio hospedado en la nube como Amazon Web Services (AWS) o Microsoft Azure, o incluso Hola portátil en su escritorio. Además, OMS también recopila datos de los equipos de Windows de forma similar, por lo que es compatible con un entorno informático realmente híbrido.

Puede ver y administrar los datos de todos esos orígenes con Log Analytics en OMS con un portal de administración único. Esto reduce la necesidad de hello toomonitor con muchos sistemas distintos, hace que resulte fácil tooconsume y que puede exportar cualquier dato que quiera toowhatever solución de análisis de negocios o sistema que ya tiene.

Este artículo es una guía de inicio rápido que le ayudará a recopilar y administrar los datos de los equipos Linux mediante Hola agente de OMS para Linux. Si desea obtener más detalles técnicos, como la configuración del servidor proxy, información acerca de las métricas de CollectD y orígenes de datos JSON personalizados, encontrará esa información en la [información general sobre el agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) y la [documentación completa sobre el agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) en GitHub.

Actualmente, puede recopilar Hola siguientes tipos de datos de los equipos Linux:

* Métricas de rendimiento
* Eventos Syslog
* Alertas de Nagios y Zabbix
* Registros, inventario y métricas de rendimiento del contenedor de Docker

## <a name="supported-linux-versions"></a>Versiones de Linux compatibles
Tanto la versión x86 como la x64 son compatibles oficialmente en una variedad de distribuciones de Linux. Sin embargo, también puede ejecutar Hola agente de OMS para Linux en otras distribuciones que no aparece.

* Amazon Linux 2012.09 hasta 2015.09
* CentOS Linux 5, 6 y 7
* Oracle Linux 5, 6 y 7
* Red Hat Enterprise Linux Server 5, 6 y 7
* Debian GNU/Linux 6, 7 y 8
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10
* SUSE Linux Enterprise Server 11 y 12

## <a name="oms-agent-for-linux"></a>Agente de OMS para Linux
Hola agente de Operations Management Suite para Linux consta de varios paquetes. archivo de la versión Hello contiene Hola después de paquetes, disponibles mediante la agrupación de shell Hola ejecución con `--extract`.

| **Paquete** | **Versión** | **Descripción** |
| --- | --- | --- |
| omsagent |1.1.0 |Hola agente de Operations Management Suite para Linux |
| omsconfig |1.1.1 |Agente de configuración para hello agente de OMS |
| omi |1.0.8.3 |Infraestructura de administración abierta (OMI), un servidor de CIM ligero |
| scx |1.6.2 |Proveedores de CIM OMI para métricas de rendimiento del sistema operativo |
| apache-cimprov |1.0.0 |Proveedor de supervisión de rendimiento de servidor HTTP de Apache para OMI. Solo se instala si se detecta un servidor HTTP de Apache. |
| mysql-cimprov |1.0.0 |Proveedor de supervisión de rendimiento de servidor MySQL Server para OMI. Solo se instala si se detecta un servidor MySQL/MariaDB de Apache. |
| docker-cimprov |0.1.0 |Proveedor de Docker para OMI. Solo se instala si se detecta Docker. |

### <a name="additional-installation-artifacts"></a>Artefactos de instalación adicionales
Después de instalar el agente de OMS de Hola para paquetes de Linux, hello siguientes cambios de configuración adicionales de todo el sistema se aplican. Estos artefactos se quitan cuando se desinstala el paquete de hello omsagent.

* Se crea un usuario sin privilegios llamado: `omsagent` . Se trata de hello cuenta hello omsagent daemon se ejecuta como
* Se crea un archivo "include" de sudoers en /etc/sudoers.d/omsagent este autoriza a omsagent toorestart Hola syslog y omsagent daemons. Si no se admiten directivas "incluir" de sudo en la versión de Hola instalada de sudo, estas entradas se escribirán demasiado/etcetera/sudoers.
* configuración de syslog de Hello es tooforward modificado un subconjunto de agente de toohello de eventos. Para obtener más información, vea hello **configurar la recopilación de datos** sección más adelante

### <a name="linux-data-collection-details"></a>Detalles de la recopilación de datos de Linux
Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos.

| de origen | Agente directo | Agente de SCOM | Azure Storage | ¿Se necesita SCOM? | Datos del agente de SCOM enviados a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- |
| Zabbix |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |1 minuto |
| Nagios |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |a la llegada |
| syslog |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |De Almacenamiento de Azure: 10 minutos; del agente: a la llegada |
| Contadores de rendimiento de Linux |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |Mínimo de 10 segundos, según lo programado |
| Seguimiento de cambios |![Sí](./media/log-analytics-linux-agents/oms-bullet-green.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |![No](./media/log-analytics-linux-agents/oms-bullet-red.png) |Cada hora |

### <a name="package-requirements"></a>Requisitos de paquete
| **Paquetes necesarios** | **Descripción** | **Versión mínima** |
| --- | --- | --- |
| Glibc |Biblioteca GNU C |2.5-12 |
| Openssl |Bibliotecas OpenSSL |0.9.8E o 1.0 |
| Curl |Cliente web de cURL |7.15.5 |
| Python ctypes |Bibliotecas de funciones |N/D |
| PAM |Módulos de autenticación conectables |N/D |

> [!NOTE]
> Rsyslog o syslog-ng es necesario toocollect mensajes de syslog. demonio de syslog de Hello predeterminado en la versión 5 de Red Hat Enterprise Linux, CentOS y Oracle Linux (sysklog) no se admite para la recopilación de eventos de syslog. toocollect datos de syslog de esta versión de las distribuciones, Hola rsyslog daemon debe estar instalado y configurado tooreplace sysklog.
>
>

## <a name="quick-install"></a>Instalación rápida
Ejecute hello después comandos toodownload hello omsagent, validar la suma de comprobación de hello, a continuación, instalar y agente de Hola incorporar. Los comandos son para 64 bits. Hello Id. de área de trabajo y la clave principal se encuentran en el portal de OMS de hello en **configuración** en hello **orígenes conectados** ficha.

![detalles de área de trabajo](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

Hay una variedad de otro métodos tooinstall Hola agente y actualizarlo. Puede obtener más información sobre estos en [Hola de pasos tooinstall agente de OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).

También puede ver hello [Azure tutorial en vídeo](https://www.youtube.com/watch?v=mF1wtHPEzT0).

## <a name="choose-your-linux-data-collection-method"></a>Selección del método de recopilación de datos de Linux
Cómo elegir Hola tipos de datos que lo haría con like toocollect depende de si desea que el portal de OMS toouse Hola o si prefiere editar varios archivos de configuración directamente en los clientes de Linux. Si decide que el portal de hello toouse, configuración de Hola se envía automáticamente tooall los clientes de Linux. Si necesita diferentes configuraciones para distintos clientes de Linux, se necesita archivos de cliente de tooedit individualmente o usar una alternativa como PowerShell DSC, Chef o Puppet.

Puede especificar los eventos de syslog de Hola y contadores de rendimiento que desea que toocollect mediante archivos de configuración en los equipos Linux Hola. *Si ha elegido tooconfigure la recopilación de datos mediante la edición de archivos de configuración del agente, debe deshabilitar la configuración centralizada Hola.*  Se proporcionan instrucciones a continuación de la recopilación de datos de tooconfigure en del agente de hello archivos de configuración, así como toodisable configuración central en todos los agentes de OMS para Linux o en equipos individuales.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>Deshabilitación de la administración de OMS para un equipo individual de Linux
Recopilación de datos centralizado para los datos de configuración está deshabilitada para un equipo individual de Linux con hello script OMS_MetaConfigHelper.py. Esto puede ser útil si un subconjunto de equipos debe tener una configuración especializada.

toodisable configuración centralizada:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

Habilitar toore configuración centralizada:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Contadores de rendimiento de Linux
Contadores de rendimiento de Linux son los contadores de rendimiento tooWindows similar: ambos funcionan de forma similar. Puede usar hello siguiendo los procedimientos tooadd y configurarlos. Una vez que se agregan tooOMS, se recopilan datos para estos cada 30 segundos.

### <a name="tooadd-a-linux-performance-counter-in-oms"></a>tooadd un contador de rendimiento de Linux en OMS
1. tooconfigure agentes de OMS para Linux mediante el portal de OMS hello, puede agregar contadores de rendimiento de Linux en la página de configuración de hello, haga clic en **datos**.  
2. En hello **configuración** página en **datos** , haga clic en **contadores de rendimiento de Linux** y, a continuación, seleccionar o escribir nombre hello del contador de Hola que desea tooadd.  
    ![Datos](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Si no sabe el nombre completo de hello del contador de hello, puede empezar a escribir un nombre parcial y aparecerá una lista de contadores disponibles. Cuando encuentre el contador de Hola que desee tooadd, haga clic en nombre de hello en lista de hello y, a continuación, haga clic en hello más hello de icono tooadd contador.
4. Después de agregar el contador de hello, aparece en la lista de Hola de contadores, resaltado con una barra coloreada.
5. De forma predeterminada, Hola **aplicar máquinas toomy de configuración siguientes** opción está seleccionada. Si desea toodisable enviar datos de configuración, desactive la selección de Hola.
6. Cuando haya terminado de modificar los contadores de rendimiento, en parte inferior de Hola de página de Hola haga clic en **guardar** toofinalize los cambios. cambios de configuración de Hola que haya hecho, a continuación, se envían tooall Hola agentes de OMS para Linux registrados con OMS, normalmente en 5 minutos.

### <a name="configure-linux-performance-counters-in-oms"></a>Configuración de los contadores de rendimiento de Linux en OMS
Para los contadores de rendimiento de Windows, puede elegir una instancia específica para cada contador de rendimiento. Sin embargo, para los contadores de rendimiento de Linux, cualquier instancia de un contador que elija aplica tooall contadores de secundarios de contador de hello primario. Hello tabla siguiente muestran instancias comunes Hola contadores de rendimiento de Linux y Windows tooboth disponible.

| **Nombre de la instancia** | **Significado** |
| --- | --- |
| \_Total |Total de todas las instancias de Hola |
| \* |Todas las instancias |
| (/&#124;/var) |Coincide con las instancias con nombre: / o /var |

De igual forma, intervalo de muestra de Hola que elija para un contador primario aplica tooall los contadores secundarios. En otras palabras, todas las instancias y los intervalos de muestra de contador de hello secundarios están unidos entre sí.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Incorporación y configuración de las métricas de rendimiento con Linux
Toocollect de las métricas de rendimiento se controlan mediante la configuración de hello en/etcetera/opt/microsoft/omsagent/&lt;Id. de área de trabajo&gt;/conf/omsagent.conf. Vea [métricas de rendimiento disponibles](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) para las clases disponibles y las métricas para hello agente de OMS para Linux.

Cada objeto o categoría de toocollect de las métricas de rendimiento debe definirse en el archivo de configuración de hello como una sola `<source>` elemento. sintaxis de Hello sigue siguiente patrón de Hola.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

Hola parámetros configurables de este elemento son:

* **Objeto\_nombre**: nombre de objeto de hello para la recopilación de Hola.
* **Instancia\_regex**: un *expresión regular* definir qué toocollect de instancias. Hola valor: `.*` especifica todas las instancias. métricas de procesador toocollect para solo hello \_instancia Total, podría especificar `_Total`. métricas de procesador toocollect solo hello instancias crond o sshd, puede especificar: `(crond|sshd)`.
* **Contador\_nombre\_regex**: un *expresión regular* definir qué toocollect contadores (para el objeto de hello). toocollect todos los contadores para el objeto de hello, especifique: `.*`. toocollect solo intercambio contadores de espacio para el objeto de memoria de hello, puede especificar:`.+Swap.+`
* **Intervalo:**: Hola la frecuencia con que Hola se recopilan los contadores del objeto.

configuración predeterminada de Hola para las métricas de rendimiento es:

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a>Habilitación de los contadores de rendimiento de MySQL mediante comandos de Linux
Si el servidor MySQL o MariaDB se detecta en el equipo de hello cuando se instala el paquete de hello omsagent, se instala automáticamente un proveedor de MySQL Server de supervisión de rendimiento. Este proveedor conecta el estadísticas de rendimiento para tooexpose el local servidor MySQL/MariaDB toohello. Tendrá que tooconfigure credenciales de usuario de MySQL para que hello proveedor pueda acceder Hola MySQL Server.

toodefine una predeterminado cuenta de usuario de MySQL server de hello en localhost, Hola use el ejemplo de comando siguiente.

> [!NOTE]
> archivo de credenciales de Hello debe ser legible por cuenta de hello omsagent. Se recomienda ejecutar comando de hello mycimprovauth como omsgent.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


Como alternativa, puede especificar Hola requiere credenciales de MySQL en un archivo, mediante la creación de archivo hello: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Para obtener más información acerca de cómo administrar las credenciales de MySQL para la supervisión a través del archivo mysql-auth de hello, consulte [MySQL administrar credenciales en el archivo de autenticación de hello de supervisión](#manage-mysql-monitoring-credentials-in-the-authentication-file).

Vea [permisos necesarios para los contadores de rendimiento de MySQL de la base de datos](#database-permissions-required-for-mysql-performance-counters) para obtener más información acerca de los permisos de objeto requeridos por toocollect de usuario de MySQL de hello datos de rendimiento del servidor MySQL.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Habilitación de los contadores de rendimiento del servidor HTTP de Apache mediante comandos de Linux
Si se detecta servidor HTTP Apache en el equipo de hello cuando se instala el paquete de hello omsagent, se instala automáticamente un proveedor para el servidor HTTP Apache de supervisión de rendimiento. Este proveedor se basa en un "módulo" Apache que debe cargarse en hello servidor HTTP Apache orden tooaccess los datos de rendimiento.

Puede cargar el módulo de hello con hello siguiente comando:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload Hola supervisión módulo Apache, ejecute el siguiente comando de hello:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a>datos de rendimiento de tooview con análisis de registros
1. En el portal de Operations Management Suite hello, haga clic en el icono de búsqueda de registro de hello.
2. En la barra de búsqueda de hello, escriba `* (Type=Perf)` tooview todos los contadores de rendimiento.

Dado que OMS también recopila datos del contador de rendimiento de Windows, debe acotar Hola datos tooLinux específicos de búsqueda. Por lo tanto, hello en el ejemplo siguiente se mostraría servidor rendimiento datos específicos tooan ejemplo Linux denominado Chorizo21.

```
Type=Perf Computer=chorizo*
```

![servidor de ejemplo que se muestra en los resultados de búsqueda](./media/log-analytics-linux-agents/oms-perfsearch01.png)

En los resultados de hello, puede hacer clic en **métricas** contadores de hello tooview que se recopilaron datos. Se muestran los datos en tiempo real como gráficos para cada contador.

![Métricas](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>syslog
Syslog es un protocolo similar tooWindows registros de eventos de registro de eventos: ambos funcionan de forma parecida al mostrarse en OMS.

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a>tooadd una nueva utilidad syslog de Linux en OMS
1. En hello **configuración** página en **datos** , haga clic en **Syslog** y, a continuación, toohello izquierda del icono de más hello, escriba Hola nombre de utilidad syslog de Hola que desea tooadd.
    ![Syslog de Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Si no sabe el nombre completo de Hola de utilidad de hello, puede empezar a escribir un nombre parcial y aparecerá una lista de las utilidades syslog disponibles. Cuando encuentre la utilidad syslog de hello desea tooadd, haga clic en nombre de hello en lista de hello y, a continuación, haga clic en hello más hello de icono tooadd utilidad syslog.
3. Después de agregar aparece en la lista de Hola de utilidad de hello, resaltado con una barra de color. A continuación, seleccione los niveles de gravedad de hello (categorías de información de la utilidad syslog) que desea toocollect.
4. En la parte inferior de Hola de página de hello haga clic en **guardar** toofinalize los cambios. cambios de configuración de Hola que haya hecho, a continuación, se envían tooall Hola agentes de OMS para Linux registrados con OMS, normalmente en 5 minutos.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Configuración de las utilidades de Syslog de Linux en Linux
Eventos de syslog se envían desde el demonio de syslog hello, por ejemplo rsyslog o syslog-ng, puerto local tooa ese Hola agente está escuchando. De forma predeterminada al puerto 25224. Cuando se instala el agente de hello, se aplica una configuración de syslog predeterminada. Esto se encuentra en:

Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf

Syslog-ng: /etc/syslog-ng/syslog-ng.conf

configuración de syslog de agente OMS de Hello predeterminado carga eventos syslog desde todas las utilidades con una gravedad de advertencia o superior.

> [!NOTE]
> Si modifica la configuración de syslog hello, debe reiniciar el demonio de syslog Hola Hola cambios tootake efecto.
>
>

Hola syslog configuración predeterminada para hello agente de OMS para Linux para OMS es:

#### <a name="rsyslog"></a>Rsyslog
```
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
```

#### <a name="syslog-ng"></a>Syslog ng
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a>tooview todos los eventos de Syslog con análisis de registros
1. En el portal de Operations Management Suite hello, haga clic en hello **Log Search** icono.
2. Hola **administración de registros** agrupación, elija una búsqueda de syslog predefinida y, a continuación, seleccione una toorun.

Este ejemplo muestra todos los eventos de Syslog.

![Eventos de Syslog que se muestran en la búsqueda de registros](./media/log-analytics-linux-agents/oms-linux-syslog.png)

Ahora puede profundizar en los resultados de la búsqueda.

## <a name="linux-alerts"></a>Alertas de Linux
Si usa Nagios o Zabbix toomanage los equipos Linux, a continuación, OMS puede recibir alertas de hello generadas desde esas herramientas. Sin embargo, no hay actualmente ningún método tooconfigure datos entrantes de alerta mediante el portal de OMS Hola. En su lugar, deberá tooedit un tooOMS envío de alertas de configuración archivo toostart.

### <a name="collect-alerts-from-nagios"></a>Recopilación de alertas de Nagios
toocollect las alertas de un servidor Nagios, debe hello toomake después de los cambios de configuración.

1. Usuario de hello GRANT **omsagent** archivo de registro de acceso de lectura toohello Nagios (es decir, /var/log/nagios/nagios.log). Suponiendo que el archivo de hello nagios.log es propiedad de grupo hello **nagios** , puede agregar el usuario hello **omsagent** toohello **nagios** grupo.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Modificar el archivo de hello omsagent.confconfiguration (/ etcetera/opt/microsoft/omsagent/&lt;Id. de área de trabajo&gt;/conf/omsagent.conf). Asegúrese de hello siguiendo las entradas está presentes y no comentadas:

    ```
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
    ```
3. Reiniciar el demonio omsagent hello:

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Recopilación de alertas de Zabbix
toocollect las alertas de un servidor Zabbix, se llevarán a cabo similar toothose pasos anteriores para Nagios, salvo que deberá toospecify un usuario y una contraseña en *borre el texto*. No es una solución ideal, pero seguramente cambiará pronto. tooaddress este problema, recomendamos que cree el usuario de Hola y conceder permiso toomonitor solo.

Una sección de ejemplo de archivo de configuración de hello omsagent.conf (/ etcetera/opt/microsoft/omsagent/&lt;Id. de área de trabajo&gt;/conf/omsagent.conf) para Zabbix debe ser similar a la siguiente hello:

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a>Visualización de alertas en búsqueda de Log Analytics
Después de haber configurado el tooOMS de las alertas de toosend de equipos Linux, puede usar alertas de Hola de tooview consultas de búsqueda de registro simples unos. Hello siguiente ejemplo de consulta de búsqueda devuelve todas las alertas de hello registrado que se generaron. Por ejemplo, si se produce algún tipo de problema en su infraestructura de TI, a continuación, resultados para hello siguiente ejemplo de consulta podría indicar dónde puede originarse problema Hola. Y puede rastrear fácilmente en las alertas de toohello por toohelp de sistema de origen estrecha la investigación. Hello ventaja es que no tiene necesariamente toogo toovarious los sistemas de administración de inicio de hello, siempre que las alertas se envíen tooOMS, puede empezar por ahí.

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a>tooview Nagios todas las alertas con análisis de registros
1. En el portal de Operations Management Suite hello, haga clic en hello **Log Search** icono.
2. En la barra de consulta de hello, escriba Hola después de consulta de búsqueda

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Alertas de Nagios que se muestran en la búsqueda de registros](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

Después de ver los resultados de búsqueda de hello, puede profundizar en los detalles adicionales, como *AlertState*.

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a>tooview todas las alertas de Zabbix con análisis de registros
1. En el portal de Operations Management Suite hello, haga clic en hello **Log Search** icono.
2. En la barra de consulta de hello, escriba Hola después de consulta de búsqueda

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Alertas de Zabbix que se muestran en la búsqueda de registros](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

Después de ver los resultados de búsqueda de hello, puede profundizar en los detalles adicionales, como *AlertName*.

## <a name="compatibility-with-system-center-operations-manager"></a>Compatibilidad con System Center Operations Manager
Hola agente de OMS para Linux comparte archivos binarios del agente con el agente de System Center Operations Manager de Hola. Instalar Hola agente de OMS para Linux en un sistema administrado por Operations Manager actualizaciones Hola paquetes OMI y SCX versión más reciente de hello equipo tooa. Hola agente de OMS para Linux y System Center 2012 R2 son compatibles. Sin embargo, **System Center 2012 SP1 y versiones anteriores no son actualmente compatibles con hello agente de OMS para Linux.**

> [!NOTE]
> Si Hola agente de OMS para Linux está instalado tooa equipo que no está administrado actualmente por Operations Manager y posteriormente desea toomanage equipo de hello con Operations Manager, debe modificar configuración de OMI Hola antes de detectar el equipo de Hola. **Este paso no es necesario si el agente de Operations Manager Hola está instalado antes de hello agente de OMS para Linux.**
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a>Hola tooenable agente de OMS para Linux toocommunicate con Operations Manager
1. Editar Hola archivo /etc/opt/omi/conf/omiserver.conf
2. Asegúrese de que Hola línea que comienza con **httpsport =** define Hola puerto 1270. Por ejemplo `httpsport=1270`
3. Reinicie el servidor de OMI de hello:

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>Permisos necesarios de la base de datos para los contadores de rendimiento de MySQL
toogrant usuario de supervisión de MySQL de permisos tooa, debe tener concediendo al usuario Hola Hola privilegio 'GRANT option', así como tener concedido el privilegio de Hola.

En orden para el usuario de MySQL hello tooreturn rendimiento datos Hola usuario necesita tener acceso toohello las siguientes consultas:

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

Además usuario de MySQL toothese consultas Hola requiere toohello acceso exclusivo siguientes tablas predeterminadas:

* information_schema
* mysql

Estos privilegios se pueden conceder ejecutando Hola siguientes comandos de concesión.

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a>Administrar credenciales en el archivo de autenticación de hello de supervisión de MySQL
Hola siguientes secciones lo administra las credenciales de MySQL.

### <a name="configure-hello-mysql-omi-provider"></a>Configurar Hola proveedor de OMI de MySQL
Hola proveedor de OMI de MySQL necesita un usuario de MySQL preconfigurado e instala las bibliotecas de cliente de MySQL en información de rendimiento y mantenimiento de pedidos tooquery Hola de instancia de MySQL Hola.

### <a name="mysql-omi-authentication-file"></a>Archivo de autenticación de MySQL para OMI
Proveedor de OMI de MySQL usa un toodetermine del archivo de autenticación qué instancia de MySQL Hola dirección de enlace y el puerto está escuchando en así como las credenciales toouse toogather métricas. Durante el saludo de instalación de OMI de MySQL proveedor examinará los archivos de configuración my.cnf de MySQL (ubicaciones predeterminadas) para la dirección de enlace y puerto parcialmente conjunto hello y archivo de autenticación de OMI de MySQL.

toocomplete la supervisión de una instancia del servidor MySQL, agregue un archivo de autenticación de OMI de MySQL pregenerado en el directorio correcto de Hola.

### <a name="authentication-file-format"></a>Formato del archivo de autenticación
Hola archivo de autenticación de OMI de MySQL es un archivo de texto que contiene información sobre:

* Port
* Dirección de enlace
* Nombre de usuario de MySQL
* Contraseña codificada en Base64

Hola archivo de autenticación de OMI de MySQL solo concede privilegios de usuario de Linux toohello de lectura/escritura que lo generó.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

Un archivo de autenticación de OMI de MySQL predeterminado contiene una instancia predeterminada y un número de puerto según la información disponible y analizada desde Hola que se encontró el archivo de configuración de MySQL.

instancia predeterminada de Hello es un toomake significa administrar varias instancias de MySQL en un host Linux y se indica mediante la instancia de hello con el puerto 0. Todas las instancias agregadas heredarán propiedades establecidas en la instancia predeterminada de Hola. Por ejemplo, si se agrega la instancia de MySQL que escucha en el puerto '3308', dirección de enlace, nombre de usuario y contraseña codificada en Base64 de instancia predeterminada de Hola se puede tootry usado y supervisar la instancia de hello escucha en 3308. Si instancia hello en 3308 está enlazado tooanother dirección y usa Hola el mismo nombre de usuario de MySQL y par de contraseña solo Hola volver a especificar de Hola se necesita la dirección de enlace y hello otras propiedades se heredarán.

Hola autenticación ejemplos de archivos de siguiente Hola.

Instancia predeterminada e instancia con el puerto 3308:

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

Instancia predeterminada e instancia con el puerto 3308 + diferente contraseña codificada en Base 64:

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| **Propiedad** | **Descripción** |
| --- | --- |
| Port |El puerto representa Hola Hola de puerto actual instancia de MySQL está escuchando.  puerto de Hello 0 implica que se usan las propiedades de hello siguientes para la instancia predeterminada. |
| Dirección de enlace |Hola dirección de enlace es Hola actual MySQL dirección de enlace |
| nombre de usuario |Este nombre de usuario de Hola de usuario de MySQL Hola desea instancia del servidor de MySQL de toouse toomonitor Hola. |
| Contraseña codificada en Base64 |Esta es la contraseña de Hola Hola MySQL supervisión del usuario de codificada en Base64. |
| Actualización automática |Cuando se actualiza el proveedor de OMI de MySQL Hola Hola proveedor a examinar los cambios en el archivo my.cnf de hello y sobrescribir el archivo de autenticación de OMI de MySQL Hola. Establecer este indicador tootrue o false, según las actualizaciones necesarias toohello OMI de MySQL archivo de autenticación. |

#### <a name="authentication-file-location"></a>Ubicación del archivo de autenticación
Hola archivo de autenticación de OMI de MySQL debe ser había ubicado en hello ubicación siguiente y con el nombre "mysql-auth":

/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth

archivo Hello (y el directorio auth/omsagent) debería pertenecer al usuario omsagent de Hola.

## <a name="agent-logs"></a>Registros del agente
registros de Hola para hello agente de OMS para Linux está en:

/var/opt/microsoft/omsagent/&lt;identificador de área de trabajo&gt;/log/

registros de Hola para hello agente de OMS para Linux para el programa omsconfig (configuración del agente) está en:

/var/opt/microsoft/omsconfig/log/

Los registros de componentes OMI y SCX hello (que proporcionan datos de métricas de rendimiento) está en:

/var/opt/omi/log/ y /var/opt/microsoft/scx/log

## <a name="troubleshooting-hello-oms-agent-for-linux"></a>Solución de problemas de hello agente de OMS para Linux
Usar hello después toodiagnose de información y solucionar problemas comunes.

Si ninguno de hello, solución de problemas de información de esta sección le ayuda a, también puede usar Hola después recursos toohelp resolver el problema.

* Los clientes con soporte técnico Premier pueden registrar un caso de soporte técnico mediante [Premier](https://premier.microsoft.com/).
* Los clientes con contratos de soporte técnico de Azure pueden registrarse casos de soporte técnico hello [portal de Azure](https://manage.windowsazure.com/?getsupport=true)
* Registre un [problema de GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues).
* Foro de comentarios para ideas y un informe de errores de toocreate [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

### <a name="important-log-locations"></a>Ubicación de registros importantes
| Archivo | Ruta de acceso |
| --- | --- |
| Archivo de registro del agente de OMS para Linux |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| Archivo de registro de la configuración del agente de OMS |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a>Archivos de configuración importantes
| Categoría | Ubicación del archivo |
| --- | --- |
| syslog |`/etc/syslog-ng/syslog-ng.conf`, `/etc/rsyslog.conf` o `/etc/rsyslog.d/95-omsagent.conf` |
| Rendimiento, Nagios, Zabbix, salida de OMS y agente general |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| Configuraciones adicionales |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> Los archivos de configuración de los contadores de rendimiento y Syslog se sobrescriben si se habilita la configuración del portal de OMS. Puede deshabilitar la configuración de hello Portal de OMS (para todos los nodos) o para los nodos únicos ejecutando Hola siguiente:
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>Habilitación del registro de depuración
depuración de tooenable registro, puede utilizar el complemento de salida de hello OMS y un resultado detallado.

#### <a name="oms-output-plugin"></a>Complemento de salida de OMS
FluentD permite Hola complemento toospecify niveles de registro para los niveles de registro diferente para las entradas y salidas. toospecify un nivel de registro diferente para la salida OMS, editar configuración de agente general de Hola Hola `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` archivo.

Cerca de la parte inferior de Hola Hola del archivo de configuración, cambiar hello `log_level` propiedad de `info` demasiado`debug`.

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

El registro de depuración permite toosee por lotes cargas toohello servicio de OMS separado por tipo, el número de elementos de datos y el tiempo que tarda toosend.

*Ejemplo de registro con depuración habilitada:*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>Salida detallada
En lugar de usar el complemento de salida de hello OMS, también puede generar elementos de datos directamente demasiado`stdout`, que es visible en hello agente de OMS para el archivo de registro de Linux.

En el archivo de configuración de agente general de OMS de hello en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comente Hola OMS salida complemento agregando un `#` delante de cada línea.

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

A continuación Hola complemento de salida, quitar comentario Hola Hola pasos de la sección quitando hello `#` símbolos al principio de Hola de cada línea.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a>Mensajes de Syslog reenviados no aparecen en el registro de hello
#### <a name="probable-causes"></a>Causas probables
* Hola configuración aplicada toohello Linux servidor no permita la recopilación de instalaciones de hello enviado o niveles de registro
* Syslog no reenviar correctamente toohello Linux server
* número de Hola de mensajes que se le reenvían por segundo es demasiado grande para la configuración básica de Hola de hello agente de OMS para Linux toohandle

#### <a name="resolutions"></a>Soluciones
* Compruebe que la configuración de Hola Hola Portal de OMS de Syslog tiene todas las instalaciones de Hola y niveles de registro correcto de Hola
  * **Portal de OMS &gt; Configuración &gt; Datos &gt; Syslog**
* Compruebe que syslog nativo daemons de mensajería (`rsyslog`, `syslog-ng`) es tooreceive capaz de mensajes de saludo reenviado
* Compruebe la configuración de firewall en los que no se bloquean los mensajes de Hola Syslog server tooensure
* Simular un tooOMS de mensaje de Syslog mediante hello `logger` comando: por ejemplo:
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a>Problemas de conexión tooOMS cuando usa un proxy
#### <a name="probable-causes"></a>Causas probables
* proxy Hola especificó al instalar y configurar el agente de Hola es incorrecto
* los puntos de conexión de servicio de OMS de Hello no son whitelistested en su centro de datos

#### <a name="resolutions"></a>Soluciones
* Reinstalar Hola agente de OMS para Linux mediante el siguiente comando con la opción de Hola de hello `-v` habilitado. Esto permite que un resultado detallado del agente de hello conexión a través de proxy de hello toohello servicio de OMS.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * Revise la documentación de hello para el proxy OMS en [configurar agente de Hola para su uso con un servidor proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* Compruebe que Hola siguiendo los puntos de conexión de servicio de OMS están en la lista blanca

| Recurso del agente | Puertos |
| --- | --- |
| &#42;.ods.opinsights.azure.com |Puerto 443 |
| &#42;.oms.opinsights.azure.com |Puerto 443 |
| ods.systemcenteradvisor.com |Puerto 443 |
| &#42;.blob.core.windows.net/ |Puerto 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>Se muestra un error 403 durante la incorporación
#### <a name="probable-causes"></a>Causas probables
* Hola fecha y hora no son correctos en el servidor Linux
* Hola Id. de área de trabajo y la clave de área de trabajo utilizados son incorrectas

#### <a name="resolution"></a>Resolución
* Comprobar tiempo de hello en el servidor Linux con hello `date` comando. Si Hola datos están superior o inferior a 15 minutos de hello hora actual, incorporación produce un error. toocorrect, actualizar la fecha de Hola o zona horaria del servidor Linux.
* versión más reciente de Hola de hello agente de OMS para Linux le notifica si una diferencia de tiempo está causando el error de incorporación
* Realizar la incorporación RE mediante Hola correcto de Id. de área de trabajo y la clave de área de trabajo. Vea [incorporación mediante la línea de comandos de hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obtener más información.

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a>Aparecerá un error 500 o error 404 en archivo de registro de hello después de la incorporación
Se trata de un problema conocido que se produce durante el saludo primera carga de datos de Linux en un área de trabajo OMS. Esto no afecta a los datos que se envían ni causa otros problemas. Puede pasar por alto los errores de hello cuando inicialmente la incorporación.

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a>Datos de Nagios no aparezcan en hello Portal de OMS
#### <a name="probable-causes"></a>Causas probables
* Hola omsagent usuario no tiene permisos tooread de archivo de registro de Nagios Hola
* Hola Nagios origen y las secciones del filtro todavía incluyen comentarios en archivo de hello omsagent.conf

#### <a name="resolutions"></a>Soluciones
* Agregar usuario omsagent de Hola en orden tooread del archivo de Nagios Hola. Consulte [Nagios Alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) (Alertas de Nagios) para más información.
* En hello agente de OMS para el archivo de configuración general de Linux en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, asegúrese de que **ambos** Hola Nagios secciones de origen y de filtro tienen comentarios quitados, toohello similar siguiente ejemplo.

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a>Los datos de Linux no aparecen en el Portal de OMS Hola
#### <a name="probable-causes"></a>Causas probables
* Error de servicio de OMS de incorporación toohello
* Toohello de conexión que se bloquea el servicio de OMS
* Hola agente de OMS para los datos de Linux es copia de seguridad

#### <a name="resolutions"></a>Soluciones
* Comprobar que toohello incorporación servicio de OMS se realizó correctamente comprobando que hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` existe.
* Realizar la incorporación RE mediante Hola omsadmin.sh línea de comandos. Vea [incorporación mediante la línea de comandos de hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obtener más información.
* Si utiliza a un proxy, use anterior de pasos para solucionar problemas de proxy de Hola
* En algunos casos, cuando Hola agente de OMS para Linux no puede comunicarse con servicio de OMS, Hola datos en hello agente son toohello de copia de seguridad de tamaño de búfer lleno de 50 MB. Reinicie Hola agente de OMS para Linux mediante la ejecución de hello `/opt/microsoft/omsagent/bin/service_control restart` comando.
  >[AZURE.NOTE] Este problema está corregido en el agente versión 1.1.0-28 y posteriores.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a>Configuración de contador de rendimiento de Syslog Linux no se aplica en el portal de OMS Hola
#### <a name="probable-causes"></a>Causas probables
* agente de configuración de Hola Hola agente de OMS para Linux no recuperado configuración más reciente de Hola Hola portal de OMS.
* Hello configuración modificada en el portal de hello no se aplicaron

#### <a name="resolutions"></a>Soluciones
`omsconfig`es el agente de configuración de Hola Hola agente de OMS para Linux que recupera los cambios de configuración del portal de OMS cada 5 minutos. Esta configuración es aplicado toohello agente de OMS para archivos de configuración de Linux que se encuentra en `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.

* En algunos casos, hello agente de OMS para el agente de configuración de Linux no sea capaz de toocommunicate con el servicio de configuración del portal de hello resultante en la configuración más reciente no se aplican.
* Compruebe que hello `omsconfig` agente se instala con siguiente hello:

  * `dpkg --list omsconfig` o `rpm -qi omsconfig`
  * Si no está instalado, volver a instalar versión más reciente de Hola de hello agente de OMS para Linux
* Compruebe que hello `omsconfig` agente pueda comunicarse con hello servicio de OMS

  * Ejecute hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando
    * Hello comando anterior devuelve Hola configuración que el agente recupera del portal de hello, incluida la configuración de Syslog, los contadores de rendimiento de Linux y los registros personalizados
    * Si se produce un error en el comando hello arriba, ejecute hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando. Este comando fuerza hello omsconfig agente toocommunicate con la configuración más reciente de hello OMS servicio tooretrieve Hola.

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a>Los datos de registro personalizados de Linux no aparecen en hello Portal de OMS
#### <a name="probable-causes"></a>Causas probables
* Error del servicio de incorporación tooOMS
* Hola **Hola aplicar después configuración toomy servidores Linux** no se ha seleccionado la configuración
* omsconfig no ha recogido de registro personalizada más reciente de Hola desde el portal de Hola
* Hola `omsagent` uso es registro personalizado de hello tooaccess no se puede debido a problemas de permisos de tooa o `omsagent` no se encontró. En este caso, verá Hola después de salida:
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* Se trata de un problema conocido con hello condición de carrera que se corrigió en hello agente de OMS para Linux versión 1.1.0-217

#### <a name="resolutions"></a>Soluciones
* Compruebe que ha incorporado, ha sido correctamente mediante la determinación de si hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` archivo existe.
  * Si fuera necesario, incorporar con línea de comandos de omsadmin.sh de Hola de nuevo. Vea [incorporación mediante la línea de comandos de hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) para obtener más información.
* En hello en el Portal de OMS, **configuración** en hello **datos** , asegúrese de que hello **Hola aplicar después configuración toomy servidores Linux** está seleccionada  
  ![Aplicar configuración](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* Compruebe que hello `omsconfig` agente pueda comunicarse con hello servicio de OMS

  * Ejecute hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` comando
  * Hello comando anterior devuelve Hola configuración que el agente recupera del Hola Portal, incluida la configuración de Syslog, los contadores de rendimiento de Linux y los registros personalizados
  * Si se produce un error en el comando hello arriba, ejecute hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` comando. Este comando fuerza hello omsconfig agente toocommunicate con el servicio OMS y recuperar la configuración más reciente de Hola.

En lugar de hello agente de OMS para ejecutarse como un usuario con privilegios de usuario de Linux `root`, Hola agente de OMS para Linux se ejecuta como hello `omsagent` usuario. En la mayoría de los casos, debe tener permiso explícito concedidos usuario toohello en orden tooread determinados archivos.

permiso de toogrant demasiado`omsagent` usuario, ejecute hello siguientes comandos:

1. Agregar hello `omsagent` grupo específico de usuarios tooa con`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. Conceder acceso de lectura universal toohello archivo necesario con`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Hay un problema conocido con la condición de carrera que se corrigió en hello agente de OMS para Linux versión 1.1.0-217 Hola. Después de actualizar el agente de toohello más reciente, ejecute hello después de la versión más reciente Hola de comando tooget de complemento de salida de hello:

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>Limitaciones conocidas
Revise Hola después toolearn secciones sobre las limitaciones actuales de hello agente de OMS para Linux.

### <a name="azure-diagnostics"></a>Diagnóstico de Azure
Para las máquinas virtuales de Linux ejecuta en Azure, pasos adicionales pueden ser tooallow requiere recopilación de datos mediante Diagnósticos de Azure y Operations Management Suite. **Versión 2.2** de hello extensión de diagnósticos para Linux es necesaria para la compatibilidad con hello agente de OMS para Linux.

Para obtener más información sobre cómo instalar y configurar Hola extensión de diagnósticos para Linux, consulte [usar tooenable de comando de CLI de Azure de hello extensión de diagnóstico de Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).

**Actualización de hello extensión de diagnósticos de Linux de 2.0 too2.2 ASM de la CLI de Azure:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

Estos ejemplos de comandos hacen referencia a un archivo denominado PrivateConfig.json. formato Hola de ese archivo debe parecerse al siguiente ejemplo de Hola.

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a>Sysklog no se admite.
Rsyslog o syslog-ng es necesario toocollect mensajes de syslog. demonio de syslog de Hello predeterminado en la versión 5 de Red Hat Enterprise Linux, CentOS y Oracle Linux (sysklog) no se admite para la recopilación de eventos de syslog. toocollect datos de syslog de esta versión de las distribuciones, Hola rsyslog daemon debe estar instalado y configurado tooreplace sysklog. Para obtener más información sobre cómo sustituir sysklog por rsyslog, consulte [instalar Hola recién creado rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).

## <a name="next-steps"></a>Pasos siguientes
* [Adición de soluciones de análisis de registros desde la Galería de soluciones de hello](log-analytics-add-solutions.md) tooadd funcionalidad y recopilar datos.
* Familiarizarse con [búsquedas de registro](log-analytics-log-searches.md) tooview detallada información recopilada por soluciones.
* Use [paneles](log-analytics-dashboards.md) toosave y mostrar busca en su propio personalizado.
