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
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a><span data-ttu-id="dad47-103">Acceso a informes de uso en Azure AD B2C a través de la API de informes de Hola</span><span class="sxs-lookup"><span data-stu-id="dad47-103">Accessing usage reports in Azure AD B2C via hello reporting API</span></span>

<span data-ttu-id="dad47-104">Azure Active Directory B2C (Azure AD B2C) proporciona autenticación basada en el inicio de sesión de los usuarios y en Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="dad47-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="dad47-105">La autenticación se proporciona para los usuarios finales de la familia de aplicaciones en los proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="dad47-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="dad47-106">Si conoce el número de Hola de los usuarios registrados en el inquilino de hello, proveedores de Hola que usan tooregister y el número de Hola de autenticaciones por tipo, puede responder a preguntas como:</span><span class="sxs-lookup"><span data-stu-id="dad47-106">When you know hello number of users registered in hello tenant, hello providers they used tooregister, and hello number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="dad47-107">¿El número de usuarios de cada tipo de proveedor de identidades (por ejemplo, una cuenta de Microsoft o LinkedIn) ha registrado en hello últimos 10 días?</span><span class="sxs-lookup"><span data-stu-id="dad47-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in hello last 10 days?</span></span>
* <span data-ttu-id="dad47-108">¿El número de autenticaciones usando la autenticación multifactor se ha completado correctamente en hello último mes?</span><span class="sxs-lookup"><span data-stu-id="dad47-108">How many authentications using Multi-Factor Authentication have completed successfully in hello last month?</span></span>
* <span data-ttu-id="dad47-109">¿Cuántas autenticaciones basadas en inicios de sesión se han realizado este mes?</span><span class="sxs-lookup"><span data-stu-id="dad47-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="dad47-110">¿Por día?</span><span class="sxs-lookup"><span data-stu-id="dad47-110">Per day?</span></span> <span data-ttu-id="dad47-111">¿Por aplicación?</span><span class="sxs-lookup"><span data-stu-id="dad47-111">Per application?</span></span>
* <span data-ttu-id="dad47-112">¿Cómo puedo calcular Hola espera costo mensual de mi actividad del inquilino de Azure AD B2C?</span><span class="sxs-lookup"><span data-stu-id="dad47-112">How can I estimate hello expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="dad47-113">En este artículo se centra en la actividad de toobilling informes vinculados, que se basa en hello número de usuarios, las autenticaciones de inicio de sesión basada en facturables y las autenticaciones Multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="dad47-113">This article focuses on reports tied toobilling activity, which is based on hello number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="dad47-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dad47-114">Prerequisites</span></span>
<span data-ttu-id="dad47-115">Antes de empezar, necesita pasos de hello toocomplete en [tooaccess de requisitos previos Hola informes de Azure AD API](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="dad47-115">Before you get started, you need toocomplete hello steps in [Prerequisites tooaccess hello Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="dad47-116">Crear una aplicación, obtener un secreto y conceder acceso derechos informes del inquilino de Azure AD B2C tooyour.</span><span class="sxs-lookup"><span data-stu-id="dad47-116">Create an application, obtain a secret for it, and grant it access rights tooyour Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="dad47-117">Aquí también se proporcionan ejemplos de *script de Bash* y *script de Python*.</span><span class="sxs-lookup"><span data-stu-id="dad47-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="dad47-118">Script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="dad47-118">PowerShell script</span></span>
<span data-ttu-id="dad47-119">Este script muestra la creación de hello de cuatro informes de uso mediante el uso de hello `TimeStamp` hello y parámetro `ApplicationId` filtro.</span><span class="sxs-lookup"><span data-stu-id="dad47-119">This script demonstrates hello creation of four usage reports by using hello `TimeStamp` parameter and hello `ApplicationId` filter.</span></span>

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


## <a name="usage-report-definitions"></a><span data-ttu-id="dad47-120">Definiciones de informes de uso</span><span class="sxs-lookup"><span data-stu-id="dad47-120">Usage report definitions</span></span>
* <span data-ttu-id="dad47-121">**tenantUserCount**: Hola número de usuarios de inquilinos de Hola por tipo de proveedor de identidad, al día en hello últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="dad47-121">**tenantUserCount**: hello number of users in hello tenant by type of identity provider, per day in hello last 30 days.</span></span> <span data-ttu-id="dad47-122">(Si lo desea, una `TimeStamp` filtro proporciona recuentos de usuarios de una fecha especificada toohello fecha actual).</span><span class="sxs-lookup"><span data-stu-id="dad47-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date toohello current date).</span></span> <span data-ttu-id="dad47-123">informe de Hello proporciona:</span><span class="sxs-lookup"><span data-stu-id="dad47-123">hello report provides:</span></span>
  * <span data-ttu-id="dad47-124">**TotalUserCount**: Hola número de todos los objetos de usuario.</span><span class="sxs-lookup"><span data-stu-id="dad47-124">**TotalUserCount**: hello number of all user objects.</span></span>
  * <span data-ttu-id="dad47-125">**OtherUserCount**: Hola número de usuarios de Azure Active Directory (no los usuarios de Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="dad47-125">**OtherUserCount**: hello number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="dad47-126">**LocalUserCount**: Hola número de cuentas de usuario de Azure AD B2C creadas con el inquilino de Azure AD B2C de toohello local de credenciales.</span><span class="sxs-lookup"><span data-stu-id="dad47-126">**LocalUserCount**: hello number of Azure AD B2C user accounts created with credentials local toohello Azure AD B2C tenant.</span></span>

* <span data-ttu-id="dad47-127">**AlternateIdUserCount**: número de Hola de usuarios de Azure AD B2C registrado con proveedores de identidades externo (por ejemplo, Facebook, de una cuenta de Microsoft o de otro inquilino de Azure Active Directory, también denominada tooas un `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="dad47-127">**AlternateIdUserCount**: hello number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred tooas an `OrgId`).</span></span>

* <span data-ttu-id="dad47-128">**b2cAuthenticationCountSummary**: resumen del número diario de Hola de autenticaciones facturables sobre Hola últimos 30 días, por día y el tipo de flujo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="dad47-128">**b2cAuthenticationCountSummary**: Summary of hello daily number of billable authentications over hello last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="dad47-129">**b2cAuthenticationCount**: Hola número de autenticaciones dentro de un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="dad47-129">**b2cAuthenticationCount**: hello number of authentications within a time period.</span></span> <span data-ttu-id="dad47-130">valor predeterminado de Hello es Hola últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="dad47-130">hello default is hello last 30 days.</span></span>  <span data-ttu-id="dad47-131">(Opcional: Hola apertura y cierre `TimeStamp` parámetros definen un período de tiempo concreto.) incluye la salida de hello `StartTimeStamp` (fecha más reciente de la actividad para este inquilino) y `EndTimeStamp` (última actualización).</span><span class="sxs-lookup"><span data-stu-id="dad47-131">(Optional: hello beginning and ending `TimeStamp` parameters define a specific time period.) hello output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="dad47-132">**b2cMfaRequestCountSummary**: resumen del número diario de Hola de autenticaciones de varios factores, por día y el tipo (SMS o voz).</span><span class="sxs-lookup"><span data-stu-id="dad47-132">**b2cMfaRequestCountSummary**: Summary of hello daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="dad47-133">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="dad47-133">Limitations</span></span>
<span data-ttu-id="dad47-134">Datos de recuento de usuario se actualizan cada 24 horas too48.</span><span class="sxs-lookup"><span data-stu-id="dad47-134">User count data is refreshed every 24 too48 hours.</span></span> <span data-ttu-id="dad47-135">Las autenticaciones se actualizan varias veces al día.</span><span class="sxs-lookup"><span data-stu-id="dad47-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="dad47-136">Cuando se usa hello `ApplicationId` filtro, una respuesta de informe vacío puede deberse tooone de las condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="dad47-136">When using hello `ApplicationId` filter, an empty report response can be due tooone of following conditions:</span></span>
  * <span data-ttu-id="dad47-137">Identificador de la aplicación Hello no existe en el inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="dad47-137">hello application ID does not exist in hello tenant.</span></span> <span data-ttu-id="dad47-138">Asegúrese de que sea correcto.</span><span class="sxs-lookup"><span data-stu-id="dad47-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="dad47-139">Identificador de la aplicación Hello existe, pero no se encontraron datos en hello período de informe.</span><span class="sxs-lookup"><span data-stu-id="dad47-139">hello application ID exists, but no data was found in hello reporting period.</span></span> <span data-ttu-id="dad47-140">Revise los parámetros de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="dad47-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dad47-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dad47-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="dad47-142">Estimaciones de las facturas mensuales para Azure AD</span><span class="sxs-lookup"><span data-stu-id="dad47-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="dad47-143">Cuando se combina con [Hola precios más reciente de Azure AD B2C disponibles](https://azure.microsoft.com/pricing/details/active-directory-b2c/), puede calcular todos los días, semanal y mensual de consumo de Azure.</span><span class="sxs-lookup"><span data-stu-id="dad47-143">When combined with [hello most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="dad47-144">Una estimación es especialmente útil cuando planee los cambios de comportamiento del inquilino, lo que puede afectar al costo general.</span><span class="sxs-lookup"><span data-stu-id="dad47-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="dad47-145">Puede revisar los costos reales en la [suscripción vinculada de Azure](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="dad47-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="dad47-146">Opciones para otros formatos de salida</span><span class="sxs-lookup"><span data-stu-id="dad47-146">Options for other output formats</span></span>
<span data-ttu-id="dad47-147">Hello código siguiente muestra ejemplos de envío tooJSON de salida, una lista de valores de nombre y XML:</span><span class="sxs-lookup"><span data-stu-id="dad47-147">hello following code shows examples of sending output tooJSON, a name value list, and XML:</span></span>
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
