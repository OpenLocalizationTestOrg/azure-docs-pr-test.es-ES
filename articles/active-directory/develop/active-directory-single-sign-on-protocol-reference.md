---
title: "inicio de sesión único en SAML protocolo aaaAzure | Documentos de Microsoft"
description: "Este artículo describe el protocolo de inicio de sesión único en SAML de hello en Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Protocolo SAML de inicio de sesión único
Este artículo tratan las solicitudes de autenticación de hello SAML 2.0 y las respuestas que admite Azure Active Directory (Azure AD) para el inicio de sesión único.

diagrama de protocolo de Hello siguiente describe la secuencia de inicio de sesión único de Hola. servicio de nube (proveedor de servicios de hello) Hello usa un toopass de enlace de redirección HTTP un `AuthnRequest` tooAzure de elemento (solicitud de autenticación) AD (proveedor de identidades de hello). Azure AD, a continuación, usa un toopost de enlace de HTTP post un `Response` servicio de nube de toohello de elemento.

![Flujo de trabajo de inicio de sesión único](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
servicios en la nube de toorequest una autenticación de usuario, envían un `AuthnRequest` elemento tooAzure AD. Un elemento `AuthnRequest` de SAML 2.0 podría tener este aspecto:

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| Parámetro |  | Description |
| --- | --- | --- |
| ID |requerido |Azure AD usa este hello toopopulate de atributo `InResponseTo` atributo de hello devolvió una respuesta. Identificador no debe empezar por un número, por lo que una estrategia habitual es tooprepend una cadena como "id" toohello representación de cadena de un GUID. Por ejemplo, `id6c1c178c166d486687be4aaf5e482730` es un id. válido. |
| Versión |requerido |Debe ser **2.0**. |
| IssueInstant |requerido |Se trata de una cadena DateTime con un valor de hora UTC y un [formato de tiempo de ida y vuelta ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD espera un valor de fecha y hora de este tipo, pero no evaluar o usar el valor de Hola. |
| AssertionConsumerServiceUrl |opcional |Si se proporciona, debe coincidir con hello `RedirectUri` del servicio de nube de hello en Azure AD. |
| ForceAuthn |opcional | Se trata de un elemento booleano. Si es true, esto significa que el usuario Hola serán toore forzada-autenticar, incluso si tienen una sesión válida con Azure AD. |
| IsPassive |opcional |Se trata de un valor booleano que especifica si Azure AD debe autenticar usuario hello en modo silencioso, sin interacción del usuario, con la cookie de sesión de hello si existe una. Si es true, Azure AD tratará de usuario de hello tooauthenticate con la cookie de sesión de Hola. |

Todos los demás atributos `AuthnRequest` , como Consent, Destination, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex y ProviderName, se **omiten**.

Azure AD también omite hello `Conditions` elemento `AuthnRequest`.

### Emisor
Hola `Issuer` elemento en un `AuthnRequest` debe coincidir exactamente con uno de hello **ServicePrincipalNames** Hola del servicio en nube de Azure AD. Normalmente, esto se establece toohello **App ID URI** que se especifica durante el registro de aplicación.

Un extracto SAML de ejemplo que contiene hello `Issuer` elemento tiene el siguiente aspecto:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
Este elemento solicita un formato de Id. de nombre determinado en la respuesta de Hola y es opcional en `AuthnRequest` tooAzure elementos que envía AD.

Un elemento `NameIdPolicy` de ejemplo tiene el siguiente aspecto:

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

Si se proporciona `NameIDPolicy`, puede incluir su atributo `Format` opcional. Hola `Format` atributo puede tener solo una de hello siguientes valores; cualquier otro valor produce un error.

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Azure Active Directory emite la notificación de hello NameID como identificador en pares.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Azure Active Directory emite la notificación NameID de hello en formato de dirección de correo electrónico.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: Este valor permite el formato de notificación de Azure Active Directory tooselect Hola. Azure Active Directory emite Hola NameID como identificador en pares.
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Azure Active Directory emite la notificación NameID de Hola como un valor generado aleatoriamente que es único toohello operación de SSO actual. Esto significa que el valor de hello es temporal y no puede ser tooidentify usado Hola autenticar usuario.

Azure AD omite hello `AllowCreate` atributo.

### RequestAuthnContext
Hola `RequestedAuthnContext` elemento especifica los métodos de autenticación de hello deseado. Es opcional en `AuthnRequest` tooAzure elementos que envía AD. Azure AD admite solo un valor `AuthnContextClassRef`: `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.

### Ámbito
Hola `Scoping` es opcional en el elemento, que incluye una lista de proveedores de identidades, `AuthnRequest` tooAzure de elementos que envía AD.

Si se proporciona, no incluya hello `ProxyCount` atributo, `IDPListOption` o `RequesterID` elemento, que no se admiten.

### Firma
No incluya un elemento `Signature` en los elementos `AuthnRequest`, ya que Azure AD no es compatible con la firma de solicitudes de autenticación.

### Asunto
Azure AD omite hello `Subject` elemento de `AuthnRequest` elementos.

## Response
Cuando un inicio de sesión solicitado se completa correctamente, Azure AD publica un servicio de nube de toohello de respuesta. Un ejemplo respuesta tooa intento correcto de inicio de sesión tiene el siguiente aspecto:

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### Response
Hola `Response` elemento incluye el resultado de hello de solicitud de autorización de Hola. Azure AD establece hello `ID`, `Version` y `IssueInstant` valores de hello `Response` elemento. También establece Hola siguientes atributos:

* `Destination`: Al inicio de sesión se completa correctamente, esto se establece toohello `RedirectUri` Hola proveedor de servicios (servicio de nube).
* `InResponseTo`: Se establece toohello `ID` atributo de hello `AuthnRequest` elemento que inició la respuesta de Hola.

### Emisor
Azure AD establece hello `Issuer` elemento demasiado`https://login.microsoftonline.com/<TenantIDGUID>/` donde <TenantIDGUID> es Hola identificador del inquilino del inquilino de hello Azure AD.

Por ejemplo, una respuesta de ejemplo con el elemento Issuer podría ser similar a la siguiente:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### Estado
Hola `Status` elemento transmite Hola éxito o fracaso del inicio de sesión. Incluye hello `StatusCode` elemento, que contiene un código o un conjunto de códigos anidados que representan el estado de saludo de solicitud de Hola. También incluye hello `StatusMessage` elemento, que contiene mensajes de error personalizados que se generan durante el proceso de inicio de sesión de Hola.

<!-- TODO: Add a authentication protocol error reference -->

Hola aquí te mostramos un SAML respuesta tooan sesión intento fallido.

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### Aserción
En suma toohello `ID`, `IssueInstant` y `Version`, Azure AD establece Hola siguientes elementos de hello `Assertion` elemento de respuesta de Hola.

#### Emisor
Esto se establece demasiado`https://sts.windows.net/<TenantIDGUID>/`donde <TenantIDGUID> es hello identificador del inquilino de hello Azure AD.

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### Firma
Azure AD firma la aserción de Hola en respuesta tooa correcta-inicio de sesión. Hola `Signature` elemento contiene una firma digital que puede usar servicio de nube de hello integridad tooauthenticate Hola origen tooverify Hola de aserción de Hola.

toogenerate usa esta firma digital, Azure AD Hola clave de firma en hello `IDPSSODescriptor` elemento de su documento de metadatos.

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### Asunto
Esto especifica a entidad Hola asunto Hola de instrucciones de hello en aserción Hola. Contiene un `NameID` elemento, que representa el usuario autenticado Hola. Hola `NameID` valor es un identificador que es el proveedor de servicios de directed toohello solo es público de hello para el token de Hola. Es persistente; es decir se puede revocar, pero nunca volver a asignar. También es opaco, ya que no revela nada sobre el usuario de hello y no se puede usar como un identificador para las consultas de atributo.

Hola `Method` atributo de hello `SubjectConfirmation` elemento siempre se establece demasiado`urn:oasis:names:tc:SAML:2.0:cm:bearer`.

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### Condiciones
Este elemento especifica las condiciones que definen Hola aceptable usan de aserciones de SAML.

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

Hola `NotBefore` y `NotOnOrAfter` atributos especifican el intervalo de saludo durante qué Hola aserción sea válida.

* Hola valo hello `NotBefore` atributo es igual tooor ligeramente (menos de un segundo) a más tardar el valor de Hola de `IssueInstant` atributo de hello `Assertion` elemento. Azure AD no tiene en cuenta ninguna diferencia horaria entre él y hello (proveedor de servicios) de servicio en la nube y no agrega ningún tiempo de toothis de búfer.
* Hola valo hello `NotOnOrAfter` atributo es 70 minutos posterior al valor de Hola Hola de `NotBefore` atributo.

#### Público
Contiene un URI que identifica una audiencia prevista. Azure AD establece el valor de hello toohello de este elemento de `Issuer` elemento de hello `AuthnRequest` que inician sesión Hola. Hola tooevaluate `Audience` valor, utilice el valor de Hola de hello `App ID URI` que se especificó durante el registro de aplicación.

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

Al igual que hello `Issuer` valor, hello `Audience` valor debe coincidir exactamente con uno de los nombres principales de hello servicio que representa el servicio de nube de hello en Azure AD. Sin embargo, si hello valor de hello `Issuer` elemento no es un valor URI, hello `Audience` valor de respuesta de hello es hello `Issuer` valor prefijado con `spn:`.

#### AttributeStatement
Contiene notificaciones sobre el sujeto de Hola o el usuario. Hello extracto siguiente contiene un ejemplo `AttributeStatement` elemento. puntos suspensivos de Hello indican que ese elemento Hola puede incluir varios atributos y valores de atributo.

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **Nombre de la notificación** : Hola valo hello `Name` atributo (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) es el nombre principal de usuario de saludo del usuario autenticado de hello, como `testuser@managedtenant.com`.
* **Notificación de ObjectIdentifier** : Hola valo hello `ObjectIdentifier` atributo (`http://schemas.microsoft.com/identity/claims/objectidentifier`) es hello `ObjectId` Hola objeto de directorio que representa Hola usuario autenticado en Azure AD. `ObjectId`es inmutable, globalmente único y volver a usar identificador seguro para la ejecución del programa Hola autentica el usuario.

#### AuthnStatement
Este elemento valida que ese asunto de aserción Hola autenticó un significado determinado en un momento determinado.

* Hola `AuthnInstant` atributo especifica la hora de hello en qué usuario Hola autenticado con Azure AD.
* Hola `AuthnContext` elemento especifica el contexto de autenticación de hello usa usuario de hello tooauthenticate.

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```