---
title: Azure AD SSPR data requirements (Requisitos de datos de SSPR de Azure AD) | Microsoft Docs
description: "Restablecer requisitos de datos para la contraseña de autoservicio de Azure AD y cómo toosatisfy ellos"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>Implementación del restablecimiento de contraseña sin necesidad de registro del usuario final

La implementación de restablecimiento de contraseña de autoservicio (SSPR) requiere autenticación datos toobe presente. Algunas organizaciones tienen sus usuarios escribir sus datos de autenticación por sí mismos, pero muchas organizaciones prefieren toosynchronize con los datos existentes en Active Directory. Si con el formato correcto datos en el directorio local y configura [Azure AD Connect con configuración rápida](./connect/active-directory-aadconnect-get-started-express.md), que los datos se hacen disponible tooAzure AD y SSPR con requiere ninguna interacción del usuario.

Cualquier número de teléfono debe estar en formato de hello + CountryCode PhoneNumber ejemplo: + 1 4255551234 toowork correctamente.

> [!NOTE]
> El restablecimiento de contraseña no admite extensiones telefónicas. Incluso en formato de hello 4255551234 + 1 X 12345, las extensiones se quitan antes de que se realiza la llamada de Hola.

## <a name="fields-populated"></a>Campos rellenos

Si usa la configuración de predeterminada Hola Hola de Azure AD Connect después de cada asignación se realiza.

| AD local | Azure AD | Información de contacto de Autenticación de Azure AD |
| --- | --- | --- |
| telephoneNumber | Teléfono del trabajo | Teléfono alternativo |
| mobile | Teléfono móvil | Teléfono |


## <a name="security-questions-and-answers"></a>Preguntas y respuestas de seguridad

Preguntas de seguridad y respuestas se almacenan de forma segura en su inquilino de Azure AD y son solo toousers accesible a través de hello [portal de registro](https://aka.ms/ssprsetup). Los administradores no se vea o modifique contenido Hola de otro preguntas de los usuarios y respuestas.

### <a name="what-happens-when-a-user-registers"></a>Qué ocurre cuando se registra un usuario

Cuando un usuario se registra, página de registro de hello establece Hola siguientes campos:

* Teléfono de autenticación
* Correo electrónico de autenticación
* Preguntas y respuestas de seguridad

Si ha proporcionado un valor para **teléfono móvil** o **correo electrónico alternativa**, los usuarios pueden usar inmediatamente los valores tooreset sus contraseñas, aunque no se haya registrado para el servicio de Hola. Además, los usuarios ver esos valores al registrarse para hello primera vez y modificarlos si lo desean. Después de que se registren correctamente, estos valores se conservarán en hello **teléfono de autenticación** y **correo electrónico de autenticación** campos, respectivamente.

## <a name="set-and-read-authentication-data-using-powershell"></a>Establecimiento y lectura de datos de autenticación mediante PowerShell

Hola después campos puede establecerse utilizando PowerShell

* Correo electrónico alternativo
* Teléfono móvil
* Teléfono del trabajo: solo puede establecerse si no se sincroniza un directorio local

### <a name="using-powershell-v1"></a>Uso de PowerShell V1

tooget iniciado, necesita demasiado[descargar e instalar el módulo de PowerShell de Azure AD de hello](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule). Una vez que se ha instalado, puede seguir los pasos de Hola que siguen tooconfigure cada campo.

#### <a name="set-authentication-data-with-powershell-v1"></a>Establecimiento de datos de autenticación con PowerShell V1

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a>Lectura de datos de autenticación con PowerShell V1

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a>Teléfono de autenticación y correo electrónico de autenticación sólo se pueden leer utilizando Powershell V1 utilizando Hola comandos que siguen

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>Uso de PowerShell V2

tooget iniciado, necesita demasiado[descargar e instalar el módulo de PowerShell de Azure AD V2 hello](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md). Una vez que se ha instalado, puede seguir los pasos de Hola que siguen tooconfigure cada campo.

tooinstall rápidamente desde las versiones recientes de PowerShell que admiten Install-Module, ejecute estos comandos (primera línea de hello simplemente comprueba toosee si se encuentra ya instalada):

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a>Establecimiento de datos de autenticación con PowerShell V2

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a>Lectura de datos de autenticación con PowerShell V2

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a>Pasos siguientes

Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD 
* [**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD
* [**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.
* [**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas
* [**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.
* [**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona
* [**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo? ¿Por qué? ¿Qué? ¿Dónde? ¿Quién? ¿Cuándo? -Responde tooquestions siempre deseara tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR
