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
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a><span data-ttu-id="32c17-103">Mover el almacenamiento a largo plazo en cinta toohello nube de Azure</span><span class="sxs-lookup"><span data-stu-id="32c17-103">Move your long-term storage from tape toohello Azure cloud</span></span>
<span data-ttu-id="32c17-104">Los clientes de Copia de seguridad de Microsoft Azure y System Center Data Protection Manager pueden:</span><span class="sxs-lookup"><span data-stu-id="32c17-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="32c17-105">Hacer copia de seguridad de los datos en las programaciones que más se ajuste a las necesidades de organización Hola.</span><span class="sxs-lookup"><span data-stu-id="32c17-105">Back up data in schedules which best suit hello organizational needs.</span></span>
* <span data-ttu-id="32c17-106">Conservar los datos de copia de seguridad de Hola durante períodos más largos</span><span class="sxs-lookup"><span data-stu-id="32c17-106">Retain hello backup data for longer periods</span></span>
* <span data-ttu-id="32c17-107">Hacer a Azure partícipe de sus necesidades de retención a largo plazo (en lugar de la cinta).</span><span class="sxs-lookup"><span data-stu-id="32c17-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="32c17-108">Este artículo explica cómo los clientes pueden habilitar las directivas de copia de seguridad y retención.</span><span class="sxs-lookup"><span data-stu-id="32c17-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="32c17-109">Los clientes que usen las cintas tooaddress su largo-duración de retención debe ahora tiene una alternativa viable y eficaz con la disponibilidad de Hola de esta característica.</span><span class="sxs-lookup"><span data-stu-id="32c17-109">Customers who use tapes tooaddress their long-term-retention needs now have a powerful and viable alternative with hello availability of this feature.</span></span> <span data-ttu-id="32c17-110">característica Hello se habilita una en la versión más reciente de Hola de hello copia de seguridad de Azure (que está disponible [aquí](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="32c17-110">hello feature is enabled in hello latest release of hello Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="32c17-111">Los clientes de System Center DPM deben actualizar a, como mínimo, DPM 2012 R2 UR5 antes de usar DPM con Hola servicio de copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="32c17-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with hello Azure Backup service.</span></span>

## <a name="what-is-hello-backup-schedule"></a><span data-ttu-id="32c17-112">¿Qué es hello programación de copia de seguridad?</span><span class="sxs-lookup"><span data-stu-id="32c17-112">What is hello Backup Schedule?</span></span>
<span data-ttu-id="32c17-113">programación de copia de seguridad de Hello indica la frecuencia de Hola de operación de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="32c17-113">hello backup schedule indicates hello frequency of hello backup operation.</span></span> <span data-ttu-id="32c17-114">Por ejemplo, la configuración de Hola Hola después de la pantalla indica que se realizan las copias de seguridad diariamente a las 6 p.m. y a medianoche.</span><span class="sxs-lookup"><span data-stu-id="32c17-114">For example, hello settings in hello following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Programación diaria](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="32c17-116">Los clientes también pueden programar una copia de seguridad semanal.</span><span class="sxs-lookup"><span data-stu-id="32c17-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="32c17-117">Por ejemplo, hello configuración Hola después de la pantalla indica que se realizan copias de seguridad cada alternativa el domingo & el miércoles a las 9:30 A.M. y las 1:00 AM.</span><span class="sxs-lookup"><span data-stu-id="32c17-117">For example, hello settings in hello following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Programación semanal](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a><span data-ttu-id="32c17-119">¿Qué es hello directiva de retención?</span><span class="sxs-lookup"><span data-stu-id="32c17-119">What is hello Retention Policy?</span></span>
<span data-ttu-id="32c17-120">Directiva de retención de Hello especifica duración hello para el que deben almacenarse copias de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="32c17-120">hello retention policy specifies hello duration for which hello backup must be stored.</span></span> <span data-ttu-id="32c17-121">En vez de simplemente especificar una "directiva" para todos los puntos de copia de seguridad, los clientes pueden especificar directivas de retención diferente en función de cuando se realizó la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="32c17-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="32c17-122">Por ejemplo, hello copia de seguridad punto pasado a todos los días, que actúa como un punto de recuperación de las operaciones, se conserva durante 90 días.</span><span class="sxs-lookup"><span data-stu-id="32c17-122">For example, hello backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="32c17-123">punto de copia de seguridad de Hello dejó final Hola de cada trimestre para fines de auditoría se conserva durante mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="32c17-123">hello backup point taken at hello end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Directiva de retención](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="32c17-125">Hello número total de "retención puntos" especificados en esta directiva es 90 (puntos diarios) + 40 (uno para cada trimestre durante 10 años) = 130.</span><span class="sxs-lookup"><span data-stu-id="32c17-125">hello total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="32c17-126">Ejemplo: reunir ambos</span><span class="sxs-lookup"><span data-stu-id="32c17-126">Example – Putting both together</span></span>
![Pantalla de ejemplo](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="32c17-128">**Directiva de retención diaria**: las copias de seguridad realizadas diariamente se almacenan durante 7 días.</span><span class="sxs-lookup"><span data-stu-id="32c17-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="32c17-129">**Directiva de retención semanal**: las copias de seguridad realizadas todos los días a medianoche y el sábado a las 18:00 h se conservan durante 4 semanas.</span><span class="sxs-lookup"><span data-stu-id="32c17-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="32c17-130">**Directiva de retención mensual**: se conservan las copias de seguridad realizadas a la medianoche y las 6 p.m. en hello último sábado de cada mes durante 12 meses</span><span class="sxs-lookup"><span data-stu-id="32c17-130">**Monthly retention policy**: Backups taken at midnight and 6pm on hello last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="32c17-131">**Directiva de retención anual**: copias de seguridad realizadas a medianoche Hola último sábado de cada marzo se conservan durante 10 años</span><span class="sxs-lookup"><span data-stu-id="32c17-131">**Yearly retention policy**: Backups taken at midnight on hello last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="32c17-132">Hola número total de "puntos de retención" (desde el que un cliente puede restaurar los datos de puntos) en hello diagrama anterior se calcula como sigue:</span><span class="sxs-lookup"><span data-stu-id="32c17-132">hello total number of “retention points” (points from which a customer can restore data) in hello preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="32c17-133">2 puntos por día durante 7 días = 14 puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="32c17-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="32c17-134">2 puntos por día durante 4 semanas = 8 puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="32c17-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="32c17-135">2 puntos por mes durante 12 meses = 24 puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="32c17-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="32c17-136">1 punto por año durante 10 años = 10 puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="32c17-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="32c17-137">número total de Hola de puntos de recuperación es 56.</span><span class="sxs-lookup"><span data-stu-id="32c17-137">hello total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="32c17-138">La copia de seguridad de Azure no tiene una restricción sobre el número de puntos de recuperación.</span><span class="sxs-lookup"><span data-stu-id="32c17-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="32c17-139">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="32c17-139">Advanced configuration</span></span>
<span data-ttu-id="32c17-140">Haciendo clic en **modificar** Hola delante de la pantalla, los clientes tienen más flexibilidad para especificar programaciones de retención.</span><span class="sxs-lookup"><span data-stu-id="32c17-140">By clicking **Modify** in hello preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Modificar](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="32c17-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32c17-142">Next Steps</span></span>
<span data-ttu-id="32c17-143">Para obtener más información sobre Azure Backup, vea</span><span class="sxs-lookup"><span data-stu-id="32c17-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="32c17-144">Introducción tooAzure copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="32c17-144">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="32c17-145">Probar Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="32c17-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
