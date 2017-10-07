---
title: "Azure AD Connect: uso de un proveedor de identidades de SAML 2.0 para el inicio de sesión único | Microsoft Docs"
description: "En este tema se describe el uso de un IdP compatible con SAML 2.0 para el inicio de sesión único."
services: active-directory
author: billmath
manager: femila
ms.custom: it-pro
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f9653dc44fb284a9b3c1988f623c33f27ae148cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a>Uso de un proveedor de identidades (IdP) de SAML 2.0 para el inicio de sesión único

Este tema contiene información sobre el uso de un SAML 2.0 perfil SP-Lite compatible según el proveedor de identidades como Hola preferido servicio de Token de seguridad (STS) / proveedor de identidades. Esta solución resulta útil si ya tiene un directorio de usuario y un almacén de contraseñas local a los que se puede acceder mediante SAML 2.0. Este directorio de usuarios existente se puede utilizar para inicio de sesión tooOffice 365 y otros recursos protegidos por AD de Azure. Hola SP-Lite de SAML 2.0 perfil se basa en hello ampliamente utilizado tooprovide estándar de identidad federada la lenguaje de marcado de aserción de seguridad (SAML) en un inicio de sesión y un marco de intercambio de atributos.

>[!NOTE]
>Para obtener una lista de parte 3ª Idps que se han probado para su uso con Azure AD vea hello [lista de compatibilidad de federación de AD de Azure](active-directory-aadconnect-federation-compatibility.md)

Microsoft admite esta experiencia de inicio de sesión como la integración de Hola de un servicio de nube de Microsoft, como Office 365, con su SAML 2.0 correctamente configurado IdP basada en el perfil. Proveedores de identidad SAML 2.0 son productos de terceros y, por tanto, Microsoft no ofrece soporte para la implementación de hello, configuración, solución de problemas de prácticas recomendadas relativas a ellos. Una vez configurado correctamente, integración de hello con hello SAML 2.0 proveedor de identidades se puede probar si una configuración correcta mediante el uso de hello herramienta de analizador de conectividad de Microsoft que se describe con más detalle a continuación. Para obtener más información acerca de su proveedor de identidad basado en perfil SP-Lite de SAML 2.0, pida organización Hola que lo proporcionó.

>[!IMPORTANT]
>Solo un conjunto limitado de clientes están disponibles en este escenario de inicio de sesión con proveedores de identidades de SAML 2.0, entre los que se incluyen:

>- Clientes basados en web como Outlook Web Access y SharePoint Online
- Los clientes de correo electrónico enriquecido que utilizan la autenticación básica y un método de acceso de Exchange admitido, como IMAP, POP, Active Sync, MAPI, etc. (Hola protocolo de cliente mejorado punto final es necesario toobe implementado), incluido:
    - Microsoft Outlook 2010, Outlook 2013, Outlook 2016, iPhone de Apple (distintas versiones de iOS)
    - Varios dispositivos de Android de Google
    - Windows Phone 7, Windows Phone 7.8 y Windows Phone 8.0
    - Cliente de correo de Windows 8 y Windows 8.1
    - Cliente de correo de Windows 10

Todos los demás clientes no están disponibles en este escenario de inicio de sesión con el proveedor de identidades de SAML 2.0. Por ejemplo, cliente de escritorio de hello Lync 2010 no es capaz de toologin en servicio de hello con tu proveedor de identidad SAML 2.0 configurado para el inicio de sesión único.

## <a name="azure-ad-saml-20-protocol-requirements"></a>Requisitos del protocolo SAML 2.0 de Azure AD
Este tema contiene los requisitos detallados en el protocolo de Hola y formato de mensajes que el proveedor de identidad SAML 2.0 debe implementar toofederate con Azure AD tooenable inicio de sesión tooone o más servicios de nube de Microsoft (por ejemplo, Office 365). usuario de confianza de Hello SAML 2.0 (SP-STS) para un servicio de nube de Microsoft utilizado en este escenario es Azure AD.

