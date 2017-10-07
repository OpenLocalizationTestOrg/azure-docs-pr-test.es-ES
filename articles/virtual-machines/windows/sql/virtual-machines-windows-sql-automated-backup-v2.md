---
title: "aaaAutomated v2 de copia de seguridad de SQL Server 2016 máquinas virtuales de Azure | Documentos de Microsoft"
description: "Explica la característica de copia de seguridad automatizada de Hola para 2016 VM de SQL Server que se ejecuta en Azure. Este artículo es específico tooVMs mediante Hola, Administrador de recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="0a312-104">Copia de seguridad automatizada v2 para Azure Virtual Machines con SQL Server 2016 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="0a312-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a312-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="0a312-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="0a312-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="0a312-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="0a312-107">V2 de copia de seguridad automatizada configura automáticamente [tooMicrosoft de copia de seguridad administrada Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todas las bases de datos nuevas y existentes en una VM de Azure que ejecutan las ediciones de SQL Server 2016 Standard, Enterprise o Developer.</span><span class="sxs-lookup"><span data-stu-id="0a312-107">Automated Backup v2 automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="0a312-108">Esto le permite las copias de seguridad de base de datos normal de tooconfigure que utilizan el almacenamiento de blobs de Azure duradero.</span><span class="sxs-lookup"><span data-stu-id="0a312-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="0a312-109">V2 de copia de seguridad automatizada depende de hello [extensión del agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0a312-109">Automated Backup v2 depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="0a312-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0a312-110">Prerequisites</span></span>
<span data-ttu-id="0a312-111">toouse v2 de copia de seguridad automatizada, revise Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="0a312-111">toouse Automated Backup v2, review hello following prerequisites:</span></span>

<span data-ttu-id="0a312-112">**Sistema operativo**:</span><span class="sxs-lookup"><span data-stu-id="0a312-112">**Operating System**:</span></span>

- <span data-ttu-id="0a312-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0a312-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="0a312-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0a312-114">Windows Server 2016</span></span>

<span data-ttu-id="0a312-115">**Edición/versión de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="0a312-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="0a312-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="0a312-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="0a312-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="0a312-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="0a312-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="0a312-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a312-119">Copia de seguridad automatizada v2 funciona con SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0a312-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="0a312-120">Si está usando SQL Server 2014, puede usar copia de seguridad automatizada v1 tooback seguridad de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="0a312-120">If you are using SQL Server 2014, you can use Automated Backup v1 tooback up your databases.</span></span> <span data-ttu-id="0a312-121">Para obtener más información, vea [Copia de seguridad automatizada para SQL Server 2014 en Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="0a312-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="0a312-122">**Configuración de base de datos**:</span><span class="sxs-lookup"><span data-stu-id="0a312-122">**Database configuration**:</span></span>

- <span data-ttu-id="0a312-123">Las bases de datos de destino deben usar el modelo de recuperación completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="0a312-124">Para obtener más información sobre las repercusiones de Hola Hola completa del modelo de recuperación en copias de seguridad, consulte [Hola de copia de seguridad en el modelo de recuperación completa](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a312-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="0a312-125">Las bases de datos del sistema no tiene toouse modelo de recuperación completa.</span><span class="sxs-lookup"><span data-stu-id="0a312-125">System databases do not have toouse full recovery model.</span></span> <span data-ttu-id="0a312-126">Sin embargo, si necesita toobe de copias de seguridad del registro de modelo o MSDB, debe usar el modelo de recuperación completa.</span><span class="sxs-lookup"><span data-stu-id="0a312-126">However, if you require log backups toobe taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="0a312-127">Las bases de datos de destino deben estar en la instancia de SQL Server predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-127">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="0a312-128">Hola extensión de IaaS de SQL Server no admite instancias con nombre.</span><span class="sxs-lookup"><span data-stu-id="0a312-128">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="0a312-129">**Modelo de implementación de Azure**:</span><span class="sxs-lookup"><span data-stu-id="0a312-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="0a312-130">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0a312-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="0a312-131">Copia de seguridad automatizada se basa en hello **extensión del agente de IaaS de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0a312-131">Automated Backup relies on hello **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="0a312-132">Las imágenes actuales de la galería de máquinas virtuales de SQL agregan esta extensión de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0a312-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="0a312-133">Para más información, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0a312-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="0a312-134">Settings</span><span class="sxs-lookup"><span data-stu-id="0a312-134">Settings</span></span>
<span data-ttu-id="0a312-135">Hello siguiente tabla describe las opciones de Hola que se pueden configurar para copia de seguridad automatizada v2.</span><span class="sxs-lookup"><span data-stu-id="0a312-135">hello following table describes hello options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="0a312-136">pasos de configuración real de Hello varían dependiendo de si utiliza Hola portal de Azure o comandos de PowerShell de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="0a312-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="0a312-137">Configuración básica</span><span class="sxs-lookup"><span data-stu-id="0a312-137">Basic Settings</span></span>

| <span data-ttu-id="0a312-138">Configuración</span><span class="sxs-lookup"><span data-stu-id="0a312-138">Setting</span></span> | <span data-ttu-id="0a312-139">Intervalo (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="0a312-139">Range (Default)</span></span> | <span data-ttu-id="0a312-140">Descripción</span><span class="sxs-lookup"><span data-stu-id="0a312-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0a312-141">**Copia de seguridad automatizada**</span><span class="sxs-lookup"><span data-stu-id="0a312-141">**Automated Backup**</span></span> | <span data-ttu-id="0a312-142">Habilitar/deshabilitar (deshabilitado)</span><span class="sxs-lookup"><span data-stu-id="0a312-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="0a312-143">Habilita o deshabilita la copia de seguridad automatizada para una VM de Azure que ejecuta SQL Server 2016 Standard o Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0a312-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="0a312-144">**Período de retención**</span><span class="sxs-lookup"><span data-stu-id="0a312-144">**Retention Period**</span></span> | <span data-ttu-id="0a312-145">1-30 días (30 días)</span><span class="sxs-lookup"><span data-stu-id="0a312-145">1-30 days (30 days)</span></span> | <span data-ttu-id="0a312-146">número de Hola de copias de seguridad de tooretain días.</span><span class="sxs-lookup"><span data-stu-id="0a312-146">hello number of days tooretain backups.</span></span> |
| <span data-ttu-id="0a312-147">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="0a312-147">**Storage Account**</span></span> | <span data-ttu-id="0a312-148">Cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="0a312-148">Azure storage account</span></span> | <span data-ttu-id="0a312-149">Un toouse de la cuenta de almacenamiento de Azure para almacenar los archivos de copia de seguridad automatizada en almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="0a312-149">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="0a312-150">Se crea un contenedor en esta ubicación toostore todos los archivos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0a312-150">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="0a312-151">archivo de copia de seguridad de Hello convención de nomenclatura incluye Hola fecha, hora y GUID de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="0a312-151">hello backup file naming convention includes hello date, time, and database GUID.</span></span> |
| <span data-ttu-id="0a312-152">**Cifrado**</span><span class="sxs-lookup"><span data-stu-id="0a312-152">**Encryption**</span></span> |<span data-ttu-id="0a312-153">Habilitar/deshabilitar (deshabilitado)</span><span class="sxs-lookup"><span data-stu-id="0a312-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="0a312-154">Habilita o deshabilita el cifrado.</span><span class="sxs-lookup"><span data-stu-id="0a312-154">Enables or disables encryption.</span></span> <span data-ttu-id="0a312-155">Cuando está habilitado el cifrado, copia de seguridad de hello certificados usados toorestore Hola se encuentran en hello especificado cuenta de almacenamiento en hello mismo **automaticbackup** contenedor mediante Hola la misma convención de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="0a312-155">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same **automaticbackup** container using hello same naming convention.</span></span> <span data-ttu-id="0a312-156">Si cambia la contraseña de hello, se genera un nuevo certificado con esa contraseña, pero los certificados antiguos Hola permanecen toorestore copias de seguridad anteriores.</span><span class="sxs-lookup"><span data-stu-id="0a312-156">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="0a312-157">**Password**</span><span class="sxs-lookup"><span data-stu-id="0a312-157">**Password**</span></span> |<span data-ttu-id="0a312-158">Texto de contraseña</span><span class="sxs-lookup"><span data-stu-id="0a312-158">Password text</span></span> | <span data-ttu-id="0a312-159">Una contraseña para claves de cifrado.</span><span class="sxs-lookup"><span data-stu-id="0a312-159">A password for encryption keys.</span></span> <span data-ttu-id="0a312-160">Esto solo es necesario si se habilita el cifrado.</span><span class="sxs-lookup"><span data-stu-id="0a312-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="0a312-161">En orden toorestore una copia de seguridad cifrada, debe tener contraseña correcta de Hola y el certificado relacionado que se usaron en tiempo de Hola se realizó la copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-161">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="0a312-162">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="0a312-162">Advanced Settings</span></span>

| <span data-ttu-id="0a312-163">Configuración</span><span class="sxs-lookup"><span data-stu-id="0a312-163">Setting</span></span> | <span data-ttu-id="0a312-164">Intervalo (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="0a312-164">Range (Default)</span></span> | <span data-ttu-id="0a312-165">Descripción</span><span class="sxs-lookup"><span data-stu-id="0a312-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0a312-166">**Copias de seguridad de bases de datos del sistema**</span><span class="sxs-lookup"><span data-stu-id="0a312-166">**System Database Backups**</span></span> | <span data-ttu-id="0a312-167">Habilitar/deshabilitar (deshabilitado)</span><span class="sxs-lookup"><span data-stu-id="0a312-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="0a312-168">Cuando se habilita, esta característica realizará también una copia de bases de datos de hello sistema: Master, MSDB y Model.</span><span class="sxs-lookup"><span data-stu-id="0a312-168">When enabled, this feature will also back up hello system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="0a312-169">Hello MSDB y las bases de datos de modelo, compruebe que están en modo de recuperación completa si desea toobe de copias de seguridad de registro realizada.</span><span class="sxs-lookup"><span data-stu-id="0a312-169">For hello MSDB and Model databases, verify that they are in full recovery mode if you want log backups toobe taken.</span></span> <span data-ttu-id="0a312-170">Nunca se realizan copias de seguridad de registros para las bases de datos maestras.</span><span class="sxs-lookup"><span data-stu-id="0a312-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="0a312-171">Tampoco se realizan copias de seguridad para TempDB.</span><span class="sxs-lookup"><span data-stu-id="0a312-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="0a312-172">**Programación de copia de seguridad**</span><span class="sxs-lookup"><span data-stu-id="0a312-172">**Backup Schedule**</span></span> | <span data-ttu-id="0a312-173">Manual/Automatizado (Automatizado)</span><span class="sxs-lookup"><span data-stu-id="0a312-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="0a312-174">De forma predeterminada, programación de copia de seguridad de Hola se determinará automáticamente en función de crecimiento del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="0a312-174">By default, hello backup schedule will be automatically determined based on hello log growth.</span></span> <span data-ttu-id="0a312-175">Programación de copia de seguridad manual permite período de tiempo de hello usuario toospecify Hola para copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0a312-175">Manual backup schedule allows hello user toospecify hello time window for backups.</span></span> <span data-ttu-id="0a312-176">En este caso, las copias de seguridad siempre tendrá lugar en hello especifica la frecuencia y Hola durante el período de tiempo de un día determinado.</span><span class="sxs-lookup"><span data-stu-id="0a312-176">In this case, backups will only ever take place at hello specified frequency and during hello specified time window of a given day.</span></span> |
| <span data-ttu-id="0a312-177">**Frecuencia de copia de seguridad completa**</span><span class="sxs-lookup"><span data-stu-id="0a312-177">**Full backup frequency**</span></span> | <span data-ttu-id="0a312-178">Diariamente/semanalmente</span><span class="sxs-lookup"><span data-stu-id="0a312-178">Daily/Weekly</span></span> | <span data-ttu-id="0a312-179">Frecuencia de las copias de seguridad completas.</span><span class="sxs-lookup"><span data-stu-id="0a312-179">Frequency of full backups.</span></span> <span data-ttu-id="0a312-180">En ambos casos, copias de seguridad completas se inician durante la ventana de hello siguiente hora programada.</span><span class="sxs-lookup"><span data-stu-id="0a312-180">In both cases, full backups will begin during hello next scheduled time window.</span></span> <span data-ttu-id="0a312-181">Cuando se selecciona semanalmente, las copias de seguridad pueden extenderse varios días hasta que se realizan correctamente las copias de seguridad de todas las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="0a312-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="0a312-182">**Hora de inicio de copia de seguridad completa**</span><span class="sxs-lookup"><span data-stu-id="0a312-182">**Full backup start time**</span></span> | <span data-ttu-id="0a312-183">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="0a312-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="0a312-184">Hora de inicio de un día determinado durante el cual se pueden realizar copias de seguridad completas.</span><span class="sxs-lookup"><span data-stu-id="0a312-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="0a312-185">**Período de tiempo de copia de seguridad completa**</span><span class="sxs-lookup"><span data-stu-id="0a312-185">**Full backup time window**</span></span> | <span data-ttu-id="0a312-186">1-23 horas (1 hora)</span><span class="sxs-lookup"><span data-stu-id="0a312-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="0a312-187">Duración del período de tiempo de Hola de un día determinado durante el cual pueden realizar copias de seguridad completas.</span><span class="sxs-lookup"><span data-stu-id="0a312-187">Duration of hello time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="0a312-188">**Frecuencia de copia de seguridad de registros**</span><span class="sxs-lookup"><span data-stu-id="0a312-188">**Log backup frequency**</span></span> | <span data-ttu-id="0a312-189">5-60 minutos (60 minutos)</span><span class="sxs-lookup"><span data-stu-id="0a312-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="0a312-190">Frecuencia de las copias de seguridad de registros.</span><span class="sxs-lookup"><span data-stu-id="0a312-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="0a312-191">Información de la frecuencia de copia de seguridad completa</span><span class="sxs-lookup"><span data-stu-id="0a312-191">Understanding full backup frequency</span></span>
<span data-ttu-id="0a312-192">Es importante toounderstand Hola diferencia entre copias de seguridad completas diarias y semanales.</span><span class="sxs-lookup"><span data-stu-id="0a312-192">It is important toounderstand hello difference between daily and weekly full backups.</span></span> <span data-ttu-id="0a312-193">Para ello, se le guiará a través de dos escenarios de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0a312-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="0a312-194">Escenario 1: Copias de seguridad semanales</span><span class="sxs-lookup"><span data-stu-id="0a312-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="0a312-195">Tiene una VM con SQL Server que contiene un número de bases de datos muy grandes.</span><span class="sxs-lookup"><span data-stu-id="0a312-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="0a312-196">El lunes, se habilita la copia de seguridad automatizada v2 con hello después de configuración:</span><span class="sxs-lookup"><span data-stu-id="0a312-196">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="0a312-197">Programación de copia de seguridad: **Manual**</span><span class="sxs-lookup"><span data-stu-id="0a312-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="0a312-198">Frecuencia de copia de seguridad completa: **Semanal**</span><span class="sxs-lookup"><span data-stu-id="0a312-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="0a312-199">Hora de inicio de copia de seguridad completa: **01:00**</span><span class="sxs-lookup"><span data-stu-id="0a312-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="0a312-200">Período de tiempo de copia de seguridad completa: **1 hora**</span><span class="sxs-lookup"><span data-stu-id="0a312-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="0a312-201">Esto significa que esa ventana de copia de seguridad de disponible siguiente de hello es el martes a la 1 A.M. durante una hora.</span><span class="sxs-lookup"><span data-stu-id="0a312-201">This means that hello next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="0a312-202">En ese momento, la copia de seguridad empieza a realizar copias de seguridad de las bases de datos una a una.</span><span class="sxs-lookup"><span data-stu-id="0a312-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="0a312-203">En este escenario, las bases de datos son lo suficientemente grandes como para que se completarán copias de seguridad completas de bases de datos primera par Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-203">In this scenario, your databases are large enough that full backups will complete for hello first couple databases.</span></span> <span data-ttu-id="0a312-204">Sin embargo, después de una hora no todas las bases de datos de hello todavía ha realizado ninguna.</span><span class="sxs-lookup"><span data-stu-id="0a312-204">However, after one hour not all of hello databases have been backed up.</span></span>

<span data-ttu-id="0a312-205">Cuando esto sucede, copia de seguridad automatizada comenzará la copia de seguridad de hello restantes Hola de bases de datos día siguiente, el miércoles a la 1 A.M. durante una hora.</span><span class="sxs-lookup"><span data-stu-id="0a312-205">When this happens, Automated Backup will begin backing up hello remaining databases hello next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="0a312-206">Si no todas las bases de datos se ha hecho en ese momento, lo intentará de nuevo Hola día siguiente en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="0a312-206">If not all databases have been backed up in that time, it will try again hello next day at hello same time.</span></span> <span data-ttu-id="0a312-207">Se aplica este mismo comportamiento hasta que se realiza correctamente la copia de seguridad de todas las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="0a312-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="0a312-208">Cuando vuelve a llegar el martes, la copia de seguridad automatizada empieza de nuevo a realizar la copia de seguridad de todas las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="0a312-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="0a312-209">Este escenario muestra que la copia de seguridad automatizada solo funcionará en el período de tiempo especificado de Hola y cada base de datos se copiarán una vez por semana.</span><span class="sxs-lookup"><span data-stu-id="0a312-209">This scenario shows that Automated Backup will only operate within hello specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="0a312-210">Esto también muestra que es posible para las copias de seguridad toospan varios días en hello caso donde no es posible toocomplete todas las copias de seguridad en un solo día.</span><span class="sxs-lookup"><span data-stu-id="0a312-210">This also shows that it is possible for backups toospan multiple days in hello case where it is not possible toocomplete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="0a312-211">Escenario 2: Copias de seguridad diarias</span><span class="sxs-lookup"><span data-stu-id="0a312-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="0a312-212">Tiene una VM con SQL Server que contiene un número de bases de datos muy grandes.</span><span class="sxs-lookup"><span data-stu-id="0a312-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="0a312-213">El lunes, se habilita la copia de seguridad automatizada v2 con hello después de configuración:</span><span class="sxs-lookup"><span data-stu-id="0a312-213">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="0a312-214">Programación de copia de seguridad: Manual</span><span class="sxs-lookup"><span data-stu-id="0a312-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="0a312-215">Frecuencia de copia de seguridad completa: Diaria</span><span class="sxs-lookup"><span data-stu-id="0a312-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="0a312-216">Hora de inicio de copia de seguridad completa: 22:00</span><span class="sxs-lookup"><span data-stu-id="0a312-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="0a312-217">Período de tiempo de copia de seguridad completa: 6 horas</span><span class="sxs-lookup"><span data-stu-id="0a312-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="0a312-218">Esto significa que esa ventana de copia de seguridad de disponible siguiente de hello es el lunes a las 10 P.M. durante 6 horas.</span><span class="sxs-lookup"><span data-stu-id="0a312-218">This means that hello next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="0a312-219">En ese momento, la copia de seguridad empieza a realizar copias de seguridad de las bases de datos una a una.</span><span class="sxs-lookup"><span data-stu-id="0a312-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="0a312-220">Posteriormente, se vuelve a realizar la copia de seguridad completa de todas las bases de datos el martes a las 22:00 horas durante seis horas.</span><span class="sxs-lookup"><span data-stu-id="0a312-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a312-221">Al programar copias de seguridad diarias, se recomienda que programe un tooensure de ventana de tiempo de ampliación todas las bases de datos pueden se copia en este momento.</span><span class="sxs-lookup"><span data-stu-id="0a312-221">When scheduling daily backups, it is recommended that you schedule a wide time window tooensure all databases can be backed up within this time.</span></span> <span data-ttu-id="0a312-222">Esto es especialmente importante en caso de hello donde haya una gran cantidad de datos tooback seguridad.</span><span class="sxs-lookup"><span data-stu-id="0a312-222">This is especially important in hello case where you have a large amount of data tooback up.</span></span>

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="0a312-223">Configuración de hello Portal</span><span class="sxs-lookup"><span data-stu-id="0a312-223">Configuration in hello Portal</span></span>

<span data-ttu-id="0a312-224">Puede usar hello tooconfigure portal Azure copia de seguridad automatizada v2 durante el aprovisionamiento o para SQL Server 2016 las máquinas virtuales existentes.</span><span class="sxs-lookup"><span data-stu-id="0a312-224">You can use hello Azure portal tooconfigure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="0a312-225">Nuevas máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="0a312-225">New VMs</span></span>

<span data-ttu-id="0a312-226">Utilice hello tooconfigure portal Azure copia de seguridad automatizada v2 cuando se crea una nueva máquina Virtual de SQL Server 2016 en el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-226">Use hello Azure portal tooconfigure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="0a312-227">Hola **configuración de SQL Server** hoja, seleccione **copia de seguridad automatizada**.</span><span class="sxs-lookup"><span data-stu-id="0a312-227">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="0a312-228">Hello siguiente captura de pantalla de portal Azure muestra hello **copia de seguridad automatizada de SQL** hoja.</span><span class="sxs-lookup"><span data-stu-id="0a312-228">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Configuración de Copia de seguridad automatizada de SQL en Azure Portal](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="0a312-230">Copia de seguridad automatizada v2 está deshabilitada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0a312-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="0a312-231">Para el contexto, vea el tema completo de hello en [aprovisionar una máquina virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="0a312-231">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="0a312-232">Máquinas virtuales existentes</span><span class="sxs-lookup"><span data-stu-id="0a312-232">Existing VMs</span></span>

<span data-ttu-id="0a312-233">Para las máquinas virtuales de SQL Server existentes, seleccione su máquina virtual de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a312-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="0a312-234">A continuación, seleccione hello **configuración de SQL Server** sección de hello **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="0a312-234">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Copia de seguridad automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="0a312-236">Hola **configuración de SQL Server** hoja, haga clic en hello **editar** botón Hola automatizada sección copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0a312-236">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Configuración de Copia de seguridad automatizada de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="0a312-238">Cuando termine, haga clic en hello **Aceptar** botón en la parte inferior de Hola de hello **configuración de SQL Server** toosave hoja los cambios.</span><span class="sxs-lookup"><span data-stu-id="0a312-238">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="0a312-239">Si va a habilitar copia de seguridad automatizada para hello primera vez, Azure configura Hola agente de IaaS de SQL Server en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-239">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="0a312-240">Durante este tiempo, Hola portal de Azure es posible que no muestre que está configurada la copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="0a312-240">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="0a312-241">Espere unos minutos para hello toobe de agente instalado, configurado.</span><span class="sxs-lookup"><span data-stu-id="0a312-241">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="0a312-242">Después de ese hello Azure portal reflejará nueva configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-242">After that hello Azure portal will reflect hello new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="0a312-243">Configuración con PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a312-243">Configuration with PowerShell</span></span>

<span data-ttu-id="0a312-244">Puede usar PowerShell tooconfigure v2 de copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="0a312-244">You can use PowerShell tooconfigure Automated Backup v2.</span></span> <span data-ttu-id="0a312-245">Antes de comenzar:</span><span class="sxs-lookup"><span data-stu-id="0a312-245">Before you begin, you must:</span></span>

- <span data-ttu-id="0a312-246">[Descargue e instale Hola más reciente de PowerShell de Azure](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="0a312-246">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="0a312-247">Abra Windows PowerShell y asócielo con su cuenta.</span><span class="sxs-lookup"><span data-stu-id="0a312-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="0a312-248">Puede hacerlo siguiendo los pasos de Hola Hola [configurar su suscripción](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sección de hello aprovisionamiento tema.</span><span class="sxs-lookup"><span data-stu-id="0a312-248">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="0a312-249">Instalar Hola extensión de IaaS de SQL</span><span class="sxs-lookup"><span data-stu-id="0a312-249">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="0a312-250">Si se aprovisiona una máquina virtual de SQL Server de hello portal de Azure, ya debe instalarse Hola extensión de IaaS de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a312-250">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="0a312-251">Puede determinar si se instaló para la máquina virtual mediante una llamada a **Get AzureRmVM** comando y el examen de hello **extensiones** propiedad.</span><span class="sxs-lookup"><span data-stu-id="0a312-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="0a312-252">Si Hola extensión del agente de IaaS de SQL Server está instalado, verá que aparece como "SqlIaaSAgent" o "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="0a312-252">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="0a312-253">**Estado de aprovisionamiento** para extensión de hello también debería mostrar "Correcto".</span><span class="sxs-lookup"><span data-stu-id="0a312-253">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="0a312-254">Si no está instalado o no se pudo toobe aprovisionado, puede instalarlo con el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-254">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="0a312-255">En suma toohello VM nombre del grupo de recursos, también debe especificar la región de hello (**$region**) que la máquina virtual se encuentra en.</span><span class="sxs-lookup"><span data-stu-id="0a312-255">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="0a312-256"><a id="verifysettings"></a> Verificación de la configuración actual</span><span class="sxs-lookup"><span data-stu-id="0a312-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="0a312-257">Si habilita la copia de seguridad automatizada durante el aprovisionamiento, puede usar PowerShell toocheck la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="0a312-257">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="0a312-258">Ejecute hello **Get AzureRmVMSqlServerExtension** comando y examine hello **AutoBackupSettings** propiedad:</span><span class="sxs-lookup"><span data-stu-id="0a312-258">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="0a312-259">Debería obtener siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="0a312-259">You should get output similar toohello following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="0a312-260">Si el resultado muestra que **habilitar** se establece demasiado**False**, tendrá que tooenable la copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="0a312-260">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="0a312-261">Hello buenas noticias son que habilitar y configurar la copia de seguridad automatizada en hello igual.</span><span class="sxs-lookup"><span data-stu-id="0a312-261">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="0a312-262">Consulte la sección siguiente de hello esta información.</span><span class="sxs-lookup"><span data-stu-id="0a312-262">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="0a312-263">Si comprobar la configuración de hello inmediatamente después de realizar un cambio, es posible que se pondrá en contacto valores de configuración anteriores Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-263">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="0a312-264">Espere unos minutos y compruebe la configuración de hello nuevo toomake seguro de que se han aplicado los cambios.</span><span class="sxs-lookup"><span data-stu-id="0a312-264">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="0a312-265">Configuración de Copia de seguridad automatizada v2</span><span class="sxs-lookup"><span data-stu-id="0a312-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="0a312-266">Puede usar PowerShell tooenable copia de seguridad automatizada, así como toomodify su configuración y el comportamiento en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="0a312-266">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="0a312-267">En primer lugar, seleccione o cree una cuenta de almacenamiento para hello archivos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0a312-267">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="0a312-268">Hello secuencia de comandos siguiente selecciona una cuenta de almacenamiento o lo crea si no existe.</span><span class="sxs-lookup"><span data-stu-id="0a312-268">hello following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> <span data-ttu-id="0a312-269">Copia de seguridad automatizada no permite almacenar las copias de seguridad en Premium Storage, pero pueden realizar copias de seguridad de discos de VM que usan Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="0a312-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="0a312-270">A continuación, usar hello **New-AzureRmVMSqlServerAutoBackupConfig** tooenable de comandos y configurar las copias de seguridad de copia de seguridad automatizada v2 Hola configuración toostore en la cuenta de almacenamiento de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-270">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup v2 settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="0a312-271">En este ejemplo, las copias de seguridad de Hola se establecen toobe conserva de 10 días.</span><span class="sxs-lookup"><span data-stu-id="0a312-271">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="0a312-272">Las copias de seguridad de las bases de datos del sistema están habilitadas.</span><span class="sxs-lookup"><span data-stu-id="0a312-272">System database backups are enabled.</span></span> <span data-ttu-id="0a312-273">Las copias de seguridad completas están programadas semanalmente con un período de tiempo que empieza a las 20:00 horas y dura dos horas.</span><span class="sxs-lookup"><span data-stu-id="0a312-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="0a312-274">Las copias de seguridad de registros están programadas para que se realicen cada 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="0a312-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="0a312-275">Hola segundo comando **AzureRmVMSqlServerExtension conjunto**, Hola actualizaciones especificado VM de Azure con esta configuración.</span><span class="sxs-lookup"><span data-stu-id="0a312-275">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="0a312-276">Podría tardar varios tooinstall minutos y configure Hola agente de IaaS de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a312-276">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="0a312-277">cifrado de tooenable, modificar Hola Hola de toopass de secuencia de comandos anterior **EnableEncryption** parámetro junto con una contraseña (cadena segura) para hello **CertificatePassword** parámetro.</span><span class="sxs-lookup"><span data-stu-id="0a312-277">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="0a312-278">Hola siguiente script habilita la configuración de copia de seguridad automatizada de hello en el ejemplo anterior de Hola y agrega el cifrado.</span><span class="sxs-lookup"><span data-stu-id="0a312-278">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="0a312-279">tooconfirm su configuración se aplica, [comprobar la configuración de copia de seguridad automatizada de hello](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="0a312-279">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="0a312-280">Deshabilitar Copia de seguridad automatizada</span><span class="sxs-lookup"><span data-stu-id="0a312-280">Disable Automated Backup</span></span>
<span data-ttu-id="0a312-281">toodisable copia de seguridad automatizada, ejecución Hola mismo script sin hello **-habilitar** parámetro toohello **AzureRmVMSqlServerAutoBackupConfig New** comando.</span><span class="sxs-lookup"><span data-stu-id="0a312-281">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="0a312-282">Hola ausencia de hello **-habilitar** característica de parámetro señales Hola comando toodisable Hola.</span><span class="sxs-lookup"><span data-stu-id="0a312-282">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="0a312-283">Al igual que con la instalación, puede tardar varios minutos toodisable copia de seguridad automatizada.</span><span class="sxs-lookup"><span data-stu-id="0a312-283">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="0a312-284">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0a312-284">Example script</span></span>
<span data-ttu-id="0a312-285">Hello siguiente script proporciona un conjunto de variables que puede personalizar tooenable y configurar copia de seguridad automatizada para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0a312-285">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="0a312-286">En su caso, tendrá que secuencia de comandos de toocustomize Hola según sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="0a312-286">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="0a312-287">Por ejemplo, podría tener cambios toomake si deseara copia de seguridad de toodisable Hola de bases de datos del sistema o habilitar el cifrado.</span><span class="sxs-lookup"><span data-stu-id="0a312-287">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="0a312-288">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a312-288">Next steps</span></span>
<span data-ttu-id="0a312-289">Copia de seguridad automatizada v2 configura Copia de seguridad administrada en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a312-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="0a312-290">Por lo que es importante[revisar la documentación de Hola para copia de seguridad administrada](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hola comportamiento e implicaciones.</span><span class="sxs-lookup"><span data-stu-id="0a312-290">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="0a312-291">Puede encontrar la copia de seguridad adicional y restaurar guía para SQL Server en máquinas virtuales de Azure en hello tema siguiente: [de copia de seguridad y restauración para SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="0a312-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="0a312-292">Para más información acerca de otras tareas de automatización disponibles, consulte la [extensión Agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0a312-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="0a312-293">Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Azure, consulte [Introducción a SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a312-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

