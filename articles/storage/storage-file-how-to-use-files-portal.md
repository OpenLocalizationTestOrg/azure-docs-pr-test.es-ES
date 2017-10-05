---
title: "Administración de Azure File Storage desde Azure Portal | Microsoft Docs"
description: Aprenda a usar Azure Portal para administrar Azure File Storage.
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
ms.openlocfilehash: d8ffb4359b0efe8da2f3bccb81c987bdeedf1a39
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-use-azure-file-storage-from-the-azure-portal"></a><span data-ttu-id="730a4-103">Uso de Azure File Storage desde Azure Portal</span><span class="sxs-lookup"><span data-stu-id="730a4-103">How to use Azure File storage from the Azure Portal</span></span>
<span data-ttu-id="730a4-104">[Azure Portal](https://portal.azure.com) ofrece una interfaz de usuario para la administración de Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="730a4-104">The [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="730a4-105">Puede realizar las siguientes acciones desde el explorador web:</span><span class="sxs-lookup"><span data-stu-id="730a4-105">You can perform the following actions from your web browser:</span></span>

* <span data-ttu-id="730a4-106">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="730a4-106">Create a File Share</span></span>
* <span data-ttu-id="730a4-107">Cargar y descargar archivos al recurso compartido de archivos y desde este.</span><span class="sxs-lookup"><span data-stu-id="730a4-107">Upload and download files to and from your file share.</span></span>
* <span data-ttu-id="730a4-108">Supervisar el uso real de cada recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="730a4-108">Monitor the actual usage of each file share.</span></span>
* <span data-ttu-id="730a4-109">Ajustar la cuota de tamaño del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="730a4-109">Adjust the file share size quota.</span></span>
* <span data-ttu-id="730a4-110">Copiar los comandos necesarios para montar el recurso compartido de archivos desde un cliente Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="730a4-110">Copy the mount commands to use to mount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="730a4-111">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="730a4-111">Create file share</span></span>
1. <span data-ttu-id="730a4-112">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="730a4-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="730a4-113">En el menú de navegación, haga clic en **Cuentas de almacenamiento** o **Cuentas de almacenamiento (clásico)**.</span><span class="sxs-lookup"><span data-stu-id="730a4-113">On the navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Captura de pantalla que muestra cómo crear un recurso compartido de archivos en el portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="730a4-115">Elija la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="730a4-115">Choose your storage account.</span></span>

    ![Captura de pantalla que muestra cómo crear un recurso compartido de archivos en el portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="730a4-117">Elija el servicio "Archivos".</span><span class="sxs-lookup"><span data-stu-id="730a4-117">Choose "Files" service.</span></span>

    ![Captura de pantalla que muestra cómo crear un recurso compartido de archivos en el portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="730a4-119">Haga clic en "Recursos compartidos de archivos" y siga el vínculo para crear su primer recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="730a4-119">Click "File shares" and follow the link to create your first file share.</span></span>

    ![Captura de pantalla que muestra cómo crear un recurso compartido de archivos en el portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="730a4-121">Rellene el nombre del recurso compartido de archivos y su tamaño (hasta 5120 GB) para crear su primer recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="730a4-121">Fill in the file share name and the size of the file share (up to 5120 GB) to create your first file share.</span></span> <span data-ttu-id="730a4-122">Una vez que se ha creado el recurso compartido de archivos, se puede montar desde cualquier sistema de archivos que admita SMB 2.1 o SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="730a4-122">Once the file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="730a4-123">Puede hacer clic en **Cuota** en el recurso compartido de archivos para cambiar el tamaño del archivo hasta 5120 GB.</span><span class="sxs-lookup"><span data-stu-id="730a4-123">You could click on **Quota** on the file share to change the size of the file up to 5120 GB.</span></span> <span data-ttu-id="730a4-124">Consulte la [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/) para estimar el costo de almacenamiento con Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="730a4-124">Please refer to [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) to estimate the storage cost of using Azure File storage.</span></span>

    ![Captura de pantalla que muestra cómo crear un recurso compartido de archivos en el portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="730a4-126">Carga y descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="730a4-126">Upload and download files</span></span>
1. <span data-ttu-id="730a4-127">Elija un recurso compartido de archivos creado previamente.</span><span class="sxs-lookup"><span data-stu-id="730a4-127">Choose one file share your have already created.</span></span>

    ![Captura de pantalla que muestra cómo cargar y descargar archivos desde el portal](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="730a4-129">Haga clic en **Cargar** para abrir la interfaz de usuario para cargar los archivos.</span><span class="sxs-lookup"><span data-stu-id="730a4-129">Click **Upload** to open the user interface for files uploading.</span></span>

    ![Captura de pantalla que muestra cómo cargar archivos desde el portal](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-to-file-share"></a><span data-ttu-id="730a4-131">Conexión al recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="730a4-131">Connect to file share</span></span>
-  <span data-ttu-id="730a4-132">Haga clic en **Conectar** para obtener la línea de comandos necesaria para montar el recurso compartido de archivos desde Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="730a4-132">Click **Connect** to get the command line for mounting the file share from Windows and Linux.</span></span> <span data-ttu-id="730a4-133">Los usuarios de Linux también pueden hacer referencia a [Uso de Azure File Storage con Linux](storage-how-to-use-files-linux.md) para obtener instrucciones adicionales de montaje para otras distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="730a4-133">For Linux users, you can also refer to [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Captura de pantalla que muestra cómo montar el recurso compartido de archivos](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="730a4-135">Puede copiar los comandos para el montaje del recurso compartido de archivos en Windows o Linux y ejecutarlos desde la máquina virtual de Azure o el equipo local.</span><span class="sxs-lookup"><span data-stu-id="730a4-135">You can copy the commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Captura de pantalla que muestra los comandos de montaje para Windows y Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="730a4-137">**Sugerencia:**</span><span class="sxs-lookup"><span data-stu-id="730a4-137">**Tip:**</span></span>  
<span data-ttu-id="730a4-138">Para obtener la clave de acceso de la cuenta de almacenamiento necesaria para el montaje, haga clic en **Ver las claves de acceso de esta cuenta de almacenamiento** en la parte inferior de la página Conectar.</span><span class="sxs-lookup"><span data-stu-id="730a4-138">To find the storage account access key for mounting, click on **View access keys for this storage account** at the bottom of the connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="730a4-139">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="730a4-139">See also</span></span>
<span data-ttu-id="730a4-140">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="730a4-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="730a4-141">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="730a4-141">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="730a4-142">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="730a4-142">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)