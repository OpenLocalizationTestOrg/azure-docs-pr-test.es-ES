---
title: "notas de la versión de aaaMicrosoft Explorador de almacenamiento de Azure (versión preliminar) | Documentos de Microsoft"
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
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="36c1c-103">Notas de la versión de Explorador de Microsoft Azure Storage (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="36c1c-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="36c1c-104">Este artículo contiene la versión de Hola notas para Azure Storage Explorer 0.8.16 (vista previa) de la versión, así como notas de la versión para las versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="36c1c-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="36c1c-105">[Explorador de almacenamiento de Microsoft Azure (vista previa)](./vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente que permite trabajar tooeasily con los datos de almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="36c1c-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="36c1c-106">Versión 0.8.16 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="36c1c-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="36c1c-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="36c1c-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="36c1c-108">Descarga del Explorador de Azure Storage 0.8.16 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="36c1c-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="36c1c-109">Explorador de Azure Storage 0.8.16 (versión preliminar) para Windows</span><span class="sxs-lookup"><span data-stu-id="36c1c-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="36c1c-110">Explorador de Azure Storage 0.8.16 (versión preliminar) para Mac</span><span class="sxs-lookup"><span data-stu-id="36c1c-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="36c1c-111">Explorador de Azure Storage 0.8.16 (versión preliminar) para Linux</span><span class="sxs-lookup"><span data-stu-id="36c1c-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="36c1c-112">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-112">New</span></span>
* <span data-ttu-id="36c1c-113">Al abrir un blob, el Explorador de almacenamiento le solicitará que tooupload Hola Descargar archivo si se detecta un cambio</span><span class="sxs-lookup"><span data-stu-id="36c1c-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="36c1c-114">Experiencia mejorada de inicio de sesión de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="36c1c-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="36c1c-115">Rendimiento mejorado Hola de carga/descarga de muchos pequeños archivos de hello mismo tiempo</span><span class="sxs-lookup"><span data-stu-id="36c1c-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="36c1c-116">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-116">Fixes</span></span>
* <span data-ttu-id="36c1c-117">En algunos tipos de blob, elegir "reemplazar" demasiado durante un conflicto de carga a veces produciría carga Hola se reinicia.</span><span class="sxs-lookup"><span data-stu-id="36c1c-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="36c1c-118">En la versión 0.8.15, las cargas se detendrían a veces en un 99 %.</span><span class="sxs-lookup"><span data-stu-id="36c1c-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="36c1c-119">Al cargar el recurso compartido de archivos de tooa de archivos, si ha elegido el directorio de tooa tooupload que aún no existe, se producirá un error en la carga.</span><span class="sxs-lookup"><span data-stu-id="36c1c-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="36c1c-120">El Explorador de Storage estaba generando marcas de tiempo de forma incorrecta para las firmas de acceso compartido y las consultas de tabla.</span><span class="sxs-lookup"><span data-stu-id="36c1c-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="36c1c-121">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-121">Known Issues</span></span>
* <span data-ttu-id="36c1c-122">El uso de un nombre y una cadena de conexión de clave no funciona actualmente.</span><span class="sxs-lookup"><span data-stu-id="36c1c-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="36c1c-123">Se corregirá en la siguiente versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c1c-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="36c1c-124">Hasta ese momento, puede usar la asociación con el nombre y la clave.</span><span class="sxs-lookup"><span data-stu-id="36c1c-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="36c1c-125">Si intentas tooopen un archivo con un nombre de archivo no válido de Windows, descarga de Hola dará como resultado un archivo de error no encontrado.</span><span class="sxs-lookup"><span data-stu-id="36c1c-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="36c1c-126">Después de hacer clic en "Cancelar" en una tarea, puede tardar unos instantes para que toocancel de tarea.</span><span class="sxs-lookup"><span data-stu-id="36c1c-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="36c1c-127">Se trata de una limitación de la biblioteca de nodo de almacenamiento de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="36c1c-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="36c1c-128">Después de completar una carga de blobs, se actualiza la pestaña de Hola que inició la carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c1c-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="36c1c-129">Esto es un cambio de comportamiento anterior y también hará que toobe dirigirá toohello raíz se encuentra en el contenedor de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="36c1c-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="36c1c-130">Si elige Hola incorrecto PIN/certificado de tarjeta inteligente, a continuación, deberá toorestart en orden toohave Explorador de almacenamiento olvida esa decisión.</span><span class="sxs-lookup"><span data-stu-id="36c1c-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="36c1c-131">puede mostrar el panel de configuración de cuenta de Hello que necesita credenciales toofilter suscripciones a tooreenter.</span><span class="sxs-lookup"><span data-stu-id="36c1c-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="36c1c-132">Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="36c1c-133">Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.</span><span class="sxs-lookup"><span data-stu-id="36c1c-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="36c1c-134">Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada.</span><span class="sxs-lookup"><span data-stu-id="36c1c-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="36c1c-135">Para los usuarios de Ubuntu 14.04, necesitará tooensure GCC está activo toodate: Esto puede hacerse mediante la ejecución de hello sigue comandos y, a continuación, reiniciar el equipo:</span><span class="sxs-lookup"><span data-stu-id="36c1c-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="36c1c-136">Para los usuarios de Ubuntu 17.04, necesitará tooinstall GConf: Esto puede hacerse ejecutando Hola sigue comandos y, a continuación, reiniciar el equipo:</span><span class="sxs-lookup"><span data-stu-id="36c1c-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="36c1c-137">Versión 0.8.14 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="36c1c-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="36c1c-138">22/06/2017</span><span class="sxs-lookup"><span data-stu-id="36c1c-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="36c1c-139">Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="36c1c-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="36c1c-140">Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar) para Windows</span><span class="sxs-lookup"><span data-stu-id="36c1c-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="36c1c-141">Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar) para Mac</span><span class="sxs-lookup"><span data-stu-id="36c1c-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="36c1c-142">Descarga del Explorador de Azure Storage 0.8.14 (versión preliminar) para Linux</span><span class="sxs-lookup"><span data-stu-id="36c1c-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="36c1c-143">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-143">New</span></span>

* <span data-ttu-id="36c1c-144">Too1.7.2 de versión actualizada de electrones en orden tootake aprovechar las varias actualizaciones de seguridad críticas</span><span class="sxs-lookup"><span data-stu-id="36c1c-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="36c1c-145">Se puede ahora acceder rápidamente a la Guía de solución de problemas en pantalla de Hola desde el menú de Ayuda de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="36c1c-146">[Guía][2] de solución de problemas del Explorador de Storage</span><span class="sxs-lookup"><span data-stu-id="36c1c-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="36c1c-147">[Instrucciones] [ 3] sobre la conexión de suscripción de Azure pila tooan</span><span class="sxs-lookup"><span data-stu-id="36c1c-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="36c1c-148">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-148">Known Issues</span></span>

* <span data-ttu-id="36c1c-149">Botones del cuadro de diálogo de confirmación de carpeta de hello delete no se registran con clics del mouse de hello en Linux.</span><span class="sxs-lookup"><span data-stu-id="36c1c-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="36c1c-150">Solución alternativa es la tecla ENTRAR de toouse Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="36c1c-151">Si elige Hola incorrecto PIN/certificado de tarjeta inteligente, deberá toorestart en orden toohave Explorador de almacenamiento olvida decisión Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="36c1c-152">Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores de</span><span class="sxs-lookup"><span data-stu-id="36c1c-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="36c1c-153">panel de configuración de cuenta de Hello puede mostrar que se necesitan credenciales de tooreenter en las suscripciones de toofilter de orden</span><span class="sxs-lookup"><span data-stu-id="36c1c-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="36c1c-154">Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="36c1c-155">Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.</span><span class="sxs-lookup"><span data-stu-id="36c1c-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="36c1c-156">Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada.</span><span class="sxs-lookup"><span data-stu-id="36c1c-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="36c1c-157">Ubuntu 14.04 instalación necesidades gcc versión había actualizado o ampliado – tooupgrade pasos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="36c1c-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="36c1c-158">Versiones anteriores</span><span class="sxs-lookup"><span data-stu-id="36c1c-158">Previous releases</span></span>

* [<span data-ttu-id="36c1c-159">Versión 0.8.13</span><span class="sxs-lookup"><span data-stu-id="36c1c-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="36c1c-160">Versión 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="36c1c-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="36c1c-161">Versión 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="36c1c-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="36c1c-162">Versión 0.8.7</span><span class="sxs-lookup"><span data-stu-id="36c1c-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="36c1c-163">Versión 0.8.6</span><span class="sxs-lookup"><span data-stu-id="36c1c-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="36c1c-164">Versión 0.8.5</span><span class="sxs-lookup"><span data-stu-id="36c1c-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="36c1c-165">Versión 0.8.4</span><span class="sxs-lookup"><span data-stu-id="36c1c-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="36c1c-166">Versión 0.8.3</span><span class="sxs-lookup"><span data-stu-id="36c1c-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="36c1c-167">Versión 0.8.2</span><span class="sxs-lookup"><span data-stu-id="36c1c-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="36c1c-168">Versión 0.8.0</span><span class="sxs-lookup"><span data-stu-id="36c1c-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="36c1c-169">Versión 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="36c1c-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="36c1c-170">Versión 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="36c1c-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="36c1c-171">Versión 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="36c1c-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="36c1c-172">Versión 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="36c1c-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="36c1c-173">Versión 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="36c1c-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="36c1c-174">Versión 0.8.13</span><span class="sxs-lookup"><span data-stu-id="36c1c-174">Version 0.8.13</span></span>
<span data-ttu-id="36c1c-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="36c1c-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="36c1c-176">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-176">New</span></span>

* <span data-ttu-id="36c1c-177">[Guía][2] de solución de problemas del Explorador de Storage</span><span class="sxs-lookup"><span data-stu-id="36c1c-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="36c1c-178">[Instrucciones] [ 3] sobre la conexión de suscripción de Azure pila tooan</span><span class="sxs-lookup"><span data-stu-id="36c1c-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-179">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-179">Fixes</span></span>

* <span data-ttu-id="36c1c-180">Problema corregido: Había una alta probabilidad de que, al cargar un archivo, se produjese un error de memoria agotada.</span><span class="sxs-lookup"><span data-stu-id="36c1c-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="36c1c-181">Problema corregido: Ahora puede iniciar sesión con una tarjeta inteligente o un PIN.</span><span class="sxs-lookup"><span data-stu-id="36c1c-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="36c1c-182">Problema corregido: Abrir en Portal ahora funciona con Azure China, Azure Germany, Azure US Government y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="36c1c-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="36c1c-183">Problema corregido: Al cargar un contenedor de blobs de tooa de carpeta, "Operación no válida" produciría un error a veces</span><span class="sxs-lookup"><span data-stu-id="36c1c-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="36c1c-184">Problema corregido: Seleccionar todo se deshabilita durante la administración de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="36c1c-185">Problema corregido: Hola metadatos del blob base Hola podrían se sobrescriban después de ver las propiedades de Hola de sus instantáneas</span><span class="sxs-lookup"><span data-stu-id="36c1c-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-186">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-186">Known Issues</span></span>

* <span data-ttu-id="36c1c-187">Si elige Hola incorrecto PIN/certificado de tarjeta inteligente, deberá toorestart en orden toohave Explorador de almacenamiento olvida decisión Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="36c1c-188">Mientras ampliada o alejar, nivel de zoom de hello momentáneamente puede restablecer nivel predeterminado de toohello</span><span class="sxs-lookup"><span data-stu-id="36c1c-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="36c1c-189">Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores de</span><span class="sxs-lookup"><span data-stu-id="36c1c-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="36c1c-190">panel de configuración de cuenta de Hello puede mostrar que se necesitan credenciales de tooreenter en las suscripciones de toofilter de orden</span><span class="sxs-lookup"><span data-stu-id="36c1c-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="36c1c-191">Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="36c1c-192">Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.</span><span class="sxs-lookup"><span data-stu-id="36c1c-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="36c1c-193">Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada.</span><span class="sxs-lookup"><span data-stu-id="36c1c-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="36c1c-194">Ubuntu 14.04 instalación necesidades gcc versión había actualizado o ampliado – tooupgrade pasos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="36c1c-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="36c1c-195">Versión 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="36c1c-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="36c1c-196">07/04/2017</span><span class="sxs-lookup"><span data-stu-id="36c1c-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="36c1c-197">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-197">New</span></span>

* <span data-ttu-id="36c1c-198">Explorador de almacenamiento ahora se cerrará automáticamente cuando se instala una actualización de notificación de actualización de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="36c1c-199">El acceso rápido local proporciona una experiencia mejorada a la hora de trabajar con los recursos a los que accede con más frecuencia.</span><span class="sxs-lookup"><span data-stu-id="36c1c-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="36c1c-200">En el editor de contenedor de blobs de hello, ahora puede ver qué máquina virtual al que pertenece un blob en concesión</span><span class="sxs-lookup"><span data-stu-id="36c1c-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="36c1c-201">Ahora se puede contraer el panel del lado izquierdo de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="36c1c-202">Detección ahora se ejecuta en hello mismo tiempo como descarga</span><span class="sxs-lookup"><span data-stu-id="36c1c-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="36c1c-203">Usar las estadísticas en hello contenedor de blobs, recurso compartido de archivos y tabla editores toosee Hola el tamaño de los recursos o la selección</span><span class="sxs-lookup"><span data-stu-id="36c1c-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="36c1c-204">Ahora puede tooAzure inicio de sesión en Active Directory (AAD) según las cuentas de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="36c1c-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="36c1c-205">Ahora el archivo de carga de archivos de cuentas de almacenamiento de más de 32 MB tooPremium puede</span><span class="sxs-lookup"><span data-stu-id="36c1c-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="36c1c-206">Compatibilidad de accesibilidad mejorada.</span><span class="sxs-lookup"><span data-stu-id="36c1c-206">Improved accessibility support</span></span>
* <span data-ttu-id="36c1c-207">Ahora puede agregar confianza Base64 codificado certificados X.509 SSL por va tooEdit -&gt; certificados de SSL:&gt; importar certificados</span><span class="sxs-lookup"><span data-stu-id="36c1c-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-208">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-208">Fixes</span></span>

* <span data-ttu-id="36c1c-209">Problema corregido: después de actualizar las credenciales de una cuenta, vista de árbol de hello haría a veces no actualizar automáticamente</span><span class="sxs-lookup"><span data-stu-id="36c1c-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="36c1c-210">Problema corregido: Al generar un SAS para tablas y colas de emulador, se producía una URL no válida.</span><span class="sxs-lookup"><span data-stu-id="36c1c-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="36c1c-211">Problema corregido: Las cuentas de almacenamiento premium ahora se pueden ampliar mientras haya un proxy habilitado.</span><span class="sxs-lookup"><span data-stu-id="36c1c-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="36c1c-212">Se ha corregido: Hola botón Aplicar en las cuentas de hello página de administración no funcionaría si hubiera 1 ó 0 cuentas seleccionadas</span><span class="sxs-lookup"><span data-stu-id="36c1c-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="36c1c-213">Problema corregido: Se puede producir un error al cargar blobs que requieran resoluciones de conflictos. Esto se ha corregido en la versión 0.8.11.</span><span class="sxs-lookup"><span data-stu-id="36c1c-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="36c1c-214">Problema corregido: No se podían enviar comentarios en la versión 0.8.11. Corregido en la versión 0.8.12.</span><span class="sxs-lookup"><span data-stu-id="36c1c-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="36c1c-215">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-215">Known Issues</span></span>

* <span data-ttu-id="36c1c-216">Después de actualizar too0.8.10, necesitará toorefresh todos sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="36c1c-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="36c1c-217">Mientras ampliada o alejar, nivel de zoom de hello momentáneamente puede restablecer nivel predeterminado de toohello.</span><span class="sxs-lookup"><span data-stu-id="36c1c-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="36c1c-218">Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores.</span><span class="sxs-lookup"><span data-stu-id="36c1c-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="36c1c-219">panel de configuración de cuenta de Hello puede mostrar que se necesitan credenciales de tooreenter en las suscripciones de toofilter de orden.</span><span class="sxs-lookup"><span data-stu-id="36c1c-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="36c1c-220">Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="36c1c-221">Todas las demás propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.</span><span class="sxs-lookup"><span data-stu-id="36c1c-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="36c1c-222">Aunque Azure Stack actualmente no admite recursos compartidos de archivos, todavía aparece un nodo de recurso compartido de archivos en la cuenta de almacenamiento de Azure Stack conectada.</span><span class="sxs-lookup"><span data-stu-id="36c1c-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="36c1c-223">Ubuntu 14.04 instalación necesidades gcc versión había actualizado o ampliado – tooupgrade pasos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="36c1c-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="36c1c-224">Versión 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="36c1c-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="36c1c-225">23/02/2017</span><span class="sxs-lookup"><span data-stu-id="36c1c-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="36c1c-226">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-226">New</span></span>

* <span data-ttu-id="36c1c-227">0.8.9 del explorador de almacenamiento descargará automáticamente la versión más reciente de Hola para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="36c1c-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="36c1c-228">Revisión: mediante el portal genera tooattach de URI de SAS que una cuenta de almacenamiento produciría un error.</span><span class="sxs-lookup"><span data-stu-id="36c1c-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="36c1c-229">Ahora puede crear, administrar y promover instantáneas de blobs.</span><span class="sxs-lookup"><span data-stu-id="36c1c-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="36c1c-230">Ahora puede iniciar sesión en cuentas tooAzure de China, Azure en Alemania y gobierno de EE.</span><span class="sxs-lookup"><span data-stu-id="36c1c-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="36c1c-231">Ahora puede cambiar el nivel de zoom de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c1c-231">You can now change hello zoom level.</span></span> <span data-ttu-id="36c1c-232">Utilizar opciones de Hola Hola vista menú tooZoom en Alejar y restablecer Zoom.</span><span class="sxs-lookup"><span data-stu-id="36c1c-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="36c1c-233">Ahora se admiten caracteres Unicode en los metadatos de usuarios para blobs y archivos.</span><span class="sxs-lookup"><span data-stu-id="36c1c-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="36c1c-234">Mejoras de accesibilidad.</span><span class="sxs-lookup"><span data-stu-id="36c1c-234">Accessibility improvements.</span></span>
* <span data-ttu-id="36c1c-235">notas de la versión de la versión siguiente de Hello pueden verse de notificación de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c1c-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="36c1c-236">También puede ver Hola actual notas de la versión desde el menú de Ayuda de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c1c-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-237">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-237">Fixes</span></span>

* <span data-ttu-id="36c1c-238">Problema corregido: número de versión de Hola correctamente aparece ahora en el Panel de Control en Windows</span><span class="sxs-lookup"><span data-stu-id="36c1c-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="36c1c-239">Problema corregido: búsqueda ya no es too50 limitado, 000 nodos</span><span class="sxs-lookup"><span data-stu-id="36c1c-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="36c1c-240">Problema corregido: recurso compartido de archivos de tooa de carga creadas para siempre si el directorio de destino de hello no existía todavía</span><span class="sxs-lookup"><span data-stu-id="36c1c-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="36c1c-241">Problema corregido: Estabilidad mejorada para cargas y descargas largas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-242">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-242">Known Issues</span></span>

* <span data-ttu-id="36c1c-243">Mientras ampliada o alejar, nivel de zoom de hello momentáneamente puede restablecer nivel predeterminado de toohello.</span><span class="sxs-lookup"><span data-stu-id="36c1c-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="36c1c-244">Acceso rápido solo funciona con elementos basados en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="36c1c-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="36c1c-245">En esta versión no se admiten recursos locales o recursos adjuntados a través de la clave o token de SAS.</span><span class="sxs-lookup"><span data-stu-id="36c1c-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="36c1c-246">Puede tardar unos segundos toonavigate toohello recurso de destino, según la cantidad de recursos que tiene un acceso rápido.</span><span class="sxs-lookup"><span data-stu-id="36c1c-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="36c1c-247">Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores.</span><span class="sxs-lookup"><span data-stu-id="36c1c-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="36c1c-248">16/12/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="36c1c-249">Versión 0.8.7</span><span class="sxs-lookup"><span data-stu-id="36c1c-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="36c1c-250">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-250">New</span></span>

* <span data-ttu-id="36c1c-251">Puede elegir cómo tooresolve conflictos al principio de Hola de una actualización, descargar o copiar la sesión en la ventana de actividades de hello</span><span class="sxs-lookup"><span data-stu-id="36c1c-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="36c1c-252">Mantenga el mouse sobre una ficha toosee Hola ruta de acceso completa del recurso de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="36c1c-253">Al hacer clic en una pestaña, se sincroniza con su ubicación en el panel de navegación del lado izquierdo de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-254">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-254">Fixes</span></span>

* <span data-ttu-id="36c1c-255">Problema corregido: El Explorador de Storage es ahora una aplicación de confianza en Mac.</span><span class="sxs-lookup"><span data-stu-id="36c1c-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="36c1c-256">Problema corregido: Ubuntu 14.04 se admite de nuevo.</span><span class="sxs-lookup"><span data-stu-id="36c1c-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="36c1c-257">Problema corregido: A veces Hola Agregar cuenta UI parpadea al cargar las suscripciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="36c1c-258">Problema corregido: En ocasiones, no todos los recursos de almacenamiento figuraban en el panel de navegación del lado izquierdo de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="36c1c-259">Problema corregido: panel de acciones de Hola a veces muestra acciones vacías</span><span class="sxs-lookup"><span data-stu-id="36c1c-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="36c1c-260">Fijo: ahora se conserva tamaño de la ventana de Hola de sesión de hello cerró por última vez</span><span class="sxs-lookup"><span data-stu-id="36c1c-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="36c1c-261">Se ha corregido: Se pueden abrir varias pestañas para hello mismo recurso mediante el menú contextual de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-262">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-262">Known Issues</span></span>

* <span data-ttu-id="36c1c-263">Acceso rápido solo funciona con elementos basados en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="36c1c-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="36c1c-264">En esta versión no se admiten recursos locales o recursos adjuntados a través de la clave o token de SAS.</span><span class="sxs-lookup"><span data-stu-id="36c1c-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="36c1c-265">Puede tardar unos segundos toonavigate toohello recurso de destino, dependiendo de cuántos recursos tendrá acceso rápido</span><span class="sxs-lookup"><span data-stu-id="36c1c-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="36c1c-266">Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores de</span><span class="sxs-lookup"><span data-stu-id="36c1c-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="36c1c-267">Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado o se pueden producir excepciones no controladas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="36c1c-268">Para hello primera vez con hello Explorador de almacenamiento en macOS, puede que vea varios mensajes piden llaveros de tooaccess de permiso del usuario.</span><span class="sxs-lookup"><span data-stu-id="36c1c-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="36c1c-269">Se recomienda que seleccione Permitir siempre por lo que el mensaje Hola no vuelva a mostrarse</span><span class="sxs-lookup"><span data-stu-id="36c1c-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="36c1c-270">18/11/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="36c1c-271">Versión 0.8.6</span><span class="sxs-lookup"><span data-stu-id="36c1c-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="36c1c-272">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-272">New</span></span>

* <span data-ttu-id="36c1c-273">Puede ahora pin usa con mayor frecuencia servicios toohello acceso rápido para facilitar la navegación</span><span class="sxs-lookup"><span data-stu-id="36c1c-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="36c1c-274">Ya puede abrir varios editores en diferentes pestañas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="36c1c-275">Un solo clic tooopen una pestaña temporal; Haga doble clic en tooopen una pestaña permanente. También puede hacer clic en hello pestaña temporal toomake, una pestaña permanente</span><span class="sxs-lookup"><span data-stu-id="36c1c-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="36c1c-276">Hemos realizado mejoras notables de rendimiento y estabilidad para cargas y descargas, especialmente para archivos de gran tamaño en máquinas rápidas</span><span class="sxs-lookup"><span data-stu-id="36c1c-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="36c1c-277">Las carpetas vacías "virtuales" ya se pueden crear en contenedores de blobs.</span><span class="sxs-lookup"><span data-stu-id="36c1c-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="36c1c-278">Hemos vuelto a incorporar la búsqueda en ámbito con la nueva y mejorada búsqueda de subcadenas, por lo que ahora tiene dos opciones para realizar búsquedas:</span><span class="sxs-lookup"><span data-stu-id="36c1c-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="36c1c-279">Global búsqueda - tan sólo debe escribir un término de búsqueda en el cuadro de texto de búsqueda de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="36c1c-280">Búsqueda de ámbito - haga clic en hello lupa icono siguiente tooa nodo, a continuación, agregar un extremo de toohello del término de búsqueda de ruta de acceso de hello, o haga clic en y seleccione "Búsqueda desde aquí"</span><span class="sxs-lookup"><span data-stu-id="36c1c-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="36c1c-281">Hemos agregado varios temas: claro (valor predeterminado), oscuro, negro en alto contraste y blanco en alto contraste.</span><span class="sxs-lookup"><span data-stu-id="36c1c-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="36c1c-282">Vaya tooEdit -&gt; toochange temas sus preferencias de temas</span><span class="sxs-lookup"><span data-stu-id="36c1c-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="36c1c-283">Puede modificar las propiedades de blobs y archivos.</span><span class="sxs-lookup"><span data-stu-id="36c1c-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="36c1c-284">Ahora se admiten mensajes de cola cifrados (Base64) y sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="36c1c-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="36c1c-285">En Linux, ahora es necesario usar un sistema operativo de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="36c1c-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="36c1c-286">En esta versión solo se admite Ubuntu 16.04.1 LTS de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="36c1c-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="36c1c-287">¡Hemos actualizado nuestro logotipo!</span><span class="sxs-lookup"><span data-stu-id="36c1c-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-288">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-288">Fixes</span></span>

* <span data-ttu-id="36c1c-289">Problema corregido: Problemas de inmovilización de pantalla</span><span class="sxs-lookup"><span data-stu-id="36c1c-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="36c1c-290">Problema corregido: Mayor seguridad</span><span class="sxs-lookup"><span data-stu-id="36c1c-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="36c1c-291">Problema corregido: A veces, podrían aparecer cuentas conectadas duplicadas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="36c1c-292">Problema corregido: Un blob con un tipo de contenido sin definir podría generar una excepción.</span><span class="sxs-lookup"><span data-stu-id="36c1c-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="36c1c-293">Problema corregido: Hola de abrir el Panel de consulta en una tabla vacía no era posible</span><span class="sxs-lookup"><span data-stu-id="36c1c-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="36c1c-294">Problema corregido: Varios errores en la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="36c1c-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="36c1c-295">Fijo: Mayor número de Hola de recursos cargados desde too100 50 al hacer clic en "Más carga"</span><span class="sxs-lookup"><span data-stu-id="36c1c-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="36c1c-296">Problema corregido: En la primera ejecución, si ha iniciado sesión con una cuenta, ahora se seleccionan todas las suscripciones para esa cuenta de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="36c1c-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="36c1c-297">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-297">Known Issues</span></span>

* <span data-ttu-id="36c1c-298">Esta versión de Hola Explorador de almacenamiento no se ejecuta en Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="36c1c-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="36c1c-299">tooopen varias pestañas para hello mismo recurso, realice continuamente no haga clic en Hola mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="36c1c-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="36c1c-300">Haga clic en otro recurso y, a continuación, volver atrás y, a continuación, vuelva a hacer clic en hello original recursos tooopen en otra ficha</span><span class="sxs-lookup"><span data-stu-id="36c1c-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="36c1c-301">Acceso rápido solo funciona con elementos basados en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="36c1c-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="36c1c-302">En esta versión no se admiten recursos locales o recursos adjuntados a través de la clave o token de SAS.</span><span class="sxs-lookup"><span data-stu-id="36c1c-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="36c1c-303">Puede tardar unos segundos toonavigate toohello recurso de destino, dependiendo de cuántos recursos tendrá acceso rápido</span><span class="sxs-lookup"><span data-stu-id="36c1c-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="36c1c-304">Tener más de 3 grupos de blobs o archivos cargar en hello mismo tiempo puede provocar errores de</span><span class="sxs-lookup"><span data-stu-id="36c1c-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="36c1c-305">Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado o se pueden producir excepciones no controladas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="36c1c-306">03/10/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="36c1c-307">Versión 0.8.5</span><span class="sxs-lookup"><span data-stu-id="36c1c-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="36c1c-308">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-308">New</span></span>

* <span data-ttu-id="36c1c-309">Puede ahora tooattach tooStorage de claves de uso SAS generado por el Portal de cuentas y recursos</span><span class="sxs-lookup"><span data-stu-id="36c1c-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-310">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-310">Fixes</span></span>

* <span data-ttu-id="36c1c-311">Corregido: condición de carrera durante la búsqueda a veces debe toobecome de nodos no se pueden expandir</span><span class="sxs-lookup"><span data-stu-id="36c1c-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="36c1c-312">Problema corregido: "Usar HTTP" no funciona cuando se conecta tooStorage cuentas con clave y el nombre de cuenta</span><span class="sxs-lookup"><span data-stu-id="36c1c-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="36c1c-313">Problema corregido: Las claves SAS (especialmente las generadas en el Portal) devuelven un error de “barra oblicua final”.</span><span class="sxs-lookup"><span data-stu-id="36c1c-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="36c1c-314">Problema corregido: Problemas al importar tablas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="36c1c-315">A veces se revertían la clave de fila y la clave de partición</span><span class="sxs-lookup"><span data-stu-id="36c1c-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="36c1c-316">No se puede tooread "null" claves de partición</span><span class="sxs-lookup"><span data-stu-id="36c1c-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-317">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-317">Known Issues</span></span>

* <span data-ttu-id="36c1c-318">Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado.</span><span class="sxs-lookup"><span data-stu-id="36c1c-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="36c1c-319">Pila de Azure no admite actualmente los archivos, para intentar tooexpand archivos mostrará un error</span><span class="sxs-lookup"><span data-stu-id="36c1c-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="36c1c-320">12/09/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="36c1c-321">Versión 0.8.4</span><span class="sxs-lookup"><span data-stu-id="36c1c-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="36c1c-322">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-322">New</span></span>

* <span data-ttu-id="36c1c-323">Generar cuentas toostorage de vínculos directos, contenedores, las colas, las tablas o recursos compartidos de archivos para compartir y fácil de obtener acceso a recursos de tooyour - Windows y Mac OS admiten</span><span class="sxs-lookup"><span data-stu-id="36c1c-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="36c1c-324">Busque los contenedores de blobs, tablas, colas, recursos compartidos de archivos o las cuentas de almacenamiento desde el cuadro de búsqueda de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="36c1c-325">Ahora puede agrupar las cláusulas en Generador de consultas de tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="36c1c-326">Cambie el nombre y copie y pegue contenedores de blobs, recursos compartidos de archivos, tablas, blobs, carpetas de blobs, archivos y directorios desde cuentas conectadas mediante SAS y contenedores.</span><span class="sxs-lookup"><span data-stu-id="36c1c-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="36c1c-327">Al cambiar el nombre y copiar contenedores de blobs y recursos compartidos de archivos, ahora se conservan las propiedades y los metadatos.</span><span class="sxs-lookup"><span data-stu-id="36c1c-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-328">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-328">Fixes</span></span>

* <span data-ttu-id="36c1c-329">Problema corregido: No se pueden editar las entidades de tablas si contienen propiedades binarias o booleanas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-330">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-330">Known Issues</span></span>

* <span data-ttu-id="36c1c-331">Identificadores de búsqueda que buscan en unos 50.000 nodos: después de esto, el rendimiento puede verse afectado.</span><span class="sxs-lookup"><span data-stu-id="36c1c-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="36c1c-332">03/08/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="36c1c-333">Versión 0.8.3</span><span class="sxs-lookup"><span data-stu-id="36c1c-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="36c1c-334">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-334">New</span></span>

* <span data-ttu-id="36c1c-335">Cambie el nombre de contenedores, tablas y recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="36c1c-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="36c1c-336">Experiencia mejorada con el generador de consultas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-336">Improved Query builder experience</span></span>
* <span data-ttu-id="36c1c-337">Consultas de toosave y carga de capacidad</span><span class="sxs-lookup"><span data-stu-id="36c1c-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="36c1c-338">Dirigir toostorage cuentas o contenedores, las colas, tablas de vínculos o recursos compartidos para compartir y acceder fácilmente a los recursos de archivos (sólo Windows - macOS admiten próximamente!)</span><span class="sxs-lookup"><span data-stu-id="36c1c-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="36c1c-339">Capacidad toomanage y configurar las reglas de CORS</span><span class="sxs-lookup"><span data-stu-id="36c1c-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-340">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-340">Fixes</span></span>

* <span data-ttu-id="36c1c-341">Problema corregido: Las cuentas de Microsoft requieren que vuelva a autenticarse en períodos de 8 a 12 horas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-342">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-342">Known Issues</span></span>

* <span data-ttu-id="36c1c-343">A veces hello interfaz de usuario podría parezca detenida: lo que maximiza la ventana hello ayuda a resolver este problema</span><span class="sxs-lookup"><span data-stu-id="36c1c-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="36c1c-344">Puede que la instalación en macOS requiera permisos elevados.</span><span class="sxs-lookup"><span data-stu-id="36c1c-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="36c1c-345">Puede mostrar el panel de configuración de la cuenta que se necesitan credenciales de tooreenter en las suscripciones de toofilter de orden</span><span class="sxs-lookup"><span data-stu-id="36c1c-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="36c1c-346">Cambio de nombre de recursos compartidos de archivos, contenedores de blobs y tablas no conserva los metadatos u otras propiedades en el contenedor de hello, como la cuota del recurso compartido de archivos, nivel de acceso público o las directivas de acceso</span><span class="sxs-lookup"><span data-stu-id="36c1c-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="36c1c-347">Al cambiar de nombre los blobs (individualmente o dentro de un contenedor de blobs cuyo nombre ha cambiado), no se conservan las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="36c1c-348">Todas las otras propiedades y metadatos de blobs, archivos y entidades se conservan al cambiar de nombre.</span><span class="sxs-lookup"><span data-stu-id="36c1c-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="36c1c-349">No se puede copiar o cambiar de nombre recursos en cuentas conectadas mediante SAS.</span><span class="sxs-lookup"><span data-stu-id="36c1c-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="36c1c-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="36c1c-351">Versión 0.8.2</span><span class="sxs-lookup"><span data-stu-id="36c1c-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="36c1c-352">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-352">New</span></span>

* <span data-ttu-id="36c1c-353">Las cuentas de almacenamiento se agrupan por suscripciones; el almacenamiento de desarrollo y los recursos conectados mediante clave o SAS se muestran en el nodo (Local y Adjuntos).</span><span class="sxs-lookup"><span data-stu-id="36c1c-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="36c1c-354">Cierre la sesión de las cuentas en el panel “Configuración de la cuenta de Azure”.</span><span class="sxs-lookup"><span data-stu-id="36c1c-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="36c1c-355">Configurar tooenable de configuración de proxy y administrar inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="36c1c-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="36c1c-356">Cree y rompa concesiones de blobs.</span><span class="sxs-lookup"><span data-stu-id="36c1c-356">Create and break blob leases</span></span>
* <span data-ttu-id="36c1c-357">Abra contenedores de blobs, colas, tablas y archivos con un solo clic.</span><span class="sxs-lookup"><span data-stu-id="36c1c-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-358">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-358">Fixes</span></span>

* <span data-ttu-id="36c1c-359">Problema corregido: Los mensajes de cola insertados con bibliotecas de Java o .NET no se descodifican correctamente desde Base64.</span><span class="sxs-lookup"><span data-stu-id="36c1c-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="36c1c-360">Problema corregido: Las tablas de $metrics no se muestran en las cuentas de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="36c1c-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="36c1c-361">Problema corregido: El nodo de tablas no funciona para el almacenamiento local (desarrollo).</span><span class="sxs-lookup"><span data-stu-id="36c1c-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-362">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-362">Known Issues</span></span>

* <span data-ttu-id="36c1c-363">Puede que la instalación en macOS requiera permisos elevados.</span><span class="sxs-lookup"><span data-stu-id="36c1c-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="36c1c-364">15/06/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="36c1c-365">Versión 0.8.0</span><span class="sxs-lookup"><span data-stu-id="36c1c-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="36c1c-366">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-366">New</span></span>

* <span data-ttu-id="36c1c-367">Compatibilidad con recursos compartidos de archivos: visualización, carga, descarga, copia de archivos y directorios, URI de SAS (creación y conexión).</span><span class="sxs-lookup"><span data-stu-id="36c1c-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="36c1c-368">Mejor experiencia del usuario para la conexión tooStorage con URI de SAS o claves de cuenta</span><span class="sxs-lookup"><span data-stu-id="36c1c-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="36c1c-369">Exportación de resultados de consulta de tabla.</span><span class="sxs-lookup"><span data-stu-id="36c1c-369">Export table query results</span></span>
* <span data-ttu-id="36c1c-370">Reordenación y personalización de columnas de tabla.</span><span class="sxs-lookup"><span data-stu-id="36c1c-370">Table column reordering and customization</span></span>
* <span data-ttu-id="36c1c-371">Consulta de contenedores de blob $logs y tablas de $metrics para cuentas de almacenamiento con las métricas habilitadas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="36c1c-372">Comportamiento de importación y exportación mejorado. Ahora incluye el tipo de valor de propiedad.</span><span class="sxs-lookup"><span data-stu-id="36c1c-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-373">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-373">Fixes</span></span>

* <span data-ttu-id="36c1c-374">Problema corregido: Al cargar o descargar blobs grandes, se puede producir una carga o descarga incompleta.</span><span class="sxs-lookup"><span data-stu-id="36c1c-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="36c1c-375">Problema corregido: edición, la adición o la importación de una entidad con un valor de cadena numérica ("1") lo convertirá toodouble</span><span class="sxs-lookup"><span data-stu-id="36c1c-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="36c1c-376">Problema corregido: Nodo de tabla de hello tooexpand no se puede en el entorno de desarrollo local Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-377">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-377">Known Issues</span></span>

* <span data-ttu-id="36c1c-378">Las tablas de $metrics no son visibles para cuentas de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="36c1c-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="36c1c-379">Cola de mensajes agregado mediante programación no se muestren correctamente si los mensajes de saludo se codifican utilizando la codificación Base64</span><span class="sxs-lookup"><span data-stu-id="36c1c-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="36c1c-380">17/05/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="36c1c-381">Versión 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="36c1c-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="36c1c-382">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-382">New</span></span>

* <span data-ttu-id="36c1c-383">Mejor control de errores para bloqueos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="36c1c-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-384">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-384">Fixes</span></span>

* <span data-ttu-id="36c1c-385">Se ha corregido un error en el que los mensajes de la barra de información a veces no se mostraban cuando se requerían credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="36c1c-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-386">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-386">Known Issues</span></span>

* <span data-ttu-id="36c1c-387">Tablas: Agregar, editar, o importar una entidad que tiene una propiedad con un valor numérico de forma ambigua, como "1" o "1.0", y Hola toosend de intentos de usuario como un `Edm.String`, valor de hello volverá a través de API como un Edm.Double de cliente hello</span><span class="sxs-lookup"><span data-stu-id="36c1c-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="36c1c-388">31/03/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="36c1c-389">Versión 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="36c1c-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="36c1c-390">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-390">New</span></span>

* <span data-ttu-id="36c1c-391">Compatibilidad con tablas: visualización, realización de consultas, exportación, importación y operaciones CRUD para entidades.</span><span class="sxs-lookup"><span data-stu-id="36c1c-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="36c1c-392">Compatibilidad con colas: visualización, adición y eliminación de mensajes de la cola.</span><span class="sxs-lookup"><span data-stu-id="36c1c-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="36c1c-393">Generación de URI de SAS para cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="36c1c-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="36c1c-394">Cuentas de conexión tooStorage con URI de SAS</span><span class="sxs-lookup"><span data-stu-id="36c1c-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="36c1c-395">Notificaciones de actualización para las actualizaciones futuras tooStorage Explorer</span><span class="sxs-lookup"><span data-stu-id="36c1c-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="36c1c-396">Apariencia actualizada.</span><span class="sxs-lookup"><span data-stu-id="36c1c-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-397">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-397">Fixes</span></span>

* <span data-ttu-id="36c1c-398">Mejoras de rendimiento y confiabilidad.</span><span class="sxs-lookup"><span data-stu-id="36c1c-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="36c1c-399">Problemas conocidos y mitigaciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="36c1c-400">La descarga de archivos de blob grandes no funciona correctamente. Le recomendamos que use AzCopy mientras no se soluciona este problema.</span><span class="sxs-lookup"><span data-stu-id="36c1c-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="36c1c-401">Las credenciales de cuenta no pueden recuperar ni almacenado en memoria caché si la carpeta particular de hello no se encuentra o no puede escribirse en</span><span class="sxs-lookup"><span data-stu-id="36c1c-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="36c1c-402">Si nos estamos agregar, editar o importar una entidad que tiene una propiedad con un valor numérico de forma ambigua, como "1" o "1.0", y trata de usuario de hello toosend como un `Edm.String`, valor de hello volverá a través de API como un Edm.Double de cliente hello</span><span class="sxs-lookup"><span data-stu-id="36c1c-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="36c1c-403">Al importar archivos CSV con los registros de varias líneas, datos de hello pueden obtener reducidos o codificadas</span><span class="sxs-lookup"><span data-stu-id="36c1c-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="36c1c-404">03/02/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="36c1c-405">Versión 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="36c1c-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-406">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-406">Fixes</span></span>

* <span data-ttu-id="36c1c-407">Rendimiento general mejorado al cargar, descargar y copiar blobs.</span><span class="sxs-lookup"><span data-stu-id="36c1c-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="36c1c-408">14/01/2016</span><span class="sxs-lookup"><span data-stu-id="36c1c-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="36c1c-409">Versión 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="36c1c-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="36c1c-410">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-410">New</span></span>

* <span data-ttu-id="36c1c-411">Compatibilidad con Linux (tooOSX de características de paridad)</span><span class="sxs-lookup"><span data-stu-id="36c1c-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="36c1c-412">Agregue contenedores de blobs con clave de Firmas de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="36c1c-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="36c1c-413">Agregue cuentas de almacenamiento para Azure China.</span><span class="sxs-lookup"><span data-stu-id="36c1c-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="36c1c-414">Agregue cuentas de almacenamiento con puntos de conexión personalizados.</span><span class="sxs-lookup"><span data-stu-id="36c1c-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="36c1c-415">Abrir y ver los blobs de texto e imagen de contenido de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="36c1c-416">Vea y edite propiedades y metadatos de blob.</span><span class="sxs-lookup"><span data-stu-id="36c1c-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="36c1c-417">Correcciones</span><span class="sxs-lookup"><span data-stu-id="36c1c-417">Fixes</span></span>

* <span data-ttu-id="36c1c-418">Se ha corregido: carga o descarga un gran número de blobs (500 +) a veces podrían Hola aplicación toohave una pantalla en blanco</span><span class="sxs-lookup"><span data-stu-id="36c1c-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="36c1c-419">Problema corregido: al establecer el nivel de acceso público de contenedor de blob, Hola nuevo valor no se actualiza hasta que se vuelva a establecer el foco de hello en el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="36c1c-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="36c1c-420">Además, el cuadro de diálogo de hello siempre tiene como valor predeterminado demasiado "de acceso No público" y no Hola actual valor real.</span><span class="sxs-lookup"><span data-stu-id="36c1c-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="36c1c-421">Mejor accesibilidad de teclado general y compatibilidad con IU.</span><span class="sxs-lookup"><span data-stu-id="36c1c-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="36c1c-422">El historial de enlaces se ajusta cuando es demasiado largo con espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="36c1c-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="36c1c-423">El cuadro de diálogo de SAS admite la validación de entradas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="36c1c-424">Almacenamiento local continúa toobe disponible incluso si las credenciales de usuario han caducado</span><span class="sxs-lookup"><span data-stu-id="36c1c-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="36c1c-425">Cuando se elimina un contenedor de blobs abierto, se cierra el Explorador de blob Hola Hola derecha</span><span class="sxs-lookup"><span data-stu-id="36c1c-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-426">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-426">Known Issues</span></span>

* <span data-ttu-id="36c1c-427">Necesidades de instalación de Linux versión gcc había actualizado o ampliado – tooupgrade pasos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="36c1c-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="36c1c-428">18/11/2015</span><span class="sxs-lookup"><span data-stu-id="36c1c-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="36c1c-429">Versión 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="36c1c-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="36c1c-430">Nuevo</span><span class="sxs-lookup"><span data-stu-id="36c1c-430">New</span></span>

* <span data-ttu-id="36c1c-431">Versiones de Windows y macOS.</span><span class="sxs-lookup"><span data-stu-id="36c1c-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="36c1c-432">Inicie sesión en tooview sus cuentas de almacenamiento: use la cuenta de organización, Microsoft Account, 2FA, etcetera.</span><span class="sxs-lookup"><span data-stu-id="36c1c-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="36c1c-433">Almacenamiento de desarrollo local (use un emulador de almacenamiento, solo para Windows).</span><span class="sxs-lookup"><span data-stu-id="36c1c-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="36c1c-434">Compatibilidad de Azure Resource Manager y recursos clásicos.</span><span class="sxs-lookup"><span data-stu-id="36c1c-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="36c1c-435">Cree y elimine blobs, colas o tablas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="36c1c-436">Busque blobs, colas o tablas específicos.</span><span class="sxs-lookup"><span data-stu-id="36c1c-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="36c1c-437">Explorar el contenido de Hola de contenedores de blob</span><span class="sxs-lookup"><span data-stu-id="36c1c-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="36c1c-438">Vea y navegue por directorios.</span><span class="sxs-lookup"><span data-stu-id="36c1c-438">View and navigate through directories</span></span>
* <span data-ttu-id="36c1c-439">Cargue, descargue y elimine blobs y carpetas.</span><span class="sxs-lookup"><span data-stu-id="36c1c-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="36c1c-440">Vea y edite propiedades y metadatos de blob.</span><span class="sxs-lookup"><span data-stu-id="36c1c-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="36c1c-441">Genere claves SAS.</span><span class="sxs-lookup"><span data-stu-id="36c1c-441">Generate SAS keys</span></span>
* <span data-ttu-id="36c1c-442">Administre y cree directivas de acceso a almacenamiento (SAP).</span><span class="sxs-lookup"><span data-stu-id="36c1c-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="36c1c-443">Busque blobs por prefijo.</span><span class="sxs-lookup"><span data-stu-id="36c1c-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="36c1c-444">Arrastrar y colocar tooupload de archivos o descarga</span><span class="sxs-lookup"><span data-stu-id="36c1c-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="36c1c-445">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="36c1c-445">Known Issues</span></span>

* <span data-ttu-id="36c1c-446">Al establecer el nivel de acceso público de contenedor de blob, valor nuevo de hello no se actualiza hasta que se vuelva a establecer el foco de hello en el contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="36c1c-447">Cuando se abre el nivel de acceso público de hello diálogo tooset hello, siempre no muestra "acceso público" como hello, valor predeterminado y no Hola real actual</span><span class="sxs-lookup"><span data-stu-id="36c1c-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="36c1c-448">No se puede cambiar el nombre de los blobs descargados.</span><span class="sxs-lookup"><span data-stu-id="36c1c-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="36c1c-449">Entradas del registro de actividad en ocasiones quedar "bloqueado" en una en curso de estado cuando se produce un error y no se muestra el error de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="36c1c-450">A veces se bloquea o pone completamente en blanco al intentar tooupload o descarga un gran número de blobs</span><span class="sxs-lookup"><span data-stu-id="36c1c-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="36c1c-451">A veces no se puede cancelar una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="36c1c-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="36c1c-452">Durante la creación de un contenedor (blob o cola o tabla), si un nombre no válido de entrada y continuar toocreate otra nueva en un tipo de contenedor diferentes no puede establecer foco en el nuevo tipo de Hola</span><span class="sxs-lookup"><span data-stu-id="36c1c-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="36c1c-453">No se puede crear una carpeta nueva ni cambiarle el nombre.</span><span class="sxs-lookup"><span data-stu-id="36c1c-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md