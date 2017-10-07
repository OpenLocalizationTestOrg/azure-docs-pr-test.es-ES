---
title: "Inicio de sesión de usuarios de Azure AD Connect | Microsoft Docs"
description: "Inicio de sesión de usuarios de Azure AD Connect para la configuración personalizada"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 547b118e-7282-4c7f-be87-c035561001df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7848b419f3855b25cfa074a46779d258bd534bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-user-sign-in-options"></a>Opciones para el inicio de sesión de los usuarios en Azure AD Connect
Connect de Azure Active Directory (Azure AD) permite la toosign de los usuarios en la nube de tooboth y recursos locales mediante el uso de Hola mismas contraseñas. Este artículo describe los conceptos clave para cada toohelp de modelo de identidad que elegir identidad Hola que desee toouse para iniciar sesión en tooAzure AD.

Si ya está familiarizado con el modelo de identidad de Azure AD de Hola y desea toolearn más información acerca de un método específico, consulte vínculo adecuado de hello:

* [Sincronización de contraseñas](#password-synchronization) con [inicio de sesión único (SSO)](active-directory-aadconnect-sso.md)
* [Autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md)
* [SSO federado (con Active Directory Federation Services [AD FS])](#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)

## <a name="choosing-hello-user-sign-in-method-for-your-organization"></a>Elegir Hola usuario método Inicio de sesión para su organización
Para la mayoría de las organizaciones que simplemente desee tooenable usuario inicio de sesión tooOffice 365, aplicaciones SaaS y otros recursos basados en AD de Azure, se recomienda opción de sincronización de contraseña de Hola de forma predeterminada. Algunas organizaciones, sin embargo, tienen un motivo concreto que no son toouse capaz de esta opción. Pueden elegir una opción de inicio de sesión federado, como AD FS, o la autenticación de paso a través. Puede usar Hola después toohelp tabla realizar elección correcta Hola.

Se necesita demasiado| PS con SSO| PA con SSO| AD FS |
 --- | --- | --- | --- |
Sincronizar automáticamente el nuevo usuario, contacto y cuentas de grupo en la nube de toohello de Active Directory local.|x|x|x|
Configurar mi inquilino para escenarios híbridos de Office 365|x|x|x|
Habilitar mis usuarios toosign en y servicios en la nube de acceso mediante su contraseña local.|x|x|x|
Implementar el inicio de sesión único utilizando credenciales corporativas|x|x|x|
Asegúrese de que ninguna contraseña se almacena en la nube de Hola.||x*|x|
Habilitar soluciones locales de autenticación multifactor|||x|

* A través de un conector ligero.

>[!NOTE]
> La autenticación de paso a través actualmente tiene algunas limitaciones con los clientes enriquecidos. Vea [Autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md) para obtener más detalles.

### <a name="password-synchronization"></a>Sincronización de contraseñas
Con la sincronización de contraseña, los valores hash de las contraseñas de usuario se sincronizan desde tooAzure de Active Directory local AD. Cuando las contraseñas se cambian o restablecer en local, las nuevas contraseñas Hola están sincronizado tooAzure AD inmediatamente para que los usuarios siempre pueden usar Hola igual contraseña para los recursos de nube y recursos locales. las contraseñas de Hola nunca se envían tooAzure AD o se almacenan en Azure AD en texto no cifrado. Puede utilizar la sincronización de contraseña junto con la contraseña tooenable de reescritura de restablecimiento de contraseña en Azure AD.

Además, puede habilitar [SSO](active-directory-aadconnect-sso.md) para los usuarios en los equipos unidos a un dominio que se encuentran en la red corporativa de Hola. Con inicio de sesión único, habilitada, los usuarios solo necesidad tooenter un toohelp de nombre de usuario a obtener acceso seguro a recursos de nube.

![Sincronización de contraseñas](./media/active-directory-aadconnect-user-signin/passwordhash.png)

Para obtener más información, vea hello [la sincronización de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) artículo.

### <a name="pass-through-authentication"></a>Autenticación de paso a través
Con la autenticación de paso a través, contraseña del usuario de Hola se valida con controlador de Active Directory de hello en local. contraseña de Hello no necesita toobe presente en Azure AD de ninguna forma. Esto permite para las directivas locales, como restricciones en la hora de inicio de sesión, toobe evaluada durante toocloud los servicios de autenticación.

Este tipo de autenticación usa a un agente simple en un equipo unido a un dominio de Windows Server 2012 R2 en el entorno local de Hola. que escucha las solicitudes de validación de contraseñas. Que no requiere ningún toohello abra Internet toobe de puertos de entrada.

Además, también puede habilitar un inicio de sesión único para los usuarios en los equipos unidos a un dominio que se encuentran en la red corporativa de Hola. Con inicio de sesión único, habilitada, los usuarios solo necesidad tooenter un toohelp de nombre de usuario a obtener acceso seguro a recursos de nube.
![Autenticación de paso a través](./media/active-directory-aadconnect-user-signin/pta.png)

Para más información, consulte:
- [Autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md)
- [Inicio de sesión único](active-directory-aadconnect-sso.md)

### <a name="federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2"></a>Federación con AD FS nuevo o existente en granja de Windows Server 2012 R2
Con el inicio de sesión federada, los usuarios pueden iniciar sesión en tooAzure servicios basados en AD con sus contraseñas locales. Mientras encuentra en la red corporativa de Hola, incluso no tienen tooenter sus contraseñas. Con la opción de federación de hello con AD FS, puede implementar una granja de servidores nuevo o existente con AD FS en Windows Server 2012 R2. Si elige toospecify una granja existente, Azure AD Connect configura Hola confianza entre la granja de servidores y Azure AD para que los usuarios pueden iniciar sesión.

<center>![Federación con AD FS en Windows Server 2012 R2](./media/active-directory-aadconnect-user-signin/federatedsignin.png)</center>

#### <a name="deploy-federation-with-ad-fs-in-windows-server-2012-r2"></a>Implementación de la federación con AD FS en Windows Server 2012 R2

Si va a implementar una nueva granja, necesita lo siguiente:

* Un servidor de Windows Server 2012 R2 para servidor de federación de Hola.
* Un servidor de Windows Server 2012 R2 para hello Proxy de aplicación Web.
* Un archivo .pfx con un certificado SSL para el nombre de servicio de federación previsto. Por ejemplo: fs.contoso.com.

Si va a implementar una nueva granja o va a utilizar una existente, necesita esto:

* Credenciales de administrador local en los servidores de federación.
* Credenciales de administrador local en los servidores de grupo de trabajo (no unidos a un dominio) que piensa toodeploy Hola rol Proxy de aplicación Web en.
* máquina de Hello ejecutar a Asistente de hello en toobe tooconnect pueda tooany otras máquinas que quiere tooinstall AD FS o Proxy de aplicación Web en, mediante la administración remota de Windows.

Para obtener más información, consulte [Configuración de SSO con AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

#### <a name="sign-in-by-using-an-earlier-version-of-ad-fs-or-a-third-party-solution"></a>Inicio de sesión con una versión anterior de AD FS o una solución de terceros
Si ya ha configurado en el inicio de sesión en la nube mediante el uso de una versión anterior de AD FS (por ejemplo, AD FS 2.0) o un proveedor de federación de terceros, puede elegir tooskip inicio de sesión en configuración de usuario a través de Azure AD Connect. Esto le permitirá sincronización más reciente de tooget hello y otras capacidades de Azure AD Connect mientras se sigue usando su solución existente para el inicio de sesión.

Para obtener más información, vea hello [lista de compatibilidad de federación de terceros de Azure AD](active-directory-aadconnect-federation-compatibility.md).


## <a name="user-sign-in-and-user-principal-name"></a>Inicio de sesión de usuario y nombre principal de usuario (UPN)
### <a name="understanding-user-principal-name"></a>Descripción del nombre principal de usuario
En Active Directory, sufijo de nombre principal (UPN) de usuario de hello predeterminado es nombre DNS de hello del dominio de Hola donde se creó la cuenta de usuario de Hola. En la mayoría de los casos, se trata de nombre de dominio de Hola que está registrado como dominio de empresa de hello en hello Internet. Sin embargo, puede agregar más sufijos UPN usando Dominios y confianzas de Active Directory.

Hola UPN del usuario de hello tiene formato de hello username@domain. Por ejemplo, para un dominio de Active Directory denominado "contoso.com", un usuario denominado John podría tener Hola UPN "john@contoso.com". Hola UPN del usuario de Hola se basa en RFC 822. Aunque hello UPN y recurso compartido de correo electrónico hello el mismo formato, valor Hola de hello UPN para un usuario puede ser o no igual Hola como dirección de correo electrónico de saludo del usuario de Hola.

### <a name="user-principal-name-in-azure-ad"></a>Nombre principal de usuario en Azure AD
Asistente de Azure AD Connect de Hello usa el atributo userPrincipalName de Hola o permite que especificar Hola toobe de atributo (en una instalación personalizada) que se usan desde el entorno local como nombre principal de usuario de hello en Azure AD. Este es el valor de Hola que se usa para iniciar sesión en tooAzure AD. Si Hola valor del atributo userPrincipalName de hello no corresponde tooa comprobado dominio en Azure AD, Azure AD lo reemplaza con un valor predeterminado. onmicrosoft.com valor.

Todos los directorios de Azure Active Directory incluyen un nombre de dominio integrado, con formato hello contoso.onmicrosoft.com, que permite empezar a utilizar Azure u otros servicios de Microsoft. Puede mejorar y simplificar la experiencia de inicio de sesión de hello mediante el uso de dominios personalizados. Para obtener información sobre los nombres de dominio personalizado en Azure AD y cómo ver un dominio, tooverify [agregar su tooAzure de nombre de dominio personalizado Active Directory](../add-custom-domain.md#add-your-custom-domain).

## <a name="azure-ad-sign-in-configuration"></a>Configuración de inicio de sesión de Azure AD
### <a name="azure-ad-sign-in-configuration-with-azure-ad-connect"></a>Configuración de inicio de sesión de Azure AD con Azure AD Connect
experiencia de inicio de sesión de Hello Azure AD depende de si Azure AD puede coincidir con el sufijo de nombre principal de usuario de Hola de un usuario que se va a tooone sincronizado de dominios personalizados de Hola que se comprueban en el directorio de Azure AD Hola. Azure AD Connect proporciona ayuda mientras configurar opciones de inicio de sesión Azure AD, por lo que Hola inicio de sesión de experiencia del usuario en la nube de hello es similar toohello local experiencia.

Listas de Azure AD Connect Hola sufijos UPN que se definen para toomatch de dominios y los intentos de hello ellas con un dominio personalizado en Azure AD. A continuación, puede ayudarle con la acción adecuada de Hola que necesita toobe realizada.
página de inicio de sesión de Hello Azure AD muestra los sufijos UPN de Hola que se definen para la instancia local de Active Directory y muestra el estado correspondiente de hello en cada sufijo. los valores de estado de Hola pueden ser uno de hello siguientes:

| Estado | Descripción | Se requiere acción |
|:--- |:--- |:--- |
| Verified |Azure AD Connect ha encontrado un dominio comprobado coincidente en Azure AD. Todos los usuarios de este dominio pueden iniciar sesión con sus credenciales locales. |No se requiere ninguna acción. |
| Not verified (Sin comprobar) |Azure AD Connect encontró una coincidencia de dominio personalizado en Azure AD, pero no está comprobada. sufijo UPN de Hola de usuarios de Hola de este dominio será cambia de forma predeterminada toohello. sufijo de onmicrosoft.com después de la sincronización si Hola dominio no comprobado. | [Comprobar el dominio personalizado de hello en Azure AD.](../add-custom-domain.md#verify-the-domain-name-with-azure-ad) |
| Not added (Sin agregar) |Azure AD Connect no encontró un dominio personalizado que sufijo UPN toohello correspondía. sufijo UPN de Hola de usuarios de Hola de este dominio será cambiado toohello predeterminado. onmicrosoft.com sufijo si dominio hello no agregado y comprobado en Azure. | [Agregar y comprobar un dominio personalizado que se corresponde el sufijo UPN toohello.](../add-custom-domain.md) |

página de inicio de sesión de Hello Azure AD muestra sufijos UPN de Hola que se definen para la instancia local de Active Directory y Hola correspondiente dominio personalizado en Azure AD con el estado de comprobación actual Hola. En una instalación personalizada, ahora puede seleccionar atributos de hello para el nombre principal de usuario de hello en hello **inicio de sesión en Azure AD** página.

![Página de inicio de sesión de AD Azure](./media/active-directory-aadconnect-user-signin/custom_azure_sign_in.png)

Puede hacer clic en hello actualización botón fetch toore Hola estado más reciente de los dominios personalizados Hola de Azure AD.

### <a name="selecting-hello-attribute-for-hello-user-principal-name-in-azure-ad"></a>Seleccionar atributo hello para el nombre principal de usuario de hello en Azure AD
Hola atributo userPrincipalName es el atributo de Hola que utilizan los usuarios cuando inician sesión en tooAzure AD y Office 365. Debe comprobar los dominios de hello (también conocido como sufijos UPN) que se usan en Azure AD antes de que los usuarios de Hola se sincronizan.

Se recomienda que mantenga Hola predeterminado atributo userPrincipalName. Si este atributo es nonroutable y no se puede comprobar, es posible tooselect otro atributo (por ejemplo, correo electrónico) como atributo de Hola que contiene Hola identificador de inicio de sesión. Esto se conoce como Id. alternativo de Hola valor del atributo Id. alternativo de Hello debe seguir Hola RFC 822 estándar. Puede utilizar un identificador alternativo con contraseña SSO y federación SSO como solución de inicio de sesión de Hola.

> [!NOTE]
> El uso de un identificador alternativo no es compatible con todas las cargas de trabajo de Office 365. Para obtener más información, consulte [Configuración del identificador de inicio de sesión alternativo](https://technet.microsoft.com/library/dn659436.aspx).
>
>

#### <a name="different-custom-domain-states-and-their-effect-on-hello-azure-sign-in-experience"></a>Estados de otro dominio personalizado y su efecto en la experiencia de Hola de inicio de sesión Azure
Es muy importante toounderstand Hola relación entre los Estados de dominio personalizado de Hola de su directorio Azure AD y hello sufijos UPN que están definidos en local. Analicemos Hola diferentes posibles Azure inicio de sesión experiencias cuando se está estableciendo la sincronización mediante el uso de Azure AD Connect.

En hello siguiente información, supongamos que estamos interesarán contoso.com de sufijo UPN de hello, que se usa en el directorio local de hello como parte del UPN, por ejemplo user@contoso.com.

###### <a name="express-settingspassword-synchronization"></a>Configuración rápida y sincronización de contraseñas
| Estado | Efecto en la experiencia de usuario sobre el inicio de sesión de Azure |
|:---:|:--- |
| Not added (Sin agregar) |En este caso, no se agregó ningún dominio personalizado para contoso.com Hola directorio de Azure AD. Los usuarios que tienen el UPN local con el sufijo de hello @contoso.com no será capaz de toouse su toosign UPN local en tooAzure. Toouse en su lugar deberá tienen un UPN nuevo que ha proporcionado toothem por Azure AD mediante la adición de sufijo de hello para el directorio de Azure AD de Hola de forma predeterminada. Por ejemplo, si está sincronizando usuarios toohello AD de Azure directory azurecontoso.onmicrosoft.com, a continuación, Hola local usuario user@contoso.com se proporcionará un UPN de user@azurecontoso.onmicrosoft.com. |
| Not verified (Sin comprobar) |En este caso, tenemos un contoso.com de dominio personalizado que se agrega en el directorio de hello Azure AD. Sin embargo, aún no se ha comprobado. Si continúe con la sincronización a los usuarios sin comprobar el dominio de hello, entonces los usuarios de Hola se va a asignar un UPN nuevo Azure AD, igual que en el escenario de "No se agrega" hello. |
| Verified |En este caso, tenemos un contoso.com de dominio personalizado que ya se ha agregado y comprobado en Azure AD para hello sufijo UPN. Los usuarios será capaz de toouse su nombre principal de usuario local, por ejemplo user@contoso.com, toosign en tooAzure después de que se sincronicen tooAzure AD. |

###### <a name="ad-fs-federation"></a>Federación de AD FS
No se puede crear una federación no tiene valor predeterminado de Hola. dominio de onmicrosoft.com en Azure AD o un dominio personalizado no comprobado en Azure AD. Cuando se ejecutan Asistente de hello Azure AD Connect, si selecciona un dominio no comprobado toocreate una federación con, a continuación, indicaciones de Azure AD Connect con hello necesario registra toobe creado donde esté hospedado el DNS de dominio de Hola. Para obtener más información, consulte [comprobar dominio de hello Azure AD seleccionado para la federación](active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation).

Si ha seleccionado la opción de inicio de sesión de usuario de hello **federación con AD FS**, a continuación, debe tener un toocontinue de dominio personalizado creando una federación en Azure AD. Para nuestro análisis, esto significa que debemos tenemos un contoso.com dominio personalizado que agregó en el directorio de hello Azure AD.

| Estado | Efecto en la experiencia del usuario de inicio de sesión Azure Hola |
|:---:|:--- |
| Not added (Sin agregar) |En este caso, Azure AD Connect no encontró un dominio personalizado correspondiente para contoso.com de sufijo UPN de Hola Hola directorio de Azure AD. Deberá tooadd un dominio personalizado contoso.com si tiene usuarios toosign en mediante AD FS con su UPN local (como user@contoso.com). |
| Not verified (Sin comprobar) |En este caso, Azure AD Connect le indicará los detalles sobre cómo puede comprobar el dominio en una etapa posterior. |
| Verified |En este caso, puede ir hacia delante con la configuración de hello sin ninguna acción adicional. |

## <a name="changing-hello-user-sign-in-method"></a>Cambiar el método de inicio de sesión de usuario de Hola
Puede cambiar el método de inicio de sesión de usuario de Hola de federación, la sincronización de contraseña o la autenticación de paso a través mediante tareas de Hola que están disponibles en Azure AD Connect tras la configuración inicial de Hola de Azure AD Connect con el Asistente de Hola. Vuelva a ejecutar el Asistente de Azure AD Connect de Hola y verá una lista de tareas que puede realizar. Seleccione **cambio en el inicio de sesión de usuario** en lista de Hola de tareas.

![Cambiar inicio de sesión de usuario](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

En la página siguiente de hello, se le pide las credenciales de hello tooprovide para Azure AD.

![Conectar tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2.png)

En hello **inicio de sesión de usuario** , seleccione Inicio de sesión de usuario de hello deseado.

![Conectar tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2a.png)

> [!NOTE]
> Si sólo realiza una sincronización de toopassword modificador temporal, a continuación, seleccione hello **no se convierten las cuentas de usuario** casilla de verificación. Si no activa la opción de hello convertirá cada toofederated de usuario y puede tardar varias horas.
>
>

## <a name="next-steps"></a>Pasos siguientes
- Obtenga más información sobre la [integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
- Más información sobre los [conceptos de diseño de Azure AD Connect](active-directory-aadconnect-design-concepts.md)
