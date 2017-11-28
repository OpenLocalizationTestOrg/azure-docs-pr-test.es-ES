---
title: Instalar Azure Backup Server v2 | Microsoft Docs
description: "Azure Backup Server v2 proporciona funciones mejoradas de copia de seguridad para proteger máquinas virtuales, archivos, carpetas, cargas de trabajo, etc. Obtenga información sobre cómo instalar Azure Backup Server v2 o actualizar a esta versión."
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
ms.openlocfilehash: 1bbb16afef7940933b4c3ae23873f212770137e0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="2bb5a-104">Instalar Azure Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="2bb5a-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="2bb5a-105">Azure Backup Server ayuda a proteger máquinas virtuales (VM), cargas de trabajo, archivos, carpetas, etc.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="2bb5a-106">Azure Backup Server v2 se basa en Azure Backup Server v1 y proporciona características nuevas que no están disponibles en la versión v1.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="2bb5a-107">Para obtener una comparación de las características de v1 y v2, vea [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md) (Matriz de protección de Azure Backup Server).</span><span class="sxs-lookup"><span data-stu-id="2bb5a-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="2bb5a-108">Las características adicionales de Backup Server v2 son una actualización de Backup Server v1.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-108">The additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="2bb5a-109">A pesar de ello, no es un requisito previo disponer de Backup Server v1 para instalar Backup Server v2.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="2bb5a-110">Si quiere actualizar de Backup Server v1 a Backup Server v2, instale Backup Server v2 en el servidor de protección de Backup Server.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-110">If you want to upgrade from Backup Server v1 to Backup Server v2, install Backup Server v2 on the Backup Server protection server.</span></span> <span data-ttu-id="2bb5a-111">La configuración existente de Backup Server permanecerá intacta.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="2bb5a-112">Puede instalar Backup Server v2 en Windows Server 2012 R2 o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="2bb5a-113">Para aprovechar características nuevas como Modern Backup Storage de System Center 2016 Data Protection Manager, debe instalar Backup Server v2 en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-113">To take advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="2bb5a-114">Antes de instalar Backup Server v2 o actualizar a esta versión, lea este artículo sobre los [requisitos previos de instalación](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="2bb5a-114">Before you upgrade to or install Backup Server v2, read about the [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="2bb5a-115">Azure Backup Server tiene la misma base de código que System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-115">Azure Backup Server has the same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="2bb5a-116">Backup Server v1 es equivalente a Data Protection Manager 2012 R2, y Backup Server v2 es equivalente a Data Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-116">Backup Server v1 is equivalent to Data Protection Manager 2012 R2, and Backup Server v2 is equivalent to Data Protection Manager 2016.</span></span> <span data-ttu-id="2bb5a-117">En ocasiones, en este artículo se hace referencia a la documentación de Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-117">This article occasionally references the Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-to-v2"></a><span data-ttu-id="2bb5a-118">Actualizar Backup Server a la versión v2</span><span class="sxs-lookup"><span data-stu-id="2bb5a-118">Upgrade Backup Server to v2</span></span>
<span data-ttu-id="2bb5a-119">Para actualizar de Backup Server v1 a Backup Server v2, asegúrese de que la instalación tiene las actualizaciones necesarias:</span><span class="sxs-lookup"><span data-stu-id="2bb5a-119">To upgrade from Backup Server v1 to Backup Server v2, make sure your installation has the required updates:</span></span>

