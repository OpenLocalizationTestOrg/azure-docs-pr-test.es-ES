---
title: problemas de almacenamiento de archivos de Azure aaaTroubleshoot en Windows | Documentos de Microsoft
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
ms.openlocfilehash: ba0315d1add76a27fec93a9aee3aa99ccb7fa164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="70dc2-103">Solución de problemas de Azure File Storage en Windows</span><span class="sxs-lookup"><span data-stu-id="70dc2-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="70dc2-104">Este artículo enumeran los problemas comunes que están relacionado tooMicrosoft almacenamiento de archivos de Azure cuando se conecta desde los clientes de Windows.</span><span class="sxs-lookup"><span data-stu-id="70dc2-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="70dc2-105">También se proporcionan posibles causas de estos problemas y sus resoluciones.</span><span class="sxs-lookup"><span data-stu-id="70dc2-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="70dc2-106">Además de solución de problemas de toohello los pasos en este artículo, también puede usar [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) para asegurarse de que Windows hello entorno de cliente tiene requisitos previos correcta.</span><span class="sxs-lookup"><span data-stu-id="70dc2-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="70dc2-107">AzFileDiagnostics automatiza la detección de la mayoría de los síntomas de Hola que se mencionan en este artículo y le ayuda a configurar su entorno tooget un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="70dc2-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="70dc2-108">También puede encontrar esta información en hello [Solucionador de problemas de recursos compartidos de archivos de Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) que proporciona pasos tooassist con problemas comparte archivos de Azure de conectarse, asignación/montaje.</span><span class="sxs-lookup"><span data-stu-id="70dc2-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="70dc2-109">Error 53, Error 67 o Error 87 al montar o desmontar un recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="70dc2-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="70dc2-110">Cuando intente toomount un archivo de recurso compartido desde el entorno local o desde otro centro de datos, podría recibir Hola siguientes errores:</span><span class="sxs-lookup"><span data-stu-id="70dc2-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="70dc2-111">Error de sistema 53.</span><span class="sxs-lookup"><span data-stu-id="70dc2-111">System error 53 has occurred.</span></span> <span data-ttu-id="70dc2-112">no se encontró la ruta de acceso de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="70dc2-112">hello network path was not found.</span></span>
- <span data-ttu-id="70dc2-113">Error de sistema 67.</span><span class="sxs-lookup"><span data-stu-id="70dc2-113">System error 67 has occurred.</span></span> <span data-ttu-id="70dc2-114">no se encuentra el nombre de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="70dc2-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="70dc2-115">Error de sistema 87.</span><span class="sxs-lookup"><span data-stu-id="70dc2-115">System error 87 has occurred.</span></span> <span data-ttu-id="70dc2-116">Hola parámetro es incorrecto.</span><span class="sxs-lookup"><span data-stu-id="70dc2-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="70dc2-117">Causa 1: Canal de comunicación sin cifrar</span><span class="sxs-lookup"><span data-stu-id="70dc2-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="70dc2-118">Por motivos de seguridad, las conexiones se bloquean recursos compartidos de archivos de tooAzure si no se cifra canal de comunicación de Hola y si no está realizando el intento de conexión de Hola de Hola mismo centro de datos donde residen los recursos compartidos de archivos de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="70dc2-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="70dc2-119">Proporciona el cifrado de canal de comunicación únicamente si el sistema operativo de cliente del usuario de hello es compatible con el cifrado SMB.</span><span class="sxs-lookup"><span data-stu-id="70dc2-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="70dc2-120">Windows 8, Windows Server 2012 y versiones posteriores de cada sistema negocian solicitudes que incluyen SMB 3.0, que es compatible con el cifrado.</span><span class="sxs-lookup"><span data-stu-id="70dc2-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="70dc2-121">Solución para la causa 1</span><span class="sxs-lookup"><span data-stu-id="70dc2-121">Solution for cause 1</span></span>

