---
title: "Usar los portales de administración y de usuarios en Azure Stack | Microsoft Docs"
description: "Aprenda las diferencias entre los portales de administración y de usuarios en Azure Stack."
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
ms.openlocfilehash: 066de8278d1ef4406cde837da4c7c65304854383
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="using-the-administrator-and-user-portals-in-azure-stack"></a><span data-ttu-id="e1fd7-103">Usar los portales de administración y de usuarios en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e1fd7-103">Using the administrator and user portals in Azure Stack</span></span>

<span data-ttu-id="e1fd7-104">Hay dos portales en Azure Stack: el portal de administración y el portal de usuarios (también llamado portal de *inquilinos*).</span><span class="sxs-lookup"><span data-stu-id="e1fd7-104">There are two portals in Azure Stack; the administrator portal and the user portal (also referred to as the *tenant* portal).</span></span> <span data-ttu-id="e1fd7-105">Los portales se apoyan en instancias independientes de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-105">The portals are backed by separate instances of Azure Resource Manager.</span></span>

<span data-ttu-id="e1fd7-106">En la tabla siguiente se muestra cómo conectarse a los portales y a los puntos de conexión de Resource Manager en un entorno de Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-106">The following table shows how to connect to the portals and to Resource Manager endpoints in an Azure Stack Development Kit environment.</span></span>

|  <span data-ttu-id="e1fd7-107">Portal</span><span class="sxs-lookup"><span data-stu-id="e1fd7-107">Portal</span></span> | <span data-ttu-id="e1fd7-108">URL del portal</span><span class="sxs-lookup"><span data-stu-id="e1fd7-108">Portal URL</span></span> | <span data-ttu-id="e1fd7-109">URL del punto de conexión de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e1fd7-109">Resource Manager endpoint URL</span></span> |   
| -------- | ------------- | ------- |  
| <span data-ttu-id="e1fd7-110">Administrador</span><span class="sxs-lookup"><span data-stu-id="e1fd7-110">Administrator</span></span> | <span data-ttu-id="e1fd7-111">https://adminportal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="e1fd7-111">https://adminportal.local.azurestack.external</span></span>  | <span data-ttu-id="e1fd7-112">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="e1fd7-112">https://adminmanagement.local.azurestack.external</span></span>  |  
| <span data-ttu-id="e1fd7-113">Usuario</span><span class="sxs-lookup"><span data-stu-id="e1fd7-113">User</span></span> | <span data-ttu-id="e1fd7-114">https://portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="e1fd7-114">https://portal.local.azurestack.external</span></span> | <span data-ttu-id="e1fd7-115">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="e1fd7-115">https://management.local.azurestack.external</span></span>  |
| | |

## <a name="the-administrator-portal"></a><span data-ttu-id="e1fd7-116">El portal de administración</span><span class="sxs-lookup"><span data-stu-id="e1fd7-116">The administrator portal</span></span>

<span data-ttu-id="e1fd7-117">El portal de administración permite que un operador de nube realice tareas administrativas y operativas.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-117">The administrator portal enables a cloud operator to perform administrative and operational tasks.</span></span> <span data-ttu-id="e1fd7-118">Un operador de nube puede hacer cosas como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="e1fd7-118">A cloud operator can do things such as:</span></span>
* <span data-ttu-id="e1fd7-119">Supervisar el estado y las alertas.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-119">monitor health and alerts</span></span>
* <span data-ttu-id="e1fd7-120">Administrar la capacidad.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-120">manage capacity</span></span>
* <span data-ttu-id="e1fd7-121">Rellenar el Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-121">populate the marketplace</span></span>
* <span data-ttu-id="e1fd7-122">Crear planes y ofertas.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-122">create plans and offers</span></span>
* <span data-ttu-id="e1fd7-123">Crear suscripciones para los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-123">create subscriptions for tenants</span></span>

