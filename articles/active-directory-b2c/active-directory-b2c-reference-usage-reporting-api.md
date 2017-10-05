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
ms.openlocfilehash: 52180b760046d273c5a75720df0a73532d0343ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-the-reporting-api"></a><span data-ttu-id="7b044-103">Acceso a informes de uso en Azure AD B2C a través de la API de informes</span><span class="sxs-lookup"><span data-stu-id="7b044-103">Accessing usage reports in Azure AD B2C via the reporting API</span></span>

<span data-ttu-id="7b044-104">Azure Active Directory B2C (Azure AD B2C) proporciona autenticación basada en el inicio de sesión de los usuarios y en Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="7b044-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="7b044-105">La autenticación se proporciona para los usuarios finales de la familia de aplicaciones en los proveedores de identidades.</span><span class="sxs-lookup"><span data-stu-id="7b044-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="7b044-106">Cuando conozca el número de usuarios registrados en el inquilino, los proveedores que usan para registrarse y el número de autenticaciones por tipo, puede responder preguntas como:</span><span class="sxs-lookup"><span data-stu-id="7b044-106">When you know the number of users registered in the tenant, the providers they used to register, and the number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="7b044-107">¿Cuántos usuarios de cada tipo de proveedor de identidades (por ejemplo, una cuenta de Microsoft o LinkedIn) se han registrado en los últimos 10 días?</span><span class="sxs-lookup"><span data-stu-id="7b044-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in the last 10 days?</span></span>
* <span data-ttu-id="7b044-108">¿Cuántas autenticaciones con Multi-Factor Authentication se han realizado correctamente en el último mes?</span><span class="sxs-lookup"><span data-stu-id="7b044-108">How many authentications using Multi-Factor Authentication have completed successfully in the last month?</span></span>
* <span data-ttu-id="7b044-109">¿Cuántas autenticaciones basadas en inicios de sesión se han realizado este mes?</span><span class="sxs-lookup"><span data-stu-id="7b044-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="7b044-110">¿Por día?</span><span class="sxs-lookup"><span data-stu-id="7b044-110">Per day?</span></span> <span data-ttu-id="7b044-111">¿Por aplicación?</span><span class="sxs-lookup"><span data-stu-id="7b044-111">Per application?</span></span>
* <span data-ttu-id="7b044-112">¿Cómo puedo estimar el costo mensual previsto de mi actividad de inquilino de Azure AD B2C?</span><span class="sxs-lookup"><span data-stu-id="7b044-112">How can I estimate the expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="7b044-113">Este artículo se centra en informes relacionados con el trabajo de facturación, que se basa en el número de usuarios, las autenticaciones basadas en inicios de sesión facturables y las autenticaciones multifactor.</span><span class="sxs-lookup"><span data-stu-id="7b044-113">This article focuses on reports tied to billing activity, which is based on the number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7b044-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7b044-114">Prerequisites</span></span>
<span data-ttu-id="7b044-115">Antes de comenzar, debe completar los pasos de [Requisitos previos para acceder a la API de informes de Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="7b044-115">Before you get started, you need to complete the steps in [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="7b044-116">Cree una aplicación, obtenga un secreto y concédale derechos de acceso a los informes del inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7b044-116">Create an application, obtain a secret for it, and grant it access rights to your Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="7b044-117">Aquí también se proporcionan ejemplos de *script de Bash* y *script de Python*.</span><span class="sxs-lookup"><span data-stu-id="7b044-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="7b044-118">Script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b044-118">PowerShell script</span></span>
<span data-ttu-id="7b044-119">Este script muestra la creación de cuatro informes de uso con el parámetro `TimeStamp` y el filtro `ApplicationId`.</span><span class="sxs-lookup"><span data-stu-id="7b044-119">This script demonstrates the creation of four usage reports by using the `TimeStamp` parameter and the `ApplicationId` filter.</span></span>

```powershell
# This script will require the Web Application and permissions setup in Azure Active Directory

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

    Write-host Data from the tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for the report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for the " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="7b044-120">Definiciones de informes de uso</span><span class="sxs-lookup"><span data-stu-id="7b044-120">Usage report definitions</span></span>
* <span data-ttu-id="7b044-121">**tenantUserCount**: el número de usuarios en el inquilino por tipo de proveedor de identidades al día en los últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="7b044-121">**tenantUserCount**: The number of users in the tenant by type of identity provider, per day in the last 30 days.</span></span> <span data-ttu-id="7b044-122">(De manera opcional, un filtro `TimeStamp` proporciona recuentos de usuarios desde una fecha especificada hasta la fecha actual).</span><span class="sxs-lookup"><span data-stu-id="7b044-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date to the current date).</span></span> <span data-ttu-id="7b044-123">El informe proporciona:</span><span class="sxs-lookup"><span data-stu-id="7b044-123">The report provides:</span></span>
  * <span data-ttu-id="7b044-124">**TotalUserCount**: el número de todos los objetos de usuario.</span><span class="sxs-lookup"><span data-stu-id="7b044-124">**TotalUserCount**: The number of all user objects.</span></span>
  * <span data-ttu-id="7b044-125">**OtherUserCount**: el número de usuarios de Azure Active Directory (no de usuarios de Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="7b044-125">**OtherUserCount**: The number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="7b044-126">**LocalUserCount**: el número de cuentas de usuario de Azure AD B2C creadas con credenciales locales para el inquilino de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7b044-126">**LocalUserCount**: The number of Azure AD B2C user accounts created with credentials local to the Azure AD B2C tenant.</span></span>

* <span data-ttu-id="7b044-127">**AlternateIdUserCount**: el número de usuarios de Azure AD B2C registrados con proveedores de identidades externos (por ejemplo, Facebook, una cuenta Microsoft u otro inquilino de Azure Active Directory, al que también se hace referencia como un `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="7b044-127">**AlternateIdUserCount**: The number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred to as an `OrgId`).</span></span>

* <span data-ttu-id="7b044-128">**b2cAuthenticationCountSummary**: resumen del recuento diario de autenticaciones facturables durante los últimos 30 días por día y por tipo de flujo de autenticación.</span><span class="sxs-lookup"><span data-stu-id="7b044-128">**b2cAuthenticationCountSummary**: Summary of the daily number of billable authentications over the last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="7b044-129">**b2cAuthenticationCount**: el número de autenticaciones dentro de un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="7b044-129">**b2cAuthenticationCount**: The number of authentications within a time period.</span></span> <span data-ttu-id="7b044-130">El valor predeterminado es los últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="7b044-130">The default is the last 30 days.</span></span>  <span data-ttu-id="7b044-131">(Opcional: los parámetros `TimeStamp` iniciales y finales definen un período de tiempo específico). La salida incluye `StartTimeStamp` (primera fecha de actividad de este inquilino) y `EndTimeStamp` (última actualización).</span><span class="sxs-lookup"><span data-stu-id="7b044-131">(Optional: The beginning and ending `TimeStamp` parameters define a specific time period.) The output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="7b044-132">**b2cMfaRequestCountSummary**: resumen del recuento diario de autenticaciones multifactor por día y por tipo (SMS o voz).</span><span class="sxs-lookup"><span data-stu-id="7b044-132">**b2cMfaRequestCountSummary**: Summary of the daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="7b044-133">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="7b044-133">Limitations</span></span>
<span data-ttu-id="7b044-134">Datos de recuento de usuarios se actualizan cada 24 a 48 horas.</span><span class="sxs-lookup"><span data-stu-id="7b044-134">User count data is refreshed every 24 to 48 hours.</span></span> <span data-ttu-id="7b044-135">Las autenticaciones se actualizan varias veces al día.</span><span class="sxs-lookup"><span data-stu-id="7b044-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="7b044-136">Al usar el filtro `ApplicationId`, una respuesta de informe vacío puede deberse a una de las condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="7b044-136">When using the `ApplicationId` filter, an empty report response can be due to one of following conditions:</span></span>
  * <span data-ttu-id="7b044-137">El identificador de la aplicación no existe en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="7b044-137">The application ID does not exist in the tenant.</span></span> <span data-ttu-id="7b044-138">Asegúrese de que sea correcto.</span><span class="sxs-lookup"><span data-stu-id="7b044-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="7b044-139">El identificador de la aplicación existe, pero no se han encontrado datos en el período de informes.</span><span class="sxs-lookup"><span data-stu-id="7b044-139">The application ID exists, but no data was found in the reporting period.</span></span> <span data-ttu-id="7b044-140">Revise los parámetros de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="7b044-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7b044-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b044-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="7b044-142">Estimaciones de las facturas mensuales para Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b044-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="7b044-143">Cuando se combina con [los precios disponibles más actualizados de Azure AD B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/), puede calcular el consumo diario, semanal y mensual de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b044-143">When combined with [the most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="7b044-144">Una estimación es especialmente útil cuando planee los cambios de comportamiento del inquilino, lo que puede afectar al costo general.</span><span class="sxs-lookup"><span data-stu-id="7b044-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="7b044-145">Puede revisar los costos reales en la [suscripción vinculada de Azure](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="7b044-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="7b044-146">Opciones para otros formatos de salida</span><span class="sxs-lookup"><span data-stu-id="7b044-146">Options for other output formats</span></span>
<span data-ttu-id="7b044-147">En el código siguiente se muestran ejemplos de envío de la salida a JSON, una lista de valores de nombre y XML:</span><span class="sxs-lookup"><span data-stu-id="7b044-147">The following code shows examples of sending output to JSON, a name value list, and XML:</span></span>
```powershell
# to output to JSON use following line in the PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# to output the content to a name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# to output the content in XML use the following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
