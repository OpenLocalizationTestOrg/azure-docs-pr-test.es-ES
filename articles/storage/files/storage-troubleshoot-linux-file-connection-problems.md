---
title: "Solución de problemas de Azure File Storage en Linux | Microsoft Docs"
description: "Solución de problemas de Azure File Storage en Linux"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 0cab2e3540afdbdc64cb77fca4b9219c77258166
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="6485a-103">Solución de problemas de Azure File Storage en Linux</span><span class="sxs-lookup"><span data-stu-id="6485a-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="6485a-104">En este artículo se enumeran los problemas habituales relacionados con Microsoft Azure File Storage cuando se conecta desde clientes de Linux.</span><span class="sxs-lookup"><span data-stu-id="6485a-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="6485a-105">También se proporcionan posibles causas de estos problemas y sus resoluciones.</span><span class="sxs-lookup"><span data-stu-id="6485a-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a><span data-ttu-id="6485a-106">"[permiso denegado] Cuota de disco superada" al intentar abrir un archivo</span><span class="sxs-lookup"><span data-stu-id="6485a-106">"[permission denied] Disk quota exceeded" when you try to open a file</span></span>

<span data-ttu-id="6485a-107">En Linux, recibe un mensaje de error similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="6485a-107">In Linux, you receive an error message that resembles the following:</span></span>

<span data-ttu-id="6485a-108">**<filename> [permiso denegado] Cuota de disco superada**</span><span class="sxs-lookup"><span data-stu-id="6485a-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="6485a-109">Causa</span><span class="sxs-lookup"><span data-stu-id="6485a-109">Cause</span></span>

<span data-ttu-id="6485a-110">Se ha alcanzado el límite superior de identificadores abiertos simultáneos permitidos para un archivo.</span><span class="sxs-lookup"><span data-stu-id="6485a-110">You have reached the upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="6485a-111">Solución</span><span class="sxs-lookup"><span data-stu-id="6485a-111">Solution</span></span>

