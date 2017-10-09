---
title: aaaInstall v2 del servidor de copia de seguridad de Azure | Documentos de Microsoft
description: "Azure Backup Server v2 proporciona funciones mejoradas de copia de seguridad para proteger máquinas virtuales, archivos, carpetas, cargas de trabajo, etc. Obtenga información acerca de cómo actualizar o tooinstall tooAzure v2 del servidor de copia de seguridad."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="81d26-104">Instalar Azure Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="81d26-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="81d26-105">Azure Backup Server ayuda a proteger máquinas virtuales (VM), cargas de trabajo, archivos, carpetas, etc.</span><span class="sxs-lookup"><span data-stu-id="81d26-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="81d26-106">Azure Backup Server v2 se basa en Azure Backup Server v1 y proporciona características nuevas que no están disponibles en la versión v1.</span><span class="sxs-lookup"><span data-stu-id="81d26-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="81d26-107">Para obtener una comparación de las características de v1 y v2, vea [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md) (Matriz de protección de Azure Backup Server).</span><span class="sxs-lookup"><span data-stu-id="81d26-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="81d26-108">características adicionales de Hello en el servidor de copia de seguridad v2 son una actualización de servidor de copia de seguridad v1.</span><span class="sxs-lookup"><span data-stu-id="81d26-108">hello additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="81d26-109">A pesar de ello, no es un requisito previo disponer de Backup Server v1 para instalar Backup Server v2.</span><span class="sxs-lookup"><span data-stu-id="81d26-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="81d26-110">Si desea tooupgrade desde el servidor de copia de seguridad v1 tooBackup v2 de servidor, instale v2 del servidor de copia de seguridad en servidor de protección del servidor de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-110">If you want tooupgrade from Backup Server v1 tooBackup Server v2, install Backup Server v2 on hello Backup Server protection server.</span></span> <span data-ttu-id="81d26-111">La configuración existente de Backup Server permanecerá intacta.</span><span class="sxs-lookup"><span data-stu-id="81d26-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="81d26-112">Puede instalar Backup Server v2 en Windows Server 2012 R2 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="81d26-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="81d26-113">tootake las nuevas características, como moderno copia de seguridad de almacenamiento de System Center 2016 datos Protection Manager, debe instalar el servidor de copia de seguridad v2 en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="81d26-113">tootake advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="81d26-114">Antes de actualizar tooor install v2 del servidor de copia de seguridad, que conozca hello [requisitos previos de instalación](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="81d26-114">Before you upgrade tooor install Backup Server v2, read about hello [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="81d26-115">Servidor de copia de seguridad de Azure tiene Hola mismo código base como System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="81d26-115">Azure Backup Server has hello same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="81d26-116">Copia de seguridad v1 de servidor es equivalente tooData Protection Manager 2012 R2 y v2 del servidor de copia de seguridad es equivalente tooData Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="81d26-116">Backup Server v1 is equivalent tooData Protection Manager 2012 R2, and Backup Server v2 is equivalent tooData Protection Manager 2016.</span></span> <span data-ttu-id="81d26-117">En ocasiones, este artículo hace referencia a documentación de Data Protection Manager Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-117">This article occasionally references hello Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-toov2"></a><span data-ttu-id="81d26-118">Actualizar toov2 de copia de seguridad de servidor</span><span class="sxs-lookup"><span data-stu-id="81d26-118">Upgrade Backup Server toov2</span></span>
<span data-ttu-id="81d26-119">tooupgrade desde el servidor de copia de seguridad v1 tooBackup v2 de servidor, asegúrese de que la instalación tiene las actualizaciones de hello necesario:</span><span class="sxs-lookup"><span data-stu-id="81d26-119">tooupgrade from Backup Server v1 tooBackup Server v2, make sure your installation has hello required updates:</span></span>

- <span data-ttu-id="81d26-120">[Actualizar agentes de protección de hello](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) en Hola de servidores protegidos.</span><span class="sxs-lookup"><span data-stu-id="81d26-120">[Update hello protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on hello protected servers.</span></span>
- <span data-ttu-id="81d26-121">Actualizar Windows Server 2012 R2 tooWindows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="81d26-121">Upgrade Windows Server 2012 R2 tooWindows Server 2016.</span></span>
- <span data-ttu-id="81d26-122">Actualice Remote Administrator de Azure Backup Server en todos los servidores de producción.</span><span class="sxs-lookup"><span data-stu-id="81d26-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="81d26-123">Asegúrese de que las copias de seguridad se establecen toocontinue sin necesidad de reiniciar el servidor de producción.</span><span class="sxs-lookup"><span data-stu-id="81d26-123">Ensure that backups are set toocontinue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="81d26-124">Pasos para actualizar a Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="81d26-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="81d26-125">En el centro de descarga, hello [Descargue el instalador de actualización de hello](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="81d26-125">In hello Download Center, [download hello upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="81d26-126">Después de extraer el Asistente para la instalación de hello, asegúrese de que **ejecutar setup.exe** está seleccionada y, a continuación, seleccione **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-126">After you extract hello setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Instalador: ejecutar el programa de instalación](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="81d26-128">En el Asistente para servidor de copia de seguridad de Microsoft Azure de hello, en **instalar**, seleccione **servidor de copia de seguridad de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="81d26-128">In hello Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Instalador: seleccionar la instalación](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="81d26-130">En hello **bienvenida** página, revise las advertencias de hello y, a continuación, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="81d26-130">On hello **Welcome** page, review hello warnings, and then select **Next**.</span></span>

  ![Instalador: página principal](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="81d26-132">Asistente para la instalación de Hello realiza comprobaciones de requisitos previos toomake seguro que puede actualizar el entorno.</span><span class="sxs-lookup"><span data-stu-id="81d26-132">hello setup wizard performs prerequisite checks toomake sure your environment can upgrade.</span></span> <span data-ttu-id="81d26-133">En hello **Prerequisite Checks** página, seleccione **comprobar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-133">On hello **Prerequisite Checks** page, select **Check**.</span></span>

  ![Instalador: página Comprobaciones de requisitos previos](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="81d26-135">El entorno debe pasar comprobaciones de requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-135">Your environment must pass hello prerequisite checks.</span></span> <span data-ttu-id="81d26-136">Si su entorno no superan las comprobaciones de hello, tenga en cuenta los problemas de Hola y corregirlos.</span><span class="sxs-lookup"><span data-stu-id="81d26-136">If your environment doesn't pass hello checks, note hello issues and fix them.</span></span> <span data-ttu-id="81d26-137">Después, seleccione **Comprobar de nuevo**.</span><span class="sxs-lookup"><span data-stu-id="81d26-137">Then, select **Check Again**.</span></span> <span data-ttu-id="81d26-138">Después de pasar comprobaciones de requisitos previos de hello, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="81d26-138">After you pass hello prerequisite checks, select **Next**.</span></span>

  ![Instalador: botón Comprobar de nuevo](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="81d26-140">En hello **configuración de SQL** , seleccione la opción relevantes de hello para la instalación de SQL y, a continuación, seleccione **comprobar e instalar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-140">On hello **SQL Settings** page, select hello relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Instalador: página Configuración de SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="81d26-142">comprobaciones de Hello pueden tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="81d26-142">hello checks might take a few minutes.</span></span> <span data-ttu-id="81d26-143">Cuando las comprobaciones de Hola se termine, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="81d26-143">When hello checks are finished, select **Next**.</span></span>

  ![Instalador: botón Comprobar e instalar en Configuración de SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="81d26-145">En hello **configuración de la instalación** página, asegúrese de cualquier ubicación de toohello de cambios que está instalado el servidor de copia de seguridad o toohello ubicación de memoria virtual.</span><span class="sxs-lookup"><span data-stu-id="81d26-145">On hello **Installation Settings** page, make any changes toohello location where Backup Server is installed, or toohello Scratch Location.</span></span> <span data-ttu-id="81d26-146">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="81d26-146">Select **Next**.</span></span>

  ![Instalador: página Configuración de la instalación](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="81d26-148">toofinish Hola Asistente para instalación, seleccione **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-148">toofinish hello setup wizard, select **Finish**.</span></span>

  ![Instalador: finalizar](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="81d26-150">Agregar almacenamiento para Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="81d26-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="81d26-151">eficiencia del almacenamiento de copia de seguridad tooimprove, servidor de reserva v2 agrega compatibilidad con volúmenes.</span><span class="sxs-lookup"><span data-stu-id="81d26-151">tooimprove backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="81d26-152">Al igual que Backup Server v1, Backup Server v2 admite discos.</span><span class="sxs-lookup"><span data-stu-id="81d26-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="81d26-153">Agregar volúmenes y discos</span><span class="sxs-lookup"><span data-stu-id="81d26-153">Add volumes and disks</span></span>
<span data-ttu-id="81d26-154">Si ejecuta v2 del servidor de copia de seguridad en Windows Server 2016, puede usar datos de copia de seguridad de volúmenes toostore.</span><span class="sxs-lookup"><span data-stu-id="81d26-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes toostore backup data.</span></span> <span data-ttu-id="81d26-155">Los volúmenes permiten ahorrar almacenamiento y realizar copias de seguridad más rápido.</span><span class="sxs-lookup"><span data-stu-id="81d26-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="81d26-156">Dado que los volúmenes son tooBackup nuevo servidor, debe agregarlos.</span><span class="sxs-lookup"><span data-stu-id="81d26-156">Because volumes are new tooBackup Server, you must add them.</span></span> 

<span data-ttu-id="81d26-157">Cuando se agrega un servidor de tooBackup de volumen, puede permitir el volumen de hello un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="81d26-157">When you add a volume tooBackup Server, you can give hello volume a friendly name.</span></span> <span data-ttu-id="81d26-158">Haga clic en hello **Nombre_descriptivo** columna del volumen de Hola que desea tooname.</span><span class="sxs-lookup"><span data-stu-id="81d26-158">Click hello **Friendly Name** column of hello volume you want tooname.</span></span> <span data-ttu-id="81d26-159">Puede cambiar el nombre de hello más adelante, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="81d26-159">You can change hello name later, if necessary.</span></span> <span data-ttu-id="81d26-160">También puede usar PowerShell tooadd o cambiar los nombres descriptivos para los volúmenes.</span><span class="sxs-lookup"><span data-stu-id="81d26-160">You also can use PowerShell tooadd or change friendly names for volumes.</span></span>

<span data-ttu-id="81d26-161">tooadd un volumen en hello consola de administrador:</span><span class="sxs-lookup"><span data-stu-id="81d26-161">tooadd a volume in hello Administrator Console:</span></span>

1. <span data-ttu-id="81d26-162">En la consola de administrador del servidor de copia de seguridad de Azure hello, seleccione **administración** > **almacenamiento en disco** > **agregar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-162">In hello Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Asistente para agregar almacenamiento en disco de hello abierto](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="81d26-164">Se abrirá el Asistente para agregar almacenamiento en disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-164">This opens hello Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="81d26-165">En hello **agregar almacenamiento en disco** página Hola **volúmenes disponibles** cuadro, seleccione un volumen y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-165">On hello **Add Disk Storage** page, in hello **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="81d26-166">Hola **seleccionado volúmenes** cuadro, escriba un nombre descriptivo para el volumen de hello y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-166">In hello **Selected volumes** box, enter a friendly name for hello volume, and then select **OK**.</span></span>

      ![Asistente para agregar almacenamiento en disco: agregar volumen](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="81d26-168">Si desea tooadd un disco, disco de hello debe pertenecer tooa grupo de protección que tiene un almacenamiento heredado.</span><span class="sxs-lookup"><span data-stu-id="81d26-168">If you want tooadd a disk, hello disk must belong tooa protection group that has legacy storage.</span></span> <span data-ttu-id="81d26-169">Estos discos solo se pueden usar para estos grupos de protección.</span><span class="sxs-lookup"><span data-stu-id="81d26-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="81d26-170">Si el servidor de copia de seguridad no tiene orígenes que tienen protección heredada, disco de hello no aparece.</span><span class="sxs-lookup"><span data-stu-id="81d26-170">If Backup Server doesn't have sources that have legacy protection, hello disk isn't listed.</span></span>

  <span data-ttu-id="81d26-171">Para obtener más información acerca de cómo agregar discos, consulte [adición de almacenamiento de discos tooincrease heredado](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="81d26-171">For more information about adding disks, see [Adding disks tooincrease legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="81d26-172">No se puede asignar un nombre descriptivo a un disco.</span><span class="sxs-lookup"><span data-stu-id="81d26-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-toovolumes"></a><span data-ttu-id="81d26-173">Asignar toovolumes de cargas de trabajo</span><span class="sxs-lookup"><span data-stu-id="81d26-173">Assign workloads toovolumes</span></span>

<span data-ttu-id="81d26-174">En el servidor de copia de seguridad, puede especificar que las cargas de trabajo se asignan toowhich volúmenes.</span><span class="sxs-lookup"><span data-stu-id="81d26-174">In Backup Server, you specify which workloads are assigned toowhich volumes.</span></span> <span data-ttu-id="81d26-175">Por ejemplo, puede establecer volúmenes costosos que admiten un gran número de operaciones de entrada/salida por segundo (IOPS) toostore solo las cargas de trabajo que requieren copias de seguridad frecuentes de gran volumen.</span><span class="sxs-lookup"><span data-stu-id="81d26-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="81d26-176">Un ejemplo es SQL Server con registros de transacciones.</span><span class="sxs-lookup"><span data-stu-id="81d26-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="81d26-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="81d26-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="81d26-178">propiedades de hello tooupdate de un volumen en el bloque de almacenamiento de hello en el servidor de copia de seguridad, use el cmdlet de PowerShell de hello DPMDiskStorage de actualización.</span><span class="sxs-lookup"><span data-stu-id="81d26-178">tooupdate hello properties of a volume in hello storage pool in Backup Server, use hello PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="81d26-179">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="81d26-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="81d26-180">Todos los cambios realizados mediante el uso de PowerShell se reflejan en hello interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="81d26-180">All changes that you make by using PowerShell are reflected in hello UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="81d26-181">Proteger orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="81d26-181">Protect data sources</span></span>
<span data-ttu-id="81d26-182">toobegin protegen orígenes de datos, cree un grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="81d26-182">toobegin protecting data sources, create a protection group.</span></span> <span data-ttu-id="81d26-183">Hola siguiendo los pasos resaltado cambios o adiciones toohello Asistente para nuevo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="81d26-183">hello following steps highlight changes or additions toohello New Protection Group wizard.</span></span>

<span data-ttu-id="81d26-184">toocreate un grupo de protección:</span><span class="sxs-lookup"><span data-stu-id="81d26-184">toocreate a protection group:</span></span>

1. <span data-ttu-id="81d26-185">En la consola de administrador del servidor de copia de seguridad de hello, seleccione **protección**.</span><span class="sxs-lookup"><span data-stu-id="81d26-185">In hello Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="81d26-186">En la cinta de opciones de herramienta de hello, seleccione **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="81d26-186">On hello tool ribbon, select **New**.</span></span>

    <span data-ttu-id="81d26-187">Se abrirá el Asistente para crear nuevo grupo de protección de Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-187">This opens hello Create New Protection Group wizard.</span></span>

  ![Asistente para crear nuevo grupo de protección](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="81d26-189">En hello **bienvenida** página, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="81d26-189">On hello **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="81d26-190">En hello **Seleccionar tipo de grupo de protección** , seleccione el tipo de saludo de grupo de protección que desee toocreate y, a continuación, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="81d26-190">On hello **Select Protection Group Type** page, select hello type of protection group you want toocreate, and then select **Next**.</span></span>

  ![Página Seleccionar tipo de grupo de protección](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="81d26-192">En hello **seleccionar miembros del grupo** página Hola **miembros disponibles** panel, los miembros de hello con se muestran los agentes de protección.</span><span class="sxs-lookup"><span data-stu-id="81d26-192">On hello **Select Group Members** page, in hello **Available members** pane, hello members with protection agents are listed.</span></span> <span data-ttu-id="81d26-193">En este ejemplo, seleccione el volumen D:\ y E:\ y agregarlas toohello **seleccionado miembros** panel.</span><span class="sxs-lookup"><span data-stu-id="81d26-193">For this example, select volume D:\ and E:\ and add them toohello **Selected members** pane.</span></span> <span data-ttu-id="81d26-194">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="81d26-194">Select **Next**.</span></span>

  ![Página Seleccionar miembros del grupo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="81d26-196">En hello **Seleccionar método de protección de datos** página, escriba un **el nombre del grupo de protección**, seleccione el método de protección de hello y, a continuación, seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="81d26-196">On hello **Select Data Protection Method** page, enter a **Protection group name**, select hello protection method, and then select **Next**.</span></span> <span data-ttu-id="81d26-197">Si desea que la protección a corto plazo, debe seleccionar hello **disco** método de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="81d26-197">If you want short-term protection, you must select hello **Disk** backup method.</span></span>

  ![Página Seleccionar método de protección de datos](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="81d26-199">En hello **especificar objetivos a corto plazo** detalles de la página, seleccione Hola para **duración de retención** y **frecuencia de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="81d26-199">On hello **Specify Short-Term Goals** page, select hello details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="81d26-200">Después, seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="81d26-200">Then, select **Next**.</span></span> <span data-ttu-id="81d26-201">Si lo desea, toochange programación Hola para cuando los puntos de recuperación se realizó, seleccione **modificar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-201">Optionally, toochange hello schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Página Especificar objetivos a corto plazo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="81d26-203">En hello **Revisar asignación de almacenamiento de disco** página, revise los detalles acerca de los orígenes de datos de hello seleccionó, su tamaño y los valores de hello espacio toobe aprovisionado y Hola volumen de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="81d26-203">On hello **Review Disk Storage Allocation** page, review details about hello data sources you selected, their size, and  values for hello space toobe provisioned and hello target storage volume.</span></span>

  ![Página Revisar la asignación del almacenamiento en disco](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="81d26-205">Volúmenes de almacenamiento se basan en la asignación del volumen de carga de trabajo de hello (establecido mediante el uso de PowerShell) y Hola almacenamiento disponible.</span><span class="sxs-lookup"><span data-stu-id="81d26-205">Storage volumes are based on hello workload volume allocation (set by using PowerShell) and hello available storage.</span></span> <span data-ttu-id="81d26-206">Puede cambiar los volúmenes de almacenamiento de hello seleccionando otros volúmenes en el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-206">You can change hello storage volumes by selecting other volumes in hello drop-down menu.</span></span> <span data-ttu-id="81d26-207">Si cambia el valor de Hola para **almacenamiento de destino**, Hola valor para **almacenamiento en disco disponible** cambia dinámicamente valores tooreflect en **espacio** y **Insuficiente espacio**.</span><span class="sxs-lookup"><span data-stu-id="81d26-207">If you change hello value for **Target Storage**, hello value for **Available disk storage** dynamically changes tooreflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="81d26-208">Si los orígenes de datos de hello aumentan según lo previsto, Hola valor para hello **espacio insuficiente** columna en **almacenamiento en disco disponible** refleja la cantidad de Hola de almacenamiento adicional que se necesita.</span><span class="sxs-lookup"><span data-stu-id="81d26-208">If hello data sources grow as planned, hello value for hello **Underprovisioned Space** column in **Available disk storage** reflects hello amount of additional storage that's needed.</span></span> <span data-ttu-id="81d26-209">Use este plan de toohelp valor las necesidades de almacenamiento de copias de seguridad sin problemas.</span><span class="sxs-lookup"><span data-stu-id="81d26-209">Use this value toohelp plan your storage needs for smooth backups.</span></span> <span data-ttu-id="81d26-210">Si Hola valor es cero, significa que no hay ningún problema potencial con el almacenamiento en un futuro previsible Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-210">If hello value is zero, there are no potential problems with storage in hello foreseeable future.</span></span> <span data-ttu-id="81d26-211">Si el valor de hello es un número distinto de cero, no tiene suficiente espacio de almacenamiento asignado (basado en protección hello y directiva de tamaño de los datos de los miembros protegidos).</span><span class="sxs-lookup"><span data-stu-id="81d26-211">If hello value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and hello data size of your protected members).</span></span>

  ![Almacenamiento en disco subasignado](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="81d26-213">toofinish crear a un asistente de hello completa, grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="81d26-213">toofinish creating your protection group, complete hello wizard.</span></span>

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a><span data-ttu-id="81d26-214">Migrar almacenamiento heredado tooModern almacenamiento de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="81d26-214">Migrate legacy storage tooModern Backup Storage</span></span>
<span data-ttu-id="81d26-215">Después de actualizar tooor install v2 del servidor de copia de seguridad y actualización hello tooWindows de sistema operativo Server 2016, actualice su toouse de grupos de protección moderna almacenamiento de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="81d26-215">After you upgrade tooor install Backup Server v2 and upgrade hello operating system tooWindows Server 2016, update your protection groups toouse Modern Backup Storage.</span></span> <span data-ttu-id="81d26-216">De forma predeterminada, los grupos de protección no se cambian.</span><span class="sxs-lookup"><span data-stu-id="81d26-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="81d26-217">Se siguen toofunction tal y como configuraron inicialmente.</span><span class="sxs-lookup"><span data-stu-id="81d26-217">They continue toofunction as they were initially set up.</span></span> 

<span data-ttu-id="81d26-218">Actualizar toouse de grupos de protección moderna almacenamiento de copia de seguridad es opcional.</span><span class="sxs-lookup"><span data-stu-id="81d26-218">Updating protection groups toouse Modern Backup Storage is optional.</span></span> <span data-ttu-id="81d26-219">grupo de protección de hello tooupdate, detenga la protección de todos los orígenes de datos mediante el uso de hello opción Conservar datos.</span><span class="sxs-lookup"><span data-stu-id="81d26-219">tooupdate hello protection group, stop protection of all data sources by using hello retain data option.</span></span> <span data-ttu-id="81d26-220">A continuación, agregue Hola datos orígenes tooa nuevo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="81d26-220">Then, add hello data sources tooa new protection group.</span></span>

1. <span data-ttu-id="81d26-221">En la consola de administrador de hello, seleccione hello **protección** característica.</span><span class="sxs-lookup"><span data-stu-id="81d26-221">In hello Administrator Console, select hello **Protection** feature.</span></span> <span data-ttu-id="81d26-222">Hola **miembro del grupo de protección** lista, haga clic en miembro de hello y, a continuación, seleccione **detener la protección de miembro**.</span><span class="sxs-lookup"><span data-stu-id="81d26-222">In hello **Protection Group Member** list, right-click hello member, and then select **Stop protection of member**.</span></span>

  ![Detener protección de miembro](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="81d26-224">Hola **quitar del grupo** cuadro de diálogo, revisión Hola utiliza espacio en disco y espacio libre disponible hello para el grupo de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-224">In hello **Remove from Group** dialog box, review hello used disk space and hello available free space for hello storage pool.</span></span> <span data-ttu-id="81d26-225">predeterminado de Hello es tooleave puntos de recuperación de hello en el disco de Hola y permitirles tooexpire por su directiva de retención asociado.</span><span class="sxs-lookup"><span data-stu-id="81d26-225">hello default is tooleave hello recovery points on hello disk and allow them tooexpire per their associated retention policy.</span></span> <span data-ttu-id="81d26-226">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-226">Click **OK**.</span></span>

  <span data-ttu-id="81d26-227">Si desea que el espacio del disco de hello devuelto utiliza de tooimmediately toohello grupo de almacenamiento libre, seleccione hello **Eliminar réplica en disco** datos de copia de seguridad de casilla de verificación toodelete Hola (y los puntos de recuperación) asociados a ese miembro.</span><span class="sxs-lookup"><span data-stu-id="81d26-227">If you want tooimmediately return hello used disk space toohello free storage pool, select hello **Delete replica on disk** check box toodelete hello backup data (and recovery points) associated with that member.</span></span>

  ![Cuadro de diálogo Quitar del grupo](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="81d26-229">Cree un grupo de protección que use Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="81d26-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="81d26-230">Incluir orígenes de datos de hello desprotegido.</span><span class="sxs-lookup"><span data-stu-id="81d26-230">Include hello unprotected data sources.</span></span>


## <a name="add-disks-tooincrease-legacy-storage"></a><span data-ttu-id="81d26-231">Agregar almacenamiento de discos tooincrease heredado</span><span class="sxs-lookup"><span data-stu-id="81d26-231">Add disks tooincrease legacy storage</span></span>

<span data-ttu-id="81d26-232">Si desea toouse almacenamiento heredado con el servidor de copia de seguridad, tendrá que almacenamiento de información de tooadd discos tooincrease heredado.</span><span class="sxs-lookup"><span data-stu-id="81d26-232">If you want toouse legacy storage with Backup Server, you might need tooadd disks tooincrease legacy storage.</span></span> 

<span data-ttu-id="81d26-233">almacenamiento en disco tooadd:</span><span class="sxs-lookup"><span data-stu-id="81d26-233">tooadd disk storage:</span></span>

1. <span data-ttu-id="81d26-234">En la consola de administrador de hello, seleccione **administración** > **almacenamiento en disco** > **agregar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-234">In hello Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Cuadro de diálogo Agregar almacenamiento en disco](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="81d26-236">Hola **agregar almacenamiento en disco** cuadro de diálogo, seleccione **agregar discos**.</span><span class="sxs-lookup"><span data-stu-id="81d26-236">In hello **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="81d26-237">En la lista de Hola de discos disponibles, seleccione los discos de hello desea tooadd, seleccione **agregar**y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-237">In hello list of available disks, select hello disks you want tooadd, select **Add**, and then select **OK**.</span></span>

## <a name="update-hello-data-protection-manager-protection-agent"></a><span data-ttu-id="81d26-238">Actualizar el agente de protección de hello Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="81d26-238">Update hello Data Protection Manager protection agent</span></span>

<span data-ttu-id="81d26-239">Servidor de copia de seguridad utiliza el agente de protección de System Center Data Protection Manager Hola para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="81d26-239">Backup Server uses hello System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="81d26-240">Si va a actualizar a un agente de protección que no sea red toohello conectado, no puede usar hello toocomplete de la consola de administrador de protección de datos de una actualización de agente conectada.</span><span class="sxs-lookup"><span data-stu-id="81d26-240">If you are upgrading a protection agent that is not connected toohello network, you cannot use hello Data Protection Manager Administrator Console toocomplete a connected agent upgrade.</span></span> <span data-ttu-id="81d26-241">Debe actualizar el agente de protección de hello en un entorno de dominio no esté activa.</span><span class="sxs-lookup"><span data-stu-id="81d26-241">You must upgrade hello protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="81d26-242">Hasta que Hola cliente equipo red toohello conectado, Hola que consola de administrador de protección de datos muestra esa actualización de agente de protección de hello está pendiente.</span><span class="sxs-lookup"><span data-stu-id="81d26-242">Until hello client computer is connected toohello network, hello Data Protection Manager Administrator Console shows that hello protection agent update is pending.</span></span>

<span data-ttu-id="81d26-243">Hello siguientes secciones se describen cómo tooupdate los agentes de protección para los equipos cliente que están conectados y los equipos cliente que no están conectados.</span><span class="sxs-lookup"><span data-stu-id="81d26-243">hello following sections describe how tooupdate protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="81d26-244">Actualizar un agente de protección de un equipo cliente conectado</span><span class="sxs-lookup"><span data-stu-id="81d26-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="81d26-245">En la consola de administrador del servidor de copia de seguridad de hello, seleccione **administración** > **agentes**.</span><span class="sxs-lookup"><span data-stu-id="81d26-245">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="81d26-246">En el panel de información de hello, seleccionar equipos de cliente de hello para el que desea que agente de protección de tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-246">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="81d26-247">Hola **las actualizaciones del agente** columna indica cuando una actualización de agente de protección está disponible para cada equipo protegido.</span><span class="sxs-lookup"><span data-stu-id="81d26-247">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="81d26-248">Hola **acciones** panel, hello **actualización** acción sólo está disponible cuando se selecciona un equipo protegido y las actualizaciones están disponibles.</span><span class="sxs-lookup"><span data-stu-id="81d26-248">In hello **Actions** pane, hello **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="81d26-249">tooinstall actualizar agentes de protección en los equipos de hello seleccionado, de hello **acciones** panel, seleccione **actualización**.</span><span class="sxs-lookup"><span data-stu-id="81d26-249">tooinstall updated protection agents on hello selected computers, in hello **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="81d26-250">Actualizar un agente de protección en un equipo cliente que no está conectado</span><span class="sxs-lookup"><span data-stu-id="81d26-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="81d26-251">En la consola de administrador del servidor de copia de seguridad de hello, seleccione **administración** > **agentes**.</span><span class="sxs-lookup"><span data-stu-id="81d26-251">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="81d26-252">En el panel de información de hello, seleccionar equipos de cliente de hello para el que desea que agente de protección de tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-252">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="81d26-253">Hola **las actualizaciones del agente** columna indica cuando una actualización de agente de protección está disponible para cada equipo protegido.</span><span class="sxs-lookup"><span data-stu-id="81d26-253">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="81d26-254">Hola **acciones** panel, hello **actualización** acción no está disponible cuando se selecciona un equipo protegido si existen actualizaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="81d26-254">In hello **Actions** pane, hello **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="81d26-255">tooinstall actualizar agentes de protección en los equipos de hello seleccionado, seleccionados **actualización**.</span><span class="sxs-lookup"><span data-stu-id="81d26-255">tooinstall updated protection agents on hello selected computers, select **Update**.</span></span>

4. <span data-ttu-id="81d26-256">Para un equipo cliente que no está conectado toohello red, hasta que el equipo de hello red toohello conectado, Hola **estado del agente** columna muestra un estado de **actualizar pendientes**.</span><span class="sxs-lookup"><span data-stu-id="81d26-256">For a client computer that is not connected toohello network, until hello computer is connected toohello network, hello **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="81d26-257">Después de que un equipo cliente está conectado toohello red, Hola **las actualizaciones del agente** columna para el equipo de cliente hello muestra un estado de **actualizar**.</span><span class="sxs-lookup"><span data-stu-id="81d26-257">After a client computer is connected toohello network, hello **Agent Updates** column for hello client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a><span data-ttu-id="81d26-258">Mover grupos de protección heredados de una versión antigua y la nueva versión de hello de sincronización con Azure</span><span class="sxs-lookup"><span data-stu-id="81d26-258">Move legacy Protection groups from old version and sync hello new version with Azure</span></span>

<span data-ttu-id="81d26-259">Una vez que se actualizan hello sistema operativo y el servidor de copia de seguridad de Azure, está listo tooprotect nuevos orígenes de datos mediante almacenamiento de copia de seguridad modernos.</span><span class="sxs-lookup"><span data-stu-id="81d26-259">Once Azure Backup Server and hello OS are both updated, you are ready tooprotect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="81d26-260">Los orígenes de datos protegidos sin embargo ya continuará toobe protegida Hola heredado forma que estuviera en el servidor de copia de seguridad de Azure pero todos los nuevo grupo de protección utilizarán moderna almacenamiento de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="81d26-260">However already protected data sources will continue toobe protected in hello legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="81d26-261">Pasos siguientes son orígenes de datos de toomigrate del modo heredado de almacenamiento de copia de seguridad de tooModern de protección.</span><span class="sxs-lookup"><span data-stu-id="81d26-261">Below steps are toomigrate data sources from legacy  mode of protection tooModern backup storage.</span></span>

<span data-ttu-id="81d26-262">• Agregue el bloque de almacenamiento para DPM el nuevo toohello volúmenes hello y asignar etiquetas de origen de datos y nombres descriptivas si lo desea.</span><span class="sxs-lookup"><span data-stu-id="81d26-262">• Add hello new volume(s) toohello DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="81d26-263">• Para cada origen de datos que se encuentra en modo heredado, detenga la protección de orígenes de datos de Hola y "Conservar datos protegidos".</span><span class="sxs-lookup"><span data-stu-id="81d26-263">• For each data source that is in legacy mode, stop protection of hello data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="81d26-264">Así permitirá la recuperación de los puntos de recuperación antiguos después de la migración.</span><span class="sxs-lookup"><span data-stu-id="81d26-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="81d26-265">• Crear un nuevo grupo de protección y seleccione orígenes de datos de Hola que son toobe almacenada con el nuevo formato.</span><span class="sxs-lookup"><span data-stu-id="81d26-265">• Create a new PG and select hello data sources that are toobe stored using new format.</span></span>
<span data-ttu-id="81d26-266">• DPM realizará una copia de la réplica de almacenamiento de copia de seguridad heredadas de hello en hello volumen de almacenamiento de copia de seguridad moderna localmente.</span><span class="sxs-lookup"><span data-stu-id="81d26-266">• DPM will do a replica copy from hello legacy backup storage into hello Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="81d26-267">Nota: Esto se verá como un trabajo de operación posterior a la recuperación • Todos los nuevos puntos de recuperación y sincronización se almacenarán entonces en Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="81d26-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="81d26-268">• Puntos de recuperación antiguos se eliminarán cuando expire y finalmente liberar espacio en disco Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-268">• Old recovery points will be pruned out as they expire and eventually free up hello disk space.</span></span>
<span data-ttu-id="81d26-269">• Una vez que todos los volúmenes de hello heredado se eliminan de almacenamiento anterior hello, disco de Hola se puede quitar del sistema de hello y copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="81d26-269">• Once all hello legacy volumes are deleted from hello old storage, hello disk can be removed from Azure backup and hello system.</span></span>
<span data-ttu-id="81d26-270">• Realizar una copia de seguridad de hello Azure DPMDB.</span><span class="sxs-lookup"><span data-stu-id="81d26-270">• Take a backup of hello  Azure DPMDB.</span></span>

<span data-ttu-id="81d26-271">Parte 2:-elementos importantes > Hola nuevo servidor deberá toobe mismo nombre como servidor de copia de seguridad de Azure de hello original.</span><span class="sxs-lookup"><span data-stu-id="81d26-271">Part 2: -Important items> hello new server will need toobe named same as hello original Azure Backup server.</span></span> <span data-ttu-id="81d26-272">No se puede cambiar el nombre de Hola Hola nueva copia de seguridad del servidor de Azure si desea toouse anterior grupo de almacenamiento y los puntos de recuperación de base de datos DPM tooretain - debe hacer copia de seguridad de base de datos DPM ya que será necesario toobe restaurar</span><span class="sxs-lookup"><span data-stu-id="81d26-272">You cannot change hello name of hello new Azure backup server if you want toouse old storage pool and DPMDB tooretain recovery points -Must have backup of DPMDB  as it will need toobe restored</span></span>

1) <span data-ttu-id="81d26-273">Cierre Hola servidor de copia de seguridad de Azure original o dejarlo fuera de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="81d26-273">Shutdown hello original Azure backup server or take it off hello wire.</span></span>
2) <span data-ttu-id="81d26-274">Restablecimiento de cuentas de máquina de hello en active directory.</span><span class="sxs-lookup"><span data-stu-id="81d26-274">Reset hello machine account in active directory.</span></span>
3) <span data-ttu-id="81d26-275">Instalar Server 2016 en el nombre Hola mismo nombre de equipo como servidor de copia de seguridad de Azure original de Hola y nueva máquina.</span><span class="sxs-lookup"><span data-stu-id="81d26-275">Install Server 2016 on new machine and name it hello same machine name as hello original Azure Backup server.</span></span>
4) <span data-ttu-id="81d26-276">Unirse a dominio Hola</span><span class="sxs-lookup"><span data-stu-id="81d26-276">Join hello Domain</span></span>
5) <span data-ttu-id="81d26-277">Instale Azure Backup Server V2 (mueva los discos del grupo de DPM Storage desde el servidor antiguo e impórtelos)</span><span class="sxs-lookup"><span data-stu-id="81d26-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="81d26-278">Restaurar Hola DPMDB tomada del final de la parte 2</span><span class="sxs-lookup"><span data-stu-id="81d26-278">Restore hello DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="81d26-279">Adjuntar almacenamiento Hola de hello original copia de seguridad toohello nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="81d26-279">Attach hello storage from hello original backup server toohello new server.</span></span>
8) <span data-ttu-id="81d26-280">De hello SQL Restaurar base de datos DPM</span><span class="sxs-lookup"><span data-stu-id="81d26-280">From SQL Restore hello DPMDB</span></span>
9) <span data-ttu-id="81d26-281">Desde la línea de comandos de administración en el nuevo servidor cd tooMicrosoft copia de seguridad de Azure instalar ubicación y la carpeta bin</span><span class="sxs-lookup"><span data-stu-id="81d26-281">From admin command line on new server cd tooMicrosoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="81d26-282">Ejemplo de ruta de acceso: C:\windows\system32>cd "c:\Archivos de programa\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="81d26-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="81d26-283">copia de seguridad de tooAzure ejecute DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="81d26-283">tooAzure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="81d26-284">Ejecute DPMSYNC-SYNC Nota Si ha agregado el nuevo grupo de almacenamiento de DPM de toohello de discos en lugar de moverse Hola gastadas, a continuación, ejecute DPMSYNC - Reallocatereplica</span><span class="sxs-lookup"><span data-stu-id="81d26-284">Run DPMSYNC -SYNC Note If you have added NEW disks toohello DPM Storage pool instead of moving hello old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="81d26-285">Nuevos cmdlets de PowerShell en v2</span><span class="sxs-lookup"><span data-stu-id="81d26-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="81d26-286">Cuando se instala Azure Backup Server v2, hay dos nuevos cmdlets disponibles:</span><span class="sxs-lookup"><span data-stu-id="81d26-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="81d26-287">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="81d26-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="81d26-288">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="81d26-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="81d26-289">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="81d26-289">Next steps</span></span>

<span data-ttu-id="81d26-290">Obtenga información acerca de cómo tooprepare el servidor o empezar a proteger una carga de trabajo:</span><span class="sxs-lookup"><span data-stu-id="81d26-290">Learn how tooprepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="81d26-291">Preparar cargas de trabajo de Backup Server</span><span class="sxs-lookup"><span data-stu-id="81d26-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="81d26-292">Usar tooback del servidor de copia de seguridad de un servidor de VMware</span><span class="sxs-lookup"><span data-stu-id="81d26-292">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="81d26-293">Usar tooback del servidor de copia de seguridad de SQL Server</span><span class="sxs-lookup"><span data-stu-id="81d26-293">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="81d26-294">Usar Modern Backup Storage con Backup Server</span><span class="sxs-lookup"><span data-stu-id="81d26-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

