---
title: Servicios de aaaOffering en la pila de Azure | Documentos de Microsoft
description: Como un operador en la nube, puede ofrecer a los usuarios de servicios tooyour.
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: 47cff8bfb202527ae4c930c7d1b9eb3998bee85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-offering-services-in-azure-stack"></a><span data-ttu-id="829f4-103">Introducción a la oferta de servicios en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="829f4-103">Overview of offering services in Azure Stack</span></span>

<span data-ttu-id="829f4-104">Microsoft Azure Stack es una nueva plataforma en la nube híbrida que le permite proporcionar servicios desde el centro de datos.</span><span class="sxs-lookup"><span data-stu-id="829f4-104">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver services from your datacenter.</span></span> <span data-ttu-id="829f4-105">Como proveedor de servicios, puede ofrecer a los inquilinos tooyour de servicios.</span><span class="sxs-lookup"><span data-stu-id="829f4-105">As a service provider, you can offer services tooyour tenants.</span></span> <span data-ttu-id="829f4-106">Dentro de una empresa u organismo gubernamental, puede ofrecer a los empleados tooyour de servicios local.</span><span class="sxs-lookup"><span data-stu-id="829f4-106">Within a business or government agency, you can offer on-premises services tooyour employees.</span></span> <span data-ttu-id="829f4-107">Servicios de Hola que puede entregar incluyen, pero no se limitan a:</span><span class="sxs-lookup"><span data-stu-id="829f4-107">hello services that you can deliver include, but are not limited to:</span></span>

- <span data-ttu-id="829f4-108">Servicios de plataforma como servicio (PaaS), como App Services, Mobile Apps, API Apps, API Functions, SQL, MySQL.</span><span class="sxs-lookup"><span data-stu-id="829f4-108">Platform as a Service (PaaS) services like App Services, Mobile Apps, API Apps, API Functions, SQL, MySQL.</span></span>
- <span data-ttu-id="829f4-109">Servicios de software como servicio (SaaS), como Sharepoint.</span><span class="sxs-lookup"><span data-stu-id="829f4-109">Software as a Service (SaaS) services like Sharepoint.</span></span>

<span data-ttu-id="829f4-110">Incluso puede combinar servicios toointegrate y crear soluciones complejas para los distintos usuarios.</span><span class="sxs-lookup"><span data-stu-id="829f4-110">You can even combine services toointegrate and build complex solutions for different users.</span></span>

<span data-ttu-id="829f4-111">toodeliver estos usuarios tooyour de servicios, debe crear [planes y ofertas, cuotas](azure-stack-plan-offer-quota-overview.md).</span><span class="sxs-lookup"><span data-stu-id="829f4-111">toodeliver these services tooyour users, you must create [plans, offers, and quotas](azure-stack-plan-offer-quota-overview.md).</span></span> <span data-ttu-id="829f4-112">Los usuarios, a continuación, pueden suscribirse tooyour ofrece toouse Hola servicios.</span><span class="sxs-lookup"><span data-stu-id="829f4-112">Your users can then subscribe tooyour offers toouse hello services.</span></span>

## <a name="plan-your-service-offers"></a><span data-ttu-id="829f4-113">Planificar las ofertas de servicios</span><span class="sxs-lookup"><span data-stu-id="829f4-113">Plan your service offers</span></span>

<span data-ttu-id="829f4-114">Hora de planear las ofertas, mantenga Hola después aspectos en mente:</span><span class="sxs-lookup"><span data-stu-id="829f4-114">When you’re planning your offers, keep hello following points in mind:</span></span>

<span data-ttu-id="829f4-115">**Ofertas de evaluación**: puede usar los nuevos usuarios de tooattract de ofertas de evaluación, que, a continuación, pueden actualizar los servicios de tooadditional.</span><span class="sxs-lookup"><span data-stu-id="829f4-115">**Trial offers**: You can use trial offers tooattract new users, who can then upgrade tooadditional services.</span></span> <span data-ttu-id="829f4-116">toocreate una oferta de prueba, crear una pequeña [plan base](azure-stack-plan-offer-quota-overview.md#base-plan) con un plan de complemento opcionales mayor.</span><span class="sxs-lookup"><span data-stu-id="829f4-116">toocreate a trial offer, create a small [base plan](azure-stack-plan-offer-quota-overview.md#base-plan) with an optional larger add-on plan.</span></span>

<span data-ttu-id="829f4-117">**Planificación de capacidad**: es posible que tenga problemas con los usuarios arrastrar grandes cantidades de recursos y atascar sistema Hola a todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="829f4-117">**Capacity planning**: You might be concerned about users grabbing large amounts of resources and clogging hello system for all users.</span></span> <span data-ttu-id="829f4-118">rendimiento de toohelp, puede [configurar sus planes con cuotas](azure-stack-plan-offer-quota-overview.md#plans) toocap uso.</span><span class="sxs-lookup"><span data-stu-id="829f4-118">toohelp performance, you can [configure your plans with quotas](azure-stack-plan-offer-quota-overview.md#plans) toocap usage.</span></span>

<span data-ttu-id="829f4-119">**Delegado proveedores**: puede conceder a otros usuarios Hola capacidad toocreate ofertas en su entorno.</span><span class="sxs-lookup"><span data-stu-id="829f4-119">**Delegated providers**: You can grant others hello ability toocreate offers in your environment.</span></span> <span data-ttu-id="829f4-120">Por ejemplo, si es un proveedor de servicios, puede [delegar](azure-stack-delegated-provider.md) este distribuidores de tooyour de capacidad.</span><span class="sxs-lookup"><span data-stu-id="829f4-120">For example, if you’re a service provider, you can [delegate](azure-stack-delegated-provider.md) this ability tooyour resellers.</span></span> <span data-ttu-id="829f4-121">O bien, si es una organización, puede delegar tooother divisiones o subsidiarias.</span><span class="sxs-lookup"><span data-stu-id="829f4-121">Or, if you’re an organization, you can delegate tooother divisions/subsidiaries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="829f4-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="829f4-122">Next steps</span></span>
[<span data-ttu-id="829f4-123">Más información sobre ofertas, planes, cuotas y suscripciones</span><span class="sxs-lookup"><span data-stu-id="829f4-123">Learn more about offers, plans, quotas, and subscriptions</span></span>](azure-stack-plan-offer-quota-overview.md)

