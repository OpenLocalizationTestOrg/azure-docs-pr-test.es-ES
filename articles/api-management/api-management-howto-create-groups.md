---
title: "las cuentas de desarrollador aaaManage usar los grupos de administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage developer cuentas con grupos de administración de API de Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="76183-103">Cómo para desarrolladores de toomanage grupos toocreate y usar las cuentas de administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="76183-103">How toocreate and use groups toomanage developer accounts in Azure API Management</span></span>
<span data-ttu-id="76183-104">Administración de API, los grupos son utilizados toomanage Hola visibilidad de toodevelopers de productos.</span><span class="sxs-lookup"><span data-stu-id="76183-104">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="76183-105">Productos son la primera toogroups visible realizadas y, a continuación, pueden ver y suscribirse toohello productos que están asociados a grupos de Hola a los desarrolladores de esos grupos.</span><span class="sxs-lookup"><span data-stu-id="76183-105">Products are first made visible toogroups, and then developers in those groups can view and subscribe toohello products that are associated with hello groups.</span></span> 

<span data-ttu-id="76183-106">Administración de API tiene Hola los grupos de sistema inmutables siguientes.</span><span class="sxs-lookup"><span data-stu-id="76183-106">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="76183-107">**Administradores** : los administradores de la suscripción de Azure son miembros de este grupo.</span><span class="sxs-lookup"><span data-stu-id="76183-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="76183-108">Los administradores administran las instancias de servicio de administración de API, crear Hola API, operaciones y productos que se usan los programadores.</span><span class="sxs-lookup"><span data-stu-id="76183-108">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="76183-109">**Desarrolladores** : los usuarios del portal para desarrolladores autenticados se incluyen en este grupo.</span><span class="sxs-lookup"><span data-stu-id="76183-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="76183-110">Los desarrolladores son clientes de Hola que compilan aplicaciones mediante las API.</span><span class="sxs-lookup"><span data-stu-id="76183-110">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="76183-111">Los programadores se conceden portal para desarrolladores de acceso toohello y creación aplicaciones que llaman a operaciones de Hola de una API.</span><span class="sxs-lookup"><span data-stu-id="76183-111">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="76183-112">**Los invitados** -sin autenticar usuarios del portal para desarrolladores, como clientes potenciales visitar el portal para desarrolladores de Hola de una caída de la instancia de administración de API en este grupo.</span><span class="sxs-lookup"><span data-stu-id="76183-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="76183-113">Se pueden conceder cierto acceso de solo lectura, como la capacidad de hello tooview API, pero no llamarlos.</span><span class="sxs-lookup"><span data-stu-id="76183-113">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="76183-114">En grupos de sistema de toothese de suma, los administradores pueden crear grupos personalizados o [aprovechar grupos externos en inquilinos de Azure Active Directory asociados][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="76183-114">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="76183-115">Grupos personalizados y externos pueden usarse junto con grupos del sistema para conceder a los desarrolladores visibilidad y tener acceso a los productos tooAPI.</span><span class="sxs-lookup"><span data-stu-id="76183-115">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="76183-116">Por ejemplo, podría crear un grupo personalizado para desarrolladores afiliados a una determinada organización de socios y permitan tener acceso toohello las API de un producto que contiene solo las API relevantes.</span><span class="sxs-lookup"><span data-stu-id="76183-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="76183-117">Un usuario puede ser miembro de más de un grupo.</span><span class="sxs-lookup"><span data-stu-id="76183-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="76183-118">En esta guía se muestra cómo los administradores de una instancia de Administración de API pueden agregar nuevos grupos y asociarlos a productos y desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="76183-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="76183-119">Además toocreating y administrar grupos en el portal para desarrolladores de hello, puede crear y administrar grupos mediante la API de REST de administración de hello [grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entidad.</span><span class="sxs-lookup"><span data-stu-id="76183-119">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="76183-120"><a name="create-group"></a>Creación de un grupo</span><span class="sxs-lookup"><span data-stu-id="76183-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="76183-121">toocreate un nuevo grupo, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="76183-121">toocreate a new group, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="76183-122">Esto le llevará toohello portal para desarrolladores de administración de API.</span><span class="sxs-lookup"><span data-stu-id="76183-122">This takes you toohello API Management publisher portal.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="76183-124">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="76183-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="76183-125">Haga clic en **grupos** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **Agregar grupo**.</span><span class="sxs-lookup"><span data-stu-id="76183-125">Click **Groups** from hello **API Management** menu on hello left, and then click **Add Group**.</span></span>

![Add new group][api-management-add-group]

<span data-ttu-id="76183-127">Escriba un nombre único para el grupo de hello y una descripción opcional y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="76183-127">Enter a unique name for hello group and an optional description, and click **Save**.</span></span>

![Add new group][api-management-add-group-window]

<span data-ttu-id="76183-129">Hola nuevo grupo se mostrará en Hola de hello grupos ficha tooedit **nombre** o **descripción** del grupo de hello, haga clic en nombre de hello del grupo de hello en lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="76183-129">hello new group is displayed in hello groups tab. tooedit hello **Name** or **Description** of hello group, click hello name of hello group in hello list.</span></span> <span data-ttu-id="76183-130">grupo de hello toodelete, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="76183-130">toodelete hello group, click **Delete**.</span></span>

![Group added][api-management-new-group]

<span data-ttu-id="76183-132">Hello grupo una vez creada, se puede asociar con los productos y los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="76183-132">Now that hello group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="76183-133"><a name="associate-group-product"></a>Asociación de un grupo a un producto</span><span class="sxs-lookup"><span data-stu-id="76183-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="76183-134">tooassociate un grupo con un producto, haga clic en **productos** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en nombre de Hola de producto de su preferencia Hola.</span><span class="sxs-lookup"><span data-stu-id="76183-134">tooassociate a group with a product, click **Products** from hello **API Management** menu on hello left, and then click hello name of hello desired product.</span></span>

![Set visibility][api-management-add-group-to-product]

<span data-ttu-id="76183-136">Seleccione hello **visibilidad** ficha tooadd y quitar grupos y tooview Hola actual para el producto de Hola.</span><span class="sxs-lookup"><span data-stu-id="76183-136">Select hello **Visibility** tab tooadd and remove groups, and tooview hello current groups for hello product.</span></span> <span data-ttu-id="76183-137">tooadd o quitar grupos, active o desactive las casillas de verificación de Hola para hello deseado grupos y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="76183-137">tooadd or remove groups, check or uncheck hello checkboxes for hello desired groups and click **Save**.</span></span>

![Set visibility][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="76183-139">los grupos de Azure Active Directory tooadd, consulte [cómo tooauthorize developer cuentas con Azure Active Directory en la administración de API de Azure](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="76183-139">tooadd Azure Active Directory groups, see [How tooauthorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="76183-140">grupos de tooconfigure de hello **visibilidad** para un producto, haga clic en **administrar grupos**.</span><span class="sxs-lookup"><span data-stu-id="76183-140">tooconfigure groups from hello **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="76183-141">Una vez que un producto está asociado a un grupo, los desarrolladores de ese grupo pueden ver y suscribirse toohello producto.</span><span class="sxs-lookup"><span data-stu-id="76183-141">Once a product is associated with a group, developers in that group can view and subscribe toohello product.</span></span>

## <span data-ttu-id="76183-142"><a name="associate-group-developer"></a>Asociación de grupos a desarrolladores</span><span class="sxs-lookup"><span data-stu-id="76183-142"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="76183-143">grupos tooassociate con desarrolladores, haga clic en **usuarios** de hello **administración de API** menú Hola izquierda y, a continuación Hola casilla situada junto a los desarrolladores de hello desea tooassociate con un grupo.</span><span class="sxs-lookup"><span data-stu-id="76183-143">tooassociate groups with developers, click **Users** from hello **API Management** menu on hello left, and then check hello box beside hello developers you wish tooassociate with a group.</span></span>

![Agregar toogroup de desarrollador][api-management-add-group-to-developer]

<span data-ttu-id="76183-145">Una vez Hola deseado se comprueban los desarrolladores, haga clic en grupo que quiera hello en hello **agregar tooGroup** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="76183-145">Once hello desired developers are checked, click hello desired group in hello **Add tooGroup** drop-down.</span></span> <span data-ttu-id="76183-146">Los desarrolladores se pueden quitar de grupos mediante el uso de hello **quitar del grupo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="76183-146">Developers can be removed from groups by using hello **Remove from Group** drop-down.</span></span> 

![Desarrolladores][api-management-add-group-to-developer-saved]

<span data-ttu-id="76183-148">Una vez agregado asociación Hola entre para desarrolladores de Hola y el grupo de hello, puede verlo en hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="76183-148">Once hello association is added between hello developer and hello group, you can view it in hello **Users** tab.</span></span>

## <span data-ttu-id="76183-149"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76183-149"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="76183-150">Una vez que un programador se agrega grupo tooa, pueden ver y suscribirse productos toohello asociados a dicho grupo.</span><span class="sxs-lookup"><span data-stu-id="76183-150">Once a developer is added tooa group, they can view and subscribe toohello products associated with that group.</span></span> <span data-ttu-id="76183-151">Para obtener más información, consulte [Creación y publicación de un producto en Azure API Management][How create and publish a product in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="76183-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="76183-152">Además toocreating y administrar grupos en el portal para desarrolladores de hello, puede crear y administrar grupos mediante la API de REST de administración de hello [grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entidad.</span><span class="sxs-lookup"><span data-stu-id="76183-152">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
