---
title: "Información de tamaño para una red virtual de Azure RemoteApp | Microsoft Docs"
description: "Obtenga información acerca de los requisitos de direcciones IP de Azure RemoteApp cuando se ejecuta con una red virtual."
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
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="2bf62-103">Información de tamaño para una red virtual de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="2bf62-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2bf62-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="2bf62-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="2bf62-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="2bf62-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="2bf62-106">Al usar Azure RemoteApp con una red virtual (VNET), RemoteApp usa direcciones IP dentro de la subred.</span><span class="sxs-lookup"><span data-stu-id="2bf62-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet.</span></span> <span data-ttu-id="2bf62-107">En función de la escala de su servicio de RemoteApp, deberá asegurarse de que la subred tiene suficientes direcciones IP disponibles para las máquinas virtuales de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2bf62-107">Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="2bf62-108">Aunque esta guía sobre tamaños no es perfecta dado el modo en que RemoteApp aumenta y disminuye dinámicamente la capacidad de las máquinas virtuales dentro de una colección, le permitirá calcular el intervalo de subredes.</span><span class="sxs-lookup"><span data-stu-id="2bf62-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="2bf62-109">Esto es especialmente importante ya que, una vez esté vigente el servicio de RemoteApp en una red virtual, no se puede aumentar el tamaño de la subred sin quitar RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="2bf62-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="2bf62-110">Para cada colección de RemoteApp que desee ejecutar a su capacidad máxima, debe tener 100 direcciones IP disponibles.</span><span class="sxs-lookup"><span data-stu-id="2bf62-110">For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="2bf62-111">Por ejemplo, si tiene una colección de RemoteApp en el plan Estándar y desea tener como máximo 500 usuarios, debe tener 100 direcciones IP para esa colección.</span><span class="sxs-lookup"><span data-stu-id="2bf62-111">For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="2bf62-112">Del mismo modo, necesita 100 direcciones IP para una colección de RemoteApp en el plan Básico que tenga 800 usuarios.</span><span class="sxs-lookup"><span data-stu-id="2bf62-112">Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users.</span></span> <span data-ttu-id="2bf62-113">Si planea tener una cantidad inferior de usuarios (por debajo del valor máximo), puede reducir las direcciones IP que se necesitan por colección.</span><span class="sxs-lookup"><span data-stu-id="2bf62-113">If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection.</span></span> <span data-ttu-id="2bf62-114">El requisito de tamaño mínimo de subred es de 30 direcciones IP (/27).</span><span class="sxs-lookup"><span data-stu-id="2bf62-114">The minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="2bf62-115">Consulte la siguiente información para asegurarse de que la red virtual está configurada y funciona correctamente:</span><span class="sxs-lookup"><span data-stu-id="2bf62-115">Check out the following information to make sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="2bf62-116">Migración de una red virtual personal a una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="2bf62-116">Migrate from a personal VNET to an Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="2bf62-117">Validación de la red virtual de Azure para su uso con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="2bf62-117">Validate the Azure VNET to use with Azure RemoteApp</span></span>](remoteapp-vnet.md)

