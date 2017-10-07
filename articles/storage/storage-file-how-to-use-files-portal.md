---
title: aaaHow toomanage almacenamiento de archivos de Azure de hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de almacenamiento de archivos de Azure de toouse hello toomanage de portal de Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="725bd-103">¿Cómo toouse almacenamiento de archivos de Azure de Hola Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="725bd-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="725bd-104">Hola [portal de Azure](https://portal.azure.com) proporciona una interfaz de usuario para administrar el almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="725bd-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="725bd-105">Puede realizar Hola siguientes acciones desde el explorador web:</span><span class="sxs-lookup"><span data-stu-id="725bd-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="725bd-106">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="725bd-106">Create a File Share</span></span>
* <span data-ttu-id="725bd-107">Cargar y descargar archivos tooand desde el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="725bd-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="725bd-108">Supervisar el uso real de hello cada recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="725bd-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="725bd-109">Ajuste la cuota de tamaño del recurso compartido de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="725bd-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="725bd-110">Copie Hola montaje comandos toouse toomount compartir el archivo desde un cliente de Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="725bd-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="725bd-111">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="725bd-111">Create file share</span></span>
1. <span data-ttu-id="725bd-112">Inicie sesión en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="725bd-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="725bd-113">En el menú de navegación de hello, haga clic en **cuentas de almacenamiento** o **cuentas de almacenamiento (clásica)**.</span><span class="sxs-lookup"><span data-stu-id="725bd-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Captura de pantalla que muestra cómo compartir archivos toocreate en el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="725bd-115">Elija la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="725bd-115">Choose your storage account.</span></span>

    ![Captura de pantalla que muestra cómo compartir archivos toocreate en el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="725bd-117">Elija el servicio "Archivos".</span><span class="sxs-lookup"><span data-stu-id="725bd-117">Choose "Files" service.</span></span>

    ![Captura de pantalla que muestra cómo compartir archivos toocreate en el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="725bd-119">Haga clic en "Recursos compartidos de archivos" y siga Hola vínculo toocreate compartir el primer archivo.</span><span class="sxs-lookup"><span data-stu-id="725bd-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![Captura de pantalla que muestra cómo compartir archivos toocreate en el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="725bd-121">Rellene los nombre de recurso compartido de archivos de Hola y el tamaño de Hola de toocreate de recurso compartido (arriba too5120 GB) del archivo de hello su primer recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="725bd-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="725bd-122">Una vez que se ha creado el recurso compartido de archivos de hello, se puede montar desde cualquier sistema de archivos compatible con SMB 2.1 o SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="725bd-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="725bd-123">Puede hacer clic en **cuota** Hola archivo recurso compartido toochange Hola tamaño de archivo hello too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="725bd-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="725bd-124">Consulte demasiado[Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/) costo de almacenamiento de información de hello tooestimate del uso de almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="725bd-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![Captura de pantalla que muestra cómo compartir archivos toocreate en el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="725bd-126">Carga y descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="725bd-126">Upload and download files</span></span>
1. <span data-ttu-id="725bd-127">Elija un recurso compartido de archivos creado previamente.</span><span class="sxs-lookup"><span data-stu-id="725bd-127">Choose one file share your have already created.</span></span>

    ![Captura de pantalla que muestra cómo tooupload y descarga los archivos de Hola portal](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="725bd-129">Haga clic en **cargar** para abrir la interfaz de usuario de Hola para cargar los archivos.</span><span class="sxs-lookup"><span data-stu-id="725bd-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![Captura de pantalla que muestra cómo se tooupload los archivos desde el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="725bd-131">Conectar el recurso compartido de toofile</span><span class="sxs-lookup"><span data-stu-id="725bd-131">Connect toofile share</span></span>
-  <span data-ttu-id="725bd-132">Haga clic en **conectar** para obtener la línea de comandos de Hola para el recurso compartido de archivos de montaje Hola de Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="725bd-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="725bd-133">Para los usuarios de Linux, también puede hacer referencia demasiado[cómo toouse almacenamiento de archivos de Azure con Linux](storage-how-to-use-files-linux.md) para obtener más instrucciones de montaje para otras distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="725bd-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Captura de pantalla que muestra cómo toomount Hola recurso compartido de archivos](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="725bd-135">Puede copiar Hola comandos para montar el archivo de recurso compartido en Windows o Linux y ejecución desde la máquina local o de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="725bd-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Captura de pantalla que muestra comandos de montaje de Hola para Windows y Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="725bd-137">**Sugerencia:**</span><span class="sxs-lookup"><span data-stu-id="725bd-137">**Tip:**</span></span>  
<span data-ttu-id="725bd-138">clave de acceso de cuenta de almacenamiento de toofind hello para el montaje, haga clic en **teclas de acceso de vista para esta cuenta de almacenamiento** final Hola de hello página Conectar.</span><span class="sxs-lookup"><span data-stu-id="725bd-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="725bd-139">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="725bd-139">See also</span></span>
<span data-ttu-id="725bd-140">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="725bd-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="725bd-141">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="725bd-141">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="725bd-142">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="725bd-142">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)