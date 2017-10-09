---
title: aaaMount almacenamiento de archivos de Azure desde una VM de Windows Azure | Documentos de Microsoft
description: "Almacene el archivo en la nube de hello con almacenamiento de archivos de Azure y montar el recurso compartido de archivos de nube desde una máquina virtual (VM) de Azure."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="9b6a5-103">Uso de recursos compartidos de archivos de Azure con máquinas virtuales de Windows</span><span class="sxs-lookup"><span data-stu-id="9b6a5-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="9b6a5-104">Puede usar recursos compartidos de archivos de Azure como los archivos de toostore y acceso de una forma de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-104">You can use Azure file shares as a way toostore and access files from your VM.</span></span> <span data-ttu-id="9b6a5-105">Por ejemplo, puede almacenar una secuencia de comandos o un archivo de configuración de aplicación que desea que su tooshare de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-105">For example, you can store a script or an application configuration file that you want all your VMs tooshare.</span></span> <span data-ttu-id="9b6a5-106">En este tema, le mostramos cómo toocreate y montaje un Azure recurso compartido de archivos y cómo tooupload y descarga los archivos.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-106">In this topic, we show you how toocreate and mount an Azure file share, and how tooupload and download files.</span></span>

## <a name="connect-tooa-file-share-from-a-vm"></a><span data-ttu-id="9b6a5-107">Conectar el recurso compartido de archivos de tooa de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9b6a5-107">Connect tooa file share from a VM</span></span>

