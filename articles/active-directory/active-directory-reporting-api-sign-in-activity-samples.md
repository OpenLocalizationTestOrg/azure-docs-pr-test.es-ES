---
title: "Ejemplos de la API de informes de actividad de inicio de sesión de Azure Active Directory | Microsoft Docs"
description: "Introducción a la API de informes de Azure Active Directory"
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
ms.openlocfilehash: 7fc2b59fe37ed2ffe85925c457300ef8fd83c3c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="e6f59-103">Ejemplos de la API de informe de actividad de inicio de sesión de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e6f59-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="e6f59-104">Este tema forma parte de una serie de temas sobre la API de informes de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e6f59-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="e6f59-105">La característica de generación de informes de Azure AD proporciona una API que permite acceder a los datos de actividades de inicio de sesión mediante el uso de código o herramientas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="e6f59-105">Azure AD reporting provides you with an API that enables you to access sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="e6f59-106">Este tema se centra en proporcionar el código de ejemplo para la **API de actividad de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e6f59-106">The scope of this topic is to provide you with sample code for the **sign-in activity API**.</span></span>

<span data-ttu-id="e6f59-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="e6f59-107">See:</span></span>

* <span data-ttu-id="e6f59-108">[Registros de auditoría](active-directory-reporting-azure-portal.md#activity-reports) para más información conceptual</span><span class="sxs-lookup"><span data-stu-id="e6f59-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="e6f59-109">[Introducción a la API de generación de informes de Azure Active Directory](active-directory-reporting-api-getting-started.md) para obtener más información sobre esta API</span><span class="sxs-lookup"><span data-stu-id="e6f59-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e6f59-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e6f59-110">Prerequisites</span></span>
<span data-ttu-id="e6f59-111">Para poder usar los ejemplos de este tema, debe completar la [requisitos previos para tener acceso a la API de generación de informes de Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="e6f59-111">Before you can use the samples in this topic, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="e6f59-112">Script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6f59-112">PowerShell script</span></span>
    # This script will require the Web Application and permissions setup in Azure Active Directory
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
        Write-Output "Save the output to a file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-the-script"></a><span data-ttu-id="e6f59-113">Ejecución del script</span><span class="sxs-lookup"><span data-stu-id="e6f59-113">Executing the script</span></span>
<span data-ttu-id="e6f59-114">Una vez que termine de editar el script, ejecútelo y compruebe que el informe de registros de auditoría devuelve los datos esperados.</span><span class="sxs-lookup"><span data-stu-id="e6f59-114">Once you finish editing the script, run it and verify that the expected data from the Audit logs report is returned.</span></span>

<span data-ttu-id="e6f59-115">El script devuelve la salida del informe de inicio de sesión en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e6f59-115">The script returns output from the sign-in report in JSON format.</span></span> <span data-ttu-id="e6f59-116">También se crea un archivo `SigninActivities.json` con la misma salida.</span><span class="sxs-lookup"><span data-stu-id="e6f59-116">It also creates an `SigninActivities.json` file with the same output.</span></span> <span data-ttu-id="e6f59-117">Puede experimentar modificando el script para que devuelva datos de otros informes y convertir en comentario los formatos de salida que no necesite.</span><span class="sxs-lookup"><span data-stu-id="e6f59-117">You can experiment by modifying the script to return data from other reports, and comment out the output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6f59-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e6f59-118">Next Steps</span></span>
* <span data-ttu-id="e6f59-119">¿Quiere personalizar los ejemplos de este tema?</span><span class="sxs-lookup"><span data-stu-id="e6f59-119">Would you like to customize the samples in this topic?</span></span> <span data-ttu-id="e6f59-120">Consulte [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-reference.md)(Referencia de la API de la actividad de inicio de sesión de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e6f59-120">Check out the [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="e6f59-121">Si quiere obtener una descripción completa del uso de la API de generación de informes de Azure Active Directory, consulte el artículo de [introducción a la API de generación de informes de Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e6f59-121">If you want to see a complete overview of using the Azure Active Directory reporting API, see [Getting started with the Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="e6f59-122">Si quiere obtener más información sobre informes de Azure Active Directory, consulte la [guía de generación de informes de Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e6f59-122">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

