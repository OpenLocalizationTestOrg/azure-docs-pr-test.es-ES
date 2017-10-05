---
title: "Solución de problemas con las colecciones en la nube de RemoteApp: creación | Microsoft Docs"
description: "Obtenga información sobre cómo solucionar problemas con la creación de las colecciones en la nube de RemoteApp"
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
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="3da54-103">Solución de problemas de creación de colecciones en la nube de RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3da54-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3da54-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="3da54-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3da54-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="3da54-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3da54-106">Si tiene problemas para crear una colección en la nube, consulte la siguiente información.</span><span class="sxs-lookup"><span data-stu-id="3da54-106">If you are having problems creating a cloud collection, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="3da54-107">La imagen no es válida</span><span class="sxs-lookup"><span data-stu-id="3da54-107">Your image is invalid</span></span>
<span data-ttu-id="3da54-108">Si ve un mensaje como "GoldImageInvalid" cuando esté esperando a que Azure aprovisione la colección, la imagen de plantilla no cumple [los requisitos definidos para la imagen](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="3da54-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="3da54-109">Por lo tanto, consulte los [requisitos](remoteapp-imagereqs.md), corrija la imagen y pruebe a crear la colección de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3da54-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="common-errors-seen-in-the-azure-management-portal"></a><span data-ttu-id="3da54-110">Errores comunes vistos en el Portal de administración de Azure</span><span class="sxs-lookup"><span data-stu-id="3da54-110">Common errors seen in the Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="3da54-111">Las colecciones en la nube a menudo presentan errores durante la creación debido a que se usan imágenes personalizadas.</span><span class="sxs-lookup"><span data-stu-id="3da54-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="3da54-112">Si ve uno de los anteriores errores y usa una imagen personalizada para crear la colección, revise lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3da54-112">If you see one of the above errors and you are using a custom image to create the collection, please check the following things:</span></span>

* <span data-ttu-id="3da54-113">Asegúrese de que la imagen personalizada que cargó cumple con los requisitos de imagen.</span><span class="sxs-lookup"><span data-stu-id="3da54-113">Ensure that the custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="3da54-114">Con frecuencia, el problema común es que la imagen no está preparada con sysprep correctamente.</span><span class="sxs-lookup"><span data-stu-id="3da54-114">Most often the common problem is that the image was not properly syspreped.</span></span>  
* <span data-ttu-id="3da54-115">Compruebe que la imagen puede arrancar dentro de Hyper-V o intente crear una máquina virtual de IAAS directamente en su suscripción de Azure con la imagen.</span><span class="sxs-lookup"><span data-stu-id="3da54-115">Verify the image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using the image.</span></span> <span data-ttu-id="3da54-116">Si la máquina virtual no arranca y no se inicia, esto normalmente indica que la imagen personalizada no se preparó correctamente.</span><span class="sxs-lookup"><span data-stu-id="3da54-116">If the VM fails to boot and not start, then this usually indicates that the custom image was not prepared correctly.</span></span>  <span data-ttu-id="3da54-117">Compruebe que la imagen personalizada se creó según lo establecido en Creación de una imagen de plantilla personalizada para RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3da54-117">Verify the custom image was built following the How to create a custom template image for RemoteApp</span></span>

<span data-ttu-id="3da54-118">Si usa una de las imágenes de Microsoft incluidas en su suscripción, intente crear nuevamente la colección.</span><span class="sxs-lookup"><span data-stu-id="3da54-118">If you are using one of the Microsoft images included with your subscription, try to create the collection again.</span></span> <span data-ttu-id="3da54-119">Si el problema persiste, póngase en contacto con Soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3da54-119">If the issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="3da54-120">Si recibe este error, normalmente significa que ha actualizado a una cuenta de pago pero intenta usar una imagen proporcionada por Microsoft que solo es válida durante el modo de prueba del servicio.</span><span class="sxs-lookup"><span data-stu-id="3da54-120">If you see this error this usually means that you been upgraded to a paid account but you are trying to use a Microsoft provided image that is valid only during the trial mode of the service.</span></span> <span data-ttu-id="3da54-121">En este caso, intente crear nuevamente la colección en la nube, pero asegúrese de especificar la imagen correcta.</span><span class="sxs-lookup"><span data-stu-id="3da54-121">In this case, try to create your cloud collection again, but be sure to specify the correct image.</span></span>

