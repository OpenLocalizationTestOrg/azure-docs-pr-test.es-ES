---
title: "aaaAuthenticate con local de Active Directory en la aplicación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de las diferentes opciones de Hola para las aplicaciones de línea de negocio de tooauthenticate de servicio de aplicaciones de Azure con la instancia local de Active Directory"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Autenticación con Active Directory local en aplicaciones de Azure
Este artículo muestra cómo tooauthenticate con local Active Directory (AD) en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md). Una aplicación de Azure se hospeda en la nube de hello, pero hay formas tooauthenticate AD usuarios locales con seguridad. 

## <a name="authenticate-through-azure-active-directory"></a>Autenticación mediante Azure Active Directory
Un inquilino de Azure Active Directory puede estar sincronizado con directorios con una implementación de AD local. Este enfoque permite a los usuarios de AD tener acceso a la aplicación desde internet de Hola y autenticarse con sus credenciales locales. Además, el Servicio de aplicaciones de Azure proporciona una [solución completa para este método](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Con algunos clics de botón, puede habilitar la autenticación con un inquilino sincronizado con directorios para la aplicación de Azure. Este enfoque tiene Hola siguientes ventajas:

* No requiere ningún código de autenticación en la aplicación. Permitir que realice de servicio de aplicaciones Hola autenticación y dedicar su tiempo a proporcionar una funcionalidad de la aplicación.
* [API de Azure AD Graph](http://msdn.microsoft.com/library/azure/hh974476.aspx) permite tener acceso a datos de toodirectory desde la aplicación de Azure.
* Proporciona SSO demasiado[todas las aplicaciones compatibles con Azure Active Directory](/marketplace/active-directory/), como Office 365, Dynamics CRM Online, Microsoft Intune y miles de aplicaciones de nube no son de Microsoft. 
* Azure Active Directory admite el control de acceso basado en roles. Puede usar el patrón de hello [Authorize(Roles="X")] con código de tooyour unos cambios mínimos.

toosee toowrite una aplicación de Azure de línea de negocio que se autentica con Azure Active Directory, vea [crear una aplicación de Azure de línea de negocio con la autenticación de Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>Autenticación mediante STS local
Si tienes un local servicio de token seguro (STS) como los servicios de federación de Active Directory (AD FS), puede usar dicha autenticación toofederate para la aplicación de Azure. Este enfoque funciona mejor cuando la directiva de empresa prohíbe almacenar datos de AD en Azure. Sin embargo, tenga en cuenta los siguiente hello:

* La topología de STS debe implementarse localmente, con la sobrecarga de administración y costo.
* Solo los administradores de AD FS pueden configurar [confianza confianzas de terceros y las reglas de notificación](http://technet.microsoft.com/library/dd807108.aspx), que pueden limitar opciones del desarrollador de Hola. En hello otra parte, es posible toomanage y personalizar [notificaciones](http://technet.microsoft.com/library/ee913571.aspx) por la aplicación.
* Acceder a tooon local datos de AD requieren una solución independiente a través del firewall corporativo Hola.

toosee toowrite una aplicación de Azure de línea de negocio que se autentica con un STS local, vea [crear una aplicación de Azure de línea de negocio con autenticación de AD FS](web-sites-dotnet-lob-application-adfs.md).