<span data-ttu-id="e1fd7-124">Un operador de nube también puede crear recursos, como máquinas virtuales, redes virtuales y cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-124">A cloud operator can also create resources such as virtual machines, virtual networks, and storage accounts.</span></span>

 ![El portal de administración](media/azure-stack-manage-portals/image1.png)

 ## <a name="the-user-portal"></a><span data-ttu-id="e1fd7-126">El portal de usuarios</span><span class="sxs-lookup"><span data-stu-id="e1fd7-126">The user portal</span></span>

 <span data-ttu-id="e1fd7-127">El portal de usuarios no proporciona acceso a cualquiera de las funcionalidades administrativas u operativas del portal de administración.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-127">The user portal does not provide access to any of the administrative or operational capabilities of the administrator portal.</span></span> <span data-ttu-id="e1fd7-128">En el portal de usuarios, un usuario puede suscribirse a las ofertas públicas y utilizar los servicios que están disponibles a través de dichas ofertas.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-128">In the user portal, a user can subscribe to public offers, and use the services that are made available through those offers.</span></span>

  ![El portal de usuarios](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a><span data-ttu-id="e1fd7-130">Comportamiento de la suscripción</span><span class="sxs-lookup"><span data-stu-id="e1fd7-130">Subscription behavior</span></span>
 
 <span data-ttu-id="e1fd7-131">Asegúrese de comprender las siguientes diferencias entre el comportamiento de la suscripción en los dos portales.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-131">Make sure that you understand the following differences between subscription behavior in the two portals.</span></span>

 <span data-ttu-id="e1fd7-132">Portal de administración:</span><span class="sxs-lookup"><span data-stu-id="e1fd7-132">Administrator portal:</span></span>
* <span data-ttu-id="e1fd7-133">Hay solo una suscripción que está disponible en el portal de administración.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-133">There is only one subscription that is available in the administrator portal.</span></span> <span data-ttu-id="e1fd7-134">Esta suscripción es la *suscripción de proveedor predeterminada*.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-134">This subscription is the *Default Provider Subscription*.</span></span> <span data-ttu-id="e1fd7-135">No se puede agregar ninguna otra suscripción para usarla en el portal de administración.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-135">You can't add any other subscriptions for use in the administrator portal.</span></span>
* <span data-ttu-id="e1fd7-136">Como operador de nube, puede agregar suscripciones para los usuarios (incluido usted mismo) desde el portal de administración.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-136">As a cloud operator, you can add subscriptions for your users (including yourself) from the administrator portal.</span></span> <span data-ttu-id="e1fd7-137">Los usuarios (incluido usted) pueden tener acceso a estas suscripciones y usarlas desde el portal de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-137">Users (including yourself) can access and use these subscriptions from the user portal.</span></span>

  >[!NOTE]
  <span data-ttu-id="e1fd7-138">Debido a la separación de Azure Resource Manager, las suscripciones no se cruzan de un portal a otro.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-138">Because of the Azure Resource Manager separation, subscriptions do not cross portals.</span></span> <span data-ttu-id="e1fd7-139">Por ejemplo, si, como operador de nube, inicia sesión en el portal de usuarios, no puede tener acceso a la suscripción de proveedor predeterminada.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-139">For example, if you as a cloud operator signs in to the user portal, you can't access the Default Provider Subscription.</span></span> <span data-ttu-id="e1fd7-140">Por lo tanto, no tiene acceso a las funciones administrativas.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-140">Therefore, you don't have access to any administrative functions.</span></span> <span data-ttu-id="e1fd7-141">Puede crear suscripciones para sí mismo a partir de ofertas públicas, pero se le considerará un usuario inquilino.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-141">You can create subscriptions for yourself from public offers, but you are considered a tenant user.</span></span>

<span data-ttu-id="e1fd7-142">Portal de usuarios:</span><span class="sxs-lookup"><span data-stu-id="e1fd7-142">User portal:</span></span>
* <span data-ttu-id="e1fd7-143">En el portal de usuarios, una cuenta puede tener varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-143">In the user portal, an account can have multiple subscriptions.</span></span>

  >[!NOTE]
  <span data-ttu-id="e1fd7-144">En el entorno del kit de desarrollo, si un usuario inquilino pertenece al mismo directorio que el operador de nube, no se le impide iniciar sesión en el portal de administración.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-144">In the development kit environment, if a tenant user belongs to the same directory as the cloud operator, they are not blocked from signing in to the administrator portal.</span></span> <span data-ttu-id="e1fd7-145">Sin embargo, no tiene acceso a ninguna de las funciones administrativas.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-145">However, they can't access any of the administrative functions.</span></span> <span data-ttu-id="e1fd7-146">Además, no puede agregar suscripciones ni acceder a las ofertas disponibles en el portal de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e1fd7-146">Also, they can't add subscriptions or access offers that are made available to them in the user portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1fd7-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e1fd7-147">Next steps</span></span>

[<span data-ttu-id="e1fd7-148">Conexión a Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e1fd7-148">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)

[<span data-ttu-id="e1fd7-149">Administración de regiones en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e1fd7-149">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
