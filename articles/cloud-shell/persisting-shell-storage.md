---
title: "archivos de aaaPersist en el Shell de nube de Azure (versión preliminar) | Documentos de Microsoft"
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
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="3925b-103">Persistencia de archivos en Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="3925b-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="3925b-104">Shell de nube aprovecha las ventajas de los archivos de toopersist de almacenamiento de archivos de Azure entre las sesiones.</span><span class="sxs-lookup"><span data-stu-id="3925b-104">Cloud Shell takes advantage of Azure File storage toopersist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="3925b-105">Configuración de un recurso compartido de archivos `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="3925b-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="3925b-106">Primer inicio, el Shell de nube le pedirá que tooassociate un archivo nuevo o existente compartir archivos toopersist entre sesiones.</span><span class="sxs-lookup"><span data-stu-id="3925b-106">On initial start, Cloud Shell prompts you tooassociate a new or existing file share toopersist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="3925b-107">creación de nuevo almacenamiento</span><span class="sxs-lookup"><span data-stu-id="3925b-107">Create new storage</span></span>

<span data-ttu-id="3925b-108">Al usar la configuración básica y seleccionar solo una suscripción, el Shell de nube crea tres recursos en su nombre de región de hello compatible que está más cerca de tooyou:</span><span class="sxs-lookup"><span data-stu-id="3925b-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in hello supported region that's nearest tooyou:</span></span>
* <span data-ttu-id="3925b-109">Grupos de recursos: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="3925b-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="3925b-110">Cuenta de almacenamiento: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="3925b-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="3925b-111">Recurso compartido de archivos: `cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="3925b-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![configuración de la suscripción de Hola](media/basic-storage.png)

<span data-ttu-id="3925b-113">recurso compartido de archivos de Hello monta como `clouddrive` en su `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="3925b-113">hello file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="3925b-114">Hello recurso compartido de archivos también es toostore usa una imagen de 5 GB que se crea automáticamente para usted y que se actualiza y se continúa la `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="3925b-114">hello file share is also used toostore a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="3925b-115">Se trata de una acción única y recurso compartido de archivos de hello monta automáticamente en las siguientes sesiones.</span><span class="sxs-lookup"><span data-stu-id="3925b-115">This is a one-time action, and hello file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="3925b-116">Uso de recursos existentes</span><span class="sxs-lookup"><span data-stu-id="3925b-116">Use existing resources</span></span>

<span data-ttu-id="3925b-117">Mediante el uso de hello opción avanzada, es posible asociar recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="3925b-117">By using hello advanced option, you can associate existing resources.</span></span> <span data-ttu-id="3925b-118">Cuando aparezca el símbolo del sistema de hello almacenamiento el programa de instalación, seleccione **Mostrar configuración avanzada** tooview las opciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="3925b-118">When hello storage setup prompt appears, select **Show advanced settings** tooview additional options.</span></span> <span data-ttu-id="3925b-119">Recursos compartidos de archivos existente reciban un toopersist de imagen de usuario de 5 GB su `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="3925b-119">Existing file shares receive a 5-GB user image toopersist your `$Home` directory.</span></span> <span data-ttu-id="3925b-120">los menús desplegables de Hola se filtran para su región de Shell en la nube y las cuentas de almacenamiento con redundancia geográfica & local redundantes.</span><span class="sxs-lookup"><span data-stu-id="3925b-120">hello drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![configuración de grupo de recursos de Hola](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="3925b-122">Restringir la creación de recursos con una directiva de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="3925b-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="3925b-123">Las cuentas de almacenamiento creadas en Cloud Shell se etiquetan con `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="3925b-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="3925b-124">Si desea que los usuarios de toodisallow desde la creación de cuentas de almacenamiento en nube Shell, cree un [directiva de recursos de Azure para etiquetas](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) que desencadena esta etiqueta específica.</span><span class="sxs-lookup"><span data-stu-id="3925b-124">If you want toodisallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="3925b-125">Cómo funciona Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="3925b-125">How Cloud Shell works</span></span>
<span data-ttu-id="3925b-126">En la nube Shell continúa archivos a través de hello siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="3925b-126">Cloud Shell persists files through both of hello following methods:</span></span>
* <span data-ttu-id="3925b-127">Crear una imagen de disco de su `$Home` directory toopersist todos los contenido en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="3925b-127">Creating a disk image of your `$Home` directory toopersist all contents within hello directory.</span></span> <span data-ttu-id="3925b-128">imagen de disco de Hola se guarda en el recurso compartido de archivo especificado como `acc_<User>.img` en `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, y sincroniza automáticamente los cambios.</span><span class="sxs-lookup"><span data-stu-id="3925b-128">hello disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="3925b-129">Montaje del recurso compartido de archivos especificado como `clouddrive` en el directorio `$Home` para la interacción directa del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="3925b-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="3925b-130">`/Home/<User>/clouddrive`se ha asignado demasiado`fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="3925b-130">`/Home/<User>/clouddrive` is mapped too`fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="3925b-131">Todos los archivos en el directorio `$Home`, como las claves de SSH, se conservan en la imagen de disco de usuario almacenada en el recurso compartido de archivos montado.</span><span class="sxs-lookup"><span data-stu-id="3925b-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="3925b-132">Ponga en práctica los procedimientos recomendados correspondientes para conservar la información en el directorio `$Home` y en el recurso compartido de archivos montado.</span><span class="sxs-lookup"><span data-stu-id="3925b-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-hello-clouddrive-command"></a><span data-ttu-id="3925b-133">Hola de uso `clouddrive` comando</span><span class="sxs-lookup"><span data-stu-id="3925b-133">Use hello `clouddrive` command</span></span>
<span data-ttu-id="3925b-134">Con el Shell de nube, puede ejecutar un comando denominado `clouddrive`, que permite toomanually actualización Hola recurso compartido de archivos que tooCloud montada Shell.</span><span class="sxs-lookup"><span data-stu-id="3925b-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you toomanually update hello file share that's mounted tooCloud Shell.</span></span>
<span data-ttu-id="3925b-135">![Ejecutar el comando "clouddrive" hello](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="3925b-135">![Running hello "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="3925b-136">Montaje de un nuevo `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="3925b-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="3925b-137">Requisitos previos para el montaje manual</span><span class="sxs-lookup"><span data-stu-id="3925b-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="3925b-138">Puede actualizar el recurso compartido de archivos de Hola que esté asociada con el Shell de nube mediante el uso de hello `clouddrive mount` comando.</span><span class="sxs-lookup"><span data-stu-id="3925b-138">You can update hello file share that's associated with Cloud Shell by using hello `clouddrive mount` command.</span></span>

<span data-ttu-id="3925b-139">Si montar un recurso compartido de archivos existente, deben ser cuentas de almacenamiento de hello:</span><span class="sxs-lookup"><span data-stu-id="3925b-139">If you mount an existing file share, hello storage accounts must be:</span></span>
* <span data-ttu-id="3925b-140">Almacenamiento con redundancia local o recursos compartidos de archivos de almacenamiento con redundancia geográfica toosupport.</span><span class="sxs-lookup"><span data-stu-id="3925b-140">Locally-redundant storage or geo-redundant storage toosupport file shares.</span></span>
* <span data-ttu-id="3925b-141">Deben ubicarse en su región asignada.</span><span class="sxs-lookup"><span data-stu-id="3925b-141">Located in your assigned region.</span></span> <span data-ttu-id="3925b-142">Cuando haya incorporación, región de Hola se asignan toois aparece en el nombre del grupo de recursos de hello `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="3925b-142">When you are onboarding, hello region you are assigned toois listed in hello resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="3925b-143">Regiones de almacenamiento admitidas</span><span class="sxs-lookup"><span data-stu-id="3925b-143">Supported storage regions</span></span>
<span data-ttu-id="3925b-144">Hello Azure archivos deben residir en hello misma región como máquina de Shell en la nube de Hola que esté montando puedan.</span><span class="sxs-lookup"><span data-stu-id="3925b-144">hello Azure files must reside in hello same region as hello Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="3925b-145">Clústeres de Shell en la nube existen actualmente en hello siguientes regiones:</span><span class="sxs-lookup"><span data-stu-id="3925b-145">Cloud Shell clusters currently exist in hello following regions:</span></span>
|<span data-ttu-id="3925b-146">Ámbito</span><span class="sxs-lookup"><span data-stu-id="3925b-146">Area</span></span>|<span data-ttu-id="3925b-147">Region</span><span class="sxs-lookup"><span data-stu-id="3925b-147">Region</span></span>|
|---|---|
|<span data-ttu-id="3925b-148">América</span><span class="sxs-lookup"><span data-stu-id="3925b-148">Americas</span></span>|<span data-ttu-id="3925b-149">Este de EE. UU., centro-sur de EE. UU. y oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="3925b-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="3925b-150">Europa</span><span class="sxs-lookup"><span data-stu-id="3925b-150">Europe</span></span>|<span data-ttu-id="3925b-151">Norte de Europa y Oeste de Europa</span><span class="sxs-lookup"><span data-stu-id="3925b-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="3925b-152">Asia Pacífico</span><span class="sxs-lookup"><span data-stu-id="3925b-152">Asia Pacific</span></span>|<span data-ttu-id="3925b-153">India central, Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="3925b-153">India Central, Southeast Asia</span></span>|

### <a name="hello-clouddrive-mount-command"></a><span data-ttu-id="3925b-154">Hola `clouddrive mount` comando</span><span class="sxs-lookup"><span data-stu-id="3925b-154">hello `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="3925b-155">Si va a montar un nuevo recurso compartido de archivos, se crea una nueva imagen de usuario para su `$Home` directorio, porque su anterior `$Home` imagen se mantiene en el recurso compartido de archivos anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="3925b-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in hello previous file share.</span></span>

<span data-ttu-id="3925b-156">Ejecute hello `clouddrive mount` comando con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="3925b-156">Run hello `clouddrive mount` command with hello following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="3925b-157">tooview obtener más detalles, ejecute `clouddrive mount -h`, tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="3925b-157">tooview more details, run `clouddrive mount -h`, as shown here:</span></span>

![Ejecución hello ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="3925b-159">Desmontar `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="3925b-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="3925b-160">Puede desmontar un recurso compartido de archivos de Shell que tooCloud montado en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="3925b-160">You can unmount a file share that's mounted tooCloud Shell at any time.</span></span> <span data-ttu-id="3925b-161">Una vez que el recurso compartido de archivos se desmonta, estará solicitada toomount un tooyour anterior del recurso compartido de archivo nueva sesión siguiente.</span><span class="sxs-lookup"><span data-stu-id="3925b-161">Once your file share is unmounted, you will be prompted toomount a new file share prior tooyour next session.</span></span>

<span data-ttu-id="3925b-162">tooremove un archivo de recurso compartido de Shell en la nube:</span><span class="sxs-lookup"><span data-stu-id="3925b-162">tooremove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="3925b-163">Ejecute `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="3925b-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="3925b-164">Confirmar y confirme los mensajes de Hola.</span><span class="sxs-lookup"><span data-stu-id="3925b-164">Acknowledge and confirm hello prompts.</span></span>

<span data-ttu-id="3925b-165">El recurso compartido de archivos continuará tooexist a menos que se elimine manualmente.</span><span class="sxs-lookup"><span data-stu-id="3925b-165">Your file share will continue tooexist unless you delete it manually.</span></span> <span data-ttu-id="3925b-166">Cloud Shell dejará de buscar este recurso compartido de archivos en sesiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="3925b-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="3925b-167">tooview obtener más detalles, ejecute `clouddrive unmount -h`, tal y como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="3925b-167">tooview more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Ejecución hello ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="3925b-169">Ejecutar este comando no eliminará ningún recurso.</span><span class="sxs-lookup"><span data-stu-id="3925b-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="3925b-170">Eliminación manual de un grupo de recursos, la cuenta de almacenamiento o el recurso compartido de archivos que está asignado tooCloud Shell, se eliminará permanentemente su `$Home` imagen de directorio y cualquier otro archivo en el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="3925b-170">Manually deleting a resource group, storage account, or file share that is mapped tooCloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="3925b-171">Esta operación no se puede deshacer.</span><span class="sxs-lookup"><span data-stu-id="3925b-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="3925b-172">Listado de Recursos compartidos de archivos de `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="3925b-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="3925b-173">toodiscover qué recurso compartido de archivos se monta como `clouddrive`, ejecute hello siguiente `df` comando.</span><span class="sxs-lookup"><span data-stu-id="3925b-173">toodiscover which file share is mounted as `clouddrive`, run hello following `df` command.</span></span> 

<span data-ttu-id="3925b-174">tooclouddrive de ruta de acceso del archivo de Hello muestra que su nombre de la cuenta de almacenamiento y el archivo compartan en la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="3925b-174">hello file path tooclouddrive shows your storage account name and file share in hello URL.</span></span> <span data-ttu-id="3925b-175">Por ejemplo: `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="3925b-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

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

## <a name="transfer-local-files-toocloud-shell"></a><span data-ttu-id="3925b-176">Transferencia de archivos locales tooCloud Shell</span><span class="sxs-lookup"><span data-stu-id="3925b-176">Transfer local files tooCloud Shell</span></span>
<span data-ttu-id="3925b-177">Hola `clouddrive` sincronizaciones de directorio con la hoja de hello almacenamiento de portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3925b-177">hello `clouddrive` directory syncs with hello Azure portal storage blade.</span></span> <span data-ttu-id="3925b-178">Utilice este tooor de hoja tootransfer archivos locales desde el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="3925b-178">Use this blade tootransfer local files tooor from your file share.</span></span> <span data-ttu-id="3925b-179">Actualizar archivos desde el Shell de nube se refleja en el almacenamiento de archivos de hello GUI al actualizar la hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="3925b-179">Updating files from within Cloud Shell is reflected in hello file storage GUI when you refresh hello blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="3925b-180">Descarga de archivos</span><span class="sxs-lookup"><span data-stu-id="3925b-180">Download files</span></span>

![Lista de archivos locales](media/download.png)
1. <span data-ttu-id="3925b-182">En hello portal de Azure, vaya el recurso compartido de archivos montados de toohello.</span><span class="sxs-lookup"><span data-stu-id="3925b-182">In hello Azure portal, go toohello mounted file share.</span></span>
2. <span data-ttu-id="3925b-183">Seleccione el archivo de destino de hello.</span><span class="sxs-lookup"><span data-stu-id="3925b-183">Select hello target file.</span></span>
3. <span data-ttu-id="3925b-184">Seleccione hello **descargar** botón.</span><span class="sxs-lookup"><span data-stu-id="3925b-184">Select hello **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="3925b-185">Carga de archivos</span><span class="sxs-lookup"><span data-stu-id="3925b-185">Upload files</span></span>

![Toobe de archivos locales cargado](media/upload.png)
1. <span data-ttu-id="3925b-187">Vaya tooyour monta el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="3925b-187">Go tooyour mounted file share.</span></span>
2. <span data-ttu-id="3925b-188">Seleccione hello **cargar** botón.</span><span class="sxs-lookup"><span data-stu-id="3925b-188">Select hello **Upload** button.</span></span>
3. <span data-ttu-id="3925b-189">Seleccione el archivo hello o archivos que desee tooupload.</span><span class="sxs-lookup"><span data-stu-id="3925b-189">Select hello file or files that you want tooupload.</span></span>
4. <span data-ttu-id="3925b-190">Confirmar carga Hola.</span><span class="sxs-lookup"><span data-stu-id="3925b-190">Confirm hello upload.</span></span>

<span data-ttu-id="3925b-191">Ahora debería ver los archivos de Hola que son accesibles en su `clouddrive` directorio en el Shell de nube.</span><span class="sxs-lookup"><span data-stu-id="3925b-191">You should now see hello files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3925b-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3925b-192">Next steps</span></span>
[<span data-ttu-id="3925b-193">Inicio rápido de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="3925b-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="3925b-194">
[Información sobre Azure File Storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="3925b-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="3925b-195">
[Información sobre las etiquetas de Storage](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="3925b-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
