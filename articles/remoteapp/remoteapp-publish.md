---
title: "una aplicación en Azure RemoteApp aaaPublish | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toopublish las aplicaciones y recursos de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="99f95-103">¿Cómo toopublish una aplicación de RemoteApp</span><span class="sxs-lookup"><span data-stu-id="99f95-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="99f95-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="99f95-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="99f95-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="99f95-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="99f95-106">Después de crear la colección de RemoteApp, necesitará toopublish Hola aplicaciones o recursos que desee toomake disponible para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="99f95-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="99f95-107">Hello imágenes de plantilla proporcionadas con la suscripción solo tienen unas pocas aplicaciones publicadas de forma predeterminada, tooshare Hola otras aplicaciones, necesita toopublish ellos.</span><span class="sxs-lookup"><span data-stu-id="99f95-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="99f95-108">¿Necesita tooupdate una aplicación?</span><span class="sxs-lookup"><span data-stu-id="99f95-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="99f95-109">Necesitará demasiado[actualización Hola imagen](remoteapp-update.md) primero.</span><span class="sxs-lookup"><span data-stu-id="99f95-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="99f95-110">En hello **publicación** , haga clic en el portal de hello **publicar**.</span><span class="sxs-lookup"><span data-stu-id="99f95-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="99f95-111">Puede agregar una aplicación de la imagen de plantilla **iniciar** menú o proporcionar aplicación Hola de hello ruta de acceso toowhere está instalado en la imagen de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="99f95-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="99f95-112">Si elige tooadd de hello **iniciar** menú, elija hello toopublish de aplicación de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="99f95-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="99f95-113">Si elige tooprovide Hola ruta de acceso toohello aplicación, escriba un nombre para la aplicación hello y aplicación de toohello de ruta de acceso de hello.</span><span class="sxs-lookup"><span data-stu-id="99f95-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="99f95-114">Usar variables en la ruta de acceso de hello - por ejemplo, "% systemdrive %" en lugar de "c:\".</span><span class="sxs-lookup"><span data-stu-id="99f95-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="99f95-115">Si desea que tooadd la aplicación de hello **iniciar** menú, necesita toohave *agrega esa aplicación toohello **iniciar** menú en la imagen de plantilla.*</span><span class="sxs-lookup"><span data-stu-id="99f95-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="99f95-116">En caso contrario, RemoteApp solo verá qué *es* en hello **iniciar** menú y se confundirse.</span><span class="sxs-lookup"><span data-stu-id="99f95-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="99f95-117">toomake seguro de que la aplicación está en hello **iniciar** menú, coloque un archivo de acceso directo - **.lnk** : dentro de la carpeta de hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs.</span><span class="sxs-lookup"><span data-stu-id="99f95-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="99f95-118">Si ha olvidado tooadd Hola aplicación toohello **iniciar** menú cuando se creó la plantilla de hello, elija aplicación toohello de tooadd hello ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="99f95-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="99f95-119">(O volver a crear la imagen de plantilla, pero supone algo más de trabajo).</span><span class="sxs-lookup"><span data-stu-id="99f95-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

