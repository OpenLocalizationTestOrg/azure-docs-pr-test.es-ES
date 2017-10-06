---
title: acceso remoto seguro aaaHow tooprovide aplicaciones tooon locales
description: "Explica cómo toouse el Proxy de aplicación de Azure AD tooprovide el acceso remoto seguro tooyour local las aplicaciones."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 289e970ed0596fcd06ccf6b2ad92203366fbb494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprovide-secure-remote-access-tooon-premises-applications"></a>Cómo tooprovide el acceso remoto a aplicaciones locales de tooon

Los empleados hoy en día desean toobe productivos en cualquier lugar, en cualquier momento y desde cualquier dispositivo. Desean toowork en sus propios dispositivos, ya sean tabletas, teléfonos o equipos portátiles. Y esperan toobe capaz de tooaccess todas sus aplicaciones, aplicaciones de SaaS en la nube de Hola y aplicaciones corporativas locales. Proporciona acceso a aplicaciones locales de tooon ha implicado tradicionalmente redes privadas virtuales (VPN) o zonas desmilitarizada (DMZ). No solo son estos toomake complejos y difíciles de soluciones seguras, pero se tooset un consumo elevado de seguridad y administrar.

Hay una forma mejor de realizar esto.

Una plantilla moderna en hello mobile-first, world de nube en primer lugar debe una solución de acceso remoto modernas. La característica Proxy de aplicación de Azure AD forma parte de Azure Active Directory y ofrece acceso remoto como servicio. Eso significa que es fácil toodeploy, usar y administrar.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a>¿Qué es el proxy de la aplicación de Azure Active Directory?
La característica Proxy de la aplicación de Azure AD proporciona un inicio de sesión único (SSO) y acceso remoto seguro para las aplicaciones web hospedadas de forma local, Algunas aplicaciones desearía toopublish incluyen sitios de SharePoint, Outlook Web Access o cualquier otra aplicación de web LOB que tiene. Estas web local las aplicaciones se integran con Azure AD, Hola la misma identidad y controlar la plataforma que usa Office 365. Los usuarios finales pueden acceder a su Hola de aplicaciones local, igual que tener acceso a Office 365 y otras aplicaciones de SaaS integrada con Azure AD. No necesita la infraestructura de red de toochange Hola o requieren VPN tooprovide esta solución para los usuarios.

## <a name="why-is-application-proxy-a-better-solution"></a>¿Por qué Proxy de aplicación es una solución mejor?
El Proxy de aplicación de Azure AD proporciona un tooall de solución de acceso remoto sencillo, seguro y rentable de las aplicaciones locales.

El proxy de aplicación de Azure AD es:

* **Simple**
   * No necesita toochange o actualizar su toowork de aplicaciones con Proxy de aplicación. 
   * Los usuarios obtienen una experiencia coherente de autenticación. Pueden utilizar aplicaciones de SaaS tooboth Hola mis aplicaciones portal tooget inicio de sesión único en la nube de Hola y de aplicaciones local. 
* **Protección**
   * Al publicar aplicaciones mediante el Proxy de aplicación de Azure AD, puede sacar provecho de los controles de autorización enriquecido Hola y análisis de seguridad en Azure. Obtendrá características de seguridad de escala en la nube y de seguridad de Azure, como el acceso condicional y la verificación en dos pasos.
   * No tienes tooopen las conexiones entrantes a través de su firewall toogive a los usuarios remotos acceso. 
* **Rentable**
   * Proxy de aplicación funciona en la nube de hello, por lo que puede ahorrar tiempo y dinero. Soluciones locales normalmente requieren tooset seguridad y mantienen DMZ, servidores perimetrales y otras infraestructuras complejas.  

## <a name="what-kind-of-applications-work-with-application-proxy"></a>¿Qué tipo de aplicaciones funcionan con la característica Proxy de aplicación?
Con esta característica puede tener acceso a diferentes tipos de aplicaciones internas:

* Aplicaciones web que usan la [autenticación integrada de Windows](active-directory-application-proxy-sso-using-kcd.md) para la autenticación.  
* Aplicaciones web que usan el acceso basado en formularios o [basado en encabezados](application-proxy-ping-access.md).  
* Las API que desea tooexpose toorich aplicaciones en distintos dispositivos Web  
* Aplicaciones que se hospedan detrás de una [puerta de enlace de escritorio remoto](application-proxy-publish-remote-desktop.md).  
* Aplicaciones de cliente enriquecido que se integran con hello biblioteca de autenticación de Active Directory (ADAL)

