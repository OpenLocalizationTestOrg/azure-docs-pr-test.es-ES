---
title: "aaaGet a trabajar con análisis de Data Lake mediante API de REST | Documentos de Microsoft"
description: "Use las API de REST de WebHDFS tooperform operaciones de análisis de Data Lake"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="2ee5c-103">Introducción a Azure Data Lake Analytics mediante API de REST</span><span class="sxs-lookup"><span data-stu-id="2ee5c-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="2ee5c-104">Obtenga información acerca de cómo toouse WebHDFS API de REST y las API de REST de análisis de datos Lake toomanage análisis de Data Lake cuentas, trabajos y de catálogo.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-104">Learn how toouse WebHDFS REST APIs and Data Lake Analytics REST APIs toomanage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2ee5c-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2ee5c-105">Prerequisites</span></span>
* <span data-ttu-id="2ee5c-106">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-106">**An Azure subscription**.</span></span> <span data-ttu-id="2ee5c-107">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2ee5c-108">**Cree una aplicación de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="2ee5c-109">Usar la aplicación de análisis de Data Lake de hello Azure AD aplicación tooauthenticate Hola con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-109">You use hello Azure AD application tooauthenticate hello Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="2ee5c-110">Hay diferentes enfoques tooauthenticate con Azure AD, que son **autenticación de usuario final** o **autenticación del servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-110">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="2ee5c-111">Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticar con análisis de Data Lake con Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-111">For instructions and more information on how tooauthenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="2ee5c-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="2ee5c-113">En este artículo usa toodemonstrate cURL cómo toomake API de REST se llama con una cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-113">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="2ee5c-114">Autenticación mediante Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ee5c-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="2ee5c-115">Hay dos métodos para autenticar con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="2ee5c-116">Autenticación de usuario final (interactiva)</span><span class="sxs-lookup"><span data-stu-id="2ee5c-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="2ee5c-117">Con este método, aplicación solicita Hola usuario toolog en y se realizan todas las operaciones de hello en contexto de saludo del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-117">Using this method, application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> 

