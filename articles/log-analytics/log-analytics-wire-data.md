---
title: "solución de datos de análisis de registros aaaWire | Documentos de Microsoft"
description: "Datos de conexión son datos consolidados de red y rendimiento de los equipos con agentes de OMS, como agentes conectados con Windows y Operations Manager. Datos de la red se combinan con la toohelp de datos de registro correlacionar los datos."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a>Solución Wire Data 2.0 (versión preliminar) en Log Analytics

![Símbolo de Wire Data](./media/log-analytics-wire-data/wire-data2-symbol.png)

Los datos de conexión son datos consolidados de red y rendimiento de los equipos con agentes de OMS, incluidos los agentes conectados con Operations Manager, Windows y Linux. Datos de red se combinan con los otro toohelp de datos de registro correlacionar los datos.

Además agentes tooOMS, Hola solución datos de conexión utiliza a agentes de Microsoft Dependency que instalación en equipos de su infraestructura de TI. Tooand dependencia agentes monitor red datos enviados desde los equipos de red niveles 2 y 3 en hello [modelo OSI](https://en.wikipedia.org/wiki/OSI_model), incluidos Hola distintos protocolos y puertos usados. A continuación, se envían datos tooLog análisis de uso de agentes.

> [!NOTE]
> No se puede agregar la versión anterior de Hola de áreas de trabajo toonew solución de datos de conexión de Hola. Si tiene solución datos de conexión original Hola habilitada, puede seguir toouse. Sin embargo, toouse 2.0 de datos de conexión, primero debe quitar versión original de Hola.

De forma predeterminada, Log Analytics recopila datos registrados de CPU, memoria, disco y los datos de rendimiento de red de contadores integrados en Windows. Recopilación de red y otro datos se realiza en tiempo real para cada agente, incluidas las subredes y los protocolos de nivel de aplicación que usa equipo Hola. Puede agregar otros contadores de rendimiento en página de configuración de hello en la pestaña de registros de Hola.

Si ha usado [sFlow](http://www.sflow.org/) u otro software con [protocolo NetFlow de Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), Hola, a continuación, estadísticas y datos de conexión que vea será tooyou familiar.

Algunos de los tipos de Hola de consultas de búsqueda de registro integradas son:

- Agentes que proporcionan datos de conexión
- Dirección IP de los agentes que proporcionan datos de conexión
- Comunicaciones salientes por direcciones IP
- Número de bytes enviados por protocolos de aplicación
- Número de bytes enviados por un servicio de aplicación
- Bytes recibidos por distintos protocolos
- Número total de bytes enviados y recibidos por versión IP
- Promedio de latencia de las conexiones que se midieron de forma fiable
- Procesos de equipo que iniciaron o recibieron tráfico de red
- Cantidad de tráfico de red de un proceso

Al realizar una búsqueda mediante datos de conexión, puede filtrar y tooview información acerca de datos de grupo Hola agentes y protocolos principales. O puede ver cuándo determinados equipos (direcciones IP y MAC) se comunicaron entre sí, durante cuánto tiempo y cuántos datos se enviaron (básicamente, verá metadatos sobre el tráfico de red, que se basan en la búsqueda).

Pero como está viendo los metadatos, no son necesariamente útiles para la solución de problemas detallada. Los datos de conexión de Log Analytics no son una captura completa de los datos de red. Por tanto, no están diseñados para la solución de problemas profunda en el nivel de paquete. Hola ventaja de usar el agente de hello, en comparación con los métodos de recopilación de tooother, que no tiene dispositivos tooinstall, volver a configurar los conmutadores de red o realizar configuraciones complicadas. Datos de conexión están simplemente basados en agente: instalar agente de hello en un equipo y estos supervisarán su propio tráfico de red. Otra ventaja es que cuando desee que las cargas de trabajo de toomonitor está ejecutando en proveedores de nube o proveedor de servicios de hospedaje o Microsoft Azure, donde usuario hello no tiene la capa de tejido de Hola.

## <a name="connected-sources"></a>Orígenes conectados

Los datos de conexión obtiene sus datos de hello Microsoft Dependency Agent. Hola Dependency Agent depende de hello agente de OMS para su análisis tooLog de conexiones. Esto significa que un servidor debe tener Hola instalado y configure primero el agente de OMS y, a continuación, instalar Hola Dependency Agent. Hello tabla siguiente describen los orígenes de hello conectado que admite la solución de datos de conexión de Hola.

| **Origen conectado** | **Compatible** | **Descripción** |
| --- | --- | --- |
| Agentes de Windows | Sí | Wire Data analiza y recopila datos de equipos del agente de Windows. <br><br> En suma toohello [agente de OMS](log-analytics-windows-agents.md), agentes de Windows requieren Hola Microsoft Dependency Agent. Vea hello [los sistemas operativos compatibles](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) para obtener una lista completa de las versiones de sistema operativo. |
| Agentes de Linux | Sí | Wire Data analiza y recopila datos de equipos del agente de Linux.<br><br> En suma toohello [agente de OMS](log-analytics-linux-agents.md), agentes de Linux requieren Hola Microsoft Dependency Agent. Vea hello [los sistemas operativos compatibles](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) para obtener una lista completa de las versiones de sistema operativo. |
| Grupo de administración de System Center Operations Manager | Sí | Wire Data analiza y recopila datos de los agentes de Windows y Linux en un [grupo de administración de System Center Operations Manager](log-analytics-om-agents.md) conectado. <br><br> Se requiere una conexión directa de tooLog de equipo de agente de System Center Operations Manager de hello análisis. Datos se reenvían desde tooLog de grupo de administración de hello análisis. |
| Cuenta de almacenamiento de Azure | No | Los datos de conexión recopila datos de equipos de agente, así que no hay ningún dato del mismo toocollect desde el almacenamiento de Azure. |

En Windows, Hola Microsoft Monitoring Agent (MMA) es usado por toogather de System Center Operations Manager y análisis de registros y enviar datos. Según el contexto de hello, agente de Hola se denomina hello agente de System Center Operations Manager, agente de OMS, agente de registro del análisis, MMA o Direct Agent. System Center Operations Manager y análisis de registros proporcionan versiones ligeramente diferentes de hello MMA. Entre estas versiones pueden mostrar tooSystem Center Operations Manager, tooLog análisis o tooboth.

En Linux, Hola agente de OMS para Linux recopila y envía datos tooLog análisis. Puede usar los datos de conexión en servidores con agentes de OMS directo o en servidores que están conectado tooLog análisis a través de grupos de administración de System Center Operations Manager.

En este artículo, hace referencia a los agentes tooall, si Linux o Windows, si grupo de administración de System Center Operations Manager tooa conectado o directamente tooLog análisis se denomina hello _agente de OMS_. Nombre de la implementación específica de Hola de agente de Hola vamos a usar solo si es necesario para el contexto.

Hola Dependency Agent no transmite los datos en Sí y no requiere puertos ni toofirewalls de cambios. datos de Hello en los datos de conexión se siempre transmite por tooLog agente OMS Hola análisis, ya sea directamente o utilizando Hola puerta de enlace de OMS.

![diagrama de agente](./media/log-analytics-wire-data/agents.png)

Si es un usuario de System Center Operations Manager con un tooLog de grupo conectado análisis de administración:

- Cuando los agentes de System Center Operations Manager pueden tener acceso a Hola Internet tooconnect tooLog análisis, se requiere ninguna configuración adicional.
- Necesitarás tooconfigure Hola puerta de enlace de OMS toowork con System Center Operations Manager cuando los agentes de System Center Operations Manager no pueden tener acceso a análisis de registros a través de Internet de Hola.

Si usas Hola Direct Agent, debe a tooconfigure Hola OMS propio agente tooconnect tooLog análisis o tooyour puerta de enlace de OMS. Puede descargar Hola puerta de enlace de OMS de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

## <a name="prerequisites"></a>Requisitos previos

- Requiere hello [una visión general y análisis](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) oferta de la solución.
- Si está utilizando la versión anterior de Hola de hello solución datos de conexión, debe quitarlo primero. Sin embargo, todos los datos capturados a través de la solución de datos de conexión original Hola sigue estando disponible en el cable datos 2.0 y búsqueda de registros.
- Privilegios de administrador son tooinstall necesaria o desinstalación Hola Dependency Agent.
- Hola Dependency Agent debe instalarse en un equipo con un sistema operativo de 64 bits.

### <a name="operating-systems"></a>Sistemas operativos

Hello las secciones siguientes enumeran Hola admitida sistemas de operativos para hello Dependency Agent. Wire Data no admite arquitecturas de 32 bits para ningún sistema operativo.

#### <a name="windows-server"></a>Windows Server

- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

#### <a name="windows-desktop"></a>Escritorio de Windows

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux y Oracle Linux (con kernel RHEL)

- Se admiten solo versiones de kernel SMP Linux y predeterminados.
- Las versiones de kernel no estándar, como PAE y Xen, no son compatibles con ninguna distribución de Linux. Por ejemplo, un sistema con la cadena de versión de Hola de _2.6.16.21-0.8-xen_ no se admite.
- No se admiten los kernel personalizados, incluidas las recompilaciones de kernels estándar.
- No se admite el kernel de CentOSPlus.
- Unbreakable Enterprise Kernel (UEK) de Oracle se aborda en una sección posterior de este artículo.

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| **Versión del sistema operativo** | **Versión de kernel** |
| --- | --- |
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7,2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| **Versión del sistema operativo** | **Versión de kernel** |
| --- | --- |
| 6.0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4. | 2.6.32-358 |
| 6.5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6,8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5

| **Versión del sistema operativo** | **Versión de kernel** |
| --- | --- |
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398 <br> 2.6.18-400 <br>2.6.18-402 <br>2.6.18-404 <br>2.6.18-406 <br> 2.6.18-407 <br> 2.6.18-408 <br> 2.6.18-409 <br> 2.6.18-410 <br> 2.6.18-411 <br> 2.6.18-412 <br> 2.6.18-416 <br> 2.6.18-417 <br> 2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux con Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6

| **Versión del sistema operativo** | **Versión de kernel** |
| --- | --- |
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4. | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| **Versión del sistema operativo** | **Versión de kernel** |
| --- | --- |
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11

| **Versión del sistema operativo** | **Versión de kernel** |
| --- | --- |
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10

| **Versión del sistema operativo** | **Versión de kernel** |
| --- | --- |
| 10 SP4 | 2.6.16.60 |

#### <a name="dependency-agent-downloads"></a>Descargas de Dependency Agent

| **Archivo** | **SISTEMA OPERATIVO** | **Versión** | **SHA-256** |
| --- | --- | --- | --- |
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |



## <a name="configuration"></a>Configuración

Realizar Hola después de la solución de datos de conexión de pasos tooconfigure Hola para las áreas de trabajo.

1. Habilitar la solución de análisis de registros de actividad de Hola de hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).
2. Instalar Hola Dependency Agent en cada equipo donde desea tooget datos. Hola Dependency Agent puede supervisar a vecinos de tooimmediate de conexiones, por lo que puede que no tenga a un agente en cada equipo.

### <a name="install-hello-dependency-agent-on-windows"></a>Instalar Hola Dependency Agent en Windows

Privilegios de administrador son tooinstall necesaria o desinstalación el agente de Hola.

Hola Dependency Agent está instalado en equipos que ejecutan Windows mediante InstallDependencyAgent Windows.exe. Si ejecuta este archivo ejecutable sin ninguna opción, se inicia a un asistente que puede seguir tooinstall interactivamente.

Usar hello siguiendo los pasos tooinstall Hola Dependency Agent en cada equipo que ejecuta Windows:

1. Instalación Hola agente de OMS mediante el uso de instrucciones de hello en [Windows conectar equipos toohello servicio de análisis de registros de Azure](log-analytics-windows-agents.md).
2. Descargar agente para Windows hello mediante el vínculo de hello en la sección anterior de hello y, a continuación, ejecutarlo mediante el siguiente comando de hello: InstallDependencyAgent Windows.exe
3. Siga el agente de hello Asistente tooinstall Hola.
4. Si Hola Dependency Agent se produce un error toostart, compruebe los registros de Hola para obtener información detallada del error. En los agentes de Windows, el directorio de registro de hello es %Programfiles%\Microsoft Agent\logs de dependencia.

#### <a name="windows-command-line"></a>Línea de comandos de Windows

Usar opciones de hello siguientes tooinstall de tabla de una línea de comandos. ¿una lista de indicadores de instalación de hello, ejecute el instalador de hello mediante el uso de hello toosee /? de la manera siguiente.

InstallDependencyAgent-Windows.exe /?

| **Marca** | **Descripción** |
| --- | --- |
| <code>/?</code> | Obtener una lista de opciones de línea de comandos de Hola. |
| <code>/S</code> | Realice una instalación silenciosa sin preguntas. |

Archivos de hello Windows Dependency Agent se colocan en C:\Program Files\Microsoft Dependency Agent de forma predeterminada.

### <a name="install-hello-dependency-agent-on-linux"></a>Instalar Hola Dependency Agent en Linux

Acceso a la raíz es necesario tooinstall o configurar el agente de Hola.

Hola Dependency Agent está instalado en equipos Linux a través de InstallDependencyAgent-Linux64.bin, un script de shell con un archivo binario autoextraíble. Puede ejecutar el archivo hello mediante _sh_ o agregar ejecutar propio archivo de toohello permisos.

Usar hello siguiendo los pasos tooinstall Hola Dependency Agent en cada equipo Linux:

1. Instalación Hola agente de OMS mediante el uso de instrucciones de hello en [recopilar y administrar datos de equipos Linux](log-analytics-agent-linux.md).
2. Descargar agente de Linux dependencia hello mediante el vínculo de hello en la sección anterior de hello y, a continuación, volver a instalarlo como raíz utilizando el siguiente comando de hello: sh InstallDependencyAgent Linux64.bin
3. Si Hola Dependency Agent se produce un error toostart, compruebe los registros de Hola para obtener información detallada del error. En los agentes de Linux, directorio de registro de hello es: /var/opt/microsoft/dependency-agent/log.

toosee una lista de indicadores de instalación de hello, ejecute el programa de instalación de hello con hello `-help` marca como se indica a continuación.

```
InstallDependencyAgent-Linux64.bin -help
```

| **Marca** | **Descripción** |
| --- | --- |
| <code>-help</code> | Obtener una lista de opciones de línea de comandos de Hola. |
| <code>-s</code> | Realice una instalación silenciosa sin preguntas. |
| <code>--check</code> | Comprobar permisos y sistema operativo de hello pero no instale al agente de Hola. |

Archivos de hello Dependency Agent se colocan en hello siguientes directorios:

| **Archivos** | **Ubicación** |
| --- | --- |
| Archivos principales | /opt/microsoft/dependency-agent |
| Archivos de registro | /var/opt/microsoft/dependency-agent/log |
| Archivos de configuración | /etc/opt/microsoft/dependency-agent/config |
| Archivos ejecutables de servicio | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br><br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| Archivos binarios de almacenamiento | /var/opt/microsoft/dependency-agent/storage |

### <a name="installation-script-examples"></a>Ejemplos de script de instalación

tooeasily implementar Hola Dependency Agent en varios servidores al mismo tiempo, ayuda a toouse una secuencia de comandos. Puede usar hello después toodownload de ejemplos de secuencias de comandos e instalar Hola Dependency Agent en Windows o Linux.

#### <a name="powershell-script-for-windows"></a>Script de PowerShell para Windows

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a>Script de shell para Linux

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a>Configuración de estado deseada

Hola toodeploy Dependency Agent a través de la configuración de estado deseado, puede usar el módulo xPSDesiredStateConfiguration de Hola y un poco de código como Hola siguiente:

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a>Desinstalar Hola Dependency Agent

Usar hello después toohelp secciones quitar Hola Dependency Agent.

#### <a name="uninstall-hello-dependency-agent-on-windows"></a>Desinstalar Hola Dependency Agent en Windows

Un administrador puede desinstalar el agente de dependencia de Hola para Windows a través del Panel de Control.

Un administrador también puede ejecutar %Programfiles%\Microsoft dependencia Agent\Uninstall.exe toouninstall Hola Dependency Agent.

#### <a name="uninstall-hello-dependency-agent-on-linux"></a>Desinstalar Hola Dependency Agent en Linux

desinstalación de toocompletely Hola Dependency Agent de Linux, debe quitar el propio agente Hola y Hola conector, que se instala automáticamente con el agente de Hola. Puede desinstalar ambos mediante Hola siguiente único comando:

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a>Módulos de administración

Cuando los datos de conexión se activa en un área de trabajo de análisis de registros, un módulo de administración de 300 KB se envía servidores de Windows hello tooall en esa área de trabajo. Si está utilizando agentes de System Center Operations Manager en un [grupo de administración conectado](log-analytics-om-agents.md), Hola módulo de administración de Monitor de dependencia se ha implementado desde System Center Operations Manager. Si los agentes de hello están conectados directamente, análisis de registros ofrece el módulo de administración de Hola.

módulo de administración de Hola se denomina Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Se escribe en: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs. origen de datos de Hola que usa el módulo de administración de hello es: % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="using-hello-solution"></a>Uso de solución de Hola

**Instalar y configurar soluciones de Hola**

Usar hello después tooinstall de información y configurar soluciones de Hola.

- Hola solución datos de conexión adquiere datos desde equipos que ejecuten Windows Server 2012 R2, Windows 8.1 y sistemas operativos posteriores.
- Se requiere Microsoft .NET Framework 4.0 o posterior en los equipos donde desea que los datos de conexión tooacquire desde.
- Agregar Hola datos de conexión solución tooyour análisis de registros área de trabajo mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md). No es necesario realizar ninguna configuración más.
- Si desea que los datos de conexión de tooview para una solución concreta, necesita solución de hello toohave ya agregado tooyour área de trabajo.

