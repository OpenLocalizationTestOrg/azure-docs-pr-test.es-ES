---
title: "Administración de cuentas de desarrollador mediante grupos en Azure API Management | Microsoft Docs"
description: "Obtenga información acerca de cómo administrar cuentas de desarrollador mediante los grupos en Administración de API de Azure."
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
ms.openlocfilehash: b4d71cdfbab535b02542fbb26c7555265e5f9c37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="5e7f8-103">Creación y uso de grupos para administrar cuentas de desarrollador en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="5e7f8-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="5e7f8-104">En Administración de API, los grupos se usan para administrar la visibilidad de productos para los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="5e7f8-105">Los productos son visibles en primer lugar para los grupos y luego los desarrolladores de dichos grupos pueden ver y suscribirse a los productos asociados a los grupos.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="5e7f8-106">Administración de API tiene los siguientes grupos invariables del sistema.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="5e7f8-107">**Administradores** : los administradores de la suscripción de Azure son miembros de este grupo.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="5e7f8-108">Los administradores controlan las instancias del servicio Administración de API y crean las API, las operaciones y los productos que usan los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="5e7f8-109">**Desarrolladores** : los usuarios del portal para desarrolladores autenticados se incluyen en este grupo.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="5e7f8-110">Los desarrolladores son los clientes que compilan aplicaciones con sus API.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="5e7f8-111">Los desarrolladores, después de que se les concede acceso al portal para desarrolladores, crean aplicaciones que llaman a las operaciones de una API.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="5e7f8-112">**Invitados** : a este grupo pertenecen los usuarios del portal para desarrolladores no autenticados como, por ejemplo, clientes potenciales que visitan el portal para desarrolladores de una instancia de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="5e7f8-113">Se les concede determinado acceso de solo lectura, como por ejemplo la posibilidad de ver API pero no llamarlas.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="5e7f8-114">Además de estos grupos del sistema, los administradores pueden crear grupos personalizados o [aprovechar los grupos externos en inquilinos de Azure Active Directory asociados][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="5e7f8-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="5e7f8-115">Los grupos personalizados y externos pueden usarse junto con grupos del sistema en la concesión a los desarrolladores de visibilidad y acceso a productos de la API.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="5e7f8-116">Por ejemplo, podría crear un grupo personalizado para los desarrolladores afiliados a una organización asociada específica y permitirles el acceso a las API a partir de un producto que contenga solo las API relevantes.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="5e7f8-117">Un usuario puede ser miembro de más de un grupo.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="5e7f8-118">En esta guía se muestra cómo los administradores de una instancia de Administración de API pueden agregar nuevos grupos y asociarlos a productos y desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="5e7f8-119">Además de crear y administrar grupos en el portal del editor, puede crear y administrar sus grupos mediante la entidad de [grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx) de la API de REST de administración.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="5e7f8-120"><a name="create-group"> </a>Creación de un grupo</span><span class="sxs-lookup"><span data-stu-id="5e7f8-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="5e7f8-121">Para crear un nuevo grupo, haga clic en **Publisher portal** (Portal del publicador) en Azure Portal para su servicio de API Management.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="5e7f8-122">De este modo, se abre el portal del publicador de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-122">This takes you to the API Management publisher portal.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="5e7f8-124">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="5e7f8-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="5e7f8-125">Haga clic en **Grupos** en el menú **API Management** de la izquierda y haga clic en **Agregar grupo**.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![Add new group][api-management-add-group]

<span data-ttu-id="5e7f8-127">Especifique un nombre único para el grupo y una descripción opcional y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![Add new group][api-management-add-group-window]

<span data-ttu-id="5e7f8-129">El nuevo grupo se muestra en la pestaña Grupos.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-129">The new group is displayed in the groups tab.</span></span> <span data-ttu-id="5e7f8-130">Para editar el **Nombre** o la **Descripción** del grupo, haga clic en el nombre del grupo en la lista.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-130">To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="5e7f8-131">Para eliminar el grupo, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-131">To delete the group, click **Delete**.</span></span>

![Group added][api-management-new-group]

<span data-ttu-id="5e7f8-133">Ahora que se ha creado el grupo, se puede asociar a productos y desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-133">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="5e7f8-134"><a name="associate-group-product"> </a>Asociación de un grupo a un producto</span><span class="sxs-lookup"><span data-stu-id="5e7f8-134"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="5e7f8-135">Para asociar un grupo a un producto, haga clic en **Productos** en el menú **API Management** de la izquierda y haga clic en el nombre del producto que desee.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-135">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![Set visibility][api-management-add-group-to-product]

<span data-ttu-id="5e7f8-137">Seleccione la pestaña **Visibilidad** para agregar y quitar grupos, así como para ver los grupos actuales para el producto.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-137">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="5e7f8-138">Para agregar o quitar grupos, active o desactive las casillas correspondientes a los grupos que desee y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-138">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![Set visibility][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="5e7f8-140">Para agregar grupos de Azure Active Directory, consulte [Autorización de las cuentas de desarrollador con Azure Active Directory en Administración de API de Azure](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="5e7f8-140">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="5e7f8-141">Para configurar grupos en la pestaña **Visibilidad** para un producto, haga clic en **Administrar grupos**.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-141">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="5e7f8-142">Una vez asociado un producto a un grupo, los desarrolladores del grupo pueden ver el producto y suscribirse a él.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-142">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="5e7f8-143"><a name="associate-group-developer"> </a>Asociación de grupos a desarrolladores</span><span class="sxs-lookup"><span data-stu-id="5e7f8-143"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="5e7f8-144">Para asociar grupos a desarrolladores, haga clic en **Usuarios** en el menú **API Management** de la izquierda y active la casilla situada junto a los desarrolladores que desee asociar a un grupo.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-144">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![Add developer to group][api-management-add-group-to-developer]

<span data-ttu-id="5e7f8-146">Una vez seleccionados los desarrolladores que desee, haga clic en el grupo que desee en la lista desplegable **Agregar a grupo** .</span><span class="sxs-lookup"><span data-stu-id="5e7f8-146">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="5e7f8-147">Los desarrolladores se pueden quitar de los grupos con la lista desplegable **Quitar de grupo** .</span><span class="sxs-lookup"><span data-stu-id="5e7f8-147">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![Desarrolladores][api-management-add-group-to-developer-saved]

<span data-ttu-id="5e7f8-149">Una vez agregada, la asociación entre el desarrollador y el grupo se puede ver en la pestaña **Usuarios** .</span><span class="sxs-lookup"><span data-stu-id="5e7f8-149">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="5e7f8-150"><a name="next-steps"> </a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5e7f8-150"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="5e7f8-151">Una vez agregado a un grupo, un desarrollador puede ver los productos asociados al grupo y suscribirse a ellos.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-151">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="5e7f8-152">Para obtener más información, consulte [Creación y publicación de un producto en Azure API Management][How create and publish a product in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="5e7f8-152">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="5e7f8-153">Además de crear y administrar grupos en el portal del editor, puede crear y administrar sus grupos mediante la entidad de [grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx) de la API de REST de administración.</span><span class="sxs-lookup"><span data-stu-id="5e7f8-153">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

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
