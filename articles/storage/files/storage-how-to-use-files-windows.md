---
title: aaaMount un recurso compartido de archivos de Azure y Hola de acceso que se comparten en Windows | Documentos de Microsoft
description: Montar un recurso compartido de archivos de Azure y el recurso compartido de Hola de acceso en Windows.
services: storage
documentationcenter: na
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
ms.openlocfilehash: eb6d58ad391adb6c06703ad694150534ccf44ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="966cf-103">Montar un recurso compartido de archivos de Azure y el recurso compartido de Hola de acceso en Windows</span><span class="sxs-lookup"><span data-stu-id="966cf-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="966cf-104">[Almacenamiento de Azure archivo](../storage-dotnet-how-to-use-files.md) es sistema de archivos de nube de Microsoft toouse fácil.</span><span class="sxs-lookup"><span data-stu-id="966cf-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="966cf-105">Los recursos compartidos de archivos de Azure se pueden montar en Windows y Windows Server.</span><span class="sxs-lookup"><span data-stu-id="966cf-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="966cf-106">Este artículo muestra un recurso compartido de archivos de Azure de tres toomount de distintas maneras en Windows: con hello IU del explorador de archivos, a través de PowerShell y Hola símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="966cf-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="966cf-107">En orden toomount de un archivo de Azure compartir fuera de hello región de Azure se hospeda en, por ejemplo, local o en una región distinta de Azure, Hola sistema operativo debe admitir SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="966cf-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="966cf-108">Un recurso compartido de archivos de Azure se puede montar en un equipo Windows tanto en local como en una máquina virtual de Azure en función de la versión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="966cf-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="966cf-109">Tabla a continuación muestra hello</span><span class="sxs-lookup"><span data-stu-id="966cf-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="966cf-110">Versión de Windows</span><span class="sxs-lookup"><span data-stu-id="966cf-110">Windows Version</span></span>        | <span data-ttu-id="966cf-111">Versión de SMB</span><span class="sxs-lookup"><span data-stu-id="966cf-111">SMB Version</span></span> |<span data-ttu-id="966cf-112">Se puede montar en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="966cf-112">Mountable On Azure VM</span></span>|<span data-ttu-id="966cf-113">Se puede montar en un entorno local</span><span class="sxs-lookup"><span data-stu-id="966cf-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="966cf-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="966cf-114">Windows 7</span></span>              | <span data-ttu-id="966cf-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="966cf-115">SMB 2.1</span></span>     | <span data-ttu-id="966cf-116">Sí</span><span class="sxs-lookup"><span data-stu-id="966cf-116">Yes</span></span>                 | <span data-ttu-id="966cf-117">No</span><span class="sxs-lookup"><span data-stu-id="966cf-117">No</span></span>                  |
| <span data-ttu-id="966cf-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="966cf-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="966cf-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="966cf-119">SMB 2.1</span></span>     | <span data-ttu-id="966cf-120">Sí</span><span class="sxs-lookup"><span data-stu-id="966cf-120">Yes</span></span>                 | <span data-ttu-id="966cf-121">No</span><span class="sxs-lookup"><span data-stu-id="966cf-121">No</span></span>                  |
| <span data-ttu-id="966cf-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="966cf-122">Windows 8</span></span>              | <span data-ttu-id="966cf-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="966cf-123">SMB 3.0</span></span>     | <span data-ttu-id="966cf-124">Sí</span><span class="sxs-lookup"><span data-stu-id="966cf-124">Yes</span></span>                 | <span data-ttu-id="966cf-125">Sí</span><span class="sxs-lookup"><span data-stu-id="966cf-125">Yes</span></span>                 |
| <span data-ttu-id="966cf-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="966cf-126">Windows Server 2012</span></span>    | <span data-ttu-id="966cf-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="966cf-127">SMB 3.0</span></span>     | <span data-ttu-id="966cf-128">Sí</span><span class="sxs-lookup"><span data-stu-id="966cf-128">Yes</span></span>                 | <span data-ttu-id="966cf-129">Sí</span><span class="sxs-lookup"><span data-stu-id="966cf-129">Yes</span></span>                 |
| <span data-ttu-id="966cf-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="966cf-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="966cf-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="966cf-131">SMB 3.0</span></span>     | <span data-ttu-id="966cf-132">Sí</span><span class="sxs-lookup"><span data-stu-id="966cf-132">Yes</span></span>                 | <span data-ttu-id="966cf-133">Sí</span><span class="sxs-lookup"><span data-stu-id="966cf-133">Yes</span></span>                 |
| <span data-ttu-id="966cf-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="966cf-134">Windows 10</span></span>             | <span data-ttu-id="966cf-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="966cf-135">SMB 3.0</span></span>     | <span data-ttu-id="966cf-136">Sí</span><span class="sxs-lookup"><span data-stu-id="966cf-136">Yes</span></span>                 | <span data-ttu-id="966cf-137">Sí</span><span class="sxs-lookup"><span data-stu-id="966cf-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="966cf-138">Siempre se recomienda tomar Hola KB más reciente para su versión de Windows.</span><span class="sxs-lookup"><span data-stu-id="966cf-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="966cf-139"></a>Requisitos previos para el montaje de un recurso compartido de archivos de Azure en Windows</span><span class="sxs-lookup"><span data-stu-id="966cf-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="966cf-140">**Nombre de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="966cf-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="966cf-141">**Clave de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola clave de almacenamiento principal (o secundario).</span><span class="sxs-lookup"><span data-stu-id="966cf-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="966cf-142">Actualmente no se admiten claves SAS para el montaje.</span><span class="sxs-lookup"><span data-stu-id="966cf-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="966cf-143">**Asegúrese de que el puerto 445 está abierto**: Azure File Storage usa el protocolo SMB.</span><span class="sxs-lookup"><span data-stu-id="966cf-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="966cf-144">SMB se comunica a través del puerto TCP 445 - Compruebe toosee si el firewall no bloquea los puertos TCP 445 en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="966cf-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="966cf-145">Montar el recurso compartido de archivos de Azure de hello con el Explorador de archivos</span><span class="sxs-lookup"><span data-stu-id="966cf-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="966cf-146">Tenga en cuenta que Hola siguiendo las instrucciones se muestran en Windows 10 y puede variar ligeramente en las versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="966cf-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="966cf-147">**Abra el Explorador de archivos**: Esto puede hacerse mediante la apertura de hello menú Inicio, o bien presionando contextual Win + E.</span><span class="sxs-lookup"><span data-stu-id="966cf-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="966cf-148">**Navegue toohello el elemento de "Este PC" en el lado izquierdo de Hola de ventana hello. Esta operación cambiará menús Hola disponibles en la cinta de opciones de Hola. En el menú de equipo de hello, seleccione "Conectar a unidad de red"**.</span><span class="sxs-lookup"><span data-stu-id="966cf-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Menú desplegable de una captura de pantalla de hello "Conectar a unidad de red"](./media/storage-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="966cf-150">**Copiar ruta de acceso UNC de hello en panel de "Conectar" Hola Hola portal de Azure**: una descripción detallada de cómo toofind esta información puede encontrarse [aquí](storage-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="966cf-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![ruta de acceso UNC de Hola desde el panel de conexión de almacenamiento de archivo de Azure de Hola](./media/storage-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="966cf-152">**Seleccione la letra de unidad de Hola y escriba la ruta de acceso UNC Hola.**</span><span class="sxs-lookup"><span data-stu-id="966cf-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    ![Una captura de pantalla del cuadro de diálogo "Conectar a unidad de red" hello](./media/storage-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="966cf-154">**Hola de uso con el nombre de cuenta de almacenamiento `Azure\` como nombre de usuario de hello y una clave de cuenta de almacenamiento como contraseña de Hola.**</span><span class="sxs-lookup"><span data-stu-id="966cf-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Una captura de pantalla del cuadro de diálogo de credenciales de red de Hola](./media/storage-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="966cf-156">**Uso del recurso compartido de archivos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="966cf-156">**Use Azure File share as desired**.</span></span>
    
    ![El recurso compartido de archivos de Azure ahora está montado](./media/storage-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="966cf-158">**Cuando se toodismount listo (o desconectarse) recurso compartido de archivos de Azure de hello, puede hacerlo haciendo clic en la entrada de hello para el recurso compartido de hello en hello "ubicaciones de red" en el Explorador de archivos y seleccionando "Desconectar"**.</span><span class="sxs-lookup"><span data-stu-id="966cf-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="966cf-159">Montar el recurso compartido de archivos de Azure de hello con PowerShell</span><span class="sxs-lookup"><span data-stu-id="966cf-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="966cf-160">**Recurso compartido de archivos de Azure de Hola de toomount de comandos siguiente Hola de uso**: Recuerde tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` con la información adecuada Hola.</span><span class="sxs-lookup"><span data-stu-id="966cf-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="966cf-161">**Recurso compartido de archivos de Azure de Hola de uso según sea necesario**.</span><span class="sxs-lookup"><span data-stu-id="966cf-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="966cf-162">**Cuando haya terminado, desmonte el recurso compartido de archivos de Azure de hello mediante el siguiente comando de hello**.</span><span class="sxs-lookup"><span data-stu-id="966cf-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="966cf-163">Puede usar hello `-Persist` parámetro en `New-PSDrive` toomake Hola rest de toohello visible de recurso compartido de archivos de Azure de hello SO mientras montado.</span><span class="sxs-lookup"><span data-stu-id="966cf-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="966cf-164">Montar el recurso compartido de archivos de Azure de hello con símbolo del sistema</span><span class="sxs-lookup"><span data-stu-id="966cf-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="966cf-165">**Recurso compartido de archivos de Azure de Hola de toomount de comandos siguiente Hola de uso**: Recuerde tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` con la información adecuada Hola.</span><span class="sxs-lookup"><span data-stu-id="966cf-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="966cf-166">**Recurso compartido de archivos de Azure de Hola de uso según sea necesario**.</span><span class="sxs-lookup"><span data-stu-id="966cf-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="966cf-167">**Cuando haya terminado, desmonte el recurso compartido de archivos de Azure de hello mediante el siguiente comando de hello**.</span><span class="sxs-lookup"><span data-stu-id="966cf-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="966cf-168">Puede configurar Hola reconexión tooautomatically del recurso compartido de archivo de Azure al reiniciar por conservar las credenciales de hello en Windows.</span><span class="sxs-lookup"><span data-stu-id="966cf-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="966cf-169">Hola siguiente comando conservará las credenciales de hello:</span><span class="sxs-lookup"><span data-stu-id="966cf-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="966cf-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="966cf-170">Next steps</span></span>
<span data-ttu-id="966cf-171">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="966cf-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="966cf-172">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="966cf-172">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="966cf-173">Solución de problemas en Windows</span><span class="sxs-lookup"><span data-stu-id="966cf-173">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="966cf-174">Artículos y vídeos conceptuales</span><span class="sxs-lookup"><span data-stu-id="966cf-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="966cf-175">Azure File Storage: un sistema de archivos SMB en la nube sin dificultades para Windows y Linux</span><span class="sxs-lookup"><span data-stu-id="966cf-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="966cf-176">¿Cómo toouse almacenamiento de archivos de Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="966cf-176">How toouse Azure File storage with Linux</span></span>](../storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="966cf-177">Compatibilidad de herramientas con Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="966cf-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="966cf-178">Cómo toouse AzCopy con almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="966cf-178">How toouse AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="966cf-179">Uso de hello CLI de Azure con el almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="966cf-179">Using hello Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="966cf-180">Solución de problemas de Azure File Storage (Windows)</span><span class="sxs-lookup"><span data-stu-id="966cf-180">Troubleshooting Azure File storage problems - Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)
* [<span data-ttu-id="966cf-181">Solución de problemas de Azure File Storage (Linux)</span><span class="sxs-lookup"><span data-stu-id="966cf-181">Troubleshooting Azure File storage problems - Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a><span data-ttu-id="966cf-182">Publicaciones de blog</span><span class="sxs-lookup"><span data-stu-id="966cf-182">Blog posts</span></span>
* [<span data-ttu-id="966cf-183">El almacenamiento de archivos de Azure ya está disponible de manera general</span><span class="sxs-lookup"><span data-stu-id="966cf-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="966cf-184">En el interior de Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="966cf-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="966cf-185">Introducing Microsoft Azure File Service (Introducción al servicio de archivos de Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="966cf-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="966cf-186">Migración de datos tooAzure archivo</span><span class="sxs-lookup"><span data-stu-id="966cf-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="966cf-187">Referencia</span><span class="sxs-lookup"><span data-stu-id="966cf-187">Reference</span></span>
* [<span data-ttu-id="966cf-188">Referencia de la biblioteca de clientes de almacenamiento para .NET</span><span class="sxs-lookup"><span data-stu-id="966cf-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="966cf-189">Referencia de la API REST del servicio de archivos</span><span class="sxs-lookup"><span data-stu-id="966cf-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
