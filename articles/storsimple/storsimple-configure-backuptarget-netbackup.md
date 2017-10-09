---
title: aaaStorSimple 8000 series como destino de copia de seguridad con NetBackup | Documentos de Microsoft
description: "Describe la configuración de destino de copia de seguridad de StorSimple Hola con Veritas NetBackup."
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: hkanna
ms.openlocfilehash: 7d032bbcf6e40e7609e51437e290fc92b232a48f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a>StorSimple como destino de copia de seguridad con NetBackup

## <a name="overview"></a>Información general

Azure StorSimple es una solución de almacenamiento en nube híbrida de Microsoft. StorSimple direcciones complejidades Hola de crecimiento exponencial de los datos con una cuenta de almacenamiento de Azure como una extensión de la solución local de Hola y apilar automáticamente datos a través de un almacenamiento local y el almacenamiento en nube.

En este artículo se describen la integración de StorSimple con NetBackup y los procedimientos recomendados para la integración de ambas soluciones. También se hacer recomendaciones sobre cómo integrar tooset seguridad Veritas NetBackup toobest con StorSimple. Se aplazan tooVeritas mejores prácticas, arquitectos de copia de seguridad y los administradores de hello tooset de manera mejor los requisitos de copia de seguridad individuales de Veritas NetBackup toomeet y contratos de nivel de servicio (SLA).

Aunque se muestran tanto los pasos de configuración como los conceptos clave, este artículo no es una guía detallada de configuración o instalación. Suponemos que infraestructura y los componentes básicos de hello están en condiciones de funcionamiento y toosupport listo conceptos de Hola que describimos.

### <a name="who-should-read-this"></a>¿A quiénes está dirigido este documento?

información de Hello en este artículo será más útiles toobackup, los administradores de almacenamiento, arquitectos y administradores almacenamiento que tienen conocimientos de almacenamiento, Windows Server 2012 R2, Ethernet, servicios en la nube y Veritas NetBackup.

### <a name="supported-versions"></a>Versiones compatibles

