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
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a>Cómo las cuentas de usuario de toomanage en la administración de API de Azure
Administración de API, los desarrolladores son usuarios de Hola de hello las API que exponen mediante administración de API. Esta guía muestra toohow toocreate e invite a los desarrolladores toouse hello las API y productos que se hace toothem disponible con la instancia de la administración de API. Para obtener información acerca de cómo administrar cuentas de usuario mediante programación, vea hello [entidad de usuario](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentación Hola [API de REST de administración](https://msdn.microsoft.com/library/azure/dn776326.aspx) referencia.

## <a name="create-developer"></a>Creación de un desarrollador
toocreate un programador nuevo, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API. Esto le llevará toohello portal para desarrolladores de administración de API. Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.

![Portal del publicador][api-management-management-console]

Haga clic en **usuarios** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **Agregar usuario**.

![Create developer][api-management-create-developer]

Escriba hello **correo electrónico**, **contraseña**, y **nombre** para nuevos desarrolladores de Hola y haga clic en **guardar**.

![Create developer][api-management-add-new-user]

De forma predeterminada, son las cuentas de desarrollador recién creado **Active**y se asocia con hello **a los desarrolladores** grupo.

![New developer][api-management-new-developer]

Las cuentas de desarrollador que se encuentran en un **active** estado puede ser usado tooaccess todas las API de hello para el que tienen suscripciones. tooassociate Hola recién creado developer con grupos adicionales, vea [cómo tooassociate los grupos con los desarrolladores][How tooassociate groups with developers].

## <a name="invite-developer"></a>Invitación a un desarrollador
tooinvite un programador, haga clic en **usuarios** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **invitar a usuario**.

![Invite developer][api-management-invite-developer]

Escriba Hola nombre y direcciones de correo de desarrollador de Hola y haga clic en **invitar a**.

![Invite developer][api-management-invite-developer-window]

Se muestra un mensaje de confirmación, pero el desarrollador Hola recién invitado no aparece en la lista de hello hasta después de que acepten la invitación de Hola. 

![Invite confirmation][api-management-invite-developer-confirmation]

Cuando un desarrollador recibe una invitación, se envía un correo electrónico para desarrolladores de toohello. Este correo electrónico se genera con una plantilla y se puede personalizar. Para obtener más información, consulte [Configuración de plantillas de correo electrónico][Configure email templates].

Una vez que se haya aceptado la invitación de hello, cuenta de hello se convierte en activa.

## <a name="block-developer"></a> Desactivación o reactivación de una cuenta de desarrollador
De forma predeterminada, las cuentas de desarrollador recién creadas o a las que se ha invitado se encuentran en estado **Activo**. Haga clic en una cuenta de desarrollador, toodeactivate **bloque**. Haga clic en una cuenta de desarrollador bloqueados, tooreactivate **activar**. Una cuenta de desarrollador bloqueados no puede tener acceso a portal para desarrolladores de Hola o llamar a las API. Haga clic en una cuenta de usuario de toodelete **eliminar**.

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a>Restablecimiento de la contraseña del usuario
contraseña de hello tooreset para una cuenta de usuario, haga clic en nombre de Hola de cuenta de hello.

![Restablecimiento de contraseña][api-management-view-developer]

Haga clic en **de restablecimiento de contraseña** toosend un tooreset de usuario de vínculo toohello su contraseña.

![Restablecimiento de contraseña][api-management-reset-password]

trabajo tooprogrammatically con cuentas de usuario, vea hello [entidad de usuario](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentación Hola [API de REST de administración](https://msdn.microsoft.com/library/azure/dn776326.aspx) referencia. tooreset un valor específico del tooa de contraseña de usuario cuenta, puede usar hello [actualizar un usuario](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operación y especifique la contraseña que quieras Hola.

## <a name="pending-verification"></a>Pendiente de comprobación
![Pendiente de comprobación][api-management-pending-verification]

## <a name="next-steps"></a>Pasos siguientes
Una vez que se crea una cuenta de desarrollador, puede asociar a roles y suscribirlo tooproducts y las API. Para obtener más información, consulte [cómo toocreate y usar grupos][How toocreate and use groups].

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