Después de tener instalados agentes e instalar soluciones de hello, mosaico de hello 2.0 de datos de conexión aparece en el área de trabajo.

> [!NOTE]
> Actualmente, debe usar datos de conexión de hello OMS tooview portal. No puede usar datos de conexión de hello tooview de portal de Azure.

![Icono de Wire Data](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a>Uso de solución de hello 2.0 de datos de conexión

En el portal de OMS de hello, haga clic en hello **conexión datos 2.0** icono tooopen Hola o panel de datos de conexión. panel de Hello incluye módulos de hello en hello en la tabla siguiente. Cada hoja se enumera los elementos de too10 coincidentes que han especificado criterios del módulo para hello ámbito y el tiempo de intervalo. Puede ejecutar una búsqueda de registros que devuelve todos los registros, haga clic en **ver todas** en parte inferior de la hoja de Hola o haciendo clic en el encabezado de la hoja de Hola de Hola.

| **Hoja** | **Descripción** |
| --- | --- |
| Agentes que capturan el tráfico de red | Muestra el número de Hola de agentes que se captura el tráfico de red y enumera Hola top 10 equipos que se capturan el tráfico. Haga clic en hello número toorun una búsqueda de registros para <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>. Haga clic en un equipo en hello lista toorun una búsqueda de registros devuelve Hola número total de bytes capturados. |
| Subredes locales | Muestra el número de Hola de subredes locales que se han descubierto agentes.  Haga clic en hello número toorun una búsqueda de registros para <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> que enumera todas las subredes con número de Hola de bytes enviados a través de cada uno de ellos. Haga clic en una subred de hello lista toorun una búsqueda de registros devuelve Hola número total de bytes enviados a través de la subred de Hola. |
| Protocolos de nivel de aplicación | Muestra el número de Hola de protocolos de nivel de aplicación en uso, como detectados por los agentes. Haga clic en hello número toorun una búsqueda de registros para <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>. Haga clic en un protocolo toorun una búsqueda de registros devolver Hola número total de bytes enviados con el protocolo de saludo. |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Panel de Wire Data](./media/log-analytics-wire-data/wire-data-dash.png)

