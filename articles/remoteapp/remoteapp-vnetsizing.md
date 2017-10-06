---
title: "información de aaaSizing para una red virtual en Azure RemoteApp | Documentos de Microsoft"
description: "Obtenga información acerca de los requisitos de dirección IP de Hola para ejecutar con una red virtual de Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="db724-103">Información de tamaño para una red virtual de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="db724-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="db724-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="db724-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="db724-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="db724-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="db724-106">Cuando usas Azure RemoteApp con una red virtual (VNET), RemoteApp usa direcciones IP dentro de la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="db724-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within hello subnet.</span></span> <span data-ttu-id="db724-107">En función de la escala de Hola de su servicio de RemoteApp, debe tooensure que la subred tiene suficientes direcciones IP disponibles para las máquinas virtuales de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="db724-107">Based on hello scale of your RemoteApp service, you need tooensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="db724-108">Aunque esta guía sobre tamaños no es perfecta dado el modo en que RemoteApp aumenta y disminuye dinámicamente la capacidad de las máquinas virtuales dentro de una colección, le permitirá calcular el intervalo de subredes.</span><span class="sxs-lookup"><span data-stu-id="db724-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="db724-109">Esto es especialmente importante que, una vez que un servicio de RemoteApp se coloca en una red virtual, no se puede aumentar el tamaño de la subred de hello sin quitar RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="db724-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase hello subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="db724-110">Para cada colección de RemoteApp que quiere que toorun en su capacidad máxima, debe tener 100 direcciones IP disponibles.</span><span class="sxs-lookup"><span data-stu-id="db724-110">For each RemoteApp collection that you want toorun at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="db724-111">Por ejemplo, si tiene una colección de RemoteApp en plan estándar de Hola y desea toohave Hola máximo 500 usuarios, debe tener 100 direcciones IP para esa colección.</span><span class="sxs-lookup"><span data-stu-id="db724-111">For example, if you have one RemoteApp collection in hello Standard plan and you want toohave hello maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="db724-112">De igual forma, necesita 100 direcciones IP para una colección de RemoteApp de plan básico Hola con 800 usuarios.</span><span class="sxs-lookup"><span data-stu-id="db724-112">Similarly, you need 100 IP addresses for a RemoteApp collection in hello Basic plan that has 800 users.</span></span> <span data-ttu-id="db724-113">Si tiene previsto toohave menos usuarios (menor que Hola máximo), puede reducir las direcciones IP Hola necesarios por la colección.</span><span class="sxs-lookup"><span data-stu-id="db724-113">If you plan toohave fewer users (less than hello maximum), you can reduce hello IP addresses needed per collection.</span></span> <span data-ttu-id="db724-114">requisito de tamaño de Hello subred mínimo es 30 direcciones IP (/ 27).</span><span class="sxs-lookup"><span data-stu-id="db724-114">hello minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="db724-115">Hola sigue toomake de información que la red virtual está configurada y funciona correctamente, consulte:</span><span class="sxs-lookup"><span data-stu-id="db724-115">Check out hello following information toomake sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="db724-116">Migrar desde una tooan de red virtual personal red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="db724-116">Migrate from a personal VNET tooan Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="db724-117">Validar hello toouse de red virtual de Azure con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="db724-117">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>](remoteapp-vnet.md)

