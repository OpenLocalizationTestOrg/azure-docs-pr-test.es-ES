---
title: Aplicaciones, permisos y consentimiento en Azure Active Directory | Microsoft Docs
description: "Azure AD Connect integrará sus directorios locales con Azure Active Directory. Esto le permite tooprovide una identidad común para las aplicaciones de Office 365, Azure y SaaS integrada con Azure AD."
keywords: "Introducción tooAzure AD, aplicaciones, ¿qué es Azure AD Connect, instalar active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a>Aplicaciones, permisos y consentimiento en Azure Active Directory
Dentro de Azure Active Directory, puede agregar el directorio de aplicaciones tooyour.  las aplicaciones de Hello pueden variar según el tipo de Hola de aplicación.  tooview aplicaciones en portal clásico de hello, seleccione un directorio y elija aplicaciones.

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.

## <a name="types-of-apps"></a>Tipos de aplicaciones

1. **Aplicaciones de inquilino único** </br>
    - **Aplicaciones de inquilinos solo** -a menudo se conoce tooas aplicaciones de línea de negocio (LOB). Esto es así de Hola donde alguien de su organización desarrolla su propia aplicación y desea que los usuarios en hello organización toobe puede toosign en toohello aplicación.
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - **Aplicaciones de Proxy de aplicación** : al exponer una aplicación local con el Proxy de aplicación de Azure AD, una aplicación único inquilino esté registrada en el inquilino (en el servicio de Proxy de aplicación de suma toohello). Esta aplicación es la que representará la aplicación local en todas las interacciones en la nube (por ejemplo, en la autenticación). (Proxy de aplicación requiere Azure AD Basic o superior).


2. **Aplicaciones multiinquilino**
    - **Aplicaciones de varios inquilinos que otras personas puedan permitir** : similar demasiado "único inquilino de aplicaciones que desarrolla la organización". Hola principal diferencia (además de la lógica de hello en la propia aplicación Hola) es que los usuarios de otros inquilinos también pueden dar su consentimiento tooand de inicio de sesión toohello aplicación.</br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - **Aplicaciones multiinquilino que desarrollan otros, a las que Contoso puede dar consentimiento**. (O "aplicaciones consentidas", para abreviar). Se trata de hello flip lado de "de su organización desarrolla aplicaciones multiempresa". Cuando otra organización desarrolla una aplicación de varios inquilinos, los usuarios de su organización pueden dar su consentimiento toohello aplicación e inicie sesión tooit.
    - **Aplicaciones propias de Microsoft**: las aplicaciones que representan los servicios de Microsoft. Consentimiento está controlado por el hecho de Hola que se registra para el servicio de Hola. A veces hay especial UX y la lógica para ciertas aplicaciones de cookies que se suele utilizar al establecimiento de directivas de aplicación de toohello de acceso.</br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - **Aplicaciones integradas previamente** -aplicaciones disponibles en la Galería de aplicaciones de Azure AD, que puede agregar hello tooyour directory tooprovide single sign-on (y en algunos casos, el aprovisionamiento) toopopular aplicaciones de SaaS.
    - **Inicio de sesión único de Azure AD**: inicio de sesión único "real" para las aplicaciones que se pueden integrar con Azure AD, mediante un protocolo de inicio de sesión compatible como SAML 2.0 o OpenID Connect. Hola asistente le guiará a través de su configuración.
    - **Inicio de sesión único en la contraseña**: Azure AD guarda las credenciales del usuario de hello para la aplicación hello y credenciales de Hola se "insertadas" en el formulario de inicio de sesión de Hola por hello extensión del explorador de acceso de la aplicación de Azure AD. A este proceso también se le conoce como "almacenamiento de contraseñas".

## <a name="permissions"></a>Permisos

Cuando se registra una aplicación, usuario de hello realizando el registro de aplicación Hola (es decir, el desarrollador de hello) define qué aplicación de hello permisos necesita tener acceso a y qué recursos. (recursos de hello son, por sí mismos, definido como otras aplicaciones). Por ejemplo, alguien compilar una aplicación de lector de correo electrónico, podría indicar que su aplicación requiere el permiso de "Acceso a los buzones como usuario con sesión iniciada Hola" Hola Hola "Office 365 Exchange Online" recursos:
    