Se recomienda que se asegure de los mensajes de salida del proveedor de identidad pueden como toohello similar proporcionada seguimientos de ejemplo como sea posible de SAML 2.0. Además, usar los valores de atributo concreto de hello proporcionan metadatos de Azure AD siempre que sea posible. Una vez que esté satisfecho con los mensajes de salida, puede probar con hello analizador de conectividad de Microsoft tal y como se describe a continuación.

metadatos de Hello Azure AD se pueden descargar desde esta dirección URL: [https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml).
Para los clientes de China utilizando hello de la instancia específica de China de Office 365, debe usarse Hola después de punto de conexión de federación: [https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml).

## <a name="saml-protocol-requirements"></a>Requisitos del protocolo SAML
Esta sección detalla cómo son pares de mensajes de solicitud y respuesta Hola reunir en orden toohelp se tooformat los mensajes correctamente.

Azure AD puede ser toowork configurado con proveedores de identidad que utilizan perfil SP-Lite de SAML 2.0 Hola con algunos requisitos específicos, como se muestra a continuación. Utilizar Hola solicitud y respuesta mensajes de SAML junto con las pruebas manuales y automatizadas, puede trabajar tooachieve interoperabilidad con Azure AD.

## <a name="signature-block-requirements"></a>Requisitos del bloque de firma
Dentro de hello respuesta SAML nodo de firma de mensaje Hola contiene información sobre la firma digital de hello para el propio mensaje Hola. bloque de firma de Hello tiene Hola según los requisitos:

1. debe firmarse el propio nodo de aserción Hola
2.  algoritmo de RSA-sha1 Hola debe utilizarse como Hola DigestMethod. No se aceptan otros algoritmos de firma digital.
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  También puede firmar el documento XML de Hola. 
4.  Hola algoritmo Transform debe coincidir con los valores de hello en el siguiente ejemplo de Hola:`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`
9.  Hola algoritmo SignatureMethod debe coincidir con hello según muestra:`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`

## <a name="supported-bindings"></a>Enlaces admitidos
Los enlaces son transporte Hola relacionados con los parámetros de comunicación necesarias. Hola según los requisitos aplica toohello enlaces

1. HTTPS es el transporte de hello necesario.
2.  Azure AD necesitará HTTP POST para el envío del token durante el inicio de sesión.
3.  Azure AD utilizará HTTP POST para el proveedor de identidad de toohello de solicitud de autenticación de Hola y REDIRECCIÓN de proveedor de identidades de toohello de mensaje de cierre de sesión de Hola.

## <a name="required-attributes"></a>Atributos necesarios
Esta tabla muestra los requisitos para atributos específicos en el mensaje de bienvenida SAML 2.0.
 
|Atributo|Descripción|
| ----- | ----- |
|NameID|valor Hola de esta aserción debe ser Hola igual a ImmutableID del usuario de hello Azure AD. Puede ser una too64 caracteres alfanuméricos. Los caracteres seguros que no sean HTML deben estar codificados, por ejemplo, un carácter "+" se muestra como ".2B".|
|IDPEmail|Hello nombre Principal de usuario (UPN) aparece en hello SAML respuesta como un elemento con hello nombre IDPEmail este está UserPrincipalName (UPN del usuario de hello) en Azure AD/Office 365. Hola UPN está en formato de dirección de correo electrónico. Valor UPN en Windows Office 365 (Azure Active Directory).|
|Emisor|Se trata de toobe requiere un URI del proveedor de identidades de Hola. No debería volver a usar Hola emisor de mensajes de ejemplo de Hola. Si tiene varios dominios de nivel superior en su Hola de inquilinos de Azure AD debe coincidir con el emisor Hola especifica configuración de URI configurada por dominio.|

>[!IMPORTANT]
>Actualmente, Azure AD admite Hola sigue URI de formato de NameID para SAML 2.0:urn:oasis:names:tc:SAML:2.0:nameid-formato: persistente.

