---
title: Montaje de Azure File Storage en una VM de Windows de Azure | Microsoft Docs
description: "Almacene archivos en la nube con Azure File Storage y monte un recurso compartido de archivos de nube en una máquina virtual (VM) de Azure."
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
ms.openlocfilehash: 6ffb2d2da1e2439df6f5da543411e3c2c68d3435
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="b9489-103">Uso de recursos compartidos de archivos de Azure con máquinas virtuales de Windows</span><span class="sxs-lookup"><span data-stu-id="b9489-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="b9489-104">Puede usar recursos compartidos de archivos de Azure como una forma de almacenar archivos y acceder a ellos desde la VM.</span><span class="sxs-lookup"><span data-stu-id="b9489-104">You can use Azure file shares as a way to store and access files from your VM.</span></span> <span data-ttu-id="b9489-105">Por ejemplo, puede almacenar un script o un archivo de configuración de la aplicación que quiera que todas las máquinas virtuales compartan.</span><span class="sxs-lookup"><span data-stu-id="b9489-105">For example, you can store a script or an application configuration file that you want all your VMs to share.</span></span> <span data-ttu-id="b9489-106">En este tema, se muestra cómo crear un recurso compartido de archivos de Azure y cómo cargar y descargar archivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-106">In this topic, we show you how to create and mount an Azure file share, and how to upload and download files.</span></span>

## <a name="connect-to-a-file-share-from-a-vm"></a><span data-ttu-id="b9489-107">Conexión a un recurso compartido desde una VM</span><span class="sxs-lookup"><span data-stu-id="b9489-107">Connect to a file share from a VM</span></span>