## <a name="how-does-application-proxy-work"></a>¿Cómo funciona el proxy de la aplicación?
Hay dos componentes que necesita tooconfigure toomake trabajo de Proxy de aplicación: un conector y un extremo externo. 

Conector de Hello es un agente ligero que se encuentra en un servidor de Windows dentro de la red. Conector de Hola facilita el flujo de tráfico de Hola de hello servicio de Proxy de aplicación de hello en la nube tooyour aplicación local. Solo usa conexiones salientes, por lo que no tiene puertos de entrada de tooopen o colocar nada en la red Perimetral de Hola. conectores de Hello no tienen estados y extracción información de nube de hello según sea necesario. Para más información sobre los conectores, por ejemplo cómo se equilibra la carga y cómo se autentican, vea [Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md). 

extremo externo Hello es cómo los usuarios obtener acceso a sus aplicaciones fuera de la red. O bien pueden ir directamente tooan dirección URL externa determinada o poder acceder a aplicación Hola a través del portal mis aplicaciones de Hola. Cuando los usuarios vayan tooone de estos puntos de conexión, que autentican en Azure AD y, a continuación, se enrutan a través de la aplicación de hello conector toohello local.

 ![Diagrama de Proxy de la aplicación de Azure AD](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. Hola usuario tiene acceso a la aplicación hello a través del servicio de Proxy de aplicación Hola y tooauthenticate de página de inicio de sesión de Azure AD toohello dirigido.
2. Después de una correcta inicio de sesión en un símbolo (token) se genera y envía toohello dispositivo de cliente.
3. Hola cliente envía Hola token toohello servicio de Proxy de aplicación, que recupera el nombre de entidad de seguridad de usuario (UPN) de Hola y nombre principal de seguridad (SPN) del token de hello, a continuación, dirige el conector del Proxy de aplicación de toohello de solicitud de Hola.
4. Si ha configurado el inicio de sesión único, el conector de hello lleva a cabo ninguna autenticación adicional necesaria en nombre de usuario de Hola.
5. Conector de Hello envía la aplicación local de hello solicitud toohello.  
6. respuesta de Hola se envía a través de usuario de toohello de servicio y el conector de Proxy de aplicación.

### <a name="single-sign-on"></a>Inicio de sesión único
El Proxy de aplicación de Azure AD proporciona el inicio de sesión único (SSO) tooapplications que usan la autenticación de Windows integrada (IWA) o aplicaciones para notificaciones. Si la aplicación utiliza IWA, Proxy de aplicación suplanta a usuario hello mediante delegación limitada de Kerberos tooprovide SSO. Si tiene una aplicación para notificaciones que confíe en Azure Active Directory, SSO funciona porque ya se ha autenticado el usuario de hello Azure AD.

Para obtener más información acerca de Kerberos, consulte [todo lo que desea tooknow sobre la delegación limitada de Kerberos (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

### <a name="managing-apps"></a>Administración de aplicaciones
Uno de la aplicación se publica con el Proxy de aplicación, se puede administrar como cualquier otra aplicación empresarial de hello portal de Azure. Puede usar características de seguridad de Azure Active Directory como la comprobación de acceso y en dos pasos condicional, controlar los permisos de usuario y personalizar Hola personalización de marca para la aplicación. 

## <a name="get-started"></a>Primeros pasos

Antes de configurar Proxy de aplicación, asegúrese de que tiene una [edición de Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) compatible y un directorio de Azure AD para el que es un administrador global.

Introducción a Proxy de aplicación en dos pasos:

1. [Habilitar el Proxy de aplicación y configurar el conector de hello](active-directory-application-proxy-enable.md).    
2. [Publicar aplicaciones](active-directory-application-proxy-publish.md) -uso Hola las aplicaciones locales publicadas y es accesibles con tooget Asistente rápida y sencilla de forma remota.

## <a name="whats-next"></a>Pasos siguientes
Después de publicar la primera aplicación, se puede hacer mucho más con Proxy de aplicación:

* [Habilitar el inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md)
* [Publicar aplicaciones mediante su propio nombre de dominio](active-directory-application-proxy-custom-domains.md)
* [Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md)
* [Trabajo con servidores proxy locales existentes](application-proxy-working-with-proxy-servers.md) 
* [Establecer una página principal personalizada](application-proxy-office365-app-launcher.md)

Para obtener las actualizaciones y noticias más recientes de hello, visite hello [blog de Proxy de aplicación](http://blogs.technet.com/b/applicationproxyblog/)

