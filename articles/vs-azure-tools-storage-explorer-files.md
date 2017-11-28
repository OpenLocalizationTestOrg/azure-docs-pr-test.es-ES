---
title: "aaaUsing Explorador de almacenamiento (versión preliminar) con el almacenamiento de archivos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo obtener información sobre cómo toouse toowork de explorador de almacenamiento (versión preliminar) con el archivo de recursos compartidos y archivos."
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
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="ed5ea-103">Uso del Explorador de Storage (versión preliminar) con Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="ed5ea-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="ed5ea-104">Archivo de almacenamiento es un servicio que proporciona el archivo de los recursos compartidos de hello en la nube con Azure Hola estándar Protocolo de bloque de mensajes del servidor (SMB).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="ed5ea-105">Se admiten SMB 2.1 y SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="ed5ea-106">Con el almacenamiento de archivos de Azure, puede migrar las aplicaciones heredadas que se basan en tooAzure de recursos compartidos de archivo rápidamente y sin costosas de escribir de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="ed5ea-107">Puede usar datos de tooexpose de almacenamiento de archivo públicamente toohello world o datos de la aplicación toostore privada.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="ed5ea-108">En este artículo, aprenderá cómo toouse toowork de explorador de almacenamiento (versión preliminar) con el archivo de recursos compartidos y archivos.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed5ea-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ed5ea-109">Prerequisites</span></span>

