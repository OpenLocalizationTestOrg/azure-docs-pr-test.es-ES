---
title: "Creación de una oferta en Azure Stack | Microsoft Docs"
description: Como administrador de la nube, aprenda a crear una oferta para los inquilinos en Azure Stack.
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
ms.openlocfilehash: 3d7360a1fb1c0cf42d77b3f39bf92c30438c2e01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="904c2-103">Creación de una oferta en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="904c2-103">Create an offer in Azure Stack</span></span>
<span data-ttu-id="904c2-104">Las [Ofertas](azure-stack-key-features.md) son grupos de uno o varios planes que los proveedores presentan a los inquilinos para que estos los compren o se suscriban a ellos.</span><span class="sxs-lookup"><span data-stu-id="904c2-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to tenants to purchase or subscribe to.</span></span> <span data-ttu-id="904c2-105">Este documento muestra cómo crear una oferta que incluye el [plan que creó](azure-stack-create-plan.md) en el último paso.</span><span class="sxs-lookup"><span data-stu-id="904c2-105">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md) in the last step.</span></span> <span data-ttu-id="904c2-106">Esta oferta da a los suscriptores la capacidad de aprovisionar máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="904c2-106">This offer gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="904c2-107">Inicie sesión en el portal de administrador de Azure Stack (https://adminportal.local.azurestack.external) > haga clic en **New** > **Tenant Offers + Plans** >  **Offer** (Nuevo > Ofertas y planes de inquilino).</span><span class="sxs-lookup"><span data-stu-id="904c2-107">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="904c2-108">En la hoja **Nueva oferta**, rellene el **Nombre para mostrar** y el **Nombre de recurso** y, a continuación, seleccione un **Grupo de recursos** nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="904c2-108">In the **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="904c2-109">El Nombre para mostrar es el nombre descriptivo de la oferta y es la única información acerca de la oferta que verán los usuarios cuando se suscriban.</span><span class="sxs-lookup"><span data-stu-id="904c2-109">The Display Name is the offer's friendly name and is the only information about the offer that the users will see when subscribing.</span></span> <span data-ttu-id="904c2-110">Por lo tanto, asegúrese de usar un nombre intuitivo que ayude al usuario a entender lo que incluye la oferta.</span><span class="sxs-lookup"><span data-stu-id="904c2-110">Therefore, be sure to use an intuitive name that helps the user understand what comes with the offer.</span></span> <span data-ttu-id="904c2-111">Solo el administrador puede ver el nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="904c2-111">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="904c2-112">Es el nombre que usan los administradores para trabajar con la oferta como un recurso de Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="904c2-112">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="904c2-113">Haga clic en **Planes de base** y, en la hoja **Plan**, seleccione los planes que desea incluir en la oferta y, a continuación, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="904c2-113">Click **Base plans** and, in the **Plan** blade, select the plans you want to include in the offer, and then click **Select**.</span></span> <span data-ttu-id="904c2-114">Haga clic en **Crear** para crear la oferta.</span><span class="sxs-lookup"><span data-stu-id="904c2-114">Click **Create** to create the offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="904c2-115">Haga clic en **Todos los recursos**, busque la nueva oferta, haga clic en la nueva oferta, haga clic en **Cambiar estado** y, a continuación, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="904c2-115">Click **All Resources**, search for your new offer, click on the new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="904c2-116">Las ofertas deben hacerse públicas para que los inquilinos obtengan la vista completa cuando se suscriban.</span><span class="sxs-lookup"><span data-stu-id="904c2-116">Offers must be made public for tenants to get the full view when subscribing.</span></span> <span data-ttu-id="904c2-117">Las ofertas pueden ser:</span><span class="sxs-lookup"><span data-stu-id="904c2-117">Offers can be:</span></span>

* <span data-ttu-id="904c2-118">**Públicos**: visible para los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="904c2-118">**Public**: Visible to tenants.</span></span>
* <span data-ttu-id="904c2-119">**Privadas**: solo son visibles para los administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="904c2-119">**Private**: Only visible to the cloud administrators.</span></span> <span data-ttu-id="904c2-120">Resulta útil durante la elaboración del plan o la oferta, o si el administrador de la nube desea aprobar todas las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="904c2-120">Useful while drafting the plan or offer, or if the cloud administrator wants to approve every subscription.</span></span>
* <span data-ttu-id="904c2-121">**Retirados**: cerrados a nuevos suscriptores.</span><span class="sxs-lookup"><span data-stu-id="904c2-121">**Decommissioned**: Closed to new subscribers.</span></span> <span data-ttu-id="904c2-122">El administrador de la nube puede usar las ofertas y planes retirados para evitar futuras suscripciones, pero dejar intactos los suscriptores actuales.</span><span class="sxs-lookup"><span data-stu-id="904c2-122">The cloud administrator can use decommissioned to prevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="904c2-123">Los cambios en la oferta no son inmediatamente visibles para el inquilino.</span><span class="sxs-lookup"><span data-stu-id="904c2-123">Changes to the offer are not immediately visible to the tenant.</span></span> <span data-ttu-id="904c2-124">Para visualizar los cambios, es posible que tenga que cerrar sesión e iniciarla para ver la nueva suscripción en el "selector de suscripciones" al crear recursos o grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="904c2-124">To see the changes, you might have to logout/login to see the new subscription in the “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="904c2-125">También puede crear ofertas, planes y cuotas predeterminadas mediante PowerShell, como se explica en el [archivo Léame del administrador de servicios de Azure Stack](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span><span class="sxs-lookup"><span data-stu-id="904c2-125">You can also create default offers, plans, and quotas by using PowerShell as explained in the [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


## <a name="next-steps"></a><span data-ttu-id="904c2-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="904c2-126">Next steps</span></span>
[<span data-ttu-id="904c2-127">Suscripción a una oferta y aprovisionamiento de una máquina virtual en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="904c2-127">Subscribe to an offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
