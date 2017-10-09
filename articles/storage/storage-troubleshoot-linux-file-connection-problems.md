---
title: problemas de almacenamiento de archivos de Azure aaaTroubleshoot en Linux | Documentos de Microsoft
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
ms.openlocfilehash: 3dc537d714244451a5ff8e01f4a27f03873cf2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="7099b-103">Solución de problemas de Azure File Storage en Linux</span><span class="sxs-lookup"><span data-stu-id="7099b-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="7099b-104">Este artículo enumeran los problemas comunes que están relacionado tooMicrosoft almacenamiento de archivos de Azure cuando conectan desde clientes de Linux.</span><span class="sxs-lookup"><span data-stu-id="7099b-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="7099b-105">También se proporcionan posibles causas de estos problemas y sus resoluciones.</span><span class="sxs-lookup"><span data-stu-id="7099b-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a><span data-ttu-id="7099b-106">"superada la cuota de disco [permiso denegado]" al intentar tooopen un archivo</span><span class="sxs-lookup"><span data-stu-id="7099b-106">"[permission denied] Disk quota exceeded" when you try tooopen a file</span></span>

<span data-ttu-id="7099b-107">En Linux, recibirá un mensaje de error similar al siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="7099b-107">In Linux, you receive an error message that resembles hello following:</span></span>

<span data-ttu-id="7099b-108">**<filename> [permiso denegado] Cuota de disco superada**</span><span class="sxs-lookup"><span data-stu-id="7099b-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="7099b-109">Causa</span><span class="sxs-lookup"><span data-stu-id="7099b-109">Cause</span></span>

<span data-ttu-id="7099b-110">Ha alcanzado el límite superior de Hola de identificadores abiertos simultáneas que se permiten en un archivo.</span><span class="sxs-lookup"><span data-stu-id="7099b-110">You have reached hello upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="7099b-111">Solución</span><span class="sxs-lookup"><span data-stu-id="7099b-111">Solution</span></span>

<span data-ttu-id="7099b-112">Reduzca el número de Hola de identificadores abiertos simultáneos cerrando algunos controladores y, a continuación, vuelva a intentar la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7099b-112">Reduce hello number of concurrent open handles by closing some handles, and then retry hello operation.</span></span> <span data-ttu-id="7099b-113">Para más información, consulte [Lista de comprobación de rendimiento y escalabilidad de Microsoft Azure Storage](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="7099b-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a><span data-ttu-id="7099b-114">Archivo lento copiar tooand de almacenamiento de archivos de Azure en Linux</span><span class="sxs-lookup"><span data-stu-id="7099b-114">Slow file copying tooand from Azure File storage in Linux</span></span>