<span data-ttu-id="2ee5c-118">Siga estos pasos para la autenticación interactiva:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="2ee5c-119">A través de la aplicación, redirigir Hola usuario toohello después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-119">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="2ee5c-120">\<URI de redireccionamiento > necesita toobe codificado para su uso en una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-120">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="2ee5c-121">Por lo tanto, para https://localhost, use `https%3A%2F%2Flocalhost`).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="2ee5c-122">A fin de Hola de este tutorial, puede reemplazar los valores de marcador de posición de hello en dirección URL de hello anteriormente y péguelo en la barra de direcciones del explorador de web.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-122">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="2ee5c-123">Será redirigido tooauthenticate mediante el inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-123">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="2ee5c-124">Una vez correctamente, inicie sesión, respuesta de Hola se muestra en la barra de direcciones del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-124">Once you succesfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="2ee5c-125">respuesta de Hello será Hola siguiendo el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-125">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="2ee5c-126">Capturar el código de autorización de Hola de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-126">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="2ee5c-127">Para este tutorial, puede copiar el código de autorización de Hola de barra de direcciones de hello del explorador web de Hola y páselo en hello POST solicitud toohello extremo de token, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-127">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="2ee5c-128">En este caso, Hola \<REDIRECT-URI > no deben codificarse.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-128">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="2ee5c-129">respuesta de Hello es un objeto JSON que contiene un token de acceso (p. ej., `"access_token": "<ACCESS_TOKEN>"`) y un token de actualización (p. ej., `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-129">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="2ee5c-130">La aplicación usa Hola token de acceso al obtener acceso a almacén de Azure Data Lake y tooget de token de actualización de hello otro token de acceso cuando caduca un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-130">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="2ee5c-131">Cuando expira el token de acceso de hello, puede solicitar un nuevo token de acceso con el token de actualización de hello, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-131">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="2ee5c-132">Para más información sobre la autenticación interactiva de usuarios, consulte el [flujo de concesión de un código de autorización](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="2ee5c-133">Autenticación de servicio a servicio (no interactiva)</span><span class="sxs-lookup"><span data-stu-id="2ee5c-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="2ee5c-134">Con este método, aplicación proporciona sus propias credenciales operaciones de hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-134">Using this method, application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="2ee5c-135">Para ello, debe emitir una solicitud POST como Hola se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-135">For this, you must issue a POST request like hello one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="2ee5c-136">salida de Hello de esta solicitud incluirá un token de autorización (indicado por `access-token` en la siguiente salida de Hola) que se pasará posteriormente con las llamadas de API de REST.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-136">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="2ee5c-137">Guarde este token de autenticación en un archivo de texto; lo necesitará más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="2ee5c-138">En este artículo usa hello **no interactivo** enfoque.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-138">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="2ee5c-139">Para obtener más información sobre no interactivo (llamadas de servicio a servicio), consulte [llamadas de tooservice utilizando las credenciales del servicio](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-139">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="2ee5c-140">Creación de una cuenta de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="2ee5c-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="2ee5c-141">Debe crear un grupo de recursos de Azure y una cuenta de Data Lake Store antes de poder crear una cuenta de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="2ee5c-142">Consulte [Creación de una cuenta de Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="2ee5c-143">Hola después del comando Curl mostrará cómo toocreate una cuenta:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-143">hello following Curl command shows how toocreate an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="2ee5c-144">Reemplace \< `REDACTED` \> con token de autorización de hello, \< `AzureSubscriptionID` \> con su identificador de suscripción, \< `AzureResourceGroupName` \> con un recurso de Azure existente Nombre de grupo, y \< `NewAzureDataLakeAnalyticsAccountName` \> con un nuevo nombre de cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-144">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="2ee5c-145">carga de la solicitud de Hola para este comando se encuentra en hello **CreateDatalakeAnalyticsAccountRequest.json** archivo que se proporciona para hello `-d` parámetro anterior.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-145">hello request payload for this command is contained in hello **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="2ee5c-146">Hola contenido del archivo de input.json hello es similar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-146">hello contents of hello input.json file resemble hello following:</span></span>

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="2ee5c-147">Lista de las cuentas de Data Lake Analytics en una suscripción</span><span class="sxs-lookup"><span data-stu-id="2ee5c-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="2ee5c-148">Hola siguiente Curl comando muestra cómo toolist cuentas en una suscripción:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-148">hello following Curl command shows how toolist accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="2ee5c-149">Reemplace \< `REDACTED` \> con token de autorización de hello, \< `AzureSubscriptionID` \> con su identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-149">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="2ee5c-150">es similar a la salida de Hello:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-150">hello output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="2ee5c-151">Información acerca de una cuenta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2ee5c-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="2ee5c-152">Hola después del comando Curl mostrará cómo tooget una información de cuenta:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-152">hello following Curl command shows how tooget an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="2ee5c-153">Reemplace \< `REDACTED` \> con token de autorización de hello, \< `AzureSubscriptionID` \> con su identificador de suscripción, \< `AzureResourceGroupName` \> con un recurso de Azure existente Nombre de grupo, y \< `DataLakeAnalyticsAccountName` \> con el nombre de Hola de una cuenta de análisis de Data Lake existente.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-153">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="2ee5c-154">es similar a la salida de Hello:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-154">hello output is similar to:</span></span>

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="2ee5c-155">Lista de instancias de Data Lake Store de una cuenta de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2ee5c-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="2ee5c-156">Hola siguiente Curl comando muestra cómo almacena toolist Data Lake de una cuenta:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-156">hello following Curl command shows how toolist Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="2ee5c-157">Reemplace \< `REDACTED` \> con token de autorización de hello, \< `AzureSubscriptionID` \> con su identificador de suscripción, \< `AzureResourceGroupName` \> con un recurso de Azure existente Nombre de grupo, y \< `DataLakeAnalyticsAccountName` \> con el nombre de Hola de una cuenta de análisis de Data Lake existente.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-157">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="2ee5c-158">es similar a la salida de Hello:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-158">hello output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="2ee5c-159">Envío de trabajos de U-SQL</span><span class="sxs-lookup"><span data-stu-id="2ee5c-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="2ee5c-160">Hola después del comando Curl mostrará cómo trabajo toosubmit U T-SQL:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-160">hello following Curl command shows how toosubmit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="2ee5c-161">Reemplace \< `REDACTED` \> con token de autorización de hello, \< `DataLakeAnalyticsAccountName` \> con el nombre de Hola de una cuenta de análisis de Data Lake existente.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-161">Replace \<`REDACTED`\> with hello authorization token, \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="2ee5c-162">carga de la solicitud de Hola para este comando se encuentra en hello **SubmitADLAJob.json** archivo que se proporciona para hello `-d` parámetro anterior.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-162">hello request payload for this command is contained in hello **SubmitADLAJob.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="2ee5c-163">Hola contenido del archivo de input.json hello es similar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-163">hello contents of hello input.json file resemble hello following:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="2ee5c-164">es similar a la salida de Hello:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-164">hello output is similar to:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a><span data-ttu-id="2ee5c-165">Lista de trabajos de U-SQL</span><span class="sxs-lookup"><span data-stu-id="2ee5c-165">List U-SQL jobs</span></span>
<span data-ttu-id="2ee5c-166">Hola después del comando Curl mostrará cómo trabajos toolist U-SQL:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-166">hello following Curl command shows how toolist U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="2ee5c-167">Reemplace \< `REDACTED` \> con token de autorización de Hola y \< `DataLakeAnalyticsAccountName` \> con el nombre de Hola de una cuenta de análisis de Data Lake existente.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-167">Replace \<`REDACTED`\> with hello authorization token, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="2ee5c-168">es similar a la salida de Hello:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-168">hello output is similar to:</span></span>

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a><span data-ttu-id="2ee5c-169">Obtener elementos del catálogo</span><span class="sxs-lookup"><span data-stu-id="2ee5c-169">Get catalog items</span></span>
<span data-ttu-id="2ee5c-170">Hola siguiente Curl comando muestra cómo las bases de datos de tooget Hola de Hola catálogo:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-170">hello following Curl command shows how tooget hello databases from hello catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="2ee5c-171">es similar a la salida de Hello:</span><span class="sxs-lookup"><span data-stu-id="2ee5c-171">hello output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="2ee5c-172">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="2ee5c-172">See also</span></span>
* <span data-ttu-id="2ee5c-173">toosee una consulta más compleja, vea [sitio Web de analizar registros con análisis de Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-173">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="2ee5c-174">tooget a desarrollar aplicaciones SQL U, consulte [scripts U T-SQL desarrollar con Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-174">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="2ee5c-175">toolearn T-SQL, vea [empezar a trabajar con el lenguaje de Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-175">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="2ee5c-176">Para conocer las tareas de administración, consulte [Administración de Azure Data Lake Analytics mediante el Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="2ee5c-177">vea tooget un resumen de análisis de Data Lake [información general de análisis de Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ee5c-177">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="2ee5c-178">Hola toosee mismo tutorial con otras herramientas, haga clic en los selectores de pestaña hello en la parte superior de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="2ee5c-178">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>