- <span data-ttu-id="2bb5a-120">[Actualice los agentes de protección](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) de los servidores protegidos.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-120">[Update the protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on the protected servers.</span></span>
- <span data-ttu-id="2bb5a-121">Actualice Windows Server 2012 R2 a Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-121">Upgrade Windows Server 2012 R2 to Windows Server 2016.</span></span>
- <span data-ttu-id="2bb5a-122">Actualice Remote Administrator de Azure Backup Server en todos los servidores de producción.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="2bb5a-123">Asegúrese de que las copias de seguridad están establecidas para continuar sin necesidad de reiniciar el servidor de producción.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-123">Ensure that backups are set to continue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="2bb5a-124">Pasos para actualizar a Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="2bb5a-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="2bb5a-125">En el Centro de descarga, [descargue el instalador de actualización](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="2bb5a-125">In the Download Center, [download the upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="2bb5a-126">Después de extraer el Asistente para instalación, asegúrese de que está seleccionado **Execute setup.exe** (Ejecutar setup.exe) y, después, seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-126">After you extract the setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Instalador: ejecutar el programa de instalación](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="2bb5a-128">En el Asistente para Microsoft Azure Backup Server, en **Instalar**, seleccione **Microsoft Azure Backup Server**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-128">In the Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Instalador: seleccionar la instalación](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="2bb5a-130">En la **página principal**, revise las advertencias y seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-130">On the **Welcome** page, review the warnings, and then select **Next**.</span></span>

  ![Instalador: página principal](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="2bb5a-132">El Asistente para instalación comprueba una serie de requisitos previos para asegurarse de que se puede actualizar el entorno.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-132">The setup wizard performs prerequisite checks to make sure your environment can upgrade.</span></span> <span data-ttu-id="2bb5a-133">En la página **Comprobaciones de requisitos previos**, seleccione **Comprobar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-133">On the **Prerequisite Checks** page, select **Check**.</span></span>

  ![Instalador: página Comprobaciones de requisitos previos](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="2bb5a-135">El entorno debe superar las comprobaciones de requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-135">Your environment must pass the prerequisite checks.</span></span> <span data-ttu-id="2bb5a-136">Si no las supera, tome nota de los problemas y corríjalos.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-136">If your environment doesn't pass the checks, note the issues and fix them.</span></span> <span data-ttu-id="2bb5a-137">Después, seleccione **Comprobar de nuevo**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-137">Then, select **Check Again**.</span></span> <span data-ttu-id="2bb5a-138">Una vez que haya superado las comprobaciones de requisitos previos, seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-138">After you pass the prerequisite checks, select **Next**.</span></span>

  ![Instalador: botón Comprobar de nuevo](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="2bb5a-140">En la página **Configuración de SQL**, seleccione la opción correspondiente a su instalación de SQL y, después, seleccione **Comprobar e instalar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-140">On the **SQL Settings** page, select the relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Instalador: página Configuración de SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="2bb5a-142">Estas comprobaciones pueden tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-142">The checks might take a few minutes.</span></span> <span data-ttu-id="2bb5a-143">Cuando las comprobaciones hayan terminado, seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-143">When the checks are finished, select **Next**.</span></span>

  ![Instalador: botón Comprobar e instalar en Configuración de SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="2bb5a-145">En la página **Configuración de la instalación**, cambie la ubicación donde se instala Backup Server o la ubicación temporal.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-145">On the **Installation Settings** page, make any changes to the location where Backup Server is installed, or to the Scratch Location.</span></span> <span data-ttu-id="2bb5a-146">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-146">Select **Next**.</span></span>

  ![Instalador: página Configuración de la instalación](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="2bb5a-148">Para finalizar el Asistente para instalación, seleccione **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-148">To finish the setup wizard, select **Finish**.</span></span>

  ![Instalador: finalizar](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="2bb5a-150">Agregar almacenamiento para Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="2bb5a-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="2bb5a-151">Para mejorar la eficacia del almacenamiento de copias de seguridad, Backup Server v2 es compatible con volúmenes.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-151">To improve backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="2bb5a-152">Al igual que Backup Server v1, Backup Server v2 admite discos.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="2bb5a-153">Agregar volúmenes y discos</span><span class="sxs-lookup"><span data-stu-id="2bb5a-153">Add volumes and disks</span></span>
<span data-ttu-id="2bb5a-154">Si ejecuta Backup Server v2 en Windows Server 2016, puede usar volúmenes para almacenar datos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes to store backup data.</span></span> <span data-ttu-id="2bb5a-155">Los volúmenes permiten ahorrar almacenamiento y realizar copias de seguridad más rápido.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="2bb5a-156">Dado que los volúmenes son una novedad de Backup Server, debe agregarlos.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-156">Because volumes are new to Backup Server, you must add them.</span></span> 

<span data-ttu-id="2bb5a-157">Al agregar un volumen a Backup Server, puede asignarle un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-157">When you add a volume to Backup Server, you can give the volume a friendly name.</span></span> <span data-ttu-id="2bb5a-158">Haga clic en la columna **Nombre descriptivo** del volumen al que quiere asignarle un nombre.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-158">Click the **Friendly Name** column of the volume you want to name.</span></span> <span data-ttu-id="2bb5a-159">Puede cambiar el nombre posteriormente, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-159">You can change the name later, if necessary.</span></span> <span data-ttu-id="2bb5a-160">También puede usar PowerShell para agregar nombres descriptivos a los volúmenes o cambiarlos.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-160">You also can use PowerShell to add or change friendly names for volumes.</span></span>

<span data-ttu-id="2bb5a-161">Para agregar un volumen en la consola de administrador:</span><span class="sxs-lookup"><span data-stu-id="2bb5a-161">To add a volume in the Administrator Console:</span></span>

1. <span data-ttu-id="2bb5a-162">En la consola de administrador de Azure Backup Server, seleccione **Administración** > **Almacenamiento en disco** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-162">In the Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Abrir el Asistente para agregar almacenamiento en disco](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="2bb5a-164">Se abre el Asistente para agregar almacenamiento en disco.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-164">This opens the Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="2bb5a-165">En la página **Agregar almacenamiento en disco**, en el cuadro **Volúmenes disponibles**, seleccione un volumen y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-165">On the **Add Disk Storage** page, in the **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="2bb5a-166">En el cuadro **Volúmenes seleccionados**, escriba un nombre descriptivo para el volumen y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-166">In the **Selected volumes** box, enter a friendly name for the volume, and then select **OK**.</span></span>

      ![Asistente para agregar almacenamiento en disco: agregar volumen](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="2bb5a-168">Si quiere agregar un disco, debe pertenecer a un grupo de protección que tenga almacenamiento heredado.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-168">If you want to add a disk, the disk must belong to a protection group that has legacy storage.</span></span> <span data-ttu-id="2bb5a-169">Estos discos solo se pueden usar para estos grupos de protección.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="2bb5a-170">Si Backup Server no tiene orígenes con protección heredada, el disco no aparecerá.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-170">If Backup Server doesn't have sources that have legacy protection, the disk isn't listed.</span></span>

  <span data-ttu-id="2bb5a-171">Para obtener más información sobre cómo agregar discos, vea [Adding disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage) (Agregar discos para aumentar el almacenamiento heredado).</span><span class="sxs-lookup"><span data-stu-id="2bb5a-171">For more information about adding disks, see [Adding disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="2bb5a-172">No se puede asignar un nombre descriptivo a un disco.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-to-volumes"></a><span data-ttu-id="2bb5a-173">Asignar cargas de trabajo a volúmenes</span><span class="sxs-lookup"><span data-stu-id="2bb5a-173">Assign workloads to volumes</span></span>

<span data-ttu-id="2bb5a-174">En Backup Server, puede especificar qué cargas de trabajo se asignan a cada volumen.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-174">In Backup Server, you specify which workloads are assigned to which volumes.</span></span> <span data-ttu-id="2bb5a-175">Por ejemplo, puede establecer volúmenes costosos que admiten un gran número de operaciones de entrada/salida por segundo (IOPS) para almacenar solo las cargas de trabajo que requieren copias de seguridad frecuentes y de gran volumen.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="2bb5a-176">Un ejemplo es SQL Server con registros de transacciones.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="2bb5a-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="2bb5a-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="2bb5a-178">Para actualizar las propiedades de un volumen en el grupo de almacenamiento de Backup Server, use el cmdlet de PowerShell Update-DPMDiskStorage.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-178">To update the properties of a volume in the storage pool in Backup Server, use the PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="2bb5a-179">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="2bb5a-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="2bb5a-180">Todos los cambios que realice mediante PowerShell se reflejarán en la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-180">All changes that you make by using PowerShell are reflected in the UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="2bb5a-181">Proteger orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="2bb5a-181">Protect data sources</span></span>
<span data-ttu-id="2bb5a-182">Para empezar a proteger los orígenes de datos, cree un grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-182">To begin protecting data sources, create a protection group.</span></span> <span data-ttu-id="2bb5a-183">En los pasos siguientes se muestran cambios o adiciones en el Asistente para nuevo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-183">The following steps highlight changes or additions to the New Protection Group wizard.</span></span>

<span data-ttu-id="2bb5a-184">Para crear un grupo de protección:</span><span class="sxs-lookup"><span data-stu-id="2bb5a-184">To create a protection group:</span></span>

1. <span data-ttu-id="2bb5a-185">En la consola de administrador de Backup Server, seleccione **Protección**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-185">In the Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="2bb5a-186">En la cinta de herramientas, seleccione **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-186">On the tool ribbon, select **New**.</span></span>

    <span data-ttu-id="2bb5a-187">Se abre el Asistente para crear nuevo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-187">This opens the Create New Protection Group wizard.</span></span>

  ![Asistente para crear nuevo grupo de protección](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="2bb5a-189">En la página **principal**, seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-189">On the **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="2bb5a-190">En la página **Seleccionar tipo de grupo de protección**, elija el tipo de grupo de protección que quiere crear y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-190">On the **Select Protection Group Type** page, select the type of protection group you want to create, and then select **Next**.</span></span>

  ![Página Seleccionar tipo de grupo de protección](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="2bb5a-192">En la página **Seleccionar miembros del grupo**, en el panel **Miembros disponibles**, se muestran los miembros con agentes de protección.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-192">On the **Select Group Members** page, in the **Available members** pane, the members with protection agents are listed.</span></span> <span data-ttu-id="2bb5a-193">Para este ejemplo, seleccione el volumen D:\ y E:\ y agréguelos al panel **Miembros seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-193">For this example, select volume D:\ and E:\ and add them to the **Selected members** pane.</span></span> <span data-ttu-id="2bb5a-194">Seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-194">Select **Next**.</span></span>

  ![Página Seleccionar miembros del grupo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="2bb5a-196">En la página **Seleccionar método de protección de datos**, escriba el **Nombre del grupo de protección**, seleccione el método de protección y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-196">On the **Select Data Protection Method** page, enter a **Protection group name**, select the protection method, and then select **Next**.</span></span> <span data-ttu-id="2bb5a-197">Si quiere protección a corto plazo, debe seleccionar el método de copia de seguridad **Disco**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-197">If you want short-term protection, you must select the **Disk** backup method.</span></span>

  ![Página Seleccionar método de protección de datos](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="2bb5a-199">En la página **Especificar objetivos a corto plazo**, seleccione los detalles de **Duración de retención** y **Frecuencia de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-199">On the **Specify Short-Term Goals** page, select the details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="2bb5a-200">Después, seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-200">Then, select **Next**.</span></span> <span data-ttu-id="2bb5a-201">Opcionalmente, para cambiar la programación en la que se toman los puntos de recuperación, seleccione **Modificar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-201">Optionally, to change the schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Página Especificar objetivos a corto plazo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="2bb5a-203">En la página **Revisar la asignación del almacenamiento en disco**, revise los detalles de los orígenes de datos que ha seleccionado, su tamaño y los valores del espacio que se aprovisionará y del volumen de almacenamiento de destino.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-203">On the **Review Disk Storage Allocation** page, review details about the data sources you selected, their size, and  values for the space to be provisioned and the target storage volume.</span></span>

  ![Página Revisar la asignación del almacenamiento en disco](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="2bb5a-205">Los volúmenes de almacenamiento se basan en la asignación de volumen de carga de trabajo (que se establece mediante PowerShell) y el almacenamiento disponible.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-205">Storage volumes are based on the workload volume allocation (set by using PowerShell) and the available storage.</span></span> <span data-ttu-id="2bb5a-206">Para cambiar los volúmenes de almacenamiento, seleccione otros volúmenes en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-206">You can change the storage volumes by selecting other volumes in the drop-down menu.</span></span> <span data-ttu-id="2bb5a-207">Si cambia el valor de **Almacenamiento de destino**, el valor de **Almacenamiento en disco disponible** cambiará dinámicamente para reflejar los valores de **Espacio disponible** y **Underprovisioned Space** (Espacio insuficiente).</span><span class="sxs-lookup"><span data-stu-id="2bb5a-207">If you change the value for **Target Storage**, the value for **Available disk storage** dynamically changes to reflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="2bb5a-208">Si los orígenes de datos aumentan según lo previsto, el valor de la columna **Underprovisioned Space** (Espacio insuficiente) de **Almacenamiento en disco disponible** refleja la cantidad de almacenamiento adicional que se necesita.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-208">If the data sources grow as planned, the value for the **Underprovisioned Space** column in **Available disk storage** reflects the amount of additional storage that's needed.</span></span> <span data-ttu-id="2bb5a-209">Use este valor como ayuda a la hora de planear las necesidades de almacenamiento para realizar copias de seguridad sin problemas.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-209">Use this value to help plan your storage needs for smooth backups.</span></span> <span data-ttu-id="2bb5a-210">Si el valor es cero, no se prevén problemas relacionados con el almacenamiento en un futuro inmediato.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-210">If the value is zero, there are no potential problems with storage in the foreseeable future.</span></span> <span data-ttu-id="2bb5a-211">Si el valor es distinto de cero, no tiene suficiente espacio de almacenamiento asignado (según la directiva de protección y el tamaño de los datos de los miembros protegidos).</span><span class="sxs-lookup"><span data-stu-id="2bb5a-211">If the value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and the data size of your protected members).</span></span>

  ![Almacenamiento en disco subasignado](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="2bb5a-213">Para acabar de crear el grupo de protección, complete el asistente.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-213">To finish creating your protection group, complete the wizard.</span></span>

## <a name="migrate-legacy-storage-to-modern-backup-storage"></a><span data-ttu-id="2bb5a-214">Migrar el almacenamiento heredado a Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="2bb5a-214">Migrate legacy storage to Modern Backup Storage</span></span>
<span data-ttu-id="2bb5a-215">Después de instalar Backup Server v2 o actualizar a esta versión, y después de actualizar el sistema operativo a Windows Server 2016, actualice los grupos de protección para que usen Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-215">After you upgrade to or install Backup Server v2 and upgrade the operating system to Windows Server 2016, update your protection groups to use Modern Backup Storage.</span></span> <span data-ttu-id="2bb5a-216">De forma predeterminada, los grupos de protección no se cambian.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="2bb5a-217">Siguen funcionando tal como se han configurado inicialmente.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-217">They continue to function as they were initially set up.</span></span> 

<span data-ttu-id="2bb5a-218">La actualización de los grupos de protección para que usen Modern Backup Storage es opcional.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-218">Updating protection groups to use Modern Backup Storage is optional.</span></span> <span data-ttu-id="2bb5a-219">Para actualizar el grupo de protección, detenga la protección de todos los orígenes de datos mediante la opción de conservar datos.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-219">To update the protection group, stop protection of all data sources by using the retain data option.</span></span> <span data-ttu-id="2bb5a-220">Después, agregue los orígenes de datos a un nuevo grupo de protección.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-220">Then, add the data sources to a new protection group.</span></span>

1. <span data-ttu-id="2bb5a-221">En la consola de administrador, seleccione la característica **Protección**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-221">In the Administrator Console, select the **Protection** feature.</span></span> <span data-ttu-id="2bb5a-222">En la lista **Miembro del grupo de protección**, haga clic con el botón derecho en el miembro y seleccione **Detener protección de miembro**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-222">In the **Protection Group Member** list, right-click the member, and then select **Stop protection of member**.</span></span>

  ![Detener protección de miembro](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="2bb5a-224">En el cuadro de diálogo **Quitar del grupo**, revise el espacio en disco usado y el espacio disponible para el grupo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-224">In the **Remove from Group** dialog box, review the used disk space and the available free space for the storage pool.</span></span> <span data-ttu-id="2bb5a-225">El valor predeterminado es dejar los puntos de recuperación en el disco y permitirles expirar según su directiva de retención asociada.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-225">The default is to leave the recovery points on the disk and allow them to expire per their associated retention policy.</span></span> <span data-ttu-id="2bb5a-226">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-226">Click **OK**.</span></span>

  <span data-ttu-id="2bb5a-227">Si quiere devolver de inmediato el espacio en disco usado al grupo de almacenamiento libre, active la casilla **Eliminar réplica en disco** para eliminar los datos de copia de seguridad (y los puntos de recuperación) asociados a ese miembro.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-227">If you want to immediately return the used disk space to the free storage pool, select the **Delete replica on disk** check box to delete the backup data (and recovery points) associated with that member.</span></span>

  ![Cuadro de diálogo Quitar del grupo](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="2bb5a-229">Cree un grupo de protección que use Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="2bb5a-230">Incluya los orígenes de datos no protegidos.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-230">Include the unprotected data sources.</span></span>


## <a name="add-disks-to-increase-legacy-storage"></a><span data-ttu-id="2bb5a-231">Agregar discos para aumentar el almacenamiento heredado</span><span class="sxs-lookup"><span data-stu-id="2bb5a-231">Add disks to increase legacy storage</span></span>

<span data-ttu-id="2bb5a-232">Si quiere usar el almacenamiento heredado con Backup Server, es posible que tenga que agregar discos para aumentar el almacenamiento heredado.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-232">If you want to use legacy storage with Backup Server, you might need to add disks to increase legacy storage.</span></span> 

<span data-ttu-id="2bb5a-233">Para agregar almacenamiento en disco:</span><span class="sxs-lookup"><span data-stu-id="2bb5a-233">To add disk storage:</span></span>

1. <span data-ttu-id="2bb5a-234">En la consola de administrador, seleccione **Administración** > **Almacenamiento en disco** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-234">In the Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Cuadro de diálogo Agregar almacenamiento en disco](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="2bb5a-236">En el cuadro de diálogo **Agregar almacenamiento en disco**, seleccione **Agregar discos**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-236">In the **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="2bb5a-237">En la lista de discos disponibles, seleccione los discos que quiera agregar y haga clic en **Agregar** y en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-237">In the list of available disks, select the disks you want to add, select **Add**, and then select **OK**.</span></span>

## <a name="update-the-data-protection-manager-protection-agent"></a><span data-ttu-id="2bb5a-238">Actualizar el agente de protección de Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="2bb5a-238">Update the Data Protection Manager protection agent</span></span>

<span data-ttu-id="2bb5a-239">Backup Server usa el agente de protección de System Center Data Protection Manager para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-239">Backup Server uses the System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="2bb5a-240">Si va a actualizar un agente de protección que no está conectado a la red, no podrá usar la consola de administrador de Data Protection Manager para completar una actualización de agente conectado.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-240">If you are upgrading a protection agent that is not connected to the network, you cannot use the Data Protection Manager Administrator Console to complete a connected agent upgrade.</span></span> <span data-ttu-id="2bb5a-241">Debe actualizar el agente de protección en un entorno de dominio que no esté activo.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-241">You must upgrade the protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="2bb5a-242">Mientras el equipo cliente no se conecte a la red, la actualización del agente de protección aparecerá como pendiente en la consola de administrador de Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-242">Until the client computer is connected to the network, the Data Protection Manager Administrator Console shows that the protection agent update is pending.</span></span>

<span data-ttu-id="2bb5a-243">En las secciones siguientes se describe cómo se actualizan los agentes de protección de equipos cliente conectados y no conectados.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-243">The following sections describe how to update protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="2bb5a-244">Actualizar un agente de protección de un equipo cliente conectado</span><span class="sxs-lookup"><span data-stu-id="2bb5a-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="2bb5a-245">En la consola de administrador de Backup Server, seleccione **Administración** > **Agentes**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-245">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="2bb5a-246">En el panel de información, seleccione los equipos cliente cuyo agente de protección quiere actualizar.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-246">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2bb5a-247">En la columna **Actualizaciones del agente** se indica cuándo está disponible una actualización del agente de protección para cada equipo protegido.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-247">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="2bb5a-248">En el panel **Acciones**, la acción **Actualización** solo está disponible cuando se selecciona un equipo protegido y las actualizaciones están disponibles.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-248">In the **Actions** pane, the **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="2bb5a-249">Para instalar agentes de protección actualizados en los equipos seleccionados, en el panel **Acciones**, seleccione **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-249">To install updated protection agents on the selected computers, in the **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="2bb5a-250">Actualizar un agente de protección en un equipo cliente que no está conectado</span><span class="sxs-lookup"><span data-stu-id="2bb5a-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="2bb5a-251">En la consola de administrador de Backup Server, seleccione **Administración** > **Agentes**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-251">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="2bb5a-252">En el panel de información, seleccione los equipos cliente cuyo agente de protección quiere actualizar.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-252">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="2bb5a-253">En la columna **Actualizaciones del agente** se indica cuándo está disponible una actualización del agente de protección para cada equipo protegido.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-253">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="2bb5a-254">En el panel **Acciones**, la acción **Actualización** no está disponible cuando se selecciona un equipo protegido, a menos que haya actualizaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-254">In the **Actions** pane, the **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="2bb5a-255">Para instalar agentes de protección actualizados en los equipos seleccionados, haga clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-255">To install updated protection agents on the selected computers, select **Update**.</span></span>

4. <span data-ttu-id="2bb5a-256">Si un equipo cliente no está conectado a la red, aparecerá el estado **Actualización pendiente** en la columna **Estado del agente** mientras el equipo no se conecte a la red.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-256">For a client computer that is not connected to the network, until the computer is connected to the network, the **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="2bb5a-257">Una vez que el equipo cliente se conecte a la red, aparecerá el estado **Actualizando** en la columna **Actualizaciones del agente** para el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-257">After a client computer is connected to the network, the **Agent Updates** column for the client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-the-new-version-with-azure"></a><span data-ttu-id="2bb5a-258">Paso de los grupos de protección heredados de una versión antigua y sincronización de la nueva versión con Azure</span><span class="sxs-lookup"><span data-stu-id="2bb5a-258">Move legacy Protection groups from old version and sync the new version with Azure</span></span>

<span data-ttu-id="2bb5a-259">Una vez que Azure Backup Server y el sistema operativo están ambos actualizados, está listo para proteger los nuevos orígenes de datos con Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-259">Once Azure Backup Server and the OS are both updated, you are ready to protect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="2bb5a-260">Aunque los orígenes de datos ya protegidos seguirán estándolo del modo antiguo, como cuando usaban Azure Backup Server, en la nueva protección se usará Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-260">However already protected data sources will continue to be protected in the legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="2bb5a-261">En los pasos siguientes se migran los orígenes de datos del modo antiguo de protección a Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-261">Below steps are to migrate data sources from legacy  mode of protection to Modern backup storage.</span></span>

<span data-ttu-id="2bb5a-262">• Agregue los nuevos volúmenes al grupo de almacenamiento DPM y asigne etiquetas de origen de datos y nombres descriptivos, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-262">• Add the new volume(s) to the DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="2bb5a-263">• Para cada origen de datos que se encuentre en el modo antiguo, detenga la protección de los orígenes de datos y use la opción “Conservar datos protegidos”.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-263">• For each data source that is in legacy mode, stop protection of the data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="2bb5a-264">Así permitirá la recuperación de los puntos de recuperación antiguos después de la migración.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="2bb5a-265">• Cree un nuevo grupo de protección y seleccione los orígenes de datos que se almacenarán con el nuevo formato.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-265">• Create a new PG and select the data sources that are to be stored using new format.</span></span>
<span data-ttu-id="2bb5a-266">• DPM realizará localmente una copia de la réplica desde el almacenamiento de copia de seguridad antiguo en el volumen de Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-266">• DPM will do a replica copy from the legacy backup storage into the Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="2bb5a-267">Nota: Esto se verá como un trabajo de operación posterior a la recuperación • Todos los nuevos puntos de recuperación y sincronización se almacenarán entonces en Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="2bb5a-268">•Los puntos de recuperación antiguos se eliminarán cuando expiren y finalmente se liberará el espacio en disco.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-268">• Old recovery points will be pruned out as they expire and eventually free up the disk space.</span></span>
<span data-ttu-id="2bb5a-269">• Una vez que se eliminan todos los volúmenes heredados del almacenamiento antiguo, el disco se puede quitar de Azure Backup y del sistema.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-269">• Once all the legacy volumes are deleted from the old storage, the disk can be removed from Azure backup and the system.</span></span>
<span data-ttu-id="2bb5a-270">• Realice una copia de seguridad de la base de datos DPM de Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-270">• Take a backup of the  Azure DPMDB.</span></span>

<span data-ttu-id="2bb5a-271">Parte 2: Elementos importantes. El nuevo servidor deberá tener mismo nombre que la instancia original de Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-271">Part 2: -Important items> The new server will need to be named same as the original Azure Backup server.</span></span> <span data-ttu-id="2bb5a-272">No se puede cambiar el nombre de la nueva instancia de Azure Backup Server, si desea usar el grupo de almacenamiento antiguo y la base de datos DPM para conservar los puntos de recuperación: debe tener la copia de seguridad de la base de datos DPM, ya que será necesario restaurarla.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-272">You cannot change the name of the new Azure backup server if you want to use old storage pool and DPMDB to retain recovery points -Must have backup of DPMDB  as it will need to be restored</span></span>

1) <span data-ttu-id="2bb5a-273">Cierre la instancia original de Azure Backup Server o desconéctela.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-273">Shutdown the original Azure backup server or take it off the wire.</span></span>
2) <span data-ttu-id="2bb5a-274">Restablezca la cuenta de máquina en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-274">Reset the machine account in active directory.</span></span>
3) <span data-ttu-id="2bb5a-275">Instale Server 2016 en un equipo nuevo y asígnele el mismo nombre de máquina que la instancia original de Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-275">Install Server 2016 on new machine and name it the same machine name as the original Azure Backup server.</span></span>
4) <span data-ttu-id="2bb5a-276">Únase al dominio</span><span class="sxs-lookup"><span data-stu-id="2bb5a-276">Join the Domain</span></span>
5) <span data-ttu-id="2bb5a-277">Instale Azure Backup Server V2 (mueva los discos del grupo de DPM Storage desde el servidor antiguo e impórtelos)</span><span class="sxs-lookup"><span data-stu-id="2bb5a-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="2bb5a-278">Restaure la base de datos DPM tomada al final de la parte 2</span><span class="sxs-lookup"><span data-stu-id="2bb5a-278">Restore the DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="2bb5a-279">Conecte el almacenamiento del servidor de copia de seguridad original al nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="2bb5a-279">Attach the storage from the original backup server to the new server.</span></span>
8) <span data-ttu-id="2bb5a-280">Desde SQL, restaure la base de datos DPM</span><span class="sxs-lookup"><span data-stu-id="2bb5a-280">From SQL Restore the DPMDB</span></span>
9) <span data-ttu-id="2bb5a-281">Desde la línea de comandos de administrador en el nuevo servidor, cambie al directorio de la ubicación de instalación de Microsoft Azure Backup y a la carpeta bin</span><span class="sxs-lookup"><span data-stu-id="2bb5a-281">From admin command line on new server cd to Microsoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="2bb5a-282">Ejemplo de ruta de acceso: C:\windows\system32>cd "c:\Archivos de programa\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="2bb5a-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="2bb5a-283">a Azure Backup. Ejecute DPMSYNC -SYNC</span><span class="sxs-lookup"><span data-stu-id="2bb5a-283">to Azure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="2bb5a-284">Ejecute DPMSYNC-SYNC Nota: Si ha agregado nuevos discos al bloque de almacenamiento DPM en lugar de mover los antiguos, ejecute DPMSYNC -Reallocatereplica</span><span class="sxs-lookup"><span data-stu-id="2bb5a-284">Run DPMSYNC -SYNC Note If you have added NEW disks to the DPM Storage pool instead of moving the old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="2bb5a-285">Nuevos cmdlets de PowerShell en v2</span><span class="sxs-lookup"><span data-stu-id="2bb5a-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="2bb5a-286">Cuando se instala Azure Backup Server v2, hay dos nuevos cmdlets disponibles:</span><span class="sxs-lookup"><span data-stu-id="2bb5a-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="2bb5a-287">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="2bb5a-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="2bb5a-288">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="2bb5a-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="2bb5a-289">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2bb5a-289">Next steps</span></span>

<span data-ttu-id="2bb5a-290">Obtenga información sobre cómo preparar el servidor o empezar a proteger la carga de trabajo:</span><span class="sxs-lookup"><span data-stu-id="2bb5a-290">Learn how to prepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="2bb5a-291">Preparar cargas de trabajo de Backup Server</span><span class="sxs-lookup"><span data-stu-id="2bb5a-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="2bb5a-292">Usar Backup Server para hacer una copia de seguridad de un servidor de VMware</span><span class="sxs-lookup"><span data-stu-id="2bb5a-292">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="2bb5a-293">Usar Backup Server para hacer una copia de seguridad de SQL Server</span><span class="sxs-lookup"><span data-stu-id="2bb5a-293">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="2bb5a-294">Usar Modern Backup Storage con Backup Server</span><span class="sxs-lookup"><span data-stu-id="2bb5a-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

