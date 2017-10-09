---
title: aaaHow toouse PerfInsights en Microsoft Azure | Documentos de Microsoft
description: "Aprende cómo problemas de rendimiento de toouse PerfInsights tootroubleshoot VM de Windows."
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a>Cómo toouse PerfInsights 

[PerfInsights](http://aka.ms/perfinsightsdownload) es un script automatizado que recopila información de diagnóstico útil, se ejecuta cargas de esfuerzo de E/S y proporciona un toohelp de informe de análisis solucionar problemas de rendimiento de la máquina virtual de Windows en Microsoft Azure. 

Se recomienda ejecutar este script antes de abrir una incidencia de soporte técnico con Microsoft para problemas de rendimiento de la máquina virtual.

## <a name="supported-troubleshooting-scenarios"></a>Escenarios admitidos de solución de problemas

PerfInsights puede recopilar y analizar varios tipos de información que se agrupan en escenarios únicos.

### <a name="collect-disk-configuration"></a>Recopilar configuración de disco 

Este escenario recopila la configuración de disco de Hola y otra información importante, incluyendo Hola siguientes elementos:

-   Registros de eventos

-   Estado de la red para todas las conexiones entrantes y salientes

-   Opciones de configuración de red y de firewall

-   Lista de tareas para todas las aplicaciones que se están ejecutando en el sistema de Hola

-   Archivo de información creado por msinfo32 para máquina virtual (VM) de Hola

-   Opciones de configuración de base de datos de Microsoft SQL Server (si Hola VM se identifica como un servidor que ejecuta SQL Server)

-   Contadores de confiabilidad de almacenamiento

-   Revisiones importantes de Windows

-   Controladores de filtro instalados

Se trata de un conjunto de datos que no deberían afectar al sistema Hola pasivo. 

>[!Note]
>Este escenario se incluye automáticamente en cada uno de los escenarios siguientes de Hola.

### <a name="benchmarkstorage-performance-test"></a>Banco de pruebas y prueba de rendimiento de almacenamiento

Este escenario ejecuta hello [diskspd](https://github.com/Microsoft/diskspd) pruebas comparativas de prueba (IOPS y MBPS) para todas las unidades que adjunta toohello máquina virtual. 

> [!Note]
> Este escenario puede afectar al sistema de hello y no debe ejecutarse en un sistema de producción en vivo. Si es necesario, ejecute este escenario en un tooavoid de la ventana de mantenimiento dedicado algún problema. Una carga de trabajo mayor que se debe a una prueba comparativa o de seguimiento podría afectar negativamente el rendimiento de saludo de la máquina virtual.
>

### <a name="general-vm-slow-analysis"></a>Análisis general de lentitud de la máquina virtual 

Este escenario se ejecuta un [contador de rendimiento](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) seguimiento mediante contadores de Hola que se especifican en el archivo de hello Generalcounters.txt. Si hello VM no se identifica como un servidor que ejecuta SQL Server, se ejecuta un seguimiento del contador de rendimiento mediante contadores de Hola que se encuentran en el archivo de hello Sqlcounters.txt. También se incluyen datos de diagnóstico de rendimiento.

### <a name="vm-slow-analysis-and-benchmark"></a>Análisis y banco de pruebas de lentitud de la máquina virtual

En este escenario se ejecuta un seguimiento del [contador de rendimiento](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) seguido de un banco de pruebas [diskspd](https://github.com/Microsoft/diskspd). 

> [!Note]
> Este escenario puede afectar al sistema de hello y no debe ejecutarse en un sistema de producción en vivo. Si es necesario, ejecute este escenario en un tooavoid de la ventana de mantenimiento dedicado algún problema. Una carga de trabajo mayor que se debe a una prueba comparativa o de seguimiento podría afectar negativamente el rendimiento de saludo de la máquina virtual.
>

### <a name="azure-files-analysis"></a>Análisis de Azure Files 

En este escenario se ejecuta una captura especial del contador de rendimiento junto con un seguimiento de red. La captura incluye todos los contadores de "Recursos compartidos de cliente SMB" Hola. continuación de Hola se muestran algunos contadores de rendimiento claves del recurso compartido de cliente SMB que forman parte de la captura de hello:

| **Tipo**     | **Contador de recursos compartidos de cliente de SMB** |
|--------------|-------------------------------|
| E/S         | Solicitudes de datos por segundo             |
|              | Solicitudes de lectura por segundo             |
|              | Solicitudes de escritura por segundo            |
| Latency      | Media de solicitud de datos por segundo         |
|              | Media de lectura por segundo                 |
|              | Media de escritura por segundo                |
| Tamaño de E/S      | Prom. de bytes/solicitud de datos       |
|              | Prom. de bytes/lectura               |
|              | Prom. de bytes/escritura              |
| Rendimiento   | Bytes de datos por segundo                |
|              | Bytes de lectura por segundo                |
|              | Bytes de escritura por segundo               |
| Longitud de la cola | Prom. Longitud de la cola de lectura        |
|              | Prom. Longitud de la cola de escritura       |
|              | Prom. Longitud de la cola de datos        |

### <a name="custom-configuration"></a>Configuración personalizada 

Al ejecutar una configuración personalizada, todos los seguimientos (diagnóstico de rendimiento, contador de rendimiento, xperf, red, storport) se ejecutan en paralelo, dependiendo de cuántos seguimientos diferentes se seleccionan. Una vez completada la traza, herramienta de hello ejecuta banco de pruebas de diskspd de hello, si está seleccionada. 

> [!Note]
> Este escenario puede afectar al sistema de hello y no debe ejecutarse en un sistema de producción en vivo. Si es necesario, ejecute este escenario en un tooavoid de la ventana de mantenimiento dedicado algún problema. Una carga de trabajo mayor que se debe a una prueba comparativa o de seguimiento podría afectar negativamente el rendimiento de saludo de la máquina virtual.
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a>¿Qué tipo de información se recopila por script de Hola?

Obtener información acerca de la máquina virtual de Windows, los discos o almacenamiento de grupos de configuración, se recopilan los contadores de rendimiento, los registros y seguimientos distintos según el escenario de rendimiento de hello usa:

|Datos recopilados                              |  |  | Escenarios de rendimiento |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | Recopilar configuración de disco | Banco de pruebas y prueba de rendimiento de almacenamiento | Análisis general de lentitud de la máquina virtual | Análisis y banco de pruebas de lentitud de la máquina virtual | Análisis de Azure Files | Configuración personalizada |
| Información de los registros de eventos      | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Información del sistema               | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Asignación de volúmenes                       | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Asignación de discos                         | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Tareas en ejecución                    | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Contadores de confiabilidad de almacenamiento     | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Información de almacenamiento              | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Salida de fsutil                    | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Información de controlador de filtro               | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Salida de netstat                   | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Network configuration (Configuración de red)            | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Configuración del firewall           | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Configuración de SQL Server         | Sí                        | Sí                                | Sí                      | Sí                            | Sí                  | Sí                  |
| Seguimientos de diagnóstico de rendimiento * |                            |                                    | Sí                      |                                |                      | Sí                  |
| Seguimiento de contadores de rendimiento **     |                            |                                    |                          |                                |                      | Sí                  |
| Seguimiento del contador de SMB **             |                            |                                    |                          |                                | Sí                  |                      |
| Seguimiento del contador de SQL Server **      |                            |                                    |                          |                                |                      | Sí                  |
| Seguimiento de XPerf                      |                            |                                    |                          |                                |                      | Sí                  |
| Seguimiento de StorPort                   |                            |                                    |                          |                                |                      | Sí                  |
| Seguimiento de la red                    |                            |                                    |                          |                                | Sí                  | Sí                  |
| Seguimiento del banco de pruebas de diskspd ***      |                            | Sí                                |                          | Sí                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a>Seguimientos de diagnóstico de rendimiento (*)

Se ejecuta un motor basado en reglas en datos de toocollect de segundo plano de Hola y diagnosticar problemas de rendimiento en curso. Hola siguiendo las reglas es compatibles actualmente:

- Regla de HighCpuUsage: detecta períodos de uso de CPU elevados y muestra los principales consumidores de uso de CPU Hola durante esos períodos.
- Regla de HighDiskUsage: detecta períodos de uso de disco alta en discos físicos y muestra los consumidores de uso de disco principal de Hola durante esos períodos.
- Regla de HighResolutionDiskMetric: muestra métricas de IOPS, rendimiento y latencia de E/S por 50 milisegundos para cada disco físico. Ayuda a identificar los períodos de limitación de disco tooquickly.
- Regla de HighMemoryUsage: detecta los períodos de utilización de memoria alta y muestra los consumidores de uso de memoria superior Hola durante esos períodos.

> [!NOTE] 
> Actualmente, se admiten las versiones de Windows que incluyen hello .NET Framework 3.5 o versiones posteriores.

### <a name="performance-counter-trace-"></a>Seguimiento de contadores de rendimiento (**)

Recopila Hola siguiendo los contadores de rendimiento:

- \Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk
- \Cache\Dirty Pages, \Cache\Lazy Write Flushes/sec, \Server\Pool Nonpaged, Failures, \Server\Pool Paged Failures
- Contadores seleccionados bajo \Network Interface, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments,  \Network Adapter, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \Network QoS Policy\Packets, \Per Processor Network Interface Card Activity, \Microsoft Winsock BSP

#### <a name="for-sql-server-instances"></a>Para instancias de SQL Server
- \SQL Server:Buffer Manager, \SQLServer:Resource Pool Stats, \SQLServer:SQL Statistics\
- \SQLServer:Locks, \SQLServer:General, Statistics
- \SQLServer:Access Methods

#### <a name="for-azure-files"></a>Para Azure Files
\Recursos compartidos de cliente de SMB

### <a name="diskspd-benchmark-trace-"></a>Seguimiento del banco de pruebas de diskspd (***)
Pruebas de carga de trabajo de E/S de diskspd [disco del sistema operativo (escritura) y unidades de grupo (lectura/escritura)]

## <a name="run-hello-perfinsights-on-your-vm"></a>Ejecute hello PerfInsights en su máquina virtual

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a>¿Qué debo tooknow antes de ejecutar script de Hola? 

**Requisitos del script**

1.  Este script se debe ejecutar en la máquina virtual que tiene un problema de rendimiento Hola Hola. 

2.  Hola se admiten los siguientes sistemas operativos: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 y Windows 10.

**Posibles problemas al ejecutar el script de Hola en máquinas virtuales de producción:**

1.  script de Hola podría afectar negativamente el rendimiento de Hola de hello VM cuando se utiliza junto con el escenario de "Prueba comparativa" o "Custom" hello que se configura mediante XPerf o DiskSpd. Tenga cuidado al ejecutar script de Hola en un entorno de producción.

2.  Si usa script de Hola junto con el escenario de "Prueba comparativa" o "Custom" hello que se configura mediante el uso de DiskSpd, asegúrese de que ninguna otra actividad en segundo plano interfiere con la carga de trabajo de E/S de hello en discos de hello probado.

3.  De forma predeterminada, el script de Hola usa datos de toocollect de unidad de almacenamiento temporal de saludo. Si realiza un seguimiento permanece habilitado durante más tiempo, la cantidad de Hola de datos que se recopilan puede ser relevante. Esto puede reducir la disponibilidad de Hola de espacio en disco temporal de hello, por lo tanto, afectar a cualquier aplicación que se basa en esta unidad.

### <a name="how-do-i-run-perfinsights"></a>¿Cómo se puede ejecutar PerfInsights? 

toorun hello secuencia de comandos, siga estos pasos:

1. Descargue [PerfInsights.zip](http://aka.ms/perfinsightsdownload).

2. Desbloquear el archivo de hello PerfInsights.zip. toodo esto, el archivo de PerfInsights.zip de hello de menú contextual, seleccione **propiedades**. Hola **General** ficha, seleccione **Unblock** y, a continuación, seleccione **Aceptar**. Este modo se asegurará de que se ejecute el script de Hola sin le pide ninguna seguridad adicional.  

    ![Desbloquear el archivo zip de Hola](media/how-to-use-perfInsights/unlock-file.png)

3.  Expanda el archivo de PerfInsights.zip de Hola comprimido en la unidad temporal (de forma predeterminada, normalmente la unidad D hello). Hello archivo comprimido debe contener los siguientes Hola archivos y carpetas:

    ![archivos en la carpeta de hello zip](media/how-to-use-perfInsights/file-folder.png)

4.  Abra Windows PowerShell como administrador y, a continuación, ejecutar script de Hola PerfInsights.ps1.

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    Es posible que tenga tooenter "y" tooif que es más frecuentes tooconfirm que desea que la directiva de ejecución de toochange Hola.

    En el cuadro de diálogo de declinación de responsabilidades de hello, tienen información de diagnóstico tooshare de hello opción con Microsoft Support. También debe dar su consentimiento toocontinue de contrato de licencia de toohello. Realice sus selecciones y, después, haga clic en **Ejecutar script**.

    ![Cuadro de declinación de responsabilidades](media/how-to-use-perfInsights/disclaimer.png)

5.  Enviar el número de casos de hello, si está disponible, al ejecutar script de Hola (Esto es para nuestras estadísticas). A continuación, haga clic en **Aceptar**.
    
    ![escribir el Id. de soporte](media/how-to-use-perfInsights/enter-support-number.png)

6.  Seleccione la unidad de almacenamiento temporal. Hola Script puede detectar automáticamente letra Hola de unidad de Hola. Si se produce algún problema en esta fase, es posible que se le solicite unidad de hello tooselect (unidad de hello predeterminada es D). Registros generados se almacenan aquí en el registro de hello\_carpeta de colección. Después de escribir o acepte la letra de unidad de hello, haga clic en **Aceptar**.

    ![especificar la unidad](media/how-to-use-perfInsights/enter-drive.png)

7.  Seleccione un escenario de solución de problemas de hello proporcionada la lista.

       ![Seleccionar escenarios de soporte técnico](media/how-to-use-perfInsights/select-scenarios.png)

8.  También puede ejecutar PerfInsights sin la interfaz de usuario.

    siguiente Hola Hola de ejecuciones de comandos "General VM lenta analysis" escenario sin un símbolo del sistema de interfaz de usuario de la solución de problemas o captura los datos durante 30 segundos. Le pide que tooconsent toohello mismo declinación de responsabilidades y los términos de licencia que se mencionan en el paso 4.

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    Si desea PerfInsights toorun en modo silencioso, utilice la **AcceptDisclaimerAndShareDiagnostics -** parámetro. Por ejemplo, use Hola siguiente comando:

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a>¿Cómo se puede solucionar problemas mientras se ejecuta el script de Hola?

Si el script de Hola finaliza correctamente, puede limpiar un estado incoherente mediante la ejecución de script de Hola junto con Hola - conmutador de limpieza, como se indica a continuación:

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

Si se produce algún problema durante la detección automática de Hola de unidad temporal de hello, es posible que se le solicite unidad de hello tooselect (unidad de hello predeterminada es D).

![especificar la unidad](media/how-to-use-perfInsights/enter-drive.png)

script de Hola desinstala las herramientas de utilidades de Hola y quita las carpetas temporales.

### <a name="troubleshooting-other-script-issues"></a>Solución de problemas con otros scripts 

Si se produce algún problema al ejecutar el script de Hola, presione la ejecución del script de Ctrl + C toointerrupt Hola. tooremove objetos temporales, vea la sección de "Limpiar después de la terminación anómala" de Hola.

Si continúa el error de secuencia de comandos de tooexperience incluso después de varios intentos, recomendamos que ejecute el script de Hola en "modo de depuración" mediante el uso de Hola "-Depurar" opción de parámetro en el inicio.

Después de error de Hola se produce, copia Hola completa salida de consola de PowerShell de hello y enviar agente de Microsoft Support toohello que está ayudando a toohelp solucionar el problema de Hola.

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a>¿Cómo se ejecuta la secuencia de comandos de hello en el modo de configuración personalizada?

Si selecciona hello **personalizado** configuración, puede habilitar varios seguimientos en paralelo (use MAYÚS toomulti-select):

![seleccionar escenarios](media/how-to-use-perfInsights/select-scenario.png)

Al seleccionar Hola de diagnóstico de rendimiento, seguimiento de contador de rendimiento, XPerf seguimiento, seguimiento de la red o escenarios de seguimiento de Storport, siga las instrucciones de hello en los cuadros de diálogo de Hola e intente tooreproduce Hola un rendimiento lento problema después de iniciar seguimientos de Hola.

Hola después el cuadro de diálogo le permite iniciar un seguimiento:

![iniciar seguimiento](media/how-to-use-perfInsights/start-trace-message.png)

seguimientos de hello toostop, tiene comandos de hello tooconfirm en un segundo cuadro de diálogo.

![detener seguimiento](media/how-to-use-perfInsights/stop-trace-message.png)
![detener seguimiento](media/how-to-use-perfInsights/ok-trace-message.png)

Cuando Hola seguimientos o las operaciones se completan, se genera un nuevo archivo en D:\\registro\_colección (o unidad temporal de Hola) que se denomina **CollectedData\_aaaa-MM-dd\_hh\_mm \_ss.zip.** Puede enviar a este agente de soporte técnico de toohello de archivo para el análisis.

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a>Revise el informe de diagnóstico de hello creado por PerfInsights

Dentro de hello **CollectedData\_aaaa-MM-dd\_hh\_mm\_archivo ss.zip,** generada por PerfInsights, encontrará un informe HTML que detalla las conclusiones de Hola de PerfInsights. tooreview Hola informe, expanda hello **CollectedData\_aaaa-MM-dd\_hh\_mm\_ss.zip** de archivos y, a continuación, abra hello **PerfInsights Report.html**archivo.

Seleccione hello **hallazgos** ficha.

![pestaña Conclusiones](media/how-to-use-perfInsights/findingtab.png)

**Notas**

-   Los mensajes en rojo son problemas de configuración conocidos que pueden causar problemas de rendimiento.

-   Los mensajes en amarillo son advertencias que representan configuraciones inadecuadas que no necesariamente provocan problemas de rendimiento.

-   Los mensajes en azul son solo instrucciones informativas.

Hola revisión vínculos HTTP para todos los mensajes de error en rojo tooget más información detallada sobre hallazgos de Hola y cómo pueden afectar al rendimiento de Hola o prácticas recomendadas para configuraciones con optimización para el rendimiento.

### <a name="disk-configuration-tab"></a>Pestaña Configuración del disco

Hola **Introducción** sección muestra distintas vistas de configuración de almacenamiento de hello, incluida la información de Diskpart y espacios de almacenamiento

Hola **DiskMap** y **VolumeMap** secciones se describen en una perspectiva dual de forma lógica los volúmenes y discos físicos están relacionado tooeach otro.

Hola PhysicalDisk perspectiva (DiskMap), tabla de hello muestra todos los volúmenes lógicos que se ejecutan en el disco de Hola. En el siguiente ejemplo de Hola, PhysicalDrive2 ejecuta 2 volúmenes lógicos creados en varias particiones (J y H):

![pestaña Datos](media/how-to-use-perfInsights/disktab.png)

Hola perspectiva de volumen (*VolumeMap*), las tablas de Hola muestran todos los discos físicos de hello en cada volumen lógico. Observe que para los discos RAID y dinámicos, puede ejecutar un volumen lógico en varios discos físicos. En el siguiente ejemplo de Hola *C:\\montar* está configurado como un punto de montaje *SpannedDisk* en discos físicos \#2 y \#3:

![pestaña Volumen](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a>Pestaña SQL Server

Si el destino de hello VM hospeda cualquier instancia de SQL Server, verá una pestaña adicional en el informe de Hola que se denomina **SQL Server**:

![ficha sql](media/how-to-use-perfInsights/sqltab.png)

Esta sección contiene una "Introducción" y pestañas de sub adicionales para cada instancia de SQL Server de hello hospedada en hello máquina virtual.

Hola sección "Introducción" contiene una tabla útil que resume todos los Hola discos físicos (discos de datos y del sistema) que se están ejecutando y que contienen una combinación de archivos de datos y archivos de registro de transacciones.

En el siguiente ejemplo, el Hola *PhysicalDrive0* (ejecutando la unidad C de Hola) se muestra porque ambos Hola *modeldev* y *modellog* archivos se encuentran en la unidad de hello C, y únicamente son de tipos diferentes (por ejemplo, el archivo de datos y registro de transacciones, respectivamente):

![loginfo](media/how-to-use-perfInsights/loginfo.png)

pestañas de específicos de la instancia de SQL Server de Hello contienen una sección general que muestra información básica acerca de la instancia seleccionada de Hola y secciones adicionales para obtener información avanzada, incluida la configuración, las configuraciones y opciones de usuario.

## <a name="references-toohello-external-tools-used"></a>Hace referencia a herramientas externas toohello usa

### <a name="diskspd"></a>Diskspd

DISKSPD es un almacenamiento carga generador y el rendimiento prueba herramienta desde equipos de ingeniería de hello Windows y Windows Server e infraestructura de servidor de nube. Para más información, vea [Diskspd](https://github.com/Microsoft/diskspd).

### <a name="xperf"></a>XPerf

Xperf es un seguimientos de toocapture herramienta de línea de comandos del Kit de herramientas de rendimiento de Windows hello.

Para más información, vea [Windows Performance Toolkit -Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/).

## <a name="next-steps"></a>Pasos siguientes

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a>Cargar diagnósticos los registros e informes tooMicrosoft soporte técnico de revisión

Cuando se trabaja con el personal de Microsoft Support hello, es posible que la salida de hello tootransmit solicitado generadas por el proceso de solución de problemas de PerfInsights tooassist Hola.

agente de asistencia de Hello creará un área de trabajo DTM por usted, y recibirá un mensaje de correo electrónico que incluye un vínculo de toohello [portal DTM (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) y un identificador de usuario único y una contraseña.

Este mensaje se enviará desde **CTS Automated Diagnostics Services** (ctsadiag@microsoft.com).

![Ejemplo de mensaje de bienvenida](media/how-to-use-perfInsights/supportemail.png)

Para obtener seguridad adicional, podrá toochange requiere la contraseña en primer lugar utilice.

Después de iniciar sesión en tooDTM, encontrará un Hola de tooupload del cuadro de diálogo **CollectedData\_aaaa-MM-dd\_hh\_mm\_ss.zip** archivo que se recopiló el inventario por PerfInsights.