Puede usar hello **agentes que capturan el tráfico de red** toodetermine hoja cuánto ancho de banda de red utilizada por los equipos. Esta hoja puede ayudarle fácilmente buscar hello _chattiest_ equipo en su entorno. Estos equipos se pueden sobrecargar, actuar de forma anómala o usar más recursos de red de lo normal.

![ejemplo de búsqueda de registros](./media/log-analytics-wire-data/log-search-example01.png)

De forma similar, puede usar hello **subredes locales** toodetermine hoja está moviendo el tráfico de red a través de las subredes. A menudo, los usuarios definen subredes en torno a áreas cruciales de sus aplicaciones. En esta hoja se ofrece una vista de esas áreas.

![ejemplo de búsqueda de registros](./media/log-analytics-wire-data/log-search-example02.png)

Hola **protocolos de nivel de aplicación** hoja es útil porque resulta útil saber qué protocolos están en uso. Por ejemplo, se puede esperar toonot SSH en se utiliza en el entorno de red. Ver la información disponible en la hoja de hello rápidamente puede confirmar o desmentir la expectativa.

![ejemplo de búsqueda de registros](./media/log-analytics-wire-data/log-search-example03.png)

En este ejemplo, se puede profundizar en SSH detalles toosee los equipos que usan SSH y muchos otros detalles de comunicación.

