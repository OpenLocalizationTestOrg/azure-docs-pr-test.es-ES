---
title: "base de datos de Analysis Services aaaAzure de copia de seguridad y restauración | Documentos de Microsoft"
description: "Describe cómo toobackup y restauración un análisis de Azure de servicios de base de datos."
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
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="0c0db-103">Copia de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="0c0db-103">Backup and restore</span></span>

<span data-ttu-id="0c0db-104">Copia de seguridad de bases de datos de modelo tabular de Analysis Services de Azure es mucho Hola igual que en local de Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="0c0db-104">Backing up tabular model databases in Azure Analysis Services is much hello same as for on-premises Analysis Services.</span></span> <span data-ttu-id="0c0db-105">Hola principal diferencia es donde se almacenan los archivos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0c0db-105">hello primary difference is where you store your backup files.</span></span> <span data-ttu-id="0c0db-106">Archivos de copia de seguridad deben guardarse contenedor tooa en una [cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0c0db-106">Backup files must be saved tooa container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="0c0db-107">Puede usar una cuenta de almacenamiento y un contenedor que ya tenga o puede crear estos al configurar el almacenamiento para el servidor.</span><span class="sxs-lookup"><span data-stu-id="0c0db-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="0c0db-108">La creación de una cuenta de almacenamiento puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="0c0db-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="0c0db-109">más información, consulte toolearn [precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="0c0db-109">toolearn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="0c0db-110">Las copias de seguridad se guardan con extensión abf.</span><span class="sxs-lookup"><span data-stu-id="0c0db-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="0c0db-111">Para los modelos tabulares en memoria, se almacenan los datos y los metadatos del modelo.</span><span class="sxs-lookup"><span data-stu-id="0c0db-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="0c0db-112">Para los modelos tabulares de consulta directa, solo se almacenan los metadatos del modelo.</span><span class="sxs-lookup"><span data-stu-id="0c0db-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="0c0db-113">Las copias de seguridad se pueden comprimir y cifrar, según las opciones de Hola que elija.</span><span class="sxs-lookup"><span data-stu-id="0c0db-113">Backups can be compressed and encrypted, depending on hello options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="0c0db-114">Configuración de los valores de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="0c0db-114">Configure storage settings</span></span>
<span data-ttu-id="0c0db-115">Antes de realizar copias de seguridad, se necesita una configuración de almacenamiento tooconfigure para el servidor.</span><span class="sxs-lookup"><span data-stu-id="0c0db-115">Before backing up, you need tooconfigure storage settings for your server.</span></span>


### <a name="tooconfigure-storage-settings"></a><span data-ttu-id="0c0db-116">configuración de almacenamiento de tooconfigure</span><span class="sxs-lookup"><span data-stu-id="0c0db-116">tooconfigure storage settings</span></span>
1.  <span data-ttu-id="0c0db-117">En el portal de Azure > **Configuración**, haga clic en **Backup**.</span><span class="sxs-lookup"><span data-stu-id="0c0db-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Copias de seguridad en Configuración](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="0c0db-119">Haga clic en **Habilitado** y, luego, haga clic en **Configuración de Storage**.</span><span class="sxs-lookup"><span data-stu-id="0c0db-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Habilitar](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="0c0db-121">Seleccione su cuenta de almacenamiento o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="0c0db-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="0c0db-122">Seleccione un contenedor o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="0c0db-122">Select a container or create a new one.</span></span>

    ![Seleccionar el contenedor](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="0c0db-124">Guarde la configuración de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0c0db-124">Save your backup settings.</span></span>

    ![Guardar la configuración de copia de seguridad](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="0c0db-126">Backup</span><span class="sxs-lookup"><span data-stu-id="0c0db-126">Backup</span></span>

### <a name="toobackup-by-using-ssms"></a><span data-ttu-id="0c0db-127">toobackup mediante SSMS</span><span class="sxs-lookup"><span data-stu-id="0c0db-127">toobackup by using SSMS</span></span>

1. <span data-ttu-id="0c0db-128">En SSMS, haga clic con el botón derecho en una base de datos > **Copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="0c0db-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="0c0db-129">En **Copia de seguridad de la base de datos** > **Archivo de copia de seguridad**, haga clic en **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="0c0db-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="0c0db-130">Hola **Guardar archivo como** cuadro de diálogo, compruebe la ruta de acceso de carpeta de hello y, a continuación, escriba un nombre para el archivo de copia de seguridad de hello.</span><span class="sxs-lookup"><span data-stu-id="0c0db-130">In hello **Save file as** dialog, verify hello folder path, and then type a name for hello backup file.</span></span> 

4. <span data-ttu-id="0c0db-131">Hola **base de datos de copia de seguridad** cuadro de diálogo, seleccione opciones.</span><span class="sxs-lookup"><span data-stu-id="0c0db-131">In hello **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="0c0db-132">**Permite el archivo sobrescribir** -Seleccione este opción toooverwrite copias de hello mismo nombre.</span><span class="sxs-lookup"><span data-stu-id="0c0db-132">**Allow file overwrite** - Select this option toooverwrite backup files of hello same name.</span></span> <span data-ttu-id="0c0db-133">Si no se selecciona esta opción, que va a guardar el archivo de Hola no puede tener Hola mismo nombre como un archivo que ya existe en hello misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="0c0db-133">If this option is not selected, hello file you are saving cannot have hello same name as a file that already exists in hello same location.</span></span>

    <span data-ttu-id="0c0db-134">**Aplicar compresión** -Seleccione este archivo de copia de seguridad de opción toocompress Hola.</span><span class="sxs-lookup"><span data-stu-id="0c0db-134">**Apply compression** - Select this option toocompress hello backup file.</span></span> <span data-ttu-id="0c0db-135">Los archivos de copia de seguridad comprimidos ahorran espacio en disco, pero requieren un uso de CPU algo mayor.</span><span class="sxs-lookup"><span data-stu-id="0c0db-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="0c0db-136">**Cifrar archivo de copia de seguridad** -Seleccione este archivo de copia de seguridad de opción tooencrypt Hola.</span><span class="sxs-lookup"><span data-stu-id="0c0db-136">**Encrypt backup file** - Select this option tooencrypt hello backup file.</span></span> <span data-ttu-id="0c0db-137">Esta opción requiere un archivo de copia de seguridad de contraseña proporcionado por el usuario toosecure Hola.</span><span class="sxs-lookup"><span data-stu-id="0c0db-137">This option requires a user-supplied password toosecure hello backup file.</span></span> <span data-ttu-id="0c0db-138">contraseña de Hola evita la lectura de datos de copia de seguridad de saludo de alguna otra forma de una operación de restauración.</span><span class="sxs-lookup"><span data-stu-id="0c0db-138">hello password prevents reading of hello backup data any other means than a restore operation.</span></span> <span data-ttu-id="0c0db-139">Si elige las copias de seguridad tooencrypt, almacenar contraseña hello en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="0c0db-139">If you choose tooencrypt backups, store hello password in a safe location.</span></span>

5. <span data-ttu-id="0c0db-140">Haga clic en **Aceptar** toocreate y guarde el archivo de copia de seguridad de hello.</span><span class="sxs-lookup"><span data-stu-id="0c0db-140">Click **OK** toocreate and save hello backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="0c0db-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c0db-141">PowerShell</span></span>
<span data-ttu-id="0c0db-142">Use el cmdlet [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="0c0db-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="0c0db-143">Restauración</span><span class="sxs-lookup"><span data-stu-id="0c0db-143">Restore</span></span>
<span data-ttu-id="0c0db-144">Cuando se restaura, debe ser el archivo de copia de seguridad de cuenta de almacenamiento de Hola que ha configurado para el servidor.</span><span class="sxs-lookup"><span data-stu-id="0c0db-144">When restoring, your backup file must be in hello storage account you've configured for your server.</span></span> <span data-ttu-id="0c0db-145">Si necesita un archivo de copia de seguridad de una cuenta de almacenamiento local ubicación tooyour toomove, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) o hello [AzCopy](../storage/common/storage-use-azcopy.md) utilidad de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="0c0db-145">If you need toomove a backup file from an on-premises location tooyour storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or hello [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="0c0db-146">Si va a restaurar desde un servidor local, debe quitar todos los usuarios del dominio Hola de roles del modelo de Hola y agregarlos hacer copia de roles de toohello como usuarios de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c0db-146">If you're restoring from an on-premises server, you must remove all hello domain users from hello model's roles and add them back toohello roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="toorestore-by-using-ssms"></a><span data-ttu-id="0c0db-147">toorestore mediante SSMS</span><span class="sxs-lookup"><span data-stu-id="0c0db-147">toorestore by using SSMS</span></span>

1. <span data-ttu-id="0c0db-148">En SSMS, haga clic con el botón derecho en una base de datos > **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="0c0db-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="0c0db-149">Hola **base de datos de copia de seguridad** cuadro de diálogo, en **archivo de copia de seguridad**, haga clic en **examinar**.</span><span class="sxs-lookup"><span data-stu-id="0c0db-149">In hello **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="0c0db-150">Hola **buscar archivos de base de datos** cuadro de diálogo, seleccione Hola archivo toorestore.</span><span class="sxs-lookup"><span data-stu-id="0c0db-150">In hello **Locate Database Files** dialog, select hello file you want toorestore.</span></span>

4. <span data-ttu-id="0c0db-151">En **Restaurar base de datos**, seleccione la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c0db-151">In **Restore database**, select hello database.</span></span>

5. <span data-ttu-id="0c0db-152">Especifique las opciones.</span><span class="sxs-lookup"><span data-stu-id="0c0db-152">Specify options.</span></span> <span data-ttu-id="0c0db-153">Opciones de seguridad deben coincidir con opciones de copia de seguridad de Hola que usó al realizar copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0c0db-153">Security options must match hello backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="0c0db-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c0db-154">PowerShell</span></span>

<span data-ttu-id="0c0db-155">Use el cmdlet [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="0c0db-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="0c0db-156">Información relacionada</span><span class="sxs-lookup"><span data-stu-id="0c0db-156">Related information</span></span>

[<span data-ttu-id="0c0db-157">Cuentas de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="0c0db-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="0c0db-158">[Alta disponibilidad](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="0c0db-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="0c0db-159">Administración de Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="0c0db-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