-   <span data-ttu-id="7099b-115">Si no tiene un requisito específico de tamaño de E/S mínima, se recomienda que utilice 1 MB como Hola tamaño de E/S para un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="7099b-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="7099b-116">Si conocer Hola tamaño final de un archivo que se está ampliando mediante el uso de escritura, y el software no experimenta problemas de compatibilidad cuando una cola no escrita en el archivo hello contiene ceros, a continuación, establecer tamaño de archivo de Hola de antemano en lugar de realizar cada escritura una extensión escritura.</span><span class="sxs-lookup"><span data-stu-id="7099b-116">If you know hello final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="7099b-117">Utilice el método de copia derecho de hello:</span><span class="sxs-lookup"><span data-stu-id="7099b-117">Use hello right copy method:</span></span>
    -   <span data-ttu-id="7099b-118">Use [AzCopy](storage-use-azcopy.md#file-copy) para todas las transferencias entre dos recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="7099b-118">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="7099b-119">Utilice [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre recursos compartidos de archivos y un equipo local.</span><span class="sxs-lookup"><span data-stu-id="7099b-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="7099b-120">"Error de montaje (112): El host está apagado" debido a un tiempo de espera de reconexión</span><span class="sxs-lookup"><span data-stu-id="7099b-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="7099b-121">Se produce un error de montaje "112" en el cliente de Linux Hola al cliente hello ha estado inactiva durante mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="7099b-121">A "112" mount error occurs on hello Linux client when hello client has been idle for a long time.</span></span> <span data-ttu-id="7099b-122">Después de inactividad prolongados, Hola cliente se desconecta y agota el tiempo de espera de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="7099b-122">After extended idle time, hello client disconnects and hello connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="7099b-123">Causa</span><span class="sxs-lookup"><span data-stu-id="7099b-123">Cause</span></span>

<span data-ttu-id="7099b-124">Hola conexión puede estar inactiva para hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="7099b-124">hello connection can be idle for hello following reasons:</span></span>

-   <span data-ttu-id="7099b-125">Errores de comunicación de red que impiden la volviendo a establecer un servidor de toohello de conexión de TCP, cuando se utiliza la opción de montaje "soft" hello predeterminada</span><span class="sxs-lookup"><span data-stu-id="7099b-125">Network communication failures that prevent re-establishing a TCP connection toohello server when hello default “soft” mount option is used</span></span>
-   <span data-ttu-id="7099b-126">Correcciones de reconexión recientes que no están presentes en los kernels anteriores</span><span class="sxs-lookup"><span data-stu-id="7099b-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="7099b-127">Solución</span><span class="sxs-lookup"><span data-stu-id="7099b-127">Solution</span></span>

<span data-ttu-id="7099b-128">Este problema de reconexión en el kernel de Linux Hola se ha corregido como parte del programa Hola siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="7099b-128">This reconnection problem in hello Linux kernel is now fixed as part of hello following changes:</span></span>

- [<span data-ttu-id="7099b-129">Corrección de volver a conectar toonot aplazar la sesión de smb3 volver a conectarse mucho después de volver a conectar de socket</span><span class="sxs-lookup"><span data-stu-id="7099b-129">Fix reconnect toonot defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   <span data-ttu-id="7099b-130">[Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7) (Llamar al servicio de eco inmediatamente después de volver a conectar el socket)</span><span class="sxs-lookup"><span data-stu-id="7099b-130">[Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)</span></span>
-   <span data-ttu-id="7099b-131">[CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b) (CIFS: Corregir un posible daño de memoria durante la reconexión)</span><span class="sxs-lookup"><span data-stu-id="7099b-131">[CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)</span></span>
-   <span data-ttu-id="7099b-132">[CIFS: Fix a possible double locking of mutex during reconnect (or kernel v4.9 and later)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183) (CIFS: Corregir un posible bloqueo doble de exclusión mutua durante la reconexión: para el kernel v4.9 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="7099b-132">[CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)</span></span>

<span data-ttu-id="7099b-133">Sin embargo, no se pueden pasar estos cambios todavía tooall Hola las distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="7099b-133">However, these changes might not be ported yet tooall hello Linux distributions.</span></span> <span data-ttu-id="7099b-134">Esta revisión y otras correcciones de reconexión se realizan en hello después populares kernels de Linux: 4.4.40, 4.8.16 y 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="7099b-134">This fix and other reconnection fixes are made in hello following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="7099b-135">Puede obtener esta revisión mediante la actualización tooone de estas versiones de kernel recomendada.</span><span class="sxs-lookup"><span data-stu-id="7099b-135">You can get this fix by upgrading tooone of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="7099b-136">Solución alternativa</span><span class="sxs-lookup"><span data-stu-id="7099b-136">Workaround</span></span>

<span data-ttu-id="7099b-137">Una solución alternativa para este problema es especificar un montaje forzado.</span><span class="sxs-lookup"><span data-stu-id="7099b-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="7099b-138">Esto fuerza Hola cliente toowait hasta que se establezca una conexión o hasta que se interrumpe explícitamente y puede ser usado tooprevent errores debido a los tiempos de espera de la red.</span><span class="sxs-lookup"><span data-stu-id="7099b-138">This forces hello client toowait until a connection is established or until it’s explicitly interrupted and can be used tooprevent errors because of network time-outs.</span></span> <span data-ttu-id="7099b-139">Sin embargo, esta solución alternativa puede provocar esperas indefinidas.</span><span class="sxs-lookup"><span data-stu-id="7099b-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="7099b-140">Ser conexiones toostop preparada según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7099b-140">Be prepared toostop connections as necessary.</span></span>

<span data-ttu-id="7099b-141">Si no se puede actualizar versiones más recientes de kernel de toohello, puede solucionar este problema manteniendo un archivo en el recurso compartido de archivos de Azure de hello escribir tooevery 30 segundos o menos.</span><span class="sxs-lookup"><span data-stu-id="7099b-141">If you cannot upgrade toohello latest kernel versions, you can work around this problem by keeping a file in hello Azure file share that you write tooevery 30 seconds or less.</span></span> <span data-ttu-id="7099b-142">Debe ser una operación de escritura, como volver a escribir Hola creado o fecha de modificación en el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="7099b-142">This must be a write operation, such as rewriting hello created or modified date on hello file.</span></span> <span data-ttu-id="7099b-143">De lo contrario, podría obtener resultados almacenados en caché y la operación puede desencadenar una reconexión Hola.</span><span class="sxs-lookup"><span data-stu-id="7099b-143">Otherwise, you might get cached results, and your operation might not trigger hello reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="7099b-144">"Error de montaje (115): Operación en curso" cuando monta Azure File Storage mediante SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="7099b-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="7099b-145">Causa</span><span class="sxs-lookup"><span data-stu-id="7099b-145">Cause</span></span>

<span data-ttu-id="7099b-146">Algunas distribuciones de Linux aún no admiten las características de cifrado de SMB 3.0 y los usuarios pueden recibir un mensaje de error "115" si intentan toomount almacenamiento de archivos de Azure mediante SMB 3.0 debido a una característica que falta.</span><span class="sxs-lookup"><span data-stu-id="7099b-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try toomount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="7099b-147">Solución</span><span class="sxs-lookup"><span data-stu-id="7099b-147">Solution</span></span>

<span data-ttu-id="7099b-148">La característica de cifrado de SMB 3.0 para Linux se introdujo en el kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="7099b-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="7099b-149">Esta característica permite el montaje de recursos compartidos de Azure File desde el entorno local o una región distinta de Azure.</span><span class="sxs-lookup"><span data-stu-id="7099b-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="7099b-150">En tiempo de presentación de la publicación, esta funcionalidad ha sido utilizados tooUbuntu 17.04 y Ubuntu 16,10.</span><span class="sxs-lookup"><span data-stu-id="7099b-150">At hello time of publishing, this functionality has been backported tooUbuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="7099b-151">Si el cliente SMB de Linux no admite el cifrado, monte el almacenamiento de archivos de Azure mediante SMB 2.1 desde una VM de Linux de Azure que se encuentra en Hola mismo centro de datos como Hola cuenta de almacenamiento de archivos.</span><span class="sxs-lookup"><span data-stu-id="7099b-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in hello same datacenter as hello File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="7099b-152">Rendimiento lento en un recurso compartido de archivos de Azure montado en una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="7099b-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="7099b-153">Causa</span><span class="sxs-lookup"><span data-stu-id="7099b-153">Cause</span></span>

<span data-ttu-id="7099b-154">Una posible causa de un rendimiento lento es que el almacenamiento en caché está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="7099b-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="7099b-155">Solución</span><span class="sxs-lookup"><span data-stu-id="7099b-155">Solution</span></span>

<span data-ttu-id="7099b-156">toocheck si se deshabilita el almacenamiento en caché, busque hello **caché =** entrada.</span><span class="sxs-lookup"><span data-stu-id="7099b-156">toocheck whether caching is disabled, look for hello **cache=** entry.</span></span> 

<span data-ttu-id="7099b-157">**Cache=none** indica que el almacenamiento en caché está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="7099b-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="7099b-158">Recurso compartido de Hola de montar el volumen mediante el comando de montaje predeterminado de Hola o agregando explícitamente hello **caché = strict** opción toohello montaje comando tooensure esos valores predeterminados de almacenamiento en caché o "strict" modo de almacenamiento en caché está habilitado.</span><span class="sxs-lookup"><span data-stu-id="7099b-158">Remount hello share by using hello default mount command or by explicitly adding hello **cache=strict** option toohello mount command tooensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="7099b-159">En algunos escenarios, Hola **serverino** opción de montaje puede producir hello **ls** stat toorun de comando en cada entrada de directorio.</span><span class="sxs-lookup"><span data-stu-id="7099b-159">In some scenarios, hello **serverino** mount option can cause hello **ls** command toorun stat against every directory entry.</span></span> <span data-ttu-id="7099b-160">Este comportamiento produce una disminución del rendimiento cuando se muestra un listado de un directorio grande.</span><span class="sxs-lookup"><span data-stu-id="7099b-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="7099b-161">Puede comprobar las opciones de montaje de hello su **/etcetera/fstab** entrada:</span><span class="sxs-lookup"><span data-stu-id="7099b-161">You can check hello mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="7099b-162">También puede comprobar si se usan opciones correctas de hello ejecutando hello **sudo montaje | grep cifs** comando y la comprobación de su salida, como la siguiente salida de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7099b-162">You can also check whether hello correct options are being used by running hello  **sudo mount | grep cifs** command and checking its output, such as hello following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="7099b-163">Si hello **caché = strict** o **serverino** opción es no presente, desmontar y volver a montar el almacenamiento de archivos de Azure ejecutando el comando de montaje de Hola de hello [documentación](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7099b-163">If hello **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running hello mount command from hello [documentation](storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="7099b-164">A continuación, volver a comprobar que hello **/etcetera/fstab** entrada tiene opciones correctas de Hola.</span><span class="sxs-lookup"><span data-stu-id="7099b-164">Then, recheck that hello **/etc/fstab** entry has hello correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a><span data-ttu-id="7099b-165">Se perdieron marcas de tiempo en copiar archivos de Windows tooLinux</span><span class="sxs-lookup"><span data-stu-id="7099b-165">Time stamps were lost in copying files from Windows tooLinux</span></span>

<span data-ttu-id="7099b-166">En las plataformas de Unix/Linux, Hola **cp -p** comando produce un error si el archivo 1 y 2 pertenecen a distintos usuarios.</span><span class="sxs-lookup"><span data-stu-id="7099b-166">On Linux/Unix platforms, hello **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="7099b-167">Causa</span><span class="sxs-lookup"><span data-stu-id="7099b-167">Cause</span></span>

<span data-ttu-id="7099b-168">Hola marca force **f** en COPYFILE da como resultado en la ejecución de **cp -p -f** en Unix.</span><span class="sxs-lookup"><span data-stu-id="7099b-168">hello force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="7099b-169">Este comando también se produce un error de marca de tiempo de hello toopreserve del archivo de Hola que no posee.</span><span class="sxs-lookup"><span data-stu-id="7099b-169">This command also fails toopreserve hello time stamp of hello file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="7099b-170">Solución alternativa</span><span class="sxs-lookup"><span data-stu-id="7099b-170">Workaround</span></span>

<span data-ttu-id="7099b-171">Usar el usuario de cuenta de almacenamiento de Hola para copiar archivos de hello:</span><span class="sxs-lookup"><span data-stu-id="7099b-171">Use hello storage account user for copying hello files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="7099b-172">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="7099b-172">Need help?</span></span> <span data-ttu-id="7099b-173">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="7099b-173">Contact support.</span></span>

<span data-ttu-id="7099b-174">Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget resuelva el problema rápidamente.</span><span class="sxs-lookup"><span data-stu-id="7099b-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