<span data-ttu-id="70dc2-122">Conectarse desde un cliente que realiza una de las siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="70dc2-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="70dc2-123">Hola cumple los requisitos de Windows 8 y Windows Server 2012 o versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="70dc2-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="70dc2-124">Se conecta desde una máquina virtual en hello mismo centro de datos como Hola cuenta de almacenamiento de Azure que se usa para el recurso compartido de archivos de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="70dc2-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="70dc2-125">Causa 2: Puerto 445 bloqueado</span><span class="sxs-lookup"><span data-stu-id="70dc2-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="70dc2-126">Error del sistema 53 o error del sistema 67 puede producirse si se ha bloqueado el puerto 445 comunicación saliente tooan archivos de Azure almacenamiento centro de datos.</span><span class="sxs-lookup"><span data-stu-id="70dc2-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="70dc2-127">Resumen de hello toosee de ISP que permitir o denegar el acceso desde el puerto 445, vaya demasiado[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="70dc2-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="70dc2-128">toounderstand si ésta es la razón de hello detrás de mensaje de bienvenida de "Error del sistema 53", puede utilizar el punto de conexión de Portqry tooquery hello TCP:445.</span><span class="sxs-lookup"><span data-stu-id="70dc2-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="70dc2-129">Si el punto de conexión de hello TCP:445 se muestra como filtrados, Hola el puerto TCP está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="70dc2-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="70dc2-130">Aquí se muestra una consulta de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="70dc2-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="70dc2-131">Si el puerto TCP 445 está bloqueado por una regla a lo largo de la ruta de acceso de red de hello, verá Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="70dc2-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="70dc2-132">Para obtener más información acerca de cómo toouse Portqry, consulte [descripción de la utilidad de línea de comandos Portqry.exe de hello](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="70dc2-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="70dc2-133">Solución para la causa 2</span><span class="sxs-lookup"><span data-stu-id="70dc2-133">Solution for cause 2</span></span>

<span data-ttu-id="70dc2-134">Trabajar con el puerto de tooopen del departamento de TI 445 saliente demasiado[intervalos de direcciones IP de Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="70dc2-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="70dc2-135">Causa 3: NTLMv1 habilitado</span><span class="sxs-lookup"><span data-stu-id="70dc2-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="70dc2-136">Error del sistema 53 o error del sistema 87 puede producirse si se habilita la comunicación de NTLMv1 en cliente Hola.</span><span class="sxs-lookup"><span data-stu-id="70dc2-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="70dc2-137">Azure File Storage solo admite la autenticación NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="70dc2-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="70dc2-138">Si se habilita NTLMv1, el cliente será menos seguro.</span><span class="sxs-lookup"><span data-stu-id="70dc2-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="70dc2-139">Por lo tanto, se bloquea la comunicación con Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="70dc2-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="70dc2-140">toodetermine si ésta es Hola causa del error de hello, compruebe que hello en la siguiente subclave del registro está establecido el valor de tooa de 3:</span><span class="sxs-lookup"><span data-stu-id="70dc2-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="70dc2-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa &gt; LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="70dc2-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="70dc2-142">Para obtener más información, vea hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) tema en TechNet.</span><span class="sxs-lookup"><span data-stu-id="70dc2-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="70dc2-143">Solución para la causa 3</span><span class="sxs-lookup"><span data-stu-id="70dc2-143">Solution for cause 3</span></span>

<span data-ttu-id="70dc2-144">Revertir hello **LmCompatibilityLevel** valor toohello el valor de 3 en la siguiente subclave del registro de hello:</span><span class="sxs-lookup"><span data-stu-id="70dc2-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="70dc2-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="70dc2-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="70dc2-146">Error 1816 "no hay suficiente cuota está disponible tooprocess este comando" al copiar recurso compartido de archivos de Azure de tooan</span><span class="sxs-lookup"><span data-stu-id="70dc2-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="70dc2-147">Causa</span><span class="sxs-lookup"><span data-stu-id="70dc2-147">Cause</span></span>

<span data-ttu-id="70dc2-148">Error 1816 se produce cuando se alcanza el límite superior de Hola de identificadores abiertos simultáneas que se permiten en un archivo en el equipo de Hola donde se está montado el recurso compartido de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="70dc2-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="70dc2-149">Solución</span><span class="sxs-lookup"><span data-stu-id="70dc2-149">Solution</span></span>

<span data-ttu-id="70dc2-150">Reduzca el número de Hola de simultáneos identificadores abiertos por cerrar algunos identificadores y, a continuación, vuelva a intentar.</span><span class="sxs-lookup"><span data-stu-id="70dc2-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="70dc2-151">Para más información, consulte [Lista de comprobación de rendimiento y escalabilidad de Microsoft Azure Storage](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="70dc2-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="70dc2-152">Archivo lento copiar tooand de almacenamiento de archivos de Azure en Windows</span><span class="sxs-lookup"><span data-stu-id="70dc2-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="70dc2-153">Puede que vea un rendimiento lento cuando intente tootransfer archivos toohello servicio archivo de Azure.</span><span class="sxs-lookup"><span data-stu-id="70dc2-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="70dc2-154">Si no tiene un requisito específico de tamaño de E/S mínima, se recomienda que utilice 1 MB como Hola tamaño de E/S para un rendimiento óptimo.</span><span class="sxs-lookup"><span data-stu-id="70dc2-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="70dc2-155">Si conoce tamaño final de Hola de un archivo que está ampliando con escribe y el software no tiene problemas de compatibilidad al final no escrito en el archivo hello hello contiene ceros, a continuación, conjunto Hola tamaño del archivo de antemano en lugar de realizar una escritura de ampliación de cada escritura.</span><span class="sxs-lookup"><span data-stu-id="70dc2-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="70dc2-156">Utilice el método de copia derecho de hello:</span><span class="sxs-lookup"><span data-stu-id="70dc2-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="70dc2-157">Use [AzCopy](storage-use-azcopy.md#file-copy) para todas las transferencias entre dos recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="70dc2-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="70dc2-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre recursos compartidos de archivos en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="70dc2-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="70dc2-159">Consideraciones para Windows 8.1 o Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="70dc2-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="70dc2-160">Para los clientes que ejecutan Windows 8.1 o Windows Server 2012 R2, asegúrese de que ese hello [KB3114025](https://support.microsoft.com/help/3114025) revisión esté instalada.</span><span class="sxs-lookup"><span data-stu-id="70dc2-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="70dc2-161">Esta revisión mejora el rendimiento de Hola de crear y cerrar identificadores.</span><span class="sxs-lookup"><span data-stu-id="70dc2-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="70dc2-162">Puede ejecutar Hola después script toocheck si se ha instalado la revisión de hello:</span><span class="sxs-lookup"><span data-stu-id="70dc2-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="70dc2-163">Si está instalada la revisión, hello resultado siguiente se muestra:</span><span class="sxs-lookup"><span data-stu-id="70dc2-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="70dc2-164">Las imágenes de Windows Server 2012 R2 de Azure Marketplace tienen la revisión KB3114025 instalada de manera predeterminada desde diciembre de 2015.</span><span class="sxs-lookup"><span data-stu-id="70dc2-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="70dc2-165">No hay ninguna carpeta con una letra de unidad en **Mi PC**</span><span class="sxs-lookup"><span data-stu-id="70dc2-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="70dc2-166">Si asigna un recurso compartido de archivos de Azure como administrador mediante el uso de net use, el recurso compartido de hello aparece toobe falta.</span><span class="sxs-lookup"><span data-stu-id="70dc2-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="70dc2-167">Causa</span><span class="sxs-lookup"><span data-stu-id="70dc2-167">Cause</span></span>

<span data-ttu-id="70dc2-168">De manera predeterminada, el Explorador de archivos de Windows no se ejecuta como administrador.</span><span class="sxs-lookup"><span data-stu-id="70dc2-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="70dc2-169">Si ejecuta net use desde un símbolo del sistema administrativo, asignar unidad de red de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="70dc2-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="70dc2-170">Dado que las unidades asignadas son centrado en el usuario, cuenta de usuario de Hola que se registra en no muestra las unidades de hello si se montan en una cuenta de usuario diferente.</span><span class="sxs-lookup"><span data-stu-id="70dc2-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="70dc2-171">Solución</span><span class="sxs-lookup"><span data-stu-id="70dc2-171">Solution</span></span>
<span data-ttu-id="70dc2-172">Monte el recurso compartido de Hola desde una línea de comandos sin privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="70dc2-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="70dc2-173">Como alternativa, puede seguir [en este tema de TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** valor del registro.</span><span class="sxs-lookup"><span data-stu-id="70dc2-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="70dc2-174">Se produce un error en el comando NET use si la cuenta de almacenamiento de hello contiene una barra diagonal</span><span class="sxs-lookup"><span data-stu-id="70dc2-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="70dc2-175">Causa</span><span class="sxs-lookup"><span data-stu-id="70dc2-175">Cause</span></span>

<span data-ttu-id="70dc2-176">comando de net use Hola interpreta una barra diagonal (/) como una opción de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="70dc2-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="70dc2-177">Si el nombre de cuenta de usuario comienza con una barra diagonal, se produce un error en la asignación de unidades de Hola.</span><span class="sxs-lookup"><span data-stu-id="70dc2-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="70dc2-178">Solución</span><span class="sxs-lookup"><span data-stu-id="70dc2-178">Solution</span></span>

<span data-ttu-id="70dc2-179">Puede utilizar cualquiera de hello siguiendo los pasos toowork problema hello:</span><span class="sxs-lookup"><span data-stu-id="70dc2-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="70dc2-180">Ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="70dc2-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="70dc2-181">Desde un archivo por lotes, puede ejecutar comandos de hello así:</span><span class="sxs-lookup"><span data-stu-id="70dc2-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="70dc2-182">Colocar comillas dobles alrededor de hello toowork clave alternativa para este problema, a menos que coincide con barra diagonal Hola Hola primer carácter.</span><span class="sxs-lookup"><span data-stu-id="70dc2-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="70dc2-183">Si es así, use el modo interactivo de Hola y escriba la contraseña por separado o volver a generar el tooget claves una clave que no se inicia con una barra diagonal.</span><span class="sxs-lookup"><span data-stu-id="70dc2-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="70dc2-184">La aplicación o el servicio no puede acceder a una unidad de Azure File Storage montada</span><span class="sxs-lookup"><span data-stu-id="70dc2-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="70dc2-185">Causa</span><span class="sxs-lookup"><span data-stu-id="70dc2-185">Cause</span></span>

<span data-ttu-id="70dc2-186">Las unidades se montan para usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="70dc2-186">Drives are mounted per user.</span></span> <span data-ttu-id="70dc2-187">Si su aplicación o servicio se ejecuta bajo una cuenta de usuario diferente de Hola que Hola unidad montada, aplicación hello no podrán ver la unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="70dc2-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="70dc2-188">Solución</span><span class="sxs-lookup"><span data-stu-id="70dc2-188">Solution</span></span>

<span data-ttu-id="70dc2-189">Use uno de hello siguientes soluciones:</span><span class="sxs-lookup"><span data-stu-id="70dc2-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="70dc2-190">Monte la unidad de Hola de hello misma cuenta de usuario que contiene la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="70dc2-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="70dc2-191">Puede usar una herramienta como PsExec.</span><span class="sxs-lookup"><span data-stu-id="70dc2-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="70dc2-192">Pasar el nombre de cuenta de almacenamiento de Hola y la clave en los parámetros de nombre y la contraseña de usuario Hola de comando de net use Hola.</span><span class="sxs-lookup"><span data-stu-id="70dc2-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="70dc2-193">Después de seguir estas instrucciones, es posible que reciba Hola mensaje de error siguiente cuando ejecute net use para la cuenta de servicio de red o sistema de hello: "1312 error del sistema.</span><span class="sxs-lookup"><span data-stu-id="70dc2-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="70dc2-194">Una sesión de inicio especificada no existe.</span><span class="sxs-lookup"><span data-stu-id="70dc2-194">A specified logon session does not exist.</span></span> <span data-ttu-id="70dc2-195">Es posible que haya finalizado."</span><span class="sxs-lookup"><span data-stu-id="70dc2-195">It may already have been terminated."</span></span> <span data-ttu-id="70dc2-196">Si esto ocurre, asegúrese de que ese nombre de usuario de Hola que se pasa el uso de toonet incluye información de dominio (por ejemplo: "[nombre de cuenta de almacenamiento]. file.core.windows. NET").</span><span class="sxs-lookup"><span data-stu-id="70dc2-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="70dc2-197">Error "Va a copiar un archivo de destino tooa que no admite el cifrado"</span><span class="sxs-lookup"><span data-stu-id="70dc2-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="70dc2-198">Cuando se copia un archivo a través de red de hello, archivo hello se descifra en equipo de origen de hello, transmiten en texto sin formato y vuelve a cifrar en el destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="70dc2-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="70dc2-199">Sin embargo, podría ver Hola tras error al que está tratando de toocopy un archivo cifrado: ", copia Hola archivo tooa destino que no admite el cifrado."</span><span class="sxs-lookup"><span data-stu-id="70dc2-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="70dc2-200">Causa</span><span class="sxs-lookup"><span data-stu-id="70dc2-200">Cause</span></span>
<span data-ttu-id="70dc2-201">Este problema puede producirse si está usando Sistema de cifrado de archivos (EFS).</span><span class="sxs-lookup"><span data-stu-id="70dc2-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="70dc2-202">Archivos cifrados mediante BitLocker pueden ser almacenamiento de archivos copiados tooAzure.</span><span class="sxs-lookup"><span data-stu-id="70dc2-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="70dc2-203">Sin embargo, Azure File Storage no admite NTFS EFS.</span><span class="sxs-lookup"><span data-stu-id="70dc2-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="70dc2-204">Solución alternativa</span><span class="sxs-lookup"><span data-stu-id="70dc2-204">Workaround</span></span>
<span data-ttu-id="70dc2-205">toocopy un archivo a través de red de hello, deberá descifrarlo.</span><span class="sxs-lookup"><span data-stu-id="70dc2-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="70dc2-206">Utilice uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="70dc2-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="70dc2-207">Hola de uso **copiar /d** comando.</span><span class="sxs-lookup"><span data-stu-id="70dc2-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="70dc2-208">Permite Hola cifrado archivos toobe guardado como archivos descifrados en el destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="70dc2-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="70dc2-209">Establecer Hola después de la clave del registro:</span><span class="sxs-lookup"><span data-stu-id="70dc2-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="70dc2-210">Ruta de acceso = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="70dc2-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="70dc2-211">Tipo de valor = DWORD</span><span class="sxs-lookup"><span data-stu-id="70dc2-211">Value type = DWORD</span></span>
  - <span data-ttu-id="70dc2-212">Nombre = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="70dc2-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="70dc2-213">Valor = 1</span><span class="sxs-lookup"><span data-stu-id="70dc2-213">Value = 1</span></span>

<span data-ttu-id="70dc2-214">Tenga en cuenta esa clave del registro de hello de configuración afecta a todas las operaciones de copia que se realizan acciones toonetwork.</span><span class="sxs-lookup"><span data-stu-id="70dc2-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="70dc2-215">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="70dc2-215">Need help?</span></span> <span data-ttu-id="70dc2-216">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="70dc2-216">Contact support.</span></span>
<span data-ttu-id="70dc2-217">Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget resuelva el problema rápidamente.</span><span class="sxs-lookup"><span data-stu-id="70dc2-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
