---
title: "Solución de problemas de Azure File Storage en Windows | Microsoft Docs"
description: "Solución de problemas de Azure File Storage en Windows"
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
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: daaf7d0589f5e2d82b43dad879bffd23370a2c81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="d5133-103">Solución de problemas de Azure File Storage en Windows</span><span class="sxs-lookup"><span data-stu-id="d5133-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="d5133-104">En este artículo se enumeran los problemas habituales relacionados con Microsoft Azure File Storage cuando se conecta desde clientes Windows.</span><span class="sxs-lookup"><span data-stu-id="d5133-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="d5133-105">También se proporcionan posibles causas de estos problemas y sus resoluciones.</span><span class="sxs-lookup"><span data-stu-id="d5133-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="d5133-106">Además de los pasos de solución de problemas de este artículo, también puede usar [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) para asegurarse de que el entorno de cliente Windows cumpla los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="d5133-106">In addition to the troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that the Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="d5133-107">AzFileDiagnostics automatiza la detección de la mayoría de los síntomas que se mencionan en este artículo y le ayuda a configurar su entorno para obtener un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="d5133-107">AzFileDiagnostics automates detection of most of the symptoms mentioned in this article and helps set up your environment to get optimal performance.</span></span> <span data-ttu-id="d5133-108">Esta información también se puede encontrar en el [Solucionador de problemas de recursos compartidos de Azure Files](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares), que proporciona los pasos necesarios para ayudarle con problemas relativos la conexión, asignación o montaje de recursos compartidos de Azure Files.</span><span class="sxs-lookup"><span data-stu-id="d5133-108">You can also find this information in the [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps to assist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="d5133-109">Error 53, Error 67 o Error 87 al montar o desmontar un recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="d5133-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="d5133-110">Cuando intenta montar un recurso compartido de archivos desde un entorno local o un centro de datos diferente, es posible que observe los errores siguientes:</span><span class="sxs-lookup"><span data-stu-id="d5133-110">When you try to mount a file share from on-premises or from a different datacenter, you might receive the following errors:</span></span>

- <span data-ttu-id="d5133-111">Error de sistema 53.</span><span class="sxs-lookup"><span data-stu-id="d5133-111">System error 53 has occurred.</span></span> <span data-ttu-id="d5133-112">No se ha encontrado la ruta de acceso de la red.</span><span class="sxs-lookup"><span data-stu-id="d5133-112">The network path was not found.</span></span>
- <span data-ttu-id="d5133-113">Error de sistema 67.</span><span class="sxs-lookup"><span data-stu-id="d5133-113">System error 67 has occurred.</span></span> <span data-ttu-id="d5133-114">No se encuentra el nombre de red especificado.</span><span class="sxs-lookup"><span data-stu-id="d5133-114">The network name cannot be found.</span></span>
- <span data-ttu-id="d5133-115">Error de sistema 87.</span><span class="sxs-lookup"><span data-stu-id="d5133-115">System error 87 has occurred.</span></span> <span data-ttu-id="d5133-116">El parámetro no es correcto.</span><span class="sxs-lookup"><span data-stu-id="d5133-116">The parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="d5133-117">Causa 1: Canal de comunicación sin cifrar</span><span class="sxs-lookup"><span data-stu-id="d5133-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="d5133-118">Por seguridad, se bloquean las conexiones a recursos compartidos de archivos de Azure si no el canal de comunicación no está cifrado y si el intento de conexión no se realiza desde el mismo centro de datos donde residen los recursos compartidos de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5133-118">For security reasons, connections to Azure file shares are blocked if the communication channel isn’t encrypted and if the connection attempt isn't made from the same datacenter where the Azure file shares reside.</span></span> <span data-ttu-id="d5133-119">Se proporciona el cifrado del canal de comunicación solamente si el sistema operativo cliente del usuario admite el cifrado SMB.</span><span class="sxs-lookup"><span data-stu-id="d5133-119">Communication channel encryption is provided only if the user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="d5133-120">Windows 8, Windows Server 2012 y versiones posteriores de cada sistema negocian solicitudes que incluyen SMB 3.0, que es compatible con el cifrado.</span><span class="sxs-lookup"><span data-stu-id="d5133-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="d5133-121">Solución para la causa 1</span><span class="sxs-lookup"><span data-stu-id="d5133-121">Solution for cause 1</span></span>

<span data-ttu-id="d5133-122">Conéctese desde un cliente que satisfaga uno de los requisitos siguientes:</span><span class="sxs-lookup"><span data-stu-id="d5133-122">Connect from a client that does one of the following:</span></span>

