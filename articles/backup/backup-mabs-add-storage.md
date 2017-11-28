---
title: aaaUse moderna de copia de seguridad de almacenamiento con el servidor de copia de seguridad de Azure v2 | Documentos de Microsoft
description: "Obtenga información sobre las nuevas características de hello en el servidor de copia de seguridad de Azure v2. Este artículo se describe cómo tooupgrade la instalación del servidor de copia de seguridad."
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
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="f15f3-104">Agregar almacenamiento tooAzure v2 del servidor de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="f15f3-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="f15f3-105">Azure Backup Server v2 incluye Modern Backup Storage de System Center 2016 Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="f15f3-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="f15f3-106">Modern Backup Storage proporciona ahorros de almacenamiento de hasta el 50 por ciento, copias de seguridad que son tres veces más rápidas y un almacenamiento más eficaz.</span><span class="sxs-lookup"><span data-stu-id="f15f3-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="f15f3-107">También ofrece almacenamiento con reconocimiento de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f15f3-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="f15f3-108">toouse moderna almacenamiento de copia de seguridad, debe ejecutar v2 del servidor de copia de seguridad en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f15f3-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="f15f3-109">Si ejecuta Backup Server v2 en una versión anterior de Windows Server, Azure Backup Server no puede sacar partido de Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="f15f3-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="f15f3-110">En su lugar, protege las cargas de trabajo como lo hace con Backup Server v1.</span><span class="sxs-lookup"><span data-stu-id="f15f3-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="f15f3-111">Para obtener más información, vea la versión del servidor de copia de seguridad de hello [matriz protección](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="f15f3-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="f15f3-112">Volúmenes en Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="f15f3-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="f15f3-113">Backup Server v2 acepta volúmenes de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f15f3-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="f15f3-114">Al agregar un volumen, el servidor de copia de seguridad da formato a Hola volumen tooResilient sistema de archivos (ReFS), que requiere almacenamiento de copia de seguridad actual.</span><span class="sxs-lookup"><span data-stu-id="f15f3-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="f15f3-115">tooadd un volumen y tooexpand que más adelante si es necesitan, se recomienda que utilice este flujo de trabajo:</span><span class="sxs-lookup"><span data-stu-id="f15f3-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="f15f3-116">Configure Backup Server v2 en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f15f3-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="f15f3-117">Cree un volumen en un disco virtual en un grupo de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="f15f3-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="f15f3-118">Agregar un grupo de almacenamiento de disco tooa y crear un disco virtual con el diseño simple.</span><span class="sxs-lookup"><span data-stu-id="f15f3-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="f15f3-119">Agregar discos adicionales y extender disco virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="f15f3-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="f15f3-120">Crear volúmenes en el disco virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f15f3-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="f15f3-121">Agregar Hola volúmenes tooBackup Server.</span><span class="sxs-lookup"><span data-stu-id="f15f3-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="f15f3-122">Configure el almacenamiento con reconocimiento de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f15f3-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="f15f3-123">Creación de un volumen para Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="f15f3-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="f15f3-124">El uso de Backup Server v2 con volúmenes como almacenamiento en disco puede ayudarle a mantener el control sobre el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f15f3-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="f15f3-125">Un volumen puede ser un único disco.</span><span class="sxs-lookup"><span data-stu-id="f15f3-125">A volume can be a single disk.</span></span> <span data-ttu-id="f15f3-126">Sin embargo, si desea tooextend almacenamiento Hola futuras, crear un volumen en un disco creado mediante el uso de espacios de almacenamiento insuficiente.</span><span class="sxs-lookup"><span data-stu-id="f15f3-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="f15f3-127">Esto puede ayudar a si desea tooexpand volumen de hello para el almacenamiento de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f15f3-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="f15f3-128">En esta sección se ofrecen procedimientos recomendados para crear un volumen con esta configuración.</span><span class="sxs-lookup"><span data-stu-id="f15f3-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="f15f3-129">En Administrador del servidor, seleccione **Servicios de archivos y almacenamiento** > **Volúmenes** > **Grupos de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="f15f3-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="f15f3-130">En **DISCOS FÍSICOS**, seleccione **Nuevo grupo de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="f15f3-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Creación de un nuevo grupo de almacenamiento](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="f15f3-132">Hola **tareas** cuadro de lista desplegable, seleccione **nuevo disco Virtual**.</span><span class="sxs-lookup"><span data-stu-id="f15f3-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Adición de un disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="f15f3-134">Seleccione el grupo de almacenamiento de hello y, a continuación, seleccione **Agregar disco físico**.</span><span class="sxs-lookup"><span data-stu-id="f15f3-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![Adición de un disco físico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="f15f3-136">Seleccione disco físico de hello y, a continuación, seleccione **extender disco Virtual**.</span><span class="sxs-lookup"><span data-stu-id="f15f3-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Extender disco virtual Hola](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="f15f3-138">Seleccione el disco virtual de hello y, a continuación, seleccione **nuevo volumen**.</span><span class="sxs-lookup"><span data-stu-id="f15f3-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![Creación de un nuevo volumen](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="f15f3-140">Hola **Seleccionar servidor de Hola y el disco** cuadro de diálogo, el servidor de select Hola y el nuevo disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="f15f3-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="f15f3-141">Después, seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f15f3-141">Then, select **Next**.</span></span>

    ![Seleccione el disco y el servidor de Hola](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="f15f3-143">Agregar almacenamiento en disco volúmenes tooBackup Server</span><span class="sxs-lookup"><span data-stu-id="f15f3-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="f15f3-144">un volumen tooBackup Server, en hello tooadd **administración** panel, vuelva a examinar almacenamiento hello y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="f15f3-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="f15f3-145">Aparece una lista de todos los Hola volúmenes disponibles toobe agregado para el almacenamiento del servidor de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f15f3-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="f15f3-146">Después de volúmenes disponibles se agregan toohello lista de los volúmenes seleccionados, puede asignarles un toohelp nombre descriptivo que se administran.</span><span class="sxs-lookup"><span data-stu-id="f15f3-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="f15f3-147">tooformat estas tooReFS de volúmenes para copia de seguridad de servidor puede usar los beneficios de Hola de almacenamiento de copia de seguridad moderna, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f15f3-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![Adición de volúmenes disponibles](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="f15f3-149">Configuración del almacenamiento con reconocimiento de la carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="f15f3-149">Set up workload-aware storage</span></span>

<span data-ttu-id="f15f3-150">Con el almacenamiento de carga de trabajo, puede seleccionar volúmenes de Hola que almacenan de forma preferente ciertos tipos de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f15f3-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="f15f3-151">Por ejemplo, puede establecer volúmenes costosos que admiten un gran número de operaciones de entrada/salida por segundo (IOPS) toostore solo hello las cargas de trabajo que requieren copias de seguridad frecuentes de gran volumen.</span><span class="sxs-lookup"><span data-stu-id="f15f3-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="f15f3-152">Un ejemplo es SQL Server con registros de transacciones.</span><span class="sxs-lookup"><span data-stu-id="f15f3-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="f15f3-153">Otras cargas de trabajo que se copian con menos frecuencia, al igual que las máquinas virtuales, pueden hacer copia de volúmenes de costo toolow.</span><span class="sxs-lookup"><span data-stu-id="f15f3-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="f15f3-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="f15f3-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="f15f3-155">Puede configurar el almacenamiento con identificación de la carga de trabajo mediante Hola PowerShell cmdlet Update-DPMDiskStorage, que actualiza las propiedades de Hola de un volumen en el bloque de almacenamiento de hello en un servidor de Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="f15f3-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="f15f3-156">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="f15f3-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="f15f3-157">Hello captura de pantalla siguiente muestra hello DPMDiskStorage actualización cmdlet en la ventana de PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="f15f3-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![Hola DPMDiskStorage de actualización de comandos en la ventana de PowerShell de hello](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="f15f3-159">cambios de Hola que realice mediante el uso de PowerShell se reflejan en hello consola de administrador del servidor de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f15f3-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![Discos y volúmenes de hello consola de administrador](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="f15f3-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f15f3-161">Next steps</span></span>
<span data-ttu-id="f15f3-162">Después de instalar el servidor de copia de seguridad, obtenga información acerca de cómo tooprepare el servidor, o empezar a proteger una carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f15f3-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="f15f3-163">Preparar cargas de trabajo de Backup Server</span><span class="sxs-lookup"><span data-stu-id="f15f3-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="f15f3-164">Usar tooback del servidor de copia de seguridad de un servidor de VMware</span><span class="sxs-lookup"><span data-stu-id="f15f3-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="f15f3-165">Usar tooback del servidor de copia de seguridad de SQL Server</span><span class="sxs-lookup"><span data-stu-id="f15f3-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

