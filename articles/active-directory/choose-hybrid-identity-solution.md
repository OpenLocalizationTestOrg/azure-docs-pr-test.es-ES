---
title: "aaaChoose una solución de identidad híbrida de Azure | Documentos de Microsoft"
description: "Tener un conocimiento básico de soluciones de identidad híbrida disponibles de Hola y recomendaciones para toomake Hola mejor identidad regulación decisión para su organización."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4ab8aff314f6308ab32f77e81cf0f07e1f5d7b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-hybrid-identity-solutions"></a>Soluciones de identidad híbrida de Microsoft
[Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) soluciones de identidad híbrida le permiten toosynchronize objetos de directorio locales con Azure AD mientras todavía administra los usuarios locales. Hola en primer lugar la toma de decisiones toomake al planear toosynchronize su en Windows Server Active Directory local con Azure AD es si desea que toouse sincronizado identidad o identidad federada. Identidades sincronizadas y, opcionalmente, hash de contraseña, permiten a los usuarios toouse Hola mismo tooaccess contraseña locales y recursos de la organización en la nube. Para los requisitos de escenario más avanzados, como inicio de sesión único (SSO) o MFA local, deberá toofederate identidades de toodeploy los servicios de federación de Active Directory (AD FS). 

Hay varias opciones disponibles para configurar la identidad híbrida. Este artículo proporciona toohelp información que elija Hola una mejor para su organización en función de facilidad de implementación y la administración de identidades y accesos específica es necesario. Mientras piensa qué modelo de identidad que mejor se adapte a las necesidades de su organización, debe toothink sobre el tiempo, la infraestructura existente, la complejidad y costo. Estos factores son diferentes para cada organización y pueden cambiar con el tiempo. Sin embargo, si cambian los requisitos, también tiene modelo de identidad diferente de hello flexibilidad tooswitch tooa.

> [!TIP]
> [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) entrega todas estas opciones.

## <a name="synchronized-identity"></a>Identidad sincronizada 
Identidades sincronizadas es toosynchronize de manera más sencilla de hello objetos de directorio (usuarios y grupos) local con Azure AD. 

![Identidad híbrida sincronizada](./media/choose-hybrid-identity-solution/synchronized-identity.png)