## <a name="sample-saml-request-and-response-messages"></a>Ejemplo de mensajes de solicitud y respuesta de SAML
Un par de mensajes de solicitud y respuesta se muestra para el intercambio de mensajes de inicio de sesión de Hola.
Se trata de un mensaje de solicitud de ejemplo que se envía desde el proveedor de identidad de Azure AD tooa ejemplo SAML 2.0. proveedor de identidad SAML 2.0 Hello es que los servicios de federación de Active Directory (AD FS) configurado toouse protocolo de SAML-P. Las pruebas de interoperabilidad también se han realizado con otros proveedores de identidades de SAML 2.0.

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

Se trata de un mensaje de respuesta de ejemplo que se envía desde Hola ejemplo SAML 2.0 identidad compatible con proveedor tooAzure AD / Office 365.

    `<samlp:Response ID="_592c022f-e85e-4d23-b55b-9141c95cd2a5" Version="2.0" IssueInstant="2014-01-31T15:36:31.357Z" Destination="https://login.microsoftonline.com/login.srf" Consent="urn:oasis:names:tc:SAML:2.0:consent:unspecified" InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
    </samlp:Status>
    <Assertion ID="_7e3c1bcd-f180-4f78-83e1-7680920793aa" IssueInstant="2014-01-31T15:36:31.279Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
        <ds:Reference URI="#_7e3c1bcd-f180-4f78-83e1-7680920793aa">
          <ds:Transforms>
            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
          </ds:Transforms>
          <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
          <ds:DigestValue>CBn/5YqbheaJP425c0pHva9PhNY=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
      <ds:SignatureValue>TciWMyHW2ZODrh/2xrvp5ggmcHBFEd9vrp6DYXp+hZWJzmXMmzwmwS8KNRJKy8H7XqBsdELA1Msqi8I3TmWdnoIRfM/ZAyUppo8suMu6Zw+boE32hoQRnX9EWN/f0vH6zA/YKTzrjca6JQ8gAV1ErwvRWDpyMcwdYCiWALv9ScbkAcebOE1s1JctZ5RBXggdZWrYi72X+I4i6WgyZcIGai/rZ4v2otoWAEHS0y1yh1qT7NDPpl/McDaTGkNU6C+8VfjD78DrUXEcAfKvPgKlKrOMZnD1lCGsViimGY+LSuIdY45MLmyaa5UT4KWph6dA==</ds:SignatureValue>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <ds:X509Data>
          <ds:X509Certificate>MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyhBREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDTE1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9ybWVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/+3ZWxd9T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEMb2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvyJOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBySx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==</ds:X509Certificate>
        </ds:X509Data>
      </KeyInfo>
    </ds:Signature>
    <Subject>
      <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">ABCDEG1234567890</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" NotOnOrAfter="2014-01-31T15:41:31.357Z" Recipient="https://login.microsoftonline.com/login.srf" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2014-01-31T15:36:31.263Z" NotOnOrAfter="2014-01-31T16:36:31.263Z">
      <AudienceRestriction>
        <Audience>urn:federation:MicrosoftOnline</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="IDPEmail">
        <AttributeValue>administrator@contoso.com</AttributeValue>
      </Attribute>
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2014-01-31T15:36:30.200Z" SessionIndex="_7e3c1bcd-f180-4f78-83e1-7680920793aa">
      <AuthnContext>
        <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
    </Assertion>
    </samlp:Response>`

## <a name="configure-your-saml-20-compliant-identity-provider"></a>Configuración del proveedor de identidades compatible con SAML 2.0
Este tema contiene orientación sobre cómo tooconfigure su toofederate de proveedor de identidad SAML 2.0 con tooone de acceso de inicio de sesión único de Azure AD tooenable o una nube de Microsoft más servicios (por ejemplo, Office 365) mediante el protocolo de hello SAML 2.0. Hello SAML 2.0 usuario para un servicio de nube de Microsoft utilizado en este escenario de confianza es Azure AD.

