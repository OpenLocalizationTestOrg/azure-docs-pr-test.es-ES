---
title: aaaStorSimple 8000 series como destino de copia de seguridad con Veeam | Documentos de Microsoft
description: "Describe la configuración de destino de copia de seguridad de StorSimple Hola con Veeam."
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
ms.date: 12/06/2016
ms.author: hkanna
ms.openlocfilehash: 74a4af307fab430942f94b3e28f514a9abce227b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-veeam"></a>StorSimple como destino de copia de seguridad con Veeam

## <a name="overview"></a>Información general

Azure StorSimple es una solución de almacenamiento en nube híbrida de Microsoft. StorSimple direcciones complejidades Hola de crecimiento exponencial de los datos con una cuenta de almacenamiento de Azure como una extensión de la solución local de Hola y apilar automáticamente datos a través de un almacenamiento local y el almacenamiento en nube.

En este artículo se describen la integración de StorSimple con Veeam y los procedimientos recomendados para la integración de ambas soluciones. También le ofrecemos recomendaciones sobre cómo integrar tooset seguridad Veeam toobest con StorSimple. Se aplazan tooVeeam mejores prácticas, arquitectos de copia de seguridad y los administradores de hello tooset de manera mejor los requisitos de copia de seguridad individuales de Veeam toomeet y contratos de nivel de servicio (SLA).

Aunque se muestran tanto los pasos de configuración como los conceptos clave, este artículo no es una guía detallada de configuración o instalación. Suponemos que infraestructura y los componentes básicos de hello están en condiciones de funcionamiento y toosupport listo conceptos de Hola que describimos.

### <a name="who-should-read-this"></a>¿A quiénes está dirigido este documento?

información de Hello en este artículo será más útiles toobackup, los administradores de almacenamiento, arquitectos y administradores almacenamiento que tienen conocimientos de almacenamiento, Windows Server 2012 R2, Ethernet, servicios en la nube y Veeam.

### <a name="supported-versions"></a>Versiones compatibles

-   Veeam 9 y versiones posteriores
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
![Diagrama de niveles de Storsimple](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)

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

| Capacidad de almacenamiento | 8100 | 8600 |
|---|---|---|
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

