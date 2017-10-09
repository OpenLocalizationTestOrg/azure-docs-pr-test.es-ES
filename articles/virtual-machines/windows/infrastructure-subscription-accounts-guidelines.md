---
title: "aaaSubscription y cuentas para máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello diseño e implementación de las instrucciones clave para las suscripciones y cuentas en Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a><span data-ttu-id="545fc-103">Directrices de suscripción y cuentas de Azure para máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="545fc-103">Azure subscription and accounts guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="545fc-104">En este artículo se centra en describir cómo tooapproach suscripción y administración de cuentas como su entorno y la base de usuarios crece.</span><span class="sxs-lookup"><span data-stu-id="545fc-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="545fc-105">Instrucciones de implementación de suscripciones y cuentas</span><span class="sxs-lookup"><span data-stu-id="545fc-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="545fc-106">Decisiones:</span><span class="sxs-lookup"><span data-stu-id="545fc-106">Decisions:</span></span>

* <span data-ttu-id="545fc-107">¿Qué conjunto de suscripciones y cuentas ¿necesita toohost su infraestructura o la carga de trabajo de TI?</span><span class="sxs-lookup"><span data-stu-id="545fc-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="545fc-108">¿Cómo toobreak hacia abajo Hola jerarquía toofit su organización?</span><span class="sxs-lookup"><span data-stu-id="545fc-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="545fc-109">Tareas:</span><span class="sxs-lookup"><span data-stu-id="545fc-109">Tasks:</span></span>

* <span data-ttu-id="545fc-110">Definir la jerarquía de organización lógica como le gustaría toomanage desde un nivel de suscripción.</span><span class="sxs-lookup"><span data-stu-id="545fc-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="545fc-111">toomatch esta jerarquía lógica, definir cuentas Hola necesarias y las suscripciones en cada cuenta.</span><span class="sxs-lookup"><span data-stu-id="545fc-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="545fc-112">Crear conjunto de Hola de suscripciones y cuentas que utilizan la convención de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="545fc-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="545fc-113">Suscripciones y cuentas </span><span class="sxs-lookup"><span data-stu-id="545fc-113">Subscriptions and accounts</span></span>
<span data-ttu-id="545fc-114">toowork con Azure, necesita una o varias suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="545fc-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="545fc-115">Existen recursos como redes o máquinas virtuales en esas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="545fc-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="545fc-116">Los clientes empresariales suelen tengan una inscripción Enterprise, que es Hola recurso de más arriba en la jerarquía de Hola y está asociado tooone o más cuentas.</span><span class="sxs-lookup"><span data-stu-id="545fc-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="545fc-117">Para los consumidores y los clientes sin una inscripción Enterprise, recursos de nivel superior de hello es la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="545fc-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="545fc-118">Las suscripciones son tooaccounts asociado, y puede haber una o varias suscripciones por cuenta.</span><span class="sxs-lookup"><span data-stu-id="545fc-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="545fc-119">Registros de Azure información en el nivel de suscripción de Hola de facturación.</span><span class="sxs-lookup"><span data-stu-id="545fc-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="545fc-120">Pagar toohello el límite de niveles de jerarquía de dos de la relación de suscripción o cuenta de hello, es importante tooalign Hola convención de nomenclatura toohello suscripciones y cuentas de facturación necesidades.</span><span class="sxs-lookup"><span data-stu-id="545fc-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="545fc-121">Por ejemplo, si una empresa global usa Azure, puede elegir cuenta toohave uno por cada región y se administran las suscripciones en Hola nivel región:</span><span class="sxs-lookup"><span data-stu-id="545fc-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="545fc-122">Por ejemplo, puede usar Hola siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="545fc-122">For instance, you might use hello following structure:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="545fc-123">Si una región decide toohave más de grupo determinado de una suscripción tooa asociado, convención de nomenclatura de hello debe incorporar una tooencode de manera Hola datos adicionales en la cuenta de Hola o nombre de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="545fc-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="545fc-124">Esta organización permite corporativos facturación datos toogenerate Hola nuevos niveles de jerarquía durante la facturación de informes:</span><span class="sxs-lookup"><span data-stu-id="545fc-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="545fc-125">organización de Hello podría verse como el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="545fc-125">hello organization could look like hello following example:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="545fc-126">Microsoft proporciona una facturación detallada a través de un archivo descargable para una sola cuenta o para todas las cuentas de un contrato Enterprise.</span><span class="sxs-lookup"><span data-stu-id="545fc-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="545fc-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="545fc-127">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