## <a name="add-azure-ad-metadata"></a>Adición de metadatos de Azure AD
El proveedor de identidad SAML 2.0 debe tooadhere tooinformation sobre el usuario de confianza de hello Azure AD. Azure AD publica los metadatos en https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml.

Se recomienda que siempre importar metadatos de hello más reciente Azure AD al configurar el proveedor de identidad SAML 2.0. Tenga en cuenta que Azure AD no lee los metadatos del proveedor de identidades de Hola.

## <a name="add-azure-ad-as-a-relying-party"></a>Adición de Azure AD como usuario de confianza
Tener tooenable comunicación entre el proveedor de identidad SAML 2.0 y Azure AD. Esta configuración será depende de su proveedor de identidad específica y se debe hacer referencia toodocumentation para él. Normalmente, configuraría hello toohello de Id. de entidad confianza igual que entityID Hola de metadatos de hello Azure AD.

>[!NOTE]
>Compruebe reloj hello en el servidor de proveedor de identidad SAML 2.0 es el origen de hora preciso tooan sincronizada. Un tiempo de reloj correcta puede provocar toofail de inicios de sesión federado.

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a>Instalación de Windows PowerShell para el inicio de sesión con el proveedor de identidades de SAML 2.0
Después de haber configurado el proveedor de identidad SAML 2.0 para utilizarlo con inicio de sesión en Azure AD, Hola siguiente paso es toodownload e instalación hello Azure módulo Active Directory para Windows PowerShell. Una vez instalado, usará estos cmdlets tooconfigure los dominios de Azure AD como dominios federados.

