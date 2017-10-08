---
title: 'Azure Active Directory B2C: directivas personalizadas | Microsoft Docs'
description: Un tema acerca de las directivas personalizadas de Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1ff398a4-2079-4615-94f1-57de22c0aad6
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: bada9cf5f1a86f3dd047536f6fd9359c0231a384
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-custom-policies"></a>Azure Active Directory B2C: directivas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

## <a name="what-are-custom-policies"></a>¿Qué son las directivas personalizadas?

Las directivas personalizadas son archivos de configuración que definen el comportamiento de Hola de su inquilino de Azure AD B2C. Mientras que **directivas integradas** están predefinidos en portal de Azure AD B2C Hola para hello tareas más habituales de identidad, las directivas personalizadas puede editarse con un toocomplete de desarrollador de identidad un número casi ilimitado de tareas. Siga leyendo toodetermine si las directivas personalizadas son mejores para usted y su escenario de identidad.

**Editar directivas personalizadas no es para todos los usuarios.** curva de aprendizaje de Hello es exigentes, tiempo de inicio de hello es más largo, y directivas de cambios futuros toocustom requerirá toomaintain de experiencia similar. Es necesario considerar cuidadosamente las directivas integradas para su escenario antes de usar las directivas personalizadas.

## <a name="comparing-built-in-policies-and-custom-policies"></a>Comparación entre directivas integradas y directivas personalizadas

| | Directivas integradas | Directivas personalizadas |
|-|-------------------|-----------------|
|Usuarios de destino | Todos los desarrolladores de aplicaciones con o sin conocimientos sobre la identidad | Profesionales de identidad: integradores de sistemas, consultores y equipos internos de identidad. Se sienten cómodos con los flujos de OpenIDConnect y comprenden a los proveedores de identidades y la autenticación basada en notificaciones |
|Método de configuración | Azure Portal con una interfaz de usuario fácil de usar | Editar directamente los archivos XML y, a continuación, cargar toohello portal de Azure |
|Personalización de la interfaz de usuario | Personalización completa de la interfaz de usuario, incluida compatibilidad con HTML, CSS y JScript (requiere un dominio personalizado)<br><br>Compatibilidad multilingüe con cadenas personalizadas | Iguales |
| Personalización de atributos | Atributos estándar y personalizados | Iguales |
|Administración de tokens y sesiones | Varias opciones de sesiones y tokens personalizados | Iguales |
|Proveedores de identidades| **Actualmente**: proveedor social local predefinido<br><br>**En el futuro**: OIDC, SAML, OAuth basado en estándares | **Actualmente**: OIDC, OAUTH, SAML basado en estándares<br><br>**En el futuro**: WsFed |
|Tareas de identidad (ejemplos) | Registro o inicio de sesión con muchas cuentas sociales y cuentas locales<br><br>Restablecimiento de contraseña de autoservicio<br><br>Edición de perfil<br><br>Escenarios de Multi-Factor Authentication<br><br>Sesiones y tokens personalizados<br><br>Flujos de token de acceso | Completar Hola mismo tareas como directivas integradas con proveedores de identidades personalizados o usar ámbitos personalizados<br><br>Usuario de aprovisionar en otro sistema en tiempo de presentación del registro<br><br>Enviar un mensaje de bienvenida con su propio proveedor de servicios de correo electrónico<br><br>Usar un almacén de usuario externo a B2C<br><br>Validar la información proporcionada por el usuario con un sistema de confianza a través de API |

## <a name="policy-files"></a>Archivos de directivas

Una directiva personalizada se representa como uno o varios archivos de formato XML que hacen referencia tooeach otro en una cadena jerárquica. definen elementos XML de Hello: esquema de notificaciones, notificaciones de transformaciones, definiciones de contenido, perfiles técnica y proveedores de notificaciones y los pasos de orquestación Userjourney, entre otros elementos.

Se recomienda el uso de Hola de tres tipos de archivos de directivas:

