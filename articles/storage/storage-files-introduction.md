---
title: "Introducción a Azure File Storage | Microsoft Docs"
description: "Información general sobre Azure File Storage, el servicio que permite crear y utilizar recursos compartidos de archivos en red en la nube de Microsoft utilizando el estándar del sector."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: bae2e9825bf158bb015ec0affa56f15ce5baa201
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="introduction-to-azure-file-storage"></a><span data-ttu-id="e553a-103">Introducción a Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="e553a-103">Introduction to Azure File storage</span></span>
<span data-ttu-id="e553a-104">Azure File Storage ofrece recursos compartidos de archivos en red en la nube mediante el uso del estándar del sector, el [Protocolo Server Message Block (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) y [Common Internet File System (CIFS)](https://technet.microsoft.com/library/cc939973.aspx).</span><span class="sxs-lookup"><span data-stu-id="e553a-104">Azure File storage offers network file shares in the cloud using the industry standard [Server Message Block (SMB) Protocol](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) and [Common Internet File System (CIFS)](https://technet.microsoft.com/library/cc939973.aspx).</span></span> <span data-ttu-id="e553a-105">Los recursos compartidos de archivos de Azure se pueden montar de modo concurrente por los clientes, como las implementaciones locales de Windows, Mac OS y Linux o Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="e553a-105">Azure File shares can be mounted concurrently by clients such as on-premises deployments of Windows, macOS, Linux, or by Azure Virtual Machines.</span></span> <span data-ttu-id="e553a-106">Una cuenta de almacenamiento de uso general proporciona acceso a Azure File Storage y otros servicios como Blobs, discos de máquina virtual de Azure o Queues, todo desde una única cuenta.</span><span class="sxs-lookup"><span data-stu-id="e553a-106">A general-purpose storage account gives you access to Azure File Storage and other services such as Blobs, Azure virtual machine disks, Queues under a single account.</span></span>



## <a name="videos"></a><span data-ttu-id="e553a-107">Vídeos</span><span class="sxs-lookup"><span data-stu-id="e553a-107">Videos</span></span>
| <span data-ttu-id="e553a-108">Introducción a Azure File Storage (27 minutos)</span><span class="sxs-lookup"><span data-stu-id="e553a-108">Introducing Azure File storage (27m)</span></span> | <span data-ttu-id="e553a-109">Tutorial de Azure File Storage (5 minutos)</span><span class="sxs-lookup"><span data-stu-id="e553a-109">Azure File storage Tutorial (5 minutes)</span></span>  |
|-|-|
| <span data-ttu-id="e553a-110">[![Captura de pantalla del vídeo Introducción a Azure File Storage - haga clic para reproducir.](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs)</span><span class="sxs-lookup"><span data-stu-id="e553a-110">[![Screencap of the Introducing Azure File storage video - click to play!](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs)</span></span> | <span data-ttu-id="e553a-111">[![Captura de pantalla del vídeo Tutorial de Azure File Storage - haga clic para reproducir.](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/)</span><span class="sxs-lookup"><span data-stu-id="e553a-111">[![Screencap of the Azure File storage Tutorial - click to play!](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/)</span></span> |

## <a name="why-azure-file-storage-is-useful"></a><span data-ttu-id="e553a-112">¿Por qué es útil Azure File Storage?</span><span class="sxs-lookup"><span data-stu-id="e553a-112">Why Azure File storage is useful</span></span>
<span data-ttu-id="e553a-113">Azure File Storage le permite reemplazar los servidores de archivos con Windows Server, Linux y basados en NAS, tanto hospedados de modo local como en la nube, por un recurso compartido de archivos en la nube independiente del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e553a-113">Azure File storage allows you to replace Windows Server, Linux, or NAS-based file servers hosted on-premises or in the cloud with an OS-free cloud file share.</span></span> <span data-ttu-id="e553a-114">Esto tiene las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e553a-114">This has the following benefits:</span></span>

* <span data-ttu-id="e553a-115">**Acceso compartido:**.</span><span class="sxs-lookup"><span data-stu-id="e553a-115">**Shared access:**.</span></span> <span data-ttu-id="e553a-116">Los recursos compartidos de archivos Azure admiten el protocolo SMB estándar del sector, lo que significa que puede reemplazar perfectamente los recursos compartidos de archivos en local por recursos compartidos de archivos de Azure sin preocuparse de compatibilidad de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e553a-116">Azure File shares support the industry standard SMB protocol, meaning you can seamlessly replace your on-premises file shares with Azure File shares without worrying about application compatibility.</span></span> <span data-ttu-id="e553a-117">La posibilidad de compartir un sistema de archivos entre varios equipos, aplicaciones o instancias es una ventaja importante de Azure File Storage para aquellas aplicaciones que necesitan la posibilidad de compartir.</span><span class="sxs-lookup"><span data-stu-id="e553a-117">Being able to share a file system across multiple machines, applications/instances is a significant advantage with Azure File storage for applications that need shareability.</span></span> 
* <span data-ttu-id="e553a-118">**Completamente administrado**.</span><span class="sxs-lookup"><span data-stu-id="e553a-118">**Fully Managed**.</span></span> <span data-ttu-id="e553a-119">Los recursos compartidos de archivos de Azure pueden crearse sin necesidad de administrar ni el hardware ni un sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e553a-119">Azure File shares can be created without the need to manage hardware or an OS.</span></span> <span data-ttu-id="e553a-120">Esto significa que no tiene que tratar con la aplicación de actualizaciones de seguridad críticas en el sistema operativo del servidor ni ocuparse de reemplazar discos duros defectuosos.</span><span class="sxs-lookup"><span data-stu-id="e553a-120">This means you don't have to deal with patching the server OS with critical security upgrades or replacing faulty hard disks.</span></span>
* <span data-ttu-id="e553a-121">**Herramientas y Scripting**.</span><span class="sxs-lookup"><span data-stu-id="e553a-121">**Scripting and Tooling**.</span></span> <span data-ttu-id="e553a-122">Los cmdlets de PowerShell y la CLI de Azure pueden utilizarse para crear, montar y administrar recursos compartidos de almacenamiento de archivos como parte de la administración de aplicaciones de Azure. Puede crear y administrar recursos compartidos de archivos de Azure mediante Azure Portal y el Explorador de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e553a-122">PowerShell cmdlets and Azure CLI  can be used to create, mount, and manage File storage shares as part of the administration of Azure applications.You can create and manage Azure file shares using Azure Portal and Azure storage Explorer.</span></span> 
* <span data-ttu-id="e553a-123">**Resistencia**.</span><span class="sxs-lookup"><span data-stu-id="e553a-123">**Resiliency**.</span></span> <span data-ttu-id="e553a-124">Azure File Storage fue creado desde sus comienzos para estar siempre disponible.</span><span class="sxs-lookup"><span data-stu-id="e553a-124">Azure File storage has been built from the ground up to be always available.</span></span> <span data-ttu-id="e553a-125">Reemplazar los recursos compartidos de archivos en local por Azure File Storage significa que ya no tendrá que tratar con problemas de red o interrupciones del suministro eléctrico local.</span><span class="sxs-lookup"><span data-stu-id="e553a-125">Replacing on-premises file shares with Azure File storage means you no longer have to wake up to deal with local power outages or network issues.</span></span> 
* <span data-ttu-id="e553a-126">**Programación amigable**.</span><span class="sxs-lookup"><span data-stu-id="e553a-126">**Familiar Programmability**.</span></span> <span data-ttu-id="e553a-127">Las aplicaciones que se ejecutan en Azure pueden tener acceso a los datos en el recurso compartido mediante las [API de E/S del sistema](https://msdn.microsoft.com/library/system.io.file.aspx).</span><span class="sxs-lookup"><span data-stu-id="e553a-127">Applications running in Azure can access data in the share via file [system I/O APIs](https://msdn.microsoft.com/library/system.io.file.aspx).</span></span> <span data-ttu-id="e553a-128">Por tanto, los desarrolladores pueden aprovechar el código y los conocimientos que ya tienen para migrar las aplicaciones actuales.</span><span class="sxs-lookup"><span data-stu-id="e553a-128">Developers can therefore leverage their existing code and skills to migrate existing applications.</span></span> <span data-ttu-id="e553a-129">Además de las API de E/S del sistema, puede usar las [Bibliotecas de cliente de Azure Storage](https://msdn.microsoft.com/library/azure/dn261237.aspx) o la [API de REST de Azure Storage](/rest/api/storageservices/file-service-rest-api).</span><span class="sxs-lookup"><span data-stu-id="e553a-129">In addition to System IO APIs, you can use [Azure Storage Client Libraries](https://msdn.microsoft.com/library/azure/dn261237.aspx) or the [Azure Storage REST API](/rest/api/storageservices/file-service-rest-api).</span></span>

<span data-ttu-id="e553a-130">Los recursos compartidos de archivos de Azure se pueden usar para:</span><span class="sxs-lookup"><span data-stu-id="e553a-130">Azure File shares can be used to:</span></span>

* <span data-ttu-id="e553a-131">**Reemplazar servidores de archivos locales**:</span><span class="sxs-lookup"><span data-stu-id="e553a-131">**Replace on-premises file servers**:</span></span>  
    <span data-ttu-id="e553a-132">Azure File Storage puede utilizarse para reemplazar completamente los recursos compartidos de archivos en servidores de archivos tradicionales en local o dispositivos NAS.</span><span class="sxs-lookup"><span data-stu-id="e553a-132">Azure File storage can be used to completely replace file shares on traditional on-premises file servers or NAS devices.</span></span> <span data-ttu-id="e553a-133">Desde sistemas operativos tan extendidos como Windows, Mac OS y Linux se puede montar de un modo sencillo un recurso compartido de archivos de Azure desde cualquier lugar del mundo.</span><span class="sxs-lookup"><span data-stu-id="e553a-133">Popular operating systems such as Windows, macOS, and Linux can easily mount an Azure File share wherever they are in the world.</span></span>

* <span data-ttu-id="e553a-134">**Aplicaciones "Levantar y mover"**:</span><span class="sxs-lookup"><span data-stu-id="e553a-134">**"Lift and Shift" applications**:</span></span>  
    <span data-ttu-id="e553a-135">Azure File Storage hace sencillo "levantar y mover" aplicaciones a la nube que utilizan recursos compartidos de archivos locales para compartir datos entre diferentes partes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e553a-135">Azure File storage makes it easy to "lift and shift" applications to the cloud that use on-premises file shares to share data between parts of the application.</span></span> <span data-ttu-id="e553a-136">Para ello, cada máquina virtual se conecta al recurso compartido de archivos y así puede leer y escribir archivos del mismo modo que lo haría sobre un recurso compartido de archivos local.</span><span class="sxs-lookup"><span data-stu-id="e553a-136">To make this happen, each VM connects to the file share and then it can read and write files just like it would against an on-premises file share.</span></span>

* <span data-ttu-id="e553a-137">**Simplificar el desarrollo en la nube**:</span><span class="sxs-lookup"><span data-stu-id="e553a-137">**Simplify Cloud Development**:</span></span>  
    <span data-ttu-id="e553a-138">Azure File Storage puede utilizarse de varias maneras diferentes para simplificar los nuevos proyectos de desarrollo en la nube.</span><span class="sxs-lookup"><span data-stu-id="e553a-138">Azure File storage can be used in a number of different ways to simplify new cloud development projects.</span></span>
    * <span data-ttu-id="e553a-139">**Configuración de aplicaciones compartida**:</span><span class="sxs-lookup"><span data-stu-id="e553a-139">**Shared Application Settings**:</span></span>  
        <span data-ttu-id="e553a-140">Un patrón habitual entre las aplicaciones distribuidas es contar con archivos de configuración en una ubicación centralizada que permite tener acceso a ellos desde muchas máquinas virtuales diferentes.</span><span class="sxs-lookup"><span data-stu-id="e553a-140">A common pattern for distributed applications is to have configuration files in a centralized location where they can be accessed from many different VMs.</span></span> <span data-ttu-id="e553a-141">Estos archivos de configuración ahora se pueden almacenar en un recurso compartido de archivos de Azure para que lo lean todas las instancias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e553a-141">Such configuration files can now be stored in an Azure File share, and read by all application instances.</span></span> <span data-ttu-id="e553a-142">La configuración se puede administrar también a través de la interfaz REST, que permite un acceso a los archivos de configuración desde cualquier parte del mundo.</span><span class="sxs-lookup"><span data-stu-id="e553a-142">These settings can also be managed via the REST interface, which allows worldwide access to the configuration files.</span></span>

    * <span data-ttu-id="e553a-143">**Recurso compartido de diagnóstico**:</span><span class="sxs-lookup"><span data-stu-id="e553a-143">**Diagnostic Share**:</span></span>  
        <span data-ttu-id="e553a-144">Un recurso compartido de archivos de Azure también puede usarse para guardar archivos de diagnóstico como los registros, las métricas y los volcados de memoria.</span><span class="sxs-lookup"><span data-stu-id="e553a-144">An Azure File share can also be used to save diagnostic files like logs, metrics, and crash dumps.</span></span> <span data-ttu-id="e553a-145">El hecho de poder tener acceso a estos archivos a través tanto de SMB como de la interfaz REST permite a las aplicaciones utilizar una variedad de herramientas de análisis para procesar y analizar los datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e553a-145">Having these available through both the SMB and REST interface allows applications to build or leverage a variety of analysis tools for processing and analyzing the diagnostic data.</span></span>

    * <span data-ttu-id="e553a-146">**Desarrollo, pruebas y depuración**:</span><span class="sxs-lookup"><span data-stu-id="e553a-146">**Dev/Test/Debug**:</span></span>  
        <span data-ttu-id="e553a-147">Cuando los desarrolladores o administradores están trabajando en máquinas virtuales en la nube, a menudo necesitan diversas herramientas o utilidades.</span><span class="sxs-lookup"><span data-stu-id="e553a-147">When developers or administrators are working on VMs in the cloud, they often need a set of tools or utilities.</span></span> <span data-ttu-id="e553a-148">La instalación y distribución de estas utilidades en cada una de las máquinas virtuales en las que se necesiten requiere mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="e553a-148">Installing and distributing these utilities on each virtual machine where they are needed can be a time consuming exercise.</span></span> <span data-ttu-id="e553a-149">Con Azure File Storage, un desarrollador o administrador puede almacenar sus herramientas favoritas en un recurso compartido de archivos y conectarse a él desde cualquier máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e553a-149">With Azure File storage, a developer or administrator can store their favorite tools on a file share, which can be easily connected to from any virtual machine.</span></span>
        
## <a name="how-does-it-work"></a><span data-ttu-id="e553a-150">¿Cómo funciona?</span><span class="sxs-lookup"><span data-stu-id="e553a-150">How does it work?</span></span>
<span data-ttu-id="e553a-151">La administración de recursos compartidos de archivos de Azure es mucho más simple que la administración de recursos compartidos de archivos en local.</span><span class="sxs-lookup"><span data-stu-id="e553a-151">Managing Azure File shares is a lot simpler than managing file shares on-premises.</span></span> <span data-ttu-id="e553a-152">El siguiente diagrama muestra la administración de Azure File Storage:</span><span class="sxs-lookup"><span data-stu-id="e553a-152">The following diagram illustrates the Azure File storage management constructs:</span></span>

![Estructura de archivos](../../includes/media/storage-file-concepts-include/files-concepts.png)

* <span data-ttu-id="e553a-154">**Cuenta de almacenamiento**: todo el acceso a Almacenamiento de Azure se realiza a través de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e553a-154">**Storage Account**: All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="e553a-155">Consulte Objetivos de escalabilidad y rendimiento del almacenamiento de Azure para obtener información sobre la capacidad de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e553a-155">See Azure Storage Scalability and Performance Targets for details about storage account capacity.</span></span>
* <span data-ttu-id="e553a-156">**Recurso compartido:** un recurso compartido de almacenamiento de archivos es un recurso compartido de archivos de SMB en Azure.</span><span class="sxs-lookup"><span data-stu-id="e553a-156">**Share**: A File Storage share is an SMB file share in Azure.</span></span> <span data-ttu-id="e553a-157">Todos los directorios y archivos se deben crear en un recurso compartido principal.</span><span class="sxs-lookup"><span data-stu-id="e553a-157">All directories and files must be created in a parent share.</span></span> <span data-ttu-id="e553a-158">Una cuenta puede contener un número ilimitado de recursos compartidos y un recurso compartido puede almacenar un número ilimitado de archivos, hasta una capacidad total de 5 TB del recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="e553a-158">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the 5 TB total capacity of the file share.</span></span>
* <span data-ttu-id="e553a-159">**Directorio:** una jerarquía de directorios opcional.</span><span class="sxs-lookup"><span data-stu-id="e553a-159">**Directory**: An optional hierarchy of directories.</span></span>
* <span data-ttu-id="e553a-160">**Archivo:** un archivo del recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="e553a-160">**File**: A file in the share.</span></span> <span data-ttu-id="e553a-161">Un archivo puede tener un tamaño de hasta 1 TB.</span><span class="sxs-lookup"><span data-stu-id="e553a-161">A file may be up to 1 TB in size.</span></span>
* <span data-ttu-id="e553a-162">**Formato de URL:** los archivos son direccionables mediante el formato de URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="e553a-162">**URL format**: Files are addressable using the following URL format:</span></span>  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```
## <a name="next-steps"></a><span data-ttu-id="e553a-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e553a-163">Next Steps</span></span>
* [<span data-ttu-id="e553a-164">Creación de un recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="e553a-164">Create Azure File Share</span></span>](storage-file-how-to-create-file-share.md)
* [<span data-ttu-id="e553a-165">Conexión y montaje en Windows</span><span class="sxs-lookup"><span data-stu-id="e553a-165">Connect and Mount on Windows</span></span>](storage-file-how-to-use-files-windows.md)
* [<span data-ttu-id="e553a-166">Conexión y montaje en Linux</span><span class="sxs-lookup"><span data-stu-id="e553a-166">Connect and Mount on Linux</span></span>](storage-how-to-use-files-linux.md)
* [<span data-ttu-id="e553a-167">Conexión y montaje en macOS</span><span class="sxs-lookup"><span data-stu-id="e553a-167">Connect and Mount on macOS</span></span>](storage-file-how-to-use-files-mac.md)
* [<span data-ttu-id="e553a-168">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="e553a-168">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="e553a-169">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="e553a-169">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="e553a-170">Artículos y vídeos conceptuales</span><span class="sxs-lookup"><span data-stu-id="e553a-170">Conceptual articles and videos</span></span>
* [<span data-ttu-id="e553a-171">Azure File Storage: un sistema de archivos SMB en la nube sin dificultades para Windows y Linux</span><span class="sxs-lookup"><span data-stu-id="e553a-171">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="e553a-172">Compatibilidad de herramientas con Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="e553a-172">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="e553a-173">Usar Azure PowerShell con Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e553a-173">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="e553a-174">Uso de AzCopy con Almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e553a-174">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="e553a-175">Uso de la CLI de Azure con Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="e553a-175">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)

### <a name="blog-posts"></a><span data-ttu-id="e553a-176">Publicaciones de blog</span><span class="sxs-lookup"><span data-stu-id="e553a-176">Blog posts</span></span>
* [<span data-ttu-id="e553a-177">El almacenamiento de archivos de Azure ya está disponible de manera general</span><span class="sxs-lookup"><span data-stu-id="e553a-177">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="e553a-178">En el interior de Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="e553a-178">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="e553a-179">Introducing Microsoft Azure File Service (Introducción al servicio de archivos de Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="e553a-179">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="e553a-180">Migración de datos a Azure Files</span><span class="sxs-lookup"><span data-stu-id="e553a-180">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="e553a-181">Referencia</span><span class="sxs-lookup"><span data-stu-id="e553a-181">Reference</span></span>
* [<span data-ttu-id="e553a-182">Referencia de la biblioteca de clientes de almacenamiento para .NET</span><span class="sxs-lookup"><span data-stu-id="e553a-182">storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="e553a-183">Referencia de la API REST del servicio de archivos</span><span class="sxs-lookup"><span data-stu-id="e553a-183">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)