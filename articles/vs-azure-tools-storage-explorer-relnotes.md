---
title: "Notas de la versión de Explorador de Microsoft Azure Storage (versión preliminar) | Microsoft Docs"
description: "Notas de la versión de Explorador de Microsoft Azure Storage (versión preliminar)"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 63a24f6b153390533bba0888fd1051508c65bf6e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="51926-103">Notas de la versión de Explorador de Microsoft Azure Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="51926-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="51926-104">En este artículo se detallan las notas de la versión para la versión 0.8.16 del Explorador de Azure Storage (versión preliminar), así como las de versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="51926-104">This article contains the release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="51926-105">[Explorador de Microsoft Azure Storage (versión preliminar)](./vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente que permite trabajar fácilmente con los datos de Azure Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="51926-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="51926-106">Versión 0.8.16 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="51926-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="51926-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="51926-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="51926-108">Descarga del Explorador de Azure Storage 0.8.16 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="51926-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="51926-109">Explorador de Azure Storage 0.8.16 (versión preliminar) para Windows</span><span class="sxs-lookup"><span data-stu-id="51926-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="51926-110">Explorador de Azure Storage 0.8.16 (versión preliminar) para Mac</span><span class="sxs-lookup"><span data-stu-id="51926-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="51926-111">Explorador de Azure Storage 0.8.16 (versión preliminar) para Linux</span><span class="sxs-lookup"><span data-stu-id="51926-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="51926-112">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-112">New</span></span>
* <span data-ttu-id="51926-113">Al abrir un blob, el Explorador de Storage le pedirá que cargue el archivo descargado si se detectó un cambio</span><span class="sxs-lookup"><span data-stu-id="51926-113">When you open a blob, Storage Explorer will prompt you to upload the downloaded file if a change is detected</span></span>
* <span data-ttu-id="51926-114">Experiencia mejorada de inicio de sesión de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="51926-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="51926-115">Mejorado el rendimiento de la carga y descarga de muchos archivos pequeños al mismo tiempo</span><span class="sxs-lookup"><span data-stu-id="51926-115">Improved the performance of uploading/downloading many small files at the same time</span></span>


### <a name="fixes"></a><span data-ttu-id="51926-116">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-116">Fixes</span></span>
* <span data-ttu-id="51926-117">En algunos tipos de blob, al elegir la opción "reemplazar" durante un conflicto de carga, a veces provocaría que la carga se volviese a reiniciar.</span><span class="sxs-lookup"><span data-stu-id="51926-117">For some blob types, choosing to "replace" during an upload conflict would sometimes result in the upload being restarted.</span></span> 
* <span data-ttu-id="51926-118">En la versión 0.8.15, las cargas se detendrían a veces en un 99 %.</span><span class="sxs-lookup"><span data-stu-id="51926-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="51926-119">Al cargar archivos en un recurso compartido de archivos, si decide cargar en un directorio que todavía no existe, la carga produciría un error.</span><span class="sxs-lookup"><span data-stu-id="51926-119">When uploading files to a file share, if you chose to upload to a directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="51926-120">El Explorador de Storage estaba generando marcas de tiempo de forma incorrecta para las firmas de acceso compartido y las consultas de tabla.</span><span class="sxs-lookup"><span data-stu-id="51926-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="51926-121">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-121">Known Issues</span></span>
* <span data-ttu-id="51926-122">El uso de un nombre y una cadena de conexión de clave no funciona actualmente.</span><span class="sxs-lookup"><span data-stu-id="51926-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="51926-123">Funcionará en la próxima versión.</span><span class="sxs-lookup"><span data-stu-id="51926-123">It will be fixed in the next release.</span></span> <span data-ttu-id="51926-124">Hasta ese momento, puede usar la asociación con el nombre y la clave.</span><span class="sxs-lookup"><span data-stu-id="51926-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="51926-125">Si intenta abrir un archivo con un nombre de archivo de Windows no válido, la descarga provocará un error de archivo no encontrado.</span><span class="sxs-lookup"><span data-stu-id="51926-125">If you try to open a file with an invalid Windows file name, the download will result in a file not found error.</span></span>
* <span data-ttu-id="51926-126">Después de hacer clic en “Cancelar” en una tarea, puede que esta tarde un tiempo en cancelarse.</span><span class="sxs-lookup"><span data-stu-id="51926-126">After clicking "Cancel" on a task, it may take a while for that task to cancel.</span></span> <span data-ttu-id="51926-127">Se trata de una limitación de la biblioteca Azure Storage Node.</span><span class="sxs-lookup"><span data-stu-id="51926-127">This is a limitation of the Azure Storage Node library.</span></span>
* <span data-ttu-id="51926-128">Después de completar una carga de blobs, se actualiza la pestaña en la que se inició la carga.</span><span class="sxs-lookup"><span data-stu-id="51926-128">After completing a blob upload, the tab which initiated the upload is refreshed.</span></span> <span data-ttu-id="51926-129">Se trata de un cambio con respecto al comportamiento anterior y también provocará que se le devuelva a la raíz del contenedor en el que se halle.</span><span class="sxs-lookup"><span data-stu-id="51926-129">This is a change from previous behavior, and will also cause you to be taken back to the root of the container you are in.</span></span>
* <span data-ttu-id="51926-130">Si no elige el certificado de tarjeta inteligente o PIN adecuados, tendrá que reiniciar para que el Explorador de Storage olvide esa decisión.</span><span class="sxs-lookup"><span data-stu-id="51926-130">If you choose the wrong PIN/Smartcard certificate, then you will need to restart in order to have Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="51926-131">El panel de configuración de la cuenta puede indicar que necesita especificar de nuevo las credenciales para filtrar las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="51926-131">The account settings panel may show that you need to reenter credentials to filter subscriptions.</span></span>
* <span data-ttu-id="51926-132">Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="51926-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="51926-133">Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.</span><span class="sxs-lookup"><span data-stu-id="51926-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="51926-134">Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada.</span><span class="sxs-lookup"><span data-stu-id="51926-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="51926-135">Los usuarios de Ubuntu 14.04 tendrán que asegurarse de que GCC está actualizado. Para ello, se pueden ejecutar los siguientes comandos. Después, es necesario reiniciar la máquina:</span><span class="sxs-lookup"><span data-stu-id="51926-135">For users on Ubuntu 14.04, you will need to ensure GCC is up to date - this can be done by running the following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="51926-136">Los usuarios de Ubuntu 17.04 tendrán que instalar GConf. Esto se puede hacer mediante la ejecución de los siguientes comandos. Después de esto, es necesario reiniciar la máquina.</span><span class="sxs-lookup"><span data-stu-id="51926-136">For users on Ubuntu 17.04, you will need to install GConf - this can be done by running the following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="51926-137">Versión 0.8.14 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="51926-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="51926-138">22/06/2017</span><span class="sxs-lookup"><span data-stu-id="51926-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="51926-139">Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="51926-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="51926-140">Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar) para Windows</span><span class="sxs-lookup"><span data-stu-id="51926-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="51926-141">Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar) para Mac</span><span class="sxs-lookup"><span data-stu-id="51926-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="51926-142">Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar) para Linux</span><span class="sxs-lookup"><span data-stu-id="51926-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="51926-143">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-143">New</span></span>

