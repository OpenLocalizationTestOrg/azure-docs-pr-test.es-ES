---
title: Montaje de un recurso compartido de archivos de Azure y acceso al recurso compartido en Windows | Microsoft Docs
description: Montaje de un recurso compartido de archivos de Azure y acceso al recurso compartido en Windows.
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
ms.openlocfilehash: e911e787cd1e29b2bbeaa648869c50245f2dd9ba
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="mount-an-azure-file-share-and-access-the-share-in-windows"></a><span data-ttu-id="827b8-103">Montaje de un recurso compartido de archivos de Azure y acceso al recurso compartido en Windows</span><span class="sxs-lookup"><span data-stu-id="827b8-103">Mount an Azure File share and access the share in Windows</span></span>
<span data-ttu-id="827b8-104">[Azure File Storage](storage-dotnet-how-to-use-files.md) es el sistema de archivos en la nube de Microsoft fácil de usar.</span><span class="sxs-lookup"><span data-stu-id="827b8-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="827b8-105">Los recursos compartidos de archivos de Azure se pueden montar en Windows y Windows Server.</span><span class="sxs-lookup"><span data-stu-id="827b8-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="827b8-106">En este artículo se muestran tres maneras diferentes para montar un recurso compartido de archivos de Azure en Windows: con la interfaz del explorador de archivos, a través de PowerShell y mediante el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="827b8-106">This article shows three different ways to mount an Azure File share on Windows: with the File Explorer UI, via PowerShell, and via the Command Prompt.</span></span> 

<span data-ttu-id="827b8-107">Para montar un recurso compartido de archivos de Azure fuera de la región de Azure en la que se hospeda, bien sea en local o en una región distinta de Azure, el sistema operativo debe admitir SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="827b8-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support SMB 3.0.</span></span> 

<span data-ttu-id="827b8-108">Un recurso compartido de archivos de Azure se puede montar en un equipo Windows tanto en local como en una máquina virtual de Azure en función de la versión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="827b8-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="827b8-109">La tabla siguiente lo describe</span><span class="sxs-lookup"><span data-stu-id="827b8-109">Below table illustrates the</span></span> 

