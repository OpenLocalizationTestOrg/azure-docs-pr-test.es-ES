---
title: "Administración de recursos de Azure Blob Storage con el Explorador de almacenamiento (versión preliminar) | Microsoft Docs"
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
ms.openlocfilehash: f833027203441e12340bd93f3570de073d297223
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="2de1b-103">Administración de recursos de Almacenamiento de blobs de Azure con el Explorador de almacenamiento (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="2de1b-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="2de1b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="2de1b-104">Overview</span></span>
<span data-ttu-id="2de1b-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o datos binarios, a los que puede acceder desde cualquier lugar del mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2de1b-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span>
<span data-ttu-id="2de1b-106">Puede usar el almacenamiento de blobs para exponer datos públicamente o para almacenar datos de la aplicación de manera privada.</span><span class="sxs-lookup"><span data-stu-id="2de1b-106">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="2de1b-107">En este artículo, aprenderá a usar el Explorador de almacenamiento (versión preliminar) para trabajar con blobs y contenedores de blobs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-107">In this article, you'll learn how to use Storage Explorer (Preview) to work with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2de1b-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2de1b-108">Prerequisites</span></span>
<span data-ttu-id="2de1b-109">Para completar los pasos de este artículo, necesitará:</span><span class="sxs-lookup"><span data-stu-id="2de1b-109">To complete the steps in this article, you'll need the following:</span></span>

* [<span data-ttu-id="2de1b-110">Descargar e instalar el Explorador de almacenamiento (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="2de1b-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="2de1b-111">Conectarse a una cuenta de almacenamiento de Azure o a un servicio</span><span class="sxs-lookup"><span data-stu-id="2de1b-111">Connect to a Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="2de1b-112">Creación de un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="2de1b-112">Create a blob container</span></span>
<span data-ttu-id="2de1b-113">Todos los blobs deben residir en un contenedor de blobs, que no es más que una agrupación lógica de blobs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="2de1b-114">Una cuenta puede contener un número ilimitado de contenedores y cada contenedor puede almacenar un número ilimitado de blobs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="2de1b-115">Los siguientes pasos muestran cómo crear un contenedor de blob en el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="2de1b-115">The following steps illustrate how to create a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="2de1b-116">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="2de1b-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="2de1b-117">En el panel izquierdo, expanda la cuenta de almacenamiento en la que desea crear el contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-117">In the left pane, expand the storage account within which you wish to create the blob container.</span></span>
3. <span data-ttu-id="2de1b-118">Haga clic con el botón derecho en **Contenedores de blobs** y, en el menú contextual, seleccione **Crear contenedor de blobs**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-118">Right-click **Blob Containers**, and - from the context menu - select **Create Blob Container**.</span></span>

   ![Menú contextual Crear contenedores de blobs][0]
4. <span data-ttu-id="2de1b-120">Aparecerá un cuadro de texto debajo de la carpeta **Contenedores de blob** .</span><span class="sxs-lookup"><span data-stu-id="2de1b-120">A text box will appear below the **Blob Containers** folder.</span></span> <span data-ttu-id="2de1b-121">Escriba el nombre del contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-121">Enter the name for your blob container.</span></span> <span data-ttu-id="2de1b-122">Para ver una lista de reglas y restricciones en la nomenclatura de contenedores de blob, consulte la sección [Reglas de nomenclatura de contenedor](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container).</span><span class="sxs-lookup"><span data-stu-id="2de1b-122">See the [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Crear cuadro de texto Contenedores de blobs][1]
5. <span data-ttu-id="2de1b-124">Presione **ENTRAR** cuando termine para crear el contenedor de blobs o **Esc** para cancelar la operación.</span><span class="sxs-lookup"><span data-stu-id="2de1b-124">Press **Enter** when done to create the blob container, or **Esc** to cancel.</span></span> <span data-ttu-id="2de1b-125">Una vez que el contenedor de blobs se haya creado correctamente, se mostrará en la carpeta **Contenedores de Blob** de la cuenta de almacenamiento seleccionada.</span><span class="sxs-lookup"><span data-stu-id="2de1b-125">Once the blob container has been successfully created, it will be displayed under the **Blob Containers** folder for the selected storage account.</span></span>

   ![Contenedor de blobs creado][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="2de1b-127">Visualización del contenido de un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="2de1b-127">View a blob container's contents</span></span>
<span data-ttu-id="2de1b-128">Los contenedores de blobs contienen blobs y carpetas (que también contienen blobs).</span><span class="sxs-lookup"><span data-stu-id="2de1b-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="2de1b-129">Los siguientes pasos muestran cómo ver el contenido de un contenedor de blobs en el Explorador de almacenamiento (versión preliminar):</span><span class="sxs-lookup"><span data-stu-id="2de1b-129">The following steps illustrate how to view the contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="2de1b-130">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="2de1b-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="2de1b-131">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el contenedor de blobs que desea ver.</span><span class="sxs-lookup"><span data-stu-id="2de1b-131">In the left pane, expand the storage account containing the blob container you wish to view.</span></span>
3. <span data-ttu-id="2de1b-132">Expanda **Contenedores de blob**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2de1b-132">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="2de1b-133">Haga clic con el botón derecho en el contenedor de blobs que desea ver y (en el menú contextual) seleccione **Abrir editor de contenedores de blobs**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-133">Right-click the blob container you wish to view, and - from the context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="2de1b-134">También puede hacer doble clic en el contenedor de blobs que desea ver.</span><span class="sxs-lookup"><span data-stu-id="2de1b-134">You can also double-click the blob container you wish to view.</span></span>

   ![Menú contextual Abrir editor de contenedor de blobs][19]
5. <span data-ttu-id="2de1b-136">El panel principal mostrará el contenido del contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-136">The main pane will display the blob container's contents.</span></span>

   ![Editor de contenedor de blobs][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="2de1b-138">Eliminación de contenedores de blobs</span><span class="sxs-lookup"><span data-stu-id="2de1b-138">Delete a blob container</span></span>
<span data-ttu-id="2de1b-139">Los contenedores de blobs se pueden crear fácilmente y eliminarse según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2de1b-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="2de1b-140">(Para ver cómo eliminar blobs individuales, consulte la sección [Administración de blobs de un contenedor de blobs](#managing-blobs-in-a-blob-container)).</span><span class="sxs-lookup"><span data-stu-id="2de1b-140">(To see how to delete individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="2de1b-141">Los siguientes pasos muestran cómo eliminar un contenedor de blobs en el Explorador de almacenamiento (versión preliminar):</span><span class="sxs-lookup"><span data-stu-id="2de1b-141">The following steps illustrate how to delete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="2de1b-142">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="2de1b-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="2de1b-143">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el contenedor de blobs que desea ver.</span><span class="sxs-lookup"><span data-stu-id="2de1b-143">In the left pane, expand the storage account containing the blob container you wish to view.</span></span>
3. <span data-ttu-id="2de1b-144">Expanda **Contenedores de blob**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2de1b-144">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="2de1b-145">Haga clic con el botón derecho en el contenedor de blobs que desea eliminar y (en el menú contextual) seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-145">Right-click the blob container you wish to delete, and - from the context menu - select **Delete**.</span></span>
   <span data-ttu-id="2de1b-146">También puede presionar **Suprimir** para eliminar el contenedor de blobs actualmente seleccionado.</span><span class="sxs-lookup"><span data-stu-id="2de1b-146">You can also press **Delete** to delete the currently selected blob container.</span></span>

   ![Menú contextual Eliminar contenedores de blobs][4]
5. <span data-ttu-id="2de1b-148">Haga clic en **Sí** en el cuadro de diálogo de confirmación.</span><span class="sxs-lookup"><span data-stu-id="2de1b-148">Select **Yes** to the confirmation dialog.</span></span>

   ![Cuadro de diálogo de confirmación Eliminar contenedores de blobs][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="2de1b-150">Copia de un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="2de1b-150">Copy a blob container</span></span>
<span data-ttu-id="2de1b-151">Explorador de almacenamiento (versión preliminar) permite copiar un contenedor de blobs en el Portapapeles y, a continuación, pegarlo en otra cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2de1b-151">Storage Explorer (Preview) enables you to copy a blob container to the clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="2de1b-152">(Para ver cómo copiar blobs individuales, consulte la sección [Administración de blobs de un contenedor de blobs](#managing-blobs-in-a-blob-container)).</span><span class="sxs-lookup"><span data-stu-id="2de1b-152">(To see how to copy individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="2de1b-153">Los siguientes pasos muestran cómo copiar un contenedor de blobs de una cuenta de almacenamiento a otra.</span><span class="sxs-lookup"><span data-stu-id="2de1b-153">The following steps illustrate how to copy a blob container from one storage account to another.</span></span>

1. <span data-ttu-id="2de1b-154">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="2de1b-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="2de1b-155">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el contenedor de blobs que desea copiar.</span><span class="sxs-lookup"><span data-stu-id="2de1b-155">In the left pane, expand the storage account containing the blob container you wish to copy.</span></span>
3. <span data-ttu-id="2de1b-156">Expanda **Contenedores de blob**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2de1b-156">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="2de1b-157">Haga clic con el botón derecho en el contenedor de blobs que desea copiar y (en el menú contextual) seleccione **Copy Blob Container**(Copiar contenedor de blobs).</span><span class="sxs-lookup"><span data-stu-id="2de1b-157">Right-click the blob container you wish to copy, and - from the context menu - select **Copy Blob Container**.</span></span>

   ![Menú contextual Copiar contenedor de blobs][6]
5. <span data-ttu-id="2de1b-159">Haga clic con el botón derecho en la cuenta de almacenamiento de "destino" deseada en la que desea pegar el contenedor de blobs y (en el menú contextual) seleccione **Paste Blob Container**(Pegar contenedor de blobs).</span><span class="sxs-lookup"><span data-stu-id="2de1b-159">Right-click the desired "target" storage account into which you want to paste the blob container, and - from the context menu - select **Paste Blob Container**.</span></span>

   ![Menú contextual Pegar contenedor de blobs][7]

## <a name="get-the-sas-for-a-blob-container"></a><span data-ttu-id="2de1b-161">Obtención de la SAS para un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="2de1b-161">Get the SAS for a blob container</span></span>
<span data-ttu-id="2de1b-162">Una [firma de acceso compartido (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) ofrece acceso delegado a los recursos en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2de1b-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access to resources in your storage account.</span></span>
<span data-ttu-id="2de1b-163">Esto significa que puede conceder permisos limitados de los clientes a objetos en su cuenta de almacenamiento durante un período específico y con un conjunto determinado de permisos sin tener que compartir las claves de acceso a las cuentas.</span><span class="sxs-lookup"><span data-stu-id="2de1b-163">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="2de1b-164">Los siguientes pasos muestran cómo crear una SAS para un contenedor de blobs:</span><span class="sxs-lookup"><span data-stu-id="2de1b-164">The following steps illustrate how to create a SAS for a blob container:</span></span>

1. <span data-ttu-id="2de1b-165">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="2de1b-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="2de1b-166">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el contenedor de blobs del que desea obtener una SAS.</span><span class="sxs-lookup"><span data-stu-id="2de1b-166">In the left pane, expand the storage account containing the blob container for which you wish to get a SAS.</span></span>
3. <span data-ttu-id="2de1b-167">Expanda **Contenedores de blob**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2de1b-167">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="2de1b-168">Haga clic con el botón derecho en el contenedor de blobs deseado y (en el menú contextual) seleccione **Get Shared Access Signature**(Obtener firma de acceso compartido).</span><span class="sxs-lookup"><span data-stu-id="2de1b-168">Right-click the desired blob container, and - from the context menu - select **Get Shared Access Signature**.</span></span>

   ![Menú contextual Obtener SAS][8]
5. <span data-ttu-id="2de1b-170">En el cuadro de diálogo **Firma de acceso compartido** , especifique la directiva, las fechas de inicio y vencimiento, la zona horaria y los niveles de acceso que desea para el recurso.</span><span class="sxs-lookup"><span data-stu-id="2de1b-170">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

   ![Opciones de Obtener SAS][9]
6. <span data-ttu-id="2de1b-172">Cuando haya terminado de especificar las opciones de SAS, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-172">When you're finished specifying the SAS options, select **Create**.</span></span>
7. <span data-ttu-id="2de1b-173">Después, un segundo cuadro de diálogo **Firma de acceso compartido** mostrará el contenedor de blobs junto con la dirección URL y las QueryStrings que se pueden utilizar para acceder al recurso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2de1b-173">A second **Shared Access Signature** dialog will then display that lists the blob container along with the URL and QueryStrings you can use to access the storage resource.</span></span>
   <span data-ttu-id="2de1b-174">Seleccione **Copiar** junto a la dirección URL que desea copiar al Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="2de1b-174">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>

   ![Copiar direcciones URL de SAS][10]
8. <span data-ttu-id="2de1b-176">Cuando haya terminado, seleccione **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="2de1b-177">Administración de directivas de acceso para un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="2de1b-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="2de1b-178">Los siguientes pasos muestran cómo administrar (agregar y quitar) las directivas de acceso de un contenedor de blobs:</span><span class="sxs-lookup"><span data-stu-id="2de1b-178">The following steps illustrate how to manage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="2de1b-179">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="2de1b-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="2de1b-180">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el contenedor de blobs cuyas directivas de acceso desea administrar.</span><span class="sxs-lookup"><span data-stu-id="2de1b-180">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span></span>
3. <span data-ttu-id="2de1b-181">Expanda **Contenedores de blob**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2de1b-181">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="2de1b-182">Seleccione el contenedor de blobs deseado y (en el menú contextual) seleccione **Manage Access Policies**(Administrar directivas de acceso).</span><span class="sxs-lookup"><span data-stu-id="2de1b-182">Select the desired blob container, and - from the context menu - select **Manage Access Policies**.</span></span>

   ![Menú contextual Administrar directivas de acceso][11]
5. <span data-ttu-id="2de1b-184">El cuadro de diálogo **Directivas de acceso** enumerará las directivas de acceso creadas para el contenedor de blobs seleccionado.</span><span class="sxs-lookup"><span data-stu-id="2de1b-184">The **Access Policies** dialog will list any access policies already created for the selected blob container.</span></span>

   ![Opciones de Directiva de acceso][12]        
6. <span data-ttu-id="2de1b-186">Siga estos pasos en función de la tarea de administración de directivas de acceso:</span><span class="sxs-lookup"><span data-stu-id="2de1b-186">Follow these steps depending on the access policy management task:</span></span>

   * <span data-ttu-id="2de1b-187">**Agregar una nueva directiva de acceso**: seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="2de1b-188">Una vez generada, el cuadro de diálogo **Directivas de acceso** mostrará la directiva de acceso recién agregada (con la configuración predeterminada).</span><span class="sxs-lookup"><span data-stu-id="2de1b-188">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="2de1b-189">**Editar una directiva de acceso**: realice las modificaciones que desee y seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="2de1b-190">**Quitar una directiva de acceso**: seleccione **Quitar** junto a la directiva de acceso que desea quitar.</span><span class="sxs-lookup"><span data-stu-id="2de1b-190">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

## <a name="set-the-public-access-level-for-a-blob-container"></a><span data-ttu-id="2de1b-191">Establecimiento del nivel de acceso público para un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="2de1b-191">Set the Public Access Level for a blob container</span></span>
<span data-ttu-id="2de1b-192">De manera predeterminada, todos los contenedores de blobs se establecen en "Sin acceso público".</span><span class="sxs-lookup"><span data-stu-id="2de1b-192">By default, every blob container is set to "No public access".</span></span>

<span data-ttu-id="2de1b-193">Los siguientes pasos muestran cómo especificar un nivel de acceso público para un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-193">The following steps illustrate how to specify a public access level for a blob container.</span></span>

1. <span data-ttu-id="2de1b-194">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="2de1b-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="2de1b-195">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el contenedor de blobs cuyas directivas de acceso desea administrar.</span><span class="sxs-lookup"><span data-stu-id="2de1b-195">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span></span>
3. <span data-ttu-id="2de1b-196">Expanda **Contenedores de blob**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2de1b-196">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="2de1b-197">Seleccione el contenedor de blobs deseado y (en el menú contextual) seleccione **Set Public Access Level**(Establecer nivel de acceso público).</span><span class="sxs-lookup"><span data-stu-id="2de1b-197">Select the desired blob container, and - from the context menu - select **Set Public Access Level**.</span></span>

   ![Menú contextual Establecer nivel de acceso público][13]
5. <span data-ttu-id="2de1b-199">En el cuadro de diálogo **Set Container Public Access Level** (Establecer nivel de acceso público de contenedor), especifique el nivel de acceso deseado.</span><span class="sxs-lookup"><span data-stu-id="2de1b-199">In the **Set Container Public Access Level** dialog, specify the desired access level.</span></span>

   ![Opciones de Establecer nivel de acceso público][14]
6. <span data-ttu-id="2de1b-201">Seleccione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="2de1b-202">Administración de blobs de un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="2de1b-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="2de1b-203">Una vez que haya creado un contenedor de blobs, puede cargar un blob en él, descargar un blob en el equipo local, abrir un blob en el equipo local, etc.</span><span class="sxs-lookup"><span data-stu-id="2de1b-203">Once you've created a blob container, you can upload a blob to that blob container, download a blob to your local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="2de1b-204">Los siguientes pasos muestran cómo administrar los blobs (y carpetas) en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-204">The following steps illustrate how to manage the blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="2de1b-205">Abra el Explorador de almacenamiento (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="2de1b-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="2de1b-206">En el panel izquierdo, expanda la cuenta de almacenamiento que contiene el contenedor de blobs que desea administrar.</span><span class="sxs-lookup"><span data-stu-id="2de1b-206">In the left pane, expand the storage account containing the blob container you wish to manage.</span></span>
3. <span data-ttu-id="2de1b-207">Expanda **Contenedores de blob**de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2de1b-207">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="2de1b-208">Haga doble clic en el contenedor de blobs que desea ver.</span><span class="sxs-lookup"><span data-stu-id="2de1b-208">Double-click the blob container you wish to view.</span></span>
5. <span data-ttu-id="2de1b-209">El panel principal mostrará el contenido del contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-209">The main pane will display the blob container's contents.</span></span>

   ![Ver contenedor de blobs][3]
6. <span data-ttu-id="2de1b-211">El panel principal mostrará el contenido del contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="2de1b-211">The main pane will display the blob container's contents.</span></span>
7. <span data-ttu-id="2de1b-212">Siga estos pasos según la tarea que desea realizar:</span><span class="sxs-lookup"><span data-stu-id="2de1b-212">Follow these steps depending on the task you wish to perform:</span></span>

   * <span data-ttu-id="2de1b-213">**Cargar archivos en un contenedor de blobs**</span><span class="sxs-lookup"><span data-stu-id="2de1b-213">**Upload files to a blob container**</span></span>

     1. <span data-ttu-id="2de1b-214">En la barra de herramientas del panel principal, seleccione **Cargar** y, luego, **Cargar archivos** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="2de1b-214">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![Menú Cargar archivos][15]
     2. <span data-ttu-id="2de1b-216">En el cuadro de diálogo **Cargar archivos**, seleccione el botón de puntos suspensivos (**...**) a la derecha del cuadro de texto **Archivos** para seleccionar los archivos que desea cargar.</span><span class="sxs-lookup"><span data-stu-id="2de1b-216">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![Opciones de Cargar archivos][16]
     3. <span data-ttu-id="2de1b-218">Especifique el **tipo de blob**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-218">Specify the type of **Blob type**.</span></span> <span data-ttu-id="2de1b-219">El artículo [Introducción a Azure Blob Storage mediante .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica las diferencias entre los distintos tipos de blob.</span><span class="sxs-lookup"><span data-stu-id="2de1b-219">The article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span></span>
     4. <span data-ttu-id="2de1b-220">Opcionalmente, especifique la carpeta de destino en la que se cargarán los archivos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="2de1b-220">Optionally, specify a target folder into which the selected file(s) will be uploaded.</span></span> <span data-ttu-id="2de1b-221">Si la carpeta de destino no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="2de1b-221">If the target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="2de1b-222">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-222">Select **Upload**.</span></span>
   * <span data-ttu-id="2de1b-223">**Cargar una carpeta en un contenedor de blobs**</span><span class="sxs-lookup"><span data-stu-id="2de1b-223">**Upload a folder to a blob container**</span></span>

     1. <span data-ttu-id="2de1b-224">En la barra de herramientas del panel principal, seleccione **Cargar**, y luego **Cargar carpeta** en el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="2de1b-224">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![Menú Cargar carpeta][17]
     2. <span data-ttu-id="2de1b-226">En el cuadro de diálogo **Cargar carpeta**, seleccione el botón de puntos suspensivos (**...**) a la derecha del cuadro de texto **Carpeta** para seleccionar la carpeta cuyo contenido desea cargar.</span><span class="sxs-lookup"><span data-stu-id="2de1b-226">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        ![Opciones de Cargar carpeta][18]
     3. <span data-ttu-id="2de1b-228">Especifique el **tipo de blob**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-228">Specify the type of **Blob type**.</span></span> <span data-ttu-id="2de1b-229">El artículo [Introducción a Azure Blob Storage mediante .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica las diferencias entre los distintos tipos de blob.</span><span class="sxs-lookup"><span data-stu-id="2de1b-229">The article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span></span>
     4. <span data-ttu-id="2de1b-230">Opcionalmente, especifique la carpeta de destino en la que se cargará el contenido de la carpeta seleccionada.</span><span class="sxs-lookup"><span data-stu-id="2de1b-230">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="2de1b-231">Si la carpeta de destino no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="2de1b-231">If the target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="2de1b-232">Seleccione **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-232">Select **Upload**.</span></span>
   * <span data-ttu-id="2de1b-233">**Descargar un blob en el equipo local**</span><span class="sxs-lookup"><span data-stu-id="2de1b-233">**Download a blob to your local computer**</span></span>

     1. <span data-ttu-id="2de1b-234">Seleccione el blob que desea descargar.</span><span class="sxs-lookup"><span data-stu-id="2de1b-234">Select the blob you wish to download.</span></span>
     2. <span data-ttu-id="2de1b-235">En la barra de herramientas del panel principal, seleccione **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-235">On the main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="2de1b-236">En el cuadro de diálogo **Specify where to save the downloaded blob** (Especificar dónde se guarda el blob descargado), especifique la ubicación en que desea descargar el blob y el nombre que desee darle.</span><span class="sxs-lookup"><span data-stu-id="2de1b-236">In the **Specify where to save the downloaded blob** dialog, specify the location where you want the blob downloaded, and the name you wish to give it.</span></span>  
     4. <span data-ttu-id="2de1b-237">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-237">Select **Save**.</span></span>
   * <span data-ttu-id="2de1b-238">**Abrir un blob en el equipo local**</span><span class="sxs-lookup"><span data-stu-id="2de1b-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="2de1b-239">Seleccione el blob que desea abrir.</span><span class="sxs-lookup"><span data-stu-id="2de1b-239">Select the blob you wish to open.</span></span>
     2. <span data-ttu-id="2de1b-240">En la barra de herramientas del panel principal, seleccione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-240">On the main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="2de1b-241">El blob se descargará y se abrirá con la aplicación asociada con el tipo de archivo subyacente del blob.</span><span class="sxs-lookup"><span data-stu-id="2de1b-241">The blob will be downloaded and opened using the application associated with the blob's underlying file type.</span></span>
   * <span data-ttu-id="2de1b-242">**Copiar un blob en el Portapapeles**</span><span class="sxs-lookup"><span data-stu-id="2de1b-242">**Copy a blob to the clipboard**</span></span>

     1. <span data-ttu-id="2de1b-243">Seleccione el blob que desea copiar.</span><span class="sxs-lookup"><span data-stu-id="2de1b-243">Select the blob you wish to copy.</span></span>
     2. <span data-ttu-id="2de1b-244">En la barra de herramientas del panel principal, seleccione **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-244">On the main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="2de1b-245">En el panel izquierdo, navegue a otro contenedor de blobs y haga doble clic en él para verlo en el panel principal.</span><span class="sxs-lookup"><span data-stu-id="2de1b-245">In the left pane, navigate to another blob container, and double-click it to view it in the main pane.</span></span>
     4. <span data-ttu-id="2de1b-246">En la barra de herramientas del panel principal, seleccione **Pegar** para crear una copia del blob.</span><span class="sxs-lookup"><span data-stu-id="2de1b-246">On the main pane's toolbar, select **Paste** to create a copy of the blob.</span></span>
   * <span data-ttu-id="2de1b-247">**Eliminar un blob**</span><span class="sxs-lookup"><span data-stu-id="2de1b-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="2de1b-248">Seleccione el blob que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="2de1b-248">Select the blob you wish to delete.</span></span>
     2. <span data-ttu-id="2de1b-249">En la barra de herramientas del panel principal, seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="2de1b-249">On the main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="2de1b-250">Haga clic en **Sí** en el cuadro de diálogo de confirmación.</span><span class="sxs-lookup"><span data-stu-id="2de1b-250">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2de1b-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2de1b-251">Next steps</span></span>
* <span data-ttu-id="2de1b-252">Ver las [notas de la versión y los vídeos más recientes del Explorador de almacenamiento (versión preliminar)](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="2de1b-252">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="2de1b-253">Obtenga información acerca de cómo [crear aplicaciones con blobs, tablas, colas y archivos de Azure](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="2de1b-253">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

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