- <span data-ttu-id="d5133-123">Cumple los requisitos de Windows 8 y Windows Server 2012 o versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="d5133-123">Meets the requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="d5133-124">Se conecta desde una máquina virtual en el mismo centro de datos que la cuenta de almacenamiento de Azure que se usa para el recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="d5133-124">Connects from a virtual machine in the same datacenter as the Azure storage account that is used for the Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="d5133-125">Causa 2: Puerto 445 bloqueado</span><span class="sxs-lookup"><span data-stu-id="d5133-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="d5133-126">Los errores del sistema 53 o 67 pueden producirse si se bloquea la comunicación de salida del puerto 445 a un centro de datos de Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="d5133-126">System error 53 or system error 67 can occur if port 445 outbound communication to an Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="d5133-127">Para ver el resumen de los ISP que permiten o deniegan el acceso desde el puerto 445, visite [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5133-127">To see the summary of ISPs that allow or disallow access from port 445, go to [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="d5133-128">Para descubrir si este es el motivo del mensaje "Error de sistema 53", puede usar Portqry para enviar una consulta al punto de conexión TCP:445.</span><span class="sxs-lookup"><span data-stu-id="d5133-128">To understand whether this is the reason behind the "System error 53" message, you can use Portqry to query the TCP:445 endpoint.</span></span> <span data-ttu-id="d5133-129">Si el punto de conexión TCP:445 se muestra como filtrado, eso quiere decir que el puerto TCP está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="d5133-129">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span></span> <span data-ttu-id="d5133-130">Aquí se muestra una consulta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d5133-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="d5133-131">Si el puerto TCP 445 está bloqueado por una regla a lo largo de la ruta de acceso de red, verá la siguiente salida:</span><span class="sxs-lookup"><span data-stu-id="d5133-131">If TCP port 445 is blocked by a rule along the network path, you will see the following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="d5133-132">Para más información sobre el uso de Portqry, consulte [Descripción de la utilidad de línea de comandos Portqry.exe](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="d5133-132">For more information about how to use Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="d5133-133">Solución para la causa 2</span><span class="sxs-lookup"><span data-stu-id="d5133-133">Solution for cause 2</span></span>

<span data-ttu-id="d5133-134">Colabore con su departamento de TI para abrir el puerto 445, de modo que acepte las conexiones salientes a los [intervalos de IP de Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="d5133-134">Work with your IT department to open port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="d5133-135">Causa 3: NTLMv1 habilitado</span><span class="sxs-lookup"><span data-stu-id="d5133-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="d5133-136">También se producen los errores del sistema 53 u 87 si se ha habilitado la comunicación NTLMv1 en el cliente.</span><span class="sxs-lookup"><span data-stu-id="d5133-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on the client.</span></span> <span data-ttu-id="d5133-137">Azure File Storage solo admite la autenticación NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="d5133-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="d5133-138">Si se habilita NTLMv1, el cliente será menos seguro.</span><span class="sxs-lookup"><span data-stu-id="d5133-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="d5133-139">Por lo tanto, se bloquea la comunicación con Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="d5133-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="d5133-140">Para determinar si esta es la causa del error, averigüe si la siguiente subclave del Registro está establecida en el valor 3:</span><span class="sxs-lookup"><span data-stu-id="d5133-140">To determine whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span></span>

<span data-ttu-id="d5133-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="d5133-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="d5133-142">Para obtener más información, consulte el tema [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) en TechNet.</span><span class="sxs-lookup"><span data-stu-id="d5133-142">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="d5133-143">Solución para la causa 3</span><span class="sxs-lookup"><span data-stu-id="d5133-143">Solution for cause 3</span></span>

<span data-ttu-id="d5133-144">Revierta el valor **LmCompatibilityLevel** al predeterminado, 3, en la siguiente subclave del Registro:</span><span class="sxs-lookup"><span data-stu-id="d5133-144">Revert the **LmCompatibilityLevel** value to the default value of 3 in the following registry subkey:</span></span>

  <span data-ttu-id="d5133-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="d5133-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-to-process-this-command-when-you-copy-to-an-azure-file-share"></a><span data-ttu-id="d5133-146">Error 1816 "Cuota insuficiente para procesar este comando" cuando se copia a un recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="d5133-146">Error 1816 “Not enough quota is available to process this command” when you copy to an Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="d5133-147">Causa</span><span class="sxs-lookup"><span data-stu-id="d5133-147">Cause</span></span>

<span data-ttu-id="d5133-148">El error 1816 se produce cuando se alcanza el límite superior de identificadores abiertos simultáneos que se permiten para un archivo en el equipo donde se está montando el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="d5133-148">Error 1816 happens when you reach the upper limit of concurrent open handles that are allowed for a file on the computer where the file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="d5133-149">Solución</span><span class="sxs-lookup"><span data-stu-id="d5133-149">Solution</span></span>

<span data-ttu-id="d5133-150">Reduzca el número de identificadores abiertos simultáneos cerrando algunos de ellos y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="d5133-150">Reduce the number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="d5133-151">Para más información, consulte [Lista de comprobación de rendimiento y escalabilidad de Microsoft Azure Storage](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d5133-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-windows"></a><span data-ttu-id="d5133-152">Lentitud al copiar archivos en Azure File Storage y desde él en Windows</span><span class="sxs-lookup"><span data-stu-id="d5133-152">Slow file copying to and from Azure File storage in Windows</span></span>

<span data-ttu-id="d5133-153">Puede que experimente un rendimiento lento cuando intente transferir archivos al servicio Azure Files.</span><span class="sxs-lookup"><span data-stu-id="d5133-153">You might see slow performance when you try to transfer files to the Azure File service.</span></span>

- <span data-ttu-id="d5133-154">Si no tiene un requisito mínimo de tamaño de E/S específico, se recomienda que utilice 1 MB como el tamaño de E/S para disfrutar de un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="d5133-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="d5133-155">Si conoce el tamaño final de un archivo que está ampliando mediante operaciones de escritura y el software no presenta problemas de compatibilidad cuando la cola no escrita del archivo contiene ceros, establezca el tamaño de archivo con antelación en lugar de hacer que cada escritura sea una escritura de ampliación.</span><span class="sxs-lookup"><span data-stu-id="d5133-155">If you know the final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when the unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="d5133-156">Utilice el método de copia correcto:</span><span class="sxs-lookup"><span data-stu-id="d5133-156">Use the right copy method:</span></span>
    -   <span data-ttu-id="d5133-157">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) para todas las transferencias entre dos recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="d5133-157">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="d5133-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre recursos compartidos de archivos en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="d5133-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="d5133-159">Consideraciones para Windows 8.1 o Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d5133-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="d5133-160">En el caso de los clientes que ejecutan Windows 8.1 o Windows Server 2012 R2, asegúrese de que la revisión [KB3114025](https://support.microsoft.com/help/3114025) esté instalada.</span><span class="sxs-lookup"><span data-stu-id="d5133-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that the [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="d5133-161">Esta revisión mejora el rendimiento de la creación y el cierre de identificadores.</span><span class="sxs-lookup"><span data-stu-id="d5133-161">This hotfix improves the performance of create and close handles.</span></span>

<span data-ttu-id="d5133-162">Puede ejecutar el siguiente script para comprobar si se ha instalado la revisión:</span><span class="sxs-lookup"><span data-stu-id="d5133-162">You can run the following script to check whether the hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="d5133-163">Si la revisión está instalada, se muestra el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="d5133-163">If hotfix is installed, the following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="d5133-164">Las imágenes de Windows Server 2012 R2 de Azure Marketplace tienen la revisión KB3114025 instalada de manera predeterminada desde diciembre de 2015.</span><span class="sxs-lookup"><span data-stu-id="d5133-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="d5133-165">No hay ninguna carpeta con una letra de unidad en **Mi PC**</span><span class="sxs-lookup"><span data-stu-id="d5133-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="d5133-166">Si asigna un recurso compartido de archivos de Azure como administrador mediante net use, el recurso compartido parece que falta.</span><span class="sxs-lookup"><span data-stu-id="d5133-166">If you map an Azure file share as an administrator by using net use, the share appears to be missing.</span></span>

### <a name="cause"></a><span data-ttu-id="d5133-167">Causa</span><span class="sxs-lookup"><span data-stu-id="d5133-167">Cause</span></span>

<span data-ttu-id="d5133-168">De manera predeterminada, el Explorador de archivos de Windows no se ejecuta como administrador.</span><span class="sxs-lookup"><span data-stu-id="d5133-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="d5133-169">Si se ejecuta net use desde un símbolo del sistema de administrador, la unidad de red se asigna como administrador.</span><span class="sxs-lookup"><span data-stu-id="d5133-169">If you run net use from an administrative command prompt, you map the network drive as an administrator.</span></span> <span data-ttu-id="d5133-170">Dado que las unidades asignadas son específicas para los usuarios, la cuenta de usuario con la que se haya iniciado sesión no mostrará las unidades si estas se han montado con una cuenta de usuario distinta.</span><span class="sxs-lookup"><span data-stu-id="d5133-170">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="d5133-171">Solución</span><span class="sxs-lookup"><span data-stu-id="d5133-171">Solution</span></span>
<span data-ttu-id="d5133-172">Monte el recurso compartido desde una línea de comandos que no sea de administrador.</span><span class="sxs-lookup"><span data-stu-id="d5133-172">Mount the share from a non-administrator command line.</span></span> <span data-ttu-id="d5133-173">Como alternativa, puede seguir las instrucciones de [este tema de TechNet](https://technet.microsoft.com/library/ee844140.aspx) para configurar el valor del Registro **EnableLinkedConnections**.</span><span class="sxs-lookup"><span data-stu-id="d5133-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-the-storage-account-contains-a-forward-slash"></a><span data-ttu-id="d5133-174">Se produce un error en el comando net use si la cuenta de almacenamiento contiene una barra diagonal</span><span class="sxs-lookup"><span data-stu-id="d5133-174">Net use command fails if the storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="d5133-175">Causa</span><span class="sxs-lookup"><span data-stu-id="d5133-175">Cause</span></span>

<span data-ttu-id="d5133-176">El comando net use interpreta la barra diagonal (/) como una opción de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d5133-176">The net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="d5133-177">Si el nombre de la cuenta de usuario comienza por una barra diagonal, se produce un error en la asignación de unidad.</span><span class="sxs-lookup"><span data-stu-id="d5133-177">If your user account name starts with a forward slash, the drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="d5133-178">Solución</span><span class="sxs-lookup"><span data-stu-id="d5133-178">Solution</span></span>

<span data-ttu-id="d5133-179">Puede utilizar cualquiera de los siguientes pasos para solucionar el problema:</span><span class="sxs-lookup"><span data-stu-id="d5133-179">You can use either of the following steps to work around the problem:</span></span>

- <span data-ttu-id="d5133-180">Ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d5133-180">Run the following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="d5133-181">Desde un archivo por lotes, puede ejecutar el comando de este modo:</span><span class="sxs-lookup"><span data-stu-id="d5133-181">From a batch file, you can run the command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="d5133-182">Encierre la clave entre comillas dobles para solucionar el problema, a menos que la barra diagonal sea el primer carácter.</span><span class="sxs-lookup"><span data-stu-id="d5133-182">Put double quotation marks around the key to work around this problem--unless the forward slash is the first character.</span></span> <span data-ttu-id="d5133-183">En ese caso, use el modo interactivo y escriba la contraseña por separado o vuelva a generar las claves para obtener una que no empiece por barra diagonal.</span><span class="sxs-lookup"><span data-stu-id="d5133-183">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="d5133-184">La aplicación o el servicio no puede acceder a una unidad de Azure File Storage montada</span><span class="sxs-lookup"><span data-stu-id="d5133-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="d5133-185">Causa</span><span class="sxs-lookup"><span data-stu-id="d5133-185">Cause</span></span>

<span data-ttu-id="d5133-186">Las unidades se montan para usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="d5133-186">Drives are mounted per user.</span></span> <span data-ttu-id="d5133-187">Si su aplicación o servicio se ejecuta con una cuenta de usuario diferente a la que montó la unidad, la aplicación no verá la unidad.</span><span class="sxs-lookup"><span data-stu-id="d5133-187">If your application or service is running under a different user account than the one that mounted the drive, the application will not see the drive.</span></span>

### <a name="solution"></a><span data-ttu-id="d5133-188">Solución</span><span class="sxs-lookup"><span data-stu-id="d5133-188">Solution</span></span>

<span data-ttu-id="d5133-189">Use una de las soluciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="d5133-189">Use one of the following solutions:</span></span>

-   <span data-ttu-id="d5133-190">Monte la unidad desde la misma cuenta de usuario que contiene la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d5133-190">Mount the drive from the same user account that contains the application.</span></span> <span data-ttu-id="d5133-191">Puede usar una herramienta como PsExec.</span><span class="sxs-lookup"><span data-stu-id="d5133-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="d5133-192">Pase el nombre y la clave de la cuenta de almacenamiento en los parámetros de nombre de usuario y contraseña del comando net use.</span><span class="sxs-lookup"><span data-stu-id="d5133-192">Pass the storage account name and key in the user name and password parameters of the net use command.</span></span>

<span data-ttu-id="d5133-193">Después de seguir estas instrucciones, podría recibir el mensaje de error siguiente cuando ejecute net use para la cuenta de servicio de red o del sistema: "Error de sistema 1312.</span><span class="sxs-lookup"><span data-stu-id="d5133-193">After you follow these instructions, you might receive the following error message when you run net use for the system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="d5133-194">Una sesión de inicio especificada no existe.</span><span class="sxs-lookup"><span data-stu-id="d5133-194">A specified logon session does not exist.</span></span> <span data-ttu-id="d5133-195">Es posible que haya finalizado."</span><span class="sxs-lookup"><span data-stu-id="d5133-195">It may already have been terminated."</span></span> <span data-ttu-id="d5133-196">En este caso, asegúrese de que el nombre de usuario pasado a net use incluya la información de dominio (por ejemplo, "[nombre de la cuenta de almacenamiento].file.core.windows.net").</span><span class="sxs-lookup"><span data-stu-id="d5133-196">If this occurs, make sure that the username that is passed to net use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-to-a-destination-that-does-not-support-encryption"></a><span data-ttu-id="d5133-197">Error "El archivo se va a copiar a un destino que no es compatible con el cifrado"</span><span class="sxs-lookup"><span data-stu-id="d5133-197">Error "You are copying a file to a destination that does not support encryption"</span></span>

<span data-ttu-id="d5133-198">Cuando se copia un archivo a través de la red, el archivo se descifra en el equipo de origen, se transmite en texto no cifrado y se vuelve a cifrar en el destino.</span><span class="sxs-lookup"><span data-stu-id="d5133-198">When a file is copied over the network, the file is decrypted on the source computer, transmitted in plaintext, and re-encrypted at the destination.</span></span> <span data-ttu-id="d5133-199">Sin embargo, es posible que vea el siguiente error cuando intente copiar un archivo cifrado: "El archivo se va a copiar a un destino que no es compatible con el cifrado."</span><span class="sxs-lookup"><span data-stu-id="d5133-199">However, you might see the following error when you're trying to copy an encrypted file: "You are copying the file to a destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="d5133-200">Causa</span><span class="sxs-lookup"><span data-stu-id="d5133-200">Cause</span></span>
<span data-ttu-id="d5133-201">Este problema puede producirse si está usando Sistema de cifrado de archivos (EFS).</span><span class="sxs-lookup"><span data-stu-id="d5133-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="d5133-202">Es posible copiar archivos cifrados con BitLocker en Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="d5133-202">BitLocker-encrypted files can be copied to Azure File storage.</span></span> <span data-ttu-id="d5133-203">Sin embargo, Azure File Storage no admite NTFS EFS.</span><span class="sxs-lookup"><span data-stu-id="d5133-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="d5133-204">Solución alternativa</span><span class="sxs-lookup"><span data-stu-id="d5133-204">Workaround</span></span>
<span data-ttu-id="d5133-205">Para copiar un archivo a través de la red, primero debe descifrarlo.</span><span class="sxs-lookup"><span data-stu-id="d5133-205">To copy a file over the network, you must first decrypt it.</span></span> <span data-ttu-id="d5133-206">Use uno de los siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="d5133-206">Use one of the following methods:</span></span>

- <span data-ttu-id="d5133-207">Use el comando **copy /d**.</span><span class="sxs-lookup"><span data-stu-id="d5133-207">Use the **copy /d** command.</span></span> <span data-ttu-id="d5133-208">Permite que los archivos cifrados se guarden como archivos descifrados en el destino.</span><span class="sxs-lookup"><span data-stu-id="d5133-208">It allows the encrypted files to be saved as decrypted files at the destination.</span></span>
- <span data-ttu-id="d5133-209">Establezca la siguiente clave del Registro:</span><span class="sxs-lookup"><span data-stu-id="d5133-209">Set the following registry key:</span></span>
  - <span data-ttu-id="d5133-210">Ruta de acceso = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="d5133-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="d5133-211">Tipo de valor = DWORD</span><span class="sxs-lookup"><span data-stu-id="d5133-211">Value type = DWORD</span></span>
  - <span data-ttu-id="d5133-212">Nombre = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="d5133-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="d5133-213">Valor = 1</span><span class="sxs-lookup"><span data-stu-id="d5133-213">Value = 1</span></span>

<span data-ttu-id="d5133-214">Tenga en cuenta que la configuración de la clave del Registro afecta a todas las operaciones de copia llevadas a cabo en recursos compartidos de red.</span><span class="sxs-lookup"><span data-stu-id="d5133-214">Be aware that setting the registry key affects all copy operations that are made to network shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="d5133-215">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="d5133-215">Need help?</span></span> <span data-ttu-id="d5133-216">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="d5133-216">Contact support.</span></span>
<span data-ttu-id="d5133-217">Si sigue necesitando ayuda, [póngase en contacto con el soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver el problema rápidamente.</span><span class="sxs-lookup"><span data-stu-id="d5133-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
