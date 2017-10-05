---
title: "Persistencia de archivos en Azure Cloud Shell (versión preliminar) | Microsoft Docs"
description: "Tutorial de cómo Azure Cloud Shell persiste archivos."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 61a8bfcf3704f361432400771d8fcc8b81927b53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="cd2d9-103">Persistencia de archivos en Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="cd2d9-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="cd2d9-104">Cloud Shell aprovecha Azure File Storage para conservar los archivos entre sesiones.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-104">Cloud Shell takes advantage of Azure File storage to persist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="cd2d9-105">Configuración de un recurso compartido de archivos `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="cd2d9-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="cd2d9-106">En el primer inicio, Cloud Shell le pedirá que asocie un recurso compartido de archivos nuevo o existente para conservar los archivos entre sesiones.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-106">On initial start, Cloud Shell prompts you to associate a new or existing file share to persist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="cd2d9-107">creación de nuevo almacenamiento</span><span class="sxs-lookup"><span data-stu-id="cd2d9-107">Create new storage</span></span>

<span data-ttu-id="cd2d9-108">Al usar la configuración básica y seleccionar solo una suscripción, Cloud Shell crea tres recursos en su nombre en la región admitida que esté más próxima:</span><span class="sxs-lookup"><span data-stu-id="cd2d9-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in the supported region that's nearest to you:</span></span>
* <span data-ttu-id="cd2d9-109">Grupos de recursos: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="cd2d9-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="cd2d9-110">Cuenta de almacenamiento: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="cd2d9-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="cd2d9-111">Recurso compartido de archivos: `cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="cd2d9-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![La configuración de la suscripción](media/basic-storage.png)

<span data-ttu-id="cd2d9-113">El recurso compartido de archivos se monta como `clouddrive` en su directorio `$Home`.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-113">The file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="cd2d9-114">Este recurso compartido de archivos también se usa para almacenar una imagen de 5 GB creada para usted, que se actualiza automáticamente y se conserva en el directorio `$Home`.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-114">The file share is also used to store a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="cd2d9-115">Se trata de una acción única y el recurso compartido de archivos se monta automáticamente en sesiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-115">This is a one-time action, and the file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="cd2d9-116">Uso de recursos existentes</span><span class="sxs-lookup"><span data-stu-id="cd2d9-116">Use existing resources</span></span>

