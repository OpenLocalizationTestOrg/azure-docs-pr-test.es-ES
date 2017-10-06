---
title: "inicio de sesión en aaaSingle con el Proxy de aplicación | Documentos de Microsoft"
description: "Explica cómo tooprovide inicio de sesión único mediante el Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 0047e834cd42e057a75ebc0c5dcf860734464a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="kerberos-constrained-delegation-for-single-sign-on-tooyour-apps-with-application-proxy"></a>Delegación limitada de Kerberos para las aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación

Puede proporcionar un inicio de sesión único para las aplicaciones locales publicadas a través de Proxy de aplicación que se protegen con la autenticación integrada de Windows. Estas aplicaciones requieren un vale Kerberos para el acceso. Proxy de aplicación utiliza la delegación limitada de Kerberos (KCD) toosupport estas aplicaciones. 

Puede habilitar las aplicaciones de tooyour de inicio de sesión único mediante la autenticación de Windows integrada (IWA) proporcionando el permiso de conectores de Proxy de aplicación en los usuarios de Active Directory tooimpersonate. conectores de Hello usar este permiso toosend y reciban tokens en su nombre.

## <a name="how-single-sign-on-with-kcd-works"></a>Cómo funciona el inicio de sesión único con KCD
Este diagrama explica el flujo de hello cuando un usuario intenta tooaccess una aplicación local que usa IWA.

