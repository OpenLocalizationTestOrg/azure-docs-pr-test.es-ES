---
title: aaaUpload VHD archivo laboratorios de desarrollo y pruebas de tooAzure mediante el Explorador de almacenamiento de Microsoft Azure | Documentos de Microsoft
description: Cargar la cuenta de almacenamiento del toolab del archivo de disco duro virtual mediante el Explorador de almacenamiento de Microsoft Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="baea2-103">Cargar la cuenta de almacenamiento del toolab del archivo de disco duro virtual mediante el Explorador de almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="baea2-103">Upload VHD file toolab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="baea2-104">En los laboratorios de desarrollo y pruebas de Azure, archivos de disco duro virtual pueden ser toocreate usa imágenes personalizadas, que son máquinas virtuales de tooprovision usado.</span><span class="sxs-lookup"><span data-stu-id="baea2-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="baea2-105">Este artículo se explica cómo toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) cuenta de almacenamiento del laboratorio de tooa de archivos tooupload un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="baea2-105">This article illustrates how toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="baea2-106">Una vez que haya cargado el archivo VHD, Hola [pasos siguientes sección](#next-steps) enumera algunos artículos que ilustran cómo toocreate una imagen personalizada de hello carga archivo de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="baea2-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="baea2-107">Para más información sobre discos y discos duros virtuales en Azure, consulte [Acerca de los discos y los discos duros virtuales para máquinas virtuales](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="baea2-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="baea2-108">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="baea2-108">Step-by-step instructions</span></span>

<span data-ttu-id="baea2-109">Hola después de recorrido de pasos a través de la carga de un disco duro virtual archivo laboratorios tooDevTest con [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="baea2-109">hello following steps walk you through uploading a VHD file tooDevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="baea2-110">[Descargue e instale la versión más reciente de Hola de hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="baea2-110">[Download and install hello latest version of hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="baea2-111">Obtener nombre de Hola de cuenta de almacenamiento del laboratorio de hello mediante Hola portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="baea2-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

    1. <span data-ttu-id="baea2-112">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="baea2-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="baea2-113">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="baea2-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
    
    1. <span data-ttu-id="baea2-114">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="baea2-114">From hello list of labs, select hello desired lab.</span></span>  
    
    1. <span data-ttu-id="baea2-115">En la hoja del laboratorio de hello, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="baea2-115">On hello lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="baea2-116">En el laboratorio de hello **configuración** hoja, seleccione **imágenes personalizadas (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="baea2-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="baea2-117">En hello **imágenes personalizadas** hoja, seleccione **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="baea2-117">On hello **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="baea2-118">En hello **imagen personalizada** hoja, seleccione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="baea2-118">On hello **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="baea2-119">En hello **VHD** hoja, seleccione **cargar un VHD con PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="baea2-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Carga del VHD mediante PowerShell][0]
    
    1. <span data-ttu-id="baea2-121">Hola **cargar una imagen con PowerShell** hoja muestra una llamada toohello **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="baea2-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="baea2-122">Hola primer parámetro (*destino*) contiene el nombre de cuenta de almacenamiento de Hola para laboratorio Hola Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="baea2-122">hello first parameter (*Destination*) contains hello storage account name for hello lab in hello following format:</span></span>
    
        <span data-ttu-id="baea2-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="baea2-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="baea2-124">Tome nota del nombre de cuenta de almacenamiento de hello tal como se utiliza en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="baea2-124">Make note of hello storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="baea2-125">Conectar tooan cuenta de suscripción de Azure mediante el Explorador de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="baea2-125">Connect tooan Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="baea2-126">El Explorador de Storage admite varias opciones de conexión.</span><span class="sxs-lookup"><span data-stu-id="baea2-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="baea2-127">Esta sección muestra la cuenta de almacenamiento tooa conexión asociada a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="baea2-127">This section illustrates connecting tooa storage account associated with your Azure subscription.</span></span> <span data-ttu-id="baea2-128">toosee Hola otras opciones de conexión admitidos por el Explorador de almacenamiento, consulte el artículo toohello, [introducción con el Explorador de almacenamiento](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="baea2-128">toosee hello other connection options supported by Storage Explorer, refer toohello article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="baea2-129">Abra el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="baea2-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="baea2-130">En el Explorador de Storage, seleccione **Azure Account settings** (Configuración de la cuenta de Azure).</span><span class="sxs-lookup"><span data-stu-id="baea2-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Configuración de la cuenta de Azure][1]
    
    1. <span data-ttu-id="baea2-132">panel izquierdo de Hello muestra las cuentas de Microsoft de Hola que ha iniciado la sesión.</span><span class="sxs-lookup"><span data-stu-id="baea2-132">hello left pane displays hello Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="baea2-133">cuenta de tooconnect tooanother, seleccione **agregar una cuenta**y siga hello toosign de cuadros de diálogo con una cuenta de Microsoft que está asociada con al menos una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="baea2-133">tooconnect tooanother account, select **Add an account**, and follow hello dialogs toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Agregar una cuenta][2]
    
    1. <span data-ttu-id="baea2-135">Una vez que inicie sesión correctamente con una cuenta de Microsoft, panel izquierdo de hello rellena con hello Azure suscripciones asociadas a esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="baea2-135">Once you successfully sign in with a Microsoft account, hello left pane populates with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="baea2-136">Seleccione Hola suscripciones de Azure con el que desea toowork y, a continuación, seleccione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="baea2-136">Select hello Azure subscriptions with which you want toowork, and then select **Apply**.</span></span> <span data-ttu-id="baea2-137">(Seleccione **todas las suscripciones** alterna Hola selección de todo o enumera ningún hello las suscripciones de Azure.)</span><span class="sxs-lookup"><span data-stu-id="baea2-137">(Selecting **All subscriptions** toggles hello selection of all or none of hello listed Azure subscriptions.)</span></span>
    
        ![Selección de suscripciones de Azure][3]
    
    1. <span data-ttu-id="baea2-139">panel izquierdo de Hello muestra las cuentas de almacenamiento de hello asociadas con suscripciones de Azure Hola seleccionado.</span><span class="sxs-lookup"><span data-stu-id="baea2-139">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>
    
        ![Suscripciones de Azure seleccionadas][4]

1. <span data-ttu-id="baea2-141">Busque la cuenta de almacenamiento del laboratorio de hello:</span><span class="sxs-lookup"><span data-stu-id="baea2-141">Locate hello lab's storage account:</span></span>

    1. <span data-ttu-id="baea2-142">En el panel izquierdo del explorador de almacenamiento de hello, busque y expanda el nodo de Hola para suscripción de Azure que posee el laboratorio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="baea2-142">In hello Storage Explorer left pane, locate, and expand hello node for hello Azure subscription that owns hello lab.</span></span>
    
    1. <span data-ttu-id="baea2-143">En el nodo de la suscripción de hello, expanda **cuentas de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="baea2-143">Under hello subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="baea2-144">Expandir los nodos del laboratorio de hello almacenamiento cuenta nodo tooreveal para **contenedores de blobs**, **recursos compartidos de archivos**, **colas**, y **tablas**.</span><span class="sxs-lookup"><span data-stu-id="baea2-144">Expand hello lab's storage account node tooreveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="baea2-145">Expanda hello **contenedores de blobs** nodo.</span><span class="sxs-lookup"><span data-stu-id="baea2-145">Expand hello **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="baea2-146">Seleccionar toodisplay del contenedor de blob de hello cargas de su contenido en el panel derecho de Hola.</span><span class="sxs-lookup"><span data-stu-id="baea2-146">Select hello uploads blob container toodisplay its contents in hello right pane.</span></span>
        
        ![Directorio de carga][5]

1. <span data-ttu-id="baea2-148">Cargar archivo de disco duro virtual de hello mediante el Explorador de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="baea2-148">Upload hello VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="baea2-149">En el panel derecho del explorador de almacenamiento de hello, verá una lista de blobs de Hola Hola **carga** contenedor de blob de cuenta de almacenamiento del laboratorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="baea2-149">In hello Storage Explorer right pane, you should see a listing of hello blobs in hello **uploads** blob container of hello lab's storage account.</span></span> <span data-ttu-id="baea2-150">En la barra de herramientas de editor de blob de hello, seleccione **cargar**</span><span class="sxs-lookup"><span data-stu-id="baea2-150">On hello blob editor toolbar, select **Upload**</span></span> 
        
        ![Botón Cargar][6]
    
    1. <span data-ttu-id="baea2-152">De hello **cargar** menú desplegable, seleccione **cargar archivos...** .</span><span class="sxs-lookup"><span data-stu-id="baea2-152">From hello **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="baea2-153">En hello **cargar archivos** cuadro de diálogo, los puntos suspensivos Hola select.</span><span class="sxs-lookup"><span data-stu-id="baea2-153">On hello **Upload files** dialog, select hello ellipsis.</span></span>
        
        ![Selección del archivo][8]  

    1. <span data-ttu-id="baea2-155">En hello **tooupload Seleccione archivos** cuadro de diálogo Examinar toohello deseado archivo VHD, selecciónelo y, a continuación, seleccione **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="baea2-155">On hello **Select files tooupload** dialog, browse toohello desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="baea2-156">Cuando se devuelve toohello **cargar archivos** cuadro de diálogo, cambio **tipo de Blob** demasiado**Blob en páginas**.</span><span class="sxs-lookup"><span data-stu-id="baea2-156">When returned toohello **Upload files** dialog, change **Blob type** too**Page Blob**.</span></span>
    
    1. <span data-ttu-id="baea2-157">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="baea2-157">Select **Upload**.</span></span>

        ![Selección del archivo][9]  
    
    1. <span data-ttu-id="baea2-159">Hola Explorador de almacenamiento **registro de actividad** panel muestra el estado de la descarga de hello (junto con vínculos toocancel Hola carga).</span><span class="sxs-lookup"><span data-stu-id="baea2-159">hello Storage Explorer **Activity Log** pane shows hello download status (along with links toocancel hello upload).</span></span> <span data-ttu-id="baea2-160">proceso de Hola de cargar un archivo de disco duro virtual puede ser larga según el tamaño de hello del archivo de disco duro virtual de hello y la velocidad de conexión.</span><span class="sxs-lookup"><span data-stu-id="baea2-160">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span> 

        ![Estado del archivo de carga][10]  

## <a name="next-steps"></a><span data-ttu-id="baea2-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="baea2-162">Next steps</span></span>

- [<span data-ttu-id="baea2-163">Crear una imagen personalizada en los laboratorios de desarrollo y pruebas de Azure desde un archivo de disco duro virtual mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="baea2-163">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="baea2-164">Creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="baea2-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