<span data-ttu-id="cd2d9-117">Mediante la opción avanzada puede asociar recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-117">By using the advanced option, you can associate existing resources.</span></span> <span data-ttu-id="cd2d9-118">Cuando aparezca el mensaje del programa de instalación, seleccione **Mostrar configuración avanzada** para ver otras opciones.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-118">When the storage setup prompt appears, select **Show advanced settings** to view additional options.</span></span> <span data-ttu-id="cd2d9-119">Los recursos compartidos de archivos existentes recibirán una imagen de usuario de 5 GB para conservar el directorio `$Home`.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-119">Existing file shares receive a 5-GB user image to persist your `$Home` directory.</span></span> <span data-ttu-id="cd2d9-120">Los menús desplegables se filtran para la región de Cloud Shell y las cuentas de almacenamiento con redundancia local y de almacenamiento con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-120">The drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![La configuración de grupo de recursos](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="cd2d9-122">Restringir la creación de recursos con una directiva de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="cd2d9-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="cd2d9-123">Las cuentas de almacenamiento creadas en Cloud Shell se etiquetan con `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="cd2d9-124">Si quiere impedir que los usuarios creen cuentas de almacenamiento en Cloud Shell, cree una [directiva de recursos de Azure para etiquetas](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) que se desencadene mediante esta etiqueta específica.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-124">If you want to disallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="cd2d9-125">Cómo funciona Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="cd2d9-125">How Cloud Shell works</span></span>
<span data-ttu-id="cd2d9-126">Cloud Shell conserva los archivos a través de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cd2d9-126">Cloud Shell persists files through both of the following methods:</span></span>
* <span data-ttu-id="cd2d9-127">Creación de una imagen de disco del directorio `$Home` para hacer persistente todo el contenido dentro del directorio.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-127">Creating a disk image of your `$Home` directory to persist all contents within the directory.</span></span> <span data-ttu-id="cd2d9-128">La imagen de disco se guarda en su recurso compartido de archivos especificado como `acc_<User>.img` en `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img` y sincroniza automáticamente los cambios.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-128">The disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="cd2d9-129">Montaje del recurso compartido de archivos especificado como `clouddrive` en el directorio `$Home` para la interacción directa del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="cd2d9-130">`/Home/<User>/clouddrive` se asigna a `fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-130">`/Home/<User>/clouddrive` is mapped to `fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="cd2d9-131">Todos los archivos en el directorio `$Home`, como las claves de SSH, se conservan en la imagen de disco de usuario almacenada en el recurso compartido de archivos montado.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="cd2d9-132">Ponga en práctica los procedimientos recomendados correspondientes para conservar la información en el directorio `$Home` y en el recurso compartido de archivos montado.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-the-clouddrive-command"></a><span data-ttu-id="cd2d9-133">Uso del comando `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="cd2d9-133">Use the `clouddrive` command</span></span>
<span data-ttu-id="cd2d9-134">Con Cloud Shell, puede ejecutar un comando denominado `clouddrive`, lo que permite actualizar manualmente el recurso compartido de archivos que está montado en Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you to manually update the file share that's mounted to Cloud Shell.</span></span>
<span data-ttu-id="cd2d9-135">![Ejecución del comando "clouddrive"](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="cd2d9-135">![Running the "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="cd2d9-136">Montaje de un nuevo `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="cd2d9-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="cd2d9-137">Requisitos previos para el montaje manual</span><span class="sxs-lookup"><span data-stu-id="cd2d9-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="cd2d9-138">Puede actualizar el recurso compartido de archivos que esté asociada con Cloud Shell mediante el uso del comando `clouddrive mount`.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-138">You can update the file share that's associated with Cloud Shell by using the `clouddrive mount` command.</span></span>

<span data-ttu-id="cd2d9-139">Si se monta un recurso compartido de archivos existente, las cuentas de almacenamiento tienen que ser:</span><span class="sxs-lookup"><span data-stu-id="cd2d9-139">If you mount an existing file share, the storage accounts must be:</span></span>
* <span data-ttu-id="cd2d9-140">De almacenamiento con redundancia local o de almacenamiento con redundancia geográfica para que admitan recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-140">Locally-redundant storage or geo-redundant storage to support file shares.</span></span>
* <span data-ttu-id="cd2d9-141">Deben ubicarse en su región asignada.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-141">Located in your assigned region.</span></span> <span data-ttu-id="cd2d9-142">Al incorporarse, la región a la que está asignado aparece en el nombre del grupo de recursos `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-142">When you are onboarding, the region you are assigned to is listed in the resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="cd2d9-143">Regiones de almacenamiento admitidas</span><span class="sxs-lookup"><span data-stu-id="cd2d9-143">Supported storage regions</span></span>
<span data-ttu-id="cd2d9-144">Los archivos de Azure tienen que residir en la misma región que la máquina de Cloud Shell en la que se montan.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-144">The Azure files must reside in the same region as the Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="cd2d9-145">Actualmente, los clústeres de Cloud Shell existen en las regiones siguientes:</span><span class="sxs-lookup"><span data-stu-id="cd2d9-145">Cloud Shell clusters currently exist in the following regions:</span></span>
|<span data-ttu-id="cd2d9-146">Ámbito</span><span class="sxs-lookup"><span data-stu-id="cd2d9-146">Area</span></span>|<span data-ttu-id="cd2d9-147">Region</span><span class="sxs-lookup"><span data-stu-id="cd2d9-147">Region</span></span>|
|---|---|
|<span data-ttu-id="cd2d9-148">América</span><span class="sxs-lookup"><span data-stu-id="cd2d9-148">Americas</span></span>|<span data-ttu-id="cd2d9-149">Este de EE. UU., centro-sur de EE. UU. y oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="cd2d9-150">Europa</span><span class="sxs-lookup"><span data-stu-id="cd2d9-150">Europe</span></span>|<span data-ttu-id="cd2d9-151">Norte de Europa y Oeste de Europa</span><span class="sxs-lookup"><span data-stu-id="cd2d9-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="cd2d9-152">Asia Pacífico</span><span class="sxs-lookup"><span data-stu-id="cd2d9-152">Asia Pacific</span></span>|<span data-ttu-id="cd2d9-153">India central, Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="cd2d9-153">India Central, Southeast Asia</span></span>|

### <a name="the-clouddrive-mount-command"></a><span data-ttu-id="cd2d9-154">El comando `clouddrive mount`</span><span class="sxs-lookup"><span data-stu-id="cd2d9-154">The `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="cd2d9-155">Si está montando un nuevo recurso compartido de archivos, se creará una nueva imagen de usuario para el directorio `$Home`, ya que la imagen de `$Home` anterior se conserva en el recurso compartido de archivos anterior.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in the previous file share.</span></span>

<span data-ttu-id="cd2d9-156">Ejecute el comando `clouddrive mount` con los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="cd2d9-156">Run the `clouddrive mount` command with the following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="cd2d9-157">Para ver más detalles, ejecute `clouddrive mount -h`, tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="cd2d9-157">To view more details, run `clouddrive mount -h`, as shown here:</span></span>

![Ejecución del comando "clouddrive"](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="cd2d9-159">Desmontar `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="cd2d9-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="cd2d9-160">Puede desmontar un recurso compartido de archivos montado en Cloud Shell en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-160">You can unmount a file share that's mounted to Cloud Shell at any time.</span></span> <span data-ttu-id="cd2d9-161">Una vez que el recurso compartido de archivos se desmonta, se le pedirá que monte uno nuevo antes de la siguiente sesión.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-161">Once your file share is unmounted, you will be prompted to mount a new file share prior to your next session.</span></span>

<span data-ttu-id="cd2d9-162">Para quitar un recurso compartido de archivos de Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="cd2d9-162">To remove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="cd2d9-163">Ejecute `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="cd2d9-164">Reconozca y confirme los avisos.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-164">Acknowledge and confirm the prompts.</span></span>

<span data-ttu-id="cd2d9-165">El recurso compartido de archivos seguirá existiendo a menos que se elimine manualmente.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-165">Your file share will continue to exist unless you delete it manually.</span></span> <span data-ttu-id="cd2d9-166">Cloud Shell dejará de buscar este recurso compartido de archivos en sesiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="cd2d9-167">Para ver más detalles, ejecute `clouddrive unmount -h`, tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="cd2d9-167">To view more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Ejecución del comando "clouddrive amount"](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="cd2d9-169">Ejecutar este comando no eliminará ningún recurso.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="cd2d9-170">Si elimina manualmente un grupo de recursos, una cuenta de almacenamiento o un recurso compartido de archivos asignados a Cloud Shell, se borrarán permanentemente la imagen del directorio `$Home` y los demás archivos del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-170">Manually deleting a resource group, storage account, or file share that is mapped to Cloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="cd2d9-171">Esta operación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="cd2d9-172">Listado de Recursos compartidos de archivos de `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="cd2d9-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="cd2d9-173">Para descubrir qué recurso compartido de archivos se monta como `clouddrive` ejecute el siguiente comando `df`:</span><span class="sxs-lookup"><span data-stu-id="cd2d9-173">To discover which file share is mounted as `clouddrive`, run the following `df` command.</span></span> 

<span data-ttu-id="cd2d9-174">La ruta de acceso de archivo a clouddrive mostrará el recurso compartido de archivos y el nombre de la cuenta de almacenamiento en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-174">The file path to clouddrive shows your storage account name and file share in the URL.</span></span> <span data-ttu-id="cd2d9-175">Por ejemplo: `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="cd2d9-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-to-cloud-shell"></a><span data-ttu-id="cd2d9-176">Transferir archivos locales a Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="cd2d9-176">Transfer local files to Cloud Shell</span></span>
<span data-ttu-id="cd2d9-177">El directorio `clouddrive` se sincroniza con la hoja de almacenamiento de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-177">The `clouddrive` directory syncs with the Azure portal storage blade.</span></span> <span data-ttu-id="cd2d9-178">Use esta hoja para transferir archivos locales al recurso compartido de archivos y viceversa.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-178">Use this blade to transfer local files to or from your file share.</span></span> <span data-ttu-id="cd2d9-179">La actualización de archivos en Cloud Shell se refleja en la GUI de File Storage al actualizarse las hojas.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-179">Updating files from within Cloud Shell is reflected in the file storage GUI when you refresh the blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="cd2d9-180">Descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="cd2d9-180">Download files</span></span>

![Lista de archivos locales](media/download.png)
1. <span data-ttu-id="cd2d9-182">En Azure Portal, vaya al recurso compartido de archivos montados.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-182">In the Azure portal, go to the mounted file share.</span></span>
2. <span data-ttu-id="cd2d9-183">Seleccione el archivo de destino.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-183">Select the target file.</span></span>
3. <span data-ttu-id="cd2d9-184">Seleccione el botón **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-184">Select the **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="cd2d9-185">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="cd2d9-185">Upload files</span></span>

![Archivos locales para cargarse](media/upload.png)
1. <span data-ttu-id="cd2d9-187">Vaya al recurso compartido de archivos montado.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-187">Go to your mounted file share.</span></span>
2. <span data-ttu-id="cd2d9-188">Seleccione el botón **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-188">Select the **Upload** button.</span></span>
3. <span data-ttu-id="cd2d9-189">Seleccione el archivo o archivos que desea cargar.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-189">Select the file or files that you want to upload.</span></span>
4. <span data-ttu-id="cd2d9-190">Confirmación de la actualización.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-190">Confirm the upload.</span></span>

<span data-ttu-id="cd2d9-191">Ahora debería ver los archivos accesibles en el directorio `clouddrive` en Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="cd2d9-191">You should now see the files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd2d9-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd2d9-192">Next steps</span></span>
[<span data-ttu-id="cd2d9-193">Inicio rápido de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="cd2d9-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="cd2d9-194">
[Información sobre Azure File Storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="cd2d9-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="cd2d9-195">
[Información sobre las etiquetas de Storage](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="cd2d9-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