![resultados de la búsqueda de sh](./media/log-analytics-wire-data/ssh-details.png)

También es útil tooknow si el tráfico de protocolo aumenta o disminuye con el tiempo. Por ejemplo, si está aumentando la cantidad de Hola de datos que se transmiten por una aplicación, que podría ser algo que debe tener en cuenta, o que puede resultarle de interés.

## <a name="input-data"></a>Datos de entrada

Los datos de conexión recopila metadatos acerca del tráfico de red utilizan a los agentes de Hola que se ha habilitado. Cada agente envía datos cada 15 segundos aproximadamente.

## <a name="output-data"></a>Datos de salida

Se crea un registro con un tipo de _WireData_ para cada tipo de datos de entrada. Registros de datos de conexión tienen propiedades que se muestran en hello en la tabla siguiente:

| Propiedad | Descripción |
|---|---|
| Equipo | Nombre de equipo del que se recopilan los datos |
| TimeGenerated | Tiempo de registro de hello |
| LocalIP | Dirección IP del equipo local Hola |
| SessionState | Conectado o desconectado |
| ReceivedBytes | Cantidad de bytes recibidos |
| ProtocolName | Nombre del protocolo de red de hello utilizado |
| IPVersion | Versión de la dirección IP |
| Dirección | De entrada o de salida |
| MaliciousIP | Dirección IP de un origen malintencionado conocido |
| Gravedad | Gravedad del supuesto malware |
| RemoteIPCountry | País de dirección IP remota de Hola |
| ManagementGroupName | Nombre del grupo de administración de Operations Manager Hola |
| SourceSystem | Origen del que se recopilan los datos |
| SessionStartTime | Hora de inicio de la sesión |
| SessionEndTime | Hora de finalización de la sesión |
| LocalSubnet | Subred de la que se recopilan los datos |
| LocalPortNumber | Número de puerto local |
| RemoteIP | Dirección IP remota utilizada por el equipo remoto hello |
| RemotePortNumber | Número de puerto usado por dirección IP remota de Hola |
| SessionID | Un valor único que identifica la sesión de comunicaciones entre dos direcciones IP |
| SentBytes | Número de bytes enviados |
| TotalBytes | Número total de bytes enviados durante la sesión |
| ApplicationProtocol | Tipo del protocolo de red que se usa   |
| ProcessID | Id. de proceso de Windows |
| ProcessName | Ruta de acceso y nombre de archivo del proceso de Hola |
| RemoteIPLongitude | Valor de longitud IP |
| RemoteIPLatitude | Valor de latitud IP |


## <a name="next-steps"></a>Pasos siguientes

- [Buscar registros](log-analytics-log-searches.md) tooview obtener registros de búsqueda de datos de conexión.
