---
title: "¿aaaWhat es el acceso a la aplicación y el inicio de sesión único con Azure Active Directory? | Microsoft Docs"
description: "Usar Azure Active Directory tooenable único inicio de sesión tooall de hello SaaS y las aplicaciones web que necesita para la empresa."
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 75d1a3fd-b3c5-4495-a5c8-c4c24145ff00
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curyand
ms.openlocfilehash: 429522cbd570ab27359c4630c5a6d7b25b692ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-access-and-single-sign-on-with-azure-active-directory"></a>¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?
Inicio de sesión único significa ser capaz de tooaccess todas las aplicaciones de Hola y recursos que necesita toodo business, debe iniciar sesión en una sola vez usando una cuenta de usuario único. Una vez iniciado sesión, puede tener acceso a todas las aplicaciones de hello necesaria sin que se va a tooauthenticate necesaria de (por ejemplo, escriba una contraseña) una segunda vez.

Muchas organizaciones confían en el modelo de software como servicio (SaaS), como Office 365, Box y Salesforce para la productividad del usuario final. Históricamente, el personal de TI necesita tooindividually crear y actualizar cuentas de usuario en cada aplicación SaaS, y los usuarios tienen tooremember una contraseña para cada aplicación SaaS.

Azure Active Directory extiende en local de Active Directory en nube de hello, lo que permite a los usuarios toouse su cuenta organizativa principal toonot solo inicio de sesión tootheir dispositivos Unidos a dominio y recursos de la empresa, sino también todas las aplicaciones de SaaS y web de Hola se necesita para realizar su trabajo.

Por lo que no solo a los usuarios no tiene toomanage varios conjuntos de nombres de usuario y contraseñas, sus aplicaciones de access puede aprovisionar automáticamente o se anula su aprovisionamiento basado en sus miembros de grupo de organización y también su estado como un empleados. Azure Active Directory se introducen seguridad y los controles de regulación de acceso que permiten toocentrally administran el acceso de los usuarios en todas las aplicaciones de SaaS.

Azure AD ofrece una integración fácil toomany de aplicaciones de SaaS populares de hoy en día; proporciona administración de identidades y acceso y permite a los usuarios toosingle inicio de sesión tooapplications directamente, o detectar e iniciarlos desde un portal como Office 365 o hello panel de acceso de Azure AD.

arquitectura de Hola de integración de hello consta de hello siguientes cuatro bloques principales:

* Inicio de sesión único permite a los usuarios tooaccess sus aplicaciones SaaS basándose en su cuenta profesional en Azure AD. Inicio de sesión único es lo que permite a los usuarios tooauthenticate tooan aplicación con su cuenta organizativa única.
* El aprovisionamiento de usuarios permite el aprovisionamiento y el desaprovisionamiento de usuarios en el SaaS de destino basándose en los cambios realizados en Windows Server Active Directory y Azure AD. Una cuenta aprovisionada es lo que permite un toouse toobe autorizada de usuario una aplicación, después de que han autenticado a través de un inicio de sesión único.
* Administración de acceso de aplicaciones centralizada en hello Portal de administración de Azure permite el acceso de aplicación de punto único de SaaS y administración, con hello capacidad toodelegate aplicación acceso decisión de decisiones y aprobaciones tooanyone de organización de Hola
* Creación de informes y supervisión unificada en Azure AD

## <a name="how-does-single-sign-on-with-azure-active-directory-work"></a>¿Cómo funciona el inicio de sesión único con Azure Active Directory?
Cuando una aplicación de tooan "inicia sesión" de usuario, se van a través de un proceso de autenticación que son necesario tooprove que realmente son quienes dicen ser. Sin inicio de sesión único, esto suele hacerse escribiendo una contraseña que se almacena en la aplicación hello y usuario de hello es necesario tooknow esta contraseña.

Azure AD admite tres toosign de distintas maneras en tooapplications:

