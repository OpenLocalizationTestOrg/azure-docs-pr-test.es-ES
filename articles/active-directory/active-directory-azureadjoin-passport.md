---
title: "aaaAuthenticating identidades sin contraseñas a través de Windows Hello para el negocio y Azure AD | Documentos de Microsoft"
description: "Proporciona una visión general de Windows Hello para empresas e información adicional sobre la implementación de Windows Hello para empresas."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>Autenticación de identidades sin contraseñas a través de Windows Hello para empresas
Hola métodos actual de autenticación con contraseñas por sí sola no son suficientes usuarios tookeep seguros. Los usuarios reutilizan y olvidan las contraseñas. Las contraseñas son breachable, phishable, toocracks propensas a y adivinar. También obtienen tooremember difícil y propensos tooattacks como "[pasar el hash de hello](https://technet.microsoft.com/dn785092.aspx)".

## <a name="about-windows-hello-for-business"></a>Acerca de Windows Hello para empresas
Windows Hello para empresas es un enfoque de autenticación basado en certificado o clave pública/privada dirigido a organizaciones y consumidores que no se limita a las contraseñas. Este tipo de autenticación se basa en las credenciales de par de claves que se pueden reemplazar las contraseñas y toobreaches son resistentes, robos y "phishing".

 Windows Hello para empresas permite al usuario autenticar la cuenta de Microsoft tooa, una cuenta de Windows Server Active Directory, una cuenta de Microsoft Azure Active Directory (Azure AD) o un servicio de terceros que admita la autenticación de rápido identidad en línea (BOBI). Después de una comprobación de dos pasos iniciales durante Windows Hello para la inscripción de negocio, Windows Hello para empresas se ha configurado en el dispositivo del usuario de Hola y usuario Hola establece un movimiento, que puede ser Windows Hello o un PIN. usuario de Hello proporciona Hola gesto tooverify su identidad. Windows, a continuación, usa Windows Hello para usuarios de empresa tooauthenticate hello y ayudarles a servicios y recursos de tooaccess protegidos.

clave privada de Hello debe ponerse a disposición únicamente a través de un gesto de usuario de"" como un PIN, biométrica o un dispositivo remoto como una tarjeta inteligente que Hola usuario utiliza toosign toohello dispositivo. Esta información es certificado tooa vinculado o un par de claves asimétrico. clave privada de Hello es hardware attested si el dispositivo de hello tiene un chip de módulo de plataforma segura (TPM). clave privada de Hello nunca abandona el dispositivo de Hola.

clave pública de Hola se registra con Azure Active Directory y Windows Server Active Directory (para local). Proveedores de identidades (IDPs) comprueba que el usuario de hello mediante clave pública de hello asignación de clave privada de hello usuario toohello y proporcionan información de inicio de sesión a través de un tiempo de contraseña (OTP), PhoneFactor o un mecanismo de notificación diferente.

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>¿Por qué las empresas deben adoptar Windows Hello para empresas?
Al habilitar Windows Hello para empresas, las empresas pueden proteger sus recursos aún mejor:

* Mediante la configuración de Windows Hello para empresas con una opción preferida de hardware. Esto significa que las claves se generarán en TPM 1.2 o TPM 2.0 cuando sea posible. Cuando TPM no está disponible, el software generará clave Hola.
* Definición de Hola de complejidad y la duración de hello ANCLAR y, si está habilitado el uso de Hello en su organización.
* Configurar Windows Hello para escenarios de tipo de tarjeta inteligente toosupport empresariales mediante basada en certificados de confianza.

## <a name="how-windows-hello-for-business-works"></a>Funcionamiento de Windows Hello para empresas
1. Las claves se generan en un hardware Hola TPM o el software. Muchos dispositivos tienen un chip TPM integrado que protege el hardware de hello mediante la integración de las claves de cifrado en dispositivos. TPM 1.2 o 2.0 de TPM genera claves o certificados que se crean a partir de las claves de hello generado.
2. Hola TPM da fe estas claves de hardware enlazado.
3. Un gesto de desbloqueo solo desbloquea el dispositivo de Hola. Este movimiento permite acceder a los recursos de toomultiple si Hola dispositivo está unido a un dominio Azure Unidos a AD.

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>Cómo funciona la hello Windows Hello para el ciclo de vida empresarial
![Ciclo de vida de Windows Hello para empresas](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

Hello diagrama anterior muestra par de claves pública/privada hello y validación de hello proveedor de identidades de Hola. Cada uno de estos pasos se explica con detalle a continuación:

1. Hola usuario demuestre su identidad a través de varios métodos integrados de corrección (gestos, las tarjetas inteligentes físicas, la autenticación multifactor) y envía este tooan información del proveedor de identidades (IDP) como Azure Active Directory o Active Directory local.
2. dispositivo Hello, a continuación, crea la clave de Hola, da fe clave Hola, toma parte pública de Hola de esta clave, asocia con instrucciones de estación, inicia sesión en y lo envía clave de hello tooregister toohello IDP.
3. Tan pronto como Hola IDP registra la parte pública de Hola de clave de hello, desafíos de IDP de Hola Hola toosign de dispositivo con la parte privada de Hola de clave de Hola.
4. Hola IDP, a continuación, valida y problemas Hola token de autenticación que permite a usuario de Hola y Hola dispositivo acceso a Hola protegida los recursos. IDPs puede escribir aplicaciones multiplataforma o usar toocreate de compatibilidad (a través de la API de JavaScript/Webcrypto) del explorador y usar Windows Hello para las credenciales de negocio para sus usuarios.

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>Hola requisitos de implementación de Windows Hello para empresas
### <a name="at-hello-enterprise-level"></a>En el nivel de empresa de Hola
* enterprise Hello tiene una suscripción de Azure.

### <a name="at-hello-user-level"></a>En el nivel de usuario de Hola
* equipo del usuario de Hola ejecuta Windows 10 Professional o Enterprise.

Para obtener instrucciones de implementación detallada, consulte [habilitar Windows Hello para empresas de organización de hello](active-directory-azureadjoin-passport-deployment.md).

## <a name="additional-information"></a>Información adicional
* [Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Conozca los escenarios de uso de Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuración de Azure AD Join](active-directory-azureadjoin-setup.md)

