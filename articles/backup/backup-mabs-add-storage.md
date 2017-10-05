---
title: Uso de Modern Backup Storage con Azure Backup Server v2 | Microsoft Docs
description: "Obtenga información sobre las nuevas características de Azure Backup Server v2. En este artículo se describe cómo actualizar la instalación de la instancia de Backup Server."
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
ms.openlocfilehash: 751b9b495fd368dff1f72429707f5f33a0ccb569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-storage-to-azure-backup-server-v2"></a><span data-ttu-id="98817-104">Adición de almacenamiento a Azure Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="98817-104">Add storage to Azure Backup Server v2</span></span>

<span data-ttu-id="98817-105">Azure Backup Server v2 incluye Modern Backup Storage de System Center 2016 Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="98817-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="98817-106">Modern Backup Storage proporciona ahorros de almacenamiento de hasta el 50 por ciento, copias de seguridad que son tres veces más rápidas y un almacenamiento más eficaz.</span><span class="sxs-lookup"><span data-stu-id="98817-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="98817-107">También ofrece almacenamiento con reconocimiento de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="98817-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="98817-108">Para utilizar Modern Backup Storage, debe ejecutar Backup Server v2 en Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="98817-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="98817-109">Si ejecuta Backup Server v2 en una versión anterior de Windows Server, Azure Backup Server no puede sacar partido de Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="98817-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="98817-110">En su lugar, protege las cargas de trabajo como lo hace con Backup Server v1.</span><span class="sxs-lookup"><span data-stu-id="98817-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="98817-111">Para más información, consulte la [matriz de protección](backup-mabs-protection-matrix.md) de la versión de Backup Server.</span><span class="sxs-lookup"><span data-stu-id="98817-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="98817-112">Volúmenes en Backup Server v2</span><span class="sxs-lookup"><span data-stu-id="98817-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="98817-113">Backup Server v2 acepta volúmenes de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="98817-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="98817-114">Al agregar un volumen, Backup Server da formato al volumen en Sistema de archivos resistente (ReFS), que requiere Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="98817-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="98817-115">Para agregar un volumen y expandirlo más adelante si es necesario, se recomienda utilizar este flujo de trabajo:</span><span class="sxs-lookup"><span data-stu-id="98817-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="98817-116">Configure Backup Server v2 en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="98817-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="98817-117">Cree un volumen en un disco virtual en un grupo de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="98817-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="98817-118">Agregue un disco a un grupo de almacenamiento y cree un disco virtual con la distribución simple.</span><span class="sxs-lookup"><span data-stu-id="98817-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="98817-119">Agregue discos adicionales y extienda el disco virtual.</span><span class="sxs-lookup"><span data-stu-id="98817-119">Add any additional disks, and extend the virtual disk.</span></span>
    3.  <span data-ttu-id="98817-120">Cree volúmenes en el disco virtual.</span><span class="sxs-lookup"><span data-stu-id="98817-120">Create volumes on the virtual disk.</span></span>
