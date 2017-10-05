---
title: "Uso del Explorador de Storage (versión preliminar) con Azure File Storage | Microsoft Docs"
description: "Aprenda a usar el Explorador de Storage (versión preliminar) para trabajar con archivos y recursos compartidos de archivos."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 964691758254531cb92a5b1cbe055ef61d25dba8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="91754-103">Uso del Explorador de Storage (versión preliminar) con Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="91754-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="91754-104">Azure File Storage es un servicio que ofrece recursos compartidos de archivos en la nube mediante el protocolo Bloque de mensajes del servidor (SMB) estándar.</span><span class="sxs-lookup"><span data-stu-id="91754-104">Azure File storage is a service that offers file shares in the cloud using the standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="91754-105">Se admiten SMB 2.1 y SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="91754-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="91754-106">Con Almacenamiento de archivos de Azure puede migrar aplicaciones heredadas basadas en recursos compartidos de archivos a Azure con rapidez y sin necesidad de costosas reescrituras.</span><span class="sxs-lookup"><span data-stu-id="91754-106">With Azure File storage, you can migrate legacy applications that rely on file shares to Azure quickly and without costly rewrites.</span></span> <span data-ttu-id="91754-107">File Storage se puede usar para exponer datos públicamente o para almacenar los datos de la aplicación de manera privada.</span><span class="sxs-lookup"><span data-stu-id="91754-107">You can use File storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="91754-108">En este artículo, aprenderá a usar el Explorador de Storage (versión preliminar) para trabajar con recursos compartidos de archivos y archivos.</span><span class="sxs-lookup"><span data-stu-id="91754-108">In this article, you'll learn how to use Storage Explorer (Preview) to work with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91754-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="91754-109">Prerequisites</span></span>

<span data-ttu-id="91754-110">Para completar los pasos de este artículo, necesitará:</span><span class="sxs-lookup"><span data-stu-id="91754-110">To complete the steps in this article, you'll need the following:</span></span>