Hello Azure módulo Active Directory para Windows PowerShell es una descarga para administrar los datos de su organización en Azure AD. Este módulo instala un conjunto de cmdlets tooWindows PowerShell; ejecutar esos tooset de cmdlets de acceso de inicio de sesión único tooAzure AD y a su vez tooall de hello servicios en la nube que está suscrito. Para obtener instrucciones acerca de cómo toodownload e instalar Hola cmdlets, consulte [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a>Configuración de una relación de confianza entre el proveedor de identidades de SAML y Azure AD
Antes de configurar la federación en un dominio de Azure AD, debe tener configurado un dominio personalizado. No se puede federar el dominio predeterminado de hello proporcionada por Microsoft. dominio predeterminado de Hola de Microsoft termina con "onmicrosoft.com".
Se ejecuta una serie de cmdlets en tooadd de interfaz de línea de comandos de Windows PowerShell de Hola o convertir dominios para el inicio de sesión único.

Cada dominio de Active Directory de Azure que desee toofederate con el proveedor de identidad SAML 2.0 o bien debe agregarse como un dominio de inicio de sesión único o toobe convertido un dominio de inicio de sesión único de un dominio estándar. El hecho de agregar o convertir un dominio establece una relación de confianza entre el proveedor de identidades de SAML 2.0 y Azure AD.

Hello siguiente procedimiento explica cómo convertir un dominio federado existente del tooa de dominio estándar con SP-Lite de SAML 2.0. Tenga en cuenta que el dominio puede sufrir una interrupción del sistema que afecta a los usuarios too2 horas después de realizar este paso.

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a>Configuración de un dominio en Azure AD Directory para federación


1. Conectar tooyour directorio de Azure AD como un administrador de inquilinos: MsolService conectarse.
2.  Configurar la federación deseada de toouse de dominio de Office 365 con SAML 2.0:`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol` 

3.  Puede obtener Hola cadena base64 del certificado desde el archivo de metadatos de IDP de firma. Aunque se ha proporcionado un ejemplo de esta ubicación, puede ser algo diferente dependiendo de su implementación.

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

Para más información sobre "Set-MsolDomainAuthentication", consulte: [http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx).

>[!NOTE]
>Debe ejecutar "$ecpUrl = “https://WS2012R2-0.contoso.com/PAOS“” solo si ha configurado una extensión ECP para el proveedor de identidades. Los clientes de Exchange Online, excepto Outlook Web Application (OWA), dependen de un punto de conexión activo basado en POST. Si tu STS SAML 2.0 implementa implementación ECP de un tooShibboleth similar de extremo activo un extremo activo es posible que estos toointeract clientes enriquecidos con hello servicio Exchange Online.

Una vez que se ha configurado la federación puede cambiar hacia atrás demasiado "no federado" (o "administrado"), sin embargo, este cambio ocupa tootwo horas toocomplete y requiere asignar nuevas contraseñas aleatorias de la nube en función de usuario de inicio de sesión tooeach. Volver demasiado "administrado" puede ser necesario en algunos escenarios tooreset un error en la configuración. Para más información sobre la conversión de dominios, consulte: [http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx).

## <a name="provision-user-principals-tooazure-ad--office-365"></a>Aprovisionar entidades de seguridad de usuario tooAzure AD / Office 365
Antes de poder autenticar su tooOffice usuarios 365 debe aprovisionar Azure AD con entidades de seguridad que corresponden toohello aserción SAML 2.0 Hola de notificación de usuario. Si estas entidades de seguridad de usuario no se conocen de antemano tooAzure AD no se utilizar para el inicio de sesión federado. Azure AD Connect o Windows PowerShell puede ser tooprovision usa entidades de seguridad de usuario.

Azure AD Connect puede ser tooprovision usa entidades de seguridad tooyour dominios en el directorio de AD de Azure de hello Active Directory local. Para más información, consulte [Integrate your on-premises directories with Azure Active Directory](active-directory-aadconnect.md) (Integración de los directorios locales con Azure Active Directory).

Windows PowerShell también pueden ser utilizado tooautomate agregar nuevos usuarios tooAzure AD y toosynchronize cambia de directorio local de Hola. Hola toouse cmdlets de Windows PowerShell, debe descargar hello [módulos de Azure Active Directory](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0).

Este procedimiento muestra cómo tooadd una tooAzure AD de usuario único.


1. Conectar tooyour directorio de Azure AD como un administrador de inquilinos: MsolService conectarse.
2.  Cree una nueva entidad de seguridad de usuario: ` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
        -ImmutableId ABCDEFG1234567890
        -DisplayName "Elwood Folk"
        -FirstName Elwood 
        -LastName Folk 
        -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
        -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
        -UsageLocation "US" `. 

Para más información sobre "New-MsolUser", consulte [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx).

>[!NOTE]
>Hola valor debe coincidir con el valor de Hola que enviarás para "IDPEmail" en la notificación de SAML 2.0 y "ImmutableID" valor debe coincidir con el valor de hello enviado en la aserción "NameID" hello "UserPrinciplName".

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a>Comprobación del inicio de sesión único con el IDP SAML 2.0
Como administrador de hello, antes de comprobar y administrar el inicio de sesión único (también denominado federación de identidades), revise la información de Hola y realice los pasos de hello en hello siguiendo artículos tooset el inicio de sesión único con el proveedor de identidad basado en SP-Lite de SAML 2.0:


1.  Revisar Hola requisitos del protocolo SAML 2.0 de Azure AD
2.  Ha configurado el proveedor de identidades de SAML 2.0.
3.  Instale Windows PowerShell para el inicio de sesión único con el proveedor de identidades de SAML 2.0.
4.  Configure una relación de confianza entre el proveedor de identidades de SAML 2.0 y Azure AD.
5.  Aprovisionar un usuario de prueba conocida principal tooAzure Active Directory (Office 365) mediante Windows PowerShell o Azure AD Connect.
6.  Configure la sincronización de directorios con [Azure AD Connect](active-directory-aadconnect.md).

Después de configurar el inicio de sesión único con el proveedor de identidades basado en SP-Lite de SAML 2.0, debe comprobar que funciona correctamente.

>[!NOTE]
>Si convierte un dominio, en lugar de agregar uno, puede llevar hasta too24 horas tooset el inicio de sesión único.
Antes de comprobar el inicio de sesión único, debe finalizar la configuración de la sincronización de Active Directory, sincronizar los directorios y activar los usuarios sincronizados.

### <a name="use-hello-tool-tooverify-that-single-sign-on-has-been-set-up-correctly"></a>Use Hola herramienta tooverify que inicio de sesión único se ha configurado correctamente
tooverify ese inicio de sesión único se ha configurado correctamente, puede realizar Hola después tooconfirm de procedimiento que es capaz de toosign toohello del servicio en nube con sus credenciales corporativas.

Microsoft ha proporcionado una herramienta que puede usar tootest su SAML 2.0 según el proveedor de identidades. Antes de ejecutar Hola probar herramienta debe haber configurado un toofederate del inquilino de Azure AD con el proveedor de identidad.

>[!NOTE]
>Hola analizador de conectividad requiere Internet Explorer 10 o posterior.



1. Descarga Hola analizador de conectividad de [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client).
2.  Haga clic en instalar ahora toobegin descarga e instalación de la herramienta de Hola.
3.  Seleccione “I can’t set up federation with Office 365, Azure, or other services that use Azure Active Directory” (No se puede configurar la federación con Office 365, Azure u otros servicios que usan Azure Active Directory).
4.  Una vez que se descarga la herramienta de Hola y en ejecución, verá ventana de diagnóstico de conectividad de Hola. herramienta de Hello recorre paso a paso a través de probar la conexión de federación.
5.  Hola analizador de conectividad se abra el IDP SAML 2.0 para toologon, escriba las credenciales de Hola de principal de usuario de Hola se prueban por: ![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)
6.  Al Hola federación probar el inicio de sesión en la ventana, que debe especificar un nombre de cuenta y una contraseña para el inquilino de Azure AD de Hola que está configurado toobe federada con el proveedor de identidad SAML 2.0. herramienta de Hello intentará en toosign con esas credenciales y resultados detallados de las pruebas realizadas durante el intento de inicio de sesión de Hola se proporcionará como salida.
![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)
7. En esta ventana se muestra un resultado erróneo de las pruebas. Al hacer clic en Revisar resultados detallados mostrarán información sobre los resultados de Hola para cada prueba que se realizó. También puede guardar Hola resultados toodisk en orden tooshare ellos.
 
>[!NOTE]
>Hello analizador de conectividad también prueba la federación activa con hello WS *-protocolos ECP/PAOS y basados en. Si no utilizas estos, puede omitir Hola siguiente error: pruebas Hola flujo de inicio de sesión activa con el punto de conexión de su proveedor de identidades federación de Active.

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a>Comprobación manual de que el inicio de sesión único se ha configurado correctamente
Comprobación manual proporciona pasos adicionales que puede llevar a cabo tooensure que el proveedor de identidad SAML 2.0 funciona correctamente en muchos escenarios.
tooverify que inicio de sesión único se ha configurado correctamente, haga Hola siguiente pasos:


1. En un equipo unido a un dominio, inicie sesión en el servicio en la nube tooyour con el mismo nombre que se utiliza para las credenciales corporativas de inicio de sesión de Hola.
2.  Haga clic dentro del cuadro de contraseña de Hola. Si el inicio de sesión único está configurado, cuadro de contraseña de Hola se sombreará y verá el siguiente mensaje de Hola: "ya está toosign necesario en <your company>."
3.  Haga clic en hello iniciar sesión en <your company> vínculo. Si es capaz de toosign en, a continuación, el inicio de sesión único se configuró.

## <a name="next-steps"></a>Pasos siguientes


- [Servicios de federación de Active Directory y personalización con Azure AD Connect](active-directory-aadconnect-federation-management.md)
- [Lista de compatibilidad de federación de AD Azure](active-directory-aadconnect-federation-compatibility.md)
- [Instalación personalizada de Azure AD Connect](active-directory-aadconnect-get-started-custom.md)
