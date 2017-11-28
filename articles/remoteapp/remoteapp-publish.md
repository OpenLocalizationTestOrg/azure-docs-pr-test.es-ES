---
title: "Publicación de una aplicación en Azure RemoteApp | Microsoft Docs"
description: "Obtenga información sobre cómo publicar aplicaciones y recursos de Azure RemoteApp."
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
ms.openlocfilehash: 4565fa498dbadd0601004c73bfee5171efe1fad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-publish-an-app-in-remoteapp"></a><span data-ttu-id="923cb-103">Cómo publicar una aplicación en RemoteApp</span><span class="sxs-lookup"><span data-stu-id="923cb-103">How to publish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="923cb-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="923cb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="923cb-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="923cb-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="923cb-106">Después de crear la colección de RemoteApp, deberá publicar las aplicaciones o los recursos que quiere que estén disponibles para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="923cb-106">After you create your RemoteApp collection, you need to publish the apps or resources that you want to make available for your users.</span></span> <span data-ttu-id="923cb-107">Las imágenes de plantilla proporcionadas con la suscripción solo tienen algunas aplicaciones publicadas de forma predeterminada. Para compartir las otras aplicaciones, debe publicarlas.</span><span class="sxs-lookup"><span data-stu-id="923cb-107">The template images provided with your subscription only have a few apps published by default - to share the other apps, you need to publish them.</span></span>

> [!NOTE]
> <span data-ttu-id="923cb-108">¿Necesita actualizar una aplicación?</span><span class="sxs-lookup"><span data-stu-id="923cb-108">Do you need to update an app?</span></span> <span data-ttu-id="923cb-109">Necesitará [actualizar la imagen](remoteapp-update.md) primero.</span><span class="sxs-lookup"><span data-stu-id="923cb-109">You'll need to [update the image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="923cb-110">En la pestaña **Publicación** del portal, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="923cb-110">On the **Publishing** tab in the portal, click **Publish**.</span></span> <span data-ttu-id="923cb-111">Puede agregar una aplicación desde el menú **Inicio** de la imagen de plantilla o proporcionar la ruta de acceso donde está instalada la aplicación en la imagen de plantilla.</span><span class="sxs-lookup"><span data-stu-id="923cb-111">You can either add an app from your template image's **Start** menu or provide the path to where the app is installed on the template image.</span></span> <span data-ttu-id="923cb-112">Si opta por agregar desde el menú **Inicio** , elija en la lista la aplicación que va a publicar.</span><span class="sxs-lookup"><span data-stu-id="923cb-112">If you choose to add from the **Start** menu, choose the app to publish from the list.</span></span> <span data-ttu-id="923cb-113">Si elige proporcionar la ruta de acceso a la aplicación, escriba un nombre para la aplicación y la ruta de acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="923cb-113">If you choose to provide the path to the app, enter a name for the app and the path to the app.</span></span> <span data-ttu-id="923cb-114">Use variables en la ruta de acceso; por ejemplo, %systemdrive% en lugar de c:\".</span><span class="sxs-lookup"><span data-stu-id="923cb-114">Use variables in the path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="923cb-115">Si quiere agregar la aplicación desde el menú **Inicio**, debe haber *agregado esa aplicación al menú **Inicio** en la imagen de plantilla.*</span><span class="sxs-lookup"><span data-stu-id="923cb-115">If you want to add your app from the **Start** menu, you need to have *added that app to the **Start** menu on your template image.*</span></span> <span data-ttu-id="923cb-116">De lo contrario, RemoteApp solo verá lo que *está* en el menú **Inicio** y usted se confundirá.</span><span class="sxs-lookup"><span data-stu-id="923cb-116">Otherwise, RemoteApp will only see what *is* on the **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="923cb-117">Para asegurarse de que la aplicación se encuentra en el menú **Inicio**, coloque un archivo de acceso directo (**.lnk**) dentro de la carpeta %systemdrive%\ProgramData\Microsoft\Windows\Menú Inicio\Programas.</span><span class="sxs-lookup"><span data-stu-id="923cb-117">To make sure your app is in the **Start** menu, place a shortcut file - **.lnk** - inside the %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="923cb-118">Si olvidó agregar la aplicación al menú **Inicio** al crear la plantilla, tiene la posibilidad de agregar la ruta de acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="923cb-118">If you forgot to add the app to the **Start** menu when you created the template, choose to add the path to the app.</span></span> <span data-ttu-id="923cb-119">(O volver a crear la imagen de plantilla, pero supone algo más de trabajo).</span><span class="sxs-lookup"><span data-stu-id="923cb-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