* **El inicio de sesión único federado** habilita aplicaciones tooredirect tooAzure AD para la autenticación de usuario en lugar de solicitar su propia contraseña. Esto es para las aplicaciones que admite compatibilidad con protocolos como SAML 2.0, WS-Federation u OpenID Connect y es el modo de numerosas Hola de inicio de sesión único.
* **Inicio de sesión único con contraseña** , que permite el almacenamiento seguro de contraseñas de las aplicaciones y reproducirlo usando una extensión de explorador web o aplicación móvil. Aprovecha Hola inicio de sesión en proceso existente proporcionada por la aplicación hello, pero permite que una contraseñas de administrador toomanage hello y no requiere Hola usuario tooknow Hola contraseña.
* **Un inicio de sesión único existente** habilita Azure AD tooleverage cualquier existente inicio de sesión único que se ha configurado para la aplicación hello, pero permite que estas aplicaciones toobe vinculado toohello Office 365 o portales de panel de acceso de Azure AD y que permite creación de informes adicionales en Azure AD cuando se inician las aplicaciones de hello no existe.

Una vez que un usuario se han autenticado con una aplicación, también debe toohave un registro de cuenta que se proporciona en la aplicación hello que indica la aplicación hello donde hay permisos y nivel de acceso que se encuentren dentro de la aplicación hello. Hola de aprovisionamiento de este registro de cuenta puede hallarse automáticamente, o puede ocurrir manualmente por un administrador antes de que el usuario de Hola se proporciona acceso de inicio de sesión único.

 A continuación se ofrecen más detalles sobre estos modos de inicio de sesión único y sobre el aprovisionamiento.

### <a name="federated-single-sign-on"></a>Inicio de sesión único federado
Un inicio de sesión único federado permite a los usuarios de hello habilita el inicio de sesión en su toobe organización sesión automáticamente en la aplicación de SaaS de terceros tooa mediante Azure AD utilizando la información de cuenta de usuario de Hola de Azure AD.

En este escenario, si ya ha iniciado en Azure AD, y usted desea tooaccess recursos controlados por una aplicación SaaS de terceros, federación elimina necesidad de Hola de un toobe de usuario vuelve a ser autenticado.

Azure AD puede admitir federado inicio de sesión único con las aplicaciones que admiten Hola SAML 2.0, WS-Federation u OpenID connect protocolos.

Consulte también: [Administración de certificados para inicio de sesión único federado](active-directory-sso-certs.md)

### <a name="password-based-single-sign-on"></a>Inicio de sesión único con contraseña
Configuración basada en contraseña de inicio de sesión único permite a los usuarios de hello en su toobe organización sesión automáticamente en la aplicación de SaaS de terceros tooa mediante Azure AD utilizando la información de cuenta de usuario de Hola de aplicación de SaaS de terceros de Hola. Cuando se habilita esta característica, Azure AD recopila y almacena de forma segura la información de cuenta de usuario de Hola y contraseña correspondiente de Hola.

Azure AD admite el inicio de sesión único con contraseña para cualquier aplicación basada en la nube cuya página de inicio de sesión esté basada en HTML. Mediante el uso de un complemento de explorador personalizado, AAD automatiza el inicio de sesión del usuario de hello en proceso a través de recuperación de forma segura las credenciales de la aplicación como nombre de usuario de Hola y la contraseña de hello del directorio de Hola e inserta estas credenciales en la página de conexión de la aplicación hello nombre de usuario de Hola. Hay dos posibles casos de uso:

