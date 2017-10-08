---
title: "informes de Active Directory de aaaAzure auditoría ejemplos de API | Documentos de Microsoft"
description: "¿Cómo tooget partió hello Azure Active Directory Reporting API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: de8b8ec3-49b3-4aa8-93fb-e38f52c99743
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 6ada8a7184d7baacaba5ba9c1b9130653b1cf7fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-audit-api-samples"></a><span data-ttu-id="ebd00-103">Ejemplos de la API de auditoría de generación de informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ebd00-103">Azure Active Directory reporting audit API samples</span></span>
<span data-ttu-id="ebd00-104">Este tema forma parte de una colección de temas sobre hello Azure Active Directory API de informes.</span><span class="sxs-lookup"><span data-stu-id="ebd00-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="ebd00-105">Reporting de Azure AD proporciona una API que permite los datos de auditoría tooaccess mediante código o herramientas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="ebd00-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="ebd00-106">Hola ámbito de este tema es tooprovide, con el ejemplo de código de hello **API de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="ebd00-106">hello scope of this topic is tooprovide you with sample code for hello **audit API**.</span></span>

<span data-ttu-id="ebd00-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="ebd00-107">See:</span></span>

* <span data-ttu-id="ebd00-108">[Registros de auditoría](active-directory-reporting-azure-portal.md#activity-reports) para obtener más información</span><span class="sxs-lookup"><span data-stu-id="ebd00-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="ebd00-109">[Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) para obtener más información acerca de la API de informes de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebd00-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>

<span data-ttu-id="ebd00-110">Para ver preguntas, problemas o comentarios, póngase en contacto con el equipo de [ayuda de informes de AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ebd00-110">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ebd00-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ebd00-111">Prerequisites</span></span>
<span data-ttu-id="ebd00-112">Para poder usar los ejemplos de hello en este tema, deberá hello toocomplete [API de generación de informes de requisitos previos tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="ebd00-112">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="known-issue"></a><span data-ttu-id="ebd00-113">Problema conocido</span><span class="sxs-lookup"><span data-stu-id="ebd00-113">Known issue</span></span>
<span data-ttu-id="ebd00-114">Autenticación de la aplicación no funcionará si su inquilino está en la región de Europa Hola.</span><span class="sxs-lookup"><span data-stu-id="ebd00-114">App Auth will not work if your tenant is in hello EU region.</span></span> <span data-ttu-id="ebd00-115">Use la autenticación de usuario para tener acceso a API de auditoría de Hola para solucionar este problema hasta que se corrija el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebd00-115">Please use User Auth for accessing hello Audit API as a workaround until we fix hello issue.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="ebd00-116">Script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebd00-116">PowerShell script</span></span>
    # This script will require registration of a Web Application in Azure Active Directory (see https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/)

    # Constants
    $ClientID       = "your-client-application-id-here"       # Insert your application's Client ID, a Globally Unique ID (registered by Global Admin)
    $ClientSecret   = "your-client-application-secret-here"   # Insert your application's Client Key/Secret string
    $loginURL       = "https://login.microsoftonline.com"     # AAD Instance; for example https://login.microsoftonline.com
    $tenantdomain   = "your-tenant-domain.onmicrosoft.com"    # AAD Tenant; for example, contoso.onmicrosoft.com
    $resource       = "https://graph.windows.net"             # Azure AD Graph API resource URI
    $7daysago       = "{0:s}" -f (get-date).AddDays(-7) + "Z" # Use 'AddMinutes(-5)' toodecrement minutes, for example
    Write-Output "Searching for events starting $7daysago"

    # Create HTTP header, get an OAuth2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    # Parse audit report items, save output toofile(s): auditX.json, where X = 0 thru n for number of nextLink pages
    if ($oauth.access_token -ne $null) {   
        $i=0
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}
        $url = 'https://graph.windows.net/' + $tenantdomain + '/activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago

        # loop through each query page (1 through n)
        Do{
            # display each event on hello console window
            Write-Output "Fetching data using Uri: $url"
            $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
            foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
                Write-Output ($event | ConvertTo-Json)
            }

            # save hello query page tooan output file
            Write-Output "Save hello output tooa file audit$i.json"
            $myReport.Content | Out-File -FilePath audit$i.json -Force
            $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
            $i = $i+1
        } while($url -ne $null)
    } else {
        Write-Host "ERROR: No Access Token"
        }

    Write-Host "Press any key toocontinue ..."
    $x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")


### <a name="executing-hello-powershell-script"></a><span data-ttu-id="ebd00-117">Ejecutar script de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="ebd00-117">Executing hello PowerShell script</span></span>
<span data-ttu-id="ebd00-118">Una vez termine de editar el script de Hola, ejecutarlo y compruebe que Hola se espera que se devuelven datos de informe de registros de auditoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebd00-118">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="ebd00-119">script de Hola devuelve una salida de informe de auditoría de hello en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ebd00-119">hello script returns output from hello audit report in JSON format.</span></span> <span data-ttu-id="ebd00-120">También se crea un `audit.json` archivos con hello el mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="ebd00-120">It also creates an `audit.json` file with hello same output.</span></span> <span data-ttu-id="ebd00-121">Puede experimentar mediante la modificación de datos de tooreturn de script de Hola desde otros informes, y marque como comentario los formatos de salida de hello que no es necesario.</span><span class="sxs-lookup"><span data-stu-id="ebd00-121">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="bash-script"></a><span data-ttu-id="ebd00-122">Script de Bash</span><span class="sxs-lookup"><span data-stu-id="ebd00-122">Bash script</span></span>
    #!/bin/bash

    # Author: Ken Hoff (kenhoff@microsoft.com)
    # Date: 2015.08.20
    # NOTE: This script requires jq (https://stedolan.github.io/jq/)

    CLIENT_ID="your-application-client-id-here"         # Should be a ~35 character string insert your info here
    CLIENT_SECRET="your-application-client-secret-here" # Should be a ~44 character string insert your info here
    LOGIN_URL="https://login.microsoftonline.com"
    TENANT_DOMAIN="your-directory-name-here.onmicrosoft.com"    # For example, contoso.onmicrosoft.com

    TOKEN_INFO=$(curl -s --data-urlencode "grant_type=client_credentials" --data-urlencode "client_id=$CLIENT_ID" --data-urlencode "client_secret=$CLIENT_SECRET" "$LOGIN_URL/$TENANT_DOMAIN/oauth2/token?api-version=1.0")

    TOKEN_TYPE=$(echo $TOKEN_INFO | ./jq-win64.exe -r '.token_type')
    ACCESS_TOKEN=$(echo $TOKEN_INFO | ./jq-win64.exe -r '.access_token')

    # get yesterday's date

    YESTERDAY=$(date --date='1 day ago' +'%Y-%m-%d')

    URL="https://graph.windows.net/$TENANT_DOMAIN/activities/audit?api-version=beta&$filter=activityDate%20gt%20$YESTERDAY"


    REPORT=$(curl -s --header "Authorization: $TOKEN_TYPE $ACCESS_TOKEN" $URL)

    echo $REPORT | ./jq-win64.exe -r '.value' | ./jq-win64.exe -r ".[]"

## <a name="python-script"></a><span data-ttu-id="ebd00-123">Script de Python</span><span class="sxs-lookup"><span data-stu-id="ebd00-123">Python script</span></span>
    # Author: Michael McLaughlin (michmcla@microsoft.com)
    # Date: January 20, 2016
    # This requires hello Python Requests module: http://docs.python-requests.org

    import requests
    import datetime
    import sys

    client_id = 'your-application-client-id-here'
    client_secret = 'your-application-client-secret-here'
    login_url = 'https://login.microsoftonline.com/'
    tenant_domain = 'your-directory-name-here.onmicrosoft.com'

    # Get an OAuth access token
    bodyvals = {'client_id': client_id,
                'client_secret': client_secret,
                'grant_type': 'client_credentials'}

    request_url = login_url + tenant_domain + '/oauth2/token?api-version=1.0'
    token_response = requests.post(request_url, data=bodyvals)

    access_token = token_response.json().get('access_token')
    token_type = token_response.json().get('token_type')

    if access_token is None or token_type is None:
        print "ERROR: Couldn't get access token"
        sys.exit(1)

    # Use hello access token toomake hello API request
    yesterday = datetime.date.strftime(datetime.date.today() - datetime.timedelta(days=1), '%Y-%m-%d')

    header_params = {'Authorization': token_type + ' ' + access_token}
    request_string = 'https://graph.windows.net/' + tenant_domain + 'activities/audit?api-version=beta&$filter=activityDate%20gt%20' + yesterday   
    response = requests.get(request_string, headers = header_params)

    if response.status_code is 200:
        print response.content
    else:
        print 'ERROR: API request failed'





## <a name="next-steps"></a><span data-ttu-id="ebd00-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ebd00-124">Next steps</span></span>
* <span data-ttu-id="ebd00-125">¿Le gustaría toocustomize ejemplos de hello en este tema?</span><span class="sxs-lookup"><span data-stu-id="ebd00-125">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="ebd00-126">Extraer del repositorio hello [auditoría de Azure Active Directory referencia de la API](active-directory-reporting-api-audit-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ebd00-126">Check out hello [Azure Active Directory audit API reference](active-directory-reporting-api-audit-reference.md).</span></span> 
* <span data-ttu-id="ebd00-127">Si desea que toosee información general completa del uso de hello Azure Active Directory API de informes, consulte [Introducción a Azure Active Directory API de informes de Hola](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="ebd00-127">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="ebd00-128">Si desea que toofind más acerca de los informes de Azure Active Directory, vea hello [Azure Active Directory Reporting guía](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="ebd00-128">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

