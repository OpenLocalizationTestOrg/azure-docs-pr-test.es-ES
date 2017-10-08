---
title: "aaaHow tooenable SSO de aplicación cruzado en iOS mediante AAL | Documentos de Microsoft"
description: "¿Cómo toouse características de Hola de Hola SDK AAL tooenable inicio de sesión único a través de las aplicaciones. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a>¿Cómo tooenable SSO de aplicación cruzado en iOS mediante AAL
Ahora se espera que proporciona el inicio de sesión único (SSO) para que los usuarios solo necesitan tooenter sus credenciales una vez y tienen esas credenciales profesional automáticamente en todas las aplicaciones por los clientes. dificultad Hola escribir su nombre de usuario y contraseña en una pantalla pequeña, a menudo veces se combinan con un factor adicional (2FA) como una llamada de teléfono o un código de mensajes de texto, resultados de insatisfacción rápido si un usuario tiene toodo esto más de una vez para el producto.

Además, si aplica una plataforma de identidad que pueden utilizar otras aplicaciones como Microsoft Accounts o una cuenta profesional de Office 365, los clientes esperan que dichos toouse disponible toobe de credenciales en todas sus aplicaciones ya no importa proveedor Hola.

Hello plataforma de Microsoft Identity, junto con nuestro SDK de identidad de Microsoft funciona todo esto disco duro para usted y proporciona Hola capacidad toodelight con SSO, ya sea dentro de su propio conjunto de aplicaciones o, como los clientes con nuestro agente capacidad y el autenticador aplicaciones, a través de dispositivo completo Hola.

Este tutorial le indicará cómo tooconfigure nuestro SDK dentro de su aplicación tooprovide esta tooyour beneficio que los clientes.

Este tutorial se aplica a:

* Azure Active Directory
* Azure Active Directory B2C
* Azure Active Directory B2B
* Acceso condicional de Azure Active Directory

