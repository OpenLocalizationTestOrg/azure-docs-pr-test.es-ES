---
title: "aaaHow administrar cuentas de usuario de administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate o invitar a los usuarios en la administración de API de Azure"
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
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a><span data-ttu-id="72769-103">Cómo las cuentas de usuario de toomanage en la administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="72769-103">How toomanage user accounts in Azure API Management</span></span>
<span data-ttu-id="72769-104">Administración de API, los desarrolladores son usuarios de Hola de hello las API que exponen mediante administración de API.</span><span class="sxs-lookup"><span data-stu-id="72769-104">In API Management, developers are hello users of hello APIs that you expose using API Management.</span></span> <span data-ttu-id="72769-105">Esta guía muestra toohow toocreate e invite a los desarrolladores toouse hello las API y productos que se hace toothem disponible con la instancia de la administración de API.</span><span class="sxs-lookup"><span data-stu-id="72769-105">This guide shows toohow toocreate and invite developers toouse hello APIs and products that you make available toothem with your API Management instance.</span></span> <span data-ttu-id="72769-106">Para obtener información acerca de cómo administrar cuentas de usuario mediante programación, vea hello [entidad de usuario](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentación Hola [API de REST de administración](https://msdn.microsoft.com/library/azure/dn776326.aspx) referencia.</span><span class="sxs-lookup"><span data-stu-id="72769-106">For information on managing user accounts programmatically, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="72769-107"><a name="create-developer"></a>Creación de un desarrollador</span><span class="sxs-lookup"><span data-stu-id="72769-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="72769-108">toocreate un programador nuevo, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="72769-108">toocreate a new developer, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="72769-109">Esto le llevará toohello portal para desarrolladores de administración de API.</span><span class="sxs-lookup"><span data-stu-id="72769-109">This takes you toohello API Management publisher portal.</span></span> <span data-ttu-id="72769-110">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="72769-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal del publicador][api-management-management-console]

<span data-ttu-id="72769-112">Haga clic en **usuarios** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="72769-112">Click **Users** from hello **API Management** menu on hello left, and then click **add user**.</span></span>

![Create developer][api-management-create-developer]

<span data-ttu-id="72769-114">Escriba hello **correo electrónico**, **contraseña**, y **nombre** para nuevos desarrolladores de Hola y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="72769-114">Enter hello **Email**, **Password**, and **Name** for hello new developer and click **Save**.</span></span>

![Create developer][api-management-add-new-user]

<span data-ttu-id="72769-116">De forma predeterminada, son las cuentas de desarrollador recién creado **Active**y se asocia con hello **a los desarrolladores** grupo.</span><span class="sxs-lookup"><span data-stu-id="72769-116">By default, newly created developer accounts are **Active**, and associated with hello **Developers** group.</span></span>

![New developer][api-management-new-developer]

<span data-ttu-id="72769-118">Las cuentas de desarrollador que se encuentran en un **active** estado puede ser usado tooaccess todas las API de hello para el que tienen suscripciones.</span><span class="sxs-lookup"><span data-stu-id="72769-118">Developer accounts that are in an **active** state can be used tooaccess all of hello APIs for which they have subscriptions.</span></span> <span data-ttu-id="72769-119">tooassociate Hola recién creado developer con grupos adicionales, vea [cómo tooassociate los grupos con los desarrolladores][How tooassociate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="72769-119">tooassociate hello newly created developer with additional groups, see [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="72769-120"><a name="invite-developer"></a>Invitación a un desarrollador</span><span class="sxs-lookup"><span data-stu-id="72769-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="72769-121">tooinvite un programador, haga clic en **usuarios** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **invitar a usuario**.</span><span class="sxs-lookup"><span data-stu-id="72769-121">tooinvite a developer, click **Users** from hello **API Management** menu on hello left, and then click **Invite User**.</span></span>

![Invite developer][api-management-invite-developer]

<span data-ttu-id="72769-123">Escriba Hola nombre y direcciones de correo de desarrollador de Hola y haga clic en **invitar a**.</span><span class="sxs-lookup"><span data-stu-id="72769-123">Enter hello name and email address of hello developer, and click **Invite**.</span></span>

![Invite developer][api-management-invite-developer-window]

<span data-ttu-id="72769-125">Se muestra un mensaje de confirmación, pero el desarrollador Hola recién invitado no aparece en la lista de hello hasta después de que acepten la invitación de Hola.</span><span class="sxs-lookup"><span data-stu-id="72769-125">A confirmation message is displayed, but hello newly invited developer does not appear in hello list until after they accept hello invitation.</span></span> 

![Invite confirmation][api-management-invite-developer-confirmation]

<span data-ttu-id="72769-127">Cuando un desarrollador recibe una invitación, se envía un correo electrónico para desarrolladores de toohello.</span><span class="sxs-lookup"><span data-stu-id="72769-127">When a developer is invited, an email is sent toohello developer.</span></span> <span data-ttu-id="72769-128">Este correo electrónico se genera con una plantilla y se puede personalizar.</span><span class="sxs-lookup"><span data-stu-id="72769-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="72769-129">Para obtener más información, consulte [Configuración de plantillas de correo electrónico][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="72769-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="72769-130">Una vez que se haya aceptado la invitación de hello, cuenta de hello se convierte en activa.</span><span class="sxs-lookup"><span data-stu-id="72769-130">Once hello invitation is accepted, hello account becomes active.</span></span>

## <span data-ttu-id="72769-131"><a name="block-developer"></a> Desactivación o reactivación de una cuenta de desarrollador</span><span class="sxs-lookup"><span data-stu-id="72769-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="72769-132">De forma predeterminada, las cuentas de desarrollador recién creadas o a las que se ha invitado se encuentran en estado **Activo**.</span><span class="sxs-lookup"><span data-stu-id="72769-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="72769-133">Haga clic en una cuenta de desarrollador, toodeactivate **bloque**.</span><span class="sxs-lookup"><span data-stu-id="72769-133">toodeactivate a developer account, click **Block**.</span></span> <span data-ttu-id="72769-134">Haga clic en una cuenta de desarrollador bloqueados, tooreactivate **activar**.</span><span class="sxs-lookup"><span data-stu-id="72769-134">tooreactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="72769-135">Una cuenta de desarrollador bloqueados no puede tener acceso a portal para desarrolladores de Hola o llamar a las API.</span><span class="sxs-lookup"><span data-stu-id="72769-135">A blocked developer account can not access hello developer portal or call any APIs.</span></span> <span data-ttu-id="72769-136">Haga clic en una cuenta de usuario de toodelete **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="72769-136">toodelete a user account, click **Delete**.</span></span>

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="72769-138">Restablecimiento de la contraseña del usuario</span><span class="sxs-lookup"><span data-stu-id="72769-138">Reset a user password</span></span>
<span data-ttu-id="72769-139">contraseña de hello tooreset para una cuenta de usuario, haga clic en nombre de Hola de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="72769-139">tooreset hello password for a user account, click hello name of hello account.</span></span>

![Restablecimiento de contraseña][api-management-view-developer]

<span data-ttu-id="72769-141">Haga clic en **de restablecimiento de contraseña** toosend un tooreset de usuario de vínculo toohello su contraseña.</span><span class="sxs-lookup"><span data-stu-id="72769-141">Click **Reset password** toosend a link toohello user tooreset their password.</span></span>

![Restablecimiento de contraseña][api-management-reset-password]

<span data-ttu-id="72769-143">trabajo tooprogrammatically con cuentas de usuario, vea hello [entidad de usuario](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentación Hola [API de REST de administración](https://msdn.microsoft.com/library/azure/dn776326.aspx) referencia.</span><span class="sxs-lookup"><span data-stu-id="72769-143">tooprogrammatically work with user accounts, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="72769-144">tooreset un valor específico del tooa de contraseña de usuario cuenta, puede usar hello [actualizar un usuario](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operación y especifique la contraseña que quieras Hola.</span><span class="sxs-lookup"><span data-stu-id="72769-144">tooreset a user account password tooa specific value, you can use hello [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify hello desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="72769-145">Pendiente de comprobación</span><span class="sxs-lookup"><span data-stu-id="72769-145">Pending verification</span></span>
![Pendiente de comprobación][api-management-pending-verification]

## <span data-ttu-id="72769-147"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72769-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="72769-148">Una vez que se crea una cuenta de desarrollador, puede asociar a roles y suscribirlo tooproducts y las API.</span><span class="sxs-lookup"><span data-stu-id="72769-148">Once a developer account is created, you can associate it with roles and subscribe it tooproducts and APIs.</span></span> <span data-ttu-id="72769-149">Para obtener más información, consulte [cómo toocreate y usar grupos][How toocreate and use groups].</span><span class="sxs-lookup"><span data-stu-id="72769-149">For more information, see [How toocreate and use groups][How toocreate and use groups].</span></span>

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
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