![Diagrama lógico de StorSimple como destino de copia de seguridad principal](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Pasos lógicos de copias de seguridad en el destino principal

1.  contactos del servidor de copia de seguridad de Hola Hola a agente de copia de seguridad de destino y agente de copia de seguridad de hello transmite el servidor de copia de seguridad de datos toohello.
2.  servidor de copia de seguridad de Hello escribe datos toohello StorSimple en niveles de volúmenes.
3.  servidor de copia de seguridad de Hello actualiza la base de datos de catálogo de hello y, a continuación, finalice el trabajo de copia de seguridad de Hola.
4.  Una secuencia de comandos de instantánea desencadena el Administrador de instantáneas de nube de hello StorSimple (inicio o eliminación).
5.  servidor de copia de seguridad de Hello elimina expiradas copias de seguridad según una directiva de retención.

### <a name="primary-target-restore-logical-steps"></a>Pasos lógicos de restauración del destino principal

1.  servidor de copia de seguridad de Hello inicia restaurar los datos adecuados de Hola de repositorio de almacenamiento de Hola.
2.  agente de copia de seguridad de Hola recibe los datos de saludo del servidor de copia de seguridad de Hola.
3.  servidor de copia de seguridad de Hello finaliza el trabajo de restauración de Hola.

## <a name="storsimple-as-a-secondary-backup-target"></a>StorSimple como destino de copia de seguridad secundario

En este escenario, los volúmenes de StorSimple se utilizan principalmente para la retención o el archivado a largo plazo.

Hello en la ilustración siguiente se muestra una arquitectura de las copias de seguridad iniciales y restaura el volumen de destino un alto rendimiento. Estas copias de seguridad se copian y archivado tooa StorSimple en niveles de volumen en una programación establecida.

Es importante toosize su volumen de alto rendimiento, por lo que puede controlar los requisitos de capacidad y rendimiento de la directiva de retención.

![Diagrama lógico de StorSimple como destino de copia de seguridad secundario](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Pasos lógicos de copias de seguridad en el destino secundario

1.  contactos del servidor de copia de seguridad de Hola Hola a agente de copia de seguridad de destino y agente de copia de seguridad de hello transmite el servidor de copia de seguridad de datos toohello.
2.  servidor de copia de seguridad de Hello escribe almacenamiento de datos toohigh rendimiento.
3.  servidor de copia de seguridad de Hello actualiza la base de datos de catálogo de hello y, a continuación, finalice el trabajo de copia de seguridad de Hola.
4.  servidor de copia de seguridad de Hello copia tooStorSimple de copias de seguridad según una directiva de retención.
5.  Una secuencia de comandos de instantánea desencadena el Administrador de instantáneas de nube de hello StorSimple (inicio o eliminación).
6.  servidor de copia de seguridad de Hello elimina expiradas copias de seguridad según una directiva de retención.

### <a name="secondary-target-restore-logical-steps"></a>Pasos lógicos de restauración del destino secundario

1.  servidor de copia de seguridad de Hello inicia restaurar los datos adecuados de Hola de repositorio de almacenamiento de Hola.
2.  agente de copia de seguridad de Hola recibe los datos de saludo del servidor de copia de seguridad de Hola.
3.  servidor de copia de seguridad de Hello finaliza el trabajo de restauración de Hola.

## <a name="deploy-hello-solution"></a>Implementar soluciones de Hola

Implementar soluciones de hello requiere tres pasos:

1. Preparar la infraestructura de red de Hola.
2. Implementación del dispositivo StorSimple como destino de copia de seguridad
3. Implementación de Veeam

Cada paso se explica con detalle en las secciones siguientes de Hola.

### <a name="set-up-hello-network"></a>Configurar una red de Hola

Debido a que StorSimple es una solución que se integra con hello nube de Azure, StorSimple requiere una nube de Azure toohello de conexión activo y en funcionamiento. Esta conexión se usa para operaciones como instantáneas en la nube, la administración de datos y metadatos transferencia y almacenamiento en nube tooAzure datos más antiguos y menos acceso tootier.

Para hello solución tooperform un rendimiento óptimo, se recomienda que siga estas prácticas recomendadas de red:

-   vínculo de Hola que conecta su tooAzure nivel de StorSimple debe cumplir los requisitos de ancho de banda. Lograr esto mediante la aplicación hello necesarios calidad de servicio (QoS) nivel tooyour infraestructura conmutadores toomatch el RPO y recuperación SLA de recuperación (RTO) de tiempo.
-   Las latencias de acceso máximas de Azure Blob Storage deben rondar los 80 ms.

### <a name="deploy-storsimple"></a>Implementación de StorSimple

Para ver instrucciones detalladas para la implementación de StorSimple, consulte [Implementar el dispositivo StorSimple local](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-veeam"></a>Implementación de Veeam

Para Veeam prácticas recomendadas de instalación, consulte [copia de seguridad de Veeam & Replication Best Practices](https://bp.veeam.expert/), y lea la Guía de usuario de hello en [Veeam centro de ayuda (documentación técnica)](https://www.veeam.com/documentation-guides-datasheets.html).

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

- No use volúmenes distribuidos (creados por Windows Disk Management). Los volúmenes distribuidos no son compatibles.
- Dé formato a los volúmenes mediante NTFS con un tamaño de la unidad de asignación de 64 kB.
- Asignar los volúmenes de StorSimple Hola directamente toohello Veeam server.
    - Use iSCSI para servidores físicos.


## <a name="best-practices-for-storsimple-and-veeam"></a>Procedimientos recomendados para StorSimple y Veeam

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

### <a name="veeam-best-practices"></a>Procedimientos recomendados para Veeam

-   base de datos de Hello Veeam debe ser servidor toohello local y no reside en un volumen de StorSimple.
-   Recuperación ante desastres, realizar una copia de base de datos de hello Veeam en un volumen de StorSimple.
-   Para esta solución se admiten copias de seguridad completas e incrementales de Veeam. Se recomienda no usar copias de seguridad sintéticas y diferenciales.
-   Archivos de copia de seguridad de datos deben contener sólo los datos de saludo de un trabajo específico. Por ejemplo, no se permiten anexos de medios entre distintos trabajos.
-   Desactive la comprobación de trabajos. Si es necesario, se debe programar la comprobación después de trabajo de copia de seguridad más reciente de Hola. Es importante toounderstand que este trabajo afecta a la ventana de copia de seguridad.
-   Active la asignación previa del soporte físico.
-   Asegúrese de que está activado el procesamiento en paralelo.
-   Desactive la compresión.
-   Desactivar la desduplicación en el trabajo de copia de seguridad de Hola.
-   Configurar la optimización demasiado**LAN destino**.
-   Active **Create active full backup** (Crear copia de seguridad completa activa) (cada 2 semanas).
-   En el repositorio de copia de seguridad de hello, configure **usar archivos de copia de seguridad por VM**.
-   Establecer **usar varios flujos de carga por trabajo** demasiado**8** (se permite un máximo de 16). Ajustar este número hacia arriba o hacia abajo en función de uso de CPU en el dispositivo StorSimple Hola.

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

## <a name="set-up-veeam-storage"></a>Configuración del almacenamiento de Veeam

### <a name="tooset-up-veeam-storage"></a>tooset el almacenamiento de Veeam

1.  En hello Veeam copia de seguridad y la consola de replicación, en **repositorio herramientas**, vaya demasiado**infraestructura de copia de seguridad**. Haga clic con el botón derecho en **Backup Repositories** (Repositorios de copia de seguridad) y seleccione **Add Backup Repository** (Agregar repositorio de copia de seguridad).

    ![consola de administración de Veeam, pantalla de repositorio de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage1.png)

2.  Hola **nuevo repositorio de copia de seguridad** diálogo cuadro, escriba un nombre y una descripción para el repositorio de Hola. Seleccione **Siguiente**.

    ![consola de administración de Veeam, página de nombre y descripción](./media/storsimple-configure-backup-target-using-veeam/veeamimage2.png)

3.  Para tipo de hello, seleccione **Microsoft Windows server**. Seleccione el servidor de Veeam Hola. Seleccione **Siguiente**.

    ![consola de administración de Veeam, selección del tipo de repositorio de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage3.png)

4.  toospecify **ubicación**, busque y seleccione el volumen de Hola. Seleccione hello **limitar el número máximo de tareas simultáneo a:** hello de conjunto y la casilla de verificación valoran demasiado**4**. Esto garantiza que solo se procesen cuatro discos virtuales simultáneamente mientras se procesa cada máquina virtual (VM). Seleccione hello **avanzadas** botón.

    ![consola de administración de Veeam, selección de volumen](./media/storsimple-configure-backup-target-using-veeam/veeamimage4.png)


5.  Hola **configuración de compatibilidad de almacenamiento** cuadro de diálogo, seleccione hello **usar archivos de copia de seguridad por VM** casilla de verificación.

    ![consola de administración de Veeam, configuración de compatibilidad de almacenamiento](./media/storsimple-configure-backup-target-using-veeam/veeamimage5.png)

6.  Hola **nuevo repositorio de copia de seguridad** cuadro de diálogo, seleccione hello **habilitar servicios de NFS vPower en servidor de montaje de hello (recomendado)** casilla de verificación. Seleccione **Siguiente**.

    ![consola de administración de Veeam, pantalla de repositorio de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage6.png)

7.  Revisar la configuración de hello y, a continuación, seleccione **siguiente**.

    ![consola de administración de Veeam, pantalla de repositorio de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage7.png)

    Un repositorio se haya agregado toohello Veeam server.

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configuración de StorSimple como destino de copia de seguridad principal

> [!IMPORTANT]
> Se produce una restauración de datos desde una copia de seguridad que se ha toohello en capas en la nube a velocidades de nube.

Hello en la ilustración siguiente se muestra hello asignación de un trabajo de copia de seguridad de tooa volumen normal. En este caso, todas las copias de seguridad semanales de hello asignan disco lleno de toohello sábado, y copias de seguridad incrementales de hello asignan discos incremental tooMonday viernes. Hola a todos las copias de seguridad y restauraciones son de un StorSimple en niveles de volumen.

![Diagrama lógico de la configuración de destino de copia de seguridad principal](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Ejemplo de programación GFS de StorSimple como destino de copia de seguridad principal

A continuación se muestra un ejemplo de programación de rotación GFS para cuatro semanas, mensual, y anual:

| Frecuencia o tipo de copia de seguridad | Completo | Incremental (días 1-5)  |   
|---|---|---|
| Semanal (semanas 1-4) | Sábado | Lunes-viernes |
| Mensual  | Sábado  |   |
| Anual | Sábado  |   |   |


### <a name="assign-storsimple-volumes-tooa-veeam-backup-job"></a>Asignar trabajo de copia de seguridad de Veeam de tooa de volúmenes de StorSimple

Para el escenario de destino de copia de seguridad principal, cree un trabajo diario con el volumen de Veeam StorSimple principal. Para un escenario de destino de copia de seguridad secundaria, cree un trabajo diario mediante almacenamiento conectado directamente (DAS), almacenamiento conectado a red (NAS) o un grupo de discos sin más (JBOD).

#### <a name="tooassign-storsimple-volumes-tooa-veeam-backup-job"></a>trabajo de copia de seguridad de tooassign StorSimple volúmenes tooa Veeam

1.  En hello Veeam copia de seguridad y la consola de replicación, seleccione **copia de seguridad y replicación**. Haga clic con el botón derecho en **Backup** (Copia de seguridad) y luego seleccione **VMware** o **Hyper-V**, en función del entorno.

    ![consola de administración de Veeam, nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage8.png)

2.  Hola **nuevo trabajo de copia de seguridad** diálogo cuadro, escriba un nombre y una descripción para el trabajo de copia de seguridad diaria Hola.

    ![consola de administración de Veeam, nueva página de trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage9.png)

3.  Seleccione hasta un tooback de máquina virtual.

    ![consola de administración de Veeam, nueva página de trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage10.png)

4.  Seleccione los valores de hello que desee para **proxy de copia de seguridad** y **repositorio de copia de seguridad**. Seleccione un valor para **tookeep los puntos de restauración en disco** almacenamiento conectado en según toohello definiciones de RPO y RTO para su entorno de forma local. Seleccione **Advanced** (Avanzadas).

    ![consola de administración de Veeam, nueva página de trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage11.png)

5. Hola **configuración avanzada** cuadro de diálogo de hello **copia de seguridad** ficha, seleccione **Incremental**. Asegúrese de que hello **crear periódicamente copias de seguridad completas sintéticos** casilla de verificación está desactivada. Seleccione hello **crear periódicamente copias de seguridad completas activas** casilla de verificación. En **copia de seguridad completa Active**, seleccione hello **semanal en los días seleccionados** casilla de verificación para el sábado.

    ![consola de administración de Veeam, página de configuración avanzada de nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage12.png)

6. En hello **almacenamiento** ficha, asegúrese de que ese hello **habilitar la desduplicación de datos en línea** casilla de verificación está desactivada. Seleccione hello **bloques de archivo de intercambio de exclusión** casilla de verificación y seleccione hello **excluir elimina bloques de archivo** casilla de verificación. Establecer **nivel de compresión** demasiado**ninguno**. Rendimiento equilibrado y desduplicación, establezca **optimización del almacenamiento** demasiado**destino LAN**. Seleccione **Aceptar**.

    ![consola de administración de Veeam, página de configuración avanzada de nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage13.png)

    Para obtener información sobre la configuración de desduplicación y de compresión de Veeam, consulte [Data Compression and Deduplication](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html) (Compresión y desduplicación de datos).

7.  Hola **Editar trabajo de copia de seguridad** cuadro de diálogo, puede seleccionar hello **Habilitar procesamiento consciente de las aplicaciones** casilla de verificación (opcional).

    ![consola de administración de Veeam, página de procesamiento de invitado de nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage14.png)

8.  Establecer Hola programación toorun una vez al día, a la vez que puede especificar.

    ![consola de administración de Veeam, página de programación de nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage15.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configuración de StorSimple como destino de copia de seguridad secundario

> [!NOTE]
> Restauraciones de datos desde una copia de seguridad que se ha toohello en capas en la nube se producen a velocidades de nube.

En este modelo, debe tener un tooserve de medios (distintos de StorSimple) de almacenamiento como una memoria caché temporal. Por ejemplo, puede usar una matriz redundante de espacio de tooaccommodate de volumen de discos independientes (RAID), la entrada/salida (E/S) y el ancho de banda. Se recomienda usar RAID 5, 50 y 10.

Hola figura siguiente muestra el típico volúmenes de local (toohello server) de retención a corto plazo y archivo retención a largo plazo. En este escenario, todas las copias de seguridad se ejecutan en hello local (toohello server) volumen RAID. Estas copias de seguridad periódicamente están duplicados y archivan tooan volumen de archivo. Es importante toosize local (toohello server) volumen RAID, por lo que puede controlar los requisitos de capacidad y rendimiento de retención a corto plazo.

![Diagrama lógico de StorSimple como destino de copia de seguridad secundario](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetdiagram.png)

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>Ejemplo de GFS de StorSimple como destino de copia de seguridad secundario

tabla Hola siguiente muestra cómo tooset una toorun de las copias de seguridad en discos de StorSimple y locales de Hola. Incluye requisitos de capacidad individual y total.

| Tipo de copia de seguridad y retención | Almacenamiento configurado | Tamaño (TiB) | Multiplicador de GFS | Capacidad total \* (TiB) |
|---|---|---|---|---|
| Semana 1 (completa e incremental) |Disco local (a corto plazo)| 1 | 1 | 1 |
| StorSimple semanas 2-4 |Disco de StorSimple (largo plazo) | 1 | 4 | 4 |
| Completa mensual |Disco de StorSimple (largo plazo) | 1 | 12 | 12 |
| Completa anual |Disco de StorSimple (largo plazo) | 1 | 1 | 1 |
|Requisito de tamaño de volúmenes de GFS |  |  |  | 18*|
\* la capacidad total incluye 17 TiB de discos de StorSimple y 1 TiB de volumen RAID local.


### <a name="gfs-example-schedule"></a>Programación de ejemplo de GFS

Programación semanal, mensual y anual de rotación de GFS

| Semana | Completo | Incremental día 1 | Incremental día 2 | Incremental día 3 | Incremental día 4 | Incremental día 5 |
|---|---|---|---|---|---|---|
| Semana 1 | Volumen RAID local  | Volumen RAID local | Volumen RAID local | Volumen RAID local | Volumen RAID local | Volumen RAID local |
| Semana 2 | StorSimple semanas 2-4 |   |   |   |   |   |
| Semana 3 | StorSimple semanas 2-4 |   |   |   |   |   |
| Semana 4 | StorSimple semanas 2-4 |   |   |   |   |   |
| Mensual | StorSimple mensual |   |   |   |   |   |
| Anual | StorSimple anual  |   |   |   |   |   |   |

### <a name="assign-storsimple-volumes-tooa-veeam-copy-job"></a>Asignar el trabajo de copia de Veeam de tooa de volúmenes de StorSimple

#### <a name="tooassign-storsimple-volumes-tooa-veeam-copy-job"></a>trabajo de copia de tooassign StorSimple volúmenes tooa Veeam

1.  En hello Veeam copia de seguridad y la consola de replicación, seleccione **copia de seguridad y replicación**. Haga clic con el botón derecho en **Backup** (Copia de seguridad) y luego seleccione **VMware** o **Hyper-V**, en función del entorno.

    ![consola de administración de Veeam, página de nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage16.png)

2.  Hola **nuevo trabajo de copia de copia de seguridad** diálogo cuadro, escriba un nombre y una descripción para el trabajo de Hola.

    ![consola de administración de Veeam, página de nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage17.png)

3.  Seleccione hello las máquinas virtuales que desee tooprocess. Seleccione desde las copias de seguridad y, a continuación, seleccione Hola copia de seguridad diaria que creó anteriormente.

    ![consola de administración de Veeam, página de nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage18.png)

4.  Excluir objetos de trabajo de copia de seguridad de hello, si es necesario.

5.  Seleccione el repositorio de copia de seguridad y establecer un valor para **tookeep los puntos de restauración**. Estar seguro de hello tooselect **siguiente de hello mantener puntos de restauración para archivarlo** casilla de verificación. Definir la frecuencia de copia de seguridad de hello y, a continuación, seleccione **avanzadas**.

    ![consola de administración de Veeam, página de nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage19.png)

6.  Especifique la siguiente Hola configuración avanzada:

    * En hello **mantenimiento** ficha, desactive la opción protección de daño en el nivel de almacenamiento.

    ![consola de administración de Veeam, página de configuración avanzada de nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage20.png)

    * En hello **almacenamiento** ficha, debe asegurarse de que la desduplicación y compresión están desactivados.

    ![consola de administración de Veeam, página de configuración avanzada de nuevo trabajo de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/veeamimage21.png)

7.  Especificar que la transferencia de datos de hello es directa.

8.  Definir la programación de la ventana de copia de seguridad Hola según las necesidades tooyour y, a continuación, finalice al Asistente de Hola.

Para obtener más información, consulte [Create backup copy jobs](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html) (Creación de trabajos de copia de seguridad).

## <a name="storsimple-cloud-snapshots"></a>Instantáneas de nube de StorSimple

Las instantáneas de nube de StorSimple protegen los datos de Hola que reside en el dispositivo StorSimple. Crear una instantánea en la nube es la herramienta de fuera del sitio de tooan de cintas de copia de seguridad local de tooshipping equivalente. Si utiliza el almacenamiento de Azure con redundancia geográfica, crear una instantánea en la nube es toomultiple sitios de tooshipping equivalente cintas de copia de seguridad. Si necesita toorestore un dispositivo después de un desastre, puede poner en línea otro dispositivo de StorSimple y realice una conmutación por error. Después de la conmutación por error de hello, serían los datos de Hola de tooaccess pueda (a velocidades de nube) desde la instantánea más reciente en la nube Hola.

Hola siguiente sección describe cómo toocreate una toostart breve secuencia de comandos y delete StorSimple instantáneas en la nube durante el procesamiento posterior a la copia de seguridad.

> [!NOTE]
> Las instantáneas que se crean manualmente o mediante programación no siguen la directiva de expiración de instantáneas de StorSimple de Hola. En otras palabras, se deben eliminar manualmente o mediante programación.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Inicio y eliminación de instantáneas en la nube con un script

> [!NOTE]
> Evalúe cuidadosamente repercusiones de retención de datos y cumplimiento de normas de hello antes de eliminar una instantánea de StorSimple. Para obtener más información acerca de cómo toorun una secuencia de comandos posteriores a la copia de seguridad, consulte la documentación de Veeam de Hola.


### <a name="backup-lifecycle"></a>Ciclo de vida de copia de seguridad

![Diagrama del ciclo de vida de copia de seguridad](./media/storsimple-configure-backup-target-using-veeam/backuplifecycle.png)

### <a name="requirements"></a>Requisitos

-   servidor de Hola que se ejecuta el script de Hola debe tener acceso a los recursos en la nube tooAzure.
-   cuenta de usuario de Hello debe tener los permisos necesarios de Hola.
-   Una directiva de copia de seguridad de StorSimple con hello asociado StorSimple volúmenes deben ser configurados pero no activados.
-   Necesitará Hola nombre de recursos de StorSimple, clave de registro, nombre de dispositivo e Id. de directiva de copia de seguridad.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart o eliminar una instantánea en la nube

1. [Instale Azure PowerShell](/powershell/azure/overview).
2. [Descargue e importe la configuración de publicación y la información de suscripción](https://msdn.microsoft.com/library/dn385850.aspx).
3. En el portal de Azure clásico de Hola, obtener el nombre de recurso de Hola y [clave de registro para el servicio StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4. En el servidor de Hola que ejecuta el script de Hola, ejecute PowerShell como administrador. Escriba el siguiente comando:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    Id. de directiva de copia de seguridad de Hola de nota.
5. En el Bloc de notas, crear un nuevo script de PowerShell mediante Hola siguiente código.

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
6. copia de seguridad de tooadd Hola script tooyour del trabajo, edite el trabajo de Veeam opciones avanzadas.

    ![Pestaña de script de configuración avanzada de copia de seguridad de Veeam](./media/storsimple-configure-backup-target-using-veeam/veeamimage22.png)

Se recomienda que ejecute la directiva de copia de seguridad de instantáneas de StorSimple en la nube como una secuencia de comandos posteriores al procesamiento final Hola de su trabajo de copia de seguridad diaria. Para obtener más información acerca de cómo tooback seguridad y restauración su toohelp de entorno de aplicación de copia de seguridad que cumple el RPO y el RTO, póngase en contacto con el arquitecto de copia de seguridad.

## <a name="storsimple-as-a-restore-source"></a>StorSimple como origen de restauración

Las restauraciones desde un dispositivo de StorSimple funcionan como las de cualquier dispositivo de almacenamiento en bloque. Restauraciones de datos que está en la nube en niveles toohello tiene lugar a velocidades de nube. Para los datos locales, restauraciones se producen a velocidad de disco local de hello de dispositivo de Hola.

Con Veeam, obtendrá una recuperación rápida granular y nivel de archivo a través de StorSimple a través de vistas de explorador integrado hello en la consola de Veeam Hola. Utilice los elementos Veeam exploradores individuales del toorecover, como mensajes de correo electrónico, los objetos de Active Directory y los elementos de SharePoint desde las copias de seguridad. recuperación de Hello puede realizarse sin interrupciones de máquina virtual local. También puede hacer recuperaciones a partir de un momento específico de Azure SQL Database y bases de datos de Oracle. Veeam y StorSimple facilitar el proceso de Hola de recuperación de nivel de elemento de Azure rápida y sencilla. Para obtener información acerca de cómo tooperform una restauración, consulte la documentación de Veeam de hello:

- Para [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)
- Para [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)
- Para [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)
- Para [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)
- Para [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)


## <a name="storsimple-failover-and-disaster-recovery"></a>Conmutación por error y recuperación ante desastres de StorSimple

> [!NOTE]
> En los escenarios de destino de copia de seguridad, StorSimple Cloud Appliance no se admite como destino de restauración.

Un desastre puede deberse a una serie de factores. Hello en la tabla siguiente enumera escenarios comunes de recuperación ante desastres.

| Escenario | Impacto | Cómo toorecover | Notas |
|---|---|---|---|
| Error de dispositivo de StorSimple | Se interrumpen las operaciones de copia de seguridad y restauración. | Reemplace el dispositivo con error de Hola y realizar [StorSimple conmutación por error y recuperación ante desastres](storsimple-device-failover-disaster-recovery.md). | Si necesita tooperform una restauración tras la recuperación de dispositivo, los espacios de trabajo de todos los datos se recuperan de nuevo dispositivo de hello en la nube toohello. Todas las operaciones se realizan a velocidades de la nube. índice de Hola y volver a examinar el proceso de catálogo pueden provocar todos los toobe de conjuntos de copia de seguridad examina y extraerse de hello capa toohello dispositivo local capa de nube, que podría ser un proceso lento. |
| Error de servidor de Veeam | Se interrumpen las operaciones de copia de seguridad y restauración. | Volver a generar el servidor de copia de seguridad de Hola y realizar la restauración de base de datos como se detalla en [Veeam centro de ayuda (documentación técnica)](https://www.veeam.com/documentation-guides-datasheets.html).  | Debe volver a generar o restaurar hello Veeam servidor en el sitio de recuperación ante desastres de Hola. Hola base de datos toohello más reciente punto de restauración. Si hello base de datos restaurada Veeam no está sincronizada con los trabajos de copia de seguridad más recientes, se requiere la indización y catalogación. Este índice y volver a examinar el proceso de catálogo pueden provocar todos los toobe de conjuntos de copia de seguridad examina y extraerse de la capa de hello nube capa toohello dispositivo local. Esto hace que requiera mucho tiempo. |
| Error del sitio que resulta en pérdida de saludo del servidor de copia de seguridad de Hola y StorSimple | Se interrumpen las operaciones de copia de seguridad y restauración. | Restaure primero StorSimple y después Veeam. | Restaure primero StorSimple y después Veeam. Si necesita tooperform una restauración tras la recuperación de dispositivo, los espacios de trabajo de datos completa de Hola se recuperan de nuevo dispositivo de hello en la nube toohello. Todas las operaciones se realizan a velocidades de la nube. |


## <a name="references"></a>Referencias

Hola después documentos hizo referencia a este artículo:

- [Configurar E/S de múltiples rutas para el dispositivo StorSimple](storsimple-configure-mpio-windows-server.md)
- [Escenarios de almacenamiento: el aprovisionamiento fino](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Using GPT drives](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD) (Uso de unidades de GPT)
- [Habilitar y configurar las instantáneas de carpetas compartidas](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Pasos siguientes

- Más información acerca de cómo demasiado[restauración a partir de un conjunto de copia de seguridad](storsimple-restore-from-backup-set-u2.md).
- Más información acerca de cómo tooperform [dispositivo conmutación por error y recuperación ante desastres](storsimple-device-failover-disaster-recovery.md).
