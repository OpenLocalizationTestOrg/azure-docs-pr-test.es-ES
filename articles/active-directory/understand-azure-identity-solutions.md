---
title: aaaUnderstand identidad de Azure | Documentos de Microsoft
description: "Tener un conocimiento básico de los términos de solución de identidad de Microsoft Azure, los conceptos y las recomendaciones para toomake Hola mejor identidad regulación decisión para su organización."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/17/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4d9c90bd7a6bcc9637be3107998f9da5bd4cbdae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-identity-solutions"></a>Información acerca de las soluciones de identidad de Azure
Microsoft Azure Active Directory (Azure AD) es una solución en la nube de administración de identidades y acceso que proporciona servicios de directorio, control de identidad y administración del acceso a las aplicaciones. Azure AD rápidamente [habilita el inicio de sesión único (SSO)](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-sso) too1, 000 preintegradas aplicaciones comerciales y personalizadas en hello [Galería de aplicaciones de Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/). Probablemente ya use muchas de estas aplicaciones, como Office 365, Salesforce.com, Box, ServiceNow y Workday.

Un único directorio de Azure AD se asocia automáticamente con una suscripción de Azure cuando se crea. Como servicio de identidad de hello en Azure, Azure AD, a continuación, proporciona toda la administración de identidad y las funciones de control de acceso para los recursos en la nube. Estos recursos pueden incluir usuarios, aplicaciones y grupos para un inquilino individual (organización), como se muestra en hello siguiente diagrama:

![Azure Active Directory](./media/understand-azure-identity-solutions/azure-ad.png)

Microsoft Azure ofrece varias identidades de tooleverage maneras como un servicio (IDaaS) con diferentes niveles de complejidad toomeet las necesidades de su organización individuales. resto de Hola de este artículo le ayudará a comprender la terminología básica de identidad de Azure y conceptos, así como recomendaciones para toomake Hola mejor elección de opciones disponibles de Hola.

## <a name="terms-tooknow"></a>Tooknow de términos

Antes de que puede decidir cuál será una solución de identidad de Azure para su organización, necesita un conocimiento básico de los términos de hello comúnmente usados al hablar sobre los servicios de identidad de Azure.