1. **Administrador administra las credenciales** : los administradores pueden crear y administrar credenciales de la aplicación y asignar esas credenciales toousers o grupos que necesitan tener acceso a la aplicación de toohello. En estos casos, usuario final de hello no necesitan tooknow Hola credenciales, pero sigue teniendo la aplicación de acceso de inicio de sesión único toohello simplemente haciendo clic en él en su panel de acceso o a través de un vínculo proporcionado. Esto permite a ambos, administración del ciclo de vida de las credenciales de Hola por administrador de hello, así como comodidad para los usuarios finales mediante el cual no necesita tooremember o administrar contraseñas específicas de la aplicación. las credenciales de Hello están ofuscadas de saludo del usuario final durante el inicio de sesión automatizado de hello en proceso; Sin embargo, técnicamente pueden detectarlos Hola usuario utilizando depuración web tools y los usuarios y los administradores deben seguir presentaban Hola mismas directivas de seguridad como si hello las credenciales directamente por el usuario de Hola. Las credenciales proporcionadas por el administrador son muy útiles, al proporcionar acceso de cuenta que comparten muchos usuarios, como aplicaciones de medios sociales o de uso compartido de documentos.
2. **Usuario administra las credenciales** : los administradores pueden asignar aplicaciones tooend usuarios o grupos y permitir Hola final a los usuarios tooenter sus propias credenciales directamente tras acceder a la aplicación hello para hello primera vez en su panel de acceso. Esto es bastante cómodo para los usuarios finales mediante el cual no es necesario toocontinually escribirlas Hola específico de la aplicación cada vez que accedan a aplicación hello. Este caso de uso también puede utilizarse como una administración tooadministrative piedra ejecución paso a paso de credenciales de hello, mediante el cual administrador Hola puede establecer nuevas credenciales para la aplicación hello en el futuro sin cambiar la experiencia de acceso de aplicación Hola de usuario final de Hola.

En ambos casos, las credenciales se almacenan en un estado cifrado en el directorio de Hola y solo se pasan a través de HTTPS durante Hola automatizada el proceso de inicio de sesión. Usando el inicio de sesión único con contraseña, Azure AD ofrece una cómoda solución de administración de identidad y acceso para las aplicaciones que no admiten el uso de protocolos de federación.

SSO basado en contraseña se basa en un explorador extensión toosecurely recuperar Hola aplicación y usuario información específica de Azure AD y aplicarla toohello servicio. La mayoría de las aplicaciones de SaaS de terceros que son compatibles con Azure AD admite esta característica.

Para el SSO basado en contraseña, pueden ser Hola exploradores de los usuarios:

* Internet Explorer 8, 9, 10 y 11, en Windows 7 o posterior (consulte también la [Guía de implementación de la extensión de IE](active-directory-saas-ie-group-policy.md))
* Chrome (en Windows 7 o posterior y en Mac OS X o posterior)
* Firefox 26.0 o posterior (en Windows XP SP2 o posterior y en Mac OS X 10.6 o posterior)

**Nota:** extensión SSO basada en contraseña de hello pasará a estar disponible para los bordes del 10 de Windows cuando se convierten en admite las extensiones del explorador de Edge.

### <a name="existing-single-sign-on"></a>Inicio de sesión único existente
Al configurar un inicio de sesión único para una aplicación, el portal de administración de Azure de hello proporciona una tercera opción de "existente Single Sign-On". Esta opción simplemente permite Hola administrador toocreate a una aplicación de tooan de vínculo y lo coloca en el panel de acceso de Hola para los usuarios seleccionados.

Por ejemplo, si hay una aplicación que está configurado tooauthenticate a los usuarios con servicios de federación de Active Directory 2.0, un administrador puede usar Hola "existente Single Sign-On" opción toocreate un tooit de vínculo en el panel de acceso de Hola. Cuando los usuarios tener acceso a vínculos de hello, estos se autentican utilizando servicios de federación de Active Directory 2.0 o cualquier único inicio de sesión solución se ha proporcionado por la aplicación hello.

### <a name="user-provisioning"></a>Aprovisionamiento de usuarios
Para seleccionadas aplicaciones, Azure AD permite el aprovisionamiento automático de usuarios y la cancelación del aprovisionamiento de cuentas en aplicaciones de SaaS de terceros de hello Portal de administración de Azure, utilizando la información de identidad de Windows Server Active Directory o Azure AD. Cuando un usuario se le concede permisos en Azure AD para una de estas aplicaciones, una cuenta puede ser crea automáticamente (aprovisionarse) en la aplicación SaaS de destino de Hola.

