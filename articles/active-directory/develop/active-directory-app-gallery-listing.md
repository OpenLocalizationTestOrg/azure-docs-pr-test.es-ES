---
title: "aaaListing la aplicación en la Galería de aplicaciones de Azure Active Directory Hola"
description: "¿Cómo toolist una aplicación que admite el inicio de sesión único en Hola Galería de Azure Active Directory | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a>Lista de la aplicación en la Galería de aplicaciones de Azure Active Directory Hola
una aplicación que admita un inicio de sesión único con Azure Active Directory en hello toolist [Galería de Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), aplicación hello en primer lugar debe tooimplement uno de los siguientes modos de integración de Hola:

* **OpenID Connect** : la integración directa con Azure AD usa OpenID Connect para la autenticación y Hola consentimiento de Azure AD API para la configuración. Si es la primera vez una integración y la aplicación no es compatible con SAML, es el modo recomendado de Hola.
* **SAML** : la aplicación ya tiene proveedores de identidad de otro fabricante Hola capacidad tooconfigure con protocolo SAML de Hola.

A continuación se enumeran los requisitos para cada modo.

## <a name="openid-connect-integration"></a>Integración mediante OpenID Connect
toointegrate su aplicación con Azure AD, Hola siguiente [instrucciones para desarrolladores](active-directory-authentication-scenarios.md). A continuación, completar las siguientes preguntas de Hola y enviar toowaadpartners@microsoft.com.

* Proporcione las credenciales para una cuenta o el inquilino de prueba con la aplicación que puede utilizarse en hello integración de Azure AD equipo tootest Hola.  
* Se proporcionan instrucciones sobre el modo en que el equipo de hello Azure AD puede iniciar sesión y conectarse a una instancia de aplicación de Azure AD tooyour con hello [marco de consentimiento de Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework). 
* Proporcionar el resto de instrucciones necesaria para hello Azure AD de equipo tootest inicio de sesión único con la aplicación. 
* Proporcionar información de hello siguiente:

> Nombre de la empresa:
> 
> Sitio web de la empresa:
> 
> Nombre de la aplicación:
> 
> Descripción de la aplicación (límite de 200 caracteres):
> 
> Sitio web de la aplicación (informativo):
> 
> Sitio web de soporte de técnico de la aplicación o información de contacto:
> 
> Id. de aplicación de la aplicación hello, como se muestra en los detalles de la aplicación hello en https://portal.azure.com:
> 
> Dirección URL de suscripción a la aplicación donde los clientes vaya toosign para y y/o aplicación hello de compra:
> 
> Elija la categoría de toothree para su toobe aplicación aparecen en (para categorías disponibles, vea hello Azure Active Directory Marketplace):
> 
> Adjunte un icono pequeño de la aplicación (archivo PNG, 45 px por 45 px, color de fondo sólido):
> 
> Adjunte un icono grande de la aplicación (archivo PNG, 215 px por 215 px, color de fondo sólido):
> 
> Adjunte el logotipo de la aplicación (archivo PNG, 150 px por 122 px, color de fondo transparente):
> 
> 

## <a name="saml-integration"></a>Integración SAML
Cualquier aplicación que admita SAML 2.0 puede integrarse directamente con un inquilino de Azure AD mediante [estos tooadd instrucciones una aplicación personalizada](../active-directory-saas-custom-apps.md). Una vez que haya probado que la integración de la aplicación funciona con Azure AD, enviar Hola siguiente información demasiado<mailto:waadpartners@microsoft.com>.

* Proporcione las credenciales para una cuenta o el inquilino de prueba con la aplicación que puede utilizarse en hello integración de Azure AD equipo tootest Hola.  
* Proporcionar Hola SAML Sign On URL, dirección URL del emisor (Id. de entidad), y los valores de dirección URL de respuesta (servicio de consumidor de aserción) para la aplicación, tal como se describe [aquí](../active-directory-saas-custom-apps.md). Si normalmente proporciona estos valores como parte de un archivo de metadatos SAML, envíelos también.
* Proporciona una breve descripción de cómo tooconfigure Azure AD como proveedor de identidades en su aplicación mediante SAML 2.0. Si la aplicación admite configurar Azure AD como proveedor de identidades a través de un portal de autoservicio administrativo, a continuación, asegúrese de las credenciales de hello proporcionadas anteriormente incluyen hello capacidad tooset este proceso.
* Proporcionar información de hello siguiente:

> Nombre de la empresa:
> 
> Sitio web de la empresa:
> 
> Nombre de la aplicación:
> 
> Descripción de la aplicación (límite de 200 caracteres):
> 
> Sitio web de la aplicación (informativo):
> 
> Sitio web de soporte de técnico de la aplicación o información de contacto:
> 
> Dirección URL de suscripción a la aplicación donde los clientes vaya toosign para y y/o aplicación hello de compra:
> 
> Elija las categorías de toothree para su toobe aplicación aparecen en (para categorías disponibles, vea hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):
> 
> Adjunte un icono pequeño de la aplicación (archivo PNG, 45 px por 45 px, color de fondo sólido):
> 
> Adjunte un icono grande de la aplicación (archivo PNG, 215 px por 215 px, color de fondo sólido):
> 
> Adjunte el logotipo de la aplicación (archivo PNG, 150 px por 122 px, color de fondo transparente):
> 
> 

