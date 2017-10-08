---
title: vigencia de los tokens aaaConfigurable en Azure Active Directory | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset duraciones para tokens emiten por Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: 0d4c8545981c5463cc7c95f669167bbc38230123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a>Vigencia de tokens configurables de Azure Active Directory (versión preliminar pública)
Puede especificar la duración de Hola de un token emitido por Azure Active Directory (Azure AD). La vigencia de los tokens se puede configurar para todas las aplicaciones de una organización, para una aplicación multiinquilino (multiorganización) o para una entidad de servicio específica de una organización.

> [!NOTE]
> Esta funcionalidad se encuentra actualmente en versión preliminar pública. Prepararán toorevert o quitar los cambios. Hola característica está disponible en ninguna suscripción de Azure Active Directory durante la vista previa pública. Sin embargo, cuando la característica de hello deja de estar disponible con carácter general, algunos aspectos de la característica de hello pueden requerir un [Azure Active Directory Premium](active-directory-get-started-premium.md) suscripción.
>
>

En Azure AD, un objeto de directiva representa un conjunto de reglas que se exigen en algunas o todas las aplicaciones de una organización. Cada tipo de directiva tiene una estructura única, con un conjunto de propiedades que son toowhich tooobjects aplicados que están asignados.

Puede designar una directiva como la directiva predeterminada de Hola para su organización. Directiva de Hello es aplicación tooany aplicados en la organización de hello, siempre y cuando no se ha reemplazado por una directiva con una prioridad más alta. También puede asignar una directiva toospecific las aplicaciones. orden de Hola de prioridad varía según el tipo de directiva.


## <a name="token-types"></a>Tipos de token

Las directivas de vigencia del token se pueden establecer para tokens de actualización, tokens de acceso, tokens de sesión y tokens de identificador.

### <a name="access-tokens"></a>Tokens de acceso
Los tokens de acceso de uso de los clientes tooaccess un recurso protegido. Solo se puede utilizar un token de acceso para una combinación específica de usuario, cliente y recurso. Los tokens de acceso no se pueden revocar y son válidos hasta que caducan. Un individuo maltintencionado que haya obtenido un token de acceso puede usarlo durante toda su vigencia. Ajustar la duración de Hola de un acceso token es un equilibrio entre la mejora de rendimiento del sistema y creciente Hola cantidad de tiempo que Hola cliente mantiene el acceso cuando se deshabilita la cuenta de usuario de Hola. Se consigue un rendimiento mejorado del sistema mediante la reducción Hola número de veces que un cliente necesita tooacquire un token de acceso actualizada.

### <a name="refresh-tokens"></a>Tokens de actualización
Cuando un cliente adquiere un tooaccess de token de acceso a un recurso protegido, el cliente de hello recibe un token de actualización y un token de acceso. token de actualización de Hello es tooobtain usado nuevos pares token acceso/actualización cuando expira el token de acceso actual de Hola. Un token de actualización es la combinación de tooa enlazado de usuario y el cliente. Se pueden revocar un token de actualización y se comprueba la validez del token de hello cada vez que se usa el token de Hola.

Es importante toomake a distinguir entre los clientes de confidenciales y pública. Para más información sobre los diferentes tipos de clientes, consulte [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a>Vigencia de los tokens de actualización de cliente confidencial
Los clientes confidenciales son aplicaciones que pueden almacenar de forma segura una contraseña (secreto) de un cliente. Puede demostrar que las solicitudes proceden de la aplicación de cliente de hello y no desde un actor malintencionado. Por ejemplo, una aplicación web es un cliente confidencial porque puede almacenar un secreto de cliente en el servidor web de Hola. Y, por tanto, este secreto no se expone. Dado que estos flujos son más seguros, Hola duraciones predeterminadas de tokens de actualización es emitido toothese flujos `until-revoked`, no se puede cambiar mediante la directiva y no se revocará en los restablecimientos de contraseña voluntaria.

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a>Vigencia de los tokens de actualización de cliente público

Los clientes públicos no pueden almacenar de forma segura una contraseña (secreto) de cliente. Por ejemplo, una aplicación de iOS y Android no puede ofuscar un secreto de propietario del recurso de hello, por lo que se considera a un cliente público. Puede establecer directivas en recursos tooprevent tokens de actualización de los clientes públicos anteriores a un período especificado obtengan un nuevo par de tokens de acceso/actualización. (toodo, Hola use propiedad actualizar Token máximo tiempo inactivo..) También puede usar tooset directivas ya no se aceptan un período más allá de los tokens de actualización de Hola. (toodo, Hola use propiedad actualizar Token Max Age.) Puede ajustar la duración de Hola de un toocontrol de token de actualización cuándo y con qué frecuencia hello usuario es tooreenter requiere credenciales, en lugar de que en modo silencioso volver a autenticarse, cuando se usa una aplicación de cliente público.

### <a name="id-tokens"></a>Tokens de identificador
Tokens de identificador se pasan toowebsites y clientes nativos. Los tokens de identificador contienen información de perfil de un usuario. Un identificador de token es dependiente tooa combinación específica de usuario y el cliente. Los tokens de identificador se consideran válidos hasta que expiran. Normalmente, una aplicación web coincide con un usuario de la duración de la sesión Hola duración de aplicación toohello del token de Id. de hello emitido para usuario Hola. Puede ajustar la duración de Hola de un identificador token toocontrol con qué frecuencia aplicación web de hello expira la sesión de la aplicación hello y con qué frecuencia requiere Hola usuario toobe volver a autenticarse con Azure AD (en modo silencioso o interactiva).

### <a name="single-sign-on-session-tokens"></a>Tokens de sesión de inicio de sesión único
Cuando un usuario se autentica con Azure AD y selecciona hello **mantener la sesión iniciada** casilla de verificación, se establece una sesión de inicio de sesión única (SSO) con el explorador del usuario de Hola y Azure AD. token SSO de Hello, en forma de Hola de una cookie, representa esta sesión. Tenga en cuenta que ese token de sesión SSO hello no es aplicación de cliente y el recurso específico tooa enlazado. Los tokens de sesión SSO se pueden revocar y su validez se comprueba cada vez que se utilizan.

Azure AD usa dos tipos de tokens de sesión SSO: persistente y no persistente. Símbolos de sesión persistentes se almacenan como cookies persistentes explorador Hola. Los tokens de sesión no persistentes se almacenan como cookies de sesión. (Las cookies de sesión se destruyen cuando se cierra el Explorador de hello).

Los tokens de sesión no persistentes tienen una vigencia de 24 horas. Los tokens persistentes tienen una vigencia de 180 días. Siempre que se usa un token de sesión SSO dentro del período de validez, período de validez de Hola se extiende otro 24 horas o 180 días, según el tipo de token Hola. Si un token de sesión SSO no se usa dentro de su período de validez, se considerará caducado y ya no se aceptará.

Puede usar una directiva tooset Hola vez primer token de sesión Hola emitió más allá de qué Hola ya no se acepta el token de sesión. (toodo, Hola use propiedad Age de máximo de Token de sesión.) Puede ajustar la duración de Hola de un toocontrol de token de sesión cuándo y con qué frecuencia un usuario es tooreenter requiere credenciales, en lugar de que se autentica de forma automática, cuando se usa una aplicación web.

### <a name="token-lifetime-policy-properties"></a>Propiedades de la directiva de vigencia del token
Una directiva de vigencia del token es un tipo de objeto de directiva que contiene reglas de vigencia del token. Utilizar propiedades de Hola de hello directiva toocontrol especifican vigencia de los tokens. Si no se establece ninguna directiva, sistema de Hola exige valor de duración de hello predeterminado.

### <a name="configurable-token-lifetime-properties"></a>Propiedades de vigencia de tokens configurables
| Propiedad | Cadena de propiedad de directiva | Afecta a | Valor predeterminado | Mínima | Máxima |
| --- | --- | --- | --- | --- | --- |
| Vigencia del token de acceso |AccessTokenLifetime |Tokens de acceso, tokens de identificador, tokens de SAML2 |1 hora |10 minutos |1 día |
| Tiempo máximo de inactividad del token de actualización |MaxInactiveTime |Tokens de actualización |14 días |10 minutos |90 días |
| Antigüedad máxima del token de actualización (un solo factor) |MaxAgeSingleFactor |Tokens de actualización (para los usuarios) |Hasta que se revoca |10 minutos |Hasta que se revoca<sup>1</sup> |
| Antigüedad máxima del token de actualización (varios factores) |MaxAgeMultiFactor |Tokens de actualización (para los usuarios) |Hasta que se revoca |10 minutos |Hasta que se revoca<sup>1</sup> |
| Antigüedad máxima del token de sesión (un solo factor) |MaxAgeSessionSingleFactor<sup>2</sup> |Tokens de sesión (persistentes y no persistentes) |Hasta que se revoca |10 minutos |Hasta que se revoca<sup>1</sup> |
| Antigüedad máxima del token de sesión (varios factores) |MaxAgeSessionMultiFactor<sup>3</sup> |Tokens de sesión (persistentes y no persistentes) |Hasta que se revoca |10 minutos |Hasta que se revoca<sup>1</sup> |

* <sup>1</sup>365 días es Hola explícita la longitud máxima que se pueden establecer para estos atributos.
* <sup>2</sup>si **MaxAgeSessionSingleFactor** no se establece, este valor tiene hello **MaxAgeSingleFactor** valor. Si se establece ninguno de estos parámetros, propiedad Hola toma el valor de predeterminado de hello (hasta revocados).
* <sup>3</sup>si **MaxAgeSessionMultiFactor** no se establece, este valor tiene hello **MaxAgeMultiFactor** valor. Si se establece ninguno de estos parámetros, propiedad Hola toma el valor de predeterminado de hello (hasta revocados).

### <a name="exceptions"></a>Excepciones
| Propiedad | Afecta a | Valor predeterminado |
| --- | --- | --- |
| Antigüedad máxima de los tokens de actualización (emitidos para usuarios federados con información de revocación insuficiente<sup>1</sup>) |Tokens de actualización (emitidos para usuarios federados con información de revocación insuficiente<sup>1</sup>) |12 horas |
| Tiempo máximo de inactividad del token de actualización (emitido para clientes confidenciales) |Tokens de actualización (emitidos para clientes confidenciales) |90 días |
| Antigüedad máxima del token de actualización (emitido para clientes confidenciales) |Tokens de actualización (emitidos para clientes confidenciales) |Hasta que se revoca |

* <sup>1</sup>federado los usuarios con la información de revocación suficientes incluyen los usuarios que no tienen Hola sincronizado de atributo de "LastPasswordChangeTimestamp". Estos usuarios tienen este breve Max Age como AAD es no se puede tooverify cuando toorevoke tokens que están vinculadas tooan antigua de credenciales (por ejemplo, una contraseña que se ha cambiado) y debe vuelva a comprobarlo en tooensure con más frecuencia que el usuario hello y símbolos (tokens) asociados seguirán de buena reputación. tooimprove esta experiencia, deben asegurarse de que están sincronizando administradores de inquilinos Hola atributo "LastPasswordChangeTimestamp" (Esto puede establecerse en el objeto de usuario de hello mediante Powershell o a través de AADSync).

### <a name="policy-evaluation-and-prioritization"></a>Evaluación y prioridades de directivas
Puede crear y, a continuación, asigne una aplicación específica de duración del token directiva tooa, tooyour organización y las entidades de seguridad tooservice. Varias directivas podrían aplicar tooa de aplicación específica. Directiva de duración del token de Hola que surte efecto sigue estas reglas:

* Si una directiva se asigna explícitamente la entidad de servicio de toohello, se aplica.
* Si no hay ninguna directiva es entidad de servicio toohello asignado explícitamente, se aplica una directiva que se asigna explícitamente la organización principal de toohello de entidad de servicio de Hola.
* Si no se asigna explícitamente ninguna directiva de entidad de servicio de toohello o toohello organización, debe aplicar directiva de hello toohello aplicación asignada.
* Se aplica si no se ha asignado ninguna directiva toohello entidad de seguridad, organización Hola u objeto de aplicación Hola, Hola valores predeterminados del servicio. (Vea la tabla de hello en [propiedades de la duración del token Configurable](#configurable-token-lifetime-properties).)

Para obtener más información acerca de la relación de hello entre objetos de entidad de seguridad de servicio y aplicación, consulte [aplicación y objetos de entidad de servicio en Azure Active Directory](active-directory-application-objects.md).

Validez del token se evalúa en tiempo de Hola Hola token se utiliza. Directiva de Hello con prioridad más alta de hello en la aplicación hello que se tiene acceso surte efecto.

> [!NOTE]
> Este es un escenario de ejemplo.
>
> Un usuario desea que las aplicaciones web de tooaccess dos: aplicación Web A y B. de aplicación Web
> 
> Factores:
> * Ambas aplicaciones web están en hello mismo primario organización.
> * Símbolo (token) de duración Policy 1 con una sesión de símbolo (token) Max Age de ocho horas se establece como valor predeterminado de la organización de hello primario.
> * Aplicación Web es una aplicación web de uso normal y no está vinculado tooany directivas.
> * La aplicación web B se usa para procesos altamente confidenciales. Su entidad de servicio está vinculado tooToken 2 de la directiva de duración, que tiene una sesión de símbolo (token) Max Age de 30 minutos.
>
> A las 12:00 P.M., usuario Hola inicia una nueva sesión del explorador y usuario Hola de intentos tooaccess A. de aplicación Web es redirigido tooAzure AD y se le pide toosign en. Esto crea una cookie que tiene un token de sesión en el Explorador de Hola. usuario de Hello es tooWeb redirigida espera una aplicación con un identificador de token que permita Hola usuario tooaccess aplicación hello.
>
> A las 12:15 P.M., usuario Hola intenta tooaccess Web aplicación B. Hola explorador redirecciones tooAzure AD, que detecta la cookie de sesión de Hola. Entidad de servicio del Web de aplicación B está vinculado tooToken 2 de la directiva de duración, pero también es parte de la organización principal de hello, no tiene valor predeterminado 1 símbolo (token) de directiva de duración. Símbolo (token) de duración Policy 2 surte efecto porque las entidades de seguridad de las directivas tooservice vinculado tienen una prioridad más alta que las directivas predeterminadas de organización. el token de sesión Hola se emitió originalmente en hello últimos 30 minutos, por lo que se considera válido. usuario de Hello es tooWeb redirigida atrás aplicación B con un identificador de token que se les concede acceso.
>
> A la 1:00 P.M., Hola intentos tooaccess A. de aplicación Web Hola usuario es redirigido tooAzure AD. Una aplicación Web no está vinculado tooany directivas, pero porque está en una organización con el valor predeterminado 1 símbolo (token) de directiva de duración, esa directiva surte efecto. se detectó la cookie de sesión de Hola que se emitió originalmente en hello últimas ocho horas. usuario de Hello es tooWeb redirigida en modo silencioso atrás una aplicación con un nuevo token de identificador. Hola usuario no es necesario tooauthenticate.
>
> Inmediatamente después de ello, Hola usuario trata de usuario Hola de tooaccess B. de aplicación Web es redirigido tooAzure AD. Como antes, se aplica la directiva 2 de vigencia del token. Dado que el token de Hola se ha emitido hace más de 30 minutos, usuario hello es tooreenter solicitada sus credenciales de inicio de sesión. Se emite un nuevo token de sesión y de identificador. usuario de Hello, a continuación, puede tener acceso a Web aplicación B.
>
>

## <a name="configurable-policy-property-details"></a>Detalles de las propiedades de directiva configurables
### <a name="access-token-lifetime"></a>Vigencia del token de acceso
**Cadena:** AccessTokenLifetime

**Afecta a:** tokens de acceso, tokens de identificador

**Resumen:** esta directiva controla cuánto tiempo se consideran válidos los token de acceso y de identificador para este recurso. Reducir la propiedad de la duración del Token de acceso de hello reduce el riesgo de Hola de un token de acceso o el identificador de token que se usa un actor malintencionado durante un largo período de tiempo. (No se puede revocar estos tokens). ventajas y desventajas de Hello son que rendimiento se vea afectado negativamente, porque los tokens de hello tienen toobe reemplazado con más frecuencia.

### <a name="refresh-token-max-inactive-time"></a>Tiempo máximo de inactividad del token de actualización
**Cadena:** MaxInactiveTime

**Afecta a:** tokens de actualización

**Resumen:** esta directiva controla la antigüedad máxima que puede ser un token de actualización antes de que un cliente puede no seguir usándolo tooretrieve un nuevo par de tokens de acceso/actualización cuando se intente tooaccess este recurso. Dado que normalmente se devuelve un nuevo token de actualización cuando se usa un token de actualización, esta directiva impide el acceso si trata de cliente hello tooaccess cualquier recurso con el token de actualización actual de Hola durante Hola período de tiempo especificado.

Esta directiva obliga a los usuarios que no han estado activos en su tooretrieve de tooreauthenticate un nuevo token de actualización de cliente.

Hola propiedad actualizar Token máximo tiempo inactivo se debe establecer valor inferior tooa Hola Factor único Token Max Age y las propiedades de multifactor actualizar Token Max Age Hola.

### <a name="single-factor-refresh-token-max-age"></a>Antigüedad máxima del token de actualización (un solo factor)
**Cadena:** MaxAgeSingleFactor

**Afecta a:** tokens de actualización

**Resumen:** esta directiva controla cómo el tiempo que un usuario puede usar un tooget de símbolo (token) de la actualización de una nueva actualización de acceso/par de tokens después última autenticado correctamente utilizando solo un único factor. Después de que un usuario se autentica y recibe un nuevo token de actualización, puede utilizar usuario de hello flujo de tokens de actualización de Hola para hello especificada periodo de tiempo. (Esto ocurre siempre que no se ha revocado el token de actualización actual de hello y no se queda inactivo durante más tiempo inactivo Hola.) En ese momento, usuario de hello es forzada tooreauthenticate tooreceive un nuevo token de actualización.

Reducir la antigüedad máxima de hello fuerza tooauthenticate de los usuarios con más frecuencia. Dado que la autenticación de factor único se considera menos segura que la autenticación multifactor, se recomienda que establezca este valor de propiedad tooa que es igual tooor anterior a Hola propiedad multifactor actualizar Token Max Age.

### <a name="multi-factor-refresh-token-max-age"></a>Antigüedad máxima del token de actualización (varios factores)
**Cadena:** MaxAgeMultiFactor

**Afecta a:** tokens de actualización

**Resumen:** esta directiva controla cómo el tiempo que un usuario puede usar un tooget de símbolo (token) de la actualización de una nueva actualización de acceso/par de tokens después última autenticado correctamente mediante el uso de varios factores. Después de que un usuario se autentica y recibe un nuevo token de actualización, puede utilizar usuario de hello flujo de tokens de actualización de Hola para hello especificada periodo de tiempo. (Esto ocurre siempre que no se ha revocado el token de actualización actual de hello y no se utiliza durante más de tiempo inactivo Hola.) En ese momento, los usuarios se convierten obligatoriamente tooreauthenticate tooreceive un nuevo token de actualización.

Reducir la antigüedad máxima de hello fuerza tooauthenticate de los usuarios con más frecuencia. Dado que la autenticación de factor único se considera menos segura que la autenticación multifactor, se recomienda establecer este valor de propiedad tooa que es mayor que la propiedad de Factor único actualizar Token Max Age Hola de tooor igual.

### <a name="single-factor-session-token-max-age"></a>Antigüedad máxima del token de sesión (un solo factor)
**Cadena:** MaxAgeSessionSingleFactor

**Afecta a:** tokens de sesión (persistentes y no persistentes)

**Resumen:** esta directiva controla cuánto tiempo los usuarios pueden usar un tooget de token de sesión una vez última autenticado correctamente utilizando solo un único factor de token un identificador y una sesión de nuevo. Después de que un usuario se autentica y recibe un token de nueva sesión, usuario Hola puede utilizar el flujo de token de sesión de Hola para hello especificado período de tiempo. (Esto ocurre siempre que el token de sesión actual de hello no está revocado y no ha expirado.) Después de hello especifica el período de tiempo, usuario de hello es forzada tooreauthenticate tooreceive un token de nueva sesión.

Reducir la antigüedad máxima de hello fuerza tooauthenticate de los usuarios con más frecuencia. Como autenticación de factor único se considera menos segura que la autenticación multifactor, se recomienda establecer este valor de propiedad tooa que es propiedad de multifactor sesión Token Max Age tooor inferior Hola igual.

### <a name="multi-factor-session-token-max-age"></a>Antigüedad máxima del token de sesión (varios factores)
**Cadena:** MaxAgeSessionMultiFactor

**Afecta a:** tokens de sesión (persistentes y no persistentes)

**Resumen:** Hola de esta directiva controla cuánto tiempo los usuarios pueden usar un tooget de token de sesión un identificador y una sesión de nuevo símbolo (token) después de la última vez que autenticó correctamente mediante el uso de varios factores. Después de que un usuario se autentica y recibe un token de nueva sesión, usuario Hola puede utilizar el flujo de token de sesión de Hola para hello especificado período de tiempo. (Esto ocurre siempre que el token de sesión actual de hello no está revocado y no ha expirado.) Después de hello especifica el período de tiempo, usuario de hello es forzada tooreauthenticate tooreceive un token de nueva sesión.

Reducir la antigüedad máxima de hello fuerza tooauthenticate de los usuarios con más frecuencia. Dado que la autenticación de factor único se considera menos segura que la autenticación multifactor, se recomienda establecer este valor de propiedad tooa que es mayor que la propiedad de Factor único sesión Token Max Age Hola de tooor igual.

## <a name="example-token-lifetime-policies"></a>Ejemplo de directivas de vigencia del token
En Azure AD, hay muchos escenarios posibles a la hora de crear y administrar la vigencia de los tokens para aplicaciones, entidades de servicio y la organización en general. En esta sección, se explican algunos escenarios de directiva comunes que le ayudarán a imponer nuevas reglas para:

* Vigencia del token
* Tiempos máximos de inactividad del token
* Antigüedad máxima del token

En los ejemplos de hello, aprenderá cómo:

* Administrar una directiva predeterminada de una organización
* Crear una directiva para inicio de sesión web
* Crear una directiva para una aplicación nativa que llama a una API web
* Administrar una directiva avanzada

### <a name="prerequisites"></a>Requisitos previos
Hola en los ejemplos siguientes, crear, actualizar, vincular y eliminar directivas de aplicaciones y entidades de servicio y su organización general. Si es nuevo tooAzure AD, se recomienda que conozcas [cómo inquilino tooget un Azure AD](active-directory-howto-tenant.md) antes de continuar con estos ejemplos.  

Hola tooget iniciado, siga los pasos:

1. Descargar más reciente hello [Azure AD PowerShell módulo versión de vista previa](https://www.powershellgallery.com/packages/AzureADPreview).
2. Ejecute hello `Connect` comando toosign en tooyour cuenta de administrador de Azure AD. Ejecute este comando cada vez que inicie una nueva sesión.

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. toosee todas las directivas que se han creado en su organización, ejecución Hola siguiendo este comando. Ejecute este comando después de la mayoría de las operaciones en los escenarios siguientes de Hola. Ejecuta el comando de hello también le ayuda a conseguir Hola ** ** de las directivas.

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a>Ejemplo: Administración de una directiva predeterminada de una organización
En este ejemplo, crearemos una directiva que permita a sus usuarios iniciar sesión con menos frecuencia en toda su organización. toodo, crear una directiva de duración del token para Tokens de actualización de Factor único, que se aplica en toda la organización. Directiva de Hello es aplicación tooevery aplicada en su organización y la entidad de servicio tooeach que ya no tiene una directiva establecida.

1. Cree una directiva de vigencia del token.

    1.  Hola de conjunto de Factor único Token de actualización demasiado "hasta revocados." símbolo (token) de Hello no expire hasta que se revoca el acceso. Crear Hola después de la definición de directiva:

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  Directiva de hello toocreate, ejecute el siguiente comando de hello:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  toosee la nueva directiva y la directiva de hello tooget **ObjectId**, ejecute hello comando siguiente:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Actualizar la directiva de Hola.

    Podría decidir que no es tan estricta como exige su servicio en la primera directiva de hello establecidas en este ejemplo. tooset su Token de actualización de Factor único tooexpire en dos días, ejecute Hola comando siguiente:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a>Ejemplo: Creación de una directiva para inicio de sesión web

En este ejemplo, cree una directiva que requiere que los usuarios tooauthenticate con más frecuencia en la aplicación web. Esta directiva establece la duración de Hola de tokens de acceso/Id. de Hola y antigüedad máxima de Hola de una entidad de servicio de sesión de multifactor toohello símbolo (token) de la aplicación web.

1. Cree una directiva de vigencia del token.

    Esta directiva, para inicio de sesión en web, Establece duración del token Hola/Id. de acceso y las horas de tootwo de hello máximo de sesiones de factor único símbolo (token) de edad.

    1.  Directiva de hello toocreate, ejecute este comando:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee la nueva directiva y directiva de hello tooget **ObjectId**, ejecute hello comando siguiente:

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  Asignar la entidad de servicio de hello directiva tooyour. También necesita hello tooget **ObjectId** de la entidad de servicio. 

    1.  toosee entidades de servicio de todos los de su organización, puede consultar [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). O bien, en [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), inicie sesión en tooyour cuenta de Azure AD.

    2.  Cuando haya hello **ObjectId** de la entidad de servicio, ejecute hello siguiente comando:

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a>Ejemplo: Creación de una directiva para una aplicación nativa que llama a una API web
En este ejemplo, cree una directiva que requiere menos tooauthenticate de los usuarios con frecuencia. Directiva de Hello también alarga cantidad Hola de tiempo que un usuario puede estar inactivo antes de que debe volver a autenticar usuario Hola. Directiva de Hello es toohello aplicado web API. Cuando aplicación nativa de hello solicita hello web API como un recurso, se aplica esta directiva.

1. Cree una directiva de vigencia del token.

    1.  una directiva estricta para una API web, ejecute el siguiente comando de Hola toocreate:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee la nueva directiva y directiva de hello tooget **ObjectId**, ejecute hello comando siguiente:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Asignar Hola directiva tooyour web API. También necesita hello tooget **ObjectId** de la aplicación. Hola toofind de mejor manera su aplicación **ObjectId** es hello toouse [portal de Azure](https://portal.azure.com/).

   Cuando haya hello **ObjectId** de la aplicación, ejecute el siguiente comando de hello:

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of hello Application> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a>Ejemplo: Administración de una directiva avanzada
En este ejemplo, puede crear directivas unas, toolearn cómo funciona el sistema de prioridad de Hola. También puede obtener información sobre cómo toomanage varias directivas que son objetos tooseveral aplicada.

1. Cree una directiva de vigencia del token.

    1.  una directiva de valores predeterminados de organización que establece los días de hello too30 de duración de Token de actualización de Factor único, ejecute el siguiente comando de Hola toocreate:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  toosee la nueva directiva y la directiva de hello tooget **ObjectId**, ejecute hello comando siguiente:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Asignar la entidad de servicio de hello directiva tooa.

    Ahora, tiene una directiva que se aplica toohello toda la organización. Quizás desee toopreserve esta directiva de 30 días para una entidad de seguridad de servicio específico, pero cambie Hola organización predeterminada directiva toohello límite superior de "hasta revocados."

    1.  toosee entidades de servicio de todos los de su organización, puede consultar [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). O bien, en [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), inicie sesión mediante su cuenta de Azure AD.

    2.  Cuando haya hello **ObjectId** de la entidad de servicio, ejecute hello siguiente comando:

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
            ```
        
3. Conjunto hello `IsOrganizationDefault` marca toofalse:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. Cree una nueva directiva predeterminada de organización:

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    Ahora tiene la entidad de servicio de directiva original de hello tooyour vinculado y nueva directiva de Hola se establece como la directiva predeterminada de organización. Es importante tooremember que las entidades de seguridad de las directivas aplicadas tooservice tienen prioridad sobre las directivas predeterminadas de organización.

## <a name="cmdlet-reference"></a>Referencia de cmdlets

### <a name="manage-policies"></a>Administración de directivas

Puede usar hello las siguientes directivas de toomanage de cmdlets.

#### <a name="new-azureadpolicy"></a>New-AzureADPolicy

Crea una nueva directiva.

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| parameters | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Definition</code> |Matriz de han convertido en cadenas JSON que contiene reglas la directiva Hola todas las. | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |Cadena de nombre de la directiva de Hola. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |Si es true, Establece la directiva de hello como directiva predeterminada de la organización de Hola. Si es false, no hace nada. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |Tipo de directiva. Para la vigencia de los tokens, use siempre "TokenLifetimePolicy". | `-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code> [Opcional] |Establece un identificador alternativo para la directiva de Hola. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a>Get-AzureADPolicy
Obtiene todas las directivas de AzureAD o una directiva especificada.

```PowerShell
Get-AzureADPolicy
```

| Parámetros | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> [Opcional] |**ObjectId (Id)** de directiva de Hola que desee. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a>Get-AzureADPolicyAppliedObject
Obtiene todas las aplicaciones y entidades de servicio que están vinculadas tooa directiva.

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| parameters | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de directiva de Hola que desee. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a>Set-AzureADPolicy
Actualiza una directiva existente.

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| Parámetros | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de directiva de Hola que desee. |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |Cadena de nombre de la directiva de Hola. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;Definition</code> [Opcional] |Matriz de han convertido en cadenas JSON que contiene reglas la directiva Hola todas las. |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;IsOrganizationDefault</code> [Opcional] |Si es true, Establece la directiva de hello como directiva predeterminada de la organización de Hola. Si es false, no hace nada. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> [Opcional] |Tipo de directiva. Para la vigencia de los tokens, use siempre "TokenLifetimePolicy". |`-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code> [Opcional] |Establece un identificador alternativo para la directiva de Hola. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a>Remove-AzureADPolicy
Hola de eliminaciones especifica la directiva.

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| parameters | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de directiva de Hola que desee. | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a>Directivas de aplicación
Puede usar Hola siguientes cmdlets para las directivas de aplicación.</br></br>

#### <a name="add-azureadapplicationpolicy"></a>Add-AzureADApplicationPolicy
Hola de vínculos especificada tooan la aplicación de directiva.

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| parameters | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de aplicación hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId** de directiva de Hola. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a>Get-AzureADApplicationPolicy
Obtiene la directiva de Hola que se asigna la aplicación tooan.

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| parameters | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de aplicación hello. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a>Remove-AzureADApplicationPolicy
Quita una directiva de una aplicación.

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| Parámetros | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de aplicación hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId** de directiva de Hola. | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a>Directivas de la entidad de servicio
Puede usar Hola siguientes cmdlets para las directivas de entidad de seguridad de servicio.

#### <a name="add-azureadserviceprincipalpolicy"></a>Add-AzureADServicePrincipalPolicy
Vínculos Hola a entidad de servicio de tooa de directiva especificada.

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| parameters | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de aplicación hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId** de directiva de Hola. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a>Get-AzureADServicePrincipalPolicy
Obtiene cualquier entidad de seguridad de servicio especificado de directiva toohello vinculado.

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| parameters | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de aplicación hello. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a>Remove-AzureADServicePrincipalPolicy
Quita la directiva de Hola de entidad de servicio especificado de Hola.

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| parameters | Descripción | Ejemplo |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ObjectId (Id)** de aplicación hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId** de directiva de Hola. | `-PolicyId <ObjectId of Policy>` |
