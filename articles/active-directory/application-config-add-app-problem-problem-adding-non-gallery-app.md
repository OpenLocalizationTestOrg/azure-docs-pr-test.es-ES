---
title: "aaaProblem agregar una aplicación no Galería | Documentos de Microsoft"
description: "Comprender la cara de personas de problemas comunes de hello al agregar aplicaciones personalizadas de galería no"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: cfe9b657ae18cbacaddbd85658471a2c57c9cf95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-adding-a-non-gallery-application"></a>Problemas al agregar una aplicación que no pertenece a la galería

En este artículo le ayudará toounderstand Hola comunes problemas se enfrentan los usuarios al agregar **aplicaciones personalizadas de galería no** y lo que puede hacer tooresolve ellos. 

## <a name="i-clicked-hello-add-button-and-my-application-took-a-long-time-tooappear"></a>Hace clic en "Agregar" botón y mi aplicación tardaron un tooappear mucho tiempo de Hola

En algunas circunstancias, puede tardar entre 1 y 2 minutos (a veces, más) para una tooappear de aplicación después de Agregar directorio tooyour. Aunque no es un rendimiento normal esperado hello, puede ver la suma de aplicación Hola está en curso haciendo clic en hello **notificaciones** icono (campana Hola) en hello parte superior derecha hello [Portal de Azure](https://portal.azure.com/)y buscando un **en curso** o **completado** notificación con la etiqueta **crear aplicación**.

Si la aplicación nunca se agrega o se produce un error al hacer clic en hello **agregar** botón, verá un **notificación** en un **Error** estado. Si desea obtener más detalles sobre Hola error toolearn tooor más compartir con un engingeer de soporte técnico, puede ver más información sobre el error de hello siguiendo los pasos de Hola Hola [cómo toosee detalles de Hola de una notificación portal](#how-to-see-the-details-of-a-portal-notification) sección.

## <a name="i-clicked-hello-add-button-and-my-application-didnt-appear"></a>Hacer clic en el botón de "Agregar" hello y no aparece mi aplicación

En ocasiones, debido a problemas de tootransient, problemas de red o un error, agregar un error de aplicación. Puede indicar esto ocurre al hacer clic en hello **notificaciones** icono (campana Hola) en la esquina superior derecha de Hola de hello Portal de Azure y vea una (!) de color rojo icono siguiente tooyour **crear aplicación** notificación. Esto indica que se produjo un error al crear la aplicación hello.

Si se produce un error al hacer clic en hello **agregar** botón, verá un **notificación** en un **Error** estado. Si desea obtener más detalles sobre Hola error toolearn tooor más compartir con un engingeer de soporte técnico, puede ver más información sobre el error de hello siguiendo los pasos de Hola Hola [cómo toosee detalles de Hola de una notificación portal](#how-to-see-the-details-of-a-portal-notification) sección.

## <a name="i-dont-know-how-tooset-up-my-application-once-ive-added-it"></a>No sé cómo tooset de mi aplicación una vez he agregado se

Si necesita ayuda para obtener información sobre las aplicaciones personalizadas, Hola [biblioteca de documentos de las aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) le ayudarán a toolearn más información acerca de inicio de sesión único con Azure AD y cómo funciona.

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>¿Cómo toosee detalles de Hola de una notificación de portal

Puede ver detalles de Hola de cualquier notificación portal siguiendo estos pasos hello:

1.  Haga clic en hello **notificaciones** icono (campana Hola) en la esquina superior derecha de Hola de hello Portal de Azure

2.  Seleccione cualquier notificación de un **Error** estado (aquellos con un toothem siguiente (!) de color rojo).

   >[!NOTE]
   >No puede hacer clic en notificaciones con un estado **Correcto** o **En curso**.
   >
   >

3.  Este Hola abierto **detalles de la notificación** hoja.

4.  Utilice esta información usted mismo toounderstand más detalles sobre el problema de Hola.

5.  Si aún necesita ayuda, también puede compartir esta información con un soporte técnico o hello grupo tooget ayuda del producto con el problema.

6.  Haga clic en hello **icono de copiar** toohello derecha de hello **error al copiar** toocopy de cuadro de texto todos los Hola tooshare de detalles de notificación con un ingeniero de grupo de soporte técnico o el producto.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Cómo ayudar tooget enviando el ingeniero de soporte técnico de notificación detalles tooa

Es muy importante que use para compartir **todos los detalles que se muestran a continuación de Hola** con un ingeniero de soporte técnico si necesita ayuda, por lo que pueden ayudarle rápidamente. Puede hacer esto fácilmente mediante **tomar una captura de pantalla,** o haciendo clic en hello **icono de error de copia**, encuentra toohello derecha de hello **error al copiar** cuadro de texto.

## <a name="notification-details-explained"></a>Explicación de los detalles de la notificación

Hola a continuación explica más cada uno de los elementos de notificación de hello significa y proporciona ejemplos de cada uno de ellos.

### <a name="essential-notification-items"></a>Elementos esenciales de notificación

-   **Título** : Hola título descriptivo de la notificación de Hola
   *  Por ejemplo: **Configuración del proxy de aplicación**

-   **Descripción** : Hola descripción de lo que se produjo como resultado de la operación de Hola

   *  Por ejemplo: **la dirección url interna especificada ya se está usando en otra aplicación**

-   **Identificador de notificación** : Id. único de Hola de notificación de Hola

   *  Por ejemplo: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Id. de solicitud de cliente** : Id. de solicitud específico de hello realizado por el explorador

   *  Por ejemplo: **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Hora UTC de marca** : Hola marca de tiempo durante el cual se produjo la notificación de hello, en UTC

   *  Por ejemplo: **2017-03-23T19:50:43.7583681Z**

-   **Id. de transacción interna** : Hola Id. interno que podemos usar error de hello toolook en nuestros sistemas

   *  Por ejemplo: **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** : usuario de Hola que realizó la operación de Hola

   *  Por ejemplo: **tperkins@f128.info**

-   **Identificador de inquilino** : Hola Id. único del inquilino Hola Hola usuario que realizó la operación de hello era miembro de

   *  Por ejemplo: **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **Id. de objeto de usuario** : Hola identificador único del usuario de Hola que realizó la operación de Hola

 *  Por ejemplo: **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Elementos detallados de notificación

-   **Nombre para mostrar** : **(puede estar vacía)** un nombre para mostrar más detallado para el error de Hola

  *  Por ejemplo: **Configuración del proxy de aplicación**

-   **Estado** : Hola estado específico de notificación de Hola

   *  Por ejemplo: **Error**

-   **Id. de objeto** : **(puede estar vacía)** Hola Id. de objeto con qué Hola se realizó la operación

   *  Por ejemplo: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Detalles** : Hola una descripción detallada de lo que se produjo como resultado de la operación de Hola

   *  Por ejemplo: **la dirección url interna 'http://bing.com/' no es válida puesto que ya está en uso**

-   **Error al copiar** : haga clic en hello **icono de copiar** toohello derecha de Hola **error al copiar** toocopy de cuadro de texto todos los Hola tooshare de detalles de notificación con un ingeniero de grupo de soporte técnico o el producto

   *  Por ejemplo, ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Pasos siguientes
[Administración de aplicaciones con Azure Active Directory](active-directory-enable-sso-scenario.md)