documento de Hello anterior se supone que sabe cómo demasiado[aprovisionar aplicaciones en portal heredado de Hola para Azure Active Directory](active-directory-how-to-integrate.md) y la aplicación integrada con hello [SDK de iOS de Microsoft Identity](https://github.com/AzureAD/azure-activedirectory-library-for-objc).

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>Conceptos de SSO en hello plataforma de identidad de Microsoft
### <a name="microsoft-identity-brokers"></a>Agentes de Microsoft Identity
Microsoft proporciona a las aplicaciones para todas las plataformas móviles que permiten Hola puentes de credenciales en todas las aplicaciones de diferentes proveedores y admite características mejoradas especiales que requieren un único lugar seguro desde donde toovalidate credenciales. A estas aplicaciones las llamamos **agentes**. En iOS y Android estos agentes se proporcionan a través de aplicaciones que se pueden descargar que los clientes instalación de forma independiente o se pueden insertar toohello dispositivo por una compañía que administra algunos o todos los dispositivos de Hola para sus empleados. Estos agentes admiten la administración de seguridad solo para algunas aplicaciones o dispositivo completo hello en función de lo que los administradores de TI desea. En Windows, esta funcionalidad se proporciona mediante un selector de la cuenta integrada en el sistema de operativo toohello, técnicamente conocido como Hola Broker de autenticación Web.

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
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
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
 
 identidad de Hello necesidad tooensure Hola de un agente de Hola de llamada de aplicación es toohello fundamental para la seguridad por que se proporcionan en los inicios de sesión de agente asistida. IOS ni Android exige identificadores únicos que solo son válidos para una aplicación determinada, por lo que pueden "Suplantar" identificador de la aplicación legítimo y reciben los testigos de hello destinados a la aplicación legítima Hola aplicaciones malintencionadas. tooensure que siempre se comunica con la aplicación correcta de hello en tiempo de ejecución, le pedimos Hola developer tooprovide un redirectURI personalizado al registrar su aplicación con Microsoft. **A continuación se describe cómo los desarrolladores deben diseñar este URI de redirección.** Este redirectURI personalizado contiene Hola identificador de paquete de aplicación hello y está garantizada toobe toohello única aplicación por hello App Store de Apple. Cuando un agente de Hola de llamadas de aplicación, agente de hello solicita Hola iOS tooprovide de sistema de operativo Hola con Id. del lote que llama broker Hola. broker de Hello proporciona esta tooMicrosoft Id. del lote en el sistema de identidades de hello llamada tooour. Si Hola identificador de paquete de aplicación hello no coincide con Id. del lote proporcionado toous desarrollador Hola durante el registro de hello, se denegará el acceso toohello tokens para hello recursos Hola aplicación está solicitando. Esta comprobación garantiza que sólo las aplicación hello registrada por el desarrollador de hello recibe los tokens.

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
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
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
Aquí usamos hello, iOS AAL SDK para:

* Activar el SSO no asistido por agente para su conjunto de aplicaciones
* Activar la compatibilidad para el SSO asistido por agente

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>Activación del SSO para el SSO no asistido por agente
Para no es del agente asistida SSO en todas las aplicaciones Hola SDK de identidad de Microsoft administra gran parte de la complejidad de Hola de SSO por usted. Esto incluye Buscar usuario hello en memoria caché de Hola y mantiene una lista de usuarios tooquery ha iniciado sesión.

tooenable SSO en todas las aplicaciones que usted es el propietario que debe hello toodo después de:

1. Asegúrese de todos los el saludo del usuario aplicaciones mismo Id. de cliente o el identificador de aplicación
2. Asegúrese de que todos los Hola de recurso compartido de aplicaciones misma firma de certificado de Apple para que puedan compartir llaves
3. Solicitar Hola mismo derecho de cadena de claves para cada una de las aplicaciones.
4. Explíquenos SDK de identidad de Microsoft de Hola Hola compartido llaveros que desea toouse.

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>Usar Hola mismo Id. de cliente / Id. de aplicación para todas las aplicaciones en el conjunto de aplicaciones de Hola
Para tooknow de plataforma de Microsoft Identity Hola que se permite tooshare símbolos (tokens) a través de las aplicaciones, cada una de las aplicaciones necesitará tooshare Hola mismo Id. de cliente o el identificador de aplicación. Se trata de un identificador único de Hola que se proporcionó tooyou cuando registra su primera aplicación de portal de Hola.

Quizás se pregunte cómo identificará las diferentes aplicaciones toohello servicio de Microsoft Identity si utiliza Hola el mismo identificador de aplicación. es la respuesta a Hola con hello **URI de redireccionamiento**. Cada aplicación puede tener varios URI de redireccionamiento registrado en el portal de incorporación de Hola. Cada una de las aplicaciones de su conjunto tendrá diferentes URI de redirección. A continuación se muestra un ejemplo típico de su aspecto:

URI de redirección de la aplicación 1: `x-msauth-mytestiosapp://com.myapp.mytestapp`

URI de redirección de la aplicación 2: `x-msauth-mytestiosapp://com.myapp.mytestapp2`

URI de redirección de la aplicación 3: `x-msauth-mytestiosapp://com.myapp.mytestapp3`

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

#### <a name="create-keychain-sharing-between-applications"></a>Permitir el uso compartido de llaveros entre aplicaciones
Habilitar uso compartido está más allá del ámbito de Hola de este documento y cubierto por Apple en el documento [agregar capacidades](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html). Lo importante es que decidir la acción que realizará su toobe de cadena de claves denominado y agregar esa capacidad a través de todas las aplicaciones.

Cuando el usuario tiene derechos configurados correctamente, deberían ver un archivo en el directorio del proyecto titulada " `entitlements.plist` que contiene algo similar Hola siguiente:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

Una vez que tiene derechos de cadena de claves de hello habilitado en cada una de las aplicaciones, y está listo toouse SSO, explíquenos Hola SDK de Microsoft Identity su cadena de claves mediante el uso de hello después de la configuración en su `ADAuthenticationSettings` con hello después de configuración:

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> Cuando se comparte una cadena de claves a través de las aplicaciones de cualquier aplicación puede eliminar usuarios o lo que es peor eliminar todos los tokens de Hola a través de la aplicación. Esto es especialmente desastroso si tiene aplicaciones que se basan en el trabajo en segundo plano toodo Hola símbolos (tokens). Uso compartido de una cadena de claves significa que debe ser mucho cuidado en todos los quite las operaciones a través de SDK de identidad de Microsoft de Hola.
> 
> 

Eso es todo. Hola SDK de Microsoft Identity ahora compartirán las credenciales en todas sus aplicaciones. lista de usuarios de Hello también se compartirán entre instancias de la aplicación.

### <a name="turning-on-sso-for-broker-assisted-sso"></a>Activación del SSO para el SSO asistido por agente
Hola la posibilidad de que un toouse de aplicación es cualquier agente que está instalada en el dispositivo de hello **está desactivada de forma predeterminada**. En Ordenar toouse su aplicación con el agente de hello debe hacer alguna configuración adicional y agregar alguna aplicación tooyour de código.

Hola pasos toofollow son:

1. Habilitar el modo de broker en toohello de llamada del código de la aplicación MS SDK.
2. Establecer un nuevo URI de redireccionamiento y proporcionar esa aplicación de hello tooboth y el registro de aplicaciones.
3. Registrar un esquema de dirección URL.
4. compatibilidad con iOS9: agregar un archivo info.plist de tooyour de permisos.

#### <a name="step-1-enable-broker-mode-in-your-application"></a>Paso 1: Habilitar el modo de agente en la aplicación
capacidad de Hello para el agente de hello toouse de aplicación está activado cuando creas Hola "context" o la instalación inicial de su objeto de autenticación. Para ello, configure el tipo de credenciales en el código:

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
Hola `AD_CREDENTIALS_AUTO` configuración permitirá Hola SDK de Microsoft Identity tootry toocall out toohello broker, `AD_CREDENTIALS_EMBEDDED` evitará Hola SDK de Microsoft Identity de la llamada a toohello broker.

#### <a name="step-2-registering-a-url-scheme"></a>Paso 2: Registrar un esquema de dirección URL
plataforma de Microsoft Identity Hello usa broker de direcciones URL tooinvoke hello y control vuelva atrás tooyour aplicación. toofinish que necesita un esquema de dirección URL de ida y registrado para la aplicación que Hola conoce plataforma de Microsoft Identity. Esto puede ser además tooany otros esquemas de aplicación puede haber registrado previamente con la aplicación.

> [!WARNING]
> Se recomienda realizar Hola posibilidades de Hola de dirección URL esquema toominimize bastante único de otra aplicación usando Hola mismo esquema de dirección URL. Apple no exigir la exclusividad de Hola de esquemas de direcciones URL que están registrados en la tienda de aplicaciones de Hola.
> 
> 

A continuación, se muestra un ejemplo del aspecto que podría tener esto en la configuración de un proyecto. También es posible hacerlo en XCode del modo siguiente:

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a>Paso 3: Establecer un nuevo URI de redirección con el esquema de dirección URL
En orden tooensure que devolvemos siempre credenciales Hola tokens toohello de aplicación correcto, necesitamos toomake seguro que se devuelva la llamada puede comprobar la aplicación tooyour de forma que Hola de sistema operativo iOS. Hola iOS sistema operativo informes toohello Microsoft broker aplicaciones Hola identificador de paquete de aplicación hello llamarlo. Este sistema no se puede suplantar por ninguna aplicación malintencionada. Por lo tanto, hemos aprovechado esto junto con el URI de nuestro tooensure de aplicación de agente que los tokens de Hola se devuelvan toohello correcta aplicación Hola. Es necesario tooestablish este tanto en la aplicación y se establece el URI de redireccionamiento único como un URI de redireccionamiento en nuestro portal para desarrolladores.

El URI de redireccionamiento debe ser en forma adecuada de Hola de:

`<app-scheme>://<your.bundle.id>`

Por ejemplo, *x-msauth-mytestiosapp://com.myapp.mytestapp*

Este URI de redireccionamiento debe toobe especificado en el registro de aplicación con hello [portal de Azure](https://portal.azure.com/). Para más información sobre el registro de aplicaciones de Azure AD, consulte [Integración con Azure Active Directory](active-directory-how-to-integrate.md).

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a>Paso 3a: agregar un URI de redirección de la autenticación basada en certificados de portal toosupport aplicación y desarrollo
toosupport autenticación basada en certificado una segunda "msauth" necesita toobe registrado en la aplicación y hello [portal de Azure](https://portal.azure.com/) toohandle de autenticación de certificado si desea tooadd que se admiten en la aplicación.

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

Por ejemplo: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a>Paso 4: iOS9: agregar una aplicación de tooyour del parámetro de configuración
AAL usa: Canopenur: toocheck si el agente de hello está instalado en el dispositivo de Hola. En iOS 9, Apple ha bloqueado los esquemas que puede consultar una aplicación. Necesitará tooadd "msauth" toohello LSApplicationQueriesSchemes sección de su `info.plist file`.

<key>LSApplicationQueriesSchemes</key>

<array><string>msauth</string>
</array>

### <a name="youve-configured-sso"></a>Ya ha configurado el SSO.
Ahora Hola SDK de Microsoft Identity usarán automáticamente tanto comparte las credenciales a través de sus aplicaciones e invocarán a broker Hola si está presente en su dispositivo.

