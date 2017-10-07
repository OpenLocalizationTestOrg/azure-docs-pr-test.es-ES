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
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Ejemplos de la API de informe de actividad de inicio de sesión de Azure Active Directory
Este tema forma parte de una colección de temas sobre hello Azure Active Directory API de informes.  
Reporting de Azure AD proporciona una API que permite datos de actividad de inicio de sesión de tooaccess mediante código o herramientas relacionadas.  
Hola ámbito de este tema es tooprovide, con el ejemplo de código de hello **API de actividad de inicio de sesión**.

Consulte:

* [Registros de auditoría](active-directory-reporting-azure-portal.md#activity-reports) para más información conceptual
* [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) para obtener más información acerca de la API de informes de Hola.


## <a name="prerequisites"></a>Requisitos previos
Para poder usar los ejemplos de hello en este tema, deberá hello toocomplete [API de generación de informes de requisitos previos tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).  

## <a name="powershell-script"></a>Script de PowerShell
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




## <a name="executing-hello-script"></a>Ejecutando script de Hola
Una vez termine de editar el script de Hola, ejecutarlo y compruebe que Hola se espera que se devuelven datos de informe de registros de auditoría de Hola.

script de Hola devuelve una salida de hello inicio de sesión de informe en formato JSON. También se crea un `SigninActivities.json` archivos con hello el mismo resultado. Puede experimentar mediante la modificación de datos de tooreturn de script de Hola desde otros informes, y marque como comentario los formatos de salida de hello que no es necesario.

## <a name="next-steps"></a>Pasos siguientes
* ¿Le gustaría toocustomize ejemplos de hello en este tema? Extraer del repositorio hello [Azure Active Directory inicio de sesión-actividad de referencia de la API](active-directory-reporting-api-sign-in-activity-reference.md). 
* Si desea que toosee información general completa del uso de hello Azure Active Directory API de informes, consulte [Introducción a Azure Active Directory API de informes de Hola](active-directory-reporting-api-getting-started.md).
* Si desea que toofind más acerca de los informes de Azure Active Directory, vea hello [Azure Active Directory Reporting guía](active-directory-reporting-guide.md).  

