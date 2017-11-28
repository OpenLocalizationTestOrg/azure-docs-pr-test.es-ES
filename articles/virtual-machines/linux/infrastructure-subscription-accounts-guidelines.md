---
title: "Suscripción y cuenta para VM de Linux en Azure| Microsoft Docs"
description: "Obtenga información sobre las instrucciones de implementación y diseño clave para las suscripciones y cuentas de Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 19695a9960d8e8f0dfca4bf0ca10761fe6ae7ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="90bc6-103">Directrices de suscripción y cuentas de Azure para máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="90bc6-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="90bc6-104">Este artículo se centra en conocer cómo enfocar la administración de cuentas y suscripciones a medida que crece su entorno y su base de usuarios.</span><span class="sxs-lookup"><span data-stu-id="90bc6-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="90bc6-105">Instrucciones de implementación de suscripciones y cuentas</span><span class="sxs-lookup"><span data-stu-id="90bc6-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="90bc6-106">Decisiones:</span><span class="sxs-lookup"><span data-stu-id="90bc6-106">Decisions:</span></span>

* <span data-ttu-id="90bc6-107">¿Qué conjunto de suscripciones y cuentas necesita para hospedar su infraestructura o carga de trabajo de TI?</span><span class="sxs-lookup"><span data-stu-id="90bc6-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span></span>
* <span data-ttu-id="90bc6-108">¿Cómo sería la jerarquía para adaptarse a su organización?</span><span class="sxs-lookup"><span data-stu-id="90bc6-108">How to break down the hierarchy to fit your organization?</span></span>

<span data-ttu-id="90bc6-109">Tareas:</span><span class="sxs-lookup"><span data-stu-id="90bc6-109">Tasks:</span></span>

* <span data-ttu-id="90bc6-110">Definir la jerarquía de organización lógica que desee administrar desde un nivel de suscripción.</span><span class="sxs-lookup"><span data-stu-id="90bc6-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span></span>
* <span data-ttu-id="90bc6-111">Definir las cuentas y las suscripciones necesarias de cada cuenta para que se correspondan con esta jerarquía lógica.</span><span class="sxs-lookup"><span data-stu-id="90bc6-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="90bc6-112">Cree el conjunto de suscripciones y cuentas usando su convención de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="90bc6-112">Create the set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="90bc6-113">Suscripciones y cuentas </span><span class="sxs-lookup"><span data-stu-id="90bc6-113">Subscriptions and accounts</span></span>
<span data-ttu-id="90bc6-114">Para trabajar con Azure, necesita una o más suscripciones a Azure.</span><span class="sxs-lookup"><span data-stu-id="90bc6-114">To work with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="90bc6-115">Existen recursos como redes o máquinas virtuales en esas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="90bc6-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="90bc6-116">Los clientes empresariales suelen tener una inscripción Enterprise, que es el recurso de nivel superior en la jerarquía y está asociado a una o varias cuentas.</span><span class="sxs-lookup"><span data-stu-id="90bc6-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span></span>
* <span data-ttu-id="90bc6-117">Para los consumidores y clientes que no tienen una inscripción Enterprise, el recurso de nivel superior es la cuenta.</span><span class="sxs-lookup"><span data-stu-id="90bc6-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span></span>
* <span data-ttu-id="90bc6-118">Las suscripciones están asociadas a las cuentas y puede haber una o más suscripciones por cuenta.</span><span class="sxs-lookup"><span data-stu-id="90bc6-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="90bc6-119">Azure registra la información de facturación por suscripción.</span><span class="sxs-lookup"><span data-stu-id="90bc6-119">Azure records billing information at the subscription level.</span></span>

<span data-ttu-id="90bc6-120">Debido al límite de dos niveles de jerarquía en la relación de cuenta/suscripción, es importante adaptar la convención de nomenclatura de las cuentas y las suscripciones a las necesidades de facturación.</span><span class="sxs-lookup"><span data-stu-id="90bc6-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span></span> <span data-ttu-id="90bc6-121">Por ejemplo, si una empresa internacional usa Azure, puede optar por tener una cuenta por región y administrar las suscripciones a nivel regional:</span><span class="sxs-lookup"><span data-stu-id="90bc6-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="90bc6-122">Por ejemplo, podría usar esta estructura:</span><span class="sxs-lookup"><span data-stu-id="90bc6-122">For instance, you might use the following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="90bc6-123">Si una región decide tener más de una suscripción asociada a un grupo determinado, la convención de nomenclatura debe incorporar un método para codificar los datos adicionales del nombre de cuenta o de suscripción.</span><span class="sxs-lookup"><span data-stu-id="90bc6-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span></span> <span data-ttu-id="90bc6-124">Esta organización permite manipular los datos de facturación para generar los nuevos niveles de jerarquía durante los informes de facturación:</span><span class="sxs-lookup"><span data-stu-id="90bc6-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="90bc6-125">La organización podría tener un aspecto similar al del siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="90bc6-125">The organization could look like the following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="90bc6-126">Microsoft proporciona una facturación detallada a través de un archivo descargable para una sola cuenta o para todas las cuentas de un contrato Enterprise.</span><span class="sxs-lookup"><span data-stu-id="90bc6-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90bc6-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90bc6-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

