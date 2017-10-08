---
title: "aaaHow tooenable SSO de aplicación cruzado en Android mediante AAL | Documentos de Microsoft"
description: "¿Cómo toouse características de Hola de Hola SDK AAL tooenable inicio de sesión único a través de las aplicaciones. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a>¿Cómo tooenable SSO de aplicación cruzado en Android mediante AAL
Ahora se espera que proporciona el inicio de sesión único (SSO) para que los usuarios solo necesitan tooenter sus credenciales una vez y tienen esas credenciales profesional automáticamente en todas las aplicaciones por los clientes. dificultad Hola escribir su nombre de usuario y contraseña en una pantalla pequeña, a menudo veces se combinan con un factor adicional (2FA) como una llamada de teléfono o un código de mensajes de texto, resultados de insatisfacción rápido si un usuario tiene toodo esto más de una vez para el producto.

Además, si aplica una plataforma de identidad que pueden utilizar otras aplicaciones como Microsoft Accounts o una cuenta profesional de Office 365, los clientes esperan que dichos toouse disponible toobe de credenciales en todas sus aplicaciones ya no importa proveedor Hola.

Hello plataforma de Microsoft Identity, junto con nuestro SDK de identidad de Microsoft funciona todo esto disco duro para usted y proporciona Hola capacidad toodelight con SSO, ya sea dentro de su propio conjunto de aplicaciones o, como los clientes con nuestro agente capacidad y el autenticador aplicaciones, a través de dispositivo completo Hola.

Este tutorial le indicará cómo tooconfigure nuestro SDK dentro de su aplicación tooprovide esta tooyour beneficio que los clientes.

Este tutorial se aplica a:

* Azure Active Directory
* Azure Active Directory B2C
* Azure Active Directory B2B
* Acceso condicional de Azure Active Directory