![](media/active-directory-apps-permissions-consent/apps6.png)

En orden para una aplicación (cliente hello) toorequest cierto permiso desde otra aplicación (recurso hello), desarrollador Hola de aplicación de recursos de hello define los permisos de Hola que existen. En nuestro ejemplo, Microsoft, propietario de Hola de aplicación de recursos "Office 365 Exchange Online" hello, ha definido un permiso denominado "Acceso a los buzones como usuario con sesión iniciada Hola".

Al definir los permisos, debe definir desarrollador de aplicaciones de hello si puede ser consentido permiso hello, o si se requiere el consentimiento del administrador. Esto permite a los desarrolladores tooallow tooconsent de los usuarios en sus propios tooapps solicita solo baja sensibilidad permisos, pero requieren permisos de administradores tooconsent toomore confidenciales. Por ejemplo, Hola "Azure Active Directory" aplicación de recurso, se ha definido, por lo que los usuarios pueden consentir tooapps, solicitar permisos limitados de solo lectura.  Sin embargo, se requiere el consentimiento del administrador para conseguir permisos completos de lectura y para todos los permisos de escritura.

Puesto que no se autentican clientes nativos, una aplicación que se define como una aplicación de cliente nativo solo puede solicitar permisos delegados. Esto significa que siempre debe haber un usuario real implicado en la obtención de un token. Las aplicaciones web y API web (clientes confidenciales), siempre se deben autenticar con Azure AD al acceder a un token. Lo que significa que tienen también la posibilidad de hello de la solicitud de permisos solo de aplicación. Por ejemplo, si un servicio back-end necesita servicio back-end de tooauthenticate tooanother. Las aplicaciones que solicitan permisos de solo aplicación requieren siempre el consentimiento del administrador.

En resumen:



- Una aplicación (cliente) indica que los permisos de Hola que necesita para otras aplicaciones (recursos).
- Una aplicación (recurso) indica qué permisos son tooother expuesto aplicaciones (clientes).
- Un permiso puede ser un permiso de solo aplicación o un permiso delegado.
- Un permiso delegado se puede marcar para indicar que "permite el consentimiento del usuario" o que "requiere el consentimiento del administrador".
- Una aplicación puede comportarse como un cliente (declarando que requiere recursos de tooa de permisos), como un recurso (mediante la declaración de los permisos que expone) o como ambos.

## <a name="controls"></a>Controles

Hola mostramos una lista de controles de administración diferentes Hola disponibles para todos los este comportamiento. Hola, administrador pueden tener acceso a controles en el portal clásico de Hola desde configurar directorio de Hola.

![](media/active-directory-apps-permissions-consent/apps7.png)

Hola Azure portal, en **administrar**, **configuración de usuario**.

![](media/active-directory-apps-permissions-consent/apps11.png)



- Puede controlar si los usuarios pueden consentir tooapps:

En el portal clásico de hello, seleccione **los usuarios pueden permitir aplicaciones permisos tooaccess sus datos.**
![](media/active-directory-apps-permissions-consent/apps8.png)

Hola portal de Azure, seleccione **a los usuarios pueden permitir aplicaciones tooaccess sus datos**.
![](media/active-directory-apps-permissions-consent/apps12.png)



- Puede controlar si los usuarios pueden registrar sus propias aplicaciones LOB único inquilino: en Seleccione portal clásico de hello **los usuarios pueden agregar aplicaciones integradas.**
![](media/active-directory-apps-permissions-consent/apps9.png)