* <span data-ttu-id="51926-144">Versión de Electron actualizada a la 1.7.2 para aprovechar las múltiples actualizaciones de seguridad críticas</span><span class="sxs-lookup"><span data-stu-id="51926-144">Updated Electron version to 1.7.2 in order to take advantage of several critical security updates</span></span>
* <span data-ttu-id="51926-145">Ahora se puede acceder rápidamente a la guía de solución de problemas en línea desde el menú de ayuda</span><span class="sxs-lookup"><span data-stu-id="51926-145">You can now quickly access the online troubleshooting guide from the help menu</span></span>
* <span data-ttu-id="51926-146">[Guía][2] de solución de problemas del Explorador de Storage</span><span class="sxs-lookup"><span data-stu-id="51926-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="51926-147">[Instrucciones][3] sobre cómo conectarse a una suscripción de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="51926-147">[Instructions][3] on connecting to an Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="51926-148">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-148">Known Issues</span></span>

* <span data-ttu-id="51926-149">Los botones del cuadro de diálogo de confirmación de eliminación de carpeta no registran los clics del mouse en Linux.</span><span class="sxs-lookup"><span data-stu-id="51926-149">Buttons on the delete folder confirmation dialog don't register with the mouse clicks on Linux.</span></span> <span data-ttu-id="51926-150">La solución alternativa consiste en usar la tecla Entrar.</span><span class="sxs-lookup"><span data-stu-id="51926-150">Workaround is to use the Enter key</span></span>
* <span data-ttu-id="51926-151">Si no elige el certificado de tarjeta inteligente o el PIN adecuados, tendrá que reiniciar para que el Explorador de Storage olvide la decisión.</span><span class="sxs-lookup"><span data-stu-id="51926-151">If you choose the wrong PIN/Smartcard certificate then you will need to restart in order to have Storage Explorer forget the decision</span></span>
* <span data-ttu-id="51926-152">Si hay más de tres grupos de blobs o archivos cargándose al mismo tiempo, se pueden producir errores.</span><span class="sxs-lookup"><span data-stu-id="51926-152">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="51926-153">El panel de configuración de la cuenta puede indicar que necesita especificar de nuevo las credenciales para filtrar las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="51926-153">The account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="51926-154">Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="51926-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="51926-155">Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.</span><span class="sxs-lookup"><span data-stu-id="51926-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="51926-156">Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada.</span><span class="sxs-lookup"><span data-stu-id="51926-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="51926-157">La instalación de Ubuntu 14.04 requiere que se actualice la versión de gcc. A continuación puede ver los pasos para actualizarla:</span><span class="sxs-lookup"><span data-stu-id="51926-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="51926-158">Versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="51926-158">Previous releases</span></span>