![Diagrama de flujos de autenticación de Microsoft AAD](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. usuario de Hello entra en la aplicación hello URL tooaccess Hola local a través de Proxy de aplicación.
2. Proxy de aplicación redirige toopreauthenticate de servicios de autenticación de hello solicitud tooAzure AD. En este momento, Azure AD aplica cualquier autenticación correspondiente, así como directivas de autorización, como la autenticación multifactor. Si se valida el usuario de hello, Azure AD crea un token y lo envía toohello usuario.
3. usuario de Hello pasa Hola token tooApplication Proxy.
4. Proxy de aplicación valida el token de Hola y recupera Hola nombre Principal de usuario (UPN) del mismo y, a continuación, envía Hola solicitud, Hola UPN y Hola nombre Principal de servicio (SPN) toohello conector a través de un canal seguro con doble autenticación.
5. Hola conector realiza la negociación de la delegación limitada de Kerberos (KCD) con hello local AD, suplantando Hola usuario tooget una aplicación de toohello símbolo (token) de Kerberos.
6. Active Directory envía el token de Kerberos Hola Hola aplicación toohello conector.
7. Hola conector envía Hola solicitud toohello aplicación servidor original, con el token de Kerberos de Hola que recibió de AD.
8. aplicación Hello envía Hola respuesta toohello conector, que, a continuación, se devuelve toohello servicio de Proxy de aplicación y, finalmente, el usuario toohello.

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar a trabajar con un inicio de sesión único para aplicaciones IWA, asegúrese de que su entorno está listo con hello siguientes configuraciones:

* Las aplicaciones, como las aplicaciones SharePoint Web, se establecen toouse autenticación integrada de Windows. Para más información, consulte [Habilitar la compatibilidad con la autenticación Kerberos](https://technet.microsoft.com/library/dd759186.aspx) o, para SharePoint, consulte [Planear la autenticación Kerberos en SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).
* Todas las aplicaciones tienen [nombres de entidad de seguridad de servicio](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).
* Hola Hola de ejecución de servidor Conector y el servidor de hello ejecutando la aplicación hello están unidos a un dominio y parte del programa Hola mismo dominio o en dominios de confianza. Para obtener más información sobre la unión a un dominio, consulte [unirse a un dominio de equipo tooa](https://technet.microsoft.com/library/dd807102.aspx).
* servidor de Hello ejecutando Hola conector tiene tooread de atributo TokenGroupsGlobalAndUniversal acceso Hola para los usuarios. Esta configuración predeterminada podría ha visto afectada por el entorno de Hola de refuerzo de la seguridad.

### <a name="configure-active-directory"></a>Configurar Active Directory
la configuración de Active Directory Hola varía, dependiendo de si el conector del Proxy de aplicación y el servidor de aplicaciones de hello están en Hola el mismo dominio o no.

#### <a name="connector-and-application-server-in-hello-same-domain"></a>Conector y el servidor de aplicaciones de hello mismo dominio
1. En Active Directory, vaya demasiado**herramientas** > **usuarios y equipos de**.
2. Seleccione servidor hello ejecuta el conector de Hola.
3. Haga clic en el botón derecho y seleccione **Propiedades** > **Delegación**.
4. Seleccione **confiar en este equipo para servicios solo de delegación toospecified**. 
5. En **toowhich servicios esta cuenta puede presentar credenciales delegadas** agregar valor Hola para hello identidad SPN Hola del servidor de aplicaciones. Esto permite a los usuarios tooimpersonate de conector del Proxy de aplicación hello en AD frente a aplicaciones de hello definidas en la lista de Hola.

   ![Captura de pantalla de ventana Conector-Propiedades SVR](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-application-server-in-different-domains"></a>Conector y servidor de aplicaciones en dominios diferentes
1. Para obtener una lista de requisitos previos para trabajar con KCD entre dominios, vea [Delegación limitada Kerberos entre dominios](https://technet.microsoft.com/library/hh831477.aspx).
2. Hola de uso `principalsallowedtodelegateto` propiedad toodelegate Hola conector server tooenable Hola Proxy de aplicación para el servidor de conector de Hola. servidor de aplicaciones de Hello es `sharepointserviceaccount` y hello delegación de servidor es `connectormachineaccount`. Para Windows 2012 R2, use este código como un ejemplo:

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

Sharepointserviceaccount puede ser la cuenta de equipo SPS de Hola o una cuenta de servicio bajo qué Hola SPS se ejecuta el grupo de aplicaciones.

## <a name="configure-single-sign-on"></a>Configurar inicio de sesión único 
1. Publicar su aplicación según las instrucciones de toohello descritas en [publicar aplicaciones con Proxy de aplicación](application-proxy-publish-azure-portal.md). Asegúrese de que tooselect **Azure Active Directory** como hello **método de autenticación previa**.
2. Después de la aplicación aparece en la lista de Hola de aplicaciones empresariales, selecciónelo y haga clic en **inicio de sesión único**.
3. Establecer el modo de inicio de sesión único de hello demasiado**autenticación integrada de Windows**.  
4. Escriba hello **SPN interno de la aplicación** Hola servidor de aplicaciones. En este ejemplo, hello SPN de nuestra aplicación publicada es http/www.contoso.com. Esta toobe de necesidades SPN en lista de hello del conector de servicios toowhich Hola puede presentar credenciales delegadas. 
5. Elija hello **delegar la identidad de inicio de sesión** para toouse de conector de hello en nombre de los usuarios. Para más información, vea [Trabajar con identidades en la nube y locales diferentes](#Working-with-different-on-premises-and-cloud-identities)

   ![Configuración avanzada de aplicaciones](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  


## <a name="sso-for-non-windows-apps"></a>SSO para las aplicaciones no son de Windows
Hola flujo de la delegación de Kerberos en el Proxy de aplicación de Azure AD se inicia cuando Azure AD autentica el usuario de hello en la nube de Hola. Una vez que llega de solicitud de hello en local, Hola Proxy de aplicación de Azure AD conector emite un vale de Kerberos en nombre de usuario de hello interactuando con Hola Active Directory local. Este proceso es que se hace referencia tooas delegación limitada de Kerberos (KCD). Hola fase siguiente, se envía una solicitud toohello aplicación de back-end con este vale de Kerberos. Hay varios protocolos que definen cómo toosend tales solicitudes. La mayoría de los servidores que no son Windows esperan Negotiate/SPNego, que ahora se admite en el proxy de aplicación de Azure AD.

Para obtener más información acerca de Kerberos, consulte [todo lo que desea tooknow sobre la delegación limitada de Kerberos (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

Las aplicaciones que no son de Windows normalmente usan nombres de usuario o nombres de cuenta SAM en lugar de direcciones de correo electrónico de dominio. Si esa situación aplica a las aplicaciones de tooyour, deberá tooconfigure Hola delegada inicio de sesión identidad campo tooconnect las identidades de aplicaciones de nube identidades tooyour. 

## <a name="working-with-different-on-premises-and-cloud-identities"></a>Trabajar con diferentes identidades locales y de nube
Proxy de aplicación se da por supuesto que los usuarios tengan exactamente Hola la misma identidad en la nube de Hola y local. Si no es el caso de hello, puede seguir sirve KCD para inicio de sesión único. Configurar un **delegar la identidad de inicio de sesión** para cada toospecify aplicación qué identidad debe usarse al realizar el inicio de sesión único.  

Esta funcionalidad permite muchas organizaciones que tienen diferentes en el local y en la nube identidades toohave SSO de hello en la nube local tooon aplicaciones sin necesidad de hello usuarios tooenter diferentes nombres de usuario y contraseñas. Esto incluye las organizaciones que:

* Tiene varios dominios internamente (joe@us.contoso.com, joe@eu.contoso.com) y un dominio individual en la nube de hello (joe@contoso.com).
* Tiene el nombre de dominio no enrutables internamente (joe@contoso.usa) y otra en la nube de hello legal.
* No utilizan nombres de dominio internamente (joe)
* Usar distintos alias local y en la nube de Hola. Por ejemplo, joe-johns@contoso.com en comparación con joej@contoso.com  

Con el Proxy de aplicación, puede seleccionar qué Hola de tooobtain toouse de identidad vale de Kerberos. Esta configuración es por aplicación. Algunas de estas opciones son adecuadas para los sistemas que no aceptan el formato de dirección de correo electrónico, otras están pensadas para el inicio de sesión alternativo.

![Captura de pantalla de parámetro de identidad de inicio de sesión delegado](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

Si se utiliza la identidad de inicio de sesión delegados, el valor de hello podría no ser único en todos los dominios de Hola o bosques de su organización. Puede evitar este problema al publicar estas aplicaciones dos veces con dos grupos diferentes de conector. Puesto que cada aplicación tiene una audiencia de usuarios diferentes, puede combinar su dominio diferente de tooa de conectores.

### <a name="configure-sso-for-different-identities"></a>Configurar el inicio de sesión único para distintas identidades
1. Configurar Azure AD Connect para que identidad principal hello es la dirección de correo electrónico (correo electrónico) de Hola. Esto se realiza como parte del programa Hola a personalizar el proceso, cambiando hello **nombre Principal de usuario** campo en la configuración de sincronización Hola. Estas opciones también determinan cómo los usuarios iniciar sesión en tooOffice365, Windows10 dispositivos y otras aplicaciones que usan Azure AD como su almacén de identidades.  
   ![Captura de pantalla de la identificación de usuarios - lista desplegable de Nombre principal de usuario](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. En Opciones de configuración de aplicación de hello para la aplicación hello le gustaría toomodify, seleccione hello **delegar la identidad de inicio de sesión** toobe utiliza:

   * Nombre principal de usuario (por ejemplo, joe@contoso.com).
   * Nombre principal de usuario alternativo (por ejemplo, joed@contoso.local).
   * Parte nombre de usuario del nombre principal de usuario (por ejemplo, joe).
   * Parte nombre de usuario del nombre principal de usuario alternativo (por ejemplo, joed).
   * Nombre de cuenta SAM local (depende de la configuración del controlador de dominio de hello)

### <a name="troubleshooting-sso-for-different-identities"></a>Solución de problemas de SSO para diferentes identidades
Si hay un error en el proceso SSO de hello, aparece en el registro de eventos de máquina de conector de hello como se explica en [solución de problemas](application-proxy-back-end-kerberos-constrained-delegation-how-to.md).
Sin embargo, en algunos casos, solicitud de Hola se envía correctamente toohello back-end aplicación mientras esta aplicación responde en diversas otras respuestas HTTP. Solución de problemas de estos casos debe empezar examinando el número de evento 24029 en la máquina de conector de hello en el registro de eventos de sesión de Proxy de aplicación Hola. identidad de usuario de Hola que se usó para la delegación aparece en campos de "usuario" hello en detalles del evento Hola. Seleccione tooturn en el registro de sesión, **mostrar analíticos y de depuración registros** en el menú de vista del Visor de eventos de Hola.

## <a name="next-steps"></a>Pasos siguientes

* [¿Cómo tooconfigure una toouse de aplicación de Proxy de aplicación delegación limitada de Kerberos](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)
* [Solucionar los problemas que tiene con el Proxy de aplicación](active-directory-application-proxy-troubleshoot.md)


Para obtener las actualizaciones y noticias más recientes de hello, visite hello [blog de Proxy de aplicación](http://blogs.technet.com/b/applicationproxyblog/)