<span data-ttu-id="9b6a5-108">En esta sección se da por supuesto que ya tiene un archivo de recurso compartido que desee tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-108">This section assumes you already have a file share that you want tooconnect to.</span></span> <span data-ttu-id="9b6a5-109">Si necesita toocreate uno, consulte [crear un recurso compartido de archivos](#create-a-file-share) más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-109">If you need toocreate one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="9b6a5-110">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b6a5-110">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b6a5-111">En el menú de la izquierda hello, haga clic en **cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-111">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="9b6a5-112">Elija la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-112">Choose your storage account.</span></span>
4. <span data-ttu-id="9b6a5-113">Hola **Introducción** página, en **servicios**, seleccione **archivos**.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-113">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="9b6a5-114">Seleccione un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-114">Select a file share.</span></span>
6. <span data-ttu-id="9b6a5-115">Haga clic en **conectar** tooopen una página que muestra la sintaxis de línea de comandos de hello para el montaje Hola el recurso compartido de archivos de Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-115">Click **Connect** tooopen a page that shows hello command-line syntax for mounting hello file share from Windows or Linux.</span></span>
7. <span data-ttu-id="9b6a5-116">Resalte Hola sintaxis de comando de Hola y péguelo en el Bloc de notas o en otro lugar donde se puede acceder fácilmente a ella.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-116">Highlight hello syntax of hello command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="9b6a5-117">Editar líder en hello sintaxis tooremove Hola ** > ** y reemplace *[letra de unidad]* con una letra de unidad de hello (por ejemplo, **Y:**) que desee que el recurso compartido de archivos de toomount Hola.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-117">Edit hello syntax tooremove hello leading **> ** and replace *[drive letter]* with hello drive letter (for example, **Y:**) where you would like toomount hello file share.</span></span>
8. <span data-ttu-id="9b6a5-118">Conéctese tooyour VM y abra un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-118">Connect tooyour VM and open a command prompt.</span></span>
9. <span data-ttu-id="9b6a5-119">Pegar en hello editado la sintaxis de la conexión y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-119">Paste in hello edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="9b6a5-120">Cuando se ha creado la conexión de hello, obtendrá un mensaje de bienvenida de **Hola comando se completó correctamente.**</span><span class="sxs-lookup"><span data-stu-id="9b6a5-120">When hello connection has been created, you get hello message **hello command completed successfully.**</span></span>
11. <span data-ttu-id="9b6a5-121">Compruebe la conexión de hello escribiendo en hello letra tooswitch toothat la unidad y, a continuación, escriba **dir** toosee contenido de Hola Hola recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-121">Check hello connection by typing in hello drive letter tooswitch toothat drive and then type **dir** toosee hello contents of hello file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="9b6a5-122">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="9b6a5-122">Create a file share</span></span> 
1. <span data-ttu-id="9b6a5-123">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b6a5-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b6a5-124">En el menú de la izquierda hello, haga clic en **cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-124">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="9b6a5-125">Elija la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-125">Choose your storage account.</span></span>
4. <span data-ttu-id="9b6a5-126">Hola **Introducción** página, en **servicios**, seleccione **archivos**.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-126">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="9b6a5-127">En la página de servicio de archivos de hello, haga clic en **+ recurso compartido de archivos** toocreate compartir el primer archivo. \\</span><span class="sxs-lookup"><span data-stu-id="9b6a5-127">In hello File Service page, click **+ File share** toocreate your first file share.\\</span></span>
6. <span data-ttu-id="9b6a5-128">Rellene el nombre de recurso compartido de archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-128">Fill in hello file share name.</span></span> <span data-ttu-id="9b6a5-129">Pueden usarse minúsculas, números y guiones individuales en los nombres de recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="9b6a5-130">Hola nombre no puede empezar con un guión y no se puede usar varios guiones consecutivos.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-130">hello name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="9b6a5-131">Puede estar relleno en un límite de tamaño archivo hello, too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-131">Fill in a limit on how large hello file can be, up too5120 GB.</span></span>
8. <span data-ttu-id="9b6a5-132">Haga clic en **Aceptar** recurso compartido de archivos de toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-132">Click **OK** toodeploy hello file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="9b6a5-133">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="9b6a5-133">Upload files</span></span>
1. <span data-ttu-id="9b6a5-134">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b6a5-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b6a5-135">En el menú de la izquierda hello, haga clic en **cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-135">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="9b6a5-136">Elija la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-136">Choose your storage account.</span></span>
4. <span data-ttu-id="9b6a5-137">Hola **Introducción** página, en **servicios**, seleccione **archivos**.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-137">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="9b6a5-138">Seleccione un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-138">Select a file share.</span></span>
6. <span data-ttu-id="9b6a5-139">Haga clic en **cargar** tooopen hello **cargar archivos** página.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-139">Click **Upload** tooopen hello **Upload files** page.</span></span>
7. <span data-ttu-id="9b6a5-140">Haga clic en toobrowse de icono de carpeta de hello su sistema de archivos local para un tooupload de archivo.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-140">Click on hello folder icon toobrowse your local file system for a file tooupload.</span></span>   
8. <span data-ttu-id="9b6a5-141">Haga clic en **cargar** recurso compartido de archivos de tooupload Hola archivo toohello.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-141">Click **Upload** tooupload hello file toohello file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="9b6a5-142">Descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="9b6a5-142">Download files</span></span>
1. <span data-ttu-id="9b6a5-143">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b6a5-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b6a5-144">En el menú de la izquierda hello, haga clic en **cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-144">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="9b6a5-145">Elija la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-145">Choose your storage account.</span></span>
4. <span data-ttu-id="9b6a5-146">Hola **Introducción** página, en **servicios**, seleccione **archivos**.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-146">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="9b6a5-147">Seleccione un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-147">Select a file share.</span></span>
6. <span data-ttu-id="9b6a5-148">Haga doble clic en el archivo hello y elija **descargar** toodownload se tooyour de equipo local.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-148">Right-click on hello file and choose **Download** toodownload it tooyour local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="9b6a5-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b6a5-149">Next steps</span></span>

<span data-ttu-id="9b6a5-150">También puede crear y administrar recursos compartidos de archivos con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b6a5-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="9b6a5-151">Para más información, vea [Introducción a Azure File Storage en Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="9b6a5-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
