---
title: "cambios de aaaTrack con análisis de registros de Azure | Documentos de Microsoft"
description: "Hola solución de seguimiento de cambios en el análisis de registros le ayuda a identificar el software y los cambios de servicio de Windows que se producen en su entorno."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>Seguimiento de cambios de software en su entorno con hello solución de seguimiento de cambios

![Símbolo de Change Tacking](./media/log-analytics-change-tracking/change-tracking-symbol.png)

En este artículo le ayuda a uso Hola solución de seguimiento de cambios en tooeasily de análisis de registros para identificar los cambios en su entorno. solución de Hello realiza un seguimiento de cambios tooWindows y software de Linux, archivos de Windows y las claves del registro, servicios de Windows y daemons de Linux. Identificar los cambios de configuración puede ayudarle a localizar problemas operativos.

Instalar a un tipo de hello tooupdate solución Hola de agente que ha instalado. Cambios tooinstalled software, servicios de Windows y daemons de Linux en servidores de hello supervisado se leen. A continuación, se envían datos de hello toohello servicio de análisis de registros durante la nube de Hola para su procesamiento. Lógica es aplicado toohello recibe datos y servicio de nube de hello registra datos de Hola. Mediante el uso de información de hello en el panel de seguimiento de cambios de hello, puede ver fácilmente los cambios de Hola que se realizaron en su infraestructura de servidor.

## <a name="installing-and-configuring-hello-solution"></a>Instalar y configurar soluciones de Hola
Usar hello después tooinstall de información y configurar soluciones de Hola.

* Debe tener un [Windows](log-analytics-windows-agents.md), [Operations Manager](log-analytics-om-agents.md), o [Linux](log-analytics-linux-agents.md) agente en cada equipo donde desea toomonitor cambios.
* Agregar Hola Change Tracking solución tooyour área de trabajo OMS de hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview). O bien, puede agregar soluciones Hola usando información de hello en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md). No es necesario realizar ninguna otra configuración.

### <a name="configure-linux-files-tootrack"></a>Configurar tootrack de archivos de Linux
Usar hello siguiendo los pasos tooconfigure archivos tootrack en equipos Linux.

1. En el portal de OMS de hello, haga clic en **configuración** (símbolo de engranaje de hello).
2. En hello **configuración** página, haga clic en **datos**y, a continuación, haga clic en **seguimiento de archivos de Linux**.
3. En seguimiento de cambios del archivo de Linux, escriba Hola ruta de acceso completa, incluido Hola de nombre de archivo del archivo de Hola que desee tootrack y, a continuación, haga clic en hello **agregar** símbolos. Por ejemplo: "/etc/*.conf"
4. Haga clic en **Guardar**.  

> [!NOTE]
> El seguimiento de archivos de Linux tiene funcionalidades adicionales, incluido el seguimiento de directorios, recursión de los directorios y seguimiento de comodines.

### <a name="configure-windows-files-tootrack"></a>Configurar tootrack de archivos de Windows
Usar hello siguiendo los pasos tooconfigure archivos tootrack en equipos Windows.