<span data-ttu-id="b9489-108">En esta sección se da por supuesto que ya tiene un recurso compartido de archivos al que quiere conectarse.</span><span class="sxs-lookup"><span data-stu-id="b9489-108">This section assumes you already have a file share that you want to connect to.</span></span> <span data-ttu-id="b9489-109">Si tiene que crear uno, vea [Creación de un recurso compartido de archivos](#create-a-file-share) más adelante en este capítulo.</span><span class="sxs-lookup"><span data-stu-id="b9489-109">If you need to create one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="b9489-110">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b9489-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b9489-111">En el menú de la izquierda, haga clic en **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="b9489-111">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="b9489-112">Elija la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b9489-112">Choose your storage account.</span></span>
4. <span data-ttu-id="b9489-113">En la página **Información general**, en **Servicios**, seleccione **Archivos**.</span><span class="sxs-lookup"><span data-stu-id="b9489-113">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="b9489-114">Seleccione un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-114">Select a file share.</span></span>
6. <span data-ttu-id="b9489-115">Haga clic en **Conectar** para abrir una página que muestra la sintaxis de línea de comandos para el montaje de recursos compartidos de archivos de Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="b9489-115">Click **Connect** to open a page that shows the command-line syntax for mounting the file share from Windows or Linux.</span></span>
7. <span data-ttu-id="b9489-116">Resalte la sintaxis del comando y péguela en el Bloc de notas o en otro lugar donde pueda acceder fácilmente a ella.</span><span class="sxs-lookup"><span data-stu-id="b9489-116">Highlight the syntax of the command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="b9489-117">Modifique la sintaxis para quitar el **> ** inicial y reemplazar *[letra de unidad]* por la letra de unidad (por ejemplo, **Y:**) donde quiere montar el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-117">Edit the syntax to remove the leading **> ** and replace *[drive letter]* with the drive letter (for example, **Y:**) where you would like to mount the file share.</span></span>
8. <span data-ttu-id="b9489-118">Conéctese a la máquina virtual y abra un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="b9489-118">Connect to your VM and open a command prompt.</span></span>
9. <span data-ttu-id="b9489-119">Pegue la sintaxis de conexión modificada y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="b9489-119">Paste in the edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="b9489-120">Una vez creada la conexión, se recibe el mensaje **El comando se ha completado correctamente.**</span><span class="sxs-lookup"><span data-stu-id="b9489-120">When the connection has been created, you get the message **The command completed successfully.**</span></span>
11. <span data-ttu-id="b9489-121">Compruebe la conexión escribiendo la letra de unidad para cambiar a esa unidad de disco y escriba **dir** para ver el contenido del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-121">Check the connection by typing in the drive letter to switch to that drive and then type **dir** to see the contents of the file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="b9489-122">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="b9489-122">Create a file share</span></span> 
1. <span data-ttu-id="b9489-123">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b9489-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b9489-124">En el menú de la izquierda, haga clic en **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="b9489-124">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="b9489-125">Elija la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b9489-125">Choose your storage account.</span></span>
4. <span data-ttu-id="b9489-126">En la página **Información general**, en **Servicios**, seleccione **Archivos**.</span><span class="sxs-lookup"><span data-stu-id="b9489-126">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="b9489-127">En la página de servicio de archivos, haga clic en **+ recurso compartido de archivos** para crear su primer recurso compartido de archivos.\\</span><span class="sxs-lookup"><span data-stu-id="b9489-127">In the File Service page, click **+ File share** to create your first file share.\\</span></span>
6. <span data-ttu-id="b9489-128">Rellene el nombre del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-128">Fill in the file share name.</span></span> <span data-ttu-id="b9489-129">Pueden usarse minúsculas, números y guiones individuales en los nombres de recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="b9489-130">El nombre no puede empezar por un guion y no se pueden usar varios guiones consecutivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-130">The name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="b9489-131">Rellene un límite para el tamaño máximo del archivo, hasta 5120 GB.</span><span class="sxs-lookup"><span data-stu-id="b9489-131">Fill in a limit on how large the file can be, up to 5120 GB.</span></span>
8. <span data-ttu-id="b9489-132">Haga clic en **Aceptar** para implementar el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-132">Click **OK** to deploy the file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="b9489-133">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="b9489-133">Upload files</span></span>
1. <span data-ttu-id="b9489-134">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b9489-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b9489-135">En el menú de la izquierda, haga clic en **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="b9489-135">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="b9489-136">Elija la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b9489-136">Choose your storage account.</span></span>
4. <span data-ttu-id="b9489-137">En la página **Información general**, en **Servicios**, seleccione **Archivos**.</span><span class="sxs-lookup"><span data-stu-id="b9489-137">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="b9489-138">Seleccione un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-138">Select a file share.</span></span>
6. <span data-ttu-id="b9489-139">Haga clic en **Cargar** para abrir la página **Cargar archivos**.</span><span class="sxs-lookup"><span data-stu-id="b9489-139">Click **Upload** to open the **Upload files** page.</span></span>
7. <span data-ttu-id="b9489-140">Haga clic en el icono de carpeta para buscar el archivo que quiere cargar en el sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="b9489-140">Click on the folder icon to browse your local file system for a file to upload.</span></span>   
8. <span data-ttu-id="b9489-141">Haga clic en **Cargar** para cargar el archivo en el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-141">Click **Upload** to upload the file to the file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="b9489-142">Descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="b9489-142">Download files</span></span>
1. <span data-ttu-id="b9489-143">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b9489-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b9489-144">En el menú de la izquierda, haga clic en **Cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="b9489-144">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="b9489-145">Elija la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b9489-145">Choose your storage account.</span></span>
4. <span data-ttu-id="b9489-146">En la página **Información general**, en **Servicios**, seleccione **Archivos**.</span><span class="sxs-lookup"><span data-stu-id="b9489-146">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="b9489-147">Seleccione un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="b9489-147">Select a file share.</span></span>
6. <span data-ttu-id="b9489-148">Haga clic con el botón derecho en un archivo y elija **Descargar** para descargarlo en una máquina local.</span><span class="sxs-lookup"><span data-stu-id="b9489-148">Right-click on the file and choose **Download** to download it to your local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="b9489-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b9489-149">Next steps</span></span>

<span data-ttu-id="b9489-150">También puede crear y administrar recursos compartidos de archivos con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9489-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="b9489-151">Para más información, vea [Introducción a Azure File Storage en Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="b9489-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
