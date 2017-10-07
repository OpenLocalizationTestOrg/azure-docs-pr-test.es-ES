---
title: "ejemplos de API de informes de actividad de aaaAzure inicio de sesión de Active Directory | Documentos de Microsoft"
description: "¿Cómo tooget partió hello Azure Active Directory Reporting API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d4fbbea95fe0b52828673b997681ae37481e21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="e9870-103">Ejemplos de la API de informe de actividad de inicio de sesión de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9870-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="e9870-104">Este tema forma parte de una colección de temas sobre hello Azure Active Directory API de informes.</span><span class="sxs-lookup"><span data-stu-id="e9870-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="e9870-105">Reporting de Azure AD proporciona una API que permite datos de actividad de inicio de sesión de tooaccess mediante código o herramientas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="e9870-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="e9870-106">Hola ámbito de este tema es tooprovide, con el ejemplo de código de hello **API de actividad de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e9870-106">hello scope of this topic is tooprovide you with sample code for hello **sign-in activity API**.</span></span>

<span data-ttu-id="e9870-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="e9870-107">See:</span></span>

* <span data-ttu-id="e9870-108">[Registros de auditoría](active-directory-reporting-azure-portal.md#activity-reports) para más información conceptual</span><span class="sxs-lookup"><span data-stu-id="e9870-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="e9870-109">[Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) para obtener más información acerca de la API de informes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9870-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e9870-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e9870-110">Prerequisites</span></span>
<span data-ttu-id="e9870-111">Para poder usar los ejemplos de hello en este tema, deberá hello toocomplete [API de generación de informes de requisitos previos tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="e9870-111">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="e9870-112">Script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9870-112">PowerShell script</span></span>
    # This script will require hello Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.microsoftonline.com/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save hello output tooa file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-hello-script"></a><span data-ttu-id="e9870-113">Ejecutando script de Hola</span><span class="sxs-lookup"><span data-stu-id="e9870-113">Executing hello script</span></span>
<span data-ttu-id="e9870-114">Una vez termine de editar el script de Hola, ejecutarlo y compruebe que Hola se espera que se devuelven datos de informe de registros de auditoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9870-114">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="e9870-115">script de Hola devuelve una salida de hello inicio de sesión de informe en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e9870-115">hello script returns output from hello sign-in report in JSON format.</span></span> <span data-ttu-id="e9870-116">También se crea un `SigninActivities.json` archivos con hello el mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="e9870-116">It also creates an `SigninActivities.json` file with hello same output.</span></span> <span data-ttu-id="e9870-117">Puede experimentar mediante la modificación de datos de tooreturn de script de Hola desde otros informes, y marque como comentario los formatos de salida de hello que no es necesario.</span><span class="sxs-lookup"><span data-stu-id="e9870-117">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9870-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e9870-118">Next Steps</span></span>
* <span data-ttu-id="e9870-119">¿Le gustaría toocustomize ejemplos de hello en este tema?</span><span class="sxs-lookup"><span data-stu-id="e9870-119">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="e9870-120">Extraer del repositorio hello [Azure Active Directory inicio de sesión-actividad de referencia de la API](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e9870-120">Check out hello [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="e9870-121">Si desea que toosee información general completa del uso de hello Azure Active Directory API de informes, consulte [Introducción a Azure Active Directory API de informes de Hola](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e9870-121">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="e9870-122">Si desea que toofind más acerca de los informes de Azure Active Directory, vea hello [Azure Active Directory Reporting guía](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e9870-122">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

