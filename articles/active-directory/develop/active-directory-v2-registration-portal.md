---
title: Temas de Ayuda del Portal de registro de aaaApp | Documentos de Microsoft
description: "Una descripción de las diversas características de portal de registro de aplicación de Microsoft de Hola."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: f0507c28-9464-4d3e-bd53-de9053fd5278
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/16/2016
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: 3eb17b629577446a336152799497e7d980fb825d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="app-registration-reference"></a>Referencia del registro de aplicaciones
Este documento proporciona el contexto y las descripciones de varias características que se encuentran en hello Portal de registro de aplicación de Microsoft [https://apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).

## <a name="my-applications"></a>Mis aplicaciones
Esta lista contiene todas las aplicaciones que se registra para su uso con el punto de conexión de hello Azure AD v2.0.  Estas aplicaciones tengan toosign de capacidad de hello en los usuarios con ambas cuentas personales de la cuenta de Microsoft y cuentas de trabajo o escuela de Azure Active Directory.  toolearn más información acerca del punto de conexión de v2.0 hello Azure AD, consulte nuestro [v2.0 información general sobre](active-directory-appmodel-v2-overview.md).  Estas aplicaciones también pueden ser toointegrate usado con el extremo de autenticación de cuenta de Microsoft hello, `https://login.live.com`.

## <a name="live-sdk-applications"></a>Aplicaciones de SDK de Live
Esta lista contiene todas las aplicaciones registradas para su uso únicamente con la cuenta Microsoft.  No están habilitadas en absoluto para su uso con Azure Active Directory.  Esto es donde se pueden buscar todas las aplicaciones que tenían que previamente se ha registrado con el portal para desarrolladores de MSA hello en `https://account.live.com/developers/applications`.  Todas las funciones que realizaba anteriormente en `https://account.live.com/developers/applications` ahora se pueden realizar en este nuevo portal, `https://apps.dev.microsoft.com`.  Si tiene alguna pregunta acerca de las aplicaciones de la cuenta Microsoft, póngase en contacto con nosotros.

## <a name="application-secrets"></a>Secretos de aplicación
Los secretos de aplicación son credenciales que permitan su tooperform aplicación confiable [autenticación de cliente](http://tools.ietf.org/html/rfc6749#section-2.3) con Azure AD.  En OAuth y OpenID Connect, los secretos de aplicación es tooas habitualmente que se hace referencia una `client_secret`.  En el protocolo de hello v2.0, cualquier aplicación que recibe un token de seguridad en una ubicación direccionable de web (mediante un `https` esquema) debe utilizar un tooidentify secreto de aplicación propio tooAzure AD al canje de ese token de seguridad.  Además, cualquier cliente nativo que recibe los tokens en un dispositivo se prohibirá utilizando una autenticación de cliente tooperform secreto de aplicación, toodiscourage Hola almacenamiento de secretos en entornos inseguros.

Cada aplicación puede contener dos secretos de aplicación válidos en un momento determinado.  Al mantener dos secretos, tendrá sustitución de claves periódica hello ablilty tooperform en todo entorno de la aplicación.  Cuando haya migrado toda Hola el secreto nuevo tooa de aplicación, puede eliminar secreto antiguo hello y aprovisionar una nueva.

En este momento, se permiten solo dos tipos de secretos de la aplicación de portal de registro de aplicación Hola.  Elegir **generar nueva contraseña** generará y almacenar un secreto compartido en el almacén de datos respectivas de hello, que puede usar en la aplicación.  Elegir **generar nuevo par de claves** creará un nuevo par de claves pública y privada que se pueden descargar y usar para la autenticación de cliente tooAzure AD.

## <a name="profile"></a>Perfil
sección de perfil de Hola de portal de registro de aplicación Hola puede ser usada de inicio de sesión de toocustomize hello en la página para la aplicación.  En este momento puede modificar el inicio de sesión de hello en el logotipo de la aplicación de la página, las condiciones de la dirección URL del servicio y la declaración de privacidad.  Hello logotipo debe ser una imagen transparente de píxel de 48 x 48 o 50 x 50 en un archivo GIF, PNG o JPEG 15 KB o más pequeños.  Intente cambiar valores de Hola y Hola de visualización resultante de la página de inicio de sesión.

## <a name="live-sdk-support"></a>Compatibilidad con SDK de Live
Cuando se habilita "SDK de Live Support", se almacena cualquier aplicación secretos que cree se aprovisionará en hello Azure AD y datos de Microsoft Account.  Esto permitirá que su toointegrate aplicación directamente con hello servicio Account de Microsoft (login.live.com).  Si desea toobuild una aplicación con Microsoft Account directamente (como lugar toousing punto de conexión de v2.0 de hello Azure AD), debe asegurarse de que está habilitada la compatibilidad del SDK de Live.

Deshabilitar la compatibilidad con SDK de Live garantizará que ese secreto de aplicación Hola sólo se escribe en el almacén de datos de hello Azure AD.  almacén de datos de Azure AD Hola incorpora las normas de nivel empresarial que permiten toomeet ciertos estándares, como el cumplimiento de FISMA.  Si habilita la compatibilidad con el SDK de Live, es posible que la aplicación no pueda lograr el cumplimiento con algunas de estos regulaciones.

Si tiene previsto siempre extremo v2.0 de toouse hello Azure AD, puede deshabilitar con seguridad soporte técnico del SDK de Live.

