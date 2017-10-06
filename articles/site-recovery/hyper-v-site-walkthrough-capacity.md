---
title: "aaaPlan capacidad y escalado de máquinas virtuales de Hyper-V tooAzure de replicación (sin WMM) con Azure Site Recovery | Documentos de Microsoft"
description: "Use este artículo tooplan capacidad y el escalado al replicar las máquinas virtuales de Hyper-V tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f5b029f273e51c01c7d918d176832f6d1735b5f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-tooazure-replication"></a>Paso 3: Planear la capacidad y ajuste de escala para la replicación de Hyper-V tooAzure

Utilice este toofigure artículo planear la capacidad y el ajuste de escala, al replicar tooAzure de máquinas virtuales de Hyper-V (sin System Center VMM) local con [Azure Site Recovery](site-recovery-overview.md).

Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="how-do-i-start-capacity-planning"></a>¿Cómo se puede iniciar el planeamiento de la capacidad?


Recopilar información acerca de su entorno de replicación y, a continuación, planear la capacidad de usar esta información, junto con las consideraciones de hello resaltado en este artículo.


## <a name="gather-information"></a>Recopilación de información

1. Recopilar información sobre su entorno de replicación, incluidas las máquinas virtuales, discos por máquina virtual y almacenamiento por disco.
2. Identifique la tasa de cambio (renovación) diaria para los datos replicados. Descargar hello [herramienta de planeación de capacidad de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) tasa de cambio de tooget Hola. Se recomienda que ejecutar esta herramienta en una semana toocapture promedios.
 

## <a name="figure-out-capacity"></a>Averiguar la capacidad

Según se haya recopilación de información de hello, ejecute hello [herramienta de planificador de capacidad de recuperación de sitios](http://aka.ms/asr-capacity-planner-excel) tooanalyze su entorno de origen y las cargas de trabajo, calcular las necesidades de ancho de banda y los recursos del servidor de ubicación de origen de Hola y Hola recursos (máquinas virtuales y almacenamiento etcetera), que necesita en la ubicación de destino de Hola. Puede ejecutar la herramienta Hola de dos modos:

- Planificación rápida: ejecutar la herramienta de hello en este modo tooget red y el servidor las proyecciones basadas en un número medio de las máquinas virtuales, discos, almacenamiento y tasa de cambio.
- Planificación detallada: ejecutar la herramienta de hello en este modo y proporcionar detalles de cada carga de trabajo en el nivel de máquina virtual. Analice la compatibilidad de la máquina virtual y obtenga proyecciones de red y del servidor.

Ahora ejecute la herramienta de hello:

1. Descargar hello [herramienta](http://aka.ms/asr-capacity-planner-excel)
2. planificador rápido de toorun hello, siga [estas instrucciones](site-recovery-capacity-planner.md#run-the-quick-planner)y seleccione Hola escenario **tooAzure de Hyper-V**.
3. toorun Hola planner detallada, siga [estas instrucciones](site-recovery-capacity-planner.md#run-the-detailed-planner)y el escenario de hello seleccione **tooAzure de Hyper-V**.

## <a name="control-network-bandwidth"></a>Ancho de banda de red de control

Cuando se haya ancho de banda de hello calculado que necesita, tiene un par de opciones para controlar cantidad Hola de ancho de banda utilizado para la replicación:

* **Limitar ancho de banda**: tráfico de Hyper-V que replica tooAzure pasa a través de un host de Hyper-V específico. También puede limitar el ancho de banda en el servidor de host de Hola.
* **Influir en el ancho de banda**: puede influir en el ancho de banda de hello utilizado para la replicación con un par de claves del registro.

### <a name="throttle-bandwidth"></a>Limitar el ancho de banda
1. Abra Hola MMC de copia de seguridad de Microsoft Azure complemento en el servidor de host de Hyper-V de Hola. De forma predeterminada un acceso directo para copia de seguridad de Microsoft Azure está disponible en el escritorio de Hola o en Agent\bin\wabadmin de servicios de recuperación de C:\Program Files\Microsoft Azure.
2. En el complemento hello, haga clic en **cambiar las propiedades de**.
3. En hello **limitación** ficha seleccione **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet**y establecer los límites de hello para el trabajo y no laborables horas. Intervalo válido es de 512 Kbps too102 Mbps por segundo.

    ![Limitar el ancho de banda](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

También puede usar hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitación. Aquí tiene un ejemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que no se requiere ninguna limitación.

### <a name="influence-network-bandwidth"></a>Control del uso de ancho de banda de red
1. En el registro de hello navegue demasiado**Backup\Replication de Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.
   * tráfico de ancho de banda de hello tooinfluence en un disco de la replicación, modificar Hola Hola de valor **UploadThreadsPerVM**, también puede crear la clave de hello si no existe.
   * ancho de banda de tooinfluence hello para el tráfico de la conmutación por recuperación de Azure, modifique el valor de hello **DownloadThreadsPerVM**.
2. valor predeterminado de Hello es 4. En una red de "sobreaprovisionada", estas claves del registro deben cambiarse de valores predeterminados de Hola. Hola máximo es 32. Supervisar el tráfico toooptimize Hola valor.

## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 4: planear las redes](hyper-v-site-walkthrough-network.md).
