---
title: "las cuentas de desarrollador aaaAuthorize con Azure Active Directory - administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los usuarios de tooauthorize con Azure Active Directory en administración de API."
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a>Cómo tooauthorize developer cuentas con Azure Active Directory en la administración de API de Azure
## <a name="overview"></a>Información general
Esta guía le mostrará cómo tooenable tener acceso a portal para desarrolladores de toohello para los usuarios de Azure Active Directory. Esta guía muestra cómo Hola toomanage grupos de usuarios de Azure Active Directory mediante la adición de grupos externos que contienen a los usuarios de Active Directory de Azure.

> Hola toocomplete los pasos de esta guía primero debe tener un Azure Active Directory en qué toocreate una aplicación.
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a>Cómo tooauthorize developer cuentas con Azure Active Directory
tooget iniciado, haga clic en **portal para desarrolladores de** Hola portal de Azure para su servicio de administración de API. Esto le llevará toohello portal para desarrolladores de administración de API.

![Portal del publicador][api-management-management-console]

> Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [Introducción a administración de API de Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Haga clic en **seguridad** de hello **administración de API** menú Hola izquierda y haga clic en **identidades externas**.

![Identidades externas][api-management-security-external-identities]

Haga clic en **Azure Active Directory**. Tome nota de hello **dirección URL de redireccionamiento** y cambiar tooyour Azure Active Directory en hello Portal clásico de Azure.

![Identidades externas][api-management-security-aad-new]

Haga clic en hello **agregar** toocreate una nueva aplicación de Azure Active Directory de botón y elija **agregar una aplicación que mi organización está desarrollando**.

![Agregar nueva aplicación de Azure Active Directory][api-management-new-aad-application-menu]

Escriba un nombre para la aplicación hello, seleccione **Web de aplicación o Web API**y haga clic en el botón siguiente Hola.

![Nueva aplicación de Azure Active Directory][api-management-new-aad-application-1]

Para **dirección URL de inicio de sesión**, escriba Hola dirección URL de inicio de sesión de su portal para desarrolladores. En este ejemplo, Hola **dirección URL de inicio de sesión** es `https://aad03.portal.current.int-azure-api.net/signin`. 

Para hello **URL de Id. de aplicación**, escriba el dominio predeterminado de Hola o un dominio personalizado para hello Azure Active Directory y anexar un tooit de cadena única. En este ejemplo, Hola dominio predeterminado de **https://contoso5api.onmicrosoft.com** se usa con el sufijo de Hola de **/API** especificado.

![Propiedades de la nueva aplicación de Azure Active Directory][api-management-new-aad-application-2]

Haga clic en toosave de botón de comprobación de Hola y crear la aplicación hello y cambiar toohello **configurar** ficha nueva aplicación de tooconfigure Hola.

![Nueva aplicación de Azure Active Directory creada][api-management-new-aad-app-created]

Si varios directorios de Azure Active Directory va toobe usada para esta aplicación, haga clic en **Sí** para **aplicación es multiempresa**. valor predeterminado de Hello es **No**.

![La aplicación es multiempresa][api-management-aad-app-multi-tenant]

Hola copia **dirección URL de redireccionamiento** de hello **Azure Active Directory** sección de hello **identidades externas** pestaña en el portal para desarrolladores de Hola y pegarlos en hello **Dirección URL de respuesta** cuadro de texto. 

![URL de respuesta][api-management-aad-reply-url]

Desplazar hacia abajo de toohello de hello configurar ficha, seleccione hello **permisos de aplicación** lista desplegable y compruebe **leer datos de directorio**.

![Permisos de la aplicación][api-management-aad-app-permissions]

Seleccione hello **delegar permisos** lista desplegable y compruebe **habilitar el inicio de sesión y leer los perfiles de usuarios**.

![Permisos delegados][api-management-aad-delegated-permissions]

> Para obtener más información acerca de la aplicación y los permisos delegados, vea [Hola al tener acceso a API Graph][Accessing hello Graph API].
> 
> 

Hola copia **Id. de cliente** toohello Portapapeles.

![Id. de cliente][api-management-aad-app-client-id]

Cambie portal para desarrolladores de toohello atrás y pegue en hello **Id. de cliente** copiados de la configuración de la aplicación hello Azure Active Directory.

![Id. de cliente][api-management-client-id]

Cambiar configuración de Azure Active Directory toohello atrás y haga clic en hello **seleccione duración** desplegable Hola **claves** sección y especificar un intervalo. En este ejemplo se usa el **año 1**.

![Clave][api-management-aad-key-before-save]

Haga clic en **guardar** toosave Hola configuración y mostrar hello la clave. Copie el Portapapeles de hello toohello clave.

> Anote esta clave. Una vez que cierre la ventana de configuración de Azure Active Directory de hello, no se puede mostrar clave Hola de nuevo.
> 
> 

![Clave][api-management-aad-key-after-save]

Conmutador toohello atrás portal y pegar Hola clave del publicador en hello **secreto de cliente** cuadro de texto.

![Secreto del cliente][api-management-client-secret]

**Permite a los inquilinos** especifica los directorios que tienen acceso toohello API de instancia de servicio de administración de API de Hola. Especifique los dominios de Hola de hello toowhich de instancias de Azure Active Directory que desee toogrant acceso. Puede separar varios dominios mediante nuevas líneas, espacios o comas.

![Inquilinos permitidos][api-management-client-allowed-tenants]


Una vez Hola deseado especifica la configuración, haga clic en **guardar**.

![Save][api-management-client-allowed-tenants-save]

Una vez que se guardan los cambios de hello, los usuarios de Hola Hola especificado Azure Active Directory puede iniciar sesión en el portal para desarrolladores de toohello siguiendo los pasos de hello en [inicie sesión en el portal para desarrolladores de toohello con una cuenta de Azure Active Directory] [Log in toohello Developer portal using an Azure Active Directory account].

Se pueden especificar varios dominios en hello **permitido inquilinos** sección. Antes de que cualquier usuario puede iniciar sesión desde un dominio distinto al dominio original Hola donde se registró la aplicación hello, un administrador global de dominio diferente de hello debe conceder permiso para hello aplicación tooaccess datos de directorio. permiso de toogrant, debería ir administrador global de hello demasiado`https://<URL of your developer portal>/aadadminconsent` (por ejemplo, https://contoso.portal.azure-api.net/aadadminconsent), tipo de nombre de dominio de Hola de Hola desean toogive acceso tooand el inquilino de Active Directory, haga clic en enviar. En la siguiente Hola ejemplo, un administrador global de `miaoaad.onmicrosoft.com` está tratando de portal para desarrolladores determinado de toogive permiso toothis. 

![Permisos][api-management-aad-consent]

En la siguiente pantalla de bienvenida, administrador global de hello será solicitada tooconfirm da permiso al Hola. 

![Permisos][api-management-permissions-form]

> Si un administrador no globales intenta toolog en antes de permisos se conceden por un administrador global, se produce un error en el intento de inicio de sesión de Hola y se muestra una pantalla de error.
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a>¿Cómo tooadd un Azure Active Directory externo de grupo
Después de habilitar el acceso de usuarios en Azure Active Directory, puede agregar grupos de Azure Active Directory en administración de API toomore administran fácilmente asociación Hola de desarrolladores de hello en el grupo de hello con productos de hello deseado.

> tooconfigure un grupo externo de Azure Active Directory, hello Azure Active Directory debe configurarse primero en la pestaña de identidades de hello siguiendo el procedimiento de hello en la sección anterior de Hola. 
> 
> 

Se agregan grupos externos de Azure Active Directory de hello **visibilidad** ficha de producto de hello para el que desea toohello grupo de acceso de toogrant. Haga clic en **productos**y, a continuación, haga clic en nombre de Hola de producto de su preferencia Hola.

![Configure product][api-management-configure-product]

Cambiar toohello **visibilidad** ficha y haga clic en **agregar grupos de Azure Active Directory**.

![Agregar grupos][api-management-add-groups]

Seleccione hello **inquilino de Azure Active Directory** desde la lista desplegable de hello y, a continuación, nombre de grupo que quiera hello en Hola Hola de tipo **grupos** toobe Agregar cuadro de texto.

![Seleccionar grupo][api-management-select-group]

Este nombre de grupo puede encontrarse en hello **grupos** lista para Azure Active Directory, como se muestra en el siguiente ejemplo de Hola.

![Lista de grupos de Azure Active Directory][api-management-aad-groups-list]

Haga clic en **agregar** toovalidate Hola nombre de grupo y agregar grupo de Hola. En este ejemplo, Hola **a los desarrolladores de Contoso 5** se agrega el grupo externo. 

![Group added][api-management-aad-group-added]

Haga clic en **guardar** toosave Hola nueva selección de grupo.

Una vez que ha configurado un grupo de Azure Active Directory desde uno de los productos, está disponible toobe comprueba en hello **visibilidad** pestaña Hola otros productos de instancia de servicio de administración de API de Hola.

tooreview y configurar las propiedades de Hola para grupos externos una vez que se hayan agregado, haga clic en nombre de hello del grupo de Hola de hello **grupos** ficha.

![Administrar grupos][api-management-groups]

Desde aquí puede editar hello **nombre** hello y **descripción** del grupo de Hola.

![Editar grupo][api-management-edit-group]

Los usuarios de hello configurado Azure Active Directory puede iniciar sesión en la vista y el portal para desarrolladores de toohello y suscribirse grupos tooany para los que tienen visibilidad siguiendo las instrucciones de Hola Hola pasos de la sección.

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a>¿Cómo toolog en el portal para desarrolladores de toohello con una cuenta de Azure Active Directory
toolog en el portal para desarrolladores de hello con una cuenta de Azure Active Directory configurada en las secciones anteriores hello, abra una nueva ventana del explorador utilizando hello **dirección URL de inicio de sesión** de configuración de aplicación de Active Directory de Hola y haga clic en **Azure Active Directory**.

![Portal para desarrolladores][api-management-dev-portal-signin]

Escriba las credenciales de Hola de uno de los usuarios de hello en Azure Active Directory y haga clic en **iniciar sesión en**.

![Iniciar sesión][api-management-aad-signin]

En caso de requerirse más información, puede que se le solicite un formulario de registro. Complete el formulario de registro de hello y haga clic en **registrarse**.

![Registro][api-management-complete-registration]

Ahora, el usuario se registra en el portal para desarrolladores de hello para la instancia de servicio de administración de API.

![Registro completado][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

