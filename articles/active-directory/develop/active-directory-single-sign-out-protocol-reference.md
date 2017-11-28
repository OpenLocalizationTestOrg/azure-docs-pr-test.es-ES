---
title: "inicio de sesión único Out SAML protocolo aaaAzure | Documentos de Microsoft"
description: "Este artículo describe Hola único protocolo de SAML de cierre de sesión en Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Protocolo SAML de cierre de sesión único
Azure Active Directory (Azure AD) admite hello perfil de cierre de sesión único de SAML 2.0 web explorador. Toowork de cierre de sesión único correctamente, Hola **LogoutURL** para la aplicación hello se debe registrar explícitamente con Azure AD durante el registro de aplicación. Azure AD usa los usuarios de hello LogoutURL tooredirect después de cerrar sesión.

Este diagrama muestra el flujo de trabajo de hello del proceso de cierre de sesión único de hello Azure AD.

![Flujo de trabajo de cierre de sesión único](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
Hola servicio de nube envía un `LogoutRequest` tooindicate tooAzure AD de mensaje que ha finalizado una sesión. Hello extracto siguiente muestra un ejemplo `LogoutRequest` elemento.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
Hola `LogoutRequest` enviado tooAzure AD requiere Hola siguientes atributos:

* `ID`: Esto identifica la solicitud de cierre de sesión de Hola. Hola valo `ID` no debe empezar por un número. práctica habitual de Hello es tooappend **identificador** toohello representación de cadena de un GUID.
* `Version`: Establecer valor de Hola de este elemento demasiado**2.0**. Este valor es necesario.
* `IssueInstant` : es una cadena `DateTime` con un valor en hora universal coordinada (UTC) y un [formato de ida y vuelta ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD espera un valor de este tipo, pero no lo fuerza.

### Emisor
Hola `Issuer` elemento en un `LogoutRequest` debe coincidir exactamente con uno de hello **ServicePrincipalNames** Hola del servicio en nube de Azure AD. Normalmente, esto se establece toohello **App ID URI** que se especifica durante el registro de aplicación.

### NameID
Hola valo hello `NameID` elemento debe coincidir exactamente con hello `NameID` Hola usuario de que se está cerrando.

## LogoutResponse
Envíos de Azure AD una `LogoutResponse` en respuesta tooa `LogoutRequest` elemento. Hello extracto siguiente muestra un ejemplo `LogoutResponse`.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
Azure AD establece hello `ID`, `Version` y `IssueInstant` valores de hello `LogoutResponse` elemento. También establece hello `InResponseTo` toohello valor del elemento de hello `ID` atributo de hello `LogoutRequest` que provocó la respuesta de Hola.

### Emisor
Azure AD establece este valor demasiado`https://login.microsoftonline.com/<TenantIdGUID>/` donde <TenantIdGUID> es Hola identificador del inquilino del inquilino de hello Azure AD.

valor de hello tooevaluate de hello `Issuer` elemento, usar el valor de Hola de hello **App ID URI** proporcionado durante el registro de aplicación.

### Estado
Azure AD usa hello `StatusCode` elemento Hola `Status` elemento tooindicate Hola realizó o no cierre de sesión. Cuando intento de cierre de sesión de hello falla, hello `StatusCode` elemento también puede contener mensajes de error personalizados.
