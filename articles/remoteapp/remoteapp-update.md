---
title: "aaaUpdate su colección de RemoteApp de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooupdate su colección de RemoteApp de Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="32cf4-103">Actualización de una colección en Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="32cf4-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="32cf4-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="32cf4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="32cf4-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="32cf4-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="32cf4-106">Aparecerá un tiempo, inevitablemente, cuando necesite tooupdate Hola aplicaciones o imagen en la colección de RemoteApp de Azure.</span><span class="sxs-lookup"><span data-stu-id="32cf4-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="32cf4-107">Si está utilizando una de las imágenes de hello incluidas con su suscripción de RemoteApp de Azure, en la colección de una nube o híbridas, una o todas las actualizaciones se controlan RemoteApp de Azure, por lo que puede colocar la forma más fácil.</span><span class="sxs-lookup"><span data-stu-id="32cf4-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="32cf4-108">Sin embargo, si está utilizando una imagen personalizada (que crea a partir de cero o que creó mediante la modificación de una de nuestras imágenes), se va a encargar de mantenimiento de aplicaciones y la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="32cf4-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="32cf4-109">Si necesita tooupdate la imagen o cualquiera de las aplicaciones de hello dentro de él, debe toocreate una versión nueva y actualizada de hello imagen y, a continuación, reemplazar Hola existente imagen en la colección con esta nueva imagen actualizada.</span><span class="sxs-lookup"><span data-stu-id="32cf4-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="32cf4-110">Por lo tanto, ¿cómo tiene que proceder para actualizar la colección?</span><span class="sxs-lookup"><span data-stu-id="32cf4-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="32cf4-111">Es bastante sencillo:</span><span class="sxs-lookup"><span data-stu-id="32cf4-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="32cf4-112">Imagen de Hola de actualización que utiliza en la colección.</span><span class="sxs-lookup"><span data-stu-id="32cf4-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="32cf4-113">Aplique las revisiones o actualizaciones necesarias y guárdela con un otro nombre.</span><span class="sxs-lookup"><span data-stu-id="32cf4-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="32cf4-114">[Cargar](remoteapp-uploadimage.md) o [importar](remoteapp-image-on-azurevm.md) tooRemoteApp de esa imagen.</span><span class="sxs-lookup"><span data-stu-id="32cf4-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="32cf4-115">Ahora, haga clic en la página de la colección de hello, **actualización**.</span><span class="sxs-lookup"><span data-stu-id="32cf4-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="32cf4-116">Elegir nueva imagen de Hola Hola **imagen de plantilla** lista.</span><span class="sxs-lookup"><span data-stu-id="32cf4-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="32cf4-117">Aquí es parte complicada hello - necesita toodecide cómo toodeal con cualquier usuario que usa actualmente una aplicación en la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="32cf4-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="32cf4-118">Tener Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="32cf4-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="32cf4-119">**Proporcionar a los usuarios 60 minutos después de la actualización de hello**.</span><span class="sxs-lookup"><span data-stu-id="32cf4-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="32cf4-120">Tan pronto como finaliza la actualización de hello, Azure RemoteApp mostrará un mensaje tooany active los usuarios informándoles toosave el trabajo y su registro desactivado y volver a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="32cf4-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="32cf4-121">Transcurridos los 60 minutos, se cerrará automáticamente la sesión de todos los usuarios activos que no la cerraron.</span><span class="sxs-lookup"><span data-stu-id="32cf4-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="32cf4-122">Los usuarios pueden volver a iniciar sesión inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="32cf4-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="32cf4-123">**Cerrar inmediatamente la sesión de los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="32cf4-123">**Sign users out immediately**.</span></span> <span data-ttu-id="32cf4-124">Tan pronto como finaliza la actualización de hello, cerrar todos los usuarios automáticamente sin previo aviso.</span><span class="sxs-lookup"><span data-stu-id="32cf4-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="32cf4-125">Si elige esta opción, los usuarios pueden perder datos.</span><span class="sxs-lookup"><span data-stu-id="32cf4-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="32cf4-126">Sin embargo, puede volver a conectar toohello aplicación inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="32cf4-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="32cf4-127">Haga clic en actualización de hello marca de verificación toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="32cf4-127">Click hello check mark toostart hello update.</span></span>

