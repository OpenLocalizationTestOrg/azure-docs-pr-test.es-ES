---
title: "recurso compartido de archivos de Azure de aaaMount a través de SMB con macOS | Documentos de Microsoft"
description: "Obtenga información acerca de cómo compartir toomount un archivo de Azure a través de SMB con macOS."
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
ms.openlocfilehash: 7b4924cb42247470521c1ae8b9d03ab1756996e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="a890e-103">Montaje de un recurso compartido de archivos de Azure mediante SMB con macOS</span><span class="sxs-lookup"><span data-stu-id="a890e-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="a890e-104">[Almacenamiento de Azure archivo](storage-dotnet-how-to-use-files.md) servicio de Microsoft que le permite toocreate y use red recursos compartidos de archivos en hello Azure usa estándar del sector Hola.</span><span class="sxs-lookup"><span data-stu-id="a890e-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="a890e-105">Los recursos compartidos de archivos de Azure se pueden montar en macOS Sierra (10.12) y El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="a890e-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="a890e-106">Este artículo muestra toomount de dos maneras diferentes un recurso compartido de archivos de Azure en macOS con hello buscador de interfaz de usuario y Hola Terminal.</span><span class="sxs-lookup"><span data-stu-id="a890e-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="a890e-107">Antes de montar un recurso compartido de archivos de Azure con SMB, se recomienda deshabilitar la firma de paquetes SMB.</span><span class="sxs-lookup"><span data-stu-id="a890e-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="a890e-108">De no hacerlo, puede producir un rendimiento deficiente al tener acceso a recurso compartido de archivos de Azure de Hola de macOS.</span><span class="sxs-lookup"><span data-stu-id="a890e-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="a890e-109">Por lo que esto no afectan a la seguridad de saludo de la conexión, se cifrará la conexión de SMB.</span><span class="sxs-lookup"><span data-stu-id="a890e-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="a890e-110">De Hola terminal hello siguientes comandos deshabilitará firma del paquete SMB, como se describe en este [artículo de soporte técnico de Apple acerca de cómo deshabilitar la firma de paquetes SMB](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="a890e-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="a890e-111">Requisitos previos para el montaje de un recurso compartido de archivos de Azure en macOS</span><span class="sxs-lookup"><span data-stu-id="a890e-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="a890e-112">**Nombre de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a890e-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="a890e-113">**Clave de la cuenta de almacenamiento**: toomount compartir de un archivo de Azure, se necesita Hola clave de almacenamiento principal (o secundario).</span><span class="sxs-lookup"><span data-stu-id="a890e-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="a890e-114">Actualmente no se admiten claves SAS para el montaje.</span><span class="sxs-lookup"><span data-stu-id="a890e-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="a890e-115">**Asegúrese de que el puerto 445 está abierto**: SMB se comunica a través del puerto TCP 445.</span><span class="sxs-lookup"><span data-stu-id="a890e-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="a890e-116">En el equipo cliente (Hola Mac), compruebe que el firewall no bloquea el puerto TCP 445 toomake.</span><span class="sxs-lookup"><span data-stu-id="a890e-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="a890e-117">Montaje de un recurso compartido de archivos de Azure con Finder</span><span class="sxs-lookup"><span data-stu-id="a890e-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="a890e-118">**Abrir el selector**: buscador está abierto en macOS de forma predeterminada, pero puede asegurarse de sea Hola seleccionado actualmente aplicación haciendo clic en hello "macOS enfrentan a icono" en hello acoplar:</span><span class="sxs-lookup"><span data-stu-id="a890e-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="a890e-119">![icono enfrentan a macOS Hola](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="a890e-119">![hello macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="a890e-120">**Seleccionar "Conexión tooServer" del menú "Ir" hello**: mediante la ruta de acceso UNC de Hola de hello [requisitos previos](#preq), convertir Hola principio doble barra diagonal inversa (`\\`) demasiado`smb://` y todas las otras barras diagonales inversas (`\`) las barras diagonales tooforwards (`/`).</span><span class="sxs-lookup"><span data-stu-id="a890e-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="a890e-121">El vínculo debe ser similar a Hola siguiente: ![cuadro de diálogo "Conectar tooServer" hello](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="a890e-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="a890e-122">**Use Hola recurso compartido de almacenamiento y el nombre de clave de cuenta cuando se le solicite un nombre de usuario y una contraseña**: al hacer clic en "Conectar" del cuadro de diálogo "Conectar tooServer" Hola, se le pedirá el nombre de usuario de hello y una contraseña (se trata de autopopulated con su macOS nombre de usuario).</span><span class="sxs-lookup"><span data-stu-id="a890e-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="a890e-123">Tiene la opción de Hola de colocar la clave de cuenta de nombre y el almacenamiento de recurso compartido de hello en la cadena de claves de macOS.</span><span class="sxs-lookup"><span data-stu-id="a890e-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="a890e-124">**Recurso compartido de archivos de Azure de Hola de uso según sea necesario**: después de sustituir Hola recurso compartido de almacenamiento y el nombre de clave de cuenta de hello nombre de usuario y una contraseña, se montará el recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="a890e-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="a890e-125">Se puede utilizar como lo haría normalmente un recurso compartido de archivo/carpeta local, incluidos arrastrar y colocar archivos en el recurso compartido de archivos de hello:</span><span class="sxs-lookup"><span data-stu-id="a890e-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![Captura de pantalla de un recurso compartido de archivos de Azure montado](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="a890e-127">Montaje de un recurso compartido de archivos de Azure con el Terminal</span><span class="sxs-lookup"><span data-stu-id="a890e-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="a890e-128">Reemplace `<storage-account-name>` con el nombre de saludo de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a890e-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="a890e-129">Proporcione la clave de cuenta de almacenamiento como contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="a890e-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="a890e-130">**Recurso compartido de archivos de Azure de Hola de uso según sea necesario**: recurso compartido de archivos de Azure de Hola se montará en punto de montaje de hello especificado por el comando anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="a890e-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Una instantánea del recurso compartido de archivos de Azure de hello montado](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="a890e-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a890e-132">Next steps</span></span>
<span data-ttu-id="a890e-133">Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a890e-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="a890e-134">Artículo de soporte técnico de Apple - cómo tooconnect con uso compartido de archivos en el equipo Mac</span><span class="sxs-lookup"><span data-stu-id="a890e-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="a890e-135">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="a890e-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="a890e-136">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="a890e-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)