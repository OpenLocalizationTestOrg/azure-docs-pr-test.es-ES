---
title: aaaCreate una oferta de pila de Azure | Documentos de Microsoft
description: "Como administrador de la nube, obtenga información acerca de cómo toocreate una oferta para los inquilinos en la pila de Azure."
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
ms.openlocfilehash: 924526a0ff1c634b7c127c03a4572057c35b497b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="d7285-103">Creación de una oferta en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d7285-103">Create an offer in Azure Stack</span></span>
<span data-ttu-id="d7285-104">[Ofrece](azure-stack-key-features.md) son grupos de uno o varios planes que toopurchase tootenants presente de proveedores o suscribirse a.</span><span class="sxs-lookup"><span data-stu-id="d7285-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present tootenants toopurchase or subscribe to.</span></span> <span data-ttu-id="d7285-105">Este documento muestra cómo una oferta que incluye hello toocreate [plan que creó](azure-stack-create-plan.md) en el último paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7285-105">This document shows you how toocreate an offer that includes hello [plan that you created](azure-stack-create-plan.md) in hello last step.</span></span> <span data-ttu-id="d7285-106">Esta oferta proporciona a los suscriptores Hola capacidad tooprovision las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d7285-106">This offer gives subscribers hello ability tooprovision virtual machines.</span></span>

1. <span data-ttu-id="d7285-107">Inicie sesión en el portal de administración de Azure pila toohello (https://adminportal.local.azurestack.external) > haga clic en **New** > **inquilino ofrece + planes**  >   **Ofrecer**.</span><span class="sxs-lookup"><span data-stu-id="d7285-107">Sign in toohello Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="d7285-108">Hola **ofrecen nuevas** hoja, rellene **nombre para mostrar** y **nombre de recurso**y, a continuación, seleccione un nuevo o existente **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="d7285-108">In hello **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="d7285-109">Hola nombre para mostrar es el nombre descriptivo de la oferta de Hola y Hola solo información acerca de la oferta de Hola que verán los usuarios de hello cuando se suscriba.</span><span class="sxs-lookup"><span data-stu-id="d7285-109">hello Display Name is hello offer's friendly name and is hello only information about hello offer that hello users will see when subscribing.</span></span> <span data-ttu-id="d7285-110">Por lo tanto, ser seguro toouse un nombre intuitivo que ayuda a usuario de Hola a entender lo que viene con la oferta de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7285-110">Therefore, be sure toouse an intuitive name that helps hello user understand what comes with hello offer.</span></span> <span data-ttu-id="d7285-111">Hola, administrador solo puede ver Hola nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="d7285-111">Only hello admin can see hello Resource Name.</span></span> <span data-ttu-id="d7285-112">Su Hola nombre que administradores utilizar toowork con Hola oferta como un recurso de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7285-112">It's hello name that admins use toowork with hello offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="d7285-113">Haga clic en **Base planes** y, en hello **planear** hoja, planes de hello select que desee tooinclude de la oferta de hello y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="d7285-113">Click **Base plans** and, in hello **Plan** blade, select hello plans you want tooinclude in hello offer, and then click **Select**.</span></span> <span data-ttu-id="d7285-114">Haga clic en **crear** oferta de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d7285-114">Click **Create** toocreate hello offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="d7285-115">Haga clic en **todos los recursos**, busque la oferta de nuevo, haga clic en nueva oferta de hello, haga clic en **cambio de estado**y, a continuación, haga clic en **público**.</span><span class="sxs-lookup"><span data-stu-id="d7285-115">Click **All Resources**, search for your new offer, click on hello new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="d7285-116">Ofertas deben realizarse públicas para la vista completa de los inquilinos tooget Hola al suscribirse.</span><span class="sxs-lookup"><span data-stu-id="d7285-116">Offers must be made public for tenants tooget hello full view when subscribing.</span></span> <span data-ttu-id="d7285-117">Las ofertas pueden ser:</span><span class="sxs-lookup"><span data-stu-id="d7285-117">Offers can be:</span></span>

* <span data-ttu-id="d7285-118">**Pública**: tootenants Visible.</span><span class="sxs-lookup"><span data-stu-id="d7285-118">**Public**: Visible tootenants.</span></span>
* <span data-ttu-id="d7285-119">**Privada**: toohello visible solo a los administradores de la nube.</span><span class="sxs-lookup"><span data-stu-id="d7285-119">**Private**: Only visible toohello cloud administrators.</span></span> <span data-ttu-id="d7285-120">Útil al plan de redacción Hola o la oferta, o si desea que Administrador de la nube de hello tooapprove todas las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="d7285-120">Useful while drafting hello plan or offer, or if hello cloud administrator wants tooapprove every subscription.</span></span>
* <span data-ttu-id="d7285-121">**Estado de retiro**: cierra toonew suscriptores.</span><span class="sxs-lookup"><span data-stu-id="d7285-121">**Decommissioned**: Closed toonew subscribers.</span></span> <span data-ttu-id="d7285-122">Administrador de la nube de Hello puede utilizar suscripciones futuras tooprevent dado de baja, pero deja intactos los suscriptores actuales.</span><span class="sxs-lookup"><span data-stu-id="d7285-122">hello cloud administrator can use decommissioned tooprevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="d7285-123">Cambios toohello oferta no son visibles inmediatamente toohello inquilino.</span><span class="sxs-lookup"><span data-stu-id="d7285-123">Changes toohello offer are not immediately visible toohello tenant.</span></span> <span data-ttu-id="d7285-124">cambios de hello toosee, podría tener nueva suscripción de inicio de sesión/toologout toosee hello en hello "Selector de suscripciones" al crear grupos de recursos y recursos.</span><span class="sxs-lookup"><span data-stu-id="d7285-124">toosee hello changes, you might have toologout/login toosee hello new subscription in hello “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="d7285-125">También puede crear ofertas de manera predeterminada, los planes y las cuotas mediante PowerShell, como se explica en hello [archivo Léame del Administrador de servicios de Azure pila](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span><span class="sxs-lookup"><span data-stu-id="d7285-125">You can also create default offers, plans, and quotas by using PowerShell as explained in hello [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


## <a name="next-steps"></a><span data-ttu-id="d7285-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d7285-126">Next steps</span></span>
[<span data-ttu-id="d7285-127">Suscribirse tooan oferta y, a continuación, aprovisionar una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d7285-127">Subscribe tooan offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
