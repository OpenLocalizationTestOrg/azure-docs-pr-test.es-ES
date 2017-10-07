---
title: aaaUse copia de seguridad de Azure tooreplace su infraestructura de cinta | Documentos de Microsoft
description: "Obtenga información acerca de la copia de seguridad de Azure proporciona semántica similar a la cinta que le permite toobackup y restaurar datos de Azure"
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a>Mover el almacenamiento a largo plazo en cinta toohello nube de Azure
Los clientes de Copia de seguridad de Microsoft Azure y System Center Data Protection Manager pueden:

* Hacer copia de seguridad de los datos en las programaciones que más se ajuste a las necesidades de organización Hola.
* Conservar los datos de copia de seguridad de Hola durante períodos más largos
* Hacer a Azure partícipe de sus necesidades de retención a largo plazo (en lugar de la cinta).

Este artículo explica cómo los clientes pueden habilitar las directivas de copia de seguridad y retención. Los clientes que usen las cintas tooaddress su largo-duración de retención debe ahora tiene una alternativa viable y eficaz con la disponibilidad de Hola de esta característica. característica Hello se habilita una en la versión más reciente de Hola de hello copia de seguridad de Azure (que está disponible [aquí](http://aka.ms/azurebackup_agent)). Los clientes de System Center DPM deben actualizar a, como mínimo, DPM 2012 R2 UR5 antes de usar DPM con Hola servicio de copia de seguridad de Azure.

## <a name="what-is-hello-backup-schedule"></a>¿Qué es hello programación de copia de seguridad?
programación de copia de seguridad de Hello indica la frecuencia de Hola de operación de copia de seguridad de Hola. Por ejemplo, la configuración de Hola Hola después de la pantalla indica que se realizan las copias de seguridad diariamente a las 6 p.m. y a medianoche.

![Programación diaria](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

Los clientes también pueden programar una copia de seguridad semanal. Por ejemplo, hello configuración Hola después de la pantalla indica que se realizan copias de seguridad cada alternativa el domingo & el miércoles a las 9:30 A.M. y las 1:00 AM.

![Programación semanal](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a>¿Qué es hello directiva de retención?
Directiva de retención de Hello especifica duración hello para el que deben almacenarse copias de seguridad de Hola. En vez de simplemente especificar una "directiva" para todos los puntos de copia de seguridad, los clientes pueden especificar directivas de retención diferente en función de cuando se realizó la copia de seguridad de Hola. Por ejemplo, hello copia de seguridad punto pasado a todos los días, que actúa como un punto de recuperación de las operaciones, se conserva durante 90 días. punto de copia de seguridad de Hello dejó final Hola de cada trimestre para fines de auditoría se conserva durante mucho tiempo.

![Directiva de retención](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

Hello número total de "retención puntos" especificados en esta directiva es 90 (puntos diarios) + 40 (uno para cada trimestre durante 10 años) = 130.

## <a name="example--putting-both-together"></a>Ejemplo: reunir ambos
![Pantalla de ejemplo](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. **Directiva de retención diaria**: las copias de seguridad realizadas diariamente se almacenan durante 7 días.
2. **Directiva de retención semanal**: las copias de seguridad realizadas todos los días a medianoche y el sábado a las 18:00 h se conservan durante 4 semanas.
3. **Directiva de retención mensual**: se conservan las copias de seguridad realizadas a la medianoche y las 6 p.m. en hello último sábado de cada mes durante 12 meses
4. **Directiva de retención anual**: copias de seguridad realizadas a medianoche Hola último sábado de cada marzo se conservan durante 10 años

Hola número total de "puntos de retención" (desde el que un cliente puede restaurar los datos de puntos) en hello diagrama anterior se calcula como sigue:

* 2 puntos por día durante 7 días = 14 puntos de recuperación
* 2 puntos por día durante 4 semanas = 8 puntos de recuperación
* 2 puntos por mes durante 12 meses = 24 puntos de recuperación
* 1 punto por año durante 10 años = 10 puntos de recuperación

número total de Hola de puntos de recuperación es 56.

> [!NOTE]
> La copia de seguridad de Azure no tiene una restricción sobre el número de puntos de recuperación.
>
>

## <a name="advanced-configuration"></a>Configuración avanzada
Haciendo clic en **modificar** Hola delante de la pantalla, los clientes tienen más flexibilidad para especificar programaciones de retención.

![Modificar](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre Azure Backup, vea

* [Introducción tooAzure copia de seguridad](backup-introduction-to-azure-backup.md)
* [Probar Copia de seguridad de Azure](backup-try-azure-backup-in-10-mins.md)