| <span data-ttu-id="827b8-110">Versión de Windows</span><span class="sxs-lookup"><span data-stu-id="827b8-110">Windows Version</span></span>        | <span data-ttu-id="827b8-111">Versión de SMB</span><span class="sxs-lookup"><span data-stu-id="827b8-111">SMB Version</span></span> |<span data-ttu-id="827b8-112">Se puede montar en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="827b8-112">Mountable On Azure VM</span></span>|<span data-ttu-id="827b8-113">Se puede montar en un entorno local</span><span class="sxs-lookup"><span data-stu-id="827b8-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="827b8-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="827b8-114">Windows 7</span></span>              | <span data-ttu-id="827b8-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="827b8-115">SMB 2.1</span></span>     | <span data-ttu-id="827b8-116">Sí</span><span class="sxs-lookup"><span data-stu-id="827b8-116">Yes</span></span>                 | <span data-ttu-id="827b8-117">No</span><span class="sxs-lookup"><span data-stu-id="827b8-117">No</span></span>                  |
| <span data-ttu-id="827b8-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="827b8-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="827b8-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="827b8-119">SMB 2.1</span></span>     | <span data-ttu-id="827b8-120">Sí</span><span class="sxs-lookup"><span data-stu-id="827b8-120">Yes</span></span>                 | <span data-ttu-id="827b8-121">No</span><span class="sxs-lookup"><span data-stu-id="827b8-121">No</span></span>                  |
| <span data-ttu-id="827b8-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="827b8-122">Windows 8</span></span>              | <span data-ttu-id="827b8-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="827b8-123">SMB 3.0</span></span>     | <span data-ttu-id="827b8-124">Sí</span><span class="sxs-lookup"><span data-stu-id="827b8-124">Yes</span></span>                 | <span data-ttu-id="827b8-125">Sí</span><span class="sxs-lookup"><span data-stu-id="827b8-125">Yes</span></span>                 |
| <span data-ttu-id="827b8-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="827b8-126">Windows Server 2012</span></span>    | <span data-ttu-id="827b8-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="827b8-127">SMB 3.0</span></span>     | <span data-ttu-id="827b8-128">Sí</span><span class="sxs-lookup"><span data-stu-id="827b8-128">Yes</span></span>                 | <span data-ttu-id="827b8-129">Sí</span><span class="sxs-lookup"><span data-stu-id="827b8-129">Yes</span></span>                 |
| <span data-ttu-id="827b8-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="827b8-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="827b8-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="827b8-131">SMB 3.0</span></span>     | <span data-ttu-id="827b8-132">Sí</span><span class="sxs-lookup"><span data-stu-id="827b8-132">Yes</span></span>                 | <span data-ttu-id="827b8-133">Sí</span><span class="sxs-lookup"><span data-stu-id="827b8-133">Yes</span></span>                 |
| <span data-ttu-id="827b8-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="827b8-134">Windows 10</span></span>             | <span data-ttu-id="827b8-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="827b8-135">SMB 3.0</span></span>     | <span data-ttu-id="827b8-136">Sí</span><span class="sxs-lookup"><span data-stu-id="827b8-136">Yes</span></span>                 | <span data-ttu-id="827b8-137">Sí</span><span class="sxs-lookup"><span data-stu-id="827b8-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="827b8-138">Siempre se recomienda disponer de la KB más reciente para su versión de Windows.</span><span class="sxs-lookup"><span data-stu-id="827b8-138">We always recommend taking the most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="827b8-139"></a>Requisitos previos para el montaje de un recurso compartido de archivos de Azure en Windows</span><span class="sxs-lookup"><span data-stu-id="827b8-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="827b8-140">**Nombre de la cuenta de almacenamiento**: para montar un recurso compartido de archivos de Azure, necesitará el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="827b8-140">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="827b8-141">**Clave de la cuenta de almacenamiento**: para montar un recurso compartido de archivos de Azure, necesitará la clave principal (o secundaria) de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="827b8-141">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="827b8-142">Actualmente no se admiten claves SAS para el montaje.</span><span class="sxs-lookup"><span data-stu-id="827b8-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="827b8-143">**Asegúrese de que el puerto 445 está abierto**: Azure File Storage usa el protocolo SMB.</span><span class="sxs-lookup"><span data-stu-id="827b8-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="827b8-144">SMB se comunica a través del puerto TCP 445: compruebe que el firewall no bloquea el puerto TCP 445 en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="827b8-144">SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-with-file-explorer"></a><span data-ttu-id="827b8-145">Montaje del recurso compartido de archivos de Azure con el explorador de archivos</span><span class="sxs-lookup"><span data-stu-id="827b8-145">Mount the Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="827b8-146">Tenga en cuenta que las instrucciones siguientes se muestran en Windows 10 y pueden variar ligeramente en las versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="827b8-146">Note that the following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="827b8-147">**Abra el Explorador de archivos**: esto puede hacerse desde el menú Inicio o bien presionando las teclas Win + E.</span><span class="sxs-lookup"><span data-stu-id="827b8-147">**Open File Explorer**: This can be done by opening from the Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="827b8-148">**Desplácese hasta el elemento "Este PC" en el lado izquierdo de la ventana. Esta operación cambiará los menús disponibles en la barra de herramientas. En el menú Equipo, seleccione "Conectar a unidad de red"**.</span><span class="sxs-lookup"><span data-stu-id="827b8-148">**Navigate to the "This PC" item on the left-hand side of the window. This will change the menus available in the ribbon. Under the Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Captura de pantalla del menú desplegable "Conectar a unidad de red"](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="827b8-150">**Copie la ruta de acceso UNC desde el panel "Conectar" de Azure Portal**: una descripción detallada de cómo buscar esta información puede encontrarse [aquí](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="827b8-150">**Copy the UNC path from the "Connect" pane in the Azure portal**: A detailed description of how to find this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![Ruta de acceso UNC en el panel Conectar de Azure File Storage](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="827b8-152">**Seleccione la letra de unidad y escriba la ruta de acceso UNC.**</span><span class="sxs-lookup"><span data-stu-id="827b8-152">**Select the Drive letter and enter the UNC path.**</span></span> 
    
    ![Captura de pantalla del cuadro de diálogo "Conectar a unidad de red"](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="827b8-154">**Utilice el nombre de la cuenta de almacenamiento prefijada con `Azure\` como el nombre de usuario y la clave de la cuenta de almacenamiento como contraseña.**</span><span class="sxs-lookup"><span data-stu-id="827b8-154">**Use the Storage Account Name prepended with `Azure\` as the username and a Storage Account Key as the password.**</span></span>
    
    ![Captura de pantalla del cuadro de diálogo credenciales de red](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="827b8-156">**Uso del recurso compartido de archivos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="827b8-156">**Use Azure File share as desired**.</span></span>
    
    ![El recurso compartido de archivos de Azure ahora está montado](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="827b8-158">**Cuando esté listo para desmontar (o desconectar) el recurso compartido de archivos de Azure, puede hacerlo haciendo clic en la entrada para el recurso compartido en "Ubicaciones de red" en el explorador de archivos y seleccionando "Desconectar"**.</span><span class="sxs-lookup"><span data-stu-id="827b8-158">**When you are ready to dismount (or disconnect) the Azure File share, you can do so by right clicking on the entry for the share under the "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-the-azure-file-share-with-powershell"></a><span data-ttu-id="827b8-159">Montaje del recurso compartido de archivos de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="827b8-159">Mount the Azure File share with PowerShell</span></span>
1. <span data-ttu-id="827b8-160">**Use el siguiente comando para montar el recurso compartido de archivos de Azure**: no olvide reemplazar `<storage-account-name>`, `<share-name>`, `<storage-account-key>` y `<desired-drive-letter>` con la información correcta.</span><span class="sxs-lookup"><span data-stu-id="827b8-160">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="827b8-161">**Uso del recurso compartido de archivos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="827b8-161">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="827b8-162">**Cuando haya terminado, puede desmontar el recurso compartido de archivos de Azure mediante el siguiente comando**.</span><span class="sxs-lookup"><span data-stu-id="827b8-162">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="827b8-163">Puede usar el parámetro `-Persist` en `New-PSDrive` para hacer visible el recurso compartido de archivos de Azure para el resto del sistema operativo durante el montaje.</span><span class="sxs-lookup"><span data-stu-id="827b8-163">You may use the `-Persist` parameter on `New-PSDrive` to make the Azure File share visible to the rest of the OS while mounted.</span></span>

## <a name="mount-the-azure-file-share-with-command-prompt"></a><span data-ttu-id="827b8-164">Montaje del recurso compartido de archivos de Azure desde el símbolo del sistema</span><span class="sxs-lookup"><span data-stu-id="827b8-164">Mount the Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="827b8-165">**Use el siguiente comando para montar el recurso compartido de archivos de Azure**: no olvide reemplazar `<storage-account-name>`, `<share-name>`, `<storage-account-key>` y `<desired-drive-letter>` con la información correcta.</span><span class="sxs-lookup"><span data-stu-id="827b8-165">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="827b8-166">**Uso del recurso compartido de archivos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="827b8-166">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="827b8-167">**Cuando haya terminado, puede desmontar el recurso compartido de archivos de Azure mediante el siguiente comando**.</span><span class="sxs-lookup"><span data-stu-id="827b8-167">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="827b8-168">Puede configurar el recurso compartido de archivos de Azure para conectar automáticamente al reiniciar haciendo conservar las credenciales de Windows.</span><span class="sxs-lookup"><span data-stu-id="827b8-168">You can configure the Azure File share to automatically reconnect on reboot by persisting the credentials in Windows.</span></span> <span data-ttu-id="827b8-169">El siguiente comando conservará las credenciales:</span><span class="sxs-lookup"><span data-stu-id="827b8-169">The following command will persist the credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="827b8-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="827b8-170">Next steps</span></span>
<span data-ttu-id="827b8-171">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="827b8-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="827b8-172">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="827b8-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="827b8-173">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="827b8-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="827b8-174">Artículos y vídeos conceptuales</span><span class="sxs-lookup"><span data-stu-id="827b8-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="827b8-175">Azure File Storage: un sistema de archivos SMB en la nube sin dificultades para Windows y Linux</span><span class="sxs-lookup"><span data-stu-id="827b8-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="827b8-176">Uso de Azure File Storage con Linux</span><span class="sxs-lookup"><span data-stu-id="827b8-176">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="827b8-177">Compatibilidad de herramientas con Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="827b8-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="827b8-178">Usar Azure PowerShell con Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="827b8-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="827b8-179">Uso de AzCopy con Almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="827b8-179">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="827b8-180">Uso de la CLI de Azure con Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="827b8-180">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="827b8-181">Solución de problemas de Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="827b8-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="827b8-182">Publicaciones de blog</span><span class="sxs-lookup"><span data-stu-id="827b8-182">Blog posts</span></span>
* [<span data-ttu-id="827b8-183">El almacenamiento de archivos de Azure ya está disponible de manera general</span><span class="sxs-lookup"><span data-stu-id="827b8-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="827b8-184">En el interior de Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="827b8-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="827b8-185">Introducing Microsoft Azure File Service (Introducción al servicio de archivos de Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="827b8-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="827b8-186">Migración de datos a Azure Files</span><span class="sxs-lookup"><span data-stu-id="827b8-186">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="827b8-187">Referencia</span><span class="sxs-lookup"><span data-stu-id="827b8-187">Reference</span></span>
* [<span data-ttu-id="827b8-188">Referencia de la biblioteca de clientes de almacenamiento para .NET</span><span class="sxs-lookup"><span data-stu-id="827b8-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="827b8-189">Referencia de la API REST del servicio de archivos</span><span class="sxs-lookup"><span data-stu-id="827b8-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