Cuando se elimina un usuario o su información cambia en Azure AD, estos cambios también se reflejan en hello aplicación SaaS. Esto significa que, configuración de la administración del ciclo de vida de identidades automatizado permite a los administradores toocontrol y proporcionar aprovisionamiento y cancelación del aprovisionamiento de aplicaciones SaaS. En Azure AD, esta automatización de la administración del ciclo de vida de identidad está habilitada por el aprovisionamiento de usuarios.

más información, consulte toolearn [automatizada de aprovisionamiento de usuarios y desaprovisionamiento tooSaaS aplicaciones](active-directory-saas-app-provisioning.md)

## <a name="get-started-with-hello-azure-ad-application-gallery"></a>Empezar a trabajar con Galería de aplicaciones de Azure AD de Hola
¿Se inició tooget listo? toodeploy inicio de sesión único entre Azure AD y las aplicaciones de SaaS que usa la organización, siga estas instrucciones.

### <a name="using-hello-azure-ad-application-gallery"></a>Uso de la Galería de aplicaciones de Azure AD Hola
Hola [Galería de aplicaciones de Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/) proporciona una lista de las aplicaciones que se conocen toosupport un formulario de inicio de sesión único con Azure Active Directory.

![][1]

Algunas sugerencias para buscar aplicaciones por las funciones que admiten:

* Azure AD admite el aprovisionamiento automático y la cancelación del aprovisionamiento para todas las aplicaciones de "Destacado" Hola [Galería de aplicaciones de Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/).
* [Aquí](http://social.technet.microsoft.com/wiki/contents/articles/20235.azure-active-directory-application-gallery-federated-saas-apps.aspx)se puede consultar una lista de aplicaciones federadas que admiten específicamente el inicio de sesión único federado usando protocolos como SAML, WS-Federation u OpenID Connect.

Una vez que ha encontrado la aplicación, que puede empezar por instrucciones paso a paso de seguimiento Hola presentadas en la Galería de aplicaciones de Hola y de tooenable de portal de administración de Azure de hello inicio de sesión único.

### <a name="application-not-in-hello-gallery"></a>¿Aplicación no está en la Galería Hola?
Si la aplicación no se encuentra en la Galería de aplicaciones de Azure AD de hello, tienes estas opciones:

* **Agregar una aplicación que no figuran en utilizas** -categoría de utilización Hola personalizado en Galería de aplicaciones de hello en hello tooconnect portal de administración de Azure una aplicación que no figuran en su organización se usa. Puede agregar cualquier aplicación que admita SAML 2.0 como aplicación federada o cualquier aplicación que tenga una página de inicio de sesión basada en HTML para usar SSO con contraseña. Para obtener más información, consulte este artículo en [Agregar su propia aplicación](active-directory-saas-custom-apps.md).
* **Agregar su propia aplicación que está desarrollando** : si ha desarrollado la aplicación hello usted mismo, siga las instrucciones de hello en hello Azure AD para desarrolladores documentación tooimplement federado inicio de sesión único o aprovisionamiento mediante Hola API graph de Azure AD. Para obtener más información, vea estos recursos:
  
  * [Escenarios de autenticación para Azure AD](active-directory-authentication-scenarios.md)
  * [https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore)
* **Solicitar una integración de aplicaciones** -solicitar soporte técnico para la aplicación de hello, debe usar hello [foro de comentarios de Azure AD](https://feedback.azure.com/forums/169401-azure-active-directory/).

### <a name="using-hello-azure-management-portal"></a>Usar el portal de administración de Azure de Hola
Puede usar hello extensión de Active Directory en hello Portal de administración de Azure tooconfigure Hola aplicación inicio de sesión único. Como primer paso, necesita un directorio de la sección de Active Directory en el portal de Hola Hola tooselect:

![][2]

toomanage las aplicaciones SaaS de terceros, puede cambiar en la pestaña de aplicaciones de hello del directorio seleccionado Hola. Esta vista permite a los administradores:

* Agregar nuevas aplicaciones de la Galería de Azure AD de hello, así como las aplicaciones que está desarrollando
* Eliminar aplicaciones integradas
* Administrar aplicaciones de Hola que ya han integrado

Tareas administrativas habituales para una aplicación de SaaS de terceros son:

* Habilitar el inicio de sesión único con Azure AD, mediante una contraseña SSO o, si está disponible para el destino de hello SaaS, el SSO federado
* También tiene la opción de habilitar el aprovisionamiento de usuarios para el aprovisionamiento y el desaprovisionamiento de usuarios (administración del ciclo de vida de identidad)
* Para las aplicaciones donde está habilitado el aprovisionamiento de usuarios, seleccione los usuarios que tienen acceso a aplicaciones de toothat

Para las aplicaciones de la galería que admiten un inicio de sesión único federado, configuración normalmente requiere que tooprovide valores de configuración adicionales, como certificados y metadatos toocreate una confianza federada entre la aplicación de terceros de hello y Azure AD. Asistente para configuración de Hello le guía a través de los detalles de Hola y proporciona un acceso sencillo toohello datos específicos de la aplicación de SaaS y las instrucciones.

Para las aplicaciones de la galería que admitan el aprovisionamiento automático de usuarios, esto requiere toogive Azure AD permisos toomanage sus cuentas en aplicaciones de SaaS Hola. Como mínimo, debe tooprovide las credenciales de Azure AD deberían utilizar para autenticar a través de la aplicación de destino de toohello. Si hay valores de configuración adicionales que necesite toobe proporciona depende de los requisitos de Hola de aplicación hello.

## <a name="deploying-azure-ad-integrated-applications-toousers"></a>Implementación de Azure AD integrado toousers de aplicaciones
Azure AD proporciona varias maneras de personalizables toodeploy aplicaciones tooend-usuarios de su organización:

* Panel de acceso de Azure AD
* Iniciador de aplicaciones de Office 365
* Aplicaciones de toofederated de inicio de sesión directo
* Vínculos profundos toofederated, basada en contraseña, o aplicaciones existentes

Los métodos elija toodeploy en su organización es su entera discreción.

### <a name="azure-ad-access-panel"></a>Panel de acceso de Azure AD
Hola Panel de acceso en https://myapps.microsoft.com es un portal basado en web que permite a un usuario final con una cuenta profesional en Azure Active Directory tooview e iniciar aplicaciones basadas en nube toowhich han sido concedido acceso hello Azure AD Administrador. Si es un usuario final con [Azure Active Directory Premium](https://azure.microsoft.com/pricing/details/active-directory/), también puede utilizar las capacidades de administración de grupos de autoservicio a través de hello Panel de acceso.

![][3]

Hola Panel de acceso es independiente de hello Portal de administración de Azure y no requiere toohave a los usuarios una suscripción de Azure o la suscripción a Office 365.

Para obtener más información sobre el panel de acceso de hello Azure AD, vea hello [panel de acceso de introducción toohello](active-directory-saas-access-panel-introduction.md).

### <a name="office-365-application-launcher"></a>Iniciador de aplicaciones de Office 365
Para las organizaciones que han implementado con Office 365, las aplicaciones asignadas toousers a través de Azure AD también aparecerá en el portal de Office 365 hello en https://portal.office.com/myapps. Resulta conveniente y fácil para los usuarios en una organización toolaunch sus aplicaciones sin necesidad de toouse un portal de segundo y recomienda Hola aplicación iniciar soluciones para organizaciones que usen Office 365.

![][4]

Para obtener más información acerca de iniciador de la aplicación hello Office 365, vea [que la aplicación aparezca en el iniciador de aplicaciones de Office 365 hello](https://msdn.microsoft.com/office/office365/howto/connect-your-app-to-o365-app-launcher).

### <a name="direct-sign-on-toofederated-apps"></a>Aplicaciones de toofederated de inicio de sesión directo
Mayoría de las aplicaciones federadas que admiten OpenID, WS-Federation o SAML 2.0 conectan también compatibilidad con capacidad de Hola para toostart de usuarios en la aplicación hello y, a continuación, obtengan iniciadas sesión a través de Azure AD por redireccionamiento automático o haciendo clic en un toosign de vínculo en. Esto se conoce como proveedor de servicios-inicia sesión y admiten más de las aplicaciones federadas en Galería de aplicaciones de hello Azure AD (vea la documentación de hello vinculado desde el Asistente para la configuración de inicio de sesión único de la aplicación hello hello Azure portal de administración de detalles).

![][5]

### <a name="direct-sign-on-links-for-federated-password-based-or-existing-apps"></a>Vínculos de inicio de sesión directos para aplicaciones federadas, con contraseña o existentes
Azure AD también admite vínculos de inicio de sesión único directos tooindividual aplicaciones que admiten basada en contraseña de inicio de sesión único, un inicio de sesión único existente y cualquier forma de un inicio de sesión único federado.

Estos vínculos son direcciones URL especialmente diseñada que envían a los usuarios a través de hello Azure AD inicio de sesión para una aplicación específica sin necesidad de usuario de hello iniciarlos desde el panel de acceso de hello Azure AD u Office 365. Estas direcciones de URL de inicio de sesión único puede encontrarse en la ficha Panel de Hola de cualquier aplicación previamente integrada en hello sección de Active Directory del portal de administración de Azure de hello, tal y como se muestra en la siguiente captura de pantalla de Hola.

![][6]

Estos vínculos se pueden copiar y pegan desde cualquier lugar que desea tooprovide un inicio de sesión de vínculo toohello seleccionado aplicación. Podría ser en un mensaje de correo electrónico o en cualquier portal personalizado basado en web que haya configurado para el acceso de los usuarios a la aplicación. Este es un ejemplo de una AD de Azure único inicio de sesión URL directa de Twitter:

`https://myapps.microsoft.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

URL específicas del tooorganization similar para el panel de acceso de hello, puede personalizar aún más esta dirección URL mediante la adición de uno de los dominios activo o comprobado de hello para el directorio después de dominio de hello myapps.microsoft.com. Esto garantiza que cualquier personalización de marca corporativa se carga inmediatamente en la página de inicio de sesión de hello sin necesidad tooenter en primer lugar su ID de usuario del usuario hello:

`https://myapps.microsoft.com/contosobuild.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Cuando un usuario autorizado hace clic en uno de estos vínculos específicos de la aplicación, primero vea su organización página de inicio de sesión (suponiendo que no están firmados) y después en el inicio de sesión son tootheir redirigida aplicación sin detener primero en el panel de acceso de Hola. Si falta requisitos previos tooaccess Hola aplicación, como la extensión del explorador de inicio de sesión único basado en contraseña hello, usuario de Hola vínculo Hola solicitará Hola usuario tooinstall Hola falta la extensión. dirección URL del vínculo Hello también permanece constante si Hola único inicio de sesión para la aplicación hello cambia la configuración.

Estos vínculos usan hello mismos mecanismos de control de acceso como Hola acceder a panel y Office 365, y solo los usuarios o grupos que se han asignado toohello aplicación de portal de administración de Azure Hola podrán autenticar toosuccessfully. Sin embargo, cualquier usuario que no está autorizada verá un mensaje que explica que no se concedió acceso y se proporciona un vínculo tooload Hola acceso panel tooview aplicaciones disponibles para los que tienen acceso.

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Búsqueda de aplicaciones de nube no sancionadas con Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)
* [Introducción tooManaging tooApps de acceso](active-directory-managing-access-to-apps.md)
* [Comparación de funcionalidades para administrar identidades externas con Azure Active Directory](active-directory-b2b-compare-external-identities.md)

<!--Image references-->
[1]: ./media/active-directory-appssoaccess-whatis/onlineappgallery.png
[2]: ./media/active-directory-appssoaccess-whatis/azuremgmtportal.png
[3]: ./media/active-directory-appssoaccess-whatis/accesspanel.png
[4]: ./media/active-directory-appssoaccess-whatis/officeapphub.png
[5]: ./media/active-directory-appssoaccess-whatis/workdaymobile.png
[6]: ./media/active-directory-appssoaccess-whatis/deeplink.png
