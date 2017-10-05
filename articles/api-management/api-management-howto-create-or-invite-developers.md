---
title: "Administración de cuentas de usuario en Azure API Management | Microsoft Docs"
description: "Más información acerca de cómo crear usuarios o invitarlos en Administración de API de Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d3a50f6d22cbf1797f580078bc0d2cc9cefe5064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="32d14-103">Administración de cuentas de usuario en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="32d14-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="32d14-104">En Administración de API, los desarrolladores son los usuarios de las API que se exponen mediante Administración de API.</span><span class="sxs-lookup"><span data-stu-id="32d14-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="32d14-105">En esta guía se muestra cómo crear desarrolladores e invitarlos a usar las API y los productos que usted pone a su disposición con la instancia de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="32d14-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="32d14-106">Para obtener información acerca de cómo administrar cuentas de usuario mediante programación, consulte la documentación de [Entidad de usuario](https://msdn.microsoft.com/library/azure/dn776330.aspx) en la referencia sobre [REST de API Management](https://msdn.microsoft.com/library/azure/dn776326.aspx).</span><span class="sxs-lookup"><span data-stu-id="32d14-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="32d14-107"><a name="create-developer"> </a>Creación de un desarrollador</span><span class="sxs-lookup"><span data-stu-id="32d14-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="32d14-108">Para crear un nuevo desarrollador, haga clic en **Publisher portal** (Portal del publicador) en Azure Portal para su servicio de API Management.</span><span class="sxs-lookup"><span data-stu-id="32d14-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="32d14-109">De este modo, se abre el portal del publicador de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="32d14-109">This takes you to the API Management publisher portal.</span></span> <span data-ttu-id="32d14-110">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Introducción a Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="32d14-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal del publicador][api-management-management-console]

<span data-ttu-id="32d14-112">Haga clic en **Usuarios** en el menú **API Management** de la izquierda y haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="32d14-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span></span>

![Create developer][api-management-create-developer]

<span data-ttu-id="32d14-114">Escriba el **Correo electrónico**, la **Contraseña** y el **nombre** del nuevo desarrollador y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="32d14-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span></span>

![Create developer][api-management-add-new-user]

<span data-ttu-id="32d14-116">De forma predeterminada, las cuentas de desarrollador recién creadas se encuentran en estado **Activo** y se asocian al grupo **Desarrolladores**.</span><span class="sxs-lookup"><span data-stu-id="32d14-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span>

![New developer][api-management-new-developer]

<span data-ttu-id="32d14-118">Las cuentas de desarrollador que se encuentran en estado **activo** se pueden usar para obtener acceso a todas las API para las que tienen suscripciones.</span><span class="sxs-lookup"><span data-stu-id="32d14-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="32d14-119">Para asociar el desarrollador recién creado a otros grupos, consulte [Asociación de grupos a desarrolladores][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="32d14-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="32d14-120"><a name="invite-developer"> </a>Invitación a un desarrollador</span><span class="sxs-lookup"><span data-stu-id="32d14-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="32d14-121">Para invitar a un desarrollador, haga clic en **Usuarios** en el menú **API Management** de la izquierda y haga clic en **Invitar a usuario**.</span><span class="sxs-lookup"><span data-stu-id="32d14-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span></span>

![Invite developer][api-management-invite-developer]

<span data-ttu-id="32d14-123">Especifique el nombre y la dirección de correo electrónico del desarrollador y haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="32d14-123">Enter the name and email address of the developer, and click **Invite**.</span></span>

![Invite developer][api-management-invite-developer-window]

<span data-ttu-id="32d14-125">Se mostrará un mensaje de confirmación, pero el desarrollador recién invitado no aparecerá en la lista hasta que acepte la invitación.</span><span class="sxs-lookup"><span data-stu-id="32d14-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

![Invite confirmation][api-management-invite-developer-confirmation]

<span data-ttu-id="32d14-127">Cuando se invita a un desarrollador, se le envía un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="32d14-127">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="32d14-128">Este correo electrónico se genera con una plantilla y se puede personalizar.</span><span class="sxs-lookup"><span data-stu-id="32d14-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="32d14-129">Para obtener más información, consulte [Configuración de plantillas de correo electrónico][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="32d14-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="32d14-130">Una vez aceptada la invitación, la cuenta se activa.</span><span class="sxs-lookup"><span data-stu-id="32d14-130">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="32d14-131"><a name="block-developer"> </a> Desactivación o reactivación de una cuenta de desarrollador</span><span class="sxs-lookup"><span data-stu-id="32d14-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="32d14-132">De forma predeterminada, las cuentas de desarrollador recién creadas o a las que se ha invitado se encuentran en estado **Activo**.</span><span class="sxs-lookup"><span data-stu-id="32d14-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="32d14-133">Para desactivar una cuenta de desarrollador, haga clic en **Bloquear**.</span><span class="sxs-lookup"><span data-stu-id="32d14-133">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="32d14-134">Para reactivar una cuenta de desarrollador bloqueada, haga clic en **Activar**.</span><span class="sxs-lookup"><span data-stu-id="32d14-134">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="32d14-135">Una cuenta de desarrollador bloqueada no puede obtener acceso al portal para desarrolladores ni llamar a ninguna API.</span><span class="sxs-lookup"><span data-stu-id="32d14-135">A blocked developer account can not access the developer portal or call any APIs.</span></span> <span data-ttu-id="32d14-136">Para eliminar una cuenta de usuario, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="32d14-136">To delete a user account, click **Delete**.</span></span>

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="32d14-138">Restablecimiento de la contraseña del usuario</span><span class="sxs-lookup"><span data-stu-id="32d14-138">Reset a user password</span></span>
<span data-ttu-id="32d14-139">Para restablecer la contraseña de una cuenta de usuario, haga clic en el nombre de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="32d14-139">To reset the password for a user account, click the name of the account.</span></span>

![Restablecer contraseña][api-management-view-developer]

<span data-ttu-id="32d14-141">Haga clic en **Restablecer contraseña** para enviar un vínculo al usuario para restablecer su contraseña.</span><span class="sxs-lookup"><span data-stu-id="32d14-141">Click **Reset password** to send a link to the user to reset their password.</span></span>

![Restablecimiento de contraseña][api-management-reset-password]

<span data-ttu-id="32d14-143">Para trabajar con cuentas de usuario mediante programación, consulte la documentación de [Entidad de usuario](https://msdn.microsoft.com/library/azure/dn776330.aspx) en la referencia sobre [REST de API Management](https://msdn.microsoft.com/library/azure/dn776326.aspx).</span><span class="sxs-lookup"><span data-stu-id="32d14-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="32d14-144">Para restablecer la contraseña de una cuenta de usuario a un valor específico, puede utilizar la operación [Actualizar un usuario](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) y especificar la contraseña que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="32d14-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="32d14-145">Pendiente de comprobación</span><span class="sxs-lookup"><span data-stu-id="32d14-145">Pending verification</span></span>
![Pendiente de comprobación][api-management-pending-verification]

## <span data-ttu-id="32d14-147"><a name="next-steps"> </a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32d14-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="32d14-148">Una vez creada una cuenta de desarrollador, se puede asociar a roles y suscribirse a productos y API.</span><span class="sxs-lookup"><span data-stu-id="32d14-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="32d14-149">Para obtener más información, consulte [Creación y uso de grupos][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="32d14-149">For more information, see [How to create and use groups][How to create and use groups].</span></span>

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
