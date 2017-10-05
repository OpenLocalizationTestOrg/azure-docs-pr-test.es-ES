---
title: Carga de un archivo VHD en Azure DevTest Labs mediante el Explorador de Microsoft Azure Storage | Microsoft Docs
description: Carga de un archivo VHD en la cuenta de almacenamiento del laboratorio mediante el Explorador de Microsoft Azure Storage
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
ms.openlocfilehash: 502e2536fb0fd2e9dfc4c7b85a6fb4e18202f38f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="8418a-103">Carga de un archivo VHD en la cuenta de almacenamiento del laboratorio mediante el Explorador de Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8418a-103">Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="8418a-104">En Azure DevTest Labs, se pueden usar archivos VHD para crear imágenes personalizadas, que se usan para aprovisionar máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8418a-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="8418a-105">En este artículo se ilustra cómo usar el [Explorador de Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) para cargar un archivo VHD en una cuenta de almacenamiento del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="8418a-105">This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="8418a-106">Cuando haya cargado el archivo VHD, en la sección de [pasos siguientes](#next-steps) se muestran algunos artículos que ilustran cómo crear una imagen personalizada a partir del archivo VHD cargado.</span><span class="sxs-lookup"><span data-stu-id="8418a-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="8418a-107">Para más información sobre discos y discos duros virtuales en Azure, consulte [Acerca de los discos y los discos duros virtuales para máquinas virtuales](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="8418a-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="8418a-108">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="8418a-108">Step-by-step instructions</span></span>

<span data-ttu-id="8418a-109">Los siguientes pasos le guían en la carga de un archivo VHD en DevTest Labs mediante el [Explorador de Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="8418a-109">The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="8418a-110">[Descargue e instale la versión más reciente del Explorador de Microsoft Azure Storage](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="8418a-110">[Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="8418a-111">Obtenga el nombre de la cuenta de almacenamiento del laboratorio mediante el portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="8418a-111">Get the name of the lab's storage account using the Azure portal:</span></span>

    1. <span data-ttu-id="8418a-112">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8418a-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="8418a-113">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="8418a-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
    
    1. <span data-ttu-id="8418a-114">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="8418a-114">From the list of labs, select the desired lab.</span></span>  
    
    1. <span data-ttu-id="8418a-115">En la hoja del laboratorio, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="8418a-115">On the lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="8418a-116">En la hoja **Configuración** del laboratorio, seleccione **Custom images (VHDs)** (Imágenes personalizadas [VHD]).</span><span class="sxs-lookup"><span data-stu-id="8418a-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="8418a-117">En la hoja **Custom images** (Imágenes personalizadas), seleccione **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8418a-117">On the **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="8418a-118">En la hoja **Custom images** (Imágenes personalizadas), seleccione **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8418a-118">On the **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="8418a-119">En la hoja **VHD**, seleccione **Upload a VHD using PowerShell** (Cargar un VHD mediante PowerShell).</span><span class="sxs-lookup"><span data-stu-id="8418a-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Carga del VHD mediante PowerShell][0]
    
    1. <span data-ttu-id="8418a-121">La hoja **Upload an image using PowerShell** (Cargar una imagen mediante PowerShell) muestra una llamada al cmdlet **Add-AzureVhd**.</span><span class="sxs-lookup"><span data-stu-id="8418a-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="8418a-122">El primer parámetro (*Destination*) contiene el nombre de la cuenta de almacenamiento del laboratorio en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="8418a-122">The first parameter (*Destination*) contains the storage account name for the lab in the following format:</span></span>
    
        <span data-ttu-id="8418a-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="8418a-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="8418a-124">Anote el nombre de la cuenta de almacenamiento tal como se ha usado en los últimos pasos.</span><span class="sxs-lookup"><span data-stu-id="8418a-124">Make note of the storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="8418a-125">Conéctese a una cuenta de suscripción de Azure mediante el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="8418a-125">Connect to an Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="8418a-126">El Explorador de Storage admite varias opciones de conexión.</span><span class="sxs-lookup"><span data-stu-id="8418a-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="8418a-127">En esta sección se ilustra la conexión a una cuenta de almacenamiento asociada a la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="8418a-127">This section illustrates connecting to a storage account associated with your Azure subscription.</span></span> <span data-ttu-id="8418a-128">Para ver las demás opciones de conexión admitidas por el Explorador de Storage, consulte el artículo [Introducción al Explorador de Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="8418a-128">To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="8418a-129">Abra el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="8418a-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="8418a-130">En el Explorador de Storage, seleccione **Azure Account settings** (Configuración de la cuenta de Azure).</span><span class="sxs-lookup"><span data-stu-id="8418a-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Configuración de la cuenta de Azure][1]
    
    1. <span data-ttu-id="8418a-132">El panel izquierdo muestra todas las cuentas de Microsoft en las que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="8418a-132">The left pane displays the Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="8418a-133">Para conectarse a otra cuenta, seleccione **Agregar una cuenta**y siga los cuadros de diálogo para iniciar sesión con una cuenta de Microsoft que esté asociada con al menos una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="8418a-133">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Agregar una cuenta][2]
    
    1. <span data-ttu-id="8418a-135">Una vez que haya iniciado sesión correctamente con una cuenta de Microsoft, el panel izquierdo se llena con las suscripciones de Azure asociadas a dicha cuenta.</span><span class="sxs-lookup"><span data-stu-id="8418a-135">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="8418a-136">Elija las suscripciones de Azure con las que desea trabajar y seleccione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="8418a-136">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="8418a-137">(Al seleccionar **All subscriptions** (Todas las suscripciones), se alterna la selección entre todas o ninguna de las suscripciones de Azure que aparecen).</span><span class="sxs-lookup"><span data-stu-id="8418a-137">(Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)</span></span>
    
        ![Selección de suscripciones de Azure][3]
    
    1. <span data-ttu-id="8418a-139">El panel izquierdo muestra ahora las cuentas de almacenamiento asociadas a las suscripciones de Azure seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="8418a-139">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>
    
        ![Suscripciones de Azure seleccionadas][4]

1. <span data-ttu-id="8418a-141">Busque la cuenta de almacenamiento del laboratorio:</span><span class="sxs-lookup"><span data-stu-id="8418a-141">Locate the lab's storage account:</span></span>

    1. <span data-ttu-id="8418a-142">En el panel izquierdo del Explorador de Storage, busque y expanda el nodo de la suscripción de Azure que posee el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="8418a-142">In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.</span></span>
    
    1. <span data-ttu-id="8418a-143">En el nodo de la suscripción, expanda **Cuentas de Storage**.</span><span class="sxs-lookup"><span data-stu-id="8418a-143">Under the subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="8418a-144">Expanda el nodo de cuenta de almacenamiento del laboratorio para mostrar los nodos **Contenedores de blobs**, **Recursos compartidos de archivos**, **Colas** y **Tablas**.</span><span class="sxs-lookup"><span data-stu-id="8418a-144">Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="8418a-145">Expanda el nodo **Contenedores de blobs**.</span><span class="sxs-lookup"><span data-stu-id="8418a-145">Expand the **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="8418a-146">Seleccione el contenedor de blobs de cargas para mostrar su contenido en el panel derecho.</span><span class="sxs-lookup"><span data-stu-id="8418a-146">Select the uploads blob container to display its contents in the right pane.</span></span>
        
        ![Directorio de carga][5]

1. <span data-ttu-id="8418a-148">Cargue el archivo VHD mediante el Explorador de Storage:</span><span class="sxs-lookup"><span data-stu-id="8418a-148">Upload the VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="8418a-149">En el panel derecho del Explorador de Storage, verá una lista de los blobs en el contenedor de blobs **uploads** de la cuenta de almacenamiento del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="8418a-149">In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account.</span></span> <span data-ttu-id="8418a-150">En la barra de herramientas del editor de blobs, seleccione **Cargar**</span><span class="sxs-lookup"><span data-stu-id="8418a-150">On the blob editor toolbar, select **Upload**</span></span> 
        
        ![Botón Cargar][6]
    
    1. <span data-ttu-id="8418a-152">En el menú desplegable **Cargar**, seleccione **Upload files...** (Cargar archivos...).</span><span class="sxs-lookup"><span data-stu-id="8418a-152">From the **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="8418a-153">En el diálogo **Upload files** (Cargar archivos), seleccione los puntos suspensivos.</span><span class="sxs-lookup"><span data-stu-id="8418a-153">On the **Upload files** dialog, select the ellipsis.</span></span>
        
        ![Selección del archivo][8]  

    1. <span data-ttu-id="8418a-155">En el diálogo **Select files to upload** (Seleccionar archivos para cargar), vaya al archivo VHD deseado, selecciónelo y luego haga clic en **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="8418a-155">On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="8418a-156">Cuando regrese al diálogo **Upload files** (Cargar archivos), cambie el **tipo de blob** por **Blob en páginas**.</span><span class="sxs-lookup"><span data-stu-id="8418a-156">When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.</span></span>
    
    1. <span data-ttu-id="8418a-157">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="8418a-157">Select **Upload**.</span></span>

        ![Selección del archivo][9]  
    
    1. <span data-ttu-id="8418a-159">El panel **Activity Log** (Registro de actividad) muestra el estado de descarga (junto con vínculos para cancelar la carga).</span><span class="sxs-lookup"><span data-stu-id="8418a-159">The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload).</span></span> <span data-ttu-id="8418a-160">El proceso de cargar un archivo VHD puede ser largo en función de su tamaño y de la velocidad de conexión.</span><span class="sxs-lookup"><span data-stu-id="8418a-160">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span> 

        ![Estado del archivo de carga][10]  

## <a name="next-steps"></a><span data-ttu-id="8418a-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8418a-162">Next steps</span></span>

- [<span data-ttu-id="8418a-163">Creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8418a-163">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="8418a-164">Creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="8418a-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

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
