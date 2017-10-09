---
title: los portales de administrador y usuario de hello aaaUsing en pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de las diferencias de hello entre portales de administrador y usuario de hello en la pila de Azure."
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 02c7ff03-874e-4951-b591-28166b7a7a79
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: twooley
ms.openlocfilehash: 5e940749917e4aade26483a79bcc238346bf94f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-administrator-and-user-portals-in-azure-stack"></a><span data-ttu-id="d5165-103">Uso de portales de administrador y usuario de hello en la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="d5165-103">Using hello administrator and user portals in Azure Stack</span></span>

<span data-ttu-id="d5165-104">Hay dos portales de pila de Azure; Hola portal de administrador y usuario hello (también denominada hello tooas *inquilino* portal).</span><span class="sxs-lookup"><span data-stu-id="d5165-104">There are two portals in Azure Stack; hello administrator portal and hello user portal (also referred tooas hello *tenant* portal).</span></span> <span data-ttu-id="d5165-105">portales de Hola se basan en instancias independientes del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5165-105">hello portals are backed by separate instances of Azure Resource Manager.</span></span>

<span data-ttu-id="d5165-106">tabla Hola siguiente muestra cómo tooconnect toohello portales y los puntos de conexión del Administrador de tooResource en un entorno de Kit de desarrollo de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5165-106">hello following table shows how tooconnect toohello portals and tooResource Manager endpoints in an Azure Stack Development Kit environment.</span></span>

|  <span data-ttu-id="d5165-107">Portal</span><span class="sxs-lookup"><span data-stu-id="d5165-107">Portal</span></span> | <span data-ttu-id="d5165-108">URL del portal</span><span class="sxs-lookup"><span data-stu-id="d5165-108">Portal URL</span></span> | <span data-ttu-id="d5165-109">URL del punto de conexión de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d5165-109">Resource Manager endpoint URL</span></span> |   
| -------- | ------------- | ------- |  
| <span data-ttu-id="d5165-110">Administrador</span><span class="sxs-lookup"><span data-stu-id="d5165-110">Administrator</span></span> | <span data-ttu-id="d5165-111">https://adminportal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="d5165-111">https://adminportal.local.azurestack.external</span></span>  | <span data-ttu-id="d5165-112">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="d5165-112">https://adminmanagement.local.azurestack.external</span></span>  |  
| <span data-ttu-id="d5165-113">Usuario</span><span class="sxs-lookup"><span data-stu-id="d5165-113">User</span></span> | <span data-ttu-id="d5165-114">https://portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="d5165-114">https://portal.local.azurestack.external</span></span> | <span data-ttu-id="d5165-115">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="d5165-115">https://management.local.azurestack.external</span></span>  |
| | |

## <a name="hello-administrator-portal"></a><span data-ttu-id="d5165-116">portal de administración de Hola</span><span class="sxs-lookup"><span data-stu-id="d5165-116">hello administrator portal</span></span>

<span data-ttu-id="d5165-117">portal de administrador de Hello permite a una nube operador tooperform administrativo y operativo las tareas.</span><span class="sxs-lookup"><span data-stu-id="d5165-117">hello administrator portal enables a cloud operator tooperform administrative and operational tasks.</span></span> <span data-ttu-id="d5165-118">Un operador de nube puede hacer cosas como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="d5165-118">A cloud operator can do things such as:</span></span>
* <span data-ttu-id="d5165-119">Supervisar el estado y las alertas.</span><span class="sxs-lookup"><span data-stu-id="d5165-119">monitor health and alerts</span></span>
* <span data-ttu-id="d5165-120">Administrar la capacidad.</span><span class="sxs-lookup"><span data-stu-id="d5165-120">manage capacity</span></span>
* <span data-ttu-id="d5165-121">rellenar marketplace Hola</span><span class="sxs-lookup"><span data-stu-id="d5165-121">populate hello marketplace</span></span>
* <span data-ttu-id="d5165-122">Crear planes y ofertas.</span><span class="sxs-lookup"><span data-stu-id="d5165-122">create plans and offers</span></span>
* <span data-ttu-id="d5165-123">Crear suscripciones para los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="d5165-123">create subscriptions for tenants</span></span>