Hola portal de Azure, seleccione **a los usuarios pueden permitir aplicaciones tooaccess sus datos**.
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
>Incluso si permitir a los usuarios de las aplicaciones LOB de tooregister único inquilino, hay límites se pueden registrar toowhat.  
>Por ejemplo, los desarrolladores que no son administradores de directorios.
>
>- Los usuarios no pueden hacer que una aplicación de inquilino único se convierta en una aplicación multiinquilino.
>- Al registrar las aplicaciones LOB único inquilino, los usuarios no pueden solicitar permisos de solo aplicación tooother aplicaciones.
>- Al registrar las aplicaciones LOB único inquilino, los usuarios no pueden solicitar permisos delegados tooother aplicaciones si esos permisos requieren consentimiento del administrador.
>- Los usuarios no pueden realizar cambios tooapps que no son propietarios de.



- Puede controlar si los usuarios pueden por sí mismos agregar aplicaciones previamente integradas que utilizan el inicio de sesión único con contraseña (proceso también conocido como "almacenamiento de contraseña") ![](media/active-directory-apps-permissions-consent/apps10.png)



- Puede controlar en qué condiciones se puede tener acceso a las aplicaciones (es decir, un acceso condicional). Tenga en cuenta que esto aplica toohello aplicación de cliente y de aplicación de recursos de toohello. Por lo tanto, supongamos que establece una directiva de acceso condicional que dice "Office 365 Exchange Online" aplicación Hola solo puede tener acceso desde máquinas, que son compatibles.  Esta directiva también se activa cuando un usuario intenta toouse una aplicación cliente que solicita permisos tooExchange en línea.



- Tener visibilidad en la que las aplicaciones han sido tooand con consentimiento cuáles se utilizan.

1.  Cuando un usuario acepta tooan aplicación, se crea un objeto ServicePrincipal en el inquilino de Hola. Creación de ServicePrincipal se incluye en el informe de auditoría de Hola.
2.  Informes de actividad de inicio de sesión de usuario saber qué usuario Hola de aplicación es iniciar sesión en. 

## <a name="example"></a>Ejemplo

Por ejemplo, echemos aplicación de "FabrikamMail para Office 365" hello, que haya observado los usuarios de su inquilino de sesión en. "FabrikamMail" es una aplicación de lector de correo electrónico para Android, publicada por "Fabrikam, Inc.". Esto entra Hola "aplicaciones de varios inquilinos otros desarrolle, que puede dar el consentimiento Contoso".

Si los usuarios pueden tooconsent, obtienen un Hola solicitar consentimiento primera vez que inicien sesión en:![](media/active-directory-apps-permissions-consent/apps14.png)

"Tener acceso a los buzones de correo" es la cadena de hello orientadas al usuario su consentimiento para permisos de "Acceso a los buzones como usuario con sesión iniciada Hola" hello expuestos por "Office 365 Exchange Online" (es decir, Exchange).

Puede ver los permisos de hello buscando objeto ServicePrincipal de Hola para Exchange (recurso hello), que se agregó al suscribirse a Office 365. Se puede considerar objeto ServicePrincipal de Hola de una "instancia" de la aplicación hello en su inquilino, que se usa para registrar las configuraciones y opciones diferentes.  Puede ver mediante el uso de hello `Get-AzureADServicePrincipal` en PowerShell.

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

Consentimiento se inicia cuando el usuario de Hola, haga clic en "Aceptar". En primer lugar, se crea un objeto ServicePrincipal para "FabrikamMail para Office 365" en inquilinos Hola. Hola ServicePrincipal tiene un aspecto similar al siguiente:

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

Consentimiento tooan aplicación creará un vínculo de Oauth2PermissionGrant entre siguiente hello:
  
- objeto de usuario de Hola
- aplicaciones cliente Hello ServicePrincipalName (SPN)
- aplicaciones de recursos de Hello ServicePrincipalName (SPN)
- permisos de aplicación de recursos de hello.  

En caso de hello de FabrikamMail, parece algo parecido a esto:

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

(**ClientId** es el identificador de objeto de entidad de servicio del FabrikamMail (Hola que simplemente se llegó a crear), **PrincipalId** es el Id. de objeto de usuario de hello (Hola del usuario de que dado su consentimiento), **ResourceId**es servicio de Exchange Id. de objeto principal, el ámbito es el permiso de hello en Exchange que se ha dado su consentimiento para).

Si los usuarios no pueden tooconsent, verá una pantalla que dice ese permiso es necesaria.