|Término tooknow| Descripción|
|-----|-----|
|Suscripción de Azure |Las suscripciones son toopay usado para los servicios de nube de Azure y tarjeta de crédito tooa normalmente vinculado. Puede tener varias suscripciones, pero puede ser difícil tooshare recursos entre suscripciones.|
|Inquilino de Azure | Un inquilino de Azure AD es representativo de una sola organización. Es una instancia dedicada y de confianza de Azure AD que se crear automáticamente cuando una organización se suscribe a un servicio en la nube, como Azure, Intune u Office 365. Los inquilinos pueden obtener acceso a tooservices en un entorno dedicado (un solo inquilino) o en un entorno compartido con otras organizaciones (multiempresa).|
|Directorio de Azure AD | Cada inquilino de Azure tiene un Azure dedicado, confianza directorio de AD que contiene usuarios del inquilino de hello, grupos y aplicaciones. Es funciones de administración de identidades y accesos tooperform usado para recursos de inquilinos. Dado que un único directorio de Azure AD es toorepresent aprovisionado automáticamente su organización al suscribirse a un servicio de nube de Microsoft como Office 365, Microsoft Intune o Azure, a veces, verá los términos de hello *inquilino*, *Azure AD*, y *directorio de Azure AD* usar indistintamente. |
|Dominio personalizado | La primera vez que se suscribe a un servicio en la nube de Microsoft, el inquilino (organización) usa un nombre de dominio *.onmicrosoft.com*. Sin embargo, la mayoría de las organizaciones tener uno o más nombres de dominio que son utilizados toodo business y que los usuarios finales utilizar recursos de la empresa tooaccess. Puede agregar su tooAzure de nombre de dominio personalizado AD para que hello nombre de dominio es usuarios tooyour familiarizado, como  *alice@contoso.com*  en lugar de  *alice@contoso.onmicrosoft.com* . |
|Cuenta de Azure AD | Se trata de identidades que se crean mediante Azure AD u otro servicio en la nube de Microsoft como Office 365. Se almacenan en Azure AD y accesible tooany de las suscripciones de servicio de nube de la organización de Hola. |
|Administrador de suscripciones de Azure| Administrador de la cuenta de Hello es Hola quien inscrito o había comprado Hola suscripción de Azure. Puede usar hello [centro de cuentas de](https://account.windowsazure.com/Home/Index) tooperform diversas tareas de administración, como crear suscripciones, cancelar suscripciones o cambiar la facturación de Hola para una suscripción o cambiar Hola Administrador de servicios. |
|Administrador global de Azure AD | Los administradores globales de Azure AD tienen funciones administrativas de acceso completo tooall Azure AD. Hola quien se suscribe a una suscripción de servicio de nube de Microsoft automáticamente se convierte en un administrador global de forma predeterminada. Puede tener más de un administrador global, pero solo los administradores globales pueden asignar cualquiera de [Hola otros roles de administrador](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) toousers. |
|Cuenta Microsoft | Cuentas de Microsoft (creadas por el usuario para su uso personal) proporcionan acceso orientados a tooconsumer productos de Microsoft y servicios de nube, como Outlook (Hotmail), OneDrive, Xbox LIVE u Office 365. Estas identidades se crean y almacenan en hello sistema de cuentas de Microsoft consumidor identidad ejecutado por Microsoft.|
|Cuentas profesionales o educativas | Cuentas profesionales o educativas (emitidas por un administrador para su uso empresarial/academic) proporcionan acceso a servicios de nube de Microsoft de tooenterprise nivel de negocio, como Office 365, Intune o Azure.|


## <a name="concepts-toounderstand"></a>Conceptos toounderstand

Ahora que sabe los términos de la identidad de Azure básico de hello, debe obtener más información acerca de estos conceptos de identidad de Azure que le ayudarán a tomar una decisión de servicio de identidad de Azure informada.

|Concepto toounderstand |Descripción|
|-----|-----|
|[Asociación de las suscripciones de Azure con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) |Cada suscripción a Azure tiene una relación de confianza con un Azure usuarios de tooauthenticate de directorio de AD, servicios y dispositivos. *Varias suscripciones pueden confiar directory Hola mismo AD de Azure, pero una suscripción solo confiarán en un único directorio de Azure AD*. Esta relación de confianza es distinto de la relación de Hola que tiene una suscripción con otros recursos de Azure (sitios Web, bases de datos etc.), que son más parecidos a los recursos secundarios de una suscripción. Si una suscripción expira, a continuación, tooresources de acceso asociados a la suscripción, Hola excepto AD de Azure también se detiene. Sin embargo, directorio de hello Azure AD permanece en Azure, para que pueda asociar otra suscripción a ese directorio y continuar toomanage recursos del inquilino.|
|[Cómo funcionan las licencias de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-get-started-azure-portal) | Al comprar o activar Enterprise Mobility Suite, Azure AD Premium o Azure AD Basic, el directorio se actualiza con la suscripción de hello, incluida su período de validez y licencias de prepago. Una vez Hola suscripción esté activa, servicio de hello puede administrarse por los administradores globales de Azure AD y utilizado por los usuarios con licencia. Información de su suscripción, incluido el número de Hola de licencias asignadas o disponibles, está disponible en el portal de Azure de Hola Hola **Azure Active Directory** > **licencias** hoja. También esto se Hola a mejor toomanage lugar las asignaciones de licencia.|
|[Control de acceso basado en roles en hello portal de Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)|El control de acceso basado en roles (RBAC) de Azure ayuda a proporcionar una administración de acceso detallada de los recursos de Azure. Pueden exponer y cuenta tooattackers demasiados permisos. Si se conceden muy pocos, los empleados no podrán realizar su trabajo de manera eficaz. Utilizando RBAC, también puede asignar empleados Hola permisos exactos que necesitan en función de tres funciones básicas que se aplican los grupos de recursos de tooall: propietario, Colaborador, lector. También puede crear hasta too2, 000 de su propio [roles personalizados de RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) toomeet sus necesidades específicas. |
|[Identidad híbrida](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)|La identidad híbrida se consigue mediante la integración de su Windows Server Active Directory (AD DS) local con directorio de Azure AD mediante [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Esto le permite tooprovide una identidad común para los usuarios de Office 365, Azure y aplicaciones locales o aplicaciones de SaaS integrada con Azure AD. Con identidad híbrida, ampliar de forma eficaz local en la nube entorno toohello de identidad y acceso.|

### <a name="hello-difference-between-windows-server-ad-ds-and-azure-ad"></a>diferencia de Hello entre Windows Server AD DS y Azure AD
Azure Active Directory (Azure AD) y Active Directory local (Active Directory Domain Services o AD DS) son los sistemas que almacenan datos de directorios y administran la comunicación entre los usuarios y los recursos, incluidos los procesos de inicio de sesión de usuario, la autenticación y las búsquedas de directorios.

Si ya está familiarizado con local Windows Server Active Directory dominio Services (AD DS), primero se introdujo con Windows 2000 Server, a continuación, es probable que comprenda concepto básico de Hola de un servicio de identidad. Sin embargo, también es importante toounderstand que Azure AD no es un controlador de dominio en la nube de Hola. Es una forma totalmente nueva de proporcionar identidad como un servicio (IDaaS) en Azure que requiere una forma totalmente nueva de capacidades en la nube de pensar toofully adoptar y proteger su organización frente a amenazas modernas. 

AD DS es un rol del servidor en Windows Server, lo que significa que se pueden implementar en máquinas físicas o virtuales. Tiene una estructura jerárquica basada en X.500. Utiliza DNS para localizar objetos, se puede interactuar usando LDAP y principalmente usa Kerberos para la autenticación. Active Directory habilita las unidades organizativas (OU) y objetos de directiva de grupo (GPO) también se crean toojoining máquinas toohello confianzas de dominio y entre dominios.

Los departamentos de TI han protegido el perímetro de seguridad durante años con AD DS, pero las empresas modernas, sin perímetro definido y con necesidades de identidad para empleados, clientes y asociados requieren un plano de control nuevo. Azure AD es ese plano de control de identidad. Seguridad se ha movido más allá de hello firewall corporativo toohello en la nube en Azure AD protege recursos de empresa y acceso al proporcionar una identidad común para los usuarios (de forma local o en la nube de hello). Esto proporciona el toosecurely de flexibilidad de Hola a los usuarios acceso Hola aplicaciones necesiten tooget su trabajo desde casi cualquier dispositivo. Controles de protección de datos en forma transparente en función del riesgo, respaldados por las capacidades de aprendizaje automático e informes detallados, también se proporcionan dicha compañía de tookeep de necesidades de TI datos seguros.

Azure AD es un servicio de directorio público de varios clientes, lo que significa que en Azure AD puede crear un inquilino para los servidores de la nube y aplicaciones como Office 365. Los usuarios y los grupos se crean en una estructura plana sin unidades organizativas ni objetos de directiva de grupo. La autenticación se realiza mediante protocolos como SAML, WS-Federation y OAuth. Es posible tooquery Azure AD, pero en lugar de usar LDAP debe usar una API de REST denominada API Graph de AD. Todos funcionan mediante HTTP y HTTPS.

### <a name="extend-office-365-management-and-security-capabilities"></a>Ampliar las funcionalidades de seguridad y administración de Office 365
¿Ya usa Office 365? Puede acelerar la transformación digital mediante la extensión de las capacidades integradas de Office 365 con Azure AD toosecure todos los recursos, tiempo la productividad segura para los trabajadores todo. Cuando se usa Azure AD, además capacidades tooOffice 365, puede proteger su cartera de toda la aplicación con una identidad que habilita un inicio de sesión único para todas las aplicaciones. Puede expandir las funcionalidades de acceso condicional en función no solo del estado del dispositivo, sino también del usuario, la ubicación, la aplicación y el riesgo. Las funcionalidades de autenticación multifactor (MFA) proporcionan aún mayor protección cuando lo necesite. Podrá obtener una supervisión adicional de los privilegios de los usuarios y proporcionar acceso administrativo bajo petición, en el momento preciso. Los usuarios sean más productivos y crear menos vales del departamento de soporte técnico, proporciona capacidades de autoservicio de gracias toohello Azure AD como restablecer contraseñas olvidadas, las solicitudes de acceso de aplicación y la creación y administración de grupos.

> [!TIP]
> ¿Desea toolearn más acerca del uso de identity management de Azure AD con Office 365? [Obtener el libro electrónico hello](https://info.microsoft.com/Extend-Office-365-security-with-EMS.html).

## <a name="microsoft-azure-identity-solutions"></a>Soluciones de identidad de Microsoft Azure

Microsoft Azure ofrece toomanage de varias maneras las identidades de los usuarios si se mantienen completamente de forma local, solo en hello en la nube, o incluso en algún lugar en medio. Estas opciones incluyen: AD DS de implementación personal en Azure, Azure Active Directory (Azure AD), identidad híbrida y Azure AD Domain Services.

### <a name="do-it-yourself-diy-ad-ds"></a>AD DS de implementación personal
Para las empresas que necesitan sólo una pequeña superficie en la nube de hello, **personal (DIY) AD DS** en Azure puede utilizarse. Esta opción admite muchos escenarios de Windows Server AD DS que son adecuados para la implementación como máquinas virtuales (VM) en Azure. Por ejemplo, puede crear una máquina virtual de Azure como un controlador de dominio en un centro de datos lejana que está conectado toohello red remota. Desde allí, Hola VM podría ser capaz de toosupport las solicitudes de autenticación de los usuarios remotos y mejorar el rendimiento de la autenticación. Esta opción también resulta muy indicada como un sitios de recuperación ante desastres costosas de sustituto de costo relativamente bajo toootherwise al alojar un pequeño número de controladores de dominio y una única red virtual en Azure. Por último, tal vez necesite toodeploy una aplicación en Azure, como SharePoint, que requiere Windows Server AD DS, pero no tiene ninguna dependencia en la red local de Hola u Hola Windows Server Active Directory corporativo. En este caso, podría implementar un bosque aislado en los requisitos del entorno de Azure toomeet Hola SharePoint server. También admitió toodeploy aplicaciones de red que requieren la red local de conectividad toohello y Hola Active Directory local.

### <a name="azure-active-directory-azure-ad"></a>Azure Active Directory (Azure AD)
**Azure AD independiente** es una solución de identidad y administración de acceso como servicio (IDaaS) basada completamente en la nube. Azure AD ofrece un potente conjunto de capacidades toomanage usuarios y grupos. Ayuda a proteger el acceso local tooon y aplicaciones, incluidos los servicios web de Microsoft como Office 365 y muchos software de terceros como aplicaciones de servicio (SaaS) en la nube. Azure AD está disponible en tres ediciones: Gratis, Básico y Premium. Azure AD aumenta la eficacia de su organización y amplía la seguridad más allá de hello perimetral firewall tooa control plano nuevo estén protegido por el aprendizaje automático de Azure y otra características de seguridad avanzadas.

### <a name="hybrid-identity"></a>Identidad híbrida
En lugar de elegir entre soluciones de identidad basado en la nube o local, muchos CIO de pensar avance y empresas, que han comenzado anticipación de la dirección a largo plazo de su empresa, están ampliando sus local en la nube toohello directorios a través de **identidad híbrida** soluciones. Con identidad híbrida, obtendrá una identidad realmente global y solución de administración de acceso que proporciona un acceso seguro y productiva a los usuarios de aplicaciones de toohello necesita toodo sus trabajos.

> [!TIP]
> toolearn Obtenga más información sobre cómo CIO realizados a Azure Active Directory una pieza fundamental de sus estrategias de TI, descargar hello [tooAzure de guía de CIO Active Directory](https://aka.ms/AzureADCIOGuide).

### <a name="azure-ad-domain-services"></a>Azure AD Domain Services
**Servicios de dominio de Azure AD** proporciona un toouse opción basada en la nube AD DS para el control de configuración de máquina virtual de Azure ligero y una toomeet de manera requisitos de identidad local para desarrollo de aplicaciones de red y las pruebas. Servicios de dominio de Azure AD no es toolift y desplazar local tooAzure de infraestructura de AD DS máquinas virtuales administrados por los servicios de dominio de AD de Azure. En su lugar, debe ser Hola máquinas virtuales de Azure en dominios administrados toosupport usado Hola desarrollar, probar y el movimiento de las aplicaciones locales que requieren la nube de toohello de métodos de autenticación de AD DS.

## <a name="common-scenarios-and-recommendations"></a>Escenarios comunes y recomendaciones

Estas son algunos escenarios comunes de identidades y accesos con recomendaciones tal como toowhich opción identidad Azure podría ser más adecuado para cada uno.

|Escenario de identidad| Recomendación|
|-----|-----|
|Mi organización ha realizado grandes inversiones en local de Windows Server Active Directory, pero es deseable en la nube tooextend identidad toohello.| solución de identidad de Azure de Hola que más se usan es [identidad híbrida](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Si ya ha realizado las inversiones en local AD DS, puede ampliar fácilmente en la nube identidad toohello mediante Azure AD Connect.|
|Mi empresa ha surgido en la nube de Hola y no tenemos ninguna inversión en soluciones de identidad local.| [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) es mejor opción de hello para empresas, solo en la nube de n las inversiones locales.|
|Necesito ligera Azure VM control toomeet local identidad requisitos de configuración y para el desarrollo de aplicaciones y las pruebas.|[Servicios de dominio de Azure AD](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) es una buena elección si necesita toouse AD DS para control de configuración de máquina virtual de Azure ligero o se encuentre toodevelop o migrar de nube de toohello aplicaciones heredadas, tenga en cuenta el directorio local.|  
|Necesito toosupport unas pocas máquinas virtuales en Azure, pero todavía requisitos se dedica a mi empresa local de Active Directory (AD DS).|Use [ADDS guía](https://msdn.microsoft.com/library/azure/jj156090.aspx) toouse máquinas virtuales de Azure cuando necesite toosupport unas pocas máquinas virtuales y tienen grandes inversiones en AD DS en local. |

## <a name="where-can-i-learn-more"></a>¿Dónde puedo obtener más información?
Tenemos una gran cantidad de recursos excelentes toohelp online que Infórmese acerca de Azure AD. Aquí es una lista de tooget grandes artículos que se inició:

* [Habilitación del directorio para la administración híbrida con Azure AD Connect](active-directory-aadconnect.md)
* [Seguridad adicional en un mundo conectado permanentemente](../multi-factor-authentication/multi-factor-authentication.md)
* [Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones con Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Introducción a los informes de Azure AD](active-directory-reporting-getting-started.md)
* [Administración de contraseñas desde cualquier lugar](active-directory-passwords.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Automatizar el aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones con Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Cómo tooprovide el acceso remoto a aplicaciones locales de tooon](active-directory-application-proxy-get-started.md)
* [Administrar acceso tooresources con grupos de Active Directory de Azure](active-directory-manage-groups.md)
* [¿Qué es la licencia de Microsoft Azure Active Directory?](active-directory-licensing-what-is.md)
* [¿Cómo puedo detectar aplicaciones en la nube no sancionadas que se usan dentro de mi organización?](active-directory-cloudappdiscovery-whatis.md)

## <a name="next-steps"></a>Pasos siguientes

Ahora que comprende los conceptos de identidad de Azure y tooyou de hello opciones disponibles, puede usar Hola después de que ha elegido por la opción de hello implementación de recursos tooget iniciado:

[Más información sobre las soluciones de identidad híbridas de Azure](https://docs.microsoft.com/azure/active-directory/choose-hybrid-identity-solution)

[Información sobre el entorno de prueba de concepto de Azure](https://aka.ms/aad-poc)

[Implementación de Azure AD en producción](https://aka.ms/aad-onboard)