* [<span data-ttu-id="51926-159">Versión 0.8.13</span><span class="sxs-lookup"><span data-stu-id="51926-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="51926-160">Versión 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="51926-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="51926-161">Versión 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="51926-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="51926-162">Versión 0.8.7</span><span class="sxs-lookup"><span data-stu-id="51926-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="51926-163">Versión 0.8.6</span><span class="sxs-lookup"><span data-stu-id="51926-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="51926-164">Versión 0.8.5</span><span class="sxs-lookup"><span data-stu-id="51926-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="51926-165">Versión 0.8.4</span><span class="sxs-lookup"><span data-stu-id="51926-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="51926-166">Versión 0.8.3</span><span class="sxs-lookup"><span data-stu-id="51926-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="51926-167">Versión 0.8.2</span><span class="sxs-lookup"><span data-stu-id="51926-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="51926-168">Versión 0.8.0</span><span class="sxs-lookup"><span data-stu-id="51926-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="51926-169">Versión 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="51926-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="51926-170">Versión 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="51926-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="51926-171">Versión 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="51926-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="51926-172">Versión 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="51926-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="51926-173">Versión 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="51926-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="51926-174">Versión 0.8.13</span><span class="sxs-lookup"><span data-stu-id="51926-174">Version 0.8.13</span></span>
<span data-ttu-id="51926-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="51926-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="51926-176">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-176">New</span></span>

* <span data-ttu-id="51926-177">[Guía][2] de solución de problemas del Explorador de Storage</span><span class="sxs-lookup"><span data-stu-id="51926-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="51926-178">[Instrucciones][3] sobre cómo conectarse a una suscripción de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="51926-178">[Instructions][3] on connecting to an Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-179">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-179">Fixes</span></span>

* <span data-ttu-id="51926-180">Problema corregido: Había una alta probabilidad de que, al cargar un archivo, se produjese un error de memoria agotada.</span><span class="sxs-lookup"><span data-stu-id="51926-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="51926-181">Problema corregido: Ahora puede iniciar sesión con una tarjeta inteligente o un PIN.</span><span class="sxs-lookup"><span data-stu-id="51926-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="51926-182">Problema corregido: Abrir en Portal ahora funciona con Azure China, Azure Germany, Azure US Government y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="51926-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="51926-183">Problema corregido: Al cargar una carpeta en un contenedor de blobs, a veces se produce un error de “operación ilegal”.</span><span class="sxs-lookup"><span data-stu-id="51926-183">Fixed: While uploading a folder to a blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="51926-184">Problema corregido: Seleccionar todo se deshabilita durante la administración de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="51926-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="51926-185">Problema corregido: Los metadatos del blob base puede que se sobrescriban después de ver las propiedades de las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="51926-185">Fixed: The metadata of the base blob might get overwritten after viewing the properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-186">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-186">Known Issues</span></span>

* <span data-ttu-id="51926-187">Si no elige el certificado de tarjeta inteligente o el PIN adecuados, tendrá que reiniciar para que el Explorador de Storage olvide la decisión.</span><span class="sxs-lookup"><span data-stu-id="51926-187">If you choose the wrong PIN/Smartcard certificate then you will need to restart in order to have Storage Explorer forget the decision</span></span>
* <span data-ttu-id="51926-188">Cuando se amplía o reduce, el nivel de zoom puede restablecerse momentáneamente al nivel predeterminado.</span><span class="sxs-lookup"><span data-stu-id="51926-188">While zoomed in or out, the zoom level may momentarily reset to the default level</span></span>
* <span data-ttu-id="51926-189">Si hay más de tres grupos de blobs o archivos cargándose al mismo tiempo, se pueden producir errores.</span><span class="sxs-lookup"><span data-stu-id="51926-189">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="51926-190">El panel de configuración de la cuenta puede indicar que necesita especificar de nuevo las credenciales para filtrar las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="51926-190">The account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="51926-191">Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="51926-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="51926-192">Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.</span><span class="sxs-lookup"><span data-stu-id="51926-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="51926-193">Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada.</span><span class="sxs-lookup"><span data-stu-id="51926-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="51926-194">La instalación de Ubuntu 14.04 requiere que se actualice la versión de gcc. A continuación puede ver los pasos para actualizarla:</span><span class="sxs-lookup"><span data-stu-id="51926-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="51926-195">Versión 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="51926-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="51926-196">07/04/2017</span><span class="sxs-lookup"><span data-stu-id="51926-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="51926-197">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-197">New</span></span>

* <span data-ttu-id="51926-198">Explorador de Storage ahora se cerrará automáticamente al instalar una actualización desde la notificación de actualización.</span><span class="sxs-lookup"><span data-stu-id="51926-198">Storage Explorer will now automatically close when you install an update from the update notification</span></span>
* <span data-ttu-id="51926-199">El acceso rápido local proporciona una experiencia mejorada a la hora de trabajar con los recursos a los que accede con más frecuencia.</span><span class="sxs-lookup"><span data-stu-id="51926-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="51926-200">En el editor de contenedores de blobs, ahora puede ver a qué máquina virtual pertenece un blob concedido.</span><span class="sxs-lookup"><span data-stu-id="51926-200">In the Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="51926-201">Ahora puede contraer el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="51926-201">You can now collapse the left side panel</span></span>
* <span data-ttu-id="51926-202">Ahora la detección se ejecuta al mismo tiempo que la descarga.</span><span class="sxs-lookup"><span data-stu-id="51926-202">Discovery now runs at the same time as download</span></span>
* <span data-ttu-id="51926-203">Use Estadísticas del contenedor de blobs, el recurso compartido de archivos y los editores de tablas para ver el tamaño del recurso o de la selección.</span><span class="sxs-lookup"><span data-stu-id="51926-203">Use Statistics in the Blob Container, File Share, and Table editors to see the size of your resource or selection</span></span>
* <span data-ttu-id="51926-204">Ahora puede iniciar sesión en Azure Active Directory (AAD) basándose en cuentas de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="51926-204">You can now sign-in to Azure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="51926-205">Ahora puede cargar archivos de archivo de más de 32 MB en cuentas de almacenamiento Premium.</span><span class="sxs-lookup"><span data-stu-id="51926-205">You can now upload archive files over 32MB to Premium storage accounts</span></span>
* <span data-ttu-id="51926-206">Compatibilidad de accesibilidad mejorada.</span><span class="sxs-lookup"><span data-stu-id="51926-206">Improved accessibility support</span></span>
* <span data-ttu-id="51926-207">Ahora puede agregar certificados SSL X.509 cifrados en Base-64 de confianza en Editar -&gt; Certificados SSL -&gt; Importar certificados.</span><span class="sxs-lookup"><span data-stu-id="51926-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going to Edit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-208">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-208">Fixes</span></span>

* <span data-ttu-id="51926-209">Problema corregido: Después de actualizar las credenciales de una cuenta, a veces no se actualizaba la vista de árbol.</span><span class="sxs-lookup"><span data-stu-id="51926-209">Fixed: after refreshing an account's credentials, the tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="51926-210">Problema corregido: Al generar un SAS para tablas y colas de emulador, se producía una URL no válida.</span><span class="sxs-lookup"><span data-stu-id="51926-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="51926-211">Problema corregido: Las cuentas de almacenamiento premium ahora se pueden ampliar mientras haya un proxy habilitado.</span><span class="sxs-lookup"><span data-stu-id="51926-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="51926-212">Problema corregido: El botón Aplicar de la página de administración de cuentas no funcionaba si había una o cero cuentas seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="51926-212">Fixed: the apply button on the accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="51926-213">Problema corregido: Se puede producir un error al cargar blobs que requieran resoluciones de conflictos. Esto se ha corregido en la versión 0.8.11.</span><span class="sxs-lookup"><span data-stu-id="51926-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="51926-214">Problema corregido: No se podían enviar comentarios en la versión 0.8.11. Corregido en la versión 0.8.12.</span><span class="sxs-lookup"><span data-stu-id="51926-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="51926-215">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-215">Known Issues</span></span>

* <span data-ttu-id="51926-216">Después de actualizar a la versión 0.8.10, tendrá que actualizar todas las credenciales.</span><span class="sxs-lookup"><span data-stu-id="51926-216">After upgrading to 0.8.10, you will need to refresh all of your credentials.</span></span>
* <span data-ttu-id="51926-217">Cuando se amplía o reduce, el nivel de zoom puede restablecerse momentáneamente al nivel predeterminado.</span><span class="sxs-lookup"><span data-stu-id="51926-217">While zoomed in or out, the zoom level may momentarily reset to the default level.</span></span>
* <span data-ttu-id="51926-218">Si hay más de tres grupos de blobs o archivos cargándose al mismo tiempo, se pueden producir errores.</span><span class="sxs-lookup"><span data-stu-id="51926-218">Having more than 3 groups of blobs or files uploading at the same time may cause errors.</span></span>
* <span data-ttu-id="51926-219">El panel de configuración de la cuenta puede indicar que necesita especificar de nuevo las credenciales para filtrar las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="51926-219">The account settings panel may show that you need to reenter credentials in order to filter subscriptions.</span></span>
* <span data-ttu-id="51926-220">Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="51926-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="51926-221">Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.</span><span class="sxs-lookup"><span data-stu-id="51926-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="51926-222">Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada.</span><span class="sxs-lookup"><span data-stu-id="51926-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="51926-223">La instalación de Ubuntu 14.04 requiere que se actualice la versión de gcc. A continuación puede ver los pasos para actualizarla:</span><span class="sxs-lookup"><span data-stu-id="51926-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="51926-224">Versión 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="51926-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="51926-225">23/02/2017</span><span class="sxs-lookup"><span data-stu-id="51926-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="51926-226">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-226">New</span></span>

* <span data-ttu-id="51926-227">Explorador de Storage 0.8.9 descargará automáticamente la última versión de las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="51926-227">Storage Explorer 0.8.9 will automatically download the latest version for updates.</span></span>
* <span data-ttu-id="51926-228">Revisión: Al usar un URI de SAS generado en el portal para conectarse a una cuenta de almacenamiento, se producía un error.</span><span class="sxs-lookup"><span data-stu-id="51926-228">Hotfix: using a portal generated SAS URI to attach a storage account would result in an error.</span></span>
* <span data-ttu-id="51926-229">Ahora puede crear, administrar y promover instantáneas de blobs.</span><span class="sxs-lookup"><span data-stu-id="51926-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="51926-230">Ahora puede iniciar sesión en cuentas de Azure China, Azure Germany y Azure US Government.</span><span class="sxs-lookup"><span data-stu-id="51926-230">You can now sign in to Azure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="51926-231">Ahora puede cambiar el nivel de zoom.</span><span class="sxs-lookup"><span data-stu-id="51926-231">You can now change the zoom level.</span></span> <span data-ttu-id="51926-232">Use las opciones del menú Ver para acercar, alejar y restablecer el zoom.</span><span class="sxs-lookup"><span data-stu-id="51926-232">Use the options in the View menu to Zoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="51926-233">Ahora se admiten caracteres Unicode en los metadatos de usuarios para blobs y archivos.</span><span class="sxs-lookup"><span data-stu-id="51926-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="51926-234">Mejoras de accesibilidad.</span><span class="sxs-lookup"><span data-stu-id="51926-234">Accessibility improvements.</span></span>
* <span data-ttu-id="51926-235">Las notas de la versión de la siguiente versión se pueden ver desde la notificación de actualización.</span><span class="sxs-lookup"><span data-stu-id="51926-235">The next version's release notes can be viewed from the update notification.</span></span> <span data-ttu-id="51926-236">También puede ver las notas de la versión actual desde el menú Ayuda.</span><span class="sxs-lookup"><span data-stu-id="51926-236">You can also view the current release notes from the Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-237">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-237">Fixes</span></span>

* <span data-ttu-id="51926-238">Problema corregido: El número de versión ahora se muestra correctamente en el Panel de control de Windows.</span><span class="sxs-lookup"><span data-stu-id="51926-238">Fixed: the version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="51926-239">Problema corregido: La búsqueda ya no está limitada a 50 000 nodos.</span><span class="sxs-lookup"><span data-stu-id="51926-239">Fixed: search is no longer limited to 50,000 nodes</span></span>
* <span data-ttu-id="51926-240">Problema corregido: La carga a un recurso compartido de archivos se alargaba infinitamente si el directorio de destino no existía anteriormente.</span><span class="sxs-lookup"><span data-stu-id="51926-240">Fixed: upload to a file share spun forever if the destination directory did not already exist</span></span>
* <span data-ttu-id="51926-241">Problema corregido: Estabilidad mejorada para cargas y descargas largas.</span><span class="sxs-lookup"><span data-stu-id="51926-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-242">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-242">Known Issues</span></span>

* <span data-ttu-id="51926-243">Cuando se amplía o reduce, el nivel de zoom puede restablecerse momentáneamente al nivel predeterminado.</span><span class="sxs-lookup"><span data-stu-id="51926-243">While zoomed in or out, the zoom level may momentarily reset to the default level.</span></span>
* <span data-ttu-id="51926-244">Acceso rápido solo funciona con elementos basados en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="51926-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="51926-245">En esta versión no se admiten recursos locales o recursos adjuntados a través de la clave o token de SAS.</span><span class="sxs-lookup"><span data-stu-id="51926-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="51926-246">Es posible que Acceso rápido tarde unos segundos en desplazarse hasta el recurso de destino, en función del número de recursos que tenga.</span><span class="sxs-lookup"><span data-stu-id="51926-246">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="51926-247">Si hay más de tres grupos de blobs o archivos cargándose al mismo tiempo, se pueden producir errores.</span><span class="sxs-lookup"><span data-stu-id="51926-247">Having more than 3 groups of blobs or files uploading at the same time may cause errors.</span></span>

<span data-ttu-id="51926-248">16/12/2016</span><span class="sxs-lookup"><span data-stu-id="51926-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="51926-249">Versión 0.8.7</span><span class="sxs-lookup"><span data-stu-id="51926-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="51926-250">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-250">New</span></span>

* <span data-ttu-id="51926-251">Puede elegir cómo resolver conflictos al principio de una actualización, descarga o sesión de copia en la ventana Actividades.</span><span class="sxs-lookup"><span data-stu-id="51926-251">You can choose how to resolve conflicts at the beginning of an update, download or copy session in the Activities window</span></span>
* <span data-ttu-id="51926-252">Mantenga el puntero sobre una pestaña para ver la ruta de acceso completa del recurso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="51926-252">Hover over a tab to see the full path of the storage resource</span></span>
* <span data-ttu-id="51926-253">Al hacer clic en una pestaña, se sincroniza con su ubicación en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="51926-253">When you click on a tab, it synchronizes with its location in the left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-254">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-254">Fixes</span></span>

* <span data-ttu-id="51926-255">Problema corregido: El Explorador de Storage es ahora una aplicación de confianza en Mac.</span><span class="sxs-lookup"><span data-stu-id="51926-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="51926-256">Problema corregido: Ubuntu 14.04 se admite de nuevo.</span><span class="sxs-lookup"><span data-stu-id="51926-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="51926-257">Problema corregido: En ocasiones, la interfaz de usuario para agregar una cuenta parpadea al cargar las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="51926-257">Fixed: Sometimes the add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="51926-258">Problema corregido: En ocasiones, no todos los recursos de almacenamiento se muestran en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="51926-258">Fixed: Sometimes not all storage resources were listed in the left side navigation pane</span></span>
* <span data-ttu-id="51926-259">Problema corregido: El panel de acciones a veces muestra acciones vacías.</span><span class="sxs-lookup"><span data-stu-id="51926-259">Fixed: The action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="51926-260">Problema corregido: Ahora se conserva el tamaño de la ventana de la última sesión que se cerró.</span><span class="sxs-lookup"><span data-stu-id="51926-260">Fixed: The window size from the last closed session is now retained</span></span>
* <span data-ttu-id="51926-261">Problema corregido: Se pueden abrir varias pestañas para el mismo recurso mediante el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="51926-261">Fixed: You can open multiple tabs for the same resource using the context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-262">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-262">Known Issues</span></span>

* <span data-ttu-id="51926-263">Acceso rápido solo funciona con elementos basados en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="51926-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="51926-264">En esta versión no se admiten recursos locales o recursos adjuntados a través de la clave o token de SAS.</span><span class="sxs-lookup"><span data-stu-id="51926-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="51926-265">Es posible que Acceso rápido tarde unos segundos en desplazarse hasta el recurso de destino, en función del número de recursos que tenga.</span><span class="sxs-lookup"><span data-stu-id="51926-265">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="51926-266">Si hay más de tres grupos de blobs o archivos cargándose al mismo tiempo, se pueden producir errores.</span><span class="sxs-lookup"><span data-stu-id="51926-266">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="51926-267">Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado o se pueden producir excepciones no controladas.</span><span class="sxs-lookup"><span data-stu-id="51926-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="51926-268">Por primera vez con el Explorador de Storage en macOS, es posible que aparezcan varias solicitudes que piden permiso del usuario para acceder a las llaves.</span><span class="sxs-lookup"><span data-stu-id="51926-268">For the first time using the Storage Explorer on macOS, you might see multiple prompts asking for user's permission to access keychain.</span></span> <span data-ttu-id="51926-269">Se recomienda seleccionar Permitir siempre para que la solicitud no vuelva a aparecer más.</span><span class="sxs-lookup"><span data-stu-id="51926-269">We suggest you select Always Allow so the prompt won't show up again</span></span>

<span data-ttu-id="51926-270">18/11/2016</span><span class="sxs-lookup"><span data-stu-id="51926-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="51926-271">Versión 0.8.6</span><span class="sxs-lookup"><span data-stu-id="51926-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="51926-272">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-272">New</span></span>

* <span data-ttu-id="51926-273">Ya puede anclar los servicios más utilizados en Acceso rápido para facilitar la navegación.</span><span class="sxs-lookup"><span data-stu-id="51926-273">You can now pin most frequently used services to the Quick Access for easy navigation</span></span>
* <span data-ttu-id="51926-274">Ya puede abrir varios editores en diferentes pestañas.</span><span class="sxs-lookup"><span data-stu-id="51926-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="51926-275">Haga un solo clic para abrir una pestaña temporal y doble clic para abrir una pestaña permanente. También puede hacer clic en la pestaña temporal para que se convierta en una pestaña permanente.</span><span class="sxs-lookup"><span data-stu-id="51926-275">Single click to open a temporary tab; double click to open a permanent tab. You can also click on the temporary tab to make it a permanent tab</span></span>
* <span data-ttu-id="51926-276">Hemos realizado mejoras notables de rendimiento y estabilidad para cargas y descargas, especialmente para archivos de gran tamaño en máquinas rápidas</span><span class="sxs-lookup"><span data-stu-id="51926-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="51926-277">Las carpetas vacías "virtuales" ya se pueden crear en contenedores de blobs.</span><span class="sxs-lookup"><span data-stu-id="51926-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="51926-278">Hemos vuelto a incorporar la búsqueda en ámbito con la nueva y mejorada búsqueda de subcadenas, por lo que ahora tiene dos opciones para realizar búsquedas:</span><span class="sxs-lookup"><span data-stu-id="51926-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="51926-279">Búsqueda global: solo tiene que indicar un término de búsqueda en el cuadro de texto de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="51926-279">Global search - just enter a search term into the search textbox</span></span>
    * <span data-ttu-id="51926-280">Búsqueda de ámbito: haga clic en el icono de lupa al lado de un nodo; después, agregue un término de búsqueda al final de la ruta o haga clic con el botón derecho y seleccione “Buscar desde aquí”.</span><span class="sxs-lookup"><span data-stu-id="51926-280">Scoped search - click the magnifying glass icon next to a node, then add a search term to the end of the path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="51926-281">Hemos agregado varios temas: claro (valor predeterminado), oscuro, negro en alto contraste y blanco en alto contraste.</span><span class="sxs-lookup"><span data-stu-id="51926-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="51926-282">Vaya a Editar -&gt; Temas para cambiar las preferencias de temas.</span><span class="sxs-lookup"><span data-stu-id="51926-282">Go to Edit -&gt; Themes to change your theming preference</span></span>
* <span data-ttu-id="51926-283">Puede modificar las propiedades de blobs y archivos.</span><span class="sxs-lookup"><span data-stu-id="51926-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="51926-284">Ahora se admiten mensajes de cola cifrados (Base64) y sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="51926-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="51926-285">En Linux, ahora es necesario usar un sistema operativo de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="51926-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="51926-286">En esta versión solo se admite Ubuntu 16.04.1 LTS de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="51926-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="51926-287">¡Hemos actualizado nuestro logotipo!</span><span class="sxs-lookup"><span data-stu-id="51926-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-288">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-288">Fixes</span></span>

* <span data-ttu-id="51926-289">Problema corregido: Problemas de inmovilización de pantalla</span><span class="sxs-lookup"><span data-stu-id="51926-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="51926-290">Problema corregido: Mayor seguridad</span><span class="sxs-lookup"><span data-stu-id="51926-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="51926-291">Problema corregido: A veces, podrían aparecer cuentas conectadas duplicadas.</span><span class="sxs-lookup"><span data-stu-id="51926-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="51926-292">Problema corregido: Un blob con un tipo de contenido sin definir podría generar una excepción.</span><span class="sxs-lookup"><span data-stu-id="51926-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="51926-293">Problema corregido: No se podía abrir el Panel de consulta en una tabla vacía.</span><span class="sxs-lookup"><span data-stu-id="51926-293">Fixed: Opening the Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="51926-294">Problema corregido: Varios errores en la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="51926-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="51926-295">Problema corregido: Aumento del número de recursos que se cargan de 50 a 100 al hacer clic en “Cargar más”.</span><span class="sxs-lookup"><span data-stu-id="51926-295">Fixed: Increased the number of resources loaded from 50 to 100 when clicking "Load More"</span></span>
* <span data-ttu-id="51926-296">Problema corregido: En la primera ejecución, si ha iniciado sesión con una cuenta, ahora se seleccionan todas las suscripciones para esa cuenta de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="51926-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="51926-297">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-297">Known Issues</span></span>

* <span data-ttu-id="51926-298">Esta versión del Explorador de Storage no se ejecuta en Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="51926-298">This release of the Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="51926-299">Para abrir varias pestañas para el mismo recurso, no haga clic varias veces en el mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="51926-299">To open multiple tabs for the same resource, do not continuously click on the same resource.</span></span> <span data-ttu-id="51926-300">Haga clic en otro recurso y, después, vuelva y haga clic en el recurso original para volver a abrirlo en otra pestaña.</span><span class="sxs-lookup"><span data-stu-id="51926-300">Click on another resource and then go back and then click on the original resource to open it again in another tab</span></span> 
* <span data-ttu-id="51926-301">Acceso rápido solo funciona con elementos basados en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="51926-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="51926-302">En esta versión no se admiten recursos locales o recursos adjuntados a través de la clave o token de SAS.</span><span class="sxs-lookup"><span data-stu-id="51926-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="51926-303">Es posible que Acceso rápido tarde unos segundos en desplazarse hasta el recurso de destino, en función del número de recursos que tenga.</span><span class="sxs-lookup"><span data-stu-id="51926-303">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="51926-304">Si hay más de tres grupos de blobs o archivos cargándose al mismo tiempo, se pueden producir errores.</span><span class="sxs-lookup"><span data-stu-id="51926-304">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="51926-305">Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado o se pueden producir excepciones no controladas.</span><span class="sxs-lookup"><span data-stu-id="51926-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="51926-306">03/10/2016</span><span class="sxs-lookup"><span data-stu-id="51926-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="51926-307">Versión 0.8.5</span><span class="sxs-lookup"><span data-stu-id="51926-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="51926-308">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-308">New</span></span>

* <span data-ttu-id="51926-309">Ahora puede usar claves SAS generadas por el Portal para conectarse a cuentas de almacenamiento y recursos</span><span class="sxs-lookup"><span data-stu-id="51926-309">Can now use Portal-generated SAS keys to attach to Storage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-310">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-310">Fixes</span></span>

* <span data-ttu-id="51926-311">Problema corregido: A veces, la condición de carrera durante las búsquedas provocaba que los nodos no se pudiesen expandir.</span><span class="sxs-lookup"><span data-stu-id="51926-311">Fixed: race condition during search sometimes caused nodes to become non-expandable</span></span>
* <span data-ttu-id="51926-312">Problema corregido: “Usar HTTP” no funciona al conectarse a cuentas de almacenamiento con un nombre de cuenta y una clave.</span><span class="sxs-lookup"><span data-stu-id="51926-312">Fixed: "Use HTTP" doesn't work when connecting to Storage Accounts with account name and key</span></span>
* <span data-ttu-id="51926-313">Problema corregido: Las claves SAS (especialmente las generadas en el Portal) devuelven un error de “barra oblicua final”.</span><span class="sxs-lookup"><span data-stu-id="51926-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="51926-314">Problema corregido: Problemas al importar tablas.</span><span class="sxs-lookup"><span data-stu-id="51926-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="51926-315">A veces se revertían la clave de fila y la clave de partición</span><span class="sxs-lookup"><span data-stu-id="51926-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="51926-316">No se puede leer las claves de partición “null”.</span><span class="sxs-lookup"><span data-stu-id="51926-316">Unable to read "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-317">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-317">Known Issues</span></span>

* <span data-ttu-id="51926-318">Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado.</span><span class="sxs-lookup"><span data-stu-id="51926-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="51926-319">Azure Stack no admite Files actualmente por lo que, al intentar expandir Files, se produce un error.</span><span class="sxs-lookup"><span data-stu-id="51926-319">Azure Stack doesn't currently support Files, so trying to expand Files will show an error</span></span>

<span data-ttu-id="51926-320">12/09/2016</span><span class="sxs-lookup"><span data-stu-id="51926-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="51926-321">Versión 0.8.4</span><span class="sxs-lookup"><span data-stu-id="51926-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="51926-322">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-322">New</span></span>

* <span data-ttu-id="51926-323">Genere vínculos directos a cuentas de almacenamiento, contenedores, colas, tablas o recursos compartidos de archivos para compartir y acceder fácilmente a sus recursos. Es compatible con Windows y Mac OS.</span><span class="sxs-lookup"><span data-stu-id="51926-323">Generate direct links to storage accounts, containers, queues, tables, or file shares for sharing and easy access to your resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="51926-324">Busque contenedores de blobs, tablas, colas, recursos compartidos de archivos o cuentas de almacenamiento en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="51926-324">Search for your blob containers, tables, queues, file shares, or storage accounts from the search box</span></span>
* <span data-ttu-id="51926-325">Ahora puede agrupar las cláusulas en el generador de consultas de tablas.</span><span class="sxs-lookup"><span data-stu-id="51926-325">You can now group clauses in the table query builder</span></span>
* <span data-ttu-id="51926-326">Cambie el nombre y copie y pegue contenedores de blobs, recursos compartidos de archivos, tablas, blobs, carpetas de blobs, archivos y directorios desde cuentas conectadas mediante SAS y contenedores.</span><span class="sxs-lookup"><span data-stu-id="51926-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="51926-327">Al cambiar el nombre y copiar contenedores de blobs y recursos compartidos de archivos, ahora se conservan las propiedades y los metadatos.</span><span class="sxs-lookup"><span data-stu-id="51926-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-328">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-328">Fixes</span></span>

* <span data-ttu-id="51926-329">Problema corregido: No se pueden editar las entidades de tablas si contienen propiedades binarias o booleanas.</span><span class="sxs-lookup"><span data-stu-id="51926-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-330">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-330">Known Issues</span></span>

* <span data-ttu-id="51926-331">Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado.</span><span class="sxs-lookup"><span data-stu-id="51926-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="51926-332">03/08/2016</span><span class="sxs-lookup"><span data-stu-id="51926-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="51926-333">Versión 0.8.3</span><span class="sxs-lookup"><span data-stu-id="51926-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="51926-334">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-334">New</span></span>

* <span data-ttu-id="51926-335">Cambie el nombre de contenedores, tablas y recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="51926-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="51926-336">Experiencia mejorada con el generador de consultas.</span><span class="sxs-lookup"><span data-stu-id="51926-336">Improved Query builder experience</span></span>
* <span data-ttu-id="51926-337">Posibilidad de guardar y cargar consultas.</span><span class="sxs-lookup"><span data-stu-id="51926-337">Ability to save and load queries</span></span>
* <span data-ttu-id="51926-338">Vínculos directos a cuentas de almacenamiento o contenedores, colas, tablas o recursos compartidos de archivos para compartir y acceder fácilmente a los recursos (solo disponible para Windows, macOS se admitirá pronto).</span><span class="sxs-lookup"><span data-stu-id="51926-338">Direct links to storage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="51926-339">Capacidad para administrar y configurar reglas de CORS</span><span class="sxs-lookup"><span data-stu-id="51926-339">Ability to manage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-340">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-340">Fixes</span></span>

* <span data-ttu-id="51926-341">Problema corregido: Las cuentas de Microsoft requieren que vuelva a autenticarse en períodos de 8 a 12 horas.</span><span class="sxs-lookup"><span data-stu-id="51926-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-342">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-342">Known Issues</span></span>

* <span data-ttu-id="51926-343">A veces, puede que parezca que la IU se bloquea. Este problema se resuelve maximizando la ventana.</span><span class="sxs-lookup"><span data-stu-id="51926-343">Sometimes the UI might appear frozen - maximizing the window helps resolve this issue</span></span>
* <span data-ttu-id="51926-344">Puede que la instalación en macOS requiera permisos elevados.</span><span class="sxs-lookup"><span data-stu-id="51926-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="51926-345">El panel de configuración de la cuenta puede indicar que necesita especificar de nuevo las credenciales para filtrar las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="51926-345">Account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="51926-346">Al cambiar de nombre los recursos compartidos, contenedores de blobs y tablas, no se conservan los metadatos ni otras propiedades del contenedor, como la cuota de uso compartido de archivos, el nivel de acceso público ni las directivas de acceso.</span><span class="sxs-lookup"><span data-stu-id="51926-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on the container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="51926-347">Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="51926-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="51926-348">Todas las otras propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.</span><span class="sxs-lookup"><span data-stu-id="51926-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="51926-349">No se puede copiar o cambiar de nombre recursos en cuentas conectadas mediante SAS.</span><span class="sxs-lookup"><span data-stu-id="51926-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="51926-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="51926-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="51926-351">Versión 0.8.2</span><span class="sxs-lookup"><span data-stu-id="51926-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="51926-352">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-352">New</span></span>

* <span data-ttu-id="51926-353">Las cuentas de almacenamiento se agrupan por suscripciones; el almacenamiento de desarrollo y los recursos conectados mediante clave o SAS se muestran en el nodo (Local y Adjuntos).</span><span class="sxs-lookup"><span data-stu-id="51926-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="51926-354">Cierre la sesión de las cuentas en el panel “Configuración de la cuenta de Azure”.</span><span class="sxs-lookup"><span data-stu-id="51926-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="51926-355">Configure el proxy para habilitar y administrar el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="51926-355">Configure proxy settings to enable and manage sign-in</span></span>
* <span data-ttu-id="51926-356">Cree y rompa concesiones de blobs.</span><span class="sxs-lookup"><span data-stu-id="51926-356">Create and break blob leases</span></span>
* <span data-ttu-id="51926-357">Abra contenedores de blobs, colas, tablas y archivos con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="51926-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-358">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-358">Fixes</span></span>

* <span data-ttu-id="51926-359">Problema corregido: Los mensajes de cola insertados con bibliotecas de Java o .NET no se descodifican correctamente desde Base64.</span><span class="sxs-lookup"><span data-stu-id="51926-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="51926-360">Problema corregido: Las tablas de $metrics no se muestran en las cuentas de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="51926-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="51926-361">Problema corregido: El nodo de tablas no funciona para el almacenamiento local (desarrollo).</span><span class="sxs-lookup"><span data-stu-id="51926-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-362">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-362">Known Issues</span></span>

* <span data-ttu-id="51926-363">Puede que la instalación en macOS requiera permisos elevados.</span><span class="sxs-lookup"><span data-stu-id="51926-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="51926-364">15/06/2016</span><span class="sxs-lookup"><span data-stu-id="51926-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="51926-365">Versión 0.8.0</span><span class="sxs-lookup"><span data-stu-id="51926-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="51926-366">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-366">New</span></span>

* <span data-ttu-id="51926-367">Compatibilidad con recursos compartidos de archivos: visualización, carga, descarga, copia de archivos y directorios, URI de SAS (creación y conexión).</span><span class="sxs-lookup"><span data-stu-id="51926-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="51926-368">Mejoras de la experiencia del usuario para conectarse a Storage con URI de SAS o claves de cuentas.</span><span class="sxs-lookup"><span data-stu-id="51926-368">Improved user experience for connecting to Storage with SAS URIs or account keys</span></span>
* <span data-ttu-id="51926-369">Exportación de resultados de consulta de tabla.</span><span class="sxs-lookup"><span data-stu-id="51926-369">Export table query results</span></span>
* <span data-ttu-id="51926-370">Reordenación y personalización de columnas de tabla.</span><span class="sxs-lookup"><span data-stu-id="51926-370">Table column reordering and customization</span></span>
* <span data-ttu-id="51926-371">Consulta de contenedores de blob $logs y tablas de $metrics para cuentas de almacenamiento con las métricas habilitadas.</span><span class="sxs-lookup"><span data-stu-id="51926-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="51926-372">Comportamiento de importación y exportación mejorado. Ahora incluye el tipo de valor de propiedad.</span><span class="sxs-lookup"><span data-stu-id="51926-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-373">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-373">Fixes</span></span>

* <span data-ttu-id="51926-374">Problema corregido: Al cargar o descargar blobs grandes, se puede producir una carga o descarga incompleta.</span><span class="sxs-lookup"><span data-stu-id="51926-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="51926-375">Problema corregido: Al editar, agregar o importar una entidad con un valor de cadena numérico (“1”) se convertirá en doble.</span><span class="sxs-lookup"><span data-stu-id="51926-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it to double</span></span>
* <span data-ttu-id="51926-376">Problema corregido: No se puede expandir el nodo de tabla en el entorno de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="51926-376">Fixed: Unable to expand the table node in the local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-377">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-377">Known Issues</span></span>

* <span data-ttu-id="51926-378">Las tablas de $metrics no son visibles para cuentas de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="51926-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="51926-379">Los mensajes de cola que se agregan mediante programación pueden no mostrarse correctamente si los mensajes se codifican con Base 64.</span><span class="sxs-lookup"><span data-stu-id="51926-379">Queue messages added programmatically may not be displayed correctly if the messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="51926-380">17/05/2016</span><span class="sxs-lookup"><span data-stu-id="51926-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="51926-381">Versión 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="51926-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="51926-382">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-382">New</span></span>

* <span data-ttu-id="51926-383">Mejor control de errores para bloqueos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="51926-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-384">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-384">Fixes</span></span>

* <span data-ttu-id="51926-385">Se ha corregido un error en el que los mensajes de la barra de información a veces no se mostraban cuando se requerían credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="51926-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-386">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-386">Known Issues</span></span>

* <span data-ttu-id="51926-387">Tablas: Al agregar, editar o importar una entidad con una propiedad con un valor numérico ambiguo, como “1” o “1.0” y cuando el usuario intenta enviarla como `Edm.String`, el valor volverá a través de la API del cliente como un Edm.Double.</span><span class="sxs-lookup"><span data-stu-id="51926-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and the user tries to send it as an `Edm.String`, the value will come back through the client API as an Edm.Double</span></span>

<span data-ttu-id="51926-388">31/03/2016</span><span class="sxs-lookup"><span data-stu-id="51926-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="51926-389">Versión 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="51926-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="51926-390">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-390">New</span></span>

* <span data-ttu-id="51926-391">Compatibilidad con tablas: visualización, realización de consultas, exportación, importación y operaciones CRUD para entidades.</span><span class="sxs-lookup"><span data-stu-id="51926-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="51926-392">Compatibilidad con colas: visualización, adición y eliminación de mensajes de la cola.</span><span class="sxs-lookup"><span data-stu-id="51926-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="51926-393">Generación de URI de SAS para cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="51926-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="51926-394">Conexión a cuentas de almacenamiento con URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="51926-394">Connecting to Storage Accounts with SAS URIs</span></span>
* <span data-ttu-id="51926-395">Notificaciones de actualizaciones para actualizaciones futuras a Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="51926-395">Update notifications for future updates to Storage Explorer</span></span>
* <span data-ttu-id="51926-396">Apariencia actualizada.</span><span class="sxs-lookup"><span data-stu-id="51926-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-397">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-397">Fixes</span></span>

* <span data-ttu-id="51926-398">Mejoras de rendimiento y confiabilidad.</span><span class="sxs-lookup"><span data-stu-id="51926-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="51926-399">Problemas conocidos y mitigaciones</span><span class="sxs-lookup"><span data-stu-id="51926-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="51926-400">La descarga de archivos de blob grandes no funciona correctamente. Le recomendamos que use AzCopy mientras no se soluciona este problema.</span><span class="sxs-lookup"><span data-stu-id="51926-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="51926-401">Las credenciales de cuentas no se recuperan ni se almacenan en caché si la carpeta de inicio no se encuentra o no se puede escribir en ella.</span><span class="sxs-lookup"><span data-stu-id="51926-401">Account credentials will not be retrieved nor cached if the home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="51926-402">Al agregar, editar o importar una entidad con una propiedad con un valor numérico ambiguo, como “1” o “1.0” y cuando el usuario intenta enviarla como `Edm.String`, el valor volverá a través de la API del cliente como un Edm.Double.</span><span class="sxs-lookup"><span data-stu-id="51926-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and the user tries to send it as an `Edm.String`, the value will come back through the client API as an Edm.Double</span></span>
* <span data-ttu-id="51926-403">Al importar archivos CSV con registros de varias líneas, es posible que los datos se corten o se desordenen.</span><span class="sxs-lookup"><span data-stu-id="51926-403">When importing CSV files with multiline records, the data may get chopped or scrambled</span></span>

<span data-ttu-id="51926-404">03/02/2016</span><span class="sxs-lookup"><span data-stu-id="51926-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="51926-405">Versión 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="51926-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-406">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-406">Fixes</span></span>

* <span data-ttu-id="51926-407">Rendimiento general mejorado al cargar, descargar y copiar blobs.</span><span class="sxs-lookup"><span data-stu-id="51926-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="51926-408">14/01/2016</span><span class="sxs-lookup"><span data-stu-id="51926-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="51926-409">Versión 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="51926-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="51926-410">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-410">New</span></span>

* <span data-ttu-id="51926-411">Compatibilidad con Linux (características de paridad para OSX)</span><span class="sxs-lookup"><span data-stu-id="51926-411">Linux support (parity features to OSX)</span></span>
* <span data-ttu-id="51926-412">Agregue contenedores de blobs con clave de Firmas de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="51926-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="51926-413">Agregue cuentas de almacenamiento para Azure China.</span><span class="sxs-lookup"><span data-stu-id="51926-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="51926-414">Agregue cuentas de almacenamiento con puntos de conexión personalizados.</span><span class="sxs-lookup"><span data-stu-id="51926-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="51926-415">Abra y vea blobs de imagen y texto de contenido.</span><span class="sxs-lookup"><span data-stu-id="51926-415">Open and view the contents text and picture blobs</span></span>
* <span data-ttu-id="51926-416">Vea y edite propiedades y metadatos de blob.</span><span class="sxs-lookup"><span data-stu-id="51926-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="51926-417">Correcciones</span><span class="sxs-lookup"><span data-stu-id="51926-417">Fixes</span></span>

* <span data-ttu-id="51926-418">Problema corregido: La carga o descarga de un gran número de blobs (más de 500) puede provocar en ocasiones que la aplicación muestre una pantalla en blanco.</span><span class="sxs-lookup"><span data-stu-id="51926-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause the app to have a white screen</span></span> 
* <span data-ttu-id="51926-419">Problema corregido: Al establecer el nivel de acceso público en un contenedor de blobs, el valor nuevo no se actualiza hasta que vuelva a establecer el foco en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="51926-419">Fixed: when setting blob container public access level, the new value is not updated until you re-set the focus on the container.</span></span> <span data-ttu-id="51926-420">Además, el diálogo siempre tiene como valor predeterminado “Sin acceso público” y no el valor real actual.</span><span class="sxs-lookup"><span data-stu-id="51926-420">Also, the dialog always defaults to "No public access", and not the actual current value.</span></span>
* <span data-ttu-id="51926-421">Mejor accesibilidad de teclado general y compatibilidad con IU.</span><span class="sxs-lookup"><span data-stu-id="51926-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="51926-422">El historial de enlaces se ajusta cuando es demasiado largo con espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="51926-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="51926-423">El cuadro de diálogo de SAS admite la validación de entradas.</span><span class="sxs-lookup"><span data-stu-id="51926-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="51926-424">El almacenamiento local sigue estando disponible incluso aunque las credenciales de usuario hayan expirado.</span><span class="sxs-lookup"><span data-stu-id="51926-424">Local storage continues to be available even if user credentials have expired</span></span>
* <span data-ttu-id="51926-425">Cuando se elimina un contenedor de blobs abierto, el explorador de blobs de la derecha se cierra.</span><span class="sxs-lookup"><span data-stu-id="51926-425">When an opened blob container is deleted, the blob explorer on the right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-426">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-426">Known Issues</span></span>

* <span data-ttu-id="51926-427">La instalación de Linux requiere que se actualice la versión de gcc. A continuación puede ver los pasos para actualizarla:</span><span class="sxs-lookup"><span data-stu-id="51926-427">Linux install needs gcc version updated or upgraded – steps to upgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="51926-428">18/11/2015</span><span class="sxs-lookup"><span data-stu-id="51926-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="51926-429">Versión 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="51926-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="51926-430">Nuevo</span><span class="sxs-lookup"><span data-stu-id="51926-430">New</span></span>

* <span data-ttu-id="51926-431">Versiones de Windows y macOS.</span><span class="sxs-lookup"><span data-stu-id="51926-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="51926-432">Inicie sesión para ver las cuentas de almacenamiento: use su cuenta de organización, cuenta Microsoft, 2FA, etc.</span><span class="sxs-lookup"><span data-stu-id="51926-432">Sign in to view your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="51926-433">Almacenamiento de desarrollo local (use un emulador de almacenamiento, solo para Windows).</span><span class="sxs-lookup"><span data-stu-id="51926-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="51926-434">Compatibilidad de Azure Resource Manager y recursos clásicos.</span><span class="sxs-lookup"><span data-stu-id="51926-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="51926-435">Cree y elimine blobs, colas o tablas.</span><span class="sxs-lookup"><span data-stu-id="51926-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="51926-436">Busque blobs, colas o tablas específicos.</span><span class="sxs-lookup"><span data-stu-id="51926-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="51926-437">Explore el contenido de los contenedores de blobs.</span><span class="sxs-lookup"><span data-stu-id="51926-437">Explore the contents of blob containers</span></span>
* <span data-ttu-id="51926-438">Vea y navegue por directorios.</span><span class="sxs-lookup"><span data-stu-id="51926-438">View and navigate through directories</span></span>
* <span data-ttu-id="51926-439">Cargue, descargue y elimine blobs y carpetas.</span><span class="sxs-lookup"><span data-stu-id="51926-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="51926-440">Vea y edite propiedades y metadatos de blob.</span><span class="sxs-lookup"><span data-stu-id="51926-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="51926-441">Genere claves SAS.</span><span class="sxs-lookup"><span data-stu-id="51926-441">Generate SAS keys</span></span>
* <span data-ttu-id="51926-442">Administre y cree directivas de acceso a almacenamiento (SAP).</span><span class="sxs-lookup"><span data-stu-id="51926-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="51926-443">Busque blobs por prefijo.</span><span class="sxs-lookup"><span data-stu-id="51926-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="51926-444">Arrastre y coloque archivos para cargarlos o descargarlos.</span><span class="sxs-lookup"><span data-stu-id="51926-444">Drag 'n drop files to upload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="51926-445">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="51926-445">Known Issues</span></span>

* <span data-ttu-id="51926-446">Al establecer el nivel de acceso público en un contenedor de blobs, el valor nuevo no se actualiza hasta que vuelva a establecer el foco en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="51926-446">When setting blob container public access level, the new value is not updated until you re-set the focus on the container</span></span>
* <span data-ttu-id="51926-447">Al abrir el cuadro de diálogo para establecer el nivel de acceso público, siempre se muestra “Sin acceso público” como valor predeterminado y no el valor real actual.</span><span class="sxs-lookup"><span data-stu-id="51926-447">When you open the dialog to set the public access level, it always shows "No public access" as the default, and not the actual current value</span></span>
* <span data-ttu-id="51926-448">No se puede cambiar el nombre de los blobs descargados.</span><span class="sxs-lookup"><span data-stu-id="51926-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="51926-449">Las entradas del registro de actividades a veces se bloquean en un estado de progreso cuando se produce un error y el error no se muestra.</span><span class="sxs-lookup"><span data-stu-id="51926-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and the error is not displayed</span></span>
* <span data-ttu-id="51926-450">A veces se bloquea o se pone en blanco al intentar cargar o descargar un gran número de blobs.</span><span class="sxs-lookup"><span data-stu-id="51926-450">Sometimes crashes or turns completely white when trying to upload or download a large number of blobs</span></span>
* <span data-ttu-id="51926-451">A veces no se puede cancelar una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="51926-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="51926-452">Durante la creación de un contenedor (blob, cola o tabla), si indica un nombre no válido y continúa creando otro en otro tipo de contenedor, no podrá establecer el foco en el tipo nuevo.</span><span class="sxs-lookup"><span data-stu-id="51926-452">During creating a container (blob/queue/table), if you input an invalid name and proceed to create another under a different container type you cannot set focus on the new type</span></span>
* <span data-ttu-id="51926-453">No se puede crear una carpeta nueva ni cambiarle el nombre.</span><span class="sxs-lookup"><span data-stu-id="51926-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md