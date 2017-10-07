---
title: 'Directiva: SSPR de Azure AD | Microsoft Docs'
description: "Opciones de directiva de autoservicio de restablecimiento de contraseña de Azure AD"
services: active-directory
keywords: "Administración de contraseñas de Active Directory, administración de contraseñas, autoservicio de restablecimiento de contraseña de Azure AD"
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
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a>Restricciones y directivas de contraseñas en Azure Active Directory

Este artículo describen las directivas de contraseñas de Hola y los requisitos de complejidad asociados con cuentas de usuario almacenadas en el inquilino de Azure AD.

## <a name="administrator-password-policy-differences"></a>Diferencias entre directivas de contraseña del administrador

Microsoft aplica una directiva de restablecimiento de contraseña predeterminada sólida de **dos puertas** para cualquier rol de administrador de Azure (ejemplo: administrador global, administrador del departamento de soporte técnico, administrador de contraseñas, etc).

Esto deshabilita a los administradores del uso de preguntas de seguridad y aplica la siguiente Hola.

Dos de puerta de enlace directiva, que requiere dos fragmentos de datos de autenticación (dirección de correo electrónico **y** número de teléfono), se aplica en hello siguientes circunstancias

* Todos los roles de administrador de Azure
  * Administrador del departamento de soporte técnico
  * Administrador del soporte técnico del servicio
  * Administrador de facturación
  * Soporte para asociados de nivel 1
  * Soporte para asociados de nivel 2
  * Administrador de servicios de Exchange
  * Administrador de servicios de Lync
  * Administrador de cuenta de usuario
  * Escritores de directorios
  * Administrador global y administrador de empresa
  * Administrador de servicios de SharePoint
  * Administrador de cumplimiento
  * Administrador de aplicaciones
  * Administrador de seguridad
  * Administrador de roles con privilegios
  * Administrador de servicios de Intune
  * Administrador del servicio de proxy de la aplicación
  * Administrador de servicios de CRM
  * Administrador de servicios de Power BI
  
* Una vez transcurridos 30 días en una versión de prueba **O**
* El dominio personal está presente (contoso.com) **O**
* Azure AD Connect sincroniza identidades desde el directorio local

### <a name="exceptions"></a>Excepciones
Directiva de una puerta, que requieren una parte de los datos de autenticación (dirección de correo electrónico **o** número de teléfono), se aplica en hello siguientes circunstancias

* Primeros 30 días de una versión de prueba **O**
* El dominio personal no está presente (* .onmicrosoft) **Y** Azure AD Connect no sincroniza identidades


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a>Políticas de UserPrincipalName que se aplican las cuentas de usuario de tooall

Cada cuenta de usuario que necesita toosign en tooAzure AD debe tener un valor de atributo de nombre principal (UPN) único usuario asociado a su cuenta. tabla de Hola a continuación se detallan hello las directivas que se aplican tooboth local de cuentas de usuario de Active Directory sincronizarán toohello en la nube y las cuentas de usuario solo toocloud.

| Propiedad | Requisitos de UserPrincipalName |
| --- | --- |
| Caracteres permitidos |<ul> <li>A – Z</li> <li>a - z</li><li>0 – 9</li> <li> . - \_ ! \# ^ \~</li></ul> |
| Caracteres no permitidos |<ul> <li>Cualquier ' @' carácter que no se separe sus nombres de usuario de Hola de dominio Hola.</li> <li>No puede contener un carácter de punto '.' hello inmediatamente anterior ' @' símbolo</li></ul> |
| Restricciones de longitud |<ul> <li>La longitud total no debe superar los 113 caracteres</li><li>64 caracteres antes de hello ' @' símbolo</li><li>48 caracteres después de hello ' @' símbolo</li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a>Directivas de contraseña que se aplican solo las cuentas de usuario de toocloud

Hello en la tabla siguiente describe la configuración de directiva de contraseña disponible de Hola que puede ser cuentas de toouser aplicado que crean y administran en Azure AD.

