---
title: Montaje de un recurso compartido de archivos de Azure mediante SMB con macOS | Microsoft Docs
description: "Obtenga información acerca de cómo montar un recurso compartido de archivos de Azure mediante SMB con macOS."
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
ms.openlocfilehash: 428086910273d10a68cb8193df377a4db267d6a3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="16d7d-103">Montaje de un recurso compartido de archivos de Azure mediante SMB con macOS</span><span class="sxs-lookup"><span data-stu-id="16d7d-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="16d7d-104">[Azure File Storage](storage-dotnet-how-to-use-files.md) es el servicio de Microsoft que permite crear y utilizar recursos compartidos de archivos en red en Azure utilizando el estándar del sector.</span><span class="sxs-lookup"><span data-stu-id="16d7d-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you to create and use network file shares in the Azure using the industry standard.</span></span> <span data-ttu-id="16d7d-105">Los recursos compartidos de archivos de Azure se pueden montar en macOS Sierra (10.12) y El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="16d7d-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="16d7d-106">En este artículo se muestran dos maneras diferentes para montar un recurso compartido de archivos de Azure en macOS, con la interfaz de usuario de Finder y utilizando el Terminal.</span><span class="sxs-lookup"><span data-stu-id="16d7d-106">This article shows two different ways to mount an Azure File share on macOS with the Finder UI and using the Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="16d7d-107">Antes de montar un recurso compartido de archivos de Azure con SMB, se recomienda deshabilitar la firma de paquetes SMB.</span><span class="sxs-lookup"><span data-stu-id="16d7d-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="16d7d-108">De no hacerlo, puede producirse un rendimiento deficiente en el acceso al recurso compartido de archivos de Azure desde macOS.</span><span class="sxs-lookup"><span data-stu-id="16d7d-108">Not doing so may yield poor performance when accessing the Azure File share from macOS.</span></span> <span data-ttu-id="16d7d-109">La conexión SMB será cifrada, por lo que esto no afecta a la seguridad de la conexión.</span><span class="sxs-lookup"><span data-stu-id="16d7d-109">Your SMB connection will be encrypted, so this does not affect the security of your connection.</span></span> <span data-ttu-id="16d7d-110">Desde el terminal, los siguientes comandos deshabilitan firma del paquete SMB, como se describe en este [artículo de soporte técnico de Apple acerca de cómo deshabilitar la firma de paquetes SMB](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="16d7d-110">From the terminal, the following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="16d7d-111">Requisitos previos para el montaje de un recurso compartido de archivos de Azure en macOS</span><span class="sxs-lookup"><span data-stu-id="16d7d-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="16d7d-112">**Nombre de la cuenta de almacenamiento**: para montar un recurso compartido de archivos de Azure, necesitará el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="16d7d-112">**Storage account name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="16d7d-113">**Clave de la cuenta de almacenamiento**: para montar un recurso compartido de archivos de Azure, necesitará la clave principal (o secundaria) de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="16d7d-113">**Storage account key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="16d7d-114">Actualmente no se admiten claves SAS para el montaje.</span><span class="sxs-lookup"><span data-stu-id="16d7d-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="16d7d-115">**Asegúrese de que el puerto 445 está abierto**: SMB se comunica a través del puerto TCP 445.</span><span class="sxs-lookup"><span data-stu-id="16d7d-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="16d7d-116">En el equipo cliente (Mac), compruebe que el firewall no bloquea el puerto TCP 445.</span><span class="sxs-lookup"><span data-stu-id="16d7d-116">On your client machine (the Mac), check to make sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="16d7d-117">Montaje de un recurso compartido de archivos de Azure con Finder</span><span class="sxs-lookup"><span data-stu-id="16d7d-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="16d7d-118">**Abrir Finder**: Finder está abierto en macOS de forma predeterminada, pero puede asegurarse de sea la aplicación seleccionada haciendo clic en el "icono de cara de macOS" en el Dock:</span><span class="sxs-lookup"><span data-stu-id="16d7d-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is the currently selected application by clicking the "macOS face icon" on the dock:</span></span>  
    <span data-ttu-id="16d7d-119">![Icono de cara de macOS](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="16d7d-119">![The macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="16d7d-120">**Seleccione "Conectar a servidor" en el menú "Ir"**: en la ruta de acceso UNC de los [requisitos previos](#preq), sustituya la doble barra diagonal inversa (`\\`) por `smb://` y todas las otras barras diagonales inversas (`\`) por barras diagonales (`/`).</span><span class="sxs-lookup"><span data-stu-id="16d7d-120">**Select "Connect to Server" from the "Go" Menu**: Using the UNC path from the [prerequisites](#preq), convert the beginning double backslash (`\\`) to `smb://` and all other backslashes (`\`) to forwards slashes (`/`).</span></span> <span data-ttu-id="16d7d-121">El vínculo debe ser similar al siguiente: ![Cuadro de diálogo "Conectar a servidor"](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="16d7d-121">Your link should look like the following: ![The "Connect to Server" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="16d7d-122">**Utilice el nombre del recurso compartido y la clave de la cuenta de almacenamiento cuando se le solicite un nombre de usuario y contraseña**: al hacer clic en "Conectar" en el cuadro de diálogo "Conectar a servidor", se le pedirá el nombre de usuario y una contraseña (se rellenará automáticamente con el nombre de usuario de macOS).</span><span class="sxs-lookup"><span data-stu-id="16d7d-122">**Use the share name and storage account key when prompted for a username and password**: When you click "Connect" on the "Connect to Server" dialog, you will be prompted for the username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="16d7d-123">Puede guardar el nombre del recurso compartido y la clave de la cuenta de almacenamiento en la cadena de claves de macOS.</span><span class="sxs-lookup"><span data-stu-id="16d7d-123">You have the option of placing the share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="16d7d-124">**Uso del recurso compartido de archivos de Azure**: después de sustituir el nombre del recurso compartido y la clave de la cuenta de almacenamiento por el nombre de usuario y contraseña, se montará el recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="16d7d-124">**Use the Azure File share as desired**: After substituting the share name and storage account key in for the username and password, the share will be mounted.</span></span> <span data-ttu-id="16d7d-125">Se puede utilizar como lo haría normalmente con una carpeta local o un recurso compartido de archivos, incluido arrastrar y soltar archivos en el recurso compartido de archivos:</span><span class="sxs-lookup"><span data-stu-id="16d7d-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into the file share:</span></span>

    ![Captura de pantalla de un recurso compartido de archivos de Azure montado](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="16d7d-127">Montaje de un recurso compartido de archivos de Azure con el Terminal</span><span class="sxs-lookup"><span data-stu-id="16d7d-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="16d7d-128">Reemplace `<storage-account-name>` por el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="16d7d-128">Replace `<storage-account-name>` with the name of your storage account.</span></span> <span data-ttu-id="16d7d-129">Proporcione la clave de cuenta de almacenamiento como contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="16d7d-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="16d7d-130">**Uso del recurso compartido de archivos de Azure**: el recurso compartido de archivos de Azure se montará en el punto de montaje especificado por el comando anterior.</span><span class="sxs-lookup"><span data-stu-id="16d7d-130">**Use the Azure File share as desired**: The Azure File share will be mounted at the mount point specified by the previous command.</span></span>  

    ![Captura de pantalla del recurso compartido de archivos de Azure montado](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="16d7d-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16d7d-132">Next steps</span></span>
<span data-ttu-id="16d7d-133">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="16d7d-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="16d7d-134">Artículo de soporte técnico de Apple: cómo conectarse con uso compartido de archivos en el equipo Mac</span><span class="sxs-lookup"><span data-stu-id="16d7d-134">Apple Support Article - How to connect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="16d7d-135">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="16d7d-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="16d7d-136">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="16d7d-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)