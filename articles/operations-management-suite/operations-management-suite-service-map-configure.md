---
title: Mapa de servicio en Operations Management Suite aaaConfigure | Documentos de Microsoft
description: "Mapa de servicio es una solución de Operations Management Suite que detecta automáticamente los componentes de la aplicación en Windows y mapas y sistemas Linux Hola comunicación entre los servicios. En este artículo se proporciona información para implementar la solución Mapa de servicio en su entorno y utilizarla en distintos escenarios."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Configuración de Service Map en Operations Management Suite
Mapa de servicio detecta automáticamente los componentes de la aplicación en los sistemas Windows y Linux y mapas Hola comunicación entre los servicios. Puede usar tooview los servidores que pensar en ellos--como sistemas interconectados que ofrecen servicios críticos. Service Map muestra las conexiones entre servidores, procesos y puertos en cualquier arquitectura conectada TCP sin una configuración necesaria que sea distinta a la instalación de un agente.

En este artículo se describe los detalles de hello de la configuración de agentes de mapa de servicio y la incorporación. Para obtener información sobre el uso de mapa de servicio, consulte [usar soluciones de mapa de servicio de hello en Operations Management Suite](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Descargas de Dependency Agent
| Archivo | SO | Versión | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>Orígenes conectados
Mapa de servicio obtiene sus datos de hello Microsoft Dependency Agent. Hola Dependency Agent depende de hello agente de OMS para su tooOperations conexiones Management Suite. Esto significa que un servidor debe tener Hola agente de OMS había instalado y configurado primero y, a continuación, Hola que se puede instalar el agente de dependencia. Hello tabla siguiente describen los orígenes de hello conectado que admite la solución de mapa de servicio de Hola.

| Origen conectado | Compatible | Description |
|:--|:--|:--|
| Agentes de Windows | Sí | Mapa de servicio analiza y recopila datos de equipos del agente de Windows. <br><br>En suma toohello [agente de OMS](../log-analytics/log-analytics-windows-agents.md), agentes de Windows requieren Hola Microsoft Dependency Agent. Vea hello [los sistemas operativos compatibles](#supported-operating-systems) para obtener una lista completa de las versiones de sistema operativo. |
| Agentes de Linux | Sí | Mapa de servicio analiza y recopila datos de equipos de agente de Linux. <br><br>En suma toohello [agente de OMS](../log-analytics/log-analytics-linux-agents.md), agentes de Linux requieren Hola Microsoft Dependency Agent. Vea hello [los sistemas operativos compatibles](#supported-operating-systems) para obtener una lista completa de las versiones de sistema operativo. |
| Grupo de administración de System Center Operations Manager | Sí | Service Map analiza y recopila datos de los agentes de Windows y Linux en un [grupo de administración de System Center Operations Manager](../log-analytics/log-analytics-om-agents.md) conectado. <br><br>Se requiere una conexión directa de tooOperations de equipo de agente de System Center Operations Manager de hello Management Suite. Datos se reenvían desde el repositorio de Operations Management Suite de toohello del grupo de administración de Hola.|
| Cuenta de almacenamiento de Azure | No | Mapa de servicio recopila datos de equipos de agente, así que no hay ningún dato del mismo toocollect desde el almacenamiento de Azure. |

Service Map solo es compatible con plataformas de 64 bits.

En Windows, System Center Operations Manager y Operations Management Suite toogather y enviar datos de supervisión usan Hola Microsoft Monitoring Agent (MMA). (Este agente se denomina hello agente de System Center Operations Manager, agente de OMS, agente de registro del análisis, MMA o Direct Agent, según el contexto de hello). System Center Operations Manager y Operations Management Suite proporcionan versiones de casilla fuera de hello diferentes de hello MMA. Entre estas versiones pueden mostrar tooSystem Center Operations Manager, tooOperations Management Suite o tooboth.  

En Linux, hello agente de OMS para Linux recopila y envía datos tooOperations Management Suite de supervisión. Puede usar el mapa de servicio en servidores con agentes de OMS directo o en servidores que están conectados tooOperations Management Suite a través de grupos de administración de System Center Operations Manager.  

En este artículo, nos referiremos agentes tooall--si Linux o Windows, si conecta tooa grupo de administración de System Center Operations Manager o directamente tooOperations Management Suite: como Hola "Agente OMS". Nombre de la implementación específica de Hola de agente de Hola vamos a usar solo si es necesario para el contexto.

agente de mapa de servicio de Hello no transmite los datos en Sí y no requiere puertos ni toofirewalls de cambios. datos de Hello en mapa de servicio siempre se transmiten en hello tooOperations de agente de OMS Management Suite, ya sea directamente o a través de hello puerta de enlace de OMS.

![Agentes de Service Map](media/oms-service-map/agents.png)

Si es un cliente de System Center Operations Manager con un tooOperations de grupo conectado administración Management Suite:

- Si los agentes de System Center Operations Manager pueden acceder a Internet tooconnect tooOperations Management Suite hello, se requiere ninguna configuración adicional.  
- Si los agentes de System Center Operations Manager no pueden obtener acceso a Operations Management Suite a través de Internet de hello, deberá tooconfigure Hola puerta de enlace de OMS toowork con System Center Operations Manager.
  
Si usas Hola OMS Direct Agent, debe tooconfigure Hola propio agente de OMS tooconnect tooOperations Management Suite o tooyour puerta de enlace de OMS. Hello puerta de enlace de OMS puede descargarse desde hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Módulos de administración
Cuando se activa el mapa de servicio en un área de trabajo de Operations Management Suite, un módulo de administración de 300 KB se envía servidores de Windows hello tooall en esa área de trabajo. Si está utilizando agentes de System Center Operations Manager en un [grupo de administración conectado](../log-analytics/log-analytics-om-agents.md), Hola módulo de administración de mapa de servicio se ha implementado desde System Center Operations Manager. Si los agentes de hello están conectados directamente, Operations Management Suite ofrece el módulo de administración de Hola.

módulo de administración de Hola se denomina Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Su escrito too%Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\. origen de datos que utiliza el módulo de administración de Hola Hola es % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID > \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Instalación
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>Instalar Hola Dependency Agent en Microsoft Windows
Privilegios de administrador son tooinstall necesaria o desinstalación el agente de Hola.

Hola Dependency Agent está instalado en equipos de Windows a través de InstallDependencyAgent Windows.exe. Si ejecuta este archivo ejecutable sin ninguna opción, se inicia a un asistente que puede seguir tooinstall interactivamente.  

Usar hello siguiendo los pasos tooinstall Hola Dependency Agent en cada equipo de Windows:

1.  Instalación Hola agente de OMS mediante el uso de instrucciones de hello en [Windows conectar equipos toohello servicio de análisis de registros de Azure](../log-analytics/log-analytics-windows-agents.md).
2.  Descargar a agente para Windows hello y ejecutarlo mediante el uso de hello siguiente comando: <br>`InstallDependencyAgent-Windows.exe`
3.  Siga el agente de hello Asistente tooinstall Hola.
4.  Si Hola Dependency Agent se produce un error toostart, compruebe los registros de Hola para obtener información detallada del error. En los agentes de Windows, el directorio de registro de hello es %Programfiles%\Microsoft Agent\logs de dependencia. 

#### <a name="windows-command-line"></a>Línea de comandos de Windows
Usar opciones de hello siguientes tooinstall de tabla de una línea de comandos. ¿una lista de indicadores de instalación de hello, ejecute el instalador de hello mediante el uso de hello toosee /? de la manera siguiente.

    InstallDependencyAgent-Windows.exe /?

| Marca | Descripción |
|:--|:--|
| /? | Obtener una lista de opciones de línea de comandos de Hola. |
| /S | Realice una instalación silenciosa sin preguntas. |

Archivos de hello Windows Dependency Agent se colocan en C:\Program Files\Microsoft Dependency Agent de forma predeterminada.

### <a name="install-hello-dependency-agent-on-linux"></a>Instalar Hola Dependency Agent en Linux
Acceso a la raíz es necesario tooinstall o configurar el agente de Hola.

Hola Dependency Agent está instalado en equipos Linux a través de InstallDependencyAgent-Linux64.bin, un script de shell con un archivo binario autoextraíble. Puede ejecutar archivo hello mediante sh o agregar ejecutar propio archivo de toohello permisos.
 
Usar hello siguiendo los pasos tooinstall Hola Dependency Agent en cada equipo Linux:

1.  Instalación Hola agente de OMS mediante el uso de instrucciones de hello en [recopilar y administrar datos de equipos Linux](https://technet.microsoft.com/library/mt622052.aspx).
2.  Instalar a agente de Linux dependencia de hello como raíz mediante Hola siguiente comando:<br>`sh InstallDependencyAgent-Linux64.bin`
3.  Si Hola Dependency Agent se produce un error toostart, compruebe los registros de Hola para obtener información detallada del error. En los agentes de Linux, el directorio de registro de hello es /var/opt/microsoft/dependency-agent/log.

toosee una lista de indicadores de instalación de hello, ejecute el programa de instalación de hello con Hola - ayuda marca como se indica a continuación.

    InstallDependencyAgent-Linux64.bin -help

| Marca | Descripción |
|:--|:--|
| -help | Obtener una lista de opciones de línea de comandos de Hola. |
| -s | Realice una instalación silenciosa sin preguntas. |
| --check | Comprobar permisos y sistema operativo de hello pero no instale al agente de Hola. |

Archivos de hello Dependency Agent se colocan en hello siguientes directorios:

| Archivos | La ubicación |
|:--|:--|
| Archivos principales | /opt/microsoft/dependency-agent |
| Archivos de registro | /var/opt/microsoft/dependency-agent/log |
| Archivos de configuración | /etc/opt/microsoft/dependency-agent/config |
| Archivos ejecutables de servicio | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| Archivos binarios de almacenamiento | /var/opt/microsoft/dependency-agent/storage |

## <a name="installation-script-examples"></a>Ejemplos de script de instalación
tooeasily implementar Hola Dependency Agent en varios servidores al mismo tiempo, ayuda a toouse una secuencia de comandos. Puede usar hello después toodownload de ejemplos de secuencias de comandos e instalar Hola Dependency Agent en Windows o Linux.

### <a name="powershell-script-for-windows"></a>Script de PowerShell para Windows
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Script de shell para Linux
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>Configuración de estado deseada
Hola toodeploy Dependency Agent a través de la configuración de estado deseado, puede usar el módulo xPSDesiredStateConfiguration de Hola y un poco de código como Hola siguiente:
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>Desinstalación
### <a name="uninstall-hello-dependency-agent-on-windows"></a>Desinstalar Hola Dependency Agent en Windows
Un administrador puede desinstalar el agente de dependencia de Hola para Windows a través del Panel de Control.

Un administrador también puede ejecutar %Programfiles%\Microsoft dependencia Agent\Uninstall.exe toouninstall Hola Dependency Agent.

### <a name="uninstall-hello-dependency-agent-on-linux"></a>Desinstalar Hola Dependency Agent en Linux
desinstalación de toocompletely Hola Dependency Agent de Linux, debe quitar el propio agente Hola y Hola conector, que se instala automáticamente con el agente de Hola. Puede desinstalar ambos mediante Hola siguiente único comando:

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>Solución de problemas
Esta sección puede ayudarle si tiene problemas para instalar o ejecutar Service Map. Si sigue sin poder resolver el problema, póngase en contacto con Soporte técnico de Microsoft.

### <a name="dependency-agent-installation-problems"></a>Problemas de instalación del agente de dependencia
#### <a name="installer-asks-for-a-reboot"></a>El instalador solicita un reinicio
Hola Dependency Agent *generalmente* no requiere un reinicio tras la instalación o desinstalación. Sin embargo, en algunos casos poco frecuentes, Windows Server requiere un toocontinue de reiniciar el equipo con una instalación. Esto sucede cuando una dependencia, normalmente Hola Microsoft Visual C++ Redistributable, requiere un reinicio debido a un archivo bloqueado.

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>Mensaje "no se puede tooinstall Dependency Agent: las bibliotecas en tiempo de ejecución Visual Studio no pudo tooinstall (código = [Número_Código])" aparece

Hola Microsoft Dependency Agent se basa en las bibliotecas en tiempo de ejecución de Microsoft Visual Studio Hola. Si hay un problema durante la instalación de las bibliotecas de hello, obtendrá un mensaje. 

instaladores de biblioteca en tiempo de ejecución de Hello crean registros en la carpeta de %LOCALAPPDATA%\temp Hola. archivo Hello es dd_vcredist_arch_yyyymmddhhmmss.log, donde *arch* es "x86" o "amd64" y *aaaammddhhmmss* es fecha hello y la hora (reloj de 24 horas) cuando se creó el registro de hello. registro de Hello proporciona detalles sobre el problema de Hola que está bloqueando la instalación.

Podría ser útil tooinstall hello [bibliotecas de tiempo de ejecución más recientes](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) usted mismo primer.

Hello tabla siguiente enumeran los números de código y las resoluciones sugeridas.

| Código | Descripción | Resolución |
|:--|:--|:--|
| 0 x 17 | instalador de la biblioteca de Hello requiere una actualización de Windows que no se instaló. | Busque en los registros del instalador de biblioteca más reciente de Hola.<br><br>Si una referencia demasiado "Windows8.1-KB2999226-x64.msu" es seguido de una línea "Error 0x80240017: paquete MSU tooexecute error," no tiene requisitos previos de hello tooinstall KB2999226. Siga las instrucciones de hello en la sección de requisitos previos de hello en [Universal en tiempo de ejecución de C en Windows](https://support.microsoft.com/kb/2999226). Podría necesita toorun Windows Update y reiniciará varias veces en los requisitos previos de orden tooinstall Hola.<br><br>Vuelva a ejecutar el instalador de Microsoft Dependency Agent Hola. |

### <a name="post-installation-issues"></a>Problemas posteriores a la instalación
#### <a name="server-doesnt-appear-in-service-map"></a>El servidor no aparece en Service Map
Si la instalación del agente de dependencia se realizó correctamente, pero no ve el servidor en hello mapa de servicio de la solución:
* ¿Se ha instalado correctamente Hola Dependency Agent? Para comprobarlo, puede comprobar toosee si está instalado el servicio de Hola y ejecutar.<br><br>
**Windows**: busque el servicio de hello denominado "Dependency de Microsoft Agent."<br>
**Linux**: busque Hola ejecutando el proceso "-dependencia-agente de microsoft."

* ¿Está en hello [libre tarifa Operations Management Suite/de análisis de registros](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? plan gratuito de hello permite la seguridad de los servidores de mapa de servicio únicos toofive. Todos los servidores posteriores no se muestran en el mapa de servicio, aunque Hola cinco anterior ya no se envían datos.

* ¿Es el registro envío de servidor y datos de rendimiento tooOperations Management Suite? Vaya tooLog búsqueda y ejecute hello después de consulta para el equipo: 

        * Computer="<your computer name here>" | measure count() by Type
        
  ¿Se obtuvo una variedad de eventos en los resultados de hello? ¿Son los datos de hello recientes? Si es así, el agente de OMS está funcionando correctamente y comunicarse con hello servicio Operations Management Suite. Si no es así, compruebe Hola agente de OMS en el servidor: [solución de problemas de agente de OMS para Windows](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) o [agente de OMS para Linux solucionar](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>El servidor aparece en Service Map, pero no tiene procesos
Si ve el servidor en el mapa de servicio, pero no tiene ningún dato de proceso o de conexión, que indica que Hola Dependency Agent está instalado y ejecutándose, pero no se cargó el controlador del kernel de Hola. 

Compruebe Hola C:\Program Files\Microsoft dependencia Agent\logs\wrapper.log archivo (Windows) o /var/opt/microsoft/dependency-agent/log/service.log (Linux). últimas líneas del archivo hello de Hello deberían indicar por qué no se cargó kernel Hola. Por ejemplo, el kernel de hello podría no admitir en Linux si ha actualizado el kernel.

## <a name="data-collection"></a>Colección de datos
Puede esperar cada tootransmit agente aproximadamente 25 MB por día, dependiendo de su complejidad la las dependencias del sistema. Cada agente envía datos de dependencia de Service Map cada 15 segundos.  

Hola Dependency Agent normalmente consume 0,1 por ciento de memoria del sistema y 0,1 por ciento de la CPU del sistema.

## <a name="supported-azure-regions"></a>Regiones de Azure compatibles
Mapa de servicio está disponible actualmente en hello después de regiones de Azure:
- Este de EE. UU.
- Europa occidental
- Centro occidental de EE.UU.


## <a name="supported-operating-systems"></a>Sistemas operativos compatibles
Hello las secciones siguientes enumeran Hola admitida sistemas de operativos para hello Dependency Agent. Service Map no admite arquitecturas de 32 bits para ningún sistema operativo.

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

### <a name="windows-desktop"></a>Escritorio de Windows
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux y Oracle Linux (con kernel RHEL)
- Se admiten solo versiones de kernel SMP Linux y predeterminados.
- Las versiones de kernel no estándar, como PAE y Xen, no son compatibles con ninguna distribución de Linux. Por ejemplo, un sistema con la cadena de versión de Hola de "2.6.16.21-0.8-xen" no se admite.
- No se admiten los kernel personalizados, incluidas las recompilaciones de kernels estándar.
- No se admite el kernel de CentOSPlus.
- Unbreakable Enterprise Kernel (UEK) de Oracle se aborda en una sección posterior de este artículo.


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| Versión del SO | Versión del kernel |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7,2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| Versión del SO | Versión del kernel |
|:--|:--|
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
| Versión del SO | Versión del kernel |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux con Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| Versión del SO | Versión del kernel
|:--|:--|
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4. | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| Versión del SO | Versión del kernel
|:--|:--|
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| Versión del SO | Versión del kernel
|:--|:--|
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| Versión del SO | Versión del kernel
|:--|:--|
| 10 SP4 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>Datos de diagnóstico y uso
Microsoft recopila automáticamente datos de uso y rendimiento mediante el uso del programa Hola a servicio de mapas de servicio. Microsoft usa esta tooprovide de datos y mejorar la calidad de hello, seguridad e integridad de hello servicio de mapas de servicio. Los datos incluyen información sobre la configuración de hello del software, como el sistema operativo y versión. También incluye dirección IP, el nombre DNS y el nombre de estación de trabajo en orden tooprovide precisas y eficaces capacidades de resolución. No recopilamos los nombres, las direcciones ni otra información de contacto.

Para obtener más información sobre el uso y recopilación de datos, vea hello [declaración de privacidad de Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Pasos siguientes
- Obtenga información acerca de cómo demasiado[usar Service Map](operations-management-suite-service-map.md) después de que se ha implementado y configurado.