3.  <span data-ttu-id="98817-121">Agregue los volúmenes a Backup Server.</span><span class="sxs-lookup"><span data-stu-id="98817-121">Add the volumes to Backup Server.</span></span>
4.  <span data-ttu-id="98817-122">Configure el almacenamiento con reconocimiento de la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="98817-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="98817-123">Creación de un volumen para Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="98817-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="98817-124">El uso de Backup Server v2 con volúmenes como almacenamiento en disco puede ayudarle a mantener el control sobre el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="98817-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="98817-125">Un volumen puede ser un único disco.</span><span class="sxs-lookup"><span data-stu-id="98817-125">A volume can be a single disk.</span></span> <span data-ttu-id="98817-126">Sin embargo, si desea extender el almacenamiento en el futuro, cree un volumen de un disco creado mediante el uso de espacios de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="98817-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="98817-127">Esto puede ayudarle si desea ampliar el volumen para el almacenamiento de copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="98817-127">This can help if you want to expand the volume for backup storage.</span></span> <span data-ttu-id="98817-128">En esta sección se ofrecen procedimientos recomendados para crear un volumen con esta configuración.</span><span class="sxs-lookup"><span data-stu-id="98817-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="98817-129">En Administrador del servidor, seleccione **Servicios de archivos y almacenamiento** > **Volúmenes** > **Grupos de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="98817-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="98817-130">En **DISCOS FÍSICOS**, seleccione **Nuevo grupo de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="98817-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Creación de un nuevo grupo de almacenamiento](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="98817-132">En el cuadro desplegable **TAREAS**, seleccione **Nuevo disco virtual**.</span><span class="sxs-lookup"><span data-stu-id="98817-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Adición de un disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="98817-134">Seleccione el grupo de almacenamiento y, después, seleccione **Agregar disco físico**.</span><span class="sxs-lookup"><span data-stu-id="98817-134">Select the storage pool, and then select **Add Physical Disk**.</span></span>

    ![Adición de un disco físico](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="98817-136">Seleccione el disco físico y, después, seleccione **Extender disco virtual**.</span><span class="sxs-lookup"><span data-stu-id="98817-136">Select the physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Extensión del disco virtual](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="98817-138">Seleccione el disco virtual y, después, seleccione **Nuevo volumen**.</span><span class="sxs-lookup"><span data-stu-id="98817-138">Select the virtual disk, and then select **New Volume**.</span></span>

    ![Creación de un nuevo volumen](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="98817-140">En el cuadro de diálogo **Seleccionar el servidor y el disco**, seleccione el servidor y el nuevo disco.</span><span class="sxs-lookup"><span data-stu-id="98817-140">In the **Select the server and disk** dialog, select the server and the new disk.</span></span> <span data-ttu-id="98817-141">A continuación, seleccione **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="98817-141">Then, select **Next**.</span></span>

    ![Selección del servidor y disco](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a><span data-ttu-id="98817-143">Adición de volúmenes al almacenamiento de disco de Backup Server</span><span class="sxs-lookup"><span data-stu-id="98817-143">Add volumes to Backup Server disk storage</span></span>

<span data-ttu-id="98817-144">Para agregar un volumen a Backup Server, en el panel **Administración**, vuelva a examinar el almacenamiento y, después, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="98817-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span></span> <span data-ttu-id="98817-145">Aparece una lista de todos los volúmenes disponibles para agregarse al almacenamiento de Backup Server.</span><span class="sxs-lookup"><span data-stu-id="98817-145">A list of all the volumes available to be added for Backup Server Storage appears.</span></span> <span data-ttu-id="98817-146">Después de que se hayan agregado los volúmenes disponibles a la lista de volúmenes seleccionados, puede asignarles un nombre descriptivo para facilitar su administración.</span><span class="sxs-lookup"><span data-stu-id="98817-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span></span> <span data-ttu-id="98817-147">Para dar formato a estos volúmenes en ReFS para que Backup Server pueda usar las ventajas de Modern Backup Storage, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="98817-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span></span>

![Adición de volúmenes disponibles](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="98817-149">Configuración del almacenamiento con reconocimiento de la carga de trabajo</span><span class="sxs-lookup"><span data-stu-id="98817-149">Set up workload-aware storage</span></span>

<span data-ttu-id="98817-150">Con el almacenamiento con reconocimiento de la carga de trabajo, puede seleccionar los volúmenes que almacenen de forma preferente ciertos tipos de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="98817-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="98817-151">Por ejemplo, puede establecer volúmenes costosos que admiten un gran número de operaciones de entrada/salida por segundo (IOPS) para almacenar solo las cargas de trabajo que requieren copias de seguridad frecuentes y de gran volumen.</span><span class="sxs-lookup"><span data-stu-id="98817-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="98817-152">Un ejemplo es SQL Server con registros de transacciones.</span><span class="sxs-lookup"><span data-stu-id="98817-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="98817-153">Otras cargas de trabajo que se almacenan en copias de seguridad con menos frecuencia, como máquinas virtuales, pueden ser guardadas en volúmenes de bajo coste.</span><span class="sxs-lookup"><span data-stu-id="98817-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="98817-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="98817-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="98817-155">Puede configurar el almacenamiento con reconocimiento de la carga de trabajo mediante el cmdlet de PowerShell Update-DPMDiskStorage, que actualiza las propiedades de un volumen en el bloque de almacenamiento en un servidor de Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="98817-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="98817-156">Sintaxis:</span><span class="sxs-lookup"><span data-stu-id="98817-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="98817-157">En la captura de pantalla siguiente se muestra el cmdlet Update-DPMDiskStorage en la ventana de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98817-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span></span>

![El comando Update-DPMDiskStorage en la ventana de PowerShell](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="98817-159">Los cambios que realice con PowerShell se reflejan en la consola de administrador de Backup Server.</span><span class="sxs-lookup"><span data-stu-id="98817-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span></span>

![Discos y volúmenes en la consola de administrador](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="98817-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="98817-161">Next steps</span></span>
<span data-ttu-id="98817-162">Después de instalar Backup Server, sepa cómo preparar el servidor o empezar a proteger la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="98817-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="98817-163">Preparar cargas de trabajo de Backup Server</span><span class="sxs-lookup"><span data-stu-id="98817-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="98817-164">Usar Backup Server para hacer una copia de seguridad de un servidor de VMware</span><span class="sxs-lookup"><span data-stu-id="98817-164">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="98817-165">Uso de Backup Server para hacer una copia de seguridad de SQL Server</span><span class="sxs-lookup"><span data-stu-id="98817-165">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)