Mientras identidad sincronizada es el método más fácil y rápido de hello, los usuarios necesitan todavía toomaintain una contraseña independiente para los recursos en la nube. tooavoid, también puede (opcionalmente) [sincronizar un hash de contraseñas de usuario](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-synchronization#what-is-password-synchronization) directory tooyour Azure AD. Sincronización de contraseña hash permite a los usuarios toolog en toocloud organizativos recursos con Hola mismo nombre de usuario y contraseña que usa en local. Azure AD Connect busca periódicamente en el directorio local los cambios y mantiene sincronizado el directorio Azure AD. Cuando se cambia un atributo de usuario o una contraseña en Active Directory local, se actualiza automáticamente en Azure AD. 

Para la mayoría de las organizaciones que sólo necesita tooenable su toosign de usuarios en tooOffice 365, aplicaciones SaaS y otros recursos basados en AD de Azure, se recomienda opción de sincronización de contraseña de Hola de forma predeterminada. Si esto no funciona para usted, deberá toodecide entre la autenticación de paso a través y AD FS.

> [!TIP]
> Las contraseñas de usuario se almacenan en local Windows Server Active Directory en forma de Hola de un valor de hash que representa la contraseña de usuario real de Hola. Un valor hash es un resultado de una función matemática unívoca (Hola algoritmo hash). No hay ningún método toorevert Hola dar lugar a una versión de texto sin formato toohello función unidireccional de una contraseña. No puede usar un toosign de hash de contraseña de red de tooyour local. Cuando se opta por toosynchronize contraseñas, Azure AD Connect extrae los hash de contraseña de hello Active Directory local y aplica la seguridad adicional procesamiento toohello hash de contraseña antes de que esté sincronizada tooAzure AD. Sincronización de contraseña también puede utilizarse junto con la contraseña tooenable de reescritura de restablecimiento de contraseña en Azure AD. Además, puede habilitar el inicio de sesión único (SSO) para los usuarios de equipos unidos a un dominio que son redes corporativas toohello conectado. Con el inicio de sesión único, los usuarios habilitados bastará tooenter un toosecurely de nombre de usuario acceso a los recursos de nube. 

## <a name="pass-through-authentication"></a>Autenticación de paso a través
La [autenticación de paso a través de Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication) proporciona una sencilla solución de validación de contraseñas para servicios basados en Azure AD mediante su instancia de Active Directory local. Si las directivas de seguridad y cumplimiento para su organización no permite el envío de contraseñas de los usuarios, incluso en un formulario con algoritmo hash y solo necesita toosupport escritorio SSO para dispositivos Unidos a un dominio, se recomienda que evaluarse mediante la autenticación de paso a través. Autenticación de paso a través no requiere ninguna implementación en hello DMZ, lo que simplifica la infraestructura de implementación de hello en comparación con AD FS. Cuando los usuarios inician sesión con Azure AD, este método de autenticación valida las contraseñas de los usuarios directamente en la instancia de Active Directory local.

![Autenticación de paso a través](./media/choose-hybrid-identity-solution/pass-through-authentication.png)

Con la autenticación de paso a través, no es necesario para una infraestructura de red compleja y no es necesario contraseñas locales de toostore en la nube de Hola. Combinar con inicio de sesión único, autenticación de paso proporciona una experiencia realmente integrada cuando inicien sesión en tooAzure AD u otros servicios en la nube.

La autenticación de paso a través se configura mediante Azure AD Connect y utiliza un agente local simple que escucha las solicitudes de validación de contraseña. agente de Hello puede ser fácil de implementar toomultiple máquinas tooprovide alta disponibilidad y equilibrio de carga. Puesto que todas las comunicaciones son salidas solo, no hay ningún requisito para hello conector toobe instalado en una red Perimetral. requisitos del equipo de servidor Hello para el conector de hello son los siguientes:

- Windows Server 2012 R2 o superior
- Se unió al dominio tooa en el bosque de Hola a través del cual se validan los usuarios

> [!NOTE]
> La autenticación de paso a través de Azure AD está actualmente en versión preliminar y es compatible para los clientes basados en explorador web y clientes de Office que admiten la autenticación moderna. Para los clientes que no son compatibles, como heredado clientes de Office y Exchange ActiveSync (incluidos a los clientes de correo electrónico nativo en dispositivos móviles), es toouse recomendada Hola la autenticación moderna equivalente. La autenticación moderna no sólo permite la autenticación de paso a través, sino que también permite toobe de directivas de acceso condicional aplicado, como la autenticación multifactor. 

Autenticación de paso a través no se admite actualmente cuando usen dispositivos Windows 10 Unidos tooAzure AD. Sin embargo, puede utilizar la sincronización de hash de contraseña como un toosupport reserva automática Windows 10 y los clientes heredados de Hola se ha mencionado anteriormente. Durante la vista previa de hello, sincronización de hash de contraseña está habilitada de forma predeterminada cuando se selecciona la autenticación de paso a través como opción de inicio de sesión de hello en Azure AD Connect.


## <a name="federated-identity-ad-fs"></a>Identidad federada (AD FS)
Para tener más control sobre cómo los usuarios acceden a Office 365 y otros servicios en la nube, puede configurar la sincronización de directorios con el inicio de sesión único (SSO) mediante [Servicios de federación de Active Directory (AD FS)](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server-2016). Federación inicios de sesión del usuario con tooan de autenticación de AD FS delegados en servidor local que valida las credenciales del usuario. En este modelo, las credenciales de Active Directory local nunca se pasan tooAzure AD.

![Identidad federada](./media/choose-hybrid-identity-solution/federated-identity.png)

También llamado federación de identidades, este método garantiza que toda la autenticación de usuario está controlada en local y permite a los administradores tooimplement más rigurosos niveles de control de acceso. Federación de identidades con AD FS es opción hello más complicada y requiere la implementación de servidores adicionales en su entorno local. Federación de identidades también confirma tooproviding 24 x 7 compatibilidad con la infraestructura de Active Directory y AD FS. Este alto nivel de compatibilidad es necesario porque si el acceso local de Internet, controlador de dominio o servidores de AD FS no están disponibles, los usuarios no pueden iniciar sesión en servicios de toocloud.

> [!TIP]
> Si decide toouse federación con los servicios de federación de Active Directory (AD FS), si lo desea puede establecer la sincronización de contraseña como una copia de seguridad en caso de que se produce un error en la infraestructura de AD FS.


## <a name="common-scenarios-and-recommendations"></a>Escenarios comunes y recomendaciones
Estos son algunos identidad híbrida común y escenarios de administración de acceso con recomendaciones como opción de identidad híbrida toowhich (u opciones) podrían ser adecuados para cada uno.

|Necesitará:|PWS y SSO<sup>1</sup>| PTA y SSO<sup>2</sup> | AD FS<sup>3</sup>|
|-----|-----|-----|-----|
|Nuevo usuario de sincronización, póngase en contacto con y las cuentas de grupo que se crean automáticamente en la nube de toohello de Active Directory local.|![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png) |![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)|
|Configurar mi inquilino para escenarios híbridos de Office 365|![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png) |![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)|
|Habilitar mi toosign de usuarios en y obtener acceso a servicios en la nube con su contraseña local|![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png) |![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)|
|Implementar el inicio de sesión único utilizando credenciales corporativas|![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)| ![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png) |![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)|
|Asegúrese de que ningún hashes de contraseña se almacenan en la nube de Hola| |![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)|![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)|
|Habilitar soluciones locales de autenticación multifactor| | |![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)|
|Admitir la autenticación de tarjeta inteligente para mis usuarios<sup>4</sup>| | |![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)|
|Mostrar notificaciones de expiración de contraseña en hello Portal de Office y en el escritorio de Windows 10 Hola| | |![Recomendado](./media/choose-hybrid-identity-solution/ic195031.png)|

> <sup>1</sup> Sincronización de contraseñas con inicio de sesión único. 

> <sup>2</sup> Autenticación de paso a través e inicio de sesión único. 

> <sup>3</sup> Inicio de sesión único federado con AD FS.

> <sup>4</sup> AD FS se puede integrar con su tooallow PKI de empresa mediante certificados de inicio de sesión. Estos certificados pueden ser certificados flexibles implementados a través de canales de aprovisionamiento de confianza, como certificados MDM o GPO o de tarjetas inteligentes (incluidas las tarjetas PIV/CAC) o Hello para empresas (cert-trust). Para más información sobre la compatibilidad con la autenticación de tarjetas inteligentes, consulte [este blog](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/).


## <a name="next-steps"></a>Pasos siguientes
[Información sobre el entorno de prueba de concepto de Azure](https://aka.ms/aad-poc)

[Instalación de Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)

[Supervisión de 'sincronización de identidades híbridas](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)

