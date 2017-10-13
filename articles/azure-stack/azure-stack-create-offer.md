---
title: "Creación de una oferta en Azure Stack | Microsoft Docs"
description: Como administrador de la nube, aprenda a crear una oferta para los usuarios de Azure Stack.
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 96b080a4-a9a5-407c-ba54-111de2413d59
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 269a6106f657536ba74be366f842b2f9cd86c5dc
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="19760-103">Creación de una oferta en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="19760-103">Create an offer in Azure Stack</span></span>

<span data-ttu-id="19760-104">*Se aplica a: Sistemas integrados de Azure Stack y Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="19760-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="19760-105">Las [ofertas](azure-stack-key-features.md) son grupos de uno o varios planes que los proveedores presentan a los usuarios para que estos los compren o se suscriban a ellos.</span><span class="sxs-lookup"><span data-stu-id="19760-105">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to users to purchase or subscribe to.</span></span> <span data-ttu-id="19760-106">Este documento muestra cómo crear una oferta que incluye el [plan que creó](azure-stack-create-plan.md) en el último paso.</span><span class="sxs-lookup"><span data-stu-id="19760-106">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md) in the last step.</span></span> <span data-ttu-id="19760-107">Esta oferta da a los suscriptores la capacidad de aprovisionar máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="19760-107">This offer gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="19760-108">Inicie sesión en el portal de administrador de Azure Stack (https://adminportal.local.azurestack.external) > haga clic en **New** > **Tenant Offers + Plans** >  **Offer** (Nuevo > Ofertas y planes de inquilino).</span><span class="sxs-lookup"><span data-stu-id="19760-108">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="19760-109">En la hoja **Nueva oferta**, rellene el **Nombre para mostrar** y el **Nombre de recurso** y, a continuación, seleccione un **Grupo de recursos** nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="19760-109">In the **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="19760-110">El Nombre para mostrar es el nombre descriptivo de la oferta y es la única información acerca de la oferta que verán los usuarios cuando se suscriban.</span><span class="sxs-lookup"><span data-stu-id="19760-110">The Display Name is the offer's friendly name and is the only information about the offer that the users will see when subscribing.</span></span> <span data-ttu-id="19760-111">Por lo tanto, asegúrese de usar un nombre intuitivo que ayude al usuario a entender lo que incluye la oferta.</span><span class="sxs-lookup"><span data-stu-id="19760-111">Therefore, be sure to use an intuitive name that helps the user understand what comes with the offer.</span></span> <span data-ttu-id="19760-112">Solo el administrador puede ver el nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="19760-112">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="19760-113">Es el nombre que usan los administradores para trabajar con la oferta como un recurso de Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="19760-113">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="19760-114">Haga clic en **Planes de base** y, en la hoja **Plan**, seleccione los planes que desea incluir en la oferta y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="19760-114">Click **Base plans** and, in the **Plan** blade, select the plans you want to include in the offer, and then click **Select**.</span></span> <span data-ttu-id="19760-115">Haga clic en **Crear** para crear la oferta.</span><span class="sxs-lookup"><span data-stu-id="19760-115">Click **Create** to create the offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="19760-116">Haga clic en **Todos los recursos**, busque la nueva oferta, haga clic en la nueva oferta, haga clic en **Cambiar estado** y, a continuación, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="19760-116">Click **All Resources**, search for your new offer, click on the new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="19760-117">Las ofertas deben hacerse públicas para que los usuarios obtengan la vista completa cuando se suscriban.</span><span class="sxs-lookup"><span data-stu-id="19760-117">Offers must be made public for users to get the full view when subscribing.</span></span> <span data-ttu-id="19760-118">Las ofertas pueden ser:</span><span class="sxs-lookup"><span data-stu-id="19760-118">Offers can be:</span></span>

* <span data-ttu-id="19760-119">**Públicas**: visibles para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="19760-119">**Public**: Visible to users.</span></span>
* <span data-ttu-id="19760-120">**Privadas**: solo son visibles para los administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="19760-120">**Private**: Only visible to the cloud administrators.</span></span> <span data-ttu-id="19760-121">Resulta útil durante la elaboración del plan o la oferta, o si el administrador de la nube desea aprobar todas las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="19760-121">Useful while drafting the plan or offer, or if the cloud administrator wants to approve every subscription.</span></span>
* <span data-ttu-id="19760-122">**Retirados**: cerrados a nuevos suscriptores.</span><span class="sxs-lookup"><span data-stu-id="19760-122">**Decommissioned**: Closed to new subscribers.</span></span> <span data-ttu-id="19760-123">El administrador de la nube puede usar las ofertas y planes retirados para evitar futuras suscripciones, pero dejar intactos los suscriptores actuales.</span><span class="sxs-lookup"><span data-stu-id="19760-123">The cloud administrator can use decommissioned to prevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="19760-124">Los cambios en la oferta no son inmediatamente visibles para el usuario.</span><span class="sxs-lookup"><span data-stu-id="19760-124">Changes to the offer are not immediately visible to the user.</span></span> <span data-ttu-id="19760-125">Para visualizar los cambios, es posible que tenga que cerrar sesión e iniciarla para ver la nueva suscripción en el "selector de suscripciones" al crear recursos o grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="19760-125">To see the changes, you might have to logout/login to see the new subscription in the “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="19760-126">También puede crear ofertas, planes y cuotas predeterminadas mediante PowerShell, como se explica en el [archivo Léame del administrador de servicios de Azure Stack](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span><span class="sxs-lookup"><span data-stu-id="19760-126">You can also create default offers, plans, and quotas by using PowerShell as explained in the [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="19760-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19760-127">Next steps</span></span>
[<span data-ttu-id="19760-128">Suscripción a una oferta y aprovisionamiento de una máquina virtual en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="19760-128">Subscribe to an offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
