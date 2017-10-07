---
title: aaaHow tooget AppSource certificada para Azure Active Directory | Documentos de Microsoft
description: "Información detallada sobre cómo tooget su aplicación AppSource certificada para Azure Active Directory."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
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
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a>Cómo tooget AppSource certificadas para Azure Active Directory
[Microsoft AppSource](https://appsource.microsoft.com/) es un destino para toodiscover de los usuarios empresariales, pruebe y administrar aplicaciones de SaaS de línea de negocio (independiente SaaS y un complemento tooexisting Microsoft SaaS productos).

toolist una aplicación de SaaS en AppSource independiente, la aplicación debe aceptar un inicio de sesión único de cuentas para el trabajo desde cualquier empresa u organización con Azure Active Directory. proceso de inicio de sesión Hola debe usar hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) o [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocolos. La integración de SAML no se acepta como certificación de AppSource.

## <a name="guides-and-code-samples"></a>Guías y ejemplos de código
Si desea toolearn sobre cómo toointegrate su aplicación con Azure Active Directory con Openid connect, siga nuestras guías y ejemplos de hello de código [Guía del desarrollador de Azure Active Directory](./active-directory-developers-guide.md#get-started "empezar a trabajar con Azure AD para los desarrolladores").

## <a name="multi-tenant-applications"></a>Aplicaciones multiinquilino

Una aplicación que acepta inicios de sesión de usuarios de cualquier compañía u organización que tenga Azure Active Directory sin que se requiera otra instancia, configuración o implementación se denomina *aplicación multiempresa*. AppSource recomienda que las aplicaciones implementan Hola multiempresa tooenable *con un solo clic* liberar una experiencia de evaluación.

En orden tooenable multiempresa en su aplicación:
- Establecer `Multi-Tenanted` propiedad demasiado`Yes` en información del registro de la aplicación hello [Portal de Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (de forma predeterminada, las aplicaciones creadas en Portal de Azure Hola están configuradas como *único inquilino*)
- Actualizar la toohello de las solicitudes de código toosend '`common`' punto de conexión (actualizar el extremo de Hola de *https://login.microsoftonline.com/ {yourtenant}* demasiado*https://login.microsoftonline.com/common*)
- Para algunas plataformas, como ASP.NET, debe también tooupdate su tooaccept código varios emisores

Para obtener más información acerca de la arquitectura multiempresa, consulte: [cómo toosign en cualquier usuario de Azure Active Directory (AD) mediante Hola patrón de aplicación de varios inquilinos](./active-directory-devhowto-multi-tenant-overview.md).

### <a name="single-tenant-applications"></a>Aplicaciones de inquilino único
Las aplicaciones que solo aceptan inicios de sesión de usuarios de una instancia de Azure Active Directory definida se denominan *aplicaciones de inquilino único*. Los usuarios externos (incluidas las cuentas de trabajo o la escuela de otras organizaciones o cuenta personal) pueden iniciar sesión en la aplicación de inquilino único tooa después de agregar cada usuario como *cuenta de invitado* toohello Azure Active Directory de la instancia que se registra la aplicación Hello. Puede agregar usuarios como tooan de cuentas de invitado Azure Active Directory a través de hello [ *colaboración B2B de Azure AD* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - y que es posible [mediante programación](../active-directory-b2b-code-samples.md). Cuando se agrega un usuario como cuenta de invitado tooan Azure Active Directory, un correo electrónico de invitación se envía toohello usuario, que tiene la invitación de hello tooaccept haciendo clic en el vínculo de hello en correo electrónico de invitación de Hola. Las invitaciones que se enviaron tooan adicional del usuario en una organización invitar a que también es un miembro de la organización del asociado de hello son tooaccept no se requiere un toosign de invitación en.

Las aplicaciones de inquilinos solo pueden habilitar hello *contacto Me* experiencia, pero si desea tooenable Hola con un solo clic / libre una experiencia de evaluación que recomienda AppSource, habilite la arquitectura multiempresa en la aplicación en su lugar.


## <a name="appsource-trial-experiences"></a>Experiencias de evaluación gratuita de AppSource

### <a name="free-trial-customer-led-trial-experience"></a>Evaluación gratuita (experiencia de evaluación dirigida por el usuario) 
Hola *orientada a los clientes de prueba* es experiencia Hola que AppSource recomienda ya que ofrecen una aplicación de tooyour de acceso con un solo clic. Vea a continuación una ilustración del aspecto que tiene esta experiencia:<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>El usuario busca su aplicación en el sitio web de AppSource</li><li>Selecciona la opción "Evaluación gratuita"</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>AppSource redirige la dirección URL de tooa de usuario en el sitio web</li><li>El sitio web inicia hello <i>single-sign-on</i> proceso automáticamente (al cargar la página)</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>Usuario es página redirigidos tooMicrosoft inicio de sesión</li><li>El usuario proporciona credenciales toosign en</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>El usuario le da su consentimiento en la aplicación</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>En el inicio de sesión se completa y el usuario es redirigido tooyour back-sitio de web</li><li>Usuario inicia la prueba gratuita de Hola</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>Ponerse en contacto conmigo (experiencia de evaluación dirigida por el partner)
Hola *una experiencia de evaluación de socios comerciales* puede usarse cuando un manual o una operación de larga duración necesita usuario Hola de toohappen tooprovision / compañía: por ejemplo, la aplicación necesita tooprovision las máquinas virtuales, instancias de base de datos, o operaciones que toman mucho tiempo toocomplete. En este caso, después de usuario selecciona hello *solicitud de versión de prueba* botón y rellena un formulario, AppSource envía Hola información de contacto del usuario. Al recibir esta información, que, a continuación, aprovisionar el entorno de Hola y enviar al usuario de toohello Hola instrucciones sobre cómo tooaccess Hola una experiencia de evaluación:<br/><br/>

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
        <ul><li>Usted recibe la información del usuario y configura la instancia de evaluación</li><li>Enviar Hola hipervínculo tooaccess su usuario de toohello la aplicación</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>Usuario tiene acceso a la aplicación y el proceso de inicio de sesión único de hello completa</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>El usuario le da su consentimiento en la aplicación</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>En el inicio de sesión se completa y el usuario es redirigido tooyour back-sitio de web</li><li>Usuario inicia la prueba gratuita de Hola</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>Más información
Para obtener más información acerca de la experiencia de evaluación de hello AppSource, consulte [este vídeo](https://aka.ms/trialexperienceforwebapps). 
 
## <a name="next-steps"></a>Pasos siguientes

- Para más información sobre cómo generar aplicaciones que admitan inicios de sesión de Azure Active Directory, vea [Escenarios de autenticación para Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios). 

- Para obtener información sobre cómo toolist la aplicación de SaaS en AppSource, visite [AppSource información de socio comercial](https://appsource.microsoft.com/partners)


## <a name="get-support"></a>Obtención de soporte técnico
Para la integración de Azure Active Directory, usamos [desbordamiento de la pila](http://stackoverflow.com/questions/tagged/azure-active-directory) con soporte técnico de hello Comunidad tooprovide. 

Se recomienda encarecidamente que haga sus preguntas acerca del desbordamiento de pila en primer lugar y examinar existente toosee problemas si alguien ha realizado su pregunta antes. Asegúrese de que sus preguntas o comentarios se etiquetan con `[azure-active-directory]`.

Usar hello después de comentarios de tooprovide de sección de comentarios y nos ayudan a refinar y dar forma a nuestro contenido.

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->