documento de Hello anterior se supone que sabe cómo demasiado[aprovisionar aplicaciones en portal heredado de Hola para Azure Active Directory](active-directory-how-to-integrate.md) y la aplicación integrada con hello [SDK de Android de identidad de Microsoft](https://github.com/AzureAD/azure-activedirectory-library-for-android) .

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>Conceptos de SSO en hello plataforma de identidad de Microsoft
### <a name="microsoft-identity-brokers"></a>Agentes de Microsoft Identity
Microsoft proporciona a las aplicaciones para todas las plataformas móviles que permiten Hola puentes de credenciales en todas las aplicaciones de diferentes proveedores y admite características mejoradas especiales que requieren un único lugar seguro desde donde toovalidate credenciales. A estas aplicaciones las llamamos **agentes**. En iOS y Android estos se proporcionan a través de aplicaciones que se pueden descargar que los clientes instalación de forma independiente o se pueden insertar toohello dispositivo por una compañía que administra algunos o todos los dispositivos de Hola para sus empleados. Estos agentes admiten la administración de seguridad solo para algunas aplicaciones o dispositivo completo hello en función de lo que los administradores de TI desea. En Windows, esta funcionalidad se proporciona mediante un selector de la cuenta integrada en el sistema de operativo toohello, técnicamente conocido como Hola Broker de autenticación Web.

Para obtener más información acerca de cómo se utilizan estos agentes y cómo los clientes pueden verlas en su flujo de inicio de sesión para la plataforma de Microsoft Identity Hola de lectura en.

### <a name="patterns-for-logging-in-on-mobile-devices"></a>Patrones para iniciar sesión en dispositivos móviles
Toocredentials de acceso en los dispositivos siga dos patrones básicos para la plataforma de Microsoft Identity hello:

* Inicios de sesión no asistidos por agente
* Inicios de sesión asistidos por agente

#### <a name="non-broker-assisted-logins"></a>Inicios de sesión no asistidos por agente
Los inicios de sesión del agente no asistidas son experiencias de inicio de sesión que se realizan en línea con la aplicación hello y usar el almacenamiento local de hello en dispositivo Hola para esa aplicación. Este almacenamiento puede compartirse en todas las aplicaciones pero credenciales Hola están estrechamente toohello aplicación o conjunto de aplicaciones con esa credencial. Probablemente ha experimentado esto en muchas aplicaciones móviles al escribir un nombre de usuario y contraseña en la propia aplicación Hola.

Estos inicios de sesión tienen Hola siguientes ventajas:

* Experiencia del usuario existe completamente dentro de la aplicación hello.
* Las credenciales se pueden compartir entre las aplicaciones que están firmadas por hello mismo certificado, lo que proporciona un conjunto de tooyour de la experiencia de inicio de sesión único de aplicaciones.
* Control alrededor de la experiencia de hello del inicio de sesión se proporciona toohello aplicación antes y después del inicio de sesión.

Estos inicios de sesión tienen Hola siguientes desventajas:

* El usuario no puede experimentar el inicio de sesión único entre todas las aplicaciones que usan una identidad de Microsoft Identity, solo en aquellas identidades de Microsoft Identity que su aplicación ha configurado.
* La aplicación no se puede usar con las características más avanzadas de negocios como acceso condicional o use Hola InTune conjunto de productos.
* La aplicación no admite la autenticación basada en certificados para usuarios empresariales.

Aquí es una representación de cómo funcionan los SDK de identidad de Microsoft hello con almacenamiento de hello compartido de su tooenable aplicaciones SSO:

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a>Inicios de sesión asistidos por agente
Asistido por el agente de inicios de sesión son experiencias de inicio de sesión que se producen dentro de la aplicación de broker de hello y utilizar almacenamiento de Hola y seguridad de credenciales de hello broker tooshare en todas las aplicaciones en dispositivos de Hola que se aplican de la plataforma de Microsoft Identity Hola. Esto significa que las aplicaciones dependen de los usuarios de hello broker toosign en. En iOS y Android estos agentes se proporcionan a través de aplicaciones que se pueden descargar que los clientes instalación de forma independiente o se pueden insertar toohello dispositivo por una compañía que administra el dispositivo de hello para el usuario. Un ejemplo de este tipo de aplicación es la aplicación de Microsoft Authenticator hello en iOS. En Windows, esta funcionalidad se proporciona mediante un selector de la cuenta integrada en el sistema de operativo toohello, técnicamente conocido como Hola Broker de autenticación Web.
experiencia de Hello varía según la plataforma y a veces puede ser perjudiciales toousers si no administra correctamente. Es probablemente más familiarizado con este patrón si tiene instalada la aplicación de Facebook de Hola y usar Facebook Connect desde otra aplicación. Hello usa de la plataforma de Microsoft Identity Hola mismo patrón.

Para iOS Esto conduce animación de "transición" tooa donde la aplicación se envía a toohello fondo mientras las aplicaciones de Microsoft Authenticator Hola procede de primer plano de toohello para hello usuario tooselect qué cuenta preferirían toosign con.  

Android y Windows cuenta Hola selector se muestra encima de la aplicación que es menos problemática toohello al usuario.

#### <a name="how-hello-broker-gets-invoked"></a>¿Cómo se invoca broker Hola
Si está instalado un agente compatible en dispositivos de hello, que configurará automáticamente y Hola aplicación Microsoft Authenticator, Hola SDK de identidad de Microsoft Hola trabajo de invocar broker Hola automáticamente cuando un usuario indica que hubieran querido toolog con cualquier cuenta de plataforma de Microsoft Identity Hola. Esta cuenta podría tratarse de una cuenta personal de Microsoft, una cuenta profesional o educativa o una cuenta que especifique y hospede en Azure mediante nuestros productos B2C y B2B. 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a>Cómo garantizamos que la aplicación hello es válido
 
 identidad de Hello necesidad tooensure Hola de un agente de Hola de llamada de aplicación es toohello fundamental para la seguridad por que se proporcionan en los inicios de sesión de agente asistida. IOS ni Android exige identificadores únicos que solo son válidos para una aplicación determinada, por lo que pueden "Suplantar" identificador de la aplicación legítimo y reciben los testigos de hello destinados a la aplicación legítima Hola aplicaciones malintencionadas. tooensure que siempre se comunica con la aplicación correcta de hello en tiempo de ejecución, le pedimos Hola developer tooprovide un redirectURI personalizado al registrar su aplicación con Microsoft. **A continuación se describe cómo los desarrolladores deben diseñar este URI de redirección.** Este redirectURI personalizada contiene la huella digital del certificado de la aplicación hello hello y está garantizada toobe toohello única aplicación por hello Google Play Store. Cuando una aplicación llama broker hello, broker Hola pide tooprovide de sistema operativo Android Hola con hello huella digital del certificado que broker Hola llamado. broker de Hello proporciona esta tooMicrosoft de huella digital de certificado en el sistema de identidades de hello llamada tooour. Si certificado Hola huella digital de la aplicación hello no coincide con la huella digital del certificado Hola proporcionado toous desarrollador Hola durante el registro, se denegará el acceso toohello tokens para hello recursos Hola aplicación está solicitando. Esta comprobación garantiza que sólo las aplicación hello registrada por el desarrollador de hello recibe los tokens.

**desarrollador de Hello tiene elección Hola de si Hola SDK de Microsoft Identity llama a broker Hola o usa flujo asistida de hello no es del agente.** Sin embargo si el desarrollador de hello elige no flujo asistidas por el agente de Hola de toouse pierden ventaja de hello del uso de credenciales de SSO que el usuario Hola puedas haber agregado ya en el dispositivo de Hola e impide que su aplicación que se va a usar con las características de business Microsoft proporciona a los clientes, como el acceso condicional y capacidades de administración de Intune, autenticación basada en certificados.

Estos inicios de sesión tienen Hola siguientes ventajas:

* Usuario experimenta SSO a través de todas sus aplicaciones, independientemente del proveedor de Hola.
* La aplicación puede utilizar las características más avanzadas de negocio, como el acceso condicional o conjunto de productos de hello InTune.
* La aplicación puede admitir la autenticación basada en certificados para los usuarios empresariales.
* Inicio de sesión mucho más segura de experimentar como identidad de Hola de aplicación hello y usuario Hola se comprobó por aplicación de broker de hello con algoritmos de seguridad adicional y el cifrado.

Estos inicios de sesión tienen Hola siguientes desventajas:

* En iOS usuario Hola pasa fuera de la experiencia de su aplicación mientras se eligen las credenciales.
* Pérdida de inicio de sesión de hello capacidad toomanage Hola experiencia para sus clientes dentro de la aplicación.

Aquí es una representación de cómo de trabajo del SDK de identidad de Microsoft de hello con hello broker tooenable aplicaciones SSO:

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

Gracias a esta información debe ser capaz de toobetter comprender e implementar SSO dentro de la aplicación con la plataforma de Microsoft Identity hello y SDK.

## <a name="enabling-cross-app-sso-using-adal"></a>Habilitación del SSO entre aplicaciones mediante ADAL
Aquí usamos Hola AAL Android SDK para:

* Activar el SSO no asistido por agente para su conjunto de aplicaciones
* Activar la compatibilidad para el SSO asistido por agente

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>Activación del SSO para el SSO no asistido por agente
Para no es del agente asistida SSO en todas las aplicaciones Hola SDK de identidad de Microsoft administra gran parte de la complejidad de Hola de SSO por usted. Esto incluye Buscar usuario hello en memoria caché de Hola y mantiene una lista de usuarios tooquery ha iniciado sesión.

tooenable SSO en todas las aplicaciones que usted es el propietario que debe hello toodo después de:

1. Asegúrese de todos los el saludo del usuario aplicaciones mismo Id. de cliente o el identificador de aplicación
2. Asegúrese de que todas las aplicaciones tienen hello que shareduserid mismo conjunto.
3. Asegúrese de que todos los Hola de recurso compartido de aplicaciones mismo certificado de firma de hello Google Play almacenar para que puedan compartir almacenamiento.

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>Paso 1: Usar Hola mismo Id. de cliente / Id. de aplicación para todas las aplicaciones en el conjunto de aplicaciones de Hola
Para tooknow de plataforma de Microsoft Identity Hola que se permite tooshare símbolos (tokens) a través de las aplicaciones, cada una de las aplicaciones necesitará tooshare Hola mismo Id. de cliente o el identificador de aplicación. Se trata de un identificador único de Hola que se proporcionó tooyou cuando registra su primera aplicación de portal de Hola.

Quizás se pregunte cómo identificará las diferentes aplicaciones toohello servicio de Microsoft Identity si utiliza Hola el mismo identificador de aplicación. es la respuesta a Hola con hello **URI de redireccionamiento**. Cada aplicación puede tener varios URI de redireccionamiento registrado en el portal de incorporación de Hola. Cada una de las aplicaciones de su conjunto tendrá diferentes URI de redirección. A continuación se muestra un ejemplo típico de su aspecto:

URI de redirección de la aplicación 1: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`

URI de redirección de la aplicación 2: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`

URI de redirección de la aplicación 3: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`

....

Estos se anidan debajo de Hola el mismo Id. de cliente / volver toous en la configuración del SDK de URI de redireccionamiento de Id. de aplicación y buscada Hola según.

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


*Tenga en cuenta que el formato de estos URI de redireccionamiento de Hola se explican a continuación. Puede usar cualquier URI de redireccionamiento a menos que se desea que el agente de hello toosupport, en cuyo caso debe ser similar a Hola anterior*

#### <a name="step-2-configuring-shared-storage-in-android"></a>Paso 2: Configuración del almacenamiento compartido en Android
Hola configuración `SharedUserID` cubre Hola de este documento, pero puede aprender, lea la documentación de Google Android en Hola Hola [manifiesto](http://developer.android.com/guide/topics/manifest/manifest-element.html). Lo importante es que decida cómo desea llamar a su sharedUserID y usar ese nombre en todas sus aplicaciones.

Una vez que tenga hello `SharedUserID` en todas las aplicaciones están listo toouse SSO.

> [!WARNING]
> Cuando se comparte el almacenamiento a través de las aplicaciones de cualquier aplicación puede eliminar usuarios o peor eliminar todos los tokens de Hola a través de la aplicación. Esto es especialmente desastroso si tiene aplicaciones que se basan en el trabajo en segundo plano toodo Hola símbolos (tokens). Uso compartido de almacenamiento significa que debe ser muy cuidadoso en las operaciones de quitar todos a través de hello SDK de identidad de Microsoft.
> 
> 

Eso es todo. Hola SDK de Microsoft Identity ahora compartirán las credenciales en todas sus aplicaciones. lista de usuarios de Hello también se compartirán entre instancias de la aplicación.

### <a name="turning-on-sso-for-broker-assisted-sso"></a>Activación del SSO para el SSO asistido por agente
Hola la posibilidad de que un toouse de aplicación es cualquier agente que está instalada en el dispositivo de hello **está desactivada de forma predeterminada**. En Ordenar toouse su aplicación con el agente de hello debe hacer alguna configuración adicional y agregar alguna aplicación tooyour de código.

Hola pasos toofollow son:

1. Habilitar el modo de broker en toohello de llamada del código de la aplicación MS SDK
2. Establecer un nuevo URI de redireccionamiento y proporcionar esa aplicación de hello tooboth y el registro de aplicaciones
3. Establecer los permisos correctos de hello en el manifiesto de Android Hola

#### <a name="step-1-enable-broker-mode-in-your-application"></a>Paso 1: Habilitar el modo de agente en la aplicación
capacidad de Hello para el agente de hello toouse de aplicación está activado cuando se crea la configuración"Hola" o la instalación inicial de la instancia de la autenticación. Para ello, configure el tipo de ApplicationSettings en el código:

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a>Paso 2: Establecer un nuevo URI de redirección con el esquema de dirección URL
En orden tooensure que devolvemos siempre credenciales Hola tokens toohello de aplicación correcto, necesitamos toomake seguro que se devuelva la llamada puede comprobar la aplicación tooyour de forma que Hola sistema operativo Android. sistema operativo Android de Hello usa hash Hola certificado Hola Hola Google Play store. Este sistema no se puede suplantar por ninguna aplicación malintencionada. Por lo tanto, hemos aprovechado esto junto con el URI de nuestro tooensure de aplicación de agente que los tokens de Hola se devuelvan toohello correcta aplicación Hola. Es necesario tooestablish este tanto en la aplicación y se establece el URI de redireccionamiento único como un URI de redireccionamiento en nuestro portal para desarrolladores.

El URI de redireccionamiento debe ser en forma adecuada de Hola de:

`msauth://packagename/Base64UrlencodedSignature`

Por ejemplo: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*

Este URI de redireccionamiento debe toobe especificado en el registro de aplicación con hello [portal de Azure](https://portal.azure.com/). Para más información sobre el registro de aplicaciones de Azure AD, consulte [Integración con Azure Active Directory](active-directory-how-to-integrate.md).

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a>Paso 3: Configurar los permisos correctos de hello en la aplicación
Nuestra aplicación de broker en Android usa la característica de administrador de cuentas de Hola de credenciales de hello Android OS toomanage en todas las aplicaciones. En el agente de pedido toouse hello en Android el manifiesto de aplicación debe tener cuentas de administrador de cuentas de toouse de permisos. Esto se explica en detalle en hello [Google documentación para el Administrador de cuentas](http://developer.android.com/reference/android/accounts/AccountManager.html)

En concreto, estos permisos son:

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a>Ya ha configurado el SSO.
Ahora Hola SDK de Microsoft Identity usarán automáticamente tanto comparte las credenciales a través de sus aplicaciones e invocarán a broker Hola si está presente en su dispositivo.

