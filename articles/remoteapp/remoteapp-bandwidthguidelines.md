---
title: 'Ancho de banda de red de Azure RemoteApp: directrices generales | Microsoft Docs'
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
ms.openlocfilehash: 0b6521cc240556186890f0b797c6d80e431ac4be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="4a961-103">Ancho de banda de red de Azure RemoteApp: directrices generales (si no puede probarlo usted mismo)</span><span class="sxs-lookup"><span data-stu-id="4a961-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4a961-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="4a961-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="4a961-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="4a961-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="4a961-106">Si no tiene el tiempo ni la posibilidad de ejecutar las [pruebas del ancho de banda de red](remoteapp-bandwidthtests.md) para Azure RemoteApp, le presentamos algunas directrices bastante genéricas que pueden ayudarle a calcular el ancho de banda de red por usuario.</span><span class="sxs-lookup"><span data-stu-id="4a961-106">If you do not have the time or capability to run the [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="4a961-107">Si tiene una combinación de estos escenarios, no le recomendamos nada que sea inferior a (o igual a) 10 MB/s como ancho de banda de red mínimo para las aplicaciones modernas conectadas a Internet en un entorno remoto.</span><span class="sxs-lookup"><span data-stu-id="4a961-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as the MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="4a961-108">(Aunque, como se explicó anteriormente, esto no garantizará una experiencia de usuario superior a la media).</span><span class="sxs-lookup"><span data-stu-id="4a961-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="4a961-109">PowerPoint de tipo complejo y de tipo simple</span><span class="sxs-lookup"><span data-stu-id="4a961-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="4a961-110">Azure RemoteApp funciona mejor con una red LAN de 100 MB.</span><span class="sxs-lookup"><span data-stu-id="4a961-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="4a961-111">En el perfil de red de 10 MB/s, cuando la vibración superior a 120 ms representa más de un 5 %, el usuario tendrá una experiencia media.</span><span class="sxs-lookup"><span data-stu-id="4a961-111">At the 10 MB/s network profile, when jitter above 120 ms is more than 5%, the user will see an average experience.</span></span> <span data-ttu-id="4a961-112">A 1 MB/s, la diferencia es evidente. Por ejemplo, en una presentación con diapositivas, el usuario podría no ver las transiciones animadas completamente ya que se omiten los fotogramas.</span><span class="sxs-lookup"><span data-stu-id="4a961-112">At 1 MB/s the different is glaring - for example, in a slide show, the user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="4a961-113">Internet Explorer, PDF mixto, PDF, texto</span><span class="sxs-lookup"><span data-stu-id="4a961-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="4a961-114">Un perfil de red de 10 MB/s se acerca a la red LAN en la mayoría de los aspectos.</span><span class="sxs-lookup"><span data-stu-id="4a961-114">10 MB/s network profile is close to LAN in most aspects.</span></span> <span data-ttu-id="4a961-115">1 MB/s proporcionará una experiencia adecuada, aunque puede haber una cierta vibración cuando un usuario se desplaza mientras hay imágenes en la pantalla.</span><span class="sxs-lookup"><span data-stu-id="4a961-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on the screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="4a961-116">Vídeo Flash (YouTube)</span><span class="sxs-lookup"><span data-stu-id="4a961-116">Flash video (YouTube)</span></span>
<span data-ttu-id="4a961-117">Una red LAN de 100 MB/s proporciona la mejor experiencia, aunque 10 MB/s es aceptable (es decir, mantenemos la velocidad de fotogramas, pero aumenta la vibración).</span><span class="sxs-lookup"><span data-stu-id="4a961-117">100 MB/s LAN provides the best experience, while 10 MB/s is acceptable (meaning we keep up with the frame rate but jitter increases).</span></span> <span data-ttu-id="4a961-118">A 1 MB/s, la vibración es muy alta y apreciable.</span><span class="sxs-lookup"><span data-stu-id="4a961-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="4a961-119">Escritura en Word (entrada remota de Word)</span><span class="sxs-lookup"><span data-stu-id="4a961-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="4a961-120">Se trata de un escenario de uso de ancho de banda bajo.</span><span class="sxs-lookup"><span data-stu-id="4a961-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="4a961-121">A 256 KB/s, proporcionamos una experiencia tan buena como la de la red LAN.</span><span class="sxs-lookup"><span data-stu-id="4a961-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="4a961-122">Más información</span><span class="sxs-lookup"><span data-stu-id="4a961-122">Learn more</span></span>
* [<span data-ttu-id="4a961-123">Cálculo aproximado del uso del ancho de banda de red de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="4a961-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="4a961-124">Azure RemoteApp: ¿cómo funcionan el ancho de banda de red y la calidad de la experiencia conjuntamente?</span><span class="sxs-lookup"><span data-stu-id="4a961-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="4a961-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios (Azure RemoteApp: probar su uso de ancho de banda de red con algunos escenarios comunes)</span><span class="sxs-lookup"><span data-stu-id="4a961-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

