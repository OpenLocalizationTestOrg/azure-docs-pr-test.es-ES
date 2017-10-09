---
title: "recursos de almacenamiento de blobs de Azure de aaaManage con el Explorador de almacenamiento (versión preliminar) | Documentos de Microsoft"
description: "Administración de blobs y contenedores de blobs de Azure con el Explorador de almacenamiento (versión preliminar)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="4f4c6-103">Administración de recursos de Almacenamiento de blobs de Azure con el Explorador de almacenamiento (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="4f4c6-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="4f4c6-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4f4c6-104">Overview</span></span>
<span data-ttu-id="4f4c6-105">[Almacenamiento de blobs de Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o binario, que puede tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="4f4c6-106">Puede usar datos de tooexpose de almacenamiento de Blob públicamente toohello world o datos de la aplicación toostore privada.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="4f4c6-107">En este artículo, aprenderá cómo toouse toowork de explorador de almacenamiento (versión preliminar) con contenedores de blob y los blobs.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f4c6-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4f4c6-108">Prerequisites</span></span>
<span data-ttu-id="4f4c6-109">pasos de hello toocomplete en este artículo, necesitará Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="4f4c6-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="4f4c6-110">Descargue e instale el Explorador de almacenamiento (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="4f4c6-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="4f4c6-111">Conectar la cuenta de almacenamiento de Azure tooa o servicio</span><span class="sxs-lookup"><span data-stu-id="4f4c6-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="4f4c6-112">Creación de un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="4f4c6-112">Create a blob container</span></span>
<span data-ttu-id="4f4c6-113">Todos los blobs deben residir en un contenedor de blobs, que no es más que una agrupación lógica de blobs.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="4f4c6-114">Una cuenta puede contener un número ilimitado de contenedores y cada contenedor puede almacenar un número ilimitado de blobs.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="4f4c6-115">Hello siguientes pasos muestran cómo toocreate un contenedor de blobs en el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="4f4c6-116">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="4f4c6-117">En el panel izquierdo de hello, expanda cuenta de almacenamiento de hello dentro del cual desea contenedor de blobs de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="4f4c6-118">Haga clic en **contenedores de blobs**y - en el menú contextual de hello: seleccione **crear contenedor de blobs**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![Menú contextual Crear contenedores de blobs][0]
4. <span data-ttu-id="4f4c6-120">Aparecerá un cuadro de texto bajo hello **contenedores de blobs** carpeta.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="4f4c6-121">Escriba el nombre de hello para el contenedor de blob.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="4f4c6-122">Vea hello [las reglas de nomenclatura de contenedor](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) sección para obtener una lista de reglas y restricciones en la nomenclatura de contenedores de blobs.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Crear cuadro de texto Contenedores de blobs][1]
5. <span data-ttu-id="4f4c6-124">Presione **ENTRAR** cuando haya finalizado la toocreate contenedor de blobs de hello, o **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="4f4c6-125">Una vez que se ha creado correctamente el contenedor de blob de hello, se mostrará en hello **contenedores de blobs** selecciona la carpeta para hello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![Contenedor de blobs creado][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="4f4c6-127">Visualización del contenido de un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="4f4c6-127">View a blob container's contents</span></span>
<span data-ttu-id="4f4c6-128">Los contenedores de blobs contienen blobs y carpetas (que también contienen blobs).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="4f4c6-129">Hello siguientes pasos muestran cómo contenido de hello tooview de un contenedor de blobs en el Explorador de almacenamiento (versión preliminar):</span><span class="sxs-lookup"><span data-stu-id="4f4c6-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="4f4c6-130">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="4f4c6-131">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello desea tooview.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="4f4c6-132">Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="4f4c6-133">Contenedor de blobs de hello contextual desea tooview y - en el menú contextual de hello: seleccione **abrir Editor de contenedor de Blob**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="4f4c6-134">También puede hacer doble clic contenedor de blobs de hello desea tooview.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![Menú contextual Abrir editor de contenedor de blobs][19]
5. <span data-ttu-id="4f4c6-136">panel principal Hola mostrará el contenido del contenedor de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-136">hello main pane will display hello blob container's contents.</span></span>

   ![Editor de contenedor de blobs][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="4f4c6-138">Eliminación de contenedores de blobs</span><span class="sxs-lookup"><span data-stu-id="4f4c6-138">Delete a blob container</span></span>
<span data-ttu-id="4f4c6-139">Los contenedores de blobs se pueden crear fácilmente y eliminarse según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="4f4c6-140">(toosee cómo blobs toodelete individuales, consulte sección toohello, [administrar blobs en un contenedor de blobs](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="4f4c6-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="4f4c6-141">Hello siguientes pasos muestran cómo toodelete un contenedor de blobs en el Explorador de almacenamiento (versión preliminar):</span><span class="sxs-lookup"><span data-stu-id="4f4c6-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="4f4c6-142">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="4f4c6-143">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello desea tooview.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="4f4c6-144">Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="4f4c6-145">Contenedor de blobs de hello contextual desea toodelete y - en el menú contextual de hello: seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="4f4c6-146">También puede presionar **eliminar** contenedor de toodelete Hola blob actualmente seleccionado.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![Menú contextual Eliminar contenedores de blobs][4]
5. <span data-ttu-id="4f4c6-148">Seleccione **Sí** toohello cuadro de diálogo de confirmación.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![Cuadro de diálogo de confirmación Eliminar contenedores de blobs][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="4f4c6-150">Copia de un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="4f4c6-150">Copy a blob container</span></span>
<span data-ttu-id="4f4c6-151">Explorador de almacenamiento (vista previa) le permite toocopy un Portapapeles toohello de contenedor de blob y, a continuación, pegue que contenedor de blobs en otra cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="4f4c6-152">(toosee cómo blobs toocopy individuales, consulte sección toohello, [administrar blobs en un contenedor de blobs](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="4f4c6-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="4f4c6-153">Hola pasos ilustran toocopy un contenedor de blob desde el almacenamiento de una cuenta y cómo tooanother.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="4f4c6-154">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="4f4c6-155">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello desea toocopy.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="4f4c6-156">Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="4f4c6-157">Contenedor de blobs de hello contextual desea toocopy y - en el menú contextual de hello: seleccione **contenedor de blobs de copia**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![Menú contextual Copiar contenedor de blobs][6]
5. <span data-ttu-id="4f4c6-159">Haga clic en la cuenta de almacenamiento de destino"hello deseado" en la que desee toopaste contenedor de blobs de Hola y - en el menú contextual de hello: seleccione **contenedor de blobs de pegar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![Menú contextual Pegar contenedor de blobs][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="4f4c6-161">Obtener Hola SAS para un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="4f4c6-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="4f4c6-162">A [firma de acceso compartido (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) proporciona acceso delegado tooresources en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="4f4c6-163">Esto significa que puede conceder a que un cliente limitada tooobjects permisos en su cuenta de almacenamiento en un periodo de tiempo y con un conjunto especificado de permisos, sin tener que compartir claves de acceso de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="4f4c6-164">Hello siguientes pasos muestran cómo toocreate una SAS para un contenedor de blobs:</span><span class="sxs-lookup"><span data-stu-id="4f4c6-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="4f4c6-165">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="4f4c6-166">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello para el que desea tooget una SAS.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="4f4c6-167">Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="4f4c6-168">Haga clic en el contenedor de blobs que se prefiera de Hola y - en el menú contextual de hello: seleccione **obtener firma de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![Menú contextual Obtener SAS][8]
5. <span data-ttu-id="4f4c6-170">Hola **firma de acceso compartido** cuadro de diálogo, especifique la directiva de hello, las fechas de inicio y finalización, zona horaria y tener acceso a niveles que desee para el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![Opciones de Obtener SAS][9]
6. <span data-ttu-id="4f4c6-172">Cuando haya terminado de especificar las opciones de SAS de hello, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="4f4c6-173">Un segundo **firma de acceso compartido** cuadro de diálogo, a continuación, mostrará que listas Hola contenedor de blobs junto con la dirección URL de Hola y cadenas que se puede usar tooaccess Hola recurso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="4f4c6-174">Seleccione **copia** siguiente dirección URL de toohello desea toocopy toohello Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![Copiar direcciones URL de SAS][10]
8. <span data-ttu-id="4f4c6-176">Cuando haya terminado, seleccione **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="4f4c6-177">Administración de directivas de acceso para un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="4f4c6-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="4f4c6-178">Hello siguientes pasos muestran cómo toomanage (agregar y quitar) las directivas para un contenedor de blobs de acceso:</span><span class="sxs-lookup"><span data-stu-id="4f4c6-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="4f4c6-179">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="4f4c6-180">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello cuyas directivas de acceso que se va toomanage.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="4f4c6-181">Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="4f4c6-182">Seleccionar contenedor de blobs deseado de Hola y - en el menú contextual de hello: seleccione **administrar directivas de acceso**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![Menú contextual Administrar directivas de acceso][11]
5. <span data-ttu-id="4f4c6-184">Hola **las directivas de acceso** cuadro de diálogo mostrará una lista de las directivas de acceso creadas anteriormente para el contenedor de blob seleccionados Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![Opciones de Directiva de acceso][12]        
6. <span data-ttu-id="4f4c6-186">Siga estos pasos dependiendo de la tarea de administración de directivas de acceso de Hola:</span><span class="sxs-lookup"><span data-stu-id="4f4c6-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="4f4c6-187">**Agregar una nueva directiva de acceso**: seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="4f4c6-188">Una vez generado, Hola **las directivas de acceso** cuadro de diálogo mostrará Hola recién agregado tener acceso a la directiva (con configuración predeterminada).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="4f4c6-189">**Editar una directiva de acceso**: realice las modificaciones que desee y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="4f4c6-190">**Quitar una directiva de acceso** : seleccione esta opción **quitar** siguiente directiva de acceso de toohello desea tooremove.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="4f4c6-191">Establecer nivel de acceso público de hello en un contenedor de blob</span><span class="sxs-lookup"><span data-stu-id="4f4c6-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="4f4c6-192">De forma predeterminada, cada contenedor de blob se establece demasiado "Ningún acceso público".</span><span class="sxs-lookup"><span data-stu-id="4f4c6-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="4f4c6-193">Hello siguientes pasos muestran cómo toospecify un complemento público tiene acceso a nivel de un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="4f4c6-194">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="4f4c6-195">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello cuyas directivas de acceso que se va toomanage.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="4f4c6-196">Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="4f4c6-197">Seleccionar contenedor de blobs deseado de Hola y - en el menú contextual de hello: seleccione **establecer el nivel de acceso público**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![Menú contextual Establecer nivel de acceso público][13]
5. <span data-ttu-id="4f4c6-199">Hola **establecer el nivel de acceso público de contenedor** cuadro de diálogo, especifique el nivel de acceso de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![Opciones de Establecer nivel de acceso público][14]
6. <span data-ttu-id="4f4c6-201">Seleccione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="4f4c6-202">Administración de blobs de un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="4f4c6-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="4f4c6-203">Una vez que ha creado un contenedor de blobs, puede cargar un contenedor de blobs de blob toothat, descargue un equipo local de blob tooyour, abrir un blob en el equipo local y mucho más.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="4f4c6-204">Hola siguientes pasos muestra cómo toomanage Hola blobs (y carpetas) dentro de un contenedor de blob.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="4f4c6-205">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="4f4c6-206">En el panel izquierdo de hello, expanda cuenta de almacenamiento de Hola que contiene el contenedor de blobs de hello desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="4f4c6-207">Expanda la cuenta de almacenamiento de hello **contenedores de blobs**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="4f4c6-208">Haga doble clic en el contenedor de blobs de hello desea tooview.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="4f4c6-209">panel principal Hola mostrará el contenido del contenedor de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-209">hello main pane will display hello blob container's contents.</span></span>

   ![Ver contenedor de blobs][3]
6. <span data-ttu-id="4f4c6-211">panel principal Hola mostrará el contenido del contenedor de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="4f4c6-212">Siga estos que pasos dependiendo de la tarea hello desea tooperform:</span><span class="sxs-lookup"><span data-stu-id="4f4c6-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="4f4c6-213">**Cargar el contenedor de blobs de tooa de archivos**</span><span class="sxs-lookup"><span data-stu-id="4f4c6-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="4f4c6-214">En la barra de herramientas del panel principal de hello, seleccione **cargar**y, a continuación, **cargar archivos** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Menú Cargar archivos][15]
     2. <span data-ttu-id="4f4c6-216">Hola **cargar archivos** cuadro de diálogo, los puntos suspensivos Hola seleccione (**...** ) situado a derecha Hola de hello **archivos** tooselect Hola archivos desea tooupload de cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Opciones de Cargar archivos][16]
     3. <span data-ttu-id="4f4c6-218">Especificar tipo de Hola de **tipo de Blob**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="4f4c6-219">artículo de Hello [Introducción al almacenamiento de blobs de Azure mediante .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) se explican las diferencias de hello entre Hola diversos tipos de blob.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="4f4c6-220">Si lo desea, especifique una carpeta de destino en la que se cargarán los archivos seleccionados de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="4f4c6-221">Si no existe la carpeta de destino de hello, se creará.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="4f4c6-222">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-222">Select **Upload**.</span></span>
   * <span data-ttu-id="4f4c6-223">**Cargar un contenedor de blobs de tooa de carpeta**</span><span class="sxs-lookup"><span data-stu-id="4f4c6-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="4f4c6-224">En la barra de herramientas del panel principal de hello, seleccione **cargar**y, a continuación, **cargar carpeta** desde el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menú Cargar carpeta][17]
     2. <span data-ttu-id="4f4c6-226">Hola **carga carpeta** cuadro de diálogo, los puntos suspensivos Hola seleccione (**...** ) situado a derecha Hola de hello **carpeta** carpeta de Hola de tooselect de cuadro de texto cuyo contenido desea tooupload.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![Opciones de Cargar carpeta][18]
     3. <span data-ttu-id="4f4c6-228">Especificar tipo de Hola de **tipo de Blob**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="4f4c6-229">artículo de Hello [Introducción al almacenamiento de blobs de Azure mediante .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) se explican las diferencias de hello entre Hola diversos tipos de blob.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="4f4c6-230">Si lo desea, especifique una carpeta de destino en qué Hola se cargará el contenido de la carpeta seleccionada.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="4f4c6-231">Si no existe la carpeta de destino de hello, se creará.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="4f4c6-232">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-232">Select **Upload**.</span></span>
   * <span data-ttu-id="4f4c6-233">**Descargar un equipo local de blob tooyour**</span><span class="sxs-lookup"><span data-stu-id="4f4c6-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="4f4c6-234">Seleccione el blob de hello desea toodownload.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="4f4c6-235">En la barra de herramientas del panel principal de hello, seleccione **descargar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="4f4c6-236">Hola **especificar donde hello toosave descarga blob** cuadro de diálogo, especificar ubicación de Hola donde desea blob Hola descargó y Hola nombre que desee toogive se.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="4f4c6-237">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-237">Select **Save**.</span></span>
   * <span data-ttu-id="4f4c6-238">**Abrir un blob en el equipo local**</span><span class="sxs-lookup"><span data-stu-id="4f4c6-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="4f4c6-239">Seleccione el blob de hello desea tooopen.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="4f4c6-240">En la barra de herramientas del panel principal de hello, seleccione **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="4f4c6-241">blob de Hola se van a descargar y abre con la aplicación hello asociada con el tipo de archivo subyacente del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="4f4c6-242">**Copiar un Portapapeles toohello de blob**</span><span class="sxs-lookup"><span data-stu-id="4f4c6-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="4f4c6-243">Seleccione el blob de hello desea toocopy.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="4f4c6-244">En la barra de herramientas del panel principal de hello, seleccione **copia**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="4f4c6-245">En el panel izquierdo de hello, navegar por el contenedor de blobs de tooanother y haga doble clic tooview en el panel principal Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="4f4c6-246">En la barra de herramientas del panel principal de hello, seleccione **pegar** toocreate una copia de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="4f4c6-247">**Eliminar un blob**</span><span class="sxs-lookup"><span data-stu-id="4f4c6-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="4f4c6-248">Seleccione el blob de hello desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="4f4c6-249">En la barra de herramientas del panel principal de hello, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="4f4c6-250">Seleccione **Sí** toohello cuadro de diálogo de confirmación.</span><span class="sxs-lookup"><span data-stu-id="4f4c6-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f4c6-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4f4c6-251">Next steps</span></span>
* <span data-ttu-id="4f4c6-252">Hola de vista [notas de la versión de explorador de almacenamiento (versión preliminar) y los vídeos más recientes](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="4f4c6-253">Obtenga información acerca de cómo demasiado[crear aplicaciones mediante Azure blobs, tablas, colas y archivos](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="4f4c6-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
