---
title: "Certificación de AppSource para Azure Active Directory | Microsoft Docs"
description: "Información detallada sobre cómo certificar su instancia de AppSource de la aplicación para Azure Active Directory."
services: active-directory
documentationcenter: 
author: andretms
manager: mtillman
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 5601ad80e271364fec519cf34bcdc2f650f3bb92
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2017
---
# <a name="how-to-get-appsource-certified-for-azure-active-directory"></a>Obtención de AppSource certificado para Azure Active Directory
[Microsoft AppSource](https://appsource.microsoft.com/) es un destino para que los usuarios empresariales detecten, prueben y administren aplicaciones SaaS de línea de negocio (SaaS independiente y un complemento para productos SaaS de Microsoft existentes).

Para que una aplicación SaaS independiente se muestre en AppSource, la aplicación debe aceptar el inicio de sesión único desde cuentas profesionales de cualquier compañía u organización que cuente con Azure Active Directory. El proceso de inicio de sesión debe usar los protocolos [OpenID Connect](./active-directory-protocols-openid-connect-code.md) o [OAuth 2.0](./active-directory-protocols-oauth-code.md). La integración de SAML no se acepta como certificación de AppSource.

## <a name="guides-and-code-samples"></a>Guías y ejemplos de código
Si quiere saber cómo integrar la aplicación con Azure Active Directory mediante OpenID Connect, siga nuestras guías y ejemplos de código en la [Guía del desarrollador de Azure Active Directory](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers") (Introducción a Azure AD para desarrolladores).

## <a name="multi-tenant-applications"></a>Aplicaciones multiinquilino

Una aplicación que acepta inicios de sesión de usuarios de cualquier compañía u organización que tenga Azure Active Directory sin que se requiera otra instancia, configuración o implementación se denomina *aplicación multiempresa*. AppSource recomienda que las aplicaciones implementen una arquitectura multiempresa para habilitar la experiencia de evaluación gratuita *con un solo clic*.

Para habilitar la arquitectura multiempresa en la aplicación:
- Establezca la propiedad `Multi-Tenanted` como `Yes` en la información de registro de la aplicación de [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (de manera predeterminada, las aplicaciones creadas en Azure se configuran como de *inquilino único*).
- Actualice el código para que envíe solicitudes al punto de conexión "`common`" (actualice el punto de conexión de *https://login.microsoftonline.com/{yourtenant}* a *https://login.microsoftonline.com/common*).
- En algunas plataformas, como ASP.NET, también hay que actualizar el código para que acepte varios emisores.

Para más información sobre la arquitectura multiempresa, vea [Inicio de sesión de cualquier usuario de Azure Active Directory (AD) mediante el patrón de aplicación multiempresa](./active-directory-devhowto-multi-tenant-overview.md).

### <a name="single-tenant-applications"></a>Aplicaciones de inquilino único
Las aplicaciones que solo aceptan inicios de sesión de usuarios de una instancia de Azure Active Directory definida se denominan *aplicaciones de inquilino único*. Los usuarios externos (incluidas las cuentas profesionales o educativas de otras organizaciones o una cuenta personal) pueden iniciar sesión en una aplicación de inquilino único después de agregar cada usuario como *cuenta de invitado* a la instancia de Azure Active Directory en la que esa aplicación está registrada. Puede agregar usuarios como cuentas de invitado a una instancia de Azure Active Directory a través de la [*Colaboración B2B en Azure AD*](../active-directory-b2b-what-is-azure-ad-b2b.md), que se puede realizar [mediante programación](../active-directory-b2b-code-samples.md). Cuando se agrega un usuario como cuenta de invitado a una instancia de Azure Active Directory, se envía un correo electrónico al usuario, que tiene que aceptar la invitación haciendo clic en el vínculo incluido en el correo electrónico de invitación. Las invitaciones que se envían a un usuario adicional de una organización que invita que también es miembro de la organización asociada no tienen que aceptarse para iniciar sesión.

Las aplicaciones de inquilino único pueden habilitar la experiencia *Ponerse en contacto conmigo*, pero si se quiere habilitar la experiencia de evaluación gratuita/con un solo clic que AppSource recomienda, habilite en su lugar la arquitectura multiempresa en la aplicación.


## <a name="appsource-trial-experiences"></a>Experiencias de evaluación gratuita de AppSource

### <a name="free-trial-customer-led-trial-experience"></a>Evaluación gratuita (experiencia de evaluación dirigida por el usuario) 
La *evaluación dirigida por el usuario* es la experiencia que AppSource recomienda porque ofrece acceso con un solo clic a la aplicación. Vea a continuación una ilustración del aspecto que tiene esta experiencia:<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>El usuario busca su aplicación en el sitio web de AppSource</li><li>Selecciona la opción "Evaluación gratuita"</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>AppSource redirige al usuario a una dirección URL en su sitio web</li><li>El sitio web inicia el proceso de <i> inicio de sesión único</i> automáticamente (al cargar la página)</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>Se redirige al usuario a la página de inicio de sesión de Microsoft</li><li>El usuario proporciona las credenciales para iniciar sesión</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>El usuario le da su consentimiento en la aplicación</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Se completa el inicio de sesión y se redirige al usuario al sitio web</li><li>El usuario inicia la evaluación gratuita</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>Ponerse en contacto conmigo (experiencia de evaluación dirigida por el partner)
La *experiencia de evaluación de asociado* puede usarse cuando tiene que producirse una operación manual o a largo plazo para aprovisionar al usuario o la compañía: por ejemplo, la aplicación tiene que aprovisionar máquinas virtuales, instancias de base de datos u operaciones que tardan mucho en completarse. En este caso, después de que el usuario seleccione el botón *"Solicitar versión de prueba"* y rellene un formulario, AppSource le envía la información de contacto del usuario. Tras recibir esta información, se aprovisiona el entorno y se envían al usuario las instrucciones sobre cómo acceder a la experiencia de evaluación:<br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li>El usuario busca su aplicación en el sitio web de AppSource</li><li>Selecciona la opción "Ponerse en contacto conmigo"</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li>Rellena un formulario con información de contacto</li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td>Usted recibe la información del usuario</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td>Configura el entorno</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td>Se pone en contacto con el usuario con información de la versión de evaluación</td>
        </tr>
        </table><br/><br/>
        <ul><li>Usted recibe la información del usuario y configura la instancia de evaluación</li><li>Envía al usuario el hipervínculo de acceso a la aplicación</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>El usuario accede a la aplicación y completa el proceso de inicio de sesión único</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>El usuario le da su consentimiento en la aplicación</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Se completa el inicio de sesión y se redirige al usuario al sitio web</li><li>El usuario inicia la evaluación gratuita</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>Más información
Para más información sobre la experiencia de evaluación de AppSource, vea [este vídeo](https://aka.ms/trialexperienceforwebapps). 
 
## <a name="next-steps"></a>Pasos siguientes

- Para más información sobre cómo generar aplicaciones que admitan inicios de sesión de Azure Active Directory, vea [Escenarios de autenticación para Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios). 

- Para información sobre cómo mostrar la aplicación SaaS en AppSource, vea [AppSource Partner Information](https://appsource.microsoft.com/partners) (Información sobre el partner de AppSource).


## <a name="get-support"></a>Obtención de soporte técnico
Para la integración de Azure Active Directory, se usa [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+appsource) con la comunidad para ofrecer soporte técnico. 

Se recomienda muy especialmente que primero plantee sus preguntas sobre Stack Overflow y examine los problemas existentes para ver si algún usuario ha hecho esa pregunta antes. Asegúrese de que sus preguntas o comentarios se etiquetan con [`[azure-active-directory]` y `[appsource]`](http://stackoverflow.com/questions/tagged/azure-active-directory+appsource).

Use la siguiente sección de comentarios para proporcionar sus opiniones y ayudarnos a afinar y remodelar el contenido.

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->