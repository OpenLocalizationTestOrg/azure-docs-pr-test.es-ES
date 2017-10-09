---
title: "Guía de implementación de Active Directory PoC aaaAzure | Documentos de Microsoft"
description: "Exploración e implementación rápida de escenarios de administración de identidades y acceso"
services: active-directory
keywords: "azure active directory, guía, Prueba de concepto, POC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 4d61f1432d5f1c15cd88fda4824cf1c1de64c712
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-implementation"></a>Guía Prueba de concepto de Azure Active Directory: Implementación | Microsoft Docs

## <a name="foundation---syncing-ad-tooazure-ad"></a>Foundation: sincronizar AD tooAzure AD 

Una identidad híbrida es foundation hello para la mayoría de los clientes de empresa de Hola que ya tienen un directorio local. Hello objetivo es toointentionally emplear como menos tiempo aquí como valor de Hola tooshow posibles escenarios de identidades y accesos de real Hola. 

| Escenario | Bloques de creación| 
| --- | --- |  
| [Extender el entorno local en la nube toohello identidad](#extending-your-on-premises-identity-to-the-cloud) | [Sincronización de directorios: sincronización de hash de contraseñas](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**Nota**: Si ya dispone de DirSync/ADSync o versiones anteriores de Azure AD Connect, este paso es opcional. Puede que algunos escenarios de esta guía requieran una versión más reciente de Azure AD Connect.  <br/>[Personalización de marca](active-directory-playbook-building-blocks.md#branding) | 
| [Asignación de licencias de Azure AD mediante grupos](#assigning-azure-ad-licenses-using-groups) | [Licencias basadas en grupos](active-directory-playbook-building-blocks.md#group-based-licensing) |


### <a name="extending-your-on-premises-identity-toohello-cloud"></a>Extender el entorno local en la nube toohello identidad 

1. Bob es administrador de Active Directory de hello en Contoso. Obtiene la identidad de tooenable de requisito de Hola como un servicio para un conjunto de usuarios. Después de la ejecución del Asistente de Azure AD Connect, identidad Hola Hola de usuarios de destino disponibles en la nube de Hola. 
2. Bob pide a Susana, uno de los usuarios de destino de hello, tooaccess Hola panel de acceso de Azure Active Directory y confirme que ella pueda autenticarse. Susie ve una página de inicio de sesión con la marca y un panel de acceso vacío que está preparado para habilitar el acceso futuro a la aplicación.

### <a name="assigning-azure-ad-licenses-using-groups"></a>Asignación de licencias de Azure AD mediante grupos 

1. Bob es hello administrador Global de Azure AD y desea tooallocate Azure AD licencias tooa conjunto específico de usuarios como parte de la implementación inicial de Hola de Azure AD.
2. Bob crea un grupo para hello usuarios pilotos. 
3. Bob asigna el grupo de hello licencias toohello
4. Susana, uno de los trabajadores de información de hello, se agrega el grupo de seguridad de toohello como parte de sus funciones de trabajo
5. Más tarde, Susana tiene licencia de acceso toohello Azure AD premium. Esto le permitirá más escenarios de prueba de concepto de hello más adelante.

## <a name="theme---lots-of-apps-one-identity"></a>Tema: muchas aplicaciones y una sola identidad

| Escenario | Bloques de creación| 
| --- | --- |  
| [Integración de aplicaciones SaaS: SSO federado](#integrate-saas-applications---federated-sso) | [Configuración de SSO federado en SaaS](active-directory-playbook-building-blocks.md#saas-federated-sso-configuration) <br/>[Grupos: propiedad delegada](active-directory-playbook-building-blocks.md#groups---delegated-ownership) |
| [Integración de aplicaciones SaaS: SSO con contraseña](#integrate-saas-applications---password-sso) | [Configuración de SSO con contraseña en SaaS](active-directory-playbook-building-blocks.md#saas-password-sso-configuration) |
| [Eventos de ciclo de vida de identidad y SSO](#sso-and-identity-lifecycle-events) | [Ciclo de vida de identidad y SaaS](active-directory-playbook-building-blocks.md#saas-and-identity-lifecycle) |
| [Proteger las cuentas de acceso tooShared](#secure-access-to-shared-accounts) | [Configuración de cuentas compartidas de SaaS](active-directory-playbook-building-blocks.md#saas-shared-accounts-configuration) |
| [Proteger las aplicaciones locales de tooOn de acceso remoto](#secure-remote-access-to-on-premises-applications) | [Configuración de proxy de aplicación](active-directory-playbook-building-blocks.md#app-proxy-configuration) |
| [Sincronizar identidades LDAP tooAzure AD](#synchronize-ldap-identities-to-azure-ad) |  [Configuración genérica del conector LDAP](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration) |

### <a name="integrate-saas-applications---federated-sso"></a>Integración de aplicaciones SaaS: SSO federado 

1. Bob es hello administrador Global de Azure AD y recibe una solicitud de hello Marketing departamento tooenable acceso tootheir instancia de ServiceNow. Bob busca tutorial paso a paso de hello en la documentación de Azure AD y lo sigue, y delegados Hola asignación de usuarios toohello aplicación tooKevin, head de hello del equipo de Marketing. 
2. Kevin inicia sesión como propietario de Hola de derechos de ServiceNow y asigna a Susana toohello aplicación. Kevin advierte también que el perfil de Susie se ha creado automáticamente en ServiceNow.
3. Susana es un trabajador de la información en el departamento de Marketing de Hola. Registra en tooazure AD y busca todas las aplicaciones SaaS que está asignada tooin mis aplicaciones portal. Desde allí, sin problemas obtiene acceso tooServiceNow.
4. departamento de Marketing de Hello desea tooaudit que han accedido a ServiceNow. Bob descarga un informe de actividad y lo comparte con Kevin por correo electrónico.  

### <a name="sso-and-identity-lifecycle-events"></a>Eventos de ciclo de vida de identidad y SSO

1. Susana toma una baja de ausencia y por la directiva corporativa Hola local cuenta AD está deshabilitada temporal. Susana ahora no se puede iniciar sesión en tooAzure AD y, por tanto, no puede acceder a ServiceNow. 
2. Susana efectúa un movimiento lateral de Marketing tooSales. Kevin quia su acceso de ServiceNow. Susana inicia sesión en mis aplicaciones de azure ad de Hola y ya no se ve Hola mosaico de ServiceNow. Diez minutos después, Kevin confirma que la cuenta de Susie se ha deshabilitado en la consola de administración de ServiceNow.

### <a name="integrate-saas-applications---password-sso"></a>Integración de aplicaciones SaaS: SSO con contraseña

1. Bob configura acceso tooAtlassian HipChat. HipChat tiene tooSusie de SSO de contraseña integración y conceder acceso
2. Susana inicia sesión en portal mis aplicaciones de toohello y ve un Hola de toodownload extensión del explorador IE de Azure AD, que descarga de vínculo
3. Después de hacer clic en el vínculo, se le piden sus credenciales de nombre de usuario y contraseña de HipChat. Se trata de una operación única y, después de completar tiene acceso tooHipChat
4. Unos días después, Susie abre el portal Mis aplicaciones y hace clic de nuevo en HipChat. En esta ocasión, obtiene acceso sin problemas.
5. Kevin, el propietario de la aplicación de HipChat hello, desea tooaudit quién tiene acceso la aplicación hello. Bob descarga un informe de auditoría y lo comparte con Kevin por correo electrónico. 

### <a name="secure-access-tooshared-accounts"></a>Proteger las cuentas de acceso tooShared 

1. Bob es identificador de Twitter de toosecure de trabajo que pidieron Hola compartido para los miembros del equipo de ventas de Hola. Agrega Twitter como una aplicación de SSO y lo asigna el grupo de seguridad de toohello de Hola, equipo de ventas. Se le asignaron cuenta toohello compartido de credenciales de Hola y le suministra en sistema Hola. 
2. Uso compartido de credenciales de Twitter ya no es de confianza debido a personas toomultiple lo sepa. Bob habilita la sustitución automática de contraseña de Twitter de Hola.
3. Susana, un miembro del equipo de ventas de hello, inicia sesión en el portal de mis aplicaciones toohello y ve un Hola de toodownload vínculo extensión del explorador IE de Azure AD. La instala.
4. Al hacer clic en el obtener acceso directo a tooTwitter. No conoce la contraseña de Hola.
5. Arnold también forma parte del equipo de ventas de Hola. Tiene Hola misma experiencia como Susana en los pasos 3 y 4
6. departamento de ventas de Hello desea tooaudit que han accedido a Twitter. Bob descarga un informe de actividad y lo comparte con Kevin por correo electrónico. 

### <a name="secure-remote-access-tooon-premises-applications"></a>Proteger las aplicaciones locales de tooOn de acceso remoto

1. Bob, hello Azure AD de administrador Global, ha recibido muchas solicitudes tooenable empleados tooaccess varios útil en recursos locales, como aplicación de gastos de hello, mientras se trabaja de forma remota. Este sigue hello [documentación del Proxy de aplicación](active-directory-application-proxy-enable.md) tooinstall un conector y publicar los gastos como una aplicación de Proxy de aplicación. 
2. Bob comparte la dirección URL de la aplicación externa de gastos de hello con Susana, uno de los empleados de Hola que necesiten acceso remoto. Vuelve a acceder vínculo hello, y tras la autenticación con AAD, es capaz de tooaccess Hola gastos aplicación continuar toobe productivo al remoto. 
3. Bob, a continuación, continúa con las aplicaciones locales adicionales toopublish Hola mismo proceso y lo que proporciona acceso toousers según sea necesario. Agrega acceso condicional y la autenticación multifactor para hello aplicaciones más confidenciales que publica, tooensure de seguridad adicional.

### <a name="synchronize-ldap-identities-tooazure-ad"></a>Sincronizar identidades LDAP tooAzure AD

1. La compañía de Bob tiene una infraestructura de identidades compleja. La mayoría de los usuarios de Hola se mantiene dentro de Windows Server Active Directory dominio servicios (ADDS). Algunos de ellos se administran en el sistema RR. HH que se encuentra en Active Directory Lightweight Directory Services (ADLDS).
2. Bob se encarga habilitar aplicaciones de tooSaaS de acceso para todos los usuarios (también estos no están presentes en ADDS).
3. Juan configura los datos de toopull de conector LDAP genérico de ADLDS en Azure AD Connect.
4. Bob crea reglas de sincronización para que los usuarios LDAP se rellenan en el metaverso y tooAzure AD
5. Susie, como usuario de LDAP, acede a su aplicación SaaS con identidad sincronizada.



> [!IMPORTANT] 
> Se trata de una configuración avanzada que requiere cierta familiaridad con FIM o MIM. Si se usa en producción, se recomienda plantear las preguntas sobre esta configuración a través de [soporte técnico Premier](https://support.microsoft.com/premier).



## <a name="theme---increase-your-security"></a>Tema: aumento de la seguridad 

| Escenario | Bloques de creación| 
| --- | --- |  
| [Acceso seguro a la cuenta de administrador](#secure-administrator-account-access) | [Azure MFA con llamadas telefónicas](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [Acceso seguro a aplicaciones](#secure-access-to-applications) | [Acceso condicional para aplicaciones SaaS](active-directory-playbook-building-blocks.md#mfa-conditional-access-for-saas-applications) |
| [Habilitar administración Just-In-Time (JIT)](#enable-just-in-time-jit-administration) | [Privileged Identity Management](active-directory-playbook-building-blocks.md#privileged-identity-management-pim) |
| [Protección de identidades basadas en riesgo](#protect-identities-based-on-risk) | [Detección de eventos de riesgo](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[Implementación de directivas de riesgo de inicio de sesión](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [Autenticación sin contraseñas mediante autenticación basada en certificados](#authenticate-without-passwords-using-certificate-based-authentication) | [Configuración de autenticación basada en certificados](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### <a name="secure-administrator-account-access"></a>Acceso seguro a la cuenta de administrador

1. Bob es hello administrador Global de Azure AD. Ha identificado a Stuart como Coadministrador del servicio de Hola. 
2. Bob configura la cuenta de Stuart tooalways requieren la postura de seguridad MFA tooimprove Hola
3. Stuart registra en toohello portal de Azure y avisos que debe tooregister su inicio de sesión de Hola de toocontinue número de teléfono
4. Inicios de sesión posteriores de Stuart ahora están protegidos con la autenticación multifactor y ahora obtiene una llamada de teléfono tooverify su identidad.

### <a name="secure-access-tooapplications"></a>Acceso seguro tooapplications

1. Kevin es propietario de la empresa de Hola de ServiceNow. compañía de Hello ahora desea esos toologin a los usuarios con MFA al tener acceso a la red corporativa de hello externa.
2. Bob, el administrador Global de Azure AD, agrega un tooenable de la aplicación del ServiceNow acceso condicional directiva toohello MFA para el acceso externo
3. Susana, el trabajador de la información, inicia sesión en Mi portal de aplicaciones y hace clic en el icono de ServiceNow Hola. Ahora tiene que enfrentarse a MFA.

### <a name="enable-just-in-time-jit-administration"></a>Habilitar administración Just-In-Time (JIT)

1. Bob y Stuart son administradores globales de Azure AD. Desean funciones de administración de tooenable JIT acceso toohello y también tookeep registros sobre el uso de Hola de hello con privilegios roles.
2. Bob permite PIM en el inquilino de Azure AD de Hola y se convierte en Administrador de seguridad de Hola. Cambia a sí mismo y pertenencia al rol de administrador global de Stuart desde tooeligible permanente.
3. Roberto y Stuart requieren ahora activa su rol a través del portal de Azure de Hola antes de realizar alguna cambia tooAzure AD configuración. 

### <a name="protect-identities-based-on-risk"></a>Protección de identidades basadas en riesgo 

1. Susie, trabajadora de la información, intenta iniciar sesión en un navegador TOR. 
2. Bob comprueba el panel de hello Azure AD identity protection y ve el inicio de sesión de Susana desde una dirección IP anónima. equipo de seguridad de Hello quiere toochallenge este tipo tiene acceso a los usuarios con MFA
3. Bob habilita la directiva de protección de Azure AD Identity toochallenge MFA para los eventos de riesgo medio o superior
4. Pasado un tiempo, Susie inicia sesión de nuevo desde un navegador Tor. Esta vez, aparece hello desafío MFA

### <a name="authenticate-without-passwords-using-certificate-based-authentication"></a>Autenticación sin contraseñas mediante autenticación basada en certificados

1. Bob es administrador global de una entidad financiera que prohíbe el uso de contraseñas como elemento de autenticación en sus aplicaciones.
2. Bob habilita y exige la autenticación de certificado en ADFS y en Azure AD.
3. Susana mientras obtiene acceso a la aplicación se le pida tooauthenticate mediante certificado

## <a name="theme---scale-with-self-service"></a>Tema: escala con autoservicio

| Escenario | Bloques de creación| 
| --- | --- |  
| [Restablecimiento de contraseñas de autoservicio](#self-service-password-reset) | [Restablecimiento de contraseñas de autoservicio](active-directory-playbook-building-blocks.md#self-service-password-reset) |
| [En sí mismo tooApplications de acceso al servicio](#self-service-access-to-applications) | [En sí mismo tooApplications de acceso al servicio](active-directory-playbook-building-blocks.md#self-service-access-to-application-management) |

### <a name="self-service-password-reset"></a>Restablecimiento de contraseñas de autoservicio 

1. Bob es hello Azure AD Global admin y habilita la administración de contraseñas de servicio de autoservicio tooa subconjunto de usuarios, incluidos a Susana. 
2. Susana registra en toomyapps portal y vea un mensaje tooregister su información de seguridad para eventos de restablecimiento de contraseña futuras.
3. Días después, Susie olvida su contraseña y la restablece a través del portal de Azure AD.

### <a name="self-service-access-tooapplications"></a>En sí mismo tooApplications de acceso al servicio 

1. Kevin es propietario de la empresa de Hola de ServiceNow. Quiere que los usuarios demasiado "suscribirse" a él a petición, en lugar de agregarlos a la vez
2. Bob, el administrador Global de Azure AD, modifica hello ServiceNow aplicación tooenable las solicitudes de autoservicio
3. Susana, el trabajador de la información, inicia sesión en Mi portal de aplicaciones y clics Hola botón "Agregar más aplicaciones" y consideran ServiceNow como uno de hello recomienda las aplicaciones. A continuación, entró navega portal de aplicaciones back-toomy y ver aplicación de hello ServiceNow.

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]