<span data-ttu-id="ed5ea-110">pasos de hello toocomplete en este artículo, necesitará Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ed5ea-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="ed5ea-111">Descargue e instale el Explorador de almacenamiento (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="ed5ea-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="ed5ea-112">Conectar la cuenta de almacenamiento de Azure tooa o servicio</span><span class="sxs-lookup"><span data-stu-id="ed5ea-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="ed5ea-113">Creación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="ed5ea-113">Create a File Share</span></span>

<span data-ttu-id="ed5ea-114">Todos los archivos deben residir en un recurso compartido de archivos, que no es más que una agrupación lógica de archivos.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="ed5ea-115">Una cuenta puede contener un número ilimitado de recursos compartidos de archivos y cada uno de ellos puede almacenar un número ilimitado de archivos.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="ed5ea-116">Hola siguientes pasos muestra cómo toocreate un recurso compartido de archivos en el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="ed5ea-117">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="ed5ea-118">En el panel izquierdo de hello, expanda cuenta de almacenamiento de hello dentro del cual desea toocreate Hola recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="ed5ea-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="ed5ea-119">Haga clic en **recursos compartidos de archivos**y - en el menú contextual de hello: seleccione **crear recurso compartido de archivos**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![Creación un recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="ed5ea-121">Aparecerá un cuadro de texto bajo hello **recursos compartidos de archivos** carpeta.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="ed5ea-122">Escriba el nombre de hello para el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-122">Enter hello name for your file share.</span></span> <span data-ttu-id="ed5ea-123">Vea hello [compartir las reglas de nomenclatura](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) sección para obtener una lista de reglas y restricciones de nomenclatura de recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Recurso compartido de Hola de nomenclatura](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="ed5ea-125">Presione **ENTRAR** cuando toocreate done Hola recurso compartido de archivos, o **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="ed5ea-126">Una vez que se creó correctamente el recurso compartido de archivos de hello, se mostrará en hello **recursos compartidos de archivos** selecciona la carpeta para hello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![nuevo recurso compartido de Hola](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="ed5ea-128">Visualización del contenido de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="ed5ea-128">View a file share's contents</span></span>

<span data-ttu-id="ed5ea-129">Los recursos compartidos de archivos contienen archivos y carpetas (que también pueden contener archivos).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="ed5ea-130">Hello siguientes pasos muestran cómo comparte contenido de hello tooview de un archivo en el Explorador de almacenamiento (versión preliminar): +</span><span class="sxs-lookup"><span data-stu-id="ed5ea-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="ed5ea-131">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="ed5ea-132">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello desea tooview.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="ed5ea-133">Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="ed5ea-134">Recurso compartido de archivos de hello contextual desea tooview y - en el menú contextual de hello: seleccione **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="ed5ea-135">Se puede hacer doble clic en recurso compartido de archivos de hello desea tooview.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-135">You can also double-click hello file share you wish tooview.</span></span>

    ![Abrir recurso compartido](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="ed5ea-137">panel principal Hola mostrará el contenido del recurso compartido de archivos Hola.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-137">hello main pane will display hello file share's contents.</span></span>
    
    ![Hola contenido del recurso compartido](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="ed5ea-139">Eliminación de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="ed5ea-139">Delete a file share</span></span>

<span data-ttu-id="ed5ea-140">Los recursos compartidos de archivos se pueden crear y eliminar fácilmente si fuera necesario.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="ed5ea-141">(toosee cómo toodelete archivos individuales, consulte la sección toohello, [administrar archivos en un recurso compartido de archivos](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="ed5ea-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="ed5ea-142">Hola siguientes pasos muestra cómo toodelete un recurso compartido de archivos en el Explorador de almacenamiento (versión preliminar):</span><span class="sxs-lookup"><span data-stu-id="ed5ea-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="ed5ea-143">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="ed5ea-144">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello desea tooview.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="ed5ea-145">Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="ed5ea-146">Recurso compartido de archivos de hello contextual desea toodelete y - en el menú contextual de hello: seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="ed5ea-147">También puede presionar **eliminar** recurso compartido de archivo actualmente seleccionado de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![Eliminar](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="ed5ea-149">Seleccione **Sí** toohello cuadro de diálogo de confirmación.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![Cuadro de diálogo Confirmación](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="ed5ea-151">Copia de un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="ed5ea-151">Copy a file share</span></span>

<span data-ttu-id="ed5ea-152">Explorador de almacenamiento (versión preliminar) permite toocopy un Portapapeles toohello de recurso compartido de archivo y, a continuación, pegue ese recurso compartido de archivos en otra cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="ed5ea-153">(toosee cómo toocopy archivos individuales, consulte la sección toohello, [administrar archivos en un recurso compartido de archivos](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="ed5ea-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="ed5ea-154">Hola siguientes pasos muestra cómo compartir toocopy un archivo desde una tooanother de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="ed5ea-155">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="ed5ea-156">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello desea toocopy.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="ed5ea-157">Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="ed5ea-158">Recurso compartido de archivos de hello contextual desea toocopy y - en el menú contextual de hello: seleccione **el recurso compartido de archivos de copia**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![Copiar recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="ed5ea-160">Haga clic en la cuenta de almacenamiento de destino"hello deseado" en la que desee recurso compartido de archivos de hello toopaste y - en el menú contextual de hello: seleccione **el recurso compartido de archivos de pegar**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![Pegar recurso compartido de archivos](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="ed5ea-162">Obtener Hola SAS para un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="ed5ea-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="ed5ea-163">A [firma de acceso compartido (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) proporciona acceso delegado tooresources en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="ed5ea-164">Esto significa que puede conceder a que un cliente limitada tooobjects permisos en su cuenta de almacenamiento en un periodo de tiempo y con un conjunto especificado de permisos, sin necesidad de tooshare las claves de acceso de cuenta.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="ed5ea-165">Hello siguientes pasos muestran cómo toocreate una SAS para un archivo compartir: +</span><span class="sxs-lookup"><span data-stu-id="ed5ea-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="ed5ea-166">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="ed5ea-167">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello para el que desea tooget una SAS.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="ed5ea-168">Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="ed5ea-169">Haga clic en recurso compartido de archivos deseado de Hola y - en el menú contextual de hello: seleccione **obtener firma de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![Obtener firma de acceso compartido](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="ed5ea-171">Hola **firma de acceso compartido** cuadro de diálogo, especifique la directiva de hello, las fechas de inicio y finalización, zona horaria y tener acceso a niveles que desee para el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![Cuadro de diálogo SAS](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="ed5ea-173">Cuando haya terminado de especificar las opciones de SAS de hello, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="ed5ea-174">Un segundo **firma de acceso compartido** cuadro de diálogo, a continuación, mostrará que listas Hola recurso compartido de archivos junto con la dirección URL de Hola y cadenas que se puede usar tooaccess Hola recurso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="ed5ea-175">Seleccione **copia** siguiente dirección URL de toohello desea toocopy toohello Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![Segundo cuadro de diálogo SAS](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="ed5ea-177">Cuando haya terminado, seleccione **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="ed5ea-178">Administración de directivas de acceso para un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="ed5ea-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="ed5ea-179">Hello siguientes pasos muestran cómo toomanage (agregar y quitar) las directivas para un recurso compartido de archivos de acceso: +.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="ed5ea-180">las directivas de acceso de Hola se usa para crear direcciones URL de SAS a través del cual las personas pueden utilizar tooaccess Hola recursos de archivo de almacenamiento durante un período de tiempo definido.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="ed5ea-181">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="ed5ea-182">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello cuyas directivas de acceso que se va toomanage.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="ed5ea-183">Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="ed5ea-184">Seleccione el recurso compartido de archivos deseado de Hola y - en el menú contextual de hello: seleccione **administrar directivas de acceso**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![Menú contextual Administrar directivas de acceso](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="ed5ea-186">Hola **las directivas de acceso** cuadro de diálogo mostrará una lista de las directivas de acceso creadas anteriormente para el recurso compartido de archivos seleccionado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![Directivas de acceso](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="ed5ea-188">Siga estos pasos dependiendo de la tarea de administración de directivas de acceso de Hola:</span><span class="sxs-lookup"><span data-stu-id="ed5ea-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="ed5ea-189">**Agregar una nueva directiva de acceso**: seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="ed5ea-190">Una vez generado, Hola **las directivas de acceso** cuadro de diálogo mostrará Hola recién agregado tener acceso a la directiva (con configuración predeterminada).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="ed5ea-191">**Editar una directiva de acceso**: realice las modificaciones que desee y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="ed5ea-192">**Quitar una directiva de acceso** : seleccione esta opción **quitar** siguiente directiva de acceso de toohello desea tooremove.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="ed5ea-193">Crear una nueva dirección URL de SAS con hello directivas de acceso que ha creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="ed5ea-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![Obtener SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nombre y propiedades de SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="ed5ea-196">Administración de archivos en un recurso compartido de archivos</span><span class="sxs-lookup"><span data-stu-id="ed5ea-196">Managing files in a file share</span></span>

<span data-ttu-id="ed5ea-197">Después de crear un recurso compartido de archivos, puede cargar un recurso compartido de archivo toothat, descargue un equipo local de tooyour de archivo, abrir un archivo en el equipo local y mucho más.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="ed5ea-198">Hello siguientes pasos muestran cómo compartan toomanage Hola archivos (y carpetas) dentro de un archivo.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="ed5ea-199">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="ed5ea-200">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el recurso compartido de archivos de hello desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="ed5ea-201">Expanda la cuenta de almacenamiento de hello **recursos compartidos de archivos**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="ed5ea-202">Haga doble clic en el recurso compartido de archivos de hello desea tooview.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="ed5ea-203">panel principal Hola mostrará el contenido del recurso compartido de archivos Hola.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-203">hello main pane will display hello file share's contents.</span></span>

    ![Hola contenido del recurso compartido](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="ed5ea-205">panel principal Hola mostrará el contenido del recurso compartido de archivos Hola.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="ed5ea-206">Siga estos que pasos dependiendo de la tarea hello desea tooperform:</span><span class="sxs-lookup"><span data-stu-id="ed5ea-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="ed5ea-207">**Cargar el recurso compartido de archivos de tooa de archivos**</span><span class="sxs-lookup"><span data-stu-id="ed5ea-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="ed5ea-208">a.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-208">a.</span></span>  <span data-ttu-id="ed5ea-209">En la barra de herramientas del panel principal de hello, seleccione **cargar**y, a continuación, **cargar archivos** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Carga de archivos](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="ed5ea-211">b.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-211">b.</span></span> <span data-ttu-id="ed5ea-212">Hola **cargar archivos** cuadro de diálogo, los puntos suspensivos Hola seleccione (**...** ) situado a derecha Hola de hello **archivos** tooselect Hola archivos desea tooupload de cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Adición de archivos](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="ed5ea-214">c.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-214">c.</span></span> <span data-ttu-id="ed5ea-215">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-215">Select **Upload**.</span></span>

    - <span data-ttu-id="ed5ea-216">**Cargar un recurso compartido de archivos de carpeta tooa**</span><span class="sxs-lookup"><span data-stu-id="ed5ea-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="ed5ea-217">a.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-217">a.</span></span> <span data-ttu-id="ed5ea-218">En la barra de herramientas del panel principal de hello, seleccione **cargar**y, a continuación, **cargar carpeta** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menú Cargar carpeta](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="ed5ea-220">b.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-220">b.</span></span> <span data-ttu-id="ed5ea-221">Hola **carga carpeta** cuadro de diálogo, los puntos suspensivos Hola seleccione (**...** ) situado a derecha Hola de hello **carpeta** carpeta de Hola de tooselect de cuadro de texto cuyo contenido desea tooupload.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="ed5ea-222">c.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-222">c.</span></span> <span data-ttu-id="ed5ea-223">Si lo desea, especifique una carpeta de destino en qué Hola se cargará el contenido de la carpeta seleccionada.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="ed5ea-224">Si no existe la carpeta de destino de hello, se creará.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="ed5ea-225">d.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-225">d.</span></span> <span data-ttu-id="ed5ea-226">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-226">Select **Upload**.</span></span>

    - <span data-ttu-id="ed5ea-227">**Descargar un equipo local de tooyour de archivo**</span><span class="sxs-lookup"><span data-stu-id="ed5ea-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="ed5ea-228">a.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-228">a.</span></span> <span data-ttu-id="ed5ea-229">Seleccione archivo hello desea toodownload.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="ed5ea-230">b.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-230">b.</span></span> <span data-ttu-id="ed5ea-231">En la barra de herramientas del panel principal de hello, seleccione **descargar**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="ed5ea-232">c.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-232">c.</span></span> <span data-ttu-id="ed5ea-233">Hola **especificar donde hello toosave descarga archivo** cuadro de diálogo, especificar ubicación de Hola donde desea descargar el archivo de Hola y Hola nombre que desee toogive se.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="ed5ea-234">d.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-234">d.</span></span> <span data-ttu-id="ed5ea-235">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-235">Select **Save**.</span></span>

    - <span data-ttu-id="ed5ea-236">**Abrir un archivo en el equipo local**</span><span class="sxs-lookup"><span data-stu-id="ed5ea-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="ed5ea-237">a.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-237">a.</span></span>  <span data-ttu-id="ed5ea-238">Seleccione archivo hello desea tooopen.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="ed5ea-239">b.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-239">b.</span></span>  <span data-ttu-id="ed5ea-240">En la barra de herramientas del panel principal de hello, seleccione **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="ed5ea-241">c.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-241">c.</span></span>  <span data-ttu-id="ed5ea-242">archivo Hello se van a descargar y abre con la aplicación hello asociada con el tipo de archivo subyacente del archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="ed5ea-243">**Copiar un Portapapeles toohello de archivo**</span><span class="sxs-lookup"><span data-stu-id="ed5ea-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="ed5ea-244">a.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-244">a.</span></span> <span data-ttu-id="ed5ea-245">Seleccione archivo hello desea toocopy.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="ed5ea-246">b.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-246">b.</span></span> <span data-ttu-id="ed5ea-247">En la barra de herramientas del panel principal de hello, seleccione **copia**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="ed5ea-248">c.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-248">c.</span></span> <span data-ttu-id="ed5ea-249">En el panel izquierdo de hello, navegar tooanother recurso compartido de archivos y haga doble clic tooview en el panel principal Hola.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="ed5ea-250">d.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-250">d.</span></span> <span data-ttu-id="ed5ea-251">En la barra de herramientas del panel principal de hello, seleccione **pegar** toocreate una copia del archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="ed5ea-252">**Eliminar un archivo**</span><span class="sxs-lookup"><span data-stu-id="ed5ea-252">**Delete a file**</span></span>

        <span data-ttu-id="ed5ea-253">a.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-253">a.</span></span> <span data-ttu-id="ed5ea-254">Seleccione archivo hello desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="ed5ea-255">b.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-255">b.</span></span> <span data-ttu-id="ed5ea-256">En la barra de herramientas del panel principal de hello, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="ed5ea-257">c.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-257">c.</span></span> <span data-ttu-id="ed5ea-258">Seleccione **Sí** toohello cuadro de diálogo de confirmación.</span><span class="sxs-lookup"><span data-stu-id="ed5ea-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed5ea-259">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ed5ea-259">Next steps</span></span>

- <span data-ttu-id="ed5ea-260">Hola de vista [notas de la versión de explorador de almacenamiento (versión preliminar) y los vídeos más recientes](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="ed5ea-261">Obtenga información acerca de cómo demasiado[crear aplicaciones mediante Azure blobs, tablas, colas y archivos](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="ed5ea-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