| Propiedad | Requisitos |
| --- | --- |
| Caracteres permitidos |<ul><li>A – Z</li><li>a - z</li><li>0 – 9</li> <li>@ # $ % ^ & * - _ ! + = [ ] { } &#124; \ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| Caracteres no permitidos |<ul><li>Caracteres Unicode</li><li>Espacios</li><li> **Solo las contraseñas seguras**: no puede contener un carácter de punto '.' hello inmediatamente anterior ' @' símbolo</li></ul> |
| Restricciones de contraseña |<ul><li>8 caracteres como mínimo y 16 caracteres como máximo.</li><li>**Solo las contraseñas seguras**: 3 requiere fuera 4 del siguiente hello:<ul><li>Caracteres en minúsculas</li><li>Caracteres en mayúsculas</li><li>Números (0 al 9)</li><li>Símbolos (consulte las restricciones de contraseña anteriores)</li></ul></li></ul> |
| Duración de las contraseñas |<ul><li>Valor predeterminado: **90** días </li><li>Valor es configurable mediante el cmdlet Set-MsolPasswordPolicy Hola de hello Azure módulo Active Directory para Windows PowerShell.</li></ul> |
| Notificación de la expiración de contraseñas |<ul><li>Valor predeterminado: **14** días (antes de que caduque la contraseña)</li><li>Valor es configurable mediante el cmdlet Set-MsolPasswordPolicy Hola.</li></ul> |
| Expiración de las contraseñas |<ul><li>Valor predeterminado: **false** días (indica que la caducidad de contraseña está habilitada) </li><li>Valor se puede configurar para cuentas de usuario individuales mediante el cmdlet Set-MsolUser de Hola. </li></ul> |
| Historial de **cambio** de contraseña |**No** puede volver a utilizarse la última contraseña usada al **cambiar** de contraseña. |
| Historial de **restablecimientos** de contraseña | **Puede** utilizar la última contraseña al **restablecer** una contraseña olvidada. |
| Bloqueo de cuenta |Después de 10 inicio de sesión intentos (contraseña incorrecta), usuario de Hola se bloqueará durante un minuto. Aún más el inicio de sesión incorrecto en intentos de usuario Hola de bloqueo para aumentar las duraciones. |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a>Establecimiento de directivas de caducidad de contraseña en Azure Active Directory

Un administrador global para un servicio de nube de Microsoft puede utilizar Hola Microsoft Azure módulo Active Directory para Windows PowerShell tooset seguridad de las contraseñas de usuario no tooexpire. También puede usar Windows PowerShell cmdlets tooremove Hola nunca expira configuración o toosee tooexpire no están configuradas las contraseñas de usuario. Esta guía aplica a los proveedores de tooother como Microsoft Intune y Office 365, que también se basan en Microsoft Azure Active Directory para los servicios de identidad y directorio.

> [!NOTE]
> Solo las contraseñas para cuentas de usuario que no están sincronizadas mediante sincronización de directorios pueden configurarse toonot expire. Para obtener más información sobre la sincronización de directorios, consulte [Conectar AD con Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).
>
>

## <a name="set-or-check-password-policies-using-powershell"></a>Establecimiento o comprobación de directivas de contraseña mediante PowerShell

tooget iniciado, necesita demasiado[descargar e instalar el módulo de PowerShell de Azure AD de hello](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0). Una vez que se ha instalado, puede seguir estos pasos hello tooconfigure cada campo.

### <a name="how-toocheck-expiration-policy-for-a-password"></a>La directiva de expiración de toocheck una contraseña
1. Conectar tooWindows PowerShell con sus credenciales de administrador de empresa.
2. Ejecute uno de hello siguientes comandos:

   * toosee si la contraseña de un usuario solo está configurada toonever expire, ejecute hello siguiente cmdlet con hello nombre principal de usuario (UPN) (por ejemplo, aprilr@contoso.onmicrosoft.com) u Hola Id. de usuario del usuario de hello desea toocheck:`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`
   * toosee Hola "La contraseña nunca expira" configuración para todos los usuarios, ejecute hello siguiente cmdlet:`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`

### <a name="set-a-password-tooexpire"></a>Establecer una contraseña tooexpire

1. Conectar tooWindows PowerShell con sus credenciales de administrador de empresa.
2. Ejecute uno de hello siguientes comandos:

   * contraseña de hello tooset de un usuario para que hello contraseña expira, ejecute hello siguiente cmdlet con hello nombre principal de usuario (UPN) u Hola Id. de usuario del usuario de hello:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`
   * las contraseñas de hello tooset de todos los usuarios de la organización de Hola para que caducan, utilice Hola siguiente cmdlet:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`

### <a name="set-a-password-toonever-expire"></a>Conjunto un toonever contraseña expire

1. Conectar tooWindows PowerShell con sus credenciales de administrador de empresa.
2. Ejecute uno de hello siguientes comandos:

   * contraseña de Hola de tooset de toonever de un usuario expire, ejecute hello siguiente cmdlet con hello nombre principal de usuario (UPN) u Hola Id. de usuario del usuario de hello:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`
   * las contraseñas de hello tooset de todos los usuarios de hello en una organización toonever expire, ejecute hello siguiente cmdlet:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`

## <a name="next-steps"></a>Pasos siguientes

Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña

* [**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD 
* [**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD
* [**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas
* [**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.
* [**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.
* [**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona
* [**Preguntas más frecuentes**](active-directory-passwords-faq.md): ¿Cómo? ¿Por qué? ¿Qué? ¿Dónde? ¿Quién? ¿Cuándo? -Responde tooquestions siempre deseara tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR
