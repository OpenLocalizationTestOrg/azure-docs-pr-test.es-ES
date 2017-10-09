---
title: "aaaHow toodelegate producto y registro de suscripción del usuario"
description: "Obtenga información acerca de cómo tooa de suscripción de producto y de registro del usuario toodelegate de terceros en la administración de API de Azure."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>La suscripción de producto y de registro de usuario toodelegate
La delegación permite toouse su sitio Web existente para controlar tooproducts de inicio de sesión-en/sesión-up y suscripción de desarrollador como opone funcionalidad integrada de toousing hello en el portal para desarrolladores de Hola. Esto permite que los datos de usuario de sitio Web tooown hello y realizar la validación de Hola de estos pasos de una manera personalizada.

## <a name="delegate-signin-up"></a>Delegación de inicios de sesión y suscripciones de desarrolladores
toodelegate developer tooyour de inicio de sesión y suscripción a un sitio Web existente que deberá toocreate un punto de conexión de delegación especial en el sitio que actúa como Hola punto de entrada para cualquiera de esas solicitudes iniciada desde el portal para desarrolladores de administración de API de Hola.

flujo de trabajo de Hello final será la siguiente:

1. Desarrollador hace clic en el vínculo de inicio de sesión o regístrese hello en hello portal de administración de API para desarrolladores
2. Browser es el punto de conexión de toohello redirigida delegación
3. Punto de conexión de la delegación de vuelta redirige tooor presenta interfaz de usuario que se pregunta usuario toosign en o inicio de sesión
4. Si se ejecuta correctamente, el usuario de hello es página de portal redirigida toohello back-administración de API para desarrolladores que inició desde

toobegin, vamos a primera tooroute de administración de API de instalación solicita a través de su punto de conexión de la delegación. En el portal para desarrolladores de administración de API hello, haga clic en **seguridad** y, a continuación, haga clic en hello **delegación** ficha. Haga clic en tooenable de casilla de verificación de hello 'Delegate inicio de sesión & inicio de sesión'.

![Delegation page][api-management-delegation-signin-up]

* Decidir cómo se pueden y escríbala de nuevo en Hola Hola URL de su punto de conexión de delegación especial **dirección URL del extremo de delegación** campo. 
* Dentro de hello **clave de autenticación de delegación** campo Escriba un secreto que será usado toocompute un tooyou firma proporcionado para comprobación tooensure que Hola solicitud procede realmente de administración de API de Azure. Puede hacer clic en hello **generar** botón toohave API Managemnet generar de forma aleatoria una clave para usted.

Ahora deberá hello toocreate **punto de conexión de delegación**. Tiene una serie de acciones tooperform:

1. Recibe una solicitud en hello siguiente forma:
   
   > *http://www.yourwebsite.com/apimdelegation?operation=SignIn&amp;returnUrl={URL de la página de origen}&amp;salt={string}&amp;sig={string}*
   > 
   > 
   
    Parámetros de consulta para el caso de inicio de sesión / registro de hello:
   
   * **operation**: identifica el tipo de solicitud de delegación del que se trata. Solo puede ser **SignIn** en este caso.
   * **returnUrl**: Hola dirección URL de página de Hola donde ha hecho clic el usuario de hello en un vínculo de inicio de sesión o regístrese
   * **salt**: una cadena salt especial que se usa para procesar un hash de seguridad
   * **SIG**: un toobe de hash calculado de seguridad utilizado para la comparación tooyour propio algoritmo hash calculado
2. Compruebe que la solicitud Hola procede de administración de API de Azure (opcional, pero muy recomendado para la seguridad)
   
   * Calcular un hash HMAC-SHA512 de una cadena basándose en hello **returnUrl** y **"salt"** parámetros de consulta ([código de ejemplo se proporciona a continuación]):
     
     > HMAC(**salt** + '\n' + **returnUrl**)
     > 
     > 
   * Comparar Hola hash calculado anteriormente toohello valor de hello **sig** parámetro de consulta. Si dos valores de hello coinciden, mueve en toohello siguiente paso, en caso contrario denegar la solicitud de Hola.
3. Comprobar que se recibe una solicitud de inicio de sesión, en/Inicio de sesión y arriba: Hola **operación** demasiado se establecerá el parámetro de consulta "**SignIn**".
4. Usuario de hello presente con interfaz de usuario en toosign o regístrese
5. Si el usuario de hello es registrarse tiene toocreate una cuenta correspondiente para ellos en administración de API. [Crear un usuario] con hello API de REST de administración. Al hacerlo, asegúrese de establecer toohello de Id. de usuario de hello mismo está en el almacén de usuario o identificador tooan que puede realizar un seguimiento de.
6. Cuando el usuario de Hola se autentica correctamente:
   
   * [solicitar un token de inicio de sesión único (SSO)] a través de hello API de REST de administración
   * anexe un parámetro de consulta returnUrl toohello dirección URL de SSO que ha recibido de la llamada de API de hello anterior:
     
     > por ejemplo, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url 
     > 
     > 
   * redirigir hello toohello de usuario por encima de la dirección URL generado

En suma toohello **SignIn** operación, también puede realizar la administración de cuentas siguiendo los pasos anteriores de Hola y utilizando una de las siguientes operaciones de Hola.

* **ChangePassword**
* **ChangeProfile**
* **CloseAccount**

Debe pasar Hola después de parámetros de consulta para las operaciones de administración de cuenta.

* **operation**: identifica qué tipo de solicitud de delegación es (ChangePassword, ChangeProfile o CloseAccount)
* **userId**: Id. de usuario de Hola de hello cuenta toomanage
* **salt**: una cadena salt especial que se usa para procesar un hash de seguridad
* **SIG**: un toobe de hash calculado de seguridad utilizado para la comparación tooyour propio algoritmo hash calculado

## <a name="delegate-product-subscription"></a>Delegación de suscripciones a productos
Delegar la suscripción del producto funciona de forma similar toodelegating usuario inicio de sesión/vertical. flujo de trabajo final Hola sería como sigue:

1. Desarrollador selecciona un producto en el portal para desarrolladores de administración de API de Hola y hace clic en el botón de suscripción de Hola
2. Browser es el punto de conexión de toohello redirigida delegación
3. Punto de conexión de delegación sigue los pasos de suscripción de producto requerido: se trata de una tooyou y puede implicar la redirección toorequest tooanother de página información de facturación, hacer preguntas adicionales, o simplemente almacenar información de hello y no requiere ninguna acción del usuario

funcionalidad de hello tooenable, en hello **delegación** página haga clic en **delegar la suscripción del producto**.

A continuación, asegúrese de punto de conexión de la delegación de hello realiza Hola siguientes acciones:

1. Recibe una solicitud en hello siguiente forma:
   
   > *{operación} http://www.yourwebsite.com/apimdelegation?Operation= & productId = {toosubscribe de producto a} & userId = {user realizar solicitud} & "salt" = {cadena} & sig = {cadena}*
   > 
   > 
   
    Parámetros de consulta para el caso de suscripción de producto de hello:
   
   * **operation**: identifica el tipo de solicitud de delegación del que se trata. Para la suscripción de producto solicitudes hello las opciones válidas son:
     * "Suscribirse": un tooa de usuario de solicitud toosubscribe Hola dada del producto con proporciona ID (ver abajo)
     * "Unsubscribe": un toounsubscribe un usuario de un producto de solicitud
     * "Renovar": un toorenew solicitud una suscripción (por ejemplo, que puede expirar)
   * **productId**: Id. de saludo del usuario de Hola de producto de hello solicitado toosubscribe a
   * **userId**: Hola Id. de usuario de hello para el que se realiza la solicitud de Hola
   * **salt**: una cadena salt especial que se usa para procesar un hash de seguridad
   * **SIG**: un toobe de hash calculado de seguridad utilizado para la comparación tooyour propio algoritmo hash calculado
2. Compruebe que la solicitud Hola procede de administración de API de Azure (opcional, pero muy recomendado para la seguridad)
   
   * Calcular un HMAC-SHA512 de una cadena basándose en hello **productId**, **userId** y **"salt"** parámetros de consulta:
     
     > HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)
     > 
     > 
   * Comparar Hola hash calculado anteriormente toohello valor de hello **sig** parámetro de consulta. Si dos valores de hello coinciden, mueve en toohello siguiente paso, en caso contrario denegar la solicitud de Hola.
3. Realizar cualquier procesamiento de suscripción de producto según el tipo de saludo de la operación solicitada en **operación** -facturación p. ej., más preguntas, etcetera.
4. Acerca de la suscripción correctamente toohello producto de usuario de hello en su lado, suscribirse el producto de administración de API de hello usuario toohello por [Hola que realiza la llamada API de REST para la suscripción de producto].

## <a name="delegate-example-code"></a> Ejemplo de código
Estos muestran ejemplos de código cómo hello tootake *clave de validación de delegación*, que se establece en pantalla de delegación de bienvenida del portal para desarrolladores de hello, toocreate un HMAC que es, a continuación, utiliza la firma de hello toovalidate, probar la validez de Hola de Hola returnUrl pasado. Hola mismo código funciona para productId hello y userId con ligeras modificaciones.

**C# código toogenerate hash returnUrl**

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

**NodeJS código hash de toogenerate de returnUrl**

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre la delegación, vea Hola después de vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[solicitar un token de inicio de sesión único (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[Cree un usuario]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[Hola que realiza la llamada API de REST para la suscripción de producto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[código de ejemplo se proporciona a continuación]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
