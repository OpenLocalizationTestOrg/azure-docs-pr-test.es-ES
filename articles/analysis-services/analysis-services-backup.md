---
title: "Copia de seguridad y restauración de bases de datos de Azure Analysis Services | Microsoft Docs"
description: "Se describe cómo realizar una copia de seguridad de una base de datos de Azure Analysis Services y restaurarla."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: bffa481a498b130ef1f2388a5ba856da5d164ee0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="63e9d-103">Copia de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="63e9d-103">Backup and restore</span></span>

<span data-ttu-id="63e9d-104">Realizar una copia de seguridad de bases de datos de modelo tabular en Azure Analysis Services es casi lo mismo que en Analysis Services local.</span><span class="sxs-lookup"><span data-stu-id="63e9d-104">Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services.</span></span> <span data-ttu-id="63e9d-105">La diferencia principal es el lugar donde se almacenan los archivos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63e9d-105">The primary difference is where you store your backup files.</span></span> <span data-ttu-id="63e9d-106">Los archivos de copia de seguridad se deben guardar en un contenedor de una [cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="63e9d-106">Backup files must be saved to a container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="63e9d-107">Puede usar una cuenta de almacenamiento y un contenedor que ya tenga o puede crear estos al configurar el almacenamiento para el servidor.</span><span class="sxs-lookup"><span data-stu-id="63e9d-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="63e9d-108">La creación de una cuenta de almacenamiento puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="63e9d-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="63e9d-109">Para más información, consulte [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="63e9d-109">To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="63e9d-110">Las copias de seguridad se guardan con extensión abf.</span><span class="sxs-lookup"><span data-stu-id="63e9d-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="63e9d-111">Para los modelos tabulares en memoria, se almacenan los datos y los metadatos del modelo.</span><span class="sxs-lookup"><span data-stu-id="63e9d-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="63e9d-112">Para los modelos tabulares de consulta directa, solo se almacenan los metadatos del modelo.</span><span class="sxs-lookup"><span data-stu-id="63e9d-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="63e9d-113">Las copias de seguridad se pueden comprimir y cifrar, según las opciones que elija.</span><span class="sxs-lookup"><span data-stu-id="63e9d-113">Backups can be compressed and encrypted, depending on the options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="63e9d-114">Configuración de los valores de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="63e9d-114">Configure storage settings</span></span>
<span data-ttu-id="63e9d-115">Antes de realizar copias de seguridad, debe configurar los valores de almacenamiento para el servidor.</span><span class="sxs-lookup"><span data-stu-id="63e9d-115">Before backing up, you need to configure storage settings for your server.</span></span>


