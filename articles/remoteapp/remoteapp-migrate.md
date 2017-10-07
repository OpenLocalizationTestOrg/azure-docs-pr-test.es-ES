---
title: datos de usuario de aaaMigrate de RemoteApp de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomigrate los datos de usuario dentro y fuera de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="42618-103">¿Cómo toomigrate datos dentro y fuera de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="42618-103">How toomigrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="42618-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="42618-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="42618-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="42618-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="42618-106">Puede usar muchas distintas herramientas y métodos tootransfer [datos de usuario](remoteapp-upd.md) dentro y fuera de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="42618-106">You can use many different tools and methods tootransfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="42618-107">Estos son algunos métodos:</span><span class="sxs-lookup"><span data-stu-id="42618-107">Here are a few methods:</span></span>

* <span data-ttu-id="42618-108">Copiar y pegar mediante el uso compartido del Portapapeles</span><span class="sxs-lookup"><span data-stu-id="42618-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="42618-109">Copiar archivos y datos de servidor de archivos de tooa</span><span class="sxs-lookup"><span data-stu-id="42618-109">Copy files and data tooa file server</span></span>
* <span data-ttu-id="42618-110">Copie los archivos tooOneDrive para la empresa a través de un explorador</span><span class="sxs-lookup"><span data-stu-id="42618-110">Copy files tooOneDrive for Business through a browser</span></span>
* <span data-ttu-id="42618-111">Copiar archivos mediante redirección</span><span class="sxs-lookup"><span data-stu-id="42618-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="42618-112">No se puede habilitar hello OneDrive para los agentes de sincronización de negocio o un consumidor - [no se admiten](remoteapp-onedrive.md) en Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="42618-112">You cannot enable hello OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="42618-113">Uso de copiar y pegar en el Explorador de archivos</span><span class="sxs-lookup"><span data-stu-id="42618-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="42618-114">Copiar y pegar mediante el Portapapeles de hello está habilitada en las implementaciones de RemoteApp [predeterminada](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="42618-114">Copy and paste using hello clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="42618-115">Gracias a esto, los usuarios pueden copiar archivos entre su equipo local y aplicaciones de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="42618-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="42618-116">A menudo, a través de curso normal de Hola de uso de aplicaciones de RemoteApp, los usuarios han guardado archivos UPD tootheir - mover que datos de RemoteApp están fáciles:</span><span class="sxs-lookup"><span data-stu-id="42618-116">Often, through hello normal course of using apps in RemoteApp, users have saved files tootheir UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="42618-117">[Publique el Explorador de archivos como aplicación](remoteapp-publish.md) en una colección de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="42618-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="42618-118">(tenga en cuenta que se trata de una tarea administrativa).</span><span class="sxs-lookup"><span data-stu-id="42618-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="42618-119">Dirigir la aplicación de explorador de archivos de los usuarios toolaunch Hola publicada y toouse que toocopy y pegue los archivos en su UPD y fuera de ella.</span><span class="sxs-lookup"><span data-stu-id="42618-119">Direct your users toolaunch hello File Explorer app you published and toouse that toocopy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="42618-120">Cargar archivos y servidor de archivos de datos tooa mediante la copia de archivos de red estándar</span><span class="sxs-lookup"><span data-stu-id="42618-120">Upload files and data tooa file server by using standard network file copy</span></span>
<span data-ttu-id="42618-121">A menudo las organizaciones usar datos generales de toostore de servidores de archivos.</span><span class="sxs-lookup"><span data-stu-id="42618-121">Often organizations use file servers toostore general data.</span></span> <span data-ttu-id="42618-122">Si conoce el nombre del servidor de Hola o ubicación, los usuarios pueden examinar Hola red local para el servidor de hello y, a continuación, copie sus archivos, igual que hicieron anteriormente.</span><span class="sxs-lookup"><span data-stu-id="42618-122">If you know hello server name or location, your users can browse hello local network for hello server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="42618-123">Nuevo podrá desea toopublish tooRemoteApp de explorador de archivos y, a continuación, compartirlo con los usuarios.</span><span class="sxs-lookup"><span data-stu-id="42618-123">Again you'll want toopublish File Explorer tooRemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="42618-124">servidor de archivos de Hello debe estar en la red enrutable Hola que RemoteApp se implementó en.</span><span class="sxs-lookup"><span data-stu-id="42618-124">hello file server must be on hello routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a><span data-ttu-id="42618-125">Copie los archivos tooOneDrive para la empresa</span><span class="sxs-lookup"><span data-stu-id="42618-125">Copy files tooOneDrive for Business</span></span>
<span data-ttu-id="42618-126">Aunque no se puede habilitar hello OneDrive para el agente de sincronización de negocios en RemoteApp, puede seguir copiar archivos desde su tooOneDrive UPD para la empresa a través de un explorador.</span><span class="sxs-lookup"><span data-stu-id="42618-126">Although you cannot enable hello OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD tooOneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="42618-127">Publicar tooRemoteApp del explorador de archivos y, a continuación, indicar a los usuarios tooaccess Hola archivos a través de esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="42618-127">Publish File Explorer tooRemoteApp and then tell users tooaccess hello files through that app.</span></span> 
2. <span data-ttu-id="42618-128">Es más fáciles archivos tootransfer si están comprimidos, por lo que los usuarios deben crear un archivo .zip que todos los de hello archivos toomove tooOneDrive contiene para la empresa.</span><span class="sxs-lookup"><span data-stu-id="42618-128">It's easiest tootransfer files if they are compressed, so users should create a .zip file that contains all of hello files toomove tooOneDrive for Business.</span></span>
3. <span data-ttu-id="42618-129">Pida el portal de usuarios toogo toohello Office 365 y, a continuación, vaya tooOneDrive y cargar el archivo .zip de Hola.</span><span class="sxs-lookup"><span data-stu-id="42618-129">Ask users toogo toohello Office 365 portal, and then go tooOneDrive and upload hello .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="42618-130">Copia de archivos mediante la redirección de unidades</span><span class="sxs-lookup"><span data-stu-id="42618-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="42618-131">Si ha habilitado la [redirección de unidades](remoteapp-redirection.md), ya ha creado una unidad asignada para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="42618-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="42618-132">En este caso, puede sus archivos en la unidad de hello redirigido zip y, a continuación, guardarlos tootheir PC local.</span><span class="sxs-lookup"><span data-stu-id="42618-132">In this case, they can zip their files on hello redirected drive and then save them tootheir local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="42618-133">Cómo pueden exportar datos los administradores</span><span class="sxs-lookup"><span data-stu-id="42618-133">How administrators can export data</span></span>

<span data-ttu-id="42618-134">Administra para Azure RemoteApp puede exportar todos los discos de perfil de usuario (UDP) para todas las colecciones dentro de un almacenamiento con PowerShell de Azure de suscripción tooAzure cmdlet Export-AzureRemoteAppUserDisk.</span><span class="sxs-lookup"><span data-stu-id="42618-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription tooAzure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="42618-135">No hay ninguna capacidad tooselect individuales UPD.</span><span class="sxs-lookup"><span data-stu-id="42618-135">There is no ability tooselect individual UPD's.</span></span>  <span data-ttu-id="42618-136">Cuando se ejecuta el comando de PowerShell de hello, cada disco de usuario podrá tener un 50gb de tamaño de disco fijo y almacenamiento tooAzure exportado.</span><span class="sxs-lookup"><span data-stu-id="42618-136">When hello PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported tooAzure storage.</span></span>  <span data-ttu-id="42618-137">Los costos del almacenamiento de Azure se cobrarán inmediatamente para este almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="42618-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="42618-138">Al ejecutar este comando Asegúrese de no hay ninguna sesión de exportación de hello en caso contrario se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="42618-138">When running this command ensure there are no sessions otherwise hello export will fail.</span></span>

<span data-ttu-id="42618-139">Los UPD para las implementaciones de Azure RemoteApp unidas a un dominio solo pueden usarse de nuevo en una implementación de RDS; las implementaciones no unidas a un dominio no se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="42618-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="42618-140">Si estos discos se utilizará en una implementación de RDS se recomienda toouse nuestro [scripts automatizados](https://github.com/arcadiahlyy/aramigration) que se exporte, convertir e importar Hola del UPD en una implementación de RDS.</span><span class="sxs-lookup"><span data-stu-id="42618-140">If these disks will be used in an RDS deployment we recommend toouse our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import hello UPD's into an RDS deployment.</span></span>

