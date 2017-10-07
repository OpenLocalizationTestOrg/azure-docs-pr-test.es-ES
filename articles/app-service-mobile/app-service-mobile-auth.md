---
title: "aaaAuthentication y la autorización en aplicaciones móviles de Azure | Documentos de Microsoft"
description: "Referencia conceptual e información general sobre Hola autenticación / autorización de características para las aplicaciones móviles de Azure"
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a>Autenticación y autorización en Aplicaciones móviles de Azure
## <a name="what-is-app-service-authentication--authorization"></a>¿Qué es la autenticación o autorización del Servicio de aplicaciones?
> [!NOTE]
> En este tema será tooa migrada consolidado [aplicación de servicio de autenticación / autorización](../app-service/app-service-authentication-overview.md) tema, que cubre a Web, móviles y aplicaciones de API.
> 
> 

Aplicación servicio de autenticación o autorización es una característica que permite su toolog de aplicación en los usuarios sin cambios de código necesarios en el back-end de hello aplicación. Proporciona una manera sencilla de tooprotect la aplicación y el trabajo con datos por usuario.

Servicio de aplicaciones usa identidades federadas, en el que una entidad 3rd **proveedor de identidades** ("IDP") almacena las cuentas y autentica a los usuarios y la aplicación hello usa esta identidad en lugar de su propio. Servicio de aplicaciones admite cinco proveedores de identidad fuera del cuadro de hello: *Azure Active Directory*, *Facebook*, *Google*, *Account Microsoft*, y *Twitter*. También puede ampliar esta compatibilidad con sus aplicaciones integrando otro proveedor de identidades o su propia solución de identidad personalizada.

La aplicación puede aprovechar cualquier cantidad de estos proveedores de identidades, por lo que puede proporcionar opciones de inicio de sesión a sus usuarios finales.

Si desea tooget inicia inmediatamente, vea uno de hello tutoriales:

* [Agregar aplicación de iOS de tooyour de autenticación]
* [Agregar aplicación de autenticación tooyour Xamarin.iOS]
* [Agregar aplicación de autenticación tooyour Xamarin.Android]
* [Agregar aplicación de Windows de autenticación tooyour]

## <a name="how-authentication-works"></a>Funcionamiento de la autenticación
En orden tooauthenticate mediante uno de los proveedores de identidades de hello, primero debe tooknow de proveedor de identidad de hello tooconfigure acerca de la aplicación. proveedor de identidades de Hello, a continuación, le proporcionará los identificadores y secretos que proporcionan aplicaciones toohello atrás. Esto completa la relación de confianza de Hola y permite tooit de servicio de aplicaciones toovalidate identidades proporcionadas.

Estos pasos se detallan en hello temas siguientes:

* [Cómo tooconfigure su inicio de sesión de Azure Active Directory de toouse de aplicación]
* [Cómo tooconfigure su inicio de sesión de Facebook de toouse de aplicación]
* [Cómo tooconfigure su inicio de sesión de Google de toouse de aplicación]
* [Cómo tooconfigure su inicio de sesión de aplicación toouse Account de Microsoft]
* [Cómo tooconfigure su inicio de sesión de Twitter de toouse de aplicación]

Una vez que está todo configurado en hello back-end, puede modificar su toolog de cliente en. Hay dos enfoques aquí:

* Con una sola línea de código, permiten Hola inicio de sesión SDK de cliente de aplicaciones móviles en los usuarios.
* Aprovechar un SDK publicado por una identidad de tooestablish de proveedor de identidad determinada y, a continuación, obtener acceso tooApp servicio.

> [!TIP]
> Mayoría de las aplicaciones debe utilizar un tooget SDK de proveedor una experiencia de inicio de sesión de esta sensación más nativo y compatibilidad con la actualización de tooleverage y otras ventajas específicas del proveedor.
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a>Funcionamiento de la autenticación sin un SDK del proveedor
Si no desea tooset un proveedor de SDK, puede permitir el inicio de sesión de aplicaciones móviles tooperform Hola automáticamente. SDK de cliente de aplicaciones móviles de Hola abrirá un proveedor de toohello de vista web de su inicio de sesión completa y eligiendo la opción de hello en. Ocasionalmente en blogs y foros que verá esto conoce tooas Hola "flujo de servidor" o "dirigida por el servidor de flujo" desde el servidor de hello es la administración de inicio de sesión de Hola y SDK de cliente de hello nunca recibe el token del proveedor Hola.

código de Hello necesario toostart que este flujo se trata en el tutorial de autenticación de Hola para cada plataforma. Al final de Hola de flujo de hello, Hola cliente SDK tiene un token de servicio de aplicaciones y el token de hello es tooall unido automáticamente las solicitudes toohello back-end.