### <a name="to-configure-storage-settings"></a><span data-ttu-id="63e9d-116">Para configurar los valores de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="63e9d-116">To configure storage settings</span></span>
1.  <span data-ttu-id="63e9d-117">En el portal de Azure > **Configuración**, haga clic en **Backup**.</span><span class="sxs-lookup"><span data-stu-id="63e9d-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Copias de seguridad en Configuración](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="63e9d-119">Haga clic en **Habilitado** y, luego, haga clic en **Configuración de Storage**.</span><span class="sxs-lookup"><span data-stu-id="63e9d-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Habilitar](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="63e9d-121">Seleccione su cuenta de almacenamiento o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="63e9d-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="63e9d-122">Seleccione un contenedor o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="63e9d-122">Select a container or create a new one.</span></span>

    ![Seleccionar el contenedor](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="63e9d-124">Guarde la configuración de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63e9d-124">Save your backup settings.</span></span>

    ![Guardar la configuración de copia de seguridad](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="63e9d-126">Backup</span><span class="sxs-lookup"><span data-stu-id="63e9d-126">Backup</span></span>

### <a name="to-backup-by-using-ssms"></a><span data-ttu-id="63e9d-127">Para realizar una copia de seguridad mediante SSMS:</span><span class="sxs-lookup"><span data-stu-id="63e9d-127">To backup by using SSMS</span></span>

1. <span data-ttu-id="63e9d-128">En SSMS, haga clic con el botón derecho en una base de datos > **Copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="63e9d-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="63e9d-129">En **Copia de seguridad de la base de datos** > **Archivo de copia de seguridad**, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="63e9d-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="63e9d-130">En el cuadro de diálogo **Guardar archivo como**, compruebe la ruta de acceso de la carpeta y luego escriba un nombre para el archivo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63e9d-130">In the **Save file as** dialog, verify the folder path, and then type a name for the backup file.</span></span> 

4. <span data-ttu-id="63e9d-131">En el cuadro de diálogo **Copia de seguridad de la base de datos**, seleccione opciones.</span><span class="sxs-lookup"><span data-stu-id="63e9d-131">In the **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="63e9d-132">**Permitir la sobrescritura de archivos**: seleccione esta opción para sobrescribir archivos de copia de seguridad del mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="63e9d-132">**Allow file overwrite** - Select this option to overwrite backup files of the same name.</span></span> <span data-ttu-id="63e9d-133">Si no se selecciona esta opción, el archivo que se guarde no podrá tener el mismo nombre que un archivo que ya exista en la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="63e9d-133">If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.</span></span>

    <span data-ttu-id="63e9d-134">**Aplicar compresión**: seleccione esta opción para comprimir el archivo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63e9d-134">**Apply compression** - Select this option to compress the backup file.</span></span> <span data-ttu-id="63e9d-135">Los archivos de copia de seguridad comprimidos ahorran espacio en disco, pero requieren un uso de CPU algo mayor.</span><span class="sxs-lookup"><span data-stu-id="63e9d-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="63e9d-136">**Cifrar archivo de copia de seguridad**: seleccione esta opción para cifrar el archivo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63e9d-136">**Encrypt backup file** - Select this option to encrypt the backup file.</span></span> <span data-ttu-id="63e9d-137">Esta opción requiere una contraseña suministrada por el usuario para proteger el archivo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63e9d-137">This option requires a user-supplied password to secure the backup file.</span></span> <span data-ttu-id="63e9d-138">La contraseña impide la lectura de los datos de copia de seguridad por cualquier medio que no sea una operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="63e9d-138">The password prevents reading of the backup data any other means than a restore operation.</span></span> <span data-ttu-id="63e9d-139">Si elige cifrar las copias de seguridad, almacene la contraseña en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="63e9d-139">If you choose to encrypt backups, store the password in a safe location.</span></span>

5. <span data-ttu-id="63e9d-140">Haga clic en **Aceptar** para crear y guardar el archivo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63e9d-140">Click **OK** to create and save the backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="63e9d-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="63e9d-141">PowerShell</span></span>
<span data-ttu-id="63e9d-142">Use el cmdlet [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="63e9d-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="63e9d-143">Restauración</span><span class="sxs-lookup"><span data-stu-id="63e9d-143">Restore</span></span>
<span data-ttu-id="63e9d-144">Para la restauración, el archivo de copia de seguridad debe estar en la cuenta de almacenamiento que configurada para el servidor.</span><span class="sxs-lookup"><span data-stu-id="63e9d-144">When restoring, your backup file must be in the storage account you've configured for your server.</span></span> <span data-ttu-id="63e9d-145">Si debe mover un archivo de copia de seguridad de una ubicación local a la cuenta de almacenamiento, utilice [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) o la utilidad de línea de comandos [AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="63e9d-145">If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="63e9d-146">Si va a restaurar desde un servidor local, debe quitar todos los usuarios del dominio de los roles del modelo y agregarlos de nuevo a los roles como usuarios de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="63e9d-146">If you're restoring from an on-premises server, you must remove all the domain users from the model's roles and add them back to the roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="to-restore-by-using-ssms"></a><span data-ttu-id="63e9d-147">Para realizar la restauración con SSMS:</span><span class="sxs-lookup"><span data-stu-id="63e9d-147">To restore by using SSMS</span></span>

1. <span data-ttu-id="63e9d-148">En SSMS, haga clic con el botón derecho en una base de datos > **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="63e9d-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="63e9d-149">En el cuadro de diálogo **Copia de seguridad de la base de datos**, en **Archivo de copia de seguridad**, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="63e9d-149">In the **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="63e9d-150">En el cuadro de diálogo **Buscar archivos de base de datos**, seleccione el archivo que quiere restaurar.</span><span class="sxs-lookup"><span data-stu-id="63e9d-150">In the **Locate Database Files** dialog, select the file you want to restore.</span></span>

4. <span data-ttu-id="63e9d-151">En **Restaurar base de datos**, seleccione la base de datos.</span><span class="sxs-lookup"><span data-stu-id="63e9d-151">In **Restore database**, select the database.</span></span>

5. <span data-ttu-id="63e9d-152">Especifique las opciones.</span><span class="sxs-lookup"><span data-stu-id="63e9d-152">Specify options.</span></span> <span data-ttu-id="63e9d-153">Las opciones de seguridad deben coincidir con las opciones de copia de seguridad que usó al realizar copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63e9d-153">Security options must match the backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="63e9d-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="63e9d-154">PowerShell</span></span>

<span data-ttu-id="63e9d-155">Use el cmdlet [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="63e9d-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="63e9d-156">Información relacionada</span><span class="sxs-lookup"><span data-stu-id="63e9d-156">Related information</span></span>

[<span data-ttu-id="63e9d-157">Cuentas de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="63e9d-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="63e9d-158">[Alta disponibilidad](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="63e9d-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="63e9d-159">Administración de Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="63e9d-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