1. En el portal de OMS de hello, haga clic en **configuración** (símbolo de engranaje de hello).
2. En hello **configuración** página, haga clic en **datos**y, a continuación, haga clic en **seguimiento de archivos de Windows**.
3. En seguimiento de cambios del archivo de Windows, escriba Hola ruta de acceso completa, incluido Hola de nombre de archivo del archivo de Hola que desee tootrack y, a continuación, haga clic en hello **agregar** símbolos. Por ejemplo: C:\Archivos de programa (x86)\Internet Explorer\iexplore.exe o C:\Windows\System32\drivers\etc\hosts.
4. Haga clic en **Guardar**.  
   ![Seguimiento de cambios de archivos de Windows](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>Configurar tootrack de claves del registro de Windows
Usar hello después tootrack de claves del registro de pasos tooconfigure en equipos Windows.

1. En el portal de OMS de hello, haga clic en **configuración** (símbolo de engranaje de hello).
2. En hello **configuración** página, haga clic en **datos**y, a continuación, haga clic en **del registro de seguimiento de Windows**.
3. En seguimiento de cambios del registro de Windows, escriba Hola toda clave que desee tootrack y, a continuación, haga clic en hello **agregar** símbolos.
4. Haga clic en **Guardar**.  
   ![Seguimiento de cambios del Registro de Windows](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Explicación de las propiedades de la colección de archivos de Linux
1. **Tipo**
   * **File** (metadatos del archivo de informe: tamaño, fecha de modificación, hash, etc.)
   * **Directory** (metadatos del directorio de informe: tamaño, fecha de modificación, etc.)
2. **Vínculos** (vínculo simbólico de Linux control hace referencia a tooother archivos o directorios)
   * **Omitir** (omitir symlinks durante recurions toonot incluyen hello archivos y directorios al que hace referencia)
   * **Siga** (vínculos simbólicos de Hola de seguimiento durante la recursividad tooalso incluyen hello archivos y directorios al que hace referencia)
   * **Administrar** (siga los vínculos simbólicos de Hola y alter tratamiento de Hola de contenido devuelto)

   > [!NOTE]   
   > no se recomienda Hola "Manage" opción de vínculos. No se admite la recuperación de contenido de los archivos.

3. **Recurse** (Recurse por los niveles de la carpeta y realizar un seguimiento de todos los archivos que cumplen la instrucción de ruta de acceso de hello)
4. **Sudo** (habilitar el acceso a los archivos o directorios que requieren el privilegio sudo)

### <a name="limitations"></a>Limitaciones
Hola solución de seguimiento de cambios no admite actualmente Hola siguientes elementos:

* Carpetas (directorios) para seguimiento de archivos de Windows
* Recursión para seguimiento de archivos de Windows
* Comodines para seguimiento de archivos de Windows
* Variables de ruta de acceso
* Sistemas de archivos de red
* Contenido del archivo

Otras limitaciones:

* Hola **tamaño máximo de archivo** columna y valores se usa en la implementación actual de Hola.
* Si recopila más de 2500 archivos en el ciclo de recopilación de 30 minutos de hello, el rendimiento de la solución puede verse reducido.
* Cuando el tráfico de red es elevado, los registros de cambio pueden tardar tooa admite un máximo de seis horas toodisplay.
* Si modifica la configuración Hola mientras se cierra un equipo, equipo Hola podría exponer los cambios de archivo que pertenecían toohello de configuración anterior.

## <a name="change-tracking-data-collection-details"></a>Detalles de la recopilación de datos de seguimiento de cambios
Seguimiento de cambios recopila el inventario de software y metadatos de servicio de Windows con agentes de Hola que ha habilitado.

Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos de seguimiento de cambios.

| plataforma | Agente directo | Agente de Operations Manager | Agente Linux | Azure Storage | ¿Se requiere Operations Manager? | Se envían los datos del agente de Operations Manager a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Windows y Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | 5 minutos too50 minutos, según el tipo de cambio de Hola. Vea Hola para obtener más información en la tabla siguiente. |


Hello siguiente tabla muestra frecuencia de recopilación de datos de Hola para tipos de Hola de cambios.

| **Tipo de cambio** | **frequency** | **¿Envía el****agente****las diferencias cuando las encuentra?** |
| --- | --- | --- |
| Registro de Windows | 50 minutos | No |
| Archivo de Windows | 30 minutos | Sí. Si no hay ningún cambio en 24 horas, se envía una instantánea. |
| Archivo de Linux | 15 minutos | Sí. Si no hay ningún cambio en 24 horas, se envía una instantánea. |
| Servicios de Windows | 30 minutos | Sí, cada 30 minutos cuando se detectan cambios. Cada 24 horas se envía una instantánea con independencia de que haya cambio o no. Por lo tanto, las instantáneas de Hola se envían incluso cuando no hay ningún cambio. |
| Demonios de Linux | 5 minutos | Sí. Si no hay ningún cambio en 24 horas, se envía una instantánea. |
| Software de Windows | 30 minutos | Sí, cada 30 minutos cuando se detectan cambios. Cada 24 horas se envía una instantánea con independencia de que haya cambio o no. Por lo tanto, las instantáneas de Hola se envían incluso cuando no hay ningún cambio. |
| Software Linux | 5 minutos | Sí. Si no hay ningún cambio en 24 horas, se envía una instantánea. |

### <a name="registry-key-change-tracking"></a>Seguimiento de cambios en las claves del Registro

Análisis de registros realiza el registro de Windows, supervisión y el seguimiento con hello solución de seguimiento de cambios. Hola de supervisión de cambios tooregistry claves sirve toopinpoint puntos de extensibilidad que pueden activar el código de terceros y malware. siguiente Hola enumerar claves del registro de la predeterminada de la hello muestra que se realiza un seguimiento por solución hello y por qué cada uno de ellos se realiza el seguimiento.

- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - Supervisa los scripts que se ejecutan al arrancar.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - Supervisa los scripts que se ejecutan al apagar el equipo.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - Supervisa las claves que se cargan antes de hello usuario inicia sesión en tootheir cuenta de Windows. Hola clave se usa para programas de 32 bits que se ejecutan en equipos de 64 bits.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components
    - Supervisa los cambios tooapplication configuración.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - Supervisa las entradas de inicio automático comunes que se enlazan directamente en el Explorador de Windows y suele ejecutar In-Process con Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - Supervisa las entradas de inicio automático comunes que se enlazan directamente en el Explorador de Windows y suele ejecutar In-Process con Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - Supervisa las entradas de inicio automático comunes que se enlazan directamente en el Explorador de Windows y suele ejecutar In-Process con Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Supervisa el registro del controlador de superposición de iconos.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Supervisa el registro del controlador de superposición de iconos para programas de 32 bits que se ejecutan en equipos de 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Supervisa si hay nuevos complementos de objeto auxiliar de explorador para Internet Explorer. Tooaccess usados Hola Document Object Model (DOM) de exploración actual de página y toocontrol Hola.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Supervisa si hay nuevos complementos de objeto auxiliar de explorador para Internet Explorer. Tooaccess usados Hola Document Object Model (DOM) de hello actual página y toocontrol la navegación para programas de 32 bits que se ejecutan en equipos de 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - Supervisa si hay nuevas extensiones de Internet Explorer, como menús de la herramienta personalizada y botones de la barra de herramientas personalizada.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - Supervisa si hay nuevas extensiones de Internet Explorer, como menús de la herramienta personalizada y botones de la barra de herramientas personalizada para programas de 32 bits que se ejecutan en equipos de 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Supervisa los controladores de 32 bits de hello asociados a wavemapper, wave1 y wave2, msacm.imaadpcm, .msadpcm, .msgsm610 y vidc. Sección de toohello [drivers] similar en hello sistema. Archivo INI.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Controladores de 32 bits de hello monitores asociados con wavemapper, wave1 y wave2, msacm.imaadpcm, .msadpcm, .msgsm610 y vidc para programas de 32 bits que se ejecutan en equipos de 64 bits. Sección de toohello [drivers] similar en hello sistema. Archivo INI.
- HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - Monitores Hola lista conocido o utilizado archivos DLL del sistema; Este sistema impide que personas aprovecharse de permisos de directorio de aplicación débil colocando en versiones de caballo de Troya de archivos DLL del sistema.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - Lista de Hola de monitores de las notificaciones de eventos de paquetes tooreceive capaz de Winlogon, modelo de soporte de inicio de sesión interactivo de hello para el sistema operativo de Windows hello.


## <a name="use-change-tracking"></a>Uso de seguimiento de cambios
Después de instala la solución de hello, puede ver resumen de Hola de cambios de los servidores supervisados mediante hello **Change Tracking** icono hello **Introducción** página de OMS.

![imagen del icono de seguimiento de cambios](./media/log-analytics-change-tracking/change-tracking-tile.png)

Puede ver la infraestructura de tooyour de cambios y, a continuación, profundizar en los detalles de hello siguientes categorías:

* Cambios realizados por el tipo de configuración para los servicios de Windows y el software
* Cambios de software tooapplications y actualizaciones para los servidores individuales
* Número total de cambios de software para cada aplicación
* Paquetes Linux
* Cambios de servicio de Windows para servidores individuales
* Cambios de demonios de Linux

![imagen del panel de seguimiento de cambios](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![imagen del panel de seguimiento de cambios](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>cambios de tooview para cualquier tipo de cambio
1. En hello **Introducción** página, haga clic en hello **Change Tracking** icono.
2. En hello **Change Tracking** panel, revise la información de resumen de hello en uno de hojas de tipo de cambio de hello y, a continuación, haga clic en uno tooview información detallada sobre él en hello **búsqueda de registros** página.
3. En cualquiera de las páginas de búsqueda de registro de hello, puede ver los resultados por tiempo, resultados detallados y el historial de búsqueda de registros. También puede filtrar por resultados de facetas toonarrow Hola.

## <a name="next-steps"></a>Pasos siguientes
* Use [búsquedas de registro de análisis de registros](log-analytics-log-searches.md) tooview obtener datos de seguimiento de cambios.
