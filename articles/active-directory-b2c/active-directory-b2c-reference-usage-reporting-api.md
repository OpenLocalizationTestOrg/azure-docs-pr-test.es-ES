---
title: 'Azure Active Directory B2C: Ejemplos y definiciones de la API de informes de uso | Microsoft Docs'
description: "Guía y ejemplos sobre la obtención de informes en las autenticaciones multifactor, las autenticaciones y los usuarios de inquilino de Azure AD B2C"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a>Acceso a informes de uso en Azure AD B2C a través de la API de informes de Hola

Azure Active Directory B2C (Azure AD B2C) proporciona autenticación basada en el inicio de sesión de los usuarios y en Azure Multi-Factor Authentication. La autenticación se proporciona para los usuarios finales de la familia de aplicaciones en los proveedores de identidades. Si conoce el número de Hola de los usuarios registrados en el inquilino de hello, proveedores de Hola que usan tooregister y el número de Hola de autenticaciones por tipo, puede responder a preguntas como:
* ¿El número de usuarios de cada tipo de proveedor de identidades (por ejemplo, una cuenta de Microsoft o LinkedIn) ha registrado en hello últimos 10 días?
* ¿El número de autenticaciones usando la autenticación multifactor se ha completado correctamente en hello último mes?
* ¿Cuántas autenticaciones basadas en inicios de sesión se han realizado este mes? ¿Por día? ¿Por aplicación?
* ¿Cómo puedo calcular Hola espera costo mensual de mi actividad del inquilino de Azure AD B2C?

En este artículo se centra en la actividad de toobilling informes vinculados, que se basa en hello número de usuarios, las autenticaciones de inicio de sesión basada en facturables y las autenticaciones Multi-factor Authentication.


## <a name="prerequisites"></a>Requisitos previos
Antes de empezar, necesita pasos de hello toocomplete en [tooaccess de requisitos previos Hola informes de Azure AD API](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/). Crear una aplicación, obtener un secreto y conceder acceso derechos informes del inquilino de Azure AD B2C tooyour. Aquí también se proporcionan ejemplos de *script de Bash* y *script de Python*. 

## <a name="powershell-script"></a>Script de PowerShell
Este script muestra la creación de hello de cuatro informes de uso mediante el uso de hello `TimeStamp` hello y parámetro `ApplicationId` filtro.

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a>Definiciones de informes de uso
* **tenantUserCount**: Hola número de usuarios de inquilinos de Hola por tipo de proveedor de identidad, al día en hello últimos 30 días. (Si lo desea, una `TimeStamp` filtro proporciona recuentos de usuarios de una fecha especificada toohello fecha actual). informe de Hello proporciona:
  * **TotalUserCount**: Hola número de todos los objetos de usuario.
  * **OtherUserCount**: Hola número de usuarios de Azure Active Directory (no los usuarios de Azure AD B2C).
  * **LocalUserCount**: Hola número de cuentas de usuario de Azure AD B2C creadas con el inquilino de Azure AD B2C de toohello local de credenciales.

* **AlternateIdUserCount**: número de Hola de usuarios de Azure AD B2C registrado con proveedores de identidades externo (por ejemplo, Facebook, de una cuenta de Microsoft o de otro inquilino de Azure Active Directory, también denominada tooas un `OrgId`).

* **b2cAuthenticationCountSummary**: resumen del número diario de Hola de autenticaciones facturables sobre Hola últimos 30 días, por día y el tipo de flujo de autenticación.

* **b2cAuthenticationCount**: Hola número de autenticaciones dentro de un período de tiempo. valor predeterminado de Hello es Hola últimos 30 días.  (Opcional: Hola apertura y cierre `TimeStamp` parámetros definen un período de tiempo concreto.) incluye la salida de hello `StartTimeStamp` (fecha más reciente de la actividad para este inquilino) y `EndTimeStamp` (última actualización).

* **b2cMfaRequestCountSummary**: resumen del número diario de Hola de autenticaciones de varios factores, por día y el tipo (SMS o voz).


## <a name="limitations"></a>Limitaciones
Datos de recuento de usuario se actualizan cada 24 horas too48. Las autenticaciones se actualizan varias veces al día. Cuando se usa hello `ApplicationId` filtro, una respuesta de informe vacío puede deberse tooone de las condiciones siguientes:
  * Identificador de la aplicación Hello no existe en el inquilino de Hola. Asegúrese de que sea correcto.
  * Identificador de la aplicación Hello existe, pero no se encontraron datos en hello período de informe. Revise los parámetros de fecha y hora.


## <a name="next-steps"></a>Pasos siguientes
### <a name="monthly-bill-estimates-for-azure-ad"></a>Estimaciones de las facturas mensuales para Azure AD
Cuando se combina con [Hola precios más reciente de Azure AD B2C disponibles](https://azure.microsoft.com/pricing/details/active-directory-b2c/), puede calcular todos los días, semanal y mensual de consumo de Azure.  Una estimación es especialmente útil cuando planee los cambios de comportamiento del inquilino, lo que puede afectar al costo general. Puede revisar los costos reales en la [suscripción vinculada de Azure](active-directory-b2c-how-to-enable-billing.md).

### <a name="options-for-other-output-formats"></a>Opciones para otros formatos de salida
Hello código siguiente muestra ejemplos de envío tooJSON de salida, una lista de valores de nombre y XML:
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