- **Un archivo de BASE**, que contiene la mayor parte de las definiciones de Hola y para que Azure proporciona un ejemplo completo.  Se recomienda que realice un número mínimo de cambios toothis archivo toohelp con la solución de problemas y mantenimiento a largo plazo de las directivas
- **un archivo de extensiones** que contiene cambios de configuración unívoco hello para el inquilino
- **un archivo de confianza (RP)** que es único basado en tareas archivo hello invocada directamente por la aplicación hello o servicio (también conocido como usuario de confianza).  Lea el artículo de hello en las definiciones del archivo de directiva para obtener más información.  Cada tarea único requiere su propio RP y según los requisitos de personalización de marca, número de Hola podría ser "total de las aplicaciones x número total de casos de uso".


Directivas integradas en Azure AD B2C siguen el patrón de archivo de 3 de hello descrito anteriormente, pero el desarrollador de hello solo ve Hola archivo de confianza (RP), mientras que el portal de hello realiza cambios en el archivo de hello fondo toohello EXTenstions.

## <a name="core-concepts-you-should-know-when-using-custom-policies"></a>Conceptos básicos que debe saber cuando usa las directivas personalizadas

### <a name="azure-active-directory-b2c"></a>Azure Active Directory B2C

Servicio de administración de identidades y acceso de cliente (CIAM) de Azure. el servicio de Hello incluye:

1. Un directorio de usuario en forma de Hola de un especial Azure Active Directory sea accesible a través de Microsoft Graph y que contiene datos de usuario para las cuentas locales y federados 
2. Obtener acceso a toohello **identidad experiencia Framework** que organiza la relación de confianza entre los usuarios y entidades y pasa notificaciones entre ellos toocomplete una tarea de administración de identidades y acceso 
3. Un símbolo (token) servicio de seguridad (STS) emite Id. tokens, la actualización de tokens y acceso tokens (y las aserciones de SAML equivalente) y validarlos tooprotect recursos.

Azure AD B2C interactúa con proveedores de identidades, los usuarios, otros sistemas y con el directorio de usuario local de hello en secuencia tooachieve una tarea de identidad (por ejemplo, inicio de sesión de un usuario, registrar un nuevo usuario, restablecer una contraseña). Hello plataforma subyacente que establece la confianza de varias parte y ejecuta estos pasos se denomina Hola Framework de la experiencia de identidad y una directiva (también denominados un viaje de usuario o una directiva de framework de confianza) explícitamente define actores hello, acciones de hello, hello protocolos y hello secuencia de pasos toocomplete.

### <a name="identity-experience-framework"></a>Marco de experiencia de identidad

Una plataforma de Azure basada en la nube, controlada por directivas y completamente configurable que orquesta la confianza entre entidades (en general, proveedores de confianza) en formatos de protocolo estándar como OpenIDConnect, OAuth, SAML, WSFed y algunos no estándar (como intercambios de notificaciones sistema a sistema basados en API de REST, por ejemplo). Hola I2E crea fácil de usar, whitelabelled experiencias que admiten HTML, CSS y jscript.  Hoy en día, Hola identidad experiencia Framework está disponible solo en el contexto de Hola de servicio de Azure AD B2C hello y nivel de prioridad para las tareas relacionadas tooCIAM.

### <a name="built-in-policies"></a>Directivas integradas

Archivos de configuración que comportamiento Hola directa de la identidad de Azure AD B2C tooperform hello más frecuente de tareas (es decir, el registro de usuario, inicio de sesión, restablecimiento de contraseña) e interactuar con entidades de confianza cuya relación también está predefinido en Azure AD B2C (de predefinidos Por ejemplo, Facebook proveedor de identidades, LinkedIn, Microsoft Account, cuentas de Google).  Hola futuras, también pueden proporcionar directivas integradas para la personalización de los proveedores de identidades que se encuentran normalmente en territorio de enterprise hello como Azure Active Directory Premium, Active Directory o ADFS, Salesforce Id. de proveedor etcetera.


### <a name="custom-policies"></a>Directivas personalizadas