- [<span data-ttu-id="91754-111">Descargar e instalar el Explorador de almacenamiento (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="91754-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="91754-112">Conectarse a una cuenta de almacenamiento de Azure o a un servicio</span><span class="sxs-lookup"><span data-stu-id="91754-112">Connect to a Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="91754-113">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="91754-113">Create a File Share</span></span>

<span data-ttu-id="91754-114">Todos los archivos deben residir en un recurso compartido de archivos, que no es más que una agrupación lógica de archivos.</span><span class="sxs-lookup"><span data-stu-id="91754-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="91754-115">Una cuenta puede contener un número ilimitado de recursos compartidos de archivos y cada uno de ellos puede almacenar un número ilimitado de archivos.</span><span class="sxs-lookup"><span data-stu-id="91754-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="91754-116">Los siguientes pasos muestran cómo crear un recurso compartido de archivos en el Explorador de Storage (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="91754-116">The following steps illustrate how to create a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="91754-117">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="91754-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="91754-118">En el panel izquierdo, expanda la cuenta de almacenamiento en la que desea crear el recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="91754-118">In the left pane, expand the storage account within which you wish to create the File Share</span></span>

3. <span data-ttu-id="91754-119">Haga clic con el botón derecho en **Recursos compartidos de archivos** y (en el menú contextual) seleccione **Create File Share** (Crear recurso compartido de archivos).</span><span class="sxs-lookup"><span data-stu-id="91754-119">Right-click **File Shares**, and - from the context menu - select **Create File Share**.</span></span>

    ![Creación un recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="91754-121">Aparecerá un cuadro de texto debajo de la carpeta **Recursos compartidos de archivos**.</span><span class="sxs-lookup"><span data-stu-id="91754-121">A text box will appear below the **File Shares** folder.</span></span> <span data-ttu-id="91754-122">Escriba el nombre del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="91754-122">Enter the name for your file share.</span></span> <span data-ttu-id="91754-123">Para ver una lista de reglas y restricciones en la nomenclatura de recursos compartidos de archivos, consulte la sección [Reglas de nomenclatura de recursos compartidos](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container).</span><span class="sxs-lookup"><span data-stu-id="91754-123">See the [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Nomenclatura de recurso compartido](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="91754-125">Presione **Entrar** cuando termine para crear el recurso compartido de archivos o **Esc** para cancelar la operación.</span><span class="sxs-lookup"><span data-stu-id="91754-125">Press **Enter** when done to create the file share, or **Esc** to cancel.</span></span> <span data-ttu-id="91754-126">Una vez que el recurso compartido de archivos se haya creado correctamente, se mostrará en la carpeta **Recursos compartidos de archivos** de la cuenta de almacenamiento seleccionada.</span><span class="sxs-lookup"><span data-stu-id="91754-126">Once the file share has been successfully created, it will be displayed under the **File Shares** folder for the selected storage account.</span></span>

    ![El nuevo recurso compartido](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="91754-128">Visualización del contenido de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="91754-128">View a file share's contents</span></span>

<span data-ttu-id="91754-129">Los recursos compartidos de archivos contienen archivos y carpetas (que también pueden contener archivos).</span><span class="sxs-lookup"><span data-stu-id="91754-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="91754-130">Los siguientes pasos muestran cómo ver el contenido de recurso compartido de archivos en el Explorador de Storage (versión preliminar):+</span><span class="sxs-lookup"><span data-stu-id="91754-130">The following steps illustrate how to view the contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="91754-131">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="91754-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="91754-132">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el recurso compartido de archivos que desea ver.</span><span class="sxs-lookup"><span data-stu-id="91754-132">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="91754-133">Expanda la opción **Recursos compartidos de archivos**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91754-133">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="91754-134">Haga clic con el botón derecho en el recurso compartido de archivos que desea ver y (en el menú contextual) seleccione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="91754-134">Right-click the file share you wish to view, and - from the context menu - select **Open**.</span></span> <span data-ttu-id="91754-135">También puede hacer doble clic en el recurso compartido de archivos que desea ver.</span><span class="sxs-lookup"><span data-stu-id="91754-135">You can also double-click the file share you wish to view.</span></span>

    ![Abrir recurso compartido](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="91754-137">El panel principal mostrará el contenido del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="91754-137">The main pane will display the file share's contents.</span></span>
    
    ![El contenido del recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="91754-139">Eliminación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="91754-139">Delete a file share</span></span>

<span data-ttu-id="91754-140">Los recursos compartidos de archivos se pueden crear y eliminar fácilmente si fuera necesario.</span><span class="sxs-lookup"><span data-stu-id="91754-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="91754-141">(para ver cómo eliminar los archivos individuales, consulte la sección [Administración de archivos en un recurso compartido de archivos](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container)).</span><span class="sxs-lookup"><span data-stu-id="91754-141">(To see how to delete individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="91754-142">Los siguientes pasos muestran cómo eliminar un recurso compartido de archivos en el Explorador de Storage (versión preliminar):</span><span class="sxs-lookup"><span data-stu-id="91754-142">The following steps illustrate how to delete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="91754-143">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="91754-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="91754-144">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el recurso compartido de archivos que desea ver.</span><span class="sxs-lookup"><span data-stu-id="91754-144">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="91754-145">Expanda la opción **Recursos compartidos de archivos**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91754-145">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="91754-146">Haga clic con el botón derecho en el recurso compartido de archivos que desea eliminar y (en el menú contextual) seleccione **Delete** (Eliminar).</span><span class="sxs-lookup"><span data-stu-id="91754-146">Right-click the file share you wish to delete, and - from the context menu - select **Delete**.</span></span> <span data-ttu-id="91754-147">También puede presionar **Suprimir** para eliminar el recurso compartido de archivos actualmente seleccionado.</span><span class="sxs-lookup"><span data-stu-id="91754-147">You can also press **Delete** to delete the currently selected file share.</span></span>

    ![Eliminar](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="91754-149">Haga clic en **Sí** en el cuadro de diálogo de confirmación.</span><span class="sxs-lookup"><span data-stu-id="91754-149">Select **Yes** to the confirmation dialog.</span></span>
    
    ![Cuadro de diálogo Confirmación](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="91754-151">Copia de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="91754-151">Copy a file share</span></span>

<span data-ttu-id="91754-152">El Explorador de Storage (versión preliminar) permite copiar un recurso compartido de archivos en el Portapapeles y, después, pegarlo en otra cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91754-152">Storage Explorer (Preview) enables you to copy a file share to the clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="91754-153">(para ver cómo copiar los archivos individuales, consulte la sección [Administración de archivos en un recurso compartido de archivos](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container)).</span><span class="sxs-lookup"><span data-stu-id="91754-153">(To see how to copy individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="91754-154">Los siguientes pasos muestran cómo copiar un recurso compartido de archivos de una cuenta de almacenamiento a otra.</span><span class="sxs-lookup"><span data-stu-id="91754-154">The following steps illustrate how to copy a file share from one storage account to another.</span></span>

1. <span data-ttu-id="91754-155">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="91754-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="91754-156">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el recurso compartido de archivos que desea copiar.</span><span class="sxs-lookup"><span data-stu-id="91754-156">In the left pane, expand the storage account containing the file share you wish to copy.</span></span>

3. <span data-ttu-id="91754-157">Expanda la opción **Recursos compartidos de archivos**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91754-157">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="91754-158">Haga clic con el botón derecho en el recurso compartido de archivos que desea copiar y (en el menú contextual) seleccione **Copy File Share** (Copar recurso compartido de archivos).</span><span class="sxs-lookup"><span data-stu-id="91754-158">Right-click the file share you wish to copy, and - from the context menu - select **Copy File Share**.</span></span>

    ![Copiar recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="91754-160">Haga clic con el botón derecho en la cuenta de almacenamiento de "destino" deseada en la que desea pegar el recurso compartido de archivos y (en el menú contextual) seleccione **Paste File Share**(Pegar recurso compartido de archivos).</span><span class="sxs-lookup"><span data-stu-id="91754-160">Right-click the desired "target" storage account into which you want to paste the file share, and - from the context menu - select **Paste File Share**.</span></span>

    ![Pegar recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-the-sas-for-a-file-share"></a><span data-ttu-id="91754-162">Obtención de la SAS de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="91754-162">Get the SAS for a file share</span></span>

<span data-ttu-id="91754-163">Una [firma de acceso compartido (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) ofrece acceso delegado a los recursos en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91754-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="91754-164">Esto significa que puede conceder permisos limitados de los clientes a objetos en su cuenta de almacenamiento durante un período específico y con un conjunto determinado de permisos sin tener que compartir las claves de acceso a las cuentas.</span><span class="sxs-lookup"><span data-stu-id="91754-164">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="91754-165">Los siguientes pasos muestran cómo crear una SAS para un recurso compartido de archivos:+</span><span class="sxs-lookup"><span data-stu-id="91754-165">The following steps illustrate how to create a SAS for a file share:+</span></span>

1. <span data-ttu-id="91754-166">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="91754-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="91754-167">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el recurso compartido de archivos del que desea obtener una SAS.</span><span class="sxs-lookup"><span data-stu-id="91754-167">In the left pane, expand the storage account containing the file share for which you wish to get a SAS.</span></span>

3. <span data-ttu-id="91754-168">Expanda la opción **Recursos compartidos de archivos**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91754-168">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="91754-169">Haga clic con el botón derecho en el recurso compartido de archivos y (en el menú contextual) seleccione **Get Shared Access Signature**(Obtener firma de acceso compartido).</span><span class="sxs-lookup"><span data-stu-id="91754-169">Right-click the desired file share, and - from the context menu - select **Get Shared Access Signature**.</span></span>

    ![Obtener firma de acceso compartido](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="91754-171">En el cuadro de diálogo **Firma de acceso compartido** , especifique la directiva, las fechas de inicio y vencimiento, la zona horaria y los niveles de acceso que desea para el recurso.</span><span class="sxs-lookup"><span data-stu-id="91754-171">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

    ![Cuadro de diálogo SAS](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="91754-173">Cuando haya terminado de especificar las opciones de SAS, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="91754-173">When you're finished specifying the SAS options, select **Create**.</span></span>

7. <span data-ttu-id="91754-174">Después, un segundo cuadro de diálogo **Firma de acceso compartido** mostrará el recurso compartido de archivos junto con la dirección URL y las QueryStrings que se pueden utilizar para acceder al recurso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91754-174">A second **Shared Access Signature** dialog will then display that lists the file share along with the URL and QueryStrings you can use to access the storage resource.</span></span> <span data-ttu-id="91754-175">Seleccione **Copiar** junto a la dirección URL que desea copiar al Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="91754-175">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>
    
    ![Segundo cuadro de diálogo SAS](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="91754-177">Cuando haya terminado, seleccione **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="91754-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="91754-178">Administración de directivas de acceso para un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="91754-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="91754-179">Los siguientes pasos muestran cómo administrar (agregar y quitar) las directivas de acceso de un recurso compartido de archivos:+.</span><span class="sxs-lookup"><span data-stu-id="91754-179">The following steps illustrate how to manage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="91754-180">Las directivas de acceso se utilizan para crear las direcciones URL de SAS que los usuarios pueden utilizar para acceder al recurso de archivo de almacenamiento durante un período definido.</span><span class="sxs-lookup"><span data-stu-id="91754-180">The Access Policies is used for creating SAS URLs through which people can use to access the Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="91754-181">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="91754-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="91754-182">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el recurso compartido de archivos cuyas directivas de acceso desea administrar.</span><span class="sxs-lookup"><span data-stu-id="91754-182">In the left pane, expand the storage account containing the file share whose access policies you wish to manage.</span></span>

3. <span data-ttu-id="91754-183">Expanda la opción **Recursos compartidos de archivos**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91754-183">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="91754-184">Seleccione el recurso compartido de archivos deseado y (en el menú contextual) seleccione **Manage Access Policies**(Administrar directivas de acceso).</span><span class="sxs-lookup"><span data-stu-id="91754-184">Select the desired file share, and - from the context menu - select **Manage Access Policies**.</span></span>

    ![Menú contextual Administrar directivas de acceso](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="91754-186">El cuadro de diálogo **Directivas de acceso** enumerará las directivas de acceso creadas para el recurso compartido de archivos seleccionado.</span><span class="sxs-lookup"><span data-stu-id="91754-186">The **Access Policies** dialog will list any access policies already created for the selected file share.</span></span>
    
    ![Directivas de acceso](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="91754-188">Siga estos pasos en función de la tarea de administración de directivas de acceso:</span><span class="sxs-lookup"><span data-stu-id="91754-188">Follow these steps depending on the access policy management task:</span></span>
    
    - <span data-ttu-id="91754-189">**Agregar una nueva directiva de acceso**: seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="91754-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="91754-190">Una vez generada, el cuadro de diálogo **Directivas de acceso** mostrará la directiva de acceso recién agregada (con la configuración predeterminada).</span><span class="sxs-lookup"><span data-stu-id="91754-190">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="91754-191">**Editar una directiva de acceso**: realice las modificaciones que desee y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="91754-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="91754-192">**Quitar una directiva de acceso**: seleccione **Quitar** junto a la directiva de acceso que desea quitar.</span><span class="sxs-lookup"><span data-stu-id="91754-192">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

7. <span data-ttu-id="91754-193">Cree una nueva dirección URL de SAS mediante la directiva de acceso que creó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="91754-193">Create a new SAS URL using the Access Policy you created earlier:</span></span>
    
    ![Obtener SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nombre y propiedades de SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="91754-196">Administración de archivos en un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="91754-196">Managing files in a file share</span></span>

<span data-ttu-id="91754-197">Una vez que haya creado un recurso compartido de archivos, puede cargar un archivo en él, descargar un archivo en el equipo local, abrir un archivo en el equipo local, etc.</span><span class="sxs-lookup"><span data-stu-id="91754-197">Once you've created a file share, you can upload a file to that file share, download a file to your local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="91754-198">Los siguientes pasos muestran cómo administrar los archivos (y carpetas) en un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="91754-198">The following steps illustrate how to manage the files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="91754-199">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="91754-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="91754-200">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el recurso compartido de archivos que desea administrar.</span><span class="sxs-lookup"><span data-stu-id="91754-200">In the left pane, expand the storage account containing the file share you wish to manage.</span></span>

3.  <span data-ttu-id="91754-201">Expanda la opción **Recursos compartidos de archivos**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="91754-201">Expand the storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="91754-202">Haga doble clic en el recurso compartido de archivos que desea ver.</span><span class="sxs-lookup"><span data-stu-id="91754-202">Double-click the file share you wish to view.</span></span>

5.  <span data-ttu-id="91754-203">El panel principal mostrará el contenido del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="91754-203">The main pane will display the file share's contents.</span></span>

    ![El contenido del recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="91754-205">El panel principal mostrará el contenido del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="91754-205">The main pane will display the file share's contents.</span></span>

7.  <span data-ttu-id="91754-206">Siga estos pasos según la tarea que desea realizar:</span><span class="sxs-lookup"><span data-stu-id="91754-206">Follow these steps depending on the task you wish to perform:</span></span>

    - <span data-ttu-id="91754-207">**Cargar archivos en un recurso compartido de archivos**</span><span class="sxs-lookup"><span data-stu-id="91754-207">**Upload files to a file share**</span></span>

        <span data-ttu-id="91754-208">a.</span><span class="sxs-lookup"><span data-stu-id="91754-208">a.</span></span>  <span data-ttu-id="91754-209">En la barra de herramientas del panel principal, seleccione **Cargar** y, luego, **Cargar archivos** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="91754-209">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![Carga de archivos](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="91754-211">b.</span><span class="sxs-lookup"><span data-stu-id="91754-211">b.</span></span> <span data-ttu-id="91754-212">En el cuadro de diálogo **Cargar archivos**, seleccione el botón de puntos suspensivos (**...**) a la derecha del cuadro de texto **Archivos** para seleccionar los archivos que desea cargar.</span><span class="sxs-lookup"><span data-stu-id="91754-212">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![Adición de archivos](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="91754-214">c.</span><span class="sxs-lookup"><span data-stu-id="91754-214">c.</span></span> <span data-ttu-id="91754-215">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="91754-215">Select **Upload**.</span></span>

    - <span data-ttu-id="91754-216">**Cargar una carpeta en un recurso compartido de archivos**</span><span class="sxs-lookup"><span data-stu-id="91754-216">**Upload a folder to a file share**</span></span>
        
        <span data-ttu-id="91754-217">a.</span><span class="sxs-lookup"><span data-stu-id="91754-217">a.</span></span> <span data-ttu-id="91754-218">En la barra de herramientas del panel principal, seleccione **Cargar**, y luego **Cargar carpeta** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="91754-218">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![Menú Cargar carpeta](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="91754-220">b.</span><span class="sxs-lookup"><span data-stu-id="91754-220">b.</span></span> <span data-ttu-id="91754-221">En el cuadro de diálogo **Cargar carpeta**, seleccione el botón de puntos suspensivos (**...**) a la derecha del cuadro de texto **Carpeta** para seleccionar la carpeta cuyo contenido desea cargar.</span><span class="sxs-lookup"><span data-stu-id="91754-221">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        <span data-ttu-id="91754-222">c.</span><span class="sxs-lookup"><span data-stu-id="91754-222">c.</span></span> <span data-ttu-id="91754-223">Opcionalmente, especifique la carpeta de destino en la que se cargará el contenido de la carpeta seleccionada.</span><span class="sxs-lookup"><span data-stu-id="91754-223">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="91754-224">Si la carpeta de destino no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="91754-224">If the target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="91754-225">d.</span><span class="sxs-lookup"><span data-stu-id="91754-225">d.</span></span> <span data-ttu-id="91754-226">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="91754-226">Select **Upload**.</span></span>

    - <span data-ttu-id="91754-227">**Descargar un archivo en el equipo local**</span><span class="sxs-lookup"><span data-stu-id="91754-227">**Download a file to your local computer**</span></span>
        
        <span data-ttu-id="91754-228">a.</span><span class="sxs-lookup"><span data-stu-id="91754-228">a.</span></span> <span data-ttu-id="91754-229">Seleccione el archivo que desea descargar.</span><span class="sxs-lookup"><span data-stu-id="91754-229">Select the file you wish to download.</span></span>
        
        <span data-ttu-id="91754-230">b.</span><span class="sxs-lookup"><span data-stu-id="91754-230">b.</span></span> <span data-ttu-id="91754-231">En la barra de herramientas del panel principal, seleccione **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="91754-231">On the main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="91754-232">c.</span><span class="sxs-lookup"><span data-stu-id="91754-232">c.</span></span> <span data-ttu-id="91754-233">En el cuadro de diálogo **Specify where to save the downloaded blob** (Especificar dónde se guarda el archivo descargado), especifique la ubicación en que desea descargar el archivo y el nombre que desee darle.</span><span class="sxs-lookup"><span data-stu-id="91754-233">In the **Specify where to save the downloaded file** dialog, specify the location where you want the file downloaded, and the name you wish to give it.</span></span>

        <span data-ttu-id="91754-234">d.</span><span class="sxs-lookup"><span data-stu-id="91754-234">d.</span></span> <span data-ttu-id="91754-235">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="91754-235">Select **Save**.</span></span>

    - <span data-ttu-id="91754-236">**Abrir un archivo en el equipo local**</span><span class="sxs-lookup"><span data-stu-id="91754-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="91754-237">a.</span><span class="sxs-lookup"><span data-stu-id="91754-237">a.</span></span>  <span data-ttu-id="91754-238">Seleccione el archivo que desea abrir.</span><span class="sxs-lookup"><span data-stu-id="91754-238">Select the file you wish to open.</span></span>
        
        <span data-ttu-id="91754-239">b.</span><span class="sxs-lookup"><span data-stu-id="91754-239">b.</span></span>  <span data-ttu-id="91754-240">En la barra de herramientas del panel principal, seleccione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="91754-240">On the main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="91754-241">c.</span><span class="sxs-lookup"><span data-stu-id="91754-241">c.</span></span>  <span data-ttu-id="91754-242">El archivo se descargará y abrirá mediante la aplicación asociada con el tipo de archivo subyacente del archivo.</span><span class="sxs-lookup"><span data-stu-id="91754-242">The file will be downloaded and opened using the application associated with the file's underlying file type.</span></span>

    - <span data-ttu-id="91754-243">**Copiar un archivo en el Portapapeles**</span><span class="sxs-lookup"><span data-stu-id="91754-243">**Copy a file to the clipboard**</span></span>

        <span data-ttu-id="91754-244">a.</span><span class="sxs-lookup"><span data-stu-id="91754-244">a.</span></span> <span data-ttu-id="91754-245">Seleccione el archivo que desea copiar.</span><span class="sxs-lookup"><span data-stu-id="91754-245">Select the file you wish to copy.</span></span>

        <span data-ttu-id="91754-246">b.</span><span class="sxs-lookup"><span data-stu-id="91754-246">b.</span></span> <span data-ttu-id="91754-247">En la barra de herramientas del panel principal, seleccione **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="91754-247">On the main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="91754-248">c.</span><span class="sxs-lookup"><span data-stu-id="91754-248">c.</span></span> <span data-ttu-id="91754-249">En el panel izquierdo, navegue a otro recurso compartido de archivos y haga doble clic en él para verlo en el panel principal.</span><span class="sxs-lookup"><span data-stu-id="91754-249">In the left pane, navigate to another file share, and double-click it to view it in the main pane.</span></span>

        <span data-ttu-id="91754-250">d.</span><span class="sxs-lookup"><span data-stu-id="91754-250">d.</span></span> <span data-ttu-id="91754-251">En la barra de herramientas del panel principal, seleccione **Pegar** para crear una copia del archivo.</span><span class="sxs-lookup"><span data-stu-id="91754-251">On the main pane's toolbar, select **Paste** to create a copy of the file.</span></span>

    - <span data-ttu-id="91754-252">**Eliminar un archivo**</span><span class="sxs-lookup"><span data-stu-id="91754-252">**Delete a file**</span></span>

        <span data-ttu-id="91754-253">a.</span><span class="sxs-lookup"><span data-stu-id="91754-253">a.</span></span> <span data-ttu-id="91754-254">Seleccione el archivo que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="91754-254">Select the file you wish to delete.</span></span>

        <span data-ttu-id="91754-255">b.</span><span class="sxs-lookup"><span data-stu-id="91754-255">b.</span></span> <span data-ttu-id="91754-256">En la barra de herramientas del panel principal, seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="91754-256">On the main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="91754-257">c.</span><span class="sxs-lookup"><span data-stu-id="91754-257">c.</span></span> <span data-ttu-id="91754-258">Haga clic en **Sí** en el cuadro de diálogo de confirmación.</span><span class="sxs-lookup"><span data-stu-id="91754-258">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91754-259">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="91754-259">Next steps</span></span>

- <span data-ttu-id="91754-260">Ver las [notas de la versión y los vídeos más recientes del Explorador de almacenamiento (versión preliminar)](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="91754-260">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="91754-261">Obtenga información acerca de cómo [crear aplicaciones con blobs, tablas, colas y archivos de Azure](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="91754-261">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