### <a name="how-authentication-with-a-provider-sdk-works"></a>Funcionamiento de la autenticación con un SDK del proveedor
Trabajar con un proveedor de SDK permite toointeract de experiencia de inicio de sesión de hello más estrechamente con la plataforma de hello aplicación hello de sistema operativo se está ejecutando en. Esto le brinda un token del proveedor y cierta información de usuario en el cliente de hello, que resulta mucho más fácil de gráfico de tooconsume API y personalizar la experiencia del usuario Hola. En ocasiones, en blogs y foros verá este hello tooas denominado "flujo de cliente" o "flujo dirigida por el cliente" desde el código de cliente de hello lleva a cabo el inicio de sesión de Hola y código de cliente de hello tiene el token de acceso del proveedor tooa.

Una vez que se obtiene un token del proveedor, debe toobe envía tooApp servicio para la validación. Al final de Hola de flujo de hello, Hola cliente SDK tiene un token de servicio de aplicaciones y el token de hello es tooall unido automáticamente las solicitudes toohello back-end. desarrollador de Hello también puede mantener un token del proveedor de toohello de referencia si así lo deciden.

## <a name="how-authorization-works"></a>Funcionamiento de la autorización
Aplicación servicio de autenticación / autorización expone varias opciones de **tootake de acción cuando no se autentica la solicitud**. Antes de que el código recibe una solicitud determinada, que puede tener toosee de comprobación de servicio de aplicaciones si Hola solicitud está autenticada y si no es así, se rechaza y se intento de inicio de sesión de usuario de toohave hello en antes de intentarlo de nuevo.

Una opción es toohave sin autenticar solicitudes redirección tooone Hola de proveedores de identidades. En un explorador web, realmente tardaría tooa nueva página de usuario de Hola. Sin embargo, su cliente móvil no puede redirigirse de esta manera y las respuestas no autenticadas recibirán una respuesta HTTP del tipo *401 - No autorizado*. Por tanto, primera solicitud de hello hace que el cliente siempre debería ser toohello extremo de inicio de sesión y, a continuación, puede realizar llamadas tooany otras API. Si intentas toocall otra API antes de iniciar sesión, el cliente recibirá un error.

Si desea que toohave más granulares control sobre qué puntos de conexión requiere autenticación, también puede seleccionar "ninguna acción (solicitud de permitidas)" para las solicitudes no autenticadas. En este caso, se difieren todas las decisiones de autenticación tooyour código de la aplicación. Esto también permite tooallow acceso toospecific a los usuarios en función de reglas de autorización personalizada.

## <a name="documentation"></a>Documentación
Hola siguientes tutoriales muestran cómo tooadd autenticación tooyour los clientes móviles mediante el servicio de aplicaciones:

* [Agregar aplicación de iOS de tooyour de autenticación]
* [Agregar aplicación de autenticación tooyour Xamarin.iOS]
* [Agregar aplicación de autenticación tooyour Xamarin.Android]
* [Agregar aplicación de Windows de autenticación tooyour]

Hola siguientes tutoriales muestran cómo tooconfigure servicio de aplicaciones tooleverage diferentes proveedores de autenticación:

* [Cómo tooconfigure su inicio de sesión de Azure Active Directory de toouse de aplicación]
* [Cómo tooconfigure su inicio de sesión de Facebook de toouse de aplicación]
* [Cómo tooconfigure su inicio de sesión de Google de toouse de aplicación]
* [Cómo tooconfigure su inicio de sesión de aplicación toouse Account de Microsoft]
* [Cómo tooconfigure su inicio de sesión de Twitter de toouse de aplicación]

Si desea toouse un sistema de identidades distinto de hello los proporcionados en este caso, también puede aprovechar hello [obtener una vista previa de compatibilidad con la autenticación personalizada en el servidor de hello .NET SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).

[Agregar aplicación de iOS de tooyour de autenticación]: app-service-mobile-ios-get-started-users.md
[Agregar aplicación de autenticación tooyour Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started-users.md
[Agregar aplicación de autenticación tooyour Xamarin.Android]: app-service-mobile-xamarin-android-get-started-users.md
[Agregar aplicación de Windows de autenticación tooyour]: app-service-mobile-windows-store-dotnet-get-started-users.md

[Cómo tooconfigure su inicio de sesión de Azure Active Directory de toouse de aplicación]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Cómo tooconfigure su inicio de sesión de Facebook de toouse de aplicación]: app-service-mobile-how-to-configure-facebook-authentication.md
[Cómo tooconfigure su inicio de sesión de Google de toouse de aplicación]: app-service-mobile-how-to-configure-google-authentication.md
[Cómo tooconfigure su inicio de sesión de aplicación toouse Account de Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Cómo tooconfigure su inicio de sesión de Twitter de toouse de aplicación]: app-service-mobile-how-to-configure-twitter-authentication.md