<span data-ttu-id="d5165-124">Un operador de nube también puede crear recursos, como máquinas virtuales, redes virtuales y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d5165-124">A cloud operator can also create resources such as virtual machines, virtual networks, and storage accounts.</span></span>

 ![portal de administración de Hola](media/azure-stack-manage-portals/image1.png)

 ## <a name="hello-user-portal"></a><span data-ttu-id="d5165-126">portal de usuarios de Hola</span><span class="sxs-lookup"><span data-stu-id="d5165-126">hello user portal</span></span>

 <span data-ttu-id="d5165-127">portal de usuarios de Hello no proporciona acceso tooany de capacidades de hello administrativos u operativos del portal de administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5165-127">hello user portal does not provide access tooany of hello administrative or operational capabilities of hello administrator portal.</span></span> <span data-ttu-id="d5165-128">En el portal de usuarios de hello, un usuario puede suscribirse toopublic ofertas y usar servicios de Hola que están disponibles a través de dichas ofertas.</span><span class="sxs-lookup"><span data-stu-id="d5165-128">In hello user portal, a user can subscribe toopublic offers, and use hello services that are made available through those offers.</span></span>

  ![portal de usuarios de Hola](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a><span data-ttu-id="d5165-130">Comportamiento de la suscripción</span><span class="sxs-lookup"><span data-stu-id="d5165-130">Subscription behavior</span></span>
 
 <span data-ttu-id="d5165-131">Asegúrese de que comprende Hola siguiendo las diferencias entre el comportamiento de suscripción en los portales de hello dos.</span><span class="sxs-lookup"><span data-stu-id="d5165-131">Make sure that you understand hello following differences between subscription behavior in hello two portals.</span></span>

 <span data-ttu-id="d5165-132">Portal de administración:</span><span class="sxs-lookup"><span data-stu-id="d5165-132">Administrator portal:</span></span>
* <span data-ttu-id="d5165-133">Hay solo una suscripción que está disponible en el portal del Administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5165-133">There is only one subscription that is available in hello administrator portal.</span></span> <span data-ttu-id="d5165-134">Esta suscripción es hello *suscripción de proveedor predeterminado*.</span><span class="sxs-lookup"><span data-stu-id="d5165-134">This subscription is hello *Default Provider Subscription*.</span></span> <span data-ttu-id="d5165-135">No se puede agregar cualquier otras suscripciones para su uso en el portal del Administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5165-135">You can't add any other subscriptions for use in hello administrator portal.</span></span>
* <span data-ttu-id="d5165-136">Como un operador en la nube, puede agregar suscripciones para los usuarios (incluido usted) en el portal del Administrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5165-136">As a cloud operator, you can add subscriptions for your users (including yourself) from hello administrator portal.</span></span> <span data-ttu-id="d5165-137">Los usuarios (incluido usted) pueden tener acceso y usar estas suscripciones desde el portal de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5165-137">Users (including yourself) can access and use these subscriptions from hello user portal.</span></span>

  >[!NOTE]
  <span data-ttu-id="d5165-138">Debido a la separación de Azure Resource Manager hello, las suscripciones no se transfieren entre portales.</span><span class="sxs-lookup"><span data-stu-id="d5165-138">Because of hello Azure Resource Manager separation, subscriptions do not cross portals.</span></span> <span data-ttu-id="d5165-139">Por ejemplo, si como un operador en la nube inicia sesión en el portal de usuarios de toohello, no se puede tener acceso a Hola suscripción de proveedor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="d5165-139">For example, if you as a cloud operator signs in toohello user portal, you can't access hello Default Provider Subscription.</span></span> <span data-ttu-id="d5165-140">Por lo tanto, no tiene acceso a las funciones administrativas de tooany.</span><span class="sxs-lookup"><span data-stu-id="d5165-140">Therefore, you don't have access tooany administrative functions.</span></span> <span data-ttu-id="d5165-141">Puede crear suscripciones para sí mismo a partir de ofertas públicas, pero se le considerará un usuario inquilino.</span><span class="sxs-lookup"><span data-stu-id="d5165-141">You can create subscriptions for yourself from public offers, but you are considered a tenant user.</span></span>

<span data-ttu-id="d5165-142">Portal de usuarios:</span><span class="sxs-lookup"><span data-stu-id="d5165-142">User portal:</span></span>
* <span data-ttu-id="d5165-143">En el portal de usuarios de hello, una cuenta puede tener varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="d5165-143">In hello user portal, an account can have multiple subscriptions.</span></span>

  >[!NOTE]
  <span data-ttu-id="d5165-144">En el entorno de kit de desarrollo hello, si un usuario inquilino pertenece toohello mismo directorio como operador de nube de hello, no se podrá iniciar sesión en toohello portal del administrador.</span><span class="sxs-lookup"><span data-stu-id="d5165-144">In hello development kit environment, if a tenant user belongs toohello same directory as hello cloud operator, they are not blocked from signing in toohello administrator portal.</span></span> <span data-ttu-id="d5165-145">Sin embargo, no se puede tener acceso a cualquiera de las funciones administrativas de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5165-145">However, they can't access any of hello administrative functions.</span></span> <span data-ttu-id="d5165-146">Además, no se agregan las suscripciones o acceso ofrece realizadas toothem disponible en el portal de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5165-146">Also, they can't add subscriptions or access offers that are made available toothem in hello user portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5165-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5165-147">Next steps</span></span>

[<span data-ttu-id="d5165-148">Conectar tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="d5165-148">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

[<span data-ttu-id="d5165-149">Administración de regiones en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d5165-149">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