<span data-ttu-id="6485a-112">Reduzca el número de identificadores abiertos simultáneos cerrando algunos de ellos y, después, vuelva a realizar la operación.</span><span class="sxs-lookup"><span data-stu-id="6485a-112">Reduce the number of concurrent open handles by closing some handles, and then retry the operation.</span></span> <span data-ttu-id="6485a-113">Para más información, consulte [Lista de comprobación de rendimiento y escalabilidad de Microsoft Azure Storage](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6485a-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-linux"></a><span data-ttu-id="6485a-114">Copia de archivos lenta en y desde Azure File Storage en Linux</span><span class="sxs-lookup"><span data-stu-id="6485a-114">Slow file copying to and from Azure File storage in Linux</span></span>

-   <span data-ttu-id="6485a-115">Si no tiene un requisito mínimo de tamaño de E/S específico, se recomienda que utilice 1 MB como el tamaño de E/S para disfrutar de un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="6485a-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="6485a-116">Si conoce el tamaño final de un archivo que amplía mediante operaciones de escritura y el software no presenta problemas de compatibilidad cuando una cola no escrita del archivo contiene ceros, establezca el tamaño de archivo con antelación en lugar de hacer que cada escritura sea una escritura de ampliación.</span><span class="sxs-lookup"><span data-stu-id="6485a-116">If you know the final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="6485a-117">Utilice el método de copia correcto:</span><span class="sxs-lookup"><span data-stu-id="6485a-117">Use the right copy method:</span></span>
    -   <span data-ttu-id="6485a-118">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) para todas las transferencias entre dos recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="6485a-118">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="6485a-119">Utilice [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre recursos compartidos de archivos y un equipo local.</span><span class="sxs-lookup"><span data-stu-id="6485a-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="6485a-120">"Error de montaje (112): El host está apagado" debido a un tiempo de espera de reconexión</span><span class="sxs-lookup"><span data-stu-id="6485a-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="6485a-121">Se produce un error de montaje "112" en el cliente de Linux cuando este lleva inactivo mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="6485a-121">A "112" mount error occurs on the Linux client when the client has been idle for a long time.</span></span> <span data-ttu-id="6485a-122">Después del tiempo de inactividad extendido, el cliente se desconecta y se agota el tiempo de espera de la conexión.</span><span class="sxs-lookup"><span data-stu-id="6485a-122">After extended idle time, the client disconnects and the connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="6485a-123">Causa</span><span class="sxs-lookup"><span data-stu-id="6485a-123">Cause</span></span>

<span data-ttu-id="6485a-124">La conexión puede estar inactiva por las razones siguientes:</span><span class="sxs-lookup"><span data-stu-id="6485a-124">The connection can be idle for the following reasons:</span></span>

-   <span data-ttu-id="6485a-125">Errores de comunicación de la red que impiden el restablecimiento de una conexión TCP con el servidor cuando se usa la opción de montaje predeterminada “flexible”</span><span class="sxs-lookup"><span data-stu-id="6485a-125">Network communication failures that prevent re-establishing a TCP connection to the server when the default “soft” mount option is used</span></span>
-   <span data-ttu-id="6485a-126">Correcciones de reconexión recientes que no están presentes en los kernels anteriores</span><span class="sxs-lookup"><span data-stu-id="6485a-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="6485a-127">Solución</span><span class="sxs-lookup"><span data-stu-id="6485a-127">Solution</span></span>

<span data-ttu-id="6485a-128">Este problema de reconexión en el kernel de Linux se ha corregido como parte de los siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="6485a-128">This reconnection problem in the Linux kernel is now fixed as part of the following changes:</span></span>

- <span data-ttu-id="6485a-129">[Fix reconnect to not defer smb3 session reconnect long after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93) (Corregir la reconexión para que no aplace la reconexión de la sesión de smb3 mucho después de la reconexión del socket)</span><span class="sxs-lookup"><span data-stu-id="6485a-129">[Fix reconnect to not defer smb3 session reconnect long after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)</span></span>
-   <span data-ttu-id="6485a-130">[Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7) (Llamar al servicio de eco inmediatamente después de volver a conectar el socket)</span><span class="sxs-lookup"><span data-stu-id="6485a-130">[Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)</span></span>
-   <span data-ttu-id="6485a-131">[CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b) (CIFS: Corregir un posible daño de memoria durante la reconexión)</span><span class="sxs-lookup"><span data-stu-id="6485a-131">[CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)</span></span>
-   <span data-ttu-id="6485a-132">[CIFS: Fix a possible double locking of mutex during reconnect (or kernel v4.9 and later)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183) (CIFS: Corregir un posible bloqueo doble de exclusión mutua durante la reconexión: para el kernel v4.9 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="6485a-132">[CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)</span></span>

<span data-ttu-id="6485a-133">Pero es posible que estos cambios todavía no se migren a todas las distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="6485a-133">However, these changes might not be ported yet to all the Linux distributions.</span></span> <span data-ttu-id="6485a-134">Esta corrección y otras correcciones de reconexión se realizan en los siguientes kernels de Linux conocidos: 4.4.40, 4.8.16 y 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="6485a-134">This fix and other reconnection fixes are made in the following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="6485a-135">Puede obtener esta corrección actualizando a una de estas versiones de kernel recomendadas.</span><span class="sxs-lookup"><span data-stu-id="6485a-135">You can get this fix by upgrading to one of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="6485a-136">Solución alternativa</span><span class="sxs-lookup"><span data-stu-id="6485a-136">Workaround</span></span>

<span data-ttu-id="6485a-137">Una solución alternativa para este problema es especificar un montaje forzado.</span><span class="sxs-lookup"><span data-stu-id="6485a-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="6485a-138">Esta solución obliga al cliente a esperar hasta que se establezca una conexión o hasta que se interrumpa explícitamente, y puede usarse para evitar errores debidos a los tiempos de espera de la red.</span><span class="sxs-lookup"><span data-stu-id="6485a-138">This forces the client to wait until a connection is established or until it’s explicitly interrupted and can be used to prevent errors because of network time-outs.</span></span> <span data-ttu-id="6485a-139">Sin embargo, esta solución alternativa puede provocar esperas indefinidas.</span><span class="sxs-lookup"><span data-stu-id="6485a-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="6485a-140">Esté preparado para detener las conexiones según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6485a-140">Be prepared to stop connections as necessary.</span></span>

<span data-ttu-id="6485a-141">Si no puede actualizar a las versiones más recientes del kernel, puede solucionar este problema manteniendo un archivo en el recurso compartido de archivos de Azure en el que se escribe cada 30 segundos o menos.</span><span class="sxs-lookup"><span data-stu-id="6485a-141">If you cannot upgrade to the latest kernel versions, you can work around this problem by keeping a file in the Azure file share that you write to every 30 seconds or less.</span></span> <span data-ttu-id="6485a-142">Esta debe ser una operación de escritura, como volver a escribir la fecha de creación o modificación en el archivo.</span><span class="sxs-lookup"><span data-stu-id="6485a-142">This must be a write operation, such as rewriting the created or modified date on the file.</span></span> <span data-ttu-id="6485a-143">De lo contrario, podría obtener resultados almacenados en caché y la operación podría no desencadenar la reconexión.</span><span class="sxs-lookup"><span data-stu-id="6485a-143">Otherwise, you might get cached results, and your operation might not trigger the reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="6485a-144">"Error de montaje (115): Operación en curso" cuando monta Azure File Storage mediante SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="6485a-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="6485a-145">Causa</span><span class="sxs-lookup"><span data-stu-id="6485a-145">Cause</span></span>

<span data-ttu-id="6485a-146">En algunas distribuciones de Linux todavía no se admiten las características de cifrado de SMB 3.0 y es posible que los usuarios reciban un mensaje de error "115" al tratar de montar Azure File Storage mediante SMB 3.0 debido a una característica que falta.</span><span class="sxs-lookup"><span data-stu-id="6485a-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try to mount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="6485a-147">Solución</span><span class="sxs-lookup"><span data-stu-id="6485a-147">Solution</span></span>

<span data-ttu-id="6485a-148">La característica de cifrado de SMB 3.0 para Linux se introdujo en el kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="6485a-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="6485a-149">Esta característica permite el montaje de recursos compartidos de Azure File desde el entorno local o una región distinta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6485a-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="6485a-150">En el momento de la publicación, esta funcionalidad se ha usado en Ubuntu 17.04 y Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="6485a-150">At the time of publishing, this functionality has been backported to Ubuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="6485a-151">Si el cliente de SMB de Linux no admite el cifrado, monte Azure File Storage con SMB 2.1 desde una máquina virtual Linux de Azure que se encuentre en el mismo centro de datos que la cuenta de File Storage.</span><span class="sxs-lookup"><span data-stu-id="6485a-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in the same datacenter as the File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="6485a-152">Rendimiento lento en un recurso compartido de archivos de Azure montado en una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="6485a-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="6485a-153">Causa</span><span class="sxs-lookup"><span data-stu-id="6485a-153">Cause</span></span>

<span data-ttu-id="6485a-154">Una posible causa de un rendimiento lento es que el almacenamiento en caché está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="6485a-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="6485a-155">Solución</span><span class="sxs-lookup"><span data-stu-id="6485a-155">Solution</span></span>

<span data-ttu-id="6485a-156">Para comprobar si el almacenamiento en caché está deshabilitado, busque la entrada **cache=**.</span><span class="sxs-lookup"><span data-stu-id="6485a-156">To check whether caching is disabled, look for the **cache=** entry.</span></span> 

<span data-ttu-id="6485a-157">**Cache=none** indica que el almacenamiento en caché está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="6485a-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="6485a-158">Vuelva a montar el recurso compartido mediante el comando de montaje predeterminado o agregando explícitamente la opción **cache=strict** al comando de montaje con el fin de asegurarse de que el almacenamiento en caché predeterminado o el modo de almacenamiento en caché "strict" esté habilitado.</span><span class="sxs-lookup"><span data-stu-id="6485a-158">Remount the share by using the default mount command or by explicitly adding the **cache=strict** option to the mount command to ensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="6485a-159">En algunos escenarios, la opción de montaje **serverino** puede hacer que el comando **ls** se ejecute en cada entrada de directorio.</span><span class="sxs-lookup"><span data-stu-id="6485a-159">In some scenarios, the **serverino** mount option can cause the **ls** command to run stat against every directory entry.</span></span> <span data-ttu-id="6485a-160">Este comportamiento produce una disminución del rendimiento cuando se muestra un listado de un directorio grande.</span><span class="sxs-lookup"><span data-stu-id="6485a-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="6485a-161">Puede comprobar las opciones de montaje en la entrada **/etc/fstab**:</span><span class="sxs-lookup"><span data-stu-id="6485a-161">You can check the mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="6485a-162">También puede comprobar si se usan las opciones correctas ejecutando el comando **sudo mount | grep cifs** y comprobando su salida, como la siguiente salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6485a-162">You can also check whether the correct options are being used by running the  **sudo mount | grep cifs** command and checking its output, such as the following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="6485a-163">Si no está presente la opción**cache=strict** o **serverino**, desmonte y vuelva a montar Azure File Storage ejecutando el comando de montaje desde la [documentación](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6485a-163">If the **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running the mount command from the [documentation](../storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="6485a-164">A continuación, vuelva a comprobar que la entrada **/etc/fstab** tiene las opciones correctas.</span><span class="sxs-lookup"><span data-stu-id="6485a-164">Then, recheck that the **/etc/fstab** entry has the correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a><span data-ttu-id="6485a-165">Se perdieron las marcas de tiempo al copiar archivos de Windows a Linux</span><span class="sxs-lookup"><span data-stu-id="6485a-165">Time stamps were lost in copying files from Windows to Linux</span></span>

<span data-ttu-id="6485a-166">En las plataformas Unix y Linux, el comando **cp -p** produce un error si los archivos 1 y 2 pertenecen a distintos usuarios.</span><span class="sxs-lookup"><span data-stu-id="6485a-166">On Linux/Unix platforms, the **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="6485a-167">Causa</span><span class="sxs-lookup"><span data-stu-id="6485a-167">Cause</span></span>

<span data-ttu-id="6485a-168">La marca para exigir **f** en COPYFILE da como resultado la ejecución de **cp -p -f** en Unix.</span><span class="sxs-lookup"><span data-stu-id="6485a-168">The force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="6485a-169">Este comando tampoco conserva la marca de tiempo del archivo que no el usuario posee.</span><span class="sxs-lookup"><span data-stu-id="6485a-169">This command also fails to preserve the time stamp of the file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="6485a-170">Solución alternativa</span><span class="sxs-lookup"><span data-stu-id="6485a-170">Workaround</span></span>

<span data-ttu-id="6485a-171">Utilice el usuario de la cuenta de almacenamiento para copiar los archivos:</span><span class="sxs-lookup"><span data-stu-id="6485a-171">Use the storage account user for copying the files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="6485a-172">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="6485a-172">Need help?</span></span> <span data-ttu-id="6485a-173">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="6485a-173">Contact support.</span></span>

<span data-ttu-id="6485a-174">Si sigue necesitando ayuda, [póngase en contacto con el soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver el problema rápidamente.</span><span class="sxs-lookup"><span data-stu-id="6485a-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