Archivos de configuración que definen el comportamiento de hello del marco de la experiencia de identidad en el inquilino de Azure AD B2C. Una directiva personalizada es accesible como uno o varios archivos XML (vea las definiciones de los archivos de directivas) que se ejecutan en hello identidad experiencia Framework cuando es invocado por un usuario de confianza (por ejemplo, una aplicación). Las directivas personalizadas se pueden editar directamente por una toocomplete de desarrollador de identidad un número casi ilimitado de tareas. Deben definir la configuración de directivas personalizadas de los desarrolladores Hola existen relaciones de confianza en los extremos de metadatos de tooinclude detalle cuidado, notificaciones exactas definiciones de exchange y configure secretos, claves y certificados según sea necesario por cada proveedor de identidades.

## <a name="policy-file-definitions-for-identity-experience-framework-trustframeworks"></a>Definiciones de archivos de directivas para marcos de confianza de Identity Experience Framework

### <a name="policy-files"></a>Archivos de directivas

Una directiva personalizada se representa como uno o varios archivos de formato XML que hacen referencia tooeach otro en una cadena jerárquica. definen elementos XML de Hello: esquema de notificaciones, notificaciones de transformaciones, definiciones de contenido, perfiles técnica y proveedores de notificaciones y los pasos de orquestación Userjourney, entre otros elementos.  Se recomienda el uso de Hola de tres tipos de archivos de directivas:

- **Un archivo de BASE**, que contiene la mayor parte de las definiciones de Hola y para que Azure proporciona un ejemplo completo.  Se recomienda que realice un número mínimo de cambios toothis archivo toohelp con la solución de problemas y mantenimiento a largo plazo de las directivas
- **un archivo de extensiones** que contiene cambios de configuración unívoco hello para el inquilino
- **un archivo de confianza (RP)** que es único basado en tareas archivo hello invocada directamente por la aplicación hello o servicio (también conocido como usuario de confianza).  Lea el artículo de hello en las definiciones del archivo de directiva para obtener más información.  Cada tarea único requiere su propio RP y según los requisitos de personalización de marca, número de Hola podría ser "total de las aplicaciones x número total de casos de uso".

![Tipos de archivos de directivas](media/active-directory-b2c-overview-custom/active-directory-b2c-overview-custom-policy-files.png)

| Tipo de archivo de directiva | Ejemplos de nombre de archivo | Uso recomendado | Hereda de |
|---------------------|--------------------|-----------------|---------------|
| BASE |TrustFrameworkBase.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_BASE1.xml | Incluye el esquema de notificaciones de núcleo de hello, las transformaciones de notificaciones, proveedores de notificaciones y viajes de usuario configurados por Microsoft<br><br>Defina los archivos de toothis unos cambios mínimos | None |
| Extensión (EXT) | TrustFrameworkExtensions.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_EXT.xml | Consolidar los cambios toohello BASE archivo aquí<br><br>Proveedores de notificaciones modificadas<br><br>Recorridos de usuario modificados<br><br>Sus propias definiciones de esquemas personalizados | Archivo BASE |
| Usuario de confianza | B2C_1A_sign_up_sign_in.xml| Cambiar aquí la configuración de la sesión y la forma del token| Archivo Extensions(EXT) |

### <a name="inheritance-model"></a>Modelo de herencia

Cuando una aplicación llama a archivo de directiva de RP de hello, Hola Identity Framework de experiencia en B2C agregará todos los elementos de Hola de BASE, a continuación, desde las extensiones y por último de Hola RP directiva archivo tooassemble Hola en vigor la directiva actual.  Elementos del programa Hola a mismo tipo y el nombre en el archivo de Hola RP invalidará en hello extensiones e invalidaciones de extensiones BASE.

**Directivas integradas** en Azure AD B2C siguen el patrón de archivo de 3 de hello descrito anteriormente, pero el desarrollador de hello solo ve Hola archivo de confianza (RP), mientras que el portal de hello realiza cambios en el archivo de hello fondo toohello EXTenstions.  Todo de Azure AD B2C comparte un archivo de BASE de directiva que está bajo control de Hola de equipo de hello B2C de Azure y se actualiza con frecuencia.
