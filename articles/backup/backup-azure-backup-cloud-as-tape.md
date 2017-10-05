---
title: Uso de Azure Backup para reemplazar la infraestructura de cintas | Microsoft Docs
description: "Aprenda cómo la Copia de seguridad de Microsoft Azure proporciona semántica similar a la cinta que le permite hacer copias de seguridad y restaurar datos en Azure"
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
ms.openlocfilehash: f0f3152daf5f91f7c9e540797bf09b21969d2d33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-your-long-term-storage-from-tape-to-the-azure-cloud"></a><span data-ttu-id="fe88a-103">Traslado del almacenamiento a largo plazo de la cinta a la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="fe88a-103">Move your long-term storage from tape to the Azure cloud</span></span>
<span data-ttu-id="fe88a-104">Los clientes de Copia de seguridad de Microsoft Azure y System Center Data Protection Manager pueden:</span><span class="sxs-lookup"><span data-stu-id="fe88a-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="fe88a-105">Realizar copias de seguridad de datos en las programaciones que mejor se adapten a las necesidades de su organización.</span><span class="sxs-lookup"><span data-stu-id="fe88a-105">Back up data in schedules which best suit the organizational needs.</span></span>
* <span data-ttu-id="fe88a-106">Conservar los datos de copia de seguridad durante períodos más largos.</span><span class="sxs-lookup"><span data-stu-id="fe88a-106">Retain the backup data for longer periods</span></span>
* <span data-ttu-id="fe88a-107">Hacer a Azure partícipe de sus necesidades de retención a largo plazo (en lugar de la cinta).</span><span class="sxs-lookup"><span data-stu-id="fe88a-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="fe88a-108">Este artículo explica cómo los clientes pueden habilitar las directivas de copia de seguridad y retención.</span><span class="sxs-lookup"><span data-stu-id="fe88a-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="fe88a-109">Los clientes que utilicen las cintas para abordar sus necesidades de retención a largo plazo ahora tienen una alternativa viable y eficaz con la disponibilidad de esta característica.</span><span class="sxs-lookup"><span data-stu-id="fe88a-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span></span> <span data-ttu-id="fe88a-110">La característica está habilitada en la versión más reciente de la copia de seguridad de Azure (que está disponible [aquí](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="fe88a-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="fe88a-111">Debe actualizarse a los clientes System Center DPM, como mínimo, DPM 2012 R2 UR5 para usar DPM con el servicio de Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="fe88a-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span></span>

## <a name="what-is-the-backup-schedule"></a><span data-ttu-id="fe88a-112">¿Cuál es la programación de copia de seguridad?</span><span class="sxs-lookup"><span data-stu-id="fe88a-112">What is the Backup Schedule?</span></span>
<span data-ttu-id="fe88a-113">La programación de copia de seguridad indica la frecuencia de la operación de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fe88a-113">The backup schedule indicates the frequency of the backup operation.</span></span> <span data-ttu-id="fe88a-114">Por ejemplo, la configuración de la pantalla siguiente indica que las copias de seguridad se tomarán diariamente a las 18:00 h y a medianoche.</span><span class="sxs-lookup"><span data-stu-id="fe88a-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Programación diaria](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="fe88a-116">Los clientes también pueden programar una copia de seguridad semanal.</span><span class="sxs-lookup"><span data-stu-id="fe88a-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="fe88a-117">Por ejemplo, la configuración de la pantalla siguiente indica que las copias de seguridad se realizarán alternando entre cada domingo y miércoles a las 09:30 h y a la 01: 00 h.</span><span class="sxs-lookup"><span data-stu-id="fe88a-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Programación semanal](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-the-retention-policy"></a><span data-ttu-id="fe88a-119">¿Qué es la directa de retención?</span><span class="sxs-lookup"><span data-stu-id="fe88a-119">What is the Retention Policy?</span></span>
<span data-ttu-id="fe88a-120">La directiva de retención especifica el tiempo durante el que debe almacenarse la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fe88a-120">The retention policy specifies the duration for which the backup must be stored.</span></span> <span data-ttu-id="fe88a-121">En vez de especificar solo una "directiva" para todos los puntos de copia de seguridad, los clientes pueden especificar directivas de retención diferentes en función de cuándo se realizó la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fe88a-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="fe88a-122">Por ejemplo, un punto de copia de seguridad diario (que sirve como punto de recuperación operativo) podría conservarse durante 90 días.</span><span class="sxs-lookup"><span data-stu-id="fe88a-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="fe88a-123">El punto de copia de seguridad realizado al final de cada trimestre con fines de auditoría se conserva durante un período prolongado.</span><span class="sxs-lookup"><span data-stu-id="fe88a-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Directiva de retención](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="fe88a-125">El número total de "puntos de retención" especificado en esta directiva es de 90 (puntos diarios) + 40 (uno cada trimestre durante 10 años) = 130.</span><span class="sxs-lookup"><span data-stu-id="fe88a-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="fe88a-126">Ejemplo: reunir ambos</span><span class="sxs-lookup"><span data-stu-id="fe88a-126">Example – Putting both together</span></span>
![Pantalla de ejemplo](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="fe88a-128">**Directiva de retención diaria**: las copias de seguridad realizadas diariamente se almacenan durante 7 días.</span><span class="sxs-lookup"><span data-stu-id="fe88a-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="fe88a-129">**Directiva de retención semanal**: las copias de seguridad realizadas todos los días a medianoche y el sábado a las 18:00 h se conservan durante 4 semanas.</span><span class="sxs-lookup"><span data-stu-id="fe88a-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="fe88a-130">**Directiva de retención mensual**: las copias de seguridad realizadas a medianoche y a las 18:00 h del último sábado de cada mes se conservarán durante 12 meses.</span><span class="sxs-lookup"><span data-stu-id="fe88a-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="fe88a-131">**Directiva de retención anual**: las copias de seguridad realizadas del último sábado de cada mes de marzo se conservarán durante 10 años.</span><span class="sxs-lookup"><span data-stu-id="fe88a-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="fe88a-132">El número total de "puntos de retención" (desde los que un cliente puede restaurar datos) en el diagrama anterior se calcula de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe88a-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="fe88a-133">2 puntos por día durante 7 días = 14 puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="fe88a-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="fe88a-134">2 puntos por día durante 4 semanas = 8 puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="fe88a-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="fe88a-135">2 puntos por mes durante 12 meses = 24 puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="fe88a-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="fe88a-136">1 punto por año durante 10 años = 10 puntos de recuperación</span><span class="sxs-lookup"><span data-stu-id="fe88a-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="fe88a-137">El número total de puntos de recuperación es 56.</span><span class="sxs-lookup"><span data-stu-id="fe88a-137">The total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="fe88a-138">La copia de seguridad de Azure no tiene una restricción sobre el número de puntos de recuperación.</span><span class="sxs-lookup"><span data-stu-id="fe88a-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="fe88a-139">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="fe88a-139">Advanced configuration</span></span>
<span data-ttu-id="fe88a-140">Al hacer clic en **Modificar** en la pantalla anterior, los clientes tienen más flexibilidad para especificar programaciones de retención.</span><span class="sxs-lookup"><span data-stu-id="fe88a-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Modificar](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="fe88a-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe88a-142">Next Steps</span></span>
<span data-ttu-id="fe88a-143">Para obtener más información sobre Azure Backup, vea</span><span class="sxs-lookup"><span data-stu-id="fe88a-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="fe88a-144">Introducción a la Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="fe88a-144">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="fe88a-145">Probar Copia de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="fe88a-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
