---
title: "aaaPlan capacidad y escalado para tooAzure de replicación de VMware con Azure Site Recovery | Documentos de Microsoft"
description: "Use este artículo tooplan capacidad y el escalado al replicar máquinas virtuales VMware tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 551533ab7090d85c216be242ea92781deb8287ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-vmware-tooazure-replication"></a>Paso 3: Planear la capacidad y ajuste de escala para la replicación de tooAzure de VMware

Utilice este toofigure artículo planear la capacidad y el ajuste de escala, al replicar máquinas virtuales de VMware locales y servidores físicos tooAzure con [Azure Site Recovery](site-recovery-overview.md).

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="how-do-i-start-capacity-planning"></a>¿Cómo se puede iniciar el planeamiento de la capacidad?

Recopilar información acerca de su entorno de replicación y, a continuación, planear la capacidad de usar esta información, junto con las consideraciones de hello resaltado en este artículo.


## <a name="gather-information"></a>Recopilación de información

1. Descargar hello [herramienta de planeación de implementación](https://aka.ms/asr-deployment-planner) para la replicación de VMware.
2. [Lea este artículo](site-recovery-deployment-planner.md) toounderstand cómo toorun Hola herramienta.
3. Mediante la herramienta de hello recopilar información sobre máquinas virtuales compatibles e incompatibles, discos por máquina virtual, y la renovación de datos por disco. herramienta de Hello también cubre hello Azure infraestructura necesaria para la replicación y prueba de conmutación por error correcta y los requisitos de ancho de banda de red.

## <a name="replication-considerations"></a>Consideraciones sobre la replicación

Tenga en cuenta estas consideraciones antes de iniciar la implementación:

**Componente** | **Detalles** |
--- | --- | ---
**Replicación** | **Tasa de cambio diario máximo:** una máquina protegida sólo puede utilizar un servidor de procesos, y puede administrar un servidor de proceso único una tasa de cambio diaria hasta too2 TB. Por lo tanto 2 TB es tasa con la que se admite para una máquina protegida de cambio de datos diario máximo Hola.<br/><br/> **Rendimiento máximo:** un equipo replicado puede pertenecer tooone cuenta de almacenamiento de Azure. Una cuenta de almacenamiento estándar puede contener un máximo de 20.000 solicitudes por segundo, y se recomienda mantener Hola número de operaciones de entrada/salida por segundo (IOPS) a través de un too20 de la máquina de origen, 000. Por ejemplo, si tiene una máquina de origen con 5 discos y cada disco genera 120 IOPS (tamaño de 8 KB) en la máquina de origen de hello, resultará en hello Azure por límite de IOPS de disco de 500. (número de Hola de cuentas de almacenamiento necesaria es la máquina de origen total igual toohello IOPS, dividida por 20.000).

## <a name="configuration-server-capacity"></a>Capacidad del servidor de configuración

servidor de configuración de Hello debería ser capacidad de tasa de cambio diaria de toohandle capaz de hello en todas las cargas de trabajo que ejecutan en equipos protegidos y necesita toocontinuously de ancho de banda suficiente replicar tooAzure almacenamiento de datos.

Como práctica recomendada, busque el servidor de configuración de hello en hello misma red y el segmento de LAN como Hola máquinas que desee tooprotect. Se puede encontrarse en una red diferente, pero las máquinas que desee tooprotect debe tener tooit de visibilidad de capa 3 red.

## <a name="sizing-recommendations"></a>Recomendaciones de tamaño

tabla de Hola resumen las recomendaciones de ajuste de tamaño en función de la CPU.

**CPU** | **Memoria** | **Tamaño del disco de caché** | **Frecuencia de cambio de datos** | **Máquinas protegidas**
--- | --- | --- | --- | ---
8 vCPU (2 sockets * 4 núcleos @ 2,5 gigahercios [GHz]) | 16 GB | < 300 GB | 500 GB o menos | Replicar menos de 100 máquinas.
12 vCPUs (2 sockets * 6 núcleos @ 2,5 GHz) | 18 GB | 600 GB | 500 GB too1 TB | Replicar entre 100 y 150 máquinas.
16 vCPUs (2 sockets * 8 núcleos @ 2,5 GHz) | 32 GB | 1 TB | 1 TB too2 TB | Replicar entre 150 y 200 máquinas.
Implementar otro servidor de procesos | | | 2 TB | Implementar servidores de procesos adicionales si se están replicando más de 200 máquinas o si cambian los datos diario de hello tasa mayor que 2 TB.

Donde:

* Cada máquina de origen está configurada con 3 discos de 100 GB cada una.
* Usamos almacenamiento de pruebas comparativas de 8 unidades SAS de 10 K RPM con RAID 10 para las mediciones de disco de caché.

## <a name="process-server-capacity"></a>Capacidad del servidor de procesos


servidor de procesos de Hello recibe datos de replicación de máquinas protegidas y optimiza con almacenamiento en caché, la compresión y cifrado. A continuación, envía hello tooAzure de datos.

- equipo del servidor de proceso de Hello debe tener suficientes tooperform recursos estas tareas.
- primer servidor de proceso Hola se instala de forma predeterminada en el servidor de configuración de Hola. Puede implementar tooscale de servidores de proceso adicionales en su entorno.
- servidor de procesos de Hello usa una caché basada en disco. Use un disco independiente de memoria caché de 600 GB o más cambios de datos de toohandle almacenados en caso de hello de un cuello de botella de red o una interrupción.
- Si necesita tooprotect más de 200 máquinas o tasa de cambio diaria de hello es mayor que 2 TB, puede agregar proceso servidores toohandle Hola replicación carga. tooscale out, puede:
    - Aumentar el número de Hola de servidores de configuración. Por ejemplo, puede proteger las máquinas de too400 con dos servidores de configuración.
    - Agregar más servidores de procesos y utilizar dichos servidores de configuración toohandle Hola de tráfico en lugar de (o además de).


### <a name="example-process-server-scaling"></a>Ejemplo de escalado de los servidores de procesos

Hello en la tabla siguiente describe un escenario en el que:

* No tiene previsto servidor de configuración de hello toouse como un servidor de procesos.
* Ha configurado un servidor de procesos adicional.
* Ha configurado el servidor de proceso adicional de máquinas virtuales protegidas toouse Hola.
* Cada máquina de origen protegida está configurada con tres discos de 100 GB cada uno.

**Servidor de configuración** | **Servidores de procesos adicionales** | **Tamaño del disco de caché** | **Frecuencia de cambio de datos** | **Máquinas protegidas**
--- | --- | --- | --- | ---
8 vCPU (2 sockets * 4 núcleos a 2,5 GHz), 16 GB de memoria | 4 vCPU (2 sockets * 2 núcleos a 2,5 GHz), 8 GB de memoria | < 300 GB | 250 GB o menos | Replicar 85 máquinas o menos.
8 vCPU (2 sockets * 4 núcleos a 2,5 GHz), 16 GB de memoria | 8 vCPU (2 sockets * 4 núcleos a 2,5 GHz), 12 GB de memoria | 600 GB | 250 GB too1 TB | Replicar entre 85 y 150 máquinas.
12 vCPU (2 sockets * 6 núcleos a 2,5 GHz), 18 GB de memoria | 12 vCPU (2 sockets * 6 núcleos a 2,5 GHz), 24 GB de memoria | 1 TB | 1 TB too2 TB | Replicar entre 150 y 225 máquinas.

forma de Hello en el que escalar los servidores depende de sus preferencias para un modelo de escalado vertical y escalado horizontal.  Puede escalar verticalmente con la implementación de algunos servidores de procesos y de configuración de alto nivel, mientras que, para escalar horizontalmente, debe implementar más servidores con menos recursos. Por ejemplo, si necesita tooprotect 220 máquinas, puede realizar una de los siguientes hello:

* Configurar el servidor de configuración de hello con 12 vCPU, 18 GB de memoria y un servidor de proceso adicionales con 12 vCPU, 24 GB de memoria. Configurar servidor de proceso adicionales solo de las máquinas protegidas toouse Hola.
* Configurar dos servidores de configuración (vCPU, 16 GB de RAM de 2 x 8) y dos servidores de proceso adicionales (vCPU de 1 x 8 y 4 vCPU 1 toohandle 135 + 85 [220] máquinas). Configure los servidores de proceso adicionales solo de las máquinas protegidas toouse Hola.

## <a name="deploy-additional-process-servers"></a>Implementar servidores de procesos adicionales

Siga estos tooset de instrucciones de un servidor de proceso adicionales. Después de configurar el servidor de hello, migrar toouse de máquinas de origen se.

1. En **servidores de Site Recovery**, haga clic en el servidor de configuración de hello > **+ servidor de procesos**.
2. En **Tipo de servidor**, haga clic en **Servidor de procesos (local)**.

    ![Servidor de proceso](./media/vmware-walkthrough-capacity/migrate-ps2.png)
3. Descargar el archivo de configuración de Site Recovery unificado de hello.
4. Ejecutar el programa de instalación tooinstall Hola proceso servidor y regístrelo en el almacén de Hola.
5. En **antes de comenzar**, seleccione **agregar tooscale de servidores de proceso adicionales horizontalmente la implementación**.
6. En **detalles del servidor de configuración**, especifique la dirección IP de Hola Hola del servidor de configuración y Hola frase de contraseña. Si no tiene la frase de contraseña de hello, puede obtenerlo mediante la ejecución de **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** en servidor de configuración de Hola.

    ![Servidor de configuración](./media/vmware-walkthrough-capacity/add-ps2.png)
7. Complete el resto de hello del programa de instalación en hello igual que utilizó al configurar el servidor de configuración de Hola.

### <a name="migrate-machines-toouse-hello-process-server"></a>Migrar el servidor de procesos de máquinas toouse Hola

1. En **configuración** > **servidores de Site Recovery**, haga clic en el servidor de configuración de hello > **servidores de procesos**.
2. Servidor de procesos de hello contextual actualmente en uso > **conmutador**.

    ![Cambio del servidor de procesos](./media/vmware-walkthrough-capacity/migrate-ps3.png)
3. En **servidor de procesos de destino Select**, seleccione servidor de procesos de Hola que desee toouse y seleccione las máquinas virtuales de hello ese servidor hello controlará.
4. Haga clic en el icono de información de Hola. toohelp realizar decisiones de carga, Hola espacio medio requerido tooreplicate se muestra cada VM toohello nuevo servidor de procesos seleccionado.
5. Haga clic en hello marca de verificación toostart replicación toohello nuevo servidor de procesos.

## <a name="control-network-bandwidth"></a>Ancho de banda de red de control

Después de ejecutar [herramienta de planeación de implementación de hello](site-recovery-deployment-planner.md) ancho de banda de hello toocalculate que necesita para la replicación (replicación inicial de hello y, a continuación, delta), puede controlar la cantidad de Hola de ancho de banda utilizado para la replicación con un par de opciones:

* **Limitar ancho de banda**: tráfico de VMware que se replica tooAzure pasa a través de un servidor de proceso específico. También puede limitar el ancho de banda en máquinas de Hola que se ejecutan como servidores de procesos.
* **Influir en el ancho de banda**: puede influir en el ancho de banda de hello usada para la replicación mediante el uso de un par de claves del registro:
  * Hola **Backup\UploadThreadsPerVM de Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows** valor del registro especifica el número de Hola de subprocesos que se usan para la transferencia de datos (la replicación inicial o delta) de un disco. Un valor mayor aumenta el ancho de banda de red de hello usada para la replicación.
  * Hola **Backup\DownloadThreadsPerVM de Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows** especifica Hola número de subprocesos usados para la transferencia de datos durante la conmutación por recuperación.

### <a name="throttle-bandwidth"></a>Limitar el ancho de banda

1. Abra hello en el complemento MMC de copias de seguridad de Azure en actúa de máquina de hello como servidor de procesos de Hola. De forma predeterminada, está disponible en el escritorio de Hola u Hola después la carpeta un acceso directo para copia de seguridad: Agent\bin\wabadmin de servicios de recuperación de C:\Program Files\Microsoft Azure.
2. En el complemento de hello, haga clic en **cambiar las propiedades de**.
3. En hello **limitación** ficha, seleccione **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet**.
4. Establecer límites de hello para el trabajo y no laborables horas. Intervalo válido es de 512 Kbps too102 Mbps por segundo.

    ![Limitación](./media/vmware-walkthrough-capacity/throttle2.png)

También puede usar hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitación. Aquí tiene un ejemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que no se requiere ninguna limitación.

### <a name="influence-network-bandwidth-for-a-vm"></a>Control del uso de ancho de banda de red para una VM

1. En el registro del programa Hola a máquina virtual, vaya demasiado**Backup\Replication de Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.
   * tráfico de ancho de banda de hello tooinfluence en un disco de la replicación, modifique el valor de Hola de **UploadThreadsPerVM**, también puede crear la clave de hello si no existe.
   * ancho de banda de tooinfluence hello para el tráfico de la conmutación por recuperación de Azure, modifique el valor de Hola de **DownloadThreadsPerVM**.
2. valor predeterminado de Hello es 4. En una red sobreaprovisionada, se deben cambiar los valores de estas claves del Registro. Hola máximo es 32. Supervisar el tráfico toooptimize Hola valor.




## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 4: planear las redes](vmware-walkthrough-network.md).
