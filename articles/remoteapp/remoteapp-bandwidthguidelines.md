---
title: ancho de banda de aaaAzure RemoteApp red - directrices generales | Documentos de Microsoft
description: "Entender algunas directrices básicas del ancho de banda de red para sus colecciones y aplicaciones de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="1b099-103">Ancho de banda de red de Azure RemoteApp: directrices generales (si no puede probarlo usted mismo)</span><span class="sxs-lookup"><span data-stu-id="1b099-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1b099-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="1b099-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1b099-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="1b099-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1b099-106">Si no tiene Hola de tiempo o la funcionalidad de Hola toorun [pruebas de ancho de banda de red](remoteapp-bandwidthtests.md) de RemoteApp de Azure, estas son algunas directrices bastante genéricas que pueden ayudarle a calcular el ancho de banda por usuario.</span><span class="sxs-lookup"><span data-stu-id="1b099-106">If you do not have hello time or capability toorun hello [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="1b099-107">Si tiene una combinación de estos escenarios, se desaconseja algo menor que (o igual que) 10 MB/s Hola ancho de banda de red de mínimo de las aplicaciones actuales en un entorno remoto conectado a Internet.</span><span class="sxs-lookup"><span data-stu-id="1b099-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as hello MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="1b099-108">(Aunque, como se explicó anteriormente, esto no garantizará una experiencia de usuario superior a la media).</span><span class="sxs-lookup"><span data-stu-id="1b099-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="1b099-109">PowerPoint de tipo complejo y de tipo simple</span><span class="sxs-lookup"><span data-stu-id="1b099-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="1b099-110">Azure RemoteApp funciona mejor con una red LAN de 100 MB.</span><span class="sxs-lookup"><span data-stu-id="1b099-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="1b099-111">En Hola 10 MB/perfil de red s, vibración por encima de 120 ms una vez más del 5%, usuario Hola verán una experiencia promedio.</span><span class="sxs-lookup"><span data-stu-id="1b099-111">At hello 10 MB/s network profile, when jitter above 120 ms is more than 5%, hello user will see an average experience.</span></span> <span data-ttu-id="1b099-112">En Hola de 1 MB/s diferentes es terribles - por ejemplo, en una presentación con diapositivas, Hola el usuario puede no ver transiciones animadas en absoluto porque se omiten los fotogramas.</span><span class="sxs-lookup"><span data-stu-id="1b099-112">At 1 MB/s hello different is glaring - for example, in a slide show, hello user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="1b099-113">Internet Explorer, PDF mixto, PDF, texto</span><span class="sxs-lookup"><span data-stu-id="1b099-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="1b099-114">Perfil de red de 10 MB/s es cerrar tooLAN en casi todos los aspectos.</span><span class="sxs-lookup"><span data-stu-id="1b099-114">10 MB/s network profile is close tooLAN in most aspects.</span></span> <span data-ttu-id="1b099-115">1 MB/s proporcionará una experiencia de Aceptar, aunque puede haber algunas vibración cuando un usuario se desplaza mientras hay imágenes en la pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="1b099-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on hello screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="1b099-116">Vídeo Flash (YouTube)</span><span class="sxs-lookup"><span data-stu-id="1b099-116">Flash video (YouTube)</span></span>
<span data-ttu-id="1b099-117">LAN de 100 MB/s proporciona mejor experiencia de hello, mientras que 10 MB/s es aceptable (es decir, hacer frente a la velocidad de fotogramas de hello, pero vibración aumenta).</span><span class="sxs-lookup"><span data-stu-id="1b099-117">100 MB/s LAN provides hello best experience, while 10 MB/s is acceptable (meaning we keep up with hello frame rate but jitter increases).</span></span> <span data-ttu-id="1b099-118">A 1 MB/s, la vibración es muy alta y apreciable.</span><span class="sxs-lookup"><span data-stu-id="1b099-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="1b099-119">Escritura en Word (entrada remota de Word)</span><span class="sxs-lookup"><span data-stu-id="1b099-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="1b099-120">Se trata de un escenario de uso de ancho de banda bajo.</span><span class="sxs-lookup"><span data-stu-id="1b099-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="1b099-121">A 256 KB/s, proporcionamos una experiencia tan buena como la de la red LAN.</span><span class="sxs-lookup"><span data-stu-id="1b099-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="1b099-122">Más información</span><span class="sxs-lookup"><span data-stu-id="1b099-122">Learn more</span></span>
* [<span data-ttu-id="1b099-123">Cálculo aproximado del uso del ancho de banda de red de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1b099-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="1b099-124">Azure RemoteApp: ¿cómo funcionan el ancho de banda de red y la calidad de la experiencia conjuntamente?</span><span class="sxs-lookup"><span data-stu-id="1b099-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="1b099-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios (Azure RemoteApp: probar su uso de ancho de banda de red con algunos escenarios comunes)</span><span class="sxs-lookup"><span data-stu-id="1b099-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