-   NetBackup 7.7.x y versiones posteriores
-   [StorSimple Update 3 y versiones posteriores](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a>¿Por qué StorSimple como destino de copia de seguridad?

StorSimple es una buena elección para un destino de copia de seguridad porque:

-   Proporciona almacenamiento estándar, local para las aplicaciones de copia de seguridad toouse como destino de copia de seguridad rápida, sin realizar ningún cambio. También puede usar StorSimple para la restauración rápida de copias de seguridad recientes.
-   Su nube niveles se integra perfectamente con una toouse de cuenta de almacenamiento de Azure en la nube rentable de almacenamiento de Azure.
-   Proporciona automáticamente almacenamiento externo para la recuperación ante desastres.

## <a name="key-concepts"></a>Conceptos clave

Al igual que con cualquier solución de almacenamiento, una evaluación minuciosa de rendimiento de almacenamiento de la solución de hello, SLA, tasa de cambio y las necesidades de crecimiento de capacidad es toosuccess críticos. idea principal Hello es que introduciendo un nivel en la nube, los tiempos de acceso y capacidad de proceso en la nube toohello desempeña un papel fundamental en cuanto a capacidad de Hola de StorSimple toodo su trabajo.

StorSimple está diseñado tooprovide tooapplications de almacenamiento que operan en un espacio de trabajo bien definido de datos (datos activos). En este modelo, espacio de trabajo de Hola de datos se almacena en capas locales de Hola y Hola restante no laborables/frío/archivado de conjunto de datos es toohello en capas en la nube. Este modelo se representa en hello figura siguiente. línea Hello casi plano verde representa datos de hello almacenados en capas locales de hello de dispositivo de StorSimple de Hola. Hello línea roja representa Hola cantidad total de datos almacenados en solución StorSimple de Hola a todos los niveles. espacio Hola entre línea hello plano verde y curva exponencial rojo de hello representa la cantidad total de Hola de los datos almacenados en la nube de Hola.

**Niveles de StorSimple**
![Diagrama de niveles de Storsimple](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)

Con esta arquitectura en mente, encontrará que StorSimple es ideal toooperate como un destino de copia de seguridad. Puede usar StorSimple para:
-   Realice las restauraciones más frecuentes de espacio de trabajo local Hola de datos.
-   Usar en la nube hello para la recuperación de desastres de fuera del sitio y los datos más antiguos, donde restauraciones son menos frecuentes.

## <a name="storsimple-benefits"></a>Ventajas de StorSimple

StorSimple ofrece una solución local que se integra perfectamente con Microsoft Azure, aprovechando las ventajas de sin problemas a tooon desde la oficina y almacenamiento en nube.

StorSimple usa niveles automática entre dispositivos locales de hello, que tiene el dispositivo de estado sólido (SSD) y conectada en serie de almacenamiento SCSI (SAS) y el almacenamiento de Azure. Automática mantiene apilar frecuencia de acceso a datos locales, en los niveles SSD y SAS de Hola. Mueve los datos que se accede con poca frecuencia tooAzure almacenamiento.

StorSimple ofrece las siguientes ventajas:

-   Algoritmos de desduplicación y la compresión únicos que usan niveles de desduplicación sin precedentes de tooachieve de hello en la nube
-   Alta disponibilidad
-   Replicación geográfica mediante el uso de la replicación geográfica de Azure
-   Integración de Azure
-   Cifrado de datos en la nube de Hola
-   Mejor recuperación ante desastres y cumplimiento normativo

Aunque StorSimple presenta dos escenarios de implementación principales (destino de copia de seguridad principal y secundario), es fundamentalmente un dispositivo de almacenamiento de bloques sin formato. StorSimple Hola compresión y desduplicación. Sin problemas, envía y recupera los datos entre la nube de Hola y aplicación hello y el sistema de archivos.

Para obtener más información sobre StorSimple, consulte [Serie StorSimple 8000: una solución de almacenamiento en la nube híbrida](storsimple-overview.md). Además, puede revisar hello [especificaciones técnicas de la serie StorSimple 8000](storsimple-technical-specifications-and-compliance.md).

> [!IMPORTANT]
> El uso del dispositivo StorSimple como destino de copia de seguridad es compatible solo con StorSimple 8000 Update 3 y versiones posteriores.

## <a name="architecture-overview"></a>Introducción a la arquitectura

Hello en las tablas siguientes muestran instrucciones inicial de arquitectura del modelo de dispositivo de Hola.

**Capacidades de StorSimple para el almacenamiento local y en la nube**

| Capacidad de almacenamiento       | 8100          | 8600            |
|------------------------|---------------|-----------------|
| Capacidad de almacenamiento local | &lt; 10 TiB\*  | &lt; 20 TiB\*  |
| Capacidad de almacenamiento en la nube | &gt; 200 TiB\* | &gt; 500 TiB\* |
\* En el tamaño de almacenamiento, se asume que no hay desduplicación ni compresión.

**Capacidades de StorSimple para copias de seguridad principales y secundarias**

| Escenario de copia de seguridad  | Capacidad de almacenamiento local  | Capacidad de almacenamiento en la nube  |
|---|---|---|
| Copia de seguridad principal  | Copias de seguridad recientes almacenados en almacenamiento local para el objetivo de punto de recuperación (RPO) de recuperación rápida toomeet | El historial de copias de seguridad (RPO) se ajusta a la capacidad de la nube |
| Copia de seguridad secundaria | La copia secundaria de los datos de las copias de seguridad se puede almacenar en la capacidad de la nube  | N/D  |

## <a name="storsimple-as-a-primary-backup-target"></a>StorSimple como destino de copia de seguridad principal

En este escenario, los volúmenes de StorSimple se presentan toohello aplicación de copia de seguridad como único repositorio de Hola para copias de seguridad. Hola figura siguiente muestra una arquitectura de la solución en la que todas las copias de seguridad use StorSimple en niveles de volúmenes para las copias de seguridad y restauraciones.

![Diagrama lógico de StorSimple como destino de copia de seguridad principal](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Pasos lógicos de copias de seguridad en el destino principal

1.  contactos del servidor de copia de seguridad de Hola Hola a agente de copia de seguridad de destino y agente de copia de seguridad de hello transmite el servidor de copia de seguridad de datos toohello.
2.  servidor de copia de seguridad de Hello escribe datos toohello StorSimple en niveles de volúmenes.
3.  servidor de copia de seguridad de Hello actualiza la base de datos de catálogo de hello y, a continuación, finalice el trabajo de copia de seguridad de Hola.
4.  Una secuencia de comandos de instantánea desencadena el Administrador de instantáneas de StorSimple Hola (inicio o eliminación).
5.  servidor de copia de seguridad de Hello elimina expiradas copias de seguridad según una directiva de retención.

### <a name="primary-target-restore-logical-steps"></a>Pasos lógicos de restauración del destino principal

1.  servidor de copia de seguridad de Hello inicia restaurar los datos adecuados de Hola de repositorio de almacenamiento de Hola.
2.  agente de copia de seguridad de Hola recibe los datos de saludo del servidor de copia de seguridad de Hola.
3.  servidor de copia de seguridad de Hello finaliza el trabajo de restauración de Hola.

## <a name="storsimple-as-a-secondary-backup-target"></a>StorSimple como destino de copia de seguridad secundario

En este escenario, los volúmenes de StorSimple se utilizan principalmente para la retención o el archivado a largo plazo.

Hello en la ilustración siguiente se muestra una arquitectura de las copias de seguridad iniciales y restaura el volumen de destino un alto rendimiento. Estas copias de seguridad se copian y archivado tooa StorSimple en niveles de volumen en una programación establecida.

Es importante toosize su volumen de alto rendimiento, por lo que TI puede controlar los requisitos de capacidad y rendimiento de la directiva de retención.

![Diagrama lógico de StorSimple como destino de copia de seguridad secundario](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Pasos lógicos de copias de seguridad en el destino secundario

1.  contactos del servidor de copia de seguridad de Hola Hola a agente de copia de seguridad de destino y agente de copia de seguridad de hello transmite el servidor de copia de seguridad de datos toohello.
2.  servidor de copia de seguridad de Hello escribe almacenamiento de datos toohigh rendimiento.
3.  servidor de copia de seguridad de Hello actualiza la base de datos de catálogo de hello y, a continuación, finalice el trabajo de copia de seguridad de Hola.
4.  servidor de copia de seguridad de Hello copia tooStorSimple de copias de seguridad según una directiva de retención.
5.  Una secuencia de comandos de instantánea desencadena el Administrador de instantáneas de StorSimple Hola (inicio o eliminación).
6.  eliminaciones de copia de seguridad de servidor Hola Hola expirado según una directiva de retención de copias de seguridad.

### <a name="secondary-target-restore-logical-steps"></a>Pasos lógicos de restauración del destino secundario

1.  servidor de copia de seguridad de Hello inicia restaurar los datos adecuados de Hola de repositorio de almacenamiento de Hola.
2.  agente de copia de seguridad de Hola recibe los datos de saludo del servidor de copia de seguridad de Hola.
3.  servidor de copia de seguridad de Hello finaliza el trabajo de restauración de Hola.

## <a name="deploy-hello-solution"></a>Implementar soluciones de Hola

La implementación de esta solución requiere tres pasos:
1. Preparar la infraestructura de red de Hola.
2. Implementación del dispositivo StorSimple como destino de copia de seguridad
3. Implementación de Veritas NetBackup

Cada paso se explica con detalle en las secciones siguientes de Hola.

### <a name="set-up-hello-network"></a>Configurar una red de Hola

Debido a que StorSimple es una solución que se integra con hello nube de Azure, StorSimple requiere una nube de Azure toohello de conexión activo y en funcionamiento. Esta conexión se usa para operaciones como instantáneas en la nube, la administración de datos y metadatos transferencia y almacenamiento en nube tooAzure datos más antiguos y menos acceso tootier.

Para hello solución tooperform un rendimiento óptimo, se recomienda que siga estas prácticas recomendadas de red:

-   vínculo de Hola que conecta hello StorSimple apilar tooAzure debe cumplir los requisitos de ancho de banda. tooachieve, aplicar Hola apropiado de calidad de servicio (QoS) nivel tooyour infraestructura conmutadores toomatch el RPO y tiempos de recuperación SLA de recuperación (RTO).

-   Las latencias de acceso máximas de Azure Blob Storage deben rondar los 80 ms.

### <a name="deploy-storsimple"></a>Implementación de StorSimple

Para ver instrucciones detalladas para la implementación de StorSimple, consulte [Implementar el dispositivo StorSimple local](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-netbackup"></a>Implementación de NetBackup

Para obtener instrucciones de implementación de 7.7.x NetBackup, consulte hello [NetBackup 7.7.x documentación](http://www.veritas.com/docs/000094423).

## <a name="set-up-hello-solution"></a>Configurar la solución de Hola

En esta sección se muestran algunos ejemplos de configuración. Hello ejemplos y las recomendaciones siguientes ilustran hello más básica y fundamentales implementación. Esta implementación podría no aplicarse directamente tooyour requisitos de copia de seguridad específicos.

### <a name="set-up-storsimple"></a>Configuración de StorSimple

| Tareas de implementación de StorSimple  | Comentarios adicionales |
|---|---|
| Implementar un dispositivo de StorSimple local. | Versiones compatibles: Update 3 y versiones posteriores. |
| Encienda el destino de copia de seguridad de Hola. | Utilice estos comandos tooturn en o desactivar el modo de destino de copia de seguridad y el estado de tooget. Para obtener más información, consulte [conectarse de forma remota el dispositivo de StorSimple tooa](storsimple-remote-connect.md).</br> tooturn en modo de copia de seguridad: `Set-HCSBackupApplianceMode -enable`. </br> tooturn desactiva el modo de copia de seguridad: `Set-HCSBackupApplianceMode -disable`. </br> estado actual de hello tooget de configuración del modo de copia de seguridad: `Get-HCSBackupApplianceMode`. |
| Crear un contenedor de volumen común para el volumen que almacena datos de copia de seguridad de saludo. Todos los datos de un contenedor de volumen se desduplican. | Los contenedores de volúmenes de StorSimple definen dominios de desduplicación.  |
| Cree volúmenes de StorSimple. | Crear volúmenes con tamaños como uso de cierre toohello previsto como sea posible, porque el tamaño del volumen afecta a la hora de duración de la instantánea de nube. Para obtener información acerca de cómo toosize un volumen que conozca [las directivas de retención](#retention-policies).</br> </br> StorSimple de uso en niveles volúmenes y seleccione hello **usar este volumen de datos acceso menos frecuente archivados** casilla de verificación. </br> No se admite que solo se usen volúmenes anclados localmente. |
| Crear una directiva de copia de seguridad de StorSimple única para todos los volúmenes de destino de copia de seguridad de Hola. | Una directiva de copia de seguridad de StorSimple define el grupo de consistencia de volumen de Hola. |
| Deshabilitar la programación de hello como las instantáneas de hello expiran. | Las instantáneas se desencadenan como operación posterior al procesamiento. |

### <a name="set-up-hello-host-backup-server-storage"></a>Configurar el almacenamiento de copia de seguridad del servidor de host de Hola

Configurar el almacenamiento de copia de seguridad del servidor de host de hello según las directrices de toothese:  

- No use volúmenes distribuidos (creados por el administrador de discos de Windows), ya que no se admiten.
- Dé formato a los volúmenes mediante NTFS con un tamaño de asignación de 64 kB.
- Asignar los volúmenes de StorSimple Hola directamente toohello NetBackup server.
    - Use iSCSI para servidores físicos.
    - Use discos de acceso directo para servidores virtuales.


## <a name="best-practices-for-storsimple-and-netbackup"></a>Procedimientos recomendados para StorSimple y NetBackup

Configure su solución según las directrices de toohello Hola algunas de las secciones siguientes.

### <a name="operating-system-best-practices"></a>Procedimientos recomendados para un sistema operativo

-   Deshabilitar el cifrado de Windows Server y desduplicación Hola sistema de archivos NTFS.
-   Deshabilite la desfragmentación de Windows Server en volúmenes de StorSimple Hola.
-   Deshabilitar la indización en hello volúmenes de StorSimple de Windows Server.
-   Ejecute un análisis antivirus en el host de origen de hello (no en relación a los volúmenes de StorSimple Hola).
-   Desactive la opción predeterminada de hello [mantenimiento de Windows Server](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) en el Administrador de tareas. Hacer esto en uno de hello siguientes maneras:
    - Desactivar la configuración de mantenimiento de hello en el programador de tareas de Windows.
    - Descargue [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) de Windows Sysinternals. Después de descargar PsExec, ejecute Windows PowerShell como administrador y escriba:
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>Procedimientos recomendados para StorSimple

-   Asegúrese de que ese dispositivo de StorSimple Hola se actualiza también[Update 3 o posterior](storsimple-install-update-3.md).
-   Aísle tráfico de iSCSI y de la nube. Usar conexiones iSCSI dedicado para el tráfico entre el servidor de copia de seguridad de StorSimple y Hola.
-   Asegúrese de que su dispositivo de StorSimple sea un destino de copia de seguridad dedicado. No se admiten cargas de trabajo mixtas porque afectan a su RTO y RPO.

### <a name="netbackup-best-practices"></a>Procedimientos recomendados para NetBackup

-   base de datos de Hello NetBackup debe ser servidor toohello local y no reside en un volumen de StorSimple.
-   Recuperación ante desastres, realizar una copia de base de datos de hello NetBackup en un volumen de StorSimple.
-   Se admiten NetBackup completas e incrementales copias de seguridad (también denominado tooas diferencial copias de seguridad incrementales en NetBackup) para esta solución. Se recomienda no usar copias de seguridad incrementales sintéticas y acumulativas.
-   Archivos de copia de seguridad de datos deben contener sólo los datos de saludo de un trabajo específico. Por ejemplo, no se permiten anexos de medios entre distintos trabajos.

Hola última configuración de NetBackup y procedimientos recomendados para implementar estos requisitos, encontrará documentación de NetBackup hello en [www.veritas.com](https://www.veritas.com).


## <a name="retention-policies"></a>Directivas de retención

Uno de los tipos de directiva de retención de copia de seguridad más comunes de hello es una directiva de su abuelo y padre, hijo (GFS). En una directiva GFS, se realiza una copia de seguridad incremental diaria y se realizan copias de seguridad completas semanales y mensuales. Este resultados de directivas de StorSimple seis niveles volúmenes: un volumen contiene Hola semanales, mensuales y anuales copias de seguridad completas; Hello otros cinco volúmenes almacenan copias de seguridad incrementales diarias.

En el siguiente ejemplo de Hola, usamos un giro GFS. ejemplo de Hola supone siguiente Hola:

-   Se usan datos no desduplicados o comprimidos.
-   Cada copia de seguridad completa ocupa 1 TiB.
-   Las copias de seguridad incrementales diarias ocupan 500 GiB.
-   Se conservan cuatro copias de seguridad semanales durante un mes.
-   Se conservan doce copias de seguridad mensuales durante un año.
-   Se conserva una copia de seguridad anual durante diez años.

En función de hello anterior suposiciones, crear un TiB 26 StorSimple en niveles de volumen para hello mensual y anual copias de seguridad completas. Crear un TiB 5 StorSimple en niveles de volumen para cada una de las copias de seguridad diarias Hola incremental.

| Retención de tipo de copia de seguridad | Tamaño (TiB) | Multiplicador de GFS\* | Capacidad total (TiB)  |
|---|---|---|---|
| Completa semanal | 1 | 4  | 4 |
| Incremental diaria | 0,5 | 20 (los ciclos equivalen al número de semanas al mes) | 12 (2 para cuota adicional) |
| Completa mensual | 1 | 12 | 12 |
| Completa anual | 1  | 10 | 10 |
| Requisito de GFS |   | 38 |   |
| Cuota adicional  | 4  |   | Requisito de GFS, un total de 42  |
\*multiplicador GFS Hello es el número de Hola de copias que necesita tooprotect y conservar toomeet los requisitos de la directiva de copia de seguridad.

## <a name="set-up-netbackup-storage"></a>Configuración del almacenamiento de NetBackup

### <a name="tooset-up-netbackup-storage"></a>tooset el almacenamiento de NetBackup

1.  En la consola de administración de NetBackup hello, seleccione **administración de dispositivos y medios** > **dispositivos** > **grupos de discos**. Hola Asistente para configuración de grupo de discos, seleccione el tipo de servidor de almacenamiento de hello **AdvancedDisk**y, a continuación, seleccione **siguiente**.

    ![Consola de administración de NetBackup, Asistente para configuración de grupo de discos](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  Busque su servidor y seleccione **Next** (Siguiente).

    ![Consola de administración de NetBackup, servidor seleccione Hola](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  Seleccione su volumen de StorSimple.

    ![Consola de administración de NetBackup, disco de volumen de StorSimple seleccione Hola](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  Escriba un nombre para el destino de copia de seguridad de hello y, a continuación, seleccione **siguiente** > **siguiente** Asistente de hello toofinish.

5.  Revisar la configuración de hello y, a continuación, seleccione **finalizar**.

6.  Al final de Hola de cada asignación de volumen, cambiar Hola almacenamiento dispositivo configuración toomatch los recomendados en [prácticas recomendadas para StorSimple y NetBackup](#best-practices-for-storsimple-and-netbackup).

7. Repita los pasos del 1 al 6 hasta que haya terminado de asignar los volúmenes de StorSimple.

    ![Consola de administración de NetBackup, configuración de discos](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configuración de StorSimple como destino de copia de seguridad principal

> [!NOTE]
> Restauraciones de datos desde una copia de seguridad que se ha toohello en capas en la nube se producen a velocidades de nube.

Hello en la ilustración siguiente se muestra hello asignación de un trabajo de copia de seguridad de tooa volumen normal. En este caso, todas las copias de seguridad semanales de hello asignan disco lleno de toohello sábado, y copias de seguridad incrementales de hello asignan discos incremental tooMonday viernes. Hola a todos las copias de seguridad y restauraciones son de un StorSimple en niveles de volumen.

![Diagrama lógico de la configuración de destino de copia de seguridad principal ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Ejemplo de programación GFS de StorSimple como destino de copia de seguridad principal

A continuación se muestra un ejemplo de programación de rotación GFS para cuatro semanas, mensual, y anual:

| Frecuencia o tipo de copia de seguridad | Completo | Incremental (días 1-5)  |   
|---|---|---|
| Semanal (semanas 1-4) | Sábado | Lunes-viernes |
| Mensual  | Sábado  |   |
| Anual | Sábado  |   |   |

## <a name="assigning-storsimple-volumes-tooa-netbackup-backup-job"></a>La asignación de trabajo de copia de seguridad de StorSimple volúmenes tooa NetBackup

Hola sigue secuencia se da por supuesto que hospedan destino hello y NetBackup se configura según las directrices de hello NetBackup agente.

### <a name="tooassign-storsimple-volumes-tooa-netbackup-backup-job"></a>trabajo de copia de seguridad de tooassign StorSimple volúmenes tooa NetBackup

1.  En la consola de administración de NetBackup hello, seleccione **NetBackup administración**, haga clic en **directivas**y, a continuación, seleccione **nueva directiva**.

    ![Consola de administración de NetBackup, creación de una nueva directiva](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  Hola **agregar una nueva directiva** cuadro de diálogo, escriba un nombre para la directiva de hello y, a continuación, seleccione hello **Asistente para configuración de directiva de uso** casilla de verificación. Seleccione **Aceptar**.

    ![Consola de administración de NetBackup, cuadro de diálogo para agregar una nueva directiva](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  En el Asistente para configuración de directiva de copia de seguridad de hello, eleccione Hola tipo de copia de seguridad que desee y, a continuación, seleccione **siguiente**.

    ![Consola de administración de NetBackup, selección del tipo de copia de seguridad](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  tipo de directiva de hello tooset, seleccione **estándar**y, a continuación, seleccione **siguiente**.

    ![Consola de administración de NetBackup, selección del tipo de directiva](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  Seleccione el host, seleccione hello **detectar el sistema operativo cliente** casilla de verificación y, a continuación, seleccione **agregar**. Seleccione **Siguiente**.

    ![Consola de administración de NetBackup, enumeración de clientes en una nueva directiva](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  Seleccionar unidades de hello que desea tooback.

    ![Consola de administración de NetBackup, selecciones de copia de seguridad para una nueva directiva](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  Seleccione la frecuencia de Hola y valores de retención que satisfacen las necesidades de rotación de copia de seguridad.

    ![Consola de administración de NetBackup, frecuencia y rotación de copias de seguridad para una nueva directiva](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  Select **Next** > **Next** > **Finish** (Siguiente > Siguiente > Finalizar).  Puede modificar programación de hello después de crear directiva Hola.

9.  Seleccionar directiva de hello tooexpand recién creado y, a continuación, seleccione **programaciones**.

    ![Consola de administración de NetBackup, programaciones para una nueva directiva](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  Haga clic en **Inc diferencial**, seleccione **copiar toonew**y, a continuación, seleccione **Aceptar**.

    ![Consola de administración de NetBackup, tooa nueva directiva de programación de copia](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  Haga clic en programación de hello recién creado y, a continuación, seleccione **cambio**.

12.  En hello **atributos** ficha, seleccione hello **anular la selección de almacenamiento de directiva** casilla de verificación y volumen de hello, a continuación, seleccione el lunes copias de seguridad incrementales dónde.

    ![Consola de administración de NetBackup, cambio de programación](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  En hello **iniciar ventana** pestaña, ventana de tiempo de hello select para las copias de seguridad.

    ![Consola de administración de NetBackup, cambio de ventana de inicio](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  Seleccione **Aceptar**.

15.  Repita los pasos del 10 al 14 para cada copia de seguridad incremental. Seleccione el volumen apropiado de Hola y programación para cada copia de seguridad que se crea.

16.  Menú contextual Hola **Inc diferencial** programar y, a continuación, elimínelo.

17.  Modifique su toomeet de programación completa que la copia de seguridad necesario.

    ![Consola de administración de NetBackup, cambio de programación completa](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  Cambio de ventana de inicio de Hola.

    ![Consola de administración de NetBackup, cambio de ventana de inicio de Hola](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  programación de Hello final tiene este aspecto:

    ![Consola de administración de NetBackup, programación final](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configuración de StorSimple como destino de copia de seguridad secundario

> [!NOTE]
>Restauraciones de datos desde una copia de seguridad que se ha toohello en capas en la nube se producen a velocidades de nube.

En este modelo, debe tener un tooserve de medios (distintos de StorSimple) de almacenamiento como una memoria caché temporal. Por ejemplo, puede usar una matriz redundante de espacio de tooaccommodate de volumen de discos independientes (RAID), la entrada/salida (E/S) y el ancho de banda. Se recomienda usar RAID 5, 50 y 10.

Hello en la ilustración siguiente se muestra típico a corto plazo de retención local (toohello server) volúmenes de archivos de volúmenes y retención a largo plazo. En este escenario, todas las copias de seguridad se ejecutan en hello local (toohello server) volumen RAID. Estas copias de seguridad periódicamente se duplican y archivado tooan archiva el volumen. Es importante toosize local (toohello server) volumen RAID, por lo que puede controlar los requisitos de capacidad y rendimiento de retención a corto plazo.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>Ejemplo de GFS de StorSimple como destino de copia de seguridad secundario

![Diagrama lógico de StorSimple como destino de copia de seguridad secundario](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

tabla Hola siguiente muestra cómo tooset una toorun de las copias de seguridad en discos de StorSimple y locales de Hola. Incluye requisitos de capacidad individual y total.

### <a name="backup-configuration-and-capacity-requirements"></a>Configuración de copia de seguridad y requisitos de capacidad

| Tipo de copia de seguridad y retención | Almacenamiento configurado | Tamaño (TiB) | Multiplicador de GFS | Capacidad total \* (TiB) |
|---|---|---|---|---|
| Semana 1 (completa e incremental) |Disco local (a corto plazo)| 1 | 1 | 1 |
| StorSimple semanas 2-4 |Disco de StorSimple (largo plazo) | 1 | 4 | 4 |
| Completa mensual |Disco de StorSimple (largo plazo) | 1 | 12 | 12 |
| Completa anual |Disco de StorSimple (largo plazo) | 1 | 1 | 1 |
|Requisito de tamaño de volúmenes de GFS |  |  |  | 18*|
\* La capacidad total incluye 17 TiB de discos de StorSimple y 1 TiB de volumen RAID local.


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a>Ejemplo de programación GFS: programación semanal, mensual y anual de rotación de GFS

| Semana | Completo | Incremental día 1 | Incremental día 2 | Incremental día 3 | Incremental día 4 | Incremental día 5 |
|---|---|---|---|---|---|---|
| Semana 1 | Volumen RAID local  | Volumen RAID local | Volumen RAID local | Volumen RAID local | Volumen RAID local | Volumen RAID local |
| Semana 2 | StorSimple semanas 2-4 |   |   |   |   |   |
| Semana 3 | StorSimple semanas 2-4 |   |   |   |   |   |
| Semana 4 | StorSimple semanas 2-4 |   |   |   |   |   |
| Mensual | StorSimple mensual |   |   |   |   |   |
| Anual | StorSimple anual  |   |   |   |   |   |   |


## <a name="assign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>Asignar StorSimple volúmenes tooa NetBackup archive y duplicación de trabajo

Como NetBackup ofrece una amplia gama de opciones para la administración de almacenamiento y los medios, se recomienda que consulte con Veritas o su tooproperly de arquitecto de NetBackup evaluar los requisitos de directiva (SLP) de almacenamiento del ciclo de vida.

Después de definir los grupos de discos inicial de hello, se necesitan tres directivas de almacenamiento adicional del ciclo de vida toodefine, para un total de cuatro directivas:
* LocalRAIDVolume
* StorSimpleWeek2-4
* StorSimpleMonthlyFulls
* StorSimpleYearlyFulls

### <a name="tooassign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>tooassign StorSimple volúmenes tooa NetBackup trabajo archive and duplicación

1.  En la consola de administración de NetBackup hello, seleccione **almacenamiento** > **las directivas de ciclo de vida de almacenamiento** > **nueva directiva de ciclo de vida de almacenamiento**.

    ![Consola de administración de NetBackup, nueva directiva de ciclo de vida de almacenamiento](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  Escriba un nombre para la instantánea de hello y, a continuación, seleccione **agregar**.

3.  Hola **nueva operación** cuadro de diálogo de hello **propiedades** ficha, para **operación**, seleccione **copia de seguridad**. Seleccione los valores de hello que desee para **almacenamiento de destino**, **tipo retención**, y **período de retención**. Seleccione **Aceptar**.

    ![Consola de administración de NetBackup, cuadro de diálogo para agregar una nueva operación](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    Esto define el repositorio y la primera operación de copia de seguridad Hola.

4.  Seleccione la operación anterior de toohighlight hello y, a continuación, seleccione **agregar**. Hola **operación de cambio de almacenamiento** cuadro de diálogo, los valores de hello select que desee para **almacenamiento de destino**, **tipo retención**, y **período de retención** .

    ![Consola de administración de NetBackup, cuadro de diálogo para cambiar una operación de almacenamiento](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  Seleccione la operación anterior de toohighlight hello y, a continuación, seleccione **agregar**. Hola **nueva directiva de ciclo de vida de almacenamiento** diálogo cuadro, agregar copias de seguridad mensuales durante un año.

    ![Consola de administración de NetBackup, cuadro de diálogo de nueva directiva de ciclo de vida de almacenamiento](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  Repita los pasos 4 y 5 hasta que haya creado Hola completa SLP directiva de retención que necesita.

    ![Consola de administración de NetBackup, agregar directivas en el cuadro de diálogo de nueva directiva de ciclo de vida de almacenamiento de Hola](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  Cuando haya terminado de definir la directiva de retención SLP, en **directiva**, definir una directiva de copia de seguridad siguiendo los pasos de hello detallados en [trabajo de copia de seguridad de StorSimple asignar volúmenes tooa NetBackup](#assigning-storsimple-volumes-to-a-netbackup-backup-job).

8.  En **programaciones**, Hola **Cambiar programación** cuadro de diálogo, haga clic en **completa**y, a continuación, seleccione **cambio**.

    ![Consola de administración de NetBackup, cuadro de diálogo de cambio de programación](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  Seleccione hello **anular la selección de almacenamiento de directiva** casilla de verificación y directiva de retención SLP hello, a continuación, seleccione que creó en los pasos 1 a 6.

    ![Consola de administración de NetBackup, invalidación de selección de almacenamiento de directivas](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  Seleccione **Aceptar**y, a continuación, se repiten para programación de copia de seguridad incremental Hola.

    ![Consola de administración de NetBackup, cuadro de diálogo de cambio de programación para copias de seguridad incrementales](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| Retención de tipo de copia de seguridad | Tamaño (TiB) | Multiplicador de GFS\* | Capacidad total (TiB)  |
|---|---|---|---|
| Completa semanal |  1  |  4 | 4  |
| Incremental diaria  | 0,5  | 20 (ciclos son iguales toohello número de semanas por mes) | 12 (2 para cuota adicional) |
| Completa mensual  | 1 | 12 | 12 |
| Completa anual | 1  | 10 | 10 |
| Requisito de GFS  |     |     | 38 |
| Cuota adicional  | 4  |    | Requisito de GFS, un total de 42 |
\*multiplicador GFS Hello es el número de Hola de copias que necesita tooprotect y conservar toomeet los requisitos de la directiva de copia de seguridad.

## <a name="storsimple-cloud-snapshots"></a>Instantáneas de nube de StorSimple

Las instantáneas de nube de StorSimple protegen los datos de Hola que reside en el dispositivo StorSimple. Crear una instantánea en la nube es la herramienta de fuera del sitio de tooan de cintas de copia de seguridad local de tooshipping equivalente. Si utiliza el almacenamiento de Azure con redundancia geográfica, crear una instantánea en la nube es toomultiple sitios de tooshipping equivalente cintas de copia de seguridad. Si necesita toorestore un dispositivo después de un desastre, puede poner en línea otro dispositivo de StorSimple y realice una conmutación por error. Después de la conmutación por error de hello, serían los datos de Hola de tooaccess pueda (a velocidades de nube) desde la instantánea más reciente en la nube Hola.

Hola siguiente sección describe cómo toocreate una toostart breve secuencia de comandos y delete StorSimple instantáneas en la nube durante el procesamiento posterior a la copia de seguridad.

> [!NOTE]
> Las instantáneas que se crean manualmente o mediante programación no siguen la directiva de expiración de instantáneas de StorSimple de Hola. En otras palabras, se deben eliminar manualmente o mediante programación.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Inicio y eliminación de instantáneas en la nube con un script

> [!NOTE]
> Evalúe cuidadosamente repercusiones de retención de datos y cumplimiento de normas de hello antes de eliminar una instantánea de StorSimple. Para obtener más información acerca de cómo toorun una secuencia de comandos posteriores a la copia de seguridad, vea hello [NetBackup documentación](http://www.veritas.com/docs/000094423).

### <a name="backup-lifecycle"></a>Ciclo de vida de copia de seguridad

![Diagrama del ciclo de vida de copia de seguridad](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

### <a name="requirements"></a>Requisitos

-   servidor de Hola que se ejecuta el script de Hola debe tener acceso a los recursos en la nube tooAzure.
-   cuenta de usuario de Hello debe tener los permisos necesarios de Hola.
-   Una directiva de copia de seguridad de StorSimple con hello asociado StorSimple volúmenes deben ser configurados pero no activados.
-   Necesitará Hola nombre de recursos de StorSimple, clave de registro, nombre de dispositivo e Id. de directiva de copia de seguridad.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart o eliminar una instantánea en la nube

1.  [Instale Azure PowerShell](/powershell/azure/overview).
2.  [Descargue e importe la configuración de publicación y la información de suscripción](https://msdn.microsoft.com/library/dn385850.aspx).
3.  En el portal de Azure clásico de Hola, obtener el nombre de recurso de Hola y [clave de registro para el servicio StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4.  En el servidor de Hola que ejecuta el script de Hola, ejecute PowerShell como administrador. Escriba el siguiente comando:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    Id. de directiva de copia de seguridad de Hola de nota.
5.  En el Bloc de notas, crear un nuevo script de PowerShell mediante Hola siguiente código.

    Copie y pegue este fragmento de código:
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
      Guardar toohello de secuencia de comandos de PowerShell de hello misma ubicación donde guardó el Azure configuración de publicación. Por ejemplo, guárdelo como C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.
6.  Agregar el trabajo de copia de seguridad de hello script tooyour en NetBackup. toodo este, edite su NetBackup trabajo options' procesamiento previo y posterior al procesamiento de comandos.

> [!NOTE]
> Se recomienda que ejecute la directiva de copia de seguridad de instantáneas de StorSimple en la nube como una secuencia de comandos posteriores al procesamiento final Hola de su trabajo de copia de seguridad diaria. Para obtener más información acerca de cómo tooback seguridad y restauración su toohelp de entorno de aplicación de copia de seguridad que cumple el RPO y el RTO, póngase en contacto con el arquitecto de copia de seguridad.

## <a name="storsimple-as-a-restore-source"></a>StorSimple como origen de restauración

Las restauraciones desde un dispositivo de StorSimple funcionan como las de cualquier dispositivo de almacenamiento en bloque. Restauraciones de datos que está en la nube en niveles toohello tiene lugar a velocidades de nube. Para los datos locales, restauraciones se producen a velocidad de disco local de hello de dispositivo de Hola. Para obtener información acerca de cómo tooperform una restauración, vea hello [NetBackup documentación](http://www.veritas.com/docs/000094423). Se recomienda que se ajustan tooNetBackup restauración los procedimientos recomendados.

## <a name="storsimple-failover-and-disaster-recovery"></a>Conmutación por error y recuperación ante desastres de StorSimple

> [!NOTE]
> En los escenarios de destino de copia de seguridad, StorSimple Cloud Appliance no se admite como destino de restauración.

Un desastre puede deberse a una serie de factores. Hello en la tabla siguiente enumera escenarios comunes de recuperación ante desastres.

| Escenario | Impacto | Cómo toorecover | Notas |
|---|---|---|---|
| Error de dispositivo de StorSimple | Se interrumpen las operaciones de copia de seguridad y restauración. | Reemplace el dispositivo con error de Hola y realizar [StorSimple conmutación por error y recuperación ante desastres](storsimple-device-failover-disaster-recovery.md). | Si necesita tooperform una restauración tras la recuperación de dispositivo, los espacios de trabajo de todos los datos se recuperan de nuevo dispositivo de hello en la nube toohello. Todas las operaciones se realizan a velocidades de la nube. índice de Hola y volver a examinar el proceso de catálogo pueden provocar todos los toobe de conjuntos de copia de seguridad examina y extraerse de hello capa toohello dispositivo local capa de nube, que podría ser un proceso lento. |
| Error en el servidor de NetBackup | Se interrumpen las operaciones de copia de seguridad y restauración. | Recompile el servidor de copia de seguridad de Hola y realizar la restauración de base de datos. | Debe volver a generar o restaurar Hola NetBackup servidor en el sitio de recuperación ante desastres de Hola. Hola base de datos toohello más reciente punto de restauración. Si hello base de datos restaurada NetBackup no está sincronizada con los trabajos de copia de seguridad más recientes, se requiere la indización y catalogación. Este índice y volver a examinar el proceso de catálogo pueden provocar todos los toobe de conjuntos de copia de seguridad examina y extraerse de la capa de hello nube capa toohello dispositivo local. Esto hace que requiera mucho tiempo. |
| Error del sitio que resulta en pérdida de saludo del servidor de copia de seguridad de Hola y StorSimple | Se interrumpen las operaciones de copia de seguridad y restauración. | Restaure primero StorSimple y después NetBackup. | Restaure primero StorSimple y después NetBackup. Si necesita tooperform una restauración tras la recuperación de dispositivo, los espacios de trabajo de datos completa de Hola se recuperan de nuevo dispositivo de hello en la nube toohello. Todas las operaciones se realizan a velocidades de la nube. |

## <a name="references"></a>Referencias

Hola después documentos hizo referencia a este artículo:

- [Configurar E/S de múltiples rutas para el dispositivo StorSimple](storsimple-configure-mpio-windows-server.md)
- [Escenarios de almacenamiento: el aprovisionamiento fino](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Using GPT drives](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD) (Uso de unidades de GPT)
- [Habilitar y configurar las instantáneas de carpetas compartidas](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Pasos siguientes

- Más información acerca de cómo demasiado[restauración a partir de un conjunto de copia de seguridad](storsimple-restore-from-backup-set-u2.md).
- Más información acerca de cómo tooperform [dispositivo conmutación por error y recuperación ante desastres](storsimple-device-failover-disaster-recovery.md).
