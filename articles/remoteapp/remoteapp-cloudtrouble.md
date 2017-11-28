---
title: "colecciones de nube de RemoteApp aaaTroubleshoot - creación | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot RemoteApp en la nube de errores de creación de colección"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="7e4a4-103">Solución de problemas de creación de colecciones en la nube de RemoteApp</span><span class="sxs-lookup"><span data-stu-id="7e4a4-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7e4a4-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="7e4a4-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="7e4a4-106">Si tiene problemas para crear una colección en la nube, consulte Hola siguiente información.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-106">If you are having problems creating a cloud collection, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="7e4a4-107">La imagen no es válida</span><span class="sxs-lookup"><span data-stu-id="7e4a4-107">Your image is invalid</span></span>
<span data-ttu-id="7e4a4-108">Si ve un mensaje como "GoldImageInvalid" cuando se está esperando tooprovision Azure la colección, significa que la imagen de plantilla no cumple con hello [define los requisitos de la imagen](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="7e4a4-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="7e4a4-109">Por lo tanto, vaya a leerlos [requisitos](remoteapp-imagereqs.md), corrija la imagen e inténtelo de toocreate volver a la colección.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="common-errors-seen-in-hello-azure-management-portal"></a><span data-ttu-id="7e4a4-110">Errores comunes que se muestra en el portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="7e4a4-110">Common errors seen in hello Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="7e4a4-111">Las colecciones en la nube a menudo presentan errores durante la creación debido a que se usan imágenes personalizadas.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="7e4a4-112">Si ve alguno de Hola por encima de los errores y se usa una imagen personalizada toocreate hello, consulte Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="7e4a4-112">If you see one of hello above errors and you are using a custom image toocreate hello collection, please check hello following things:</span></span>

* <span data-ttu-id="7e4a4-113">Asegúrese de que esa imagen personalizada hello cargado cumple los requisitos de imagen.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-113">Ensure that hello custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="7e4a4-114">Con mayor frecuencia problema común de hello es que esa imagen hello no estaba correctamente preparada con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-114">Most often hello common problem is that hello image was not properly syspreped.</span></span>  
* <span data-ttu-id="7e4a4-115">Comprobar la imagen de hello pueda arrancar dentro de Hyper-V o intente crear una VM de IAAS directamente en su suscripción de Azure con imagen Hola.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-115">Verify hello image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using hello image.</span></span> <span data-ttu-id="7e4a4-116">Si se produce un error en la VM de hello tooboot y no se inicia, a continuación, esto normalmente indica que esa imagen personalizada hello no estaba preparada correctamente.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-116">If hello VM fails tooboot and not start, then this usually indicates that hello custom image was not prepared correctly.</span></span>  <span data-ttu-id="7e4a4-117">Compruebe la imagen personalizada de Hola se creó después de hello cómo toocreate una plantilla personalizada de la imagen de RemoteApp</span><span class="sxs-lookup"><span data-stu-id="7e4a4-117">Verify hello custom image was built following hello How toocreate a custom template image for RemoteApp</span></span>

<span data-ttu-id="7e4a4-118">Si está utilizando uno de imágenes de Microsoft de hello incluidas con su suscripción, intente volver a la colección de Hola de toocreate.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-118">If you are using one of hello Microsoft images included with your subscription, try toocreate hello collection again.</span></span> <span data-ttu-id="7e4a4-119">Si no se soluciona el problema de hello, a continuación, póngase en contacto con soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-119">If hello issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="7e4a4-120">Si ve este error normalmente significa que se hayan actualizado tooa pago cuenta pero que está tratando de toouse una imagen de Microsoft proporcionado es válida solo durante el modo de evaluación de hello del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-120">If you see this error this usually means that you been upgraded tooa paid account but you are trying toouse a Microsoft provided image that is valid only during hello trial mode of hello service.</span></span> <span data-ttu-id="7e4a4-121">En este caso, intente toocreate volver a la colección en la nube, pero ser seguro toospecify Hola correcto imagen.</span><span class="sxs-lookup"><span data-stu-id="7e4a4-121">In this case, try toocreate your cloud collection again, but be sure toospecify hello correct image.</span></span>

