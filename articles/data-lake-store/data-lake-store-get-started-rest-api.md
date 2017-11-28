---
title: "tooget de API de REST de hello aaaUse a trabajar con el almacén de Data Lake | Documentos de Microsoft"
description: "Use las API de REST de WebHDFS tooperform operaciones en el almacén de Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="1b690-103">Introducción al Almacén de Azure Data Lake mediante las API de REST</span><span class="sxs-lookup"><span data-stu-id="1b690-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b690-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1b690-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="1b690-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b690-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="1b690-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="1b690-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="1b690-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="1b690-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="1b690-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="1b690-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="1b690-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1b690-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="1b690-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="1b690-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="1b690-111">Python</span><span class="sxs-lookup"><span data-stu-id="1b690-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="1b690-112">En este artículo, aprenderá cómo toouse WebHDFS API de REST API de REST de almacén de datos Lake tooperform de cuentas y administración, así como las operaciones de sistema de archivos en el almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1b690-112">In this article, you will learn how toouse WebHDFS REST APIs and Data Lake Store REST APIs tooperform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="1b690-113">El Almacén de Azure Data Lake expone sus propias API de REST para operaciones de administración de cuentas.</span><span class="sxs-lookup"><span data-stu-id="1b690-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="1b690-114">Sin embargo, como el Almacén de Data Lake es compatible con el ecosistema de HDFS y Hadoop, admite el uso de las API de REST de WebHDFS para las operaciones del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="1b690-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="1b690-115">Para obtener información detallada sobre la compatibilidad con API de REST de hello para el almacén de Data Lake, consulte [referencia de API de REST de almacén de Azure datos Lake](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b690-115">For detailed information on hello REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1b690-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1b690-116">Prerequisites</span></span>
* <span data-ttu-id="1b690-117">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="1b690-117">**An Azure subscription**.</span></span> <span data-ttu-id="1b690-118">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b690-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1b690-119">**Cree una aplicación de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1b690-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="1b690-120">Usar la aplicación de almacén de Data Lake de hello Azure AD aplicación tooauthenticate Hola con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b690-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="1b690-121">Hay diferentes enfoques tooauthenticate con Azure AD, que son **autenticación de usuario final** o **autenticación del servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="1b690-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="1b690-122">Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="1b690-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="1b690-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="1b690-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="1b690-124">En este artículo usa toodemonstrate cURL cómo toomake API de REST se llama con una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1b690-124">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="1b690-125">¿Cómo se puede autenticar mediante Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b690-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="1b690-126">Puede utilizar dos tooauthenticate enfoques con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b690-126">You can use two approaches tooauthenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="1b690-127">Autenticación de usuario final (interactiva)</span><span class="sxs-lookup"><span data-stu-id="1b690-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="1b690-128">En este escenario, aplicación hello pide toolog de usuario de hello en y se realizan todas las operaciones de hello en contexto de saludo del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b690-128">In this scenario, hello application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> <span data-ttu-id="1b690-129">Realizar Hola siguiendo los pasos para la autenticación interactiva.</span><span class="sxs-lookup"><span data-stu-id="1b690-129">Perform hello following steps for interactive authentication.</span></span>

1. <span data-ttu-id="1b690-130">A través de la aplicación, redirigir Hola usuario toohello después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="1b690-130">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="1b690-131">\<URI de redireccionamiento > necesita toobe codificado para su uso en una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="1b690-131">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="1b690-132">Por lo tanto, para https://localhost, use `https%3A%2F%2Flocalhost`).</span><span class="sxs-lookup"><span data-stu-id="1b690-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="1b690-133">A fin de Hola de este tutorial, puede reemplazar los valores de marcador de posición de hello en dirección URL de hello anteriormente y péguelo en la barra de direcciones del explorador de web.</span><span class="sxs-lookup"><span data-stu-id="1b690-133">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="1b690-134">Será redirigido tooauthenticate mediante el inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b690-134">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="1b690-135">Una vez que ha iniciado sesión correctamente, respuesta de Hola se muestra en la barra de direcciones del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b690-135">Once you successfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="1b690-136">respuesta de Hello será Hola siguiendo el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b690-136">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="1b690-137">Capturar el código de autorización de Hola de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b690-137">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="1b690-138">Para este tutorial, puede copiar el código de autorización de Hola de barra de direcciones de hello del explorador web de Hola y páselo en hello POST solicitud toohello extremo de token, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="1b690-138">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="1b690-139">En este caso, Hola \<REDIRECT-URI > no deben codificarse.</span><span class="sxs-lookup"><span data-stu-id="1b690-139">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="1b690-140">respuesta de Hello es un objeto JSON que contiene un token de acceso (p. ej., `"access_token": "<ACCESS_TOKEN>"`) y un token de actualización (p. ej., `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="1b690-140">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="1b690-141">La aplicación usa Hola token de acceso al obtener acceso a almacén de Azure Data Lake y tooget de token de actualización de hello otro token de acceso cuando caduca un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="1b690-141">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="1b690-142">Cuando expira el token de acceso de hello, puede solicitar un nuevo token de acceso con el token de actualización de hello, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="1b690-142">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="1b690-143">Para más información sobre la autenticación interactiva de usuarios, consulte el [flujo de concesión de un código de autorización](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b690-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="1b690-144">Autenticación de servicio a servicio (no interactiva)</span><span class="sxs-lookup"><span data-stu-id="1b690-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="1b690-145">En este escenario, aplicación de Hola Hola proporciona sus propias credenciales operaciones de hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="1b690-145">In this scenario, hello hello application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="1b690-146">Para ello, debe emitir una solicitud POST como Hola se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="1b690-146">For this, you must issue a POST request like hello one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="1b690-147">salida de Hello de esta solicitud incluirá un token de autorización (indicado por `access-token` en la siguiente salida de Hola) que se pasará posteriormente con las llamadas de API de REST.</span><span class="sxs-lookup"><span data-stu-id="1b690-147">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="1b690-148">Guarde este token de autenticación en un archivo de texto; lo necesitará más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1b690-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="1b690-149">En este artículo usa hello **no interactivo** enfoque.</span><span class="sxs-lookup"><span data-stu-id="1b690-149">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="1b690-150">Para obtener más información sobre no interactivo (llamadas de servicio a servicio), consulte [llamadas de tooservice utilizando las credenciales del servicio](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b690-150">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="1b690-151">Crear una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1b690-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="1b690-152">Esta operación se basa en la llamada de API de REST de hello definido [aquí](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b690-152">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="1b690-153">Usar hello siguiente comando cURL.</span><span class="sxs-lookup"><span data-stu-id="1b690-153">Use hello following cURL command.</span></span> <span data-ttu-id="1b690-154">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1b690-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="1b690-155">Hola por encima del comando, reemplace \< `REDACTED` \> con token de autorización de hello recuperar versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="1b690-155">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="1b690-156">carga de la solicitud de Hola para este comando se encuentra en hello **input.json** archivo que se proporciona para hello `-d` parámetro anterior.</span><span class="sxs-lookup"><span data-stu-id="1b690-156">hello request payload for this command is contained in hello **input.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="1b690-157">Hola contenido del archivo de input.json hello es similar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="1b690-157">hello contents of hello input.json file resemble hello following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="1b690-158">Crear carpetas en una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1b690-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="1b690-159">Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="1b690-159">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="1b690-160">Usar hello siguiente comando cURL.</span><span class="sxs-lookup"><span data-stu-id="1b690-160">Use hello following cURL command.</span></span> <span data-ttu-id="1b690-161">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1b690-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="1b690-162">Hola por encima del comando, reemplace \< `REDACTED` \> con token de autorización de hello recuperar versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="1b690-162">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="1b690-163">Este comando crea un directorio llamado **mytempdir** en la carpeta de raíz de Hola de su cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1b690-163">This command creates a directory called **mytempdir** under hello root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="1b690-164">Debería ver una respuesta similar al siguiente si Hola operación se completa correctamente:</span><span class="sxs-lookup"><span data-stu-id="1b690-164">You should see a response like this if hello operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="1b690-165">Mostrar carpetas en una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1b690-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="1b690-166">Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="1b690-166">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="1b690-167">Usar hello siguiente comando cURL.</span><span class="sxs-lookup"><span data-stu-id="1b690-167">Use hello following cURL command.</span></span> <span data-ttu-id="1b690-168">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1b690-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="1b690-169">Hola por encima del comando, reemplace \< `REDACTED` \> con token de autorización de hello recuperar versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="1b690-169">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span>

<span data-ttu-id="1b690-170">Debería ver una respuesta similar al siguiente si Hola operación se completa correctamente:</span><span class="sxs-lookup"><span data-stu-id="1b690-170">You should see a response like this if hello operation completes successfully:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="1b690-171">Cargar datos en una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1b690-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="1b690-172">Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="1b690-172">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="1b690-173">Usar hello siguiente comando cURL.</span><span class="sxs-lookup"><span data-stu-id="1b690-173">Use hello following cURL command.</span></span> <span data-ttu-id="1b690-174">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1b690-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="1b690-175">Hola por encima de la sintaxis **-T** parámetro es Hola ubicación del archivo de Hola que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="1b690-175">In hello above syntax **-T** parameter is hello location of hello file you are uploading.</span></span>

<span data-ttu-id="1b690-176">salida de Hello es siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="1b690-176">hello output is similar toohello following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="1b690-177">Leer datos de una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1b690-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="1b690-178">Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="1b690-178">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="1b690-179">La lectura de datos desde una cuenta del Almacén de Data Lake es un proceso de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="1b690-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="1b690-180">En primer lugar enviar una solicitud GET en el punto de conexión de hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="1b690-180">You first submit a GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="1b690-181">Esto devolverá una ubicación toosubmit Hola siguiente GET solicitud.</span><span class="sxs-lookup"><span data-stu-id="1b690-181">This will return a location toosubmit hello next GET request to.</span></span>
* <span data-ttu-id="1b690-182">A continuación, enviar solicitud de obtención de hello en el punto de conexión de hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="1b690-182">You then submit hello GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="1b690-183">Esto mostrará el contenido de hello del archivo hello.</span><span class="sxs-lookup"><span data-stu-id="1b690-183">This will display hello contents of hello file.</span></span>

<span data-ttu-id="1b690-184">Sin embargo, porque no hay ninguna diferencia en Hola parámetros de entrada entre hello en primer lugar y hello segundo paso, puede usar hello `-L` primera solicitud de parámetro toosubmit Hola.</span><span class="sxs-lookup"><span data-stu-id="1b690-184">However, because there is no difference in hello input parameters between hello first and hello second step, you can use hello `-L` parameter toosubmit hello first request.</span></span> <span data-ttu-id="1b690-185">`-L`opción básicamente combina dos solicitudes en uno y hará que cURL solicitud hello en la nueva ubicación de Hola de puesta al día.</span><span class="sxs-lookup"><span data-stu-id="1b690-185">`-L` option essentially combines two requests into one and will make cURL redo hello request on hello new location.</span></span> <span data-ttu-id="1b690-186">Por último, se muestra la salida de hello de todas las llamadas de solicitud de hello, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="1b690-186">Finally, hello output from all hello request calls is displayed, like shown below.</span></span> <span data-ttu-id="1b690-187">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1b690-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="1b690-188">Debería ver un siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="1b690-188">You should see an output similar toohello following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="1b690-189">Cambiar el nombre de un archivo en una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1b690-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="1b690-190">Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="1b690-190">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="1b690-191">Siguiente Hola de uso cURL toorename de comando en un archivo.</span><span class="sxs-lookup"><span data-stu-id="1b690-191">Use hello following cURL command toorename a file.</span></span> <span data-ttu-id="1b690-192">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1b690-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="1b690-193">Debería ver un siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="1b690-193">You should see an output similar toohello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="1b690-194">Eliminar un archivo de una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1b690-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="1b690-195">Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="1b690-195">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="1b690-196">Siguiente Hola de uso cURL toodelete de comando en un archivo.</span><span class="sxs-lookup"><span data-stu-id="1b690-196">Use hello following cURL command toodelete a file.</span></span> <span data-ttu-id="1b690-197">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1b690-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="1b690-198">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b690-198">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="1b690-199">Eliminar una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1b690-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="1b690-200">Esta operación se basa en la llamada de API de REST de hello definido [aquí](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b690-200">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="1b690-201">Siguiente Hola de uso cURL comando toodelete una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1b690-201">Use hello following cURL command toodelete a Data Lake Store account.</span></span> <span data-ttu-id="1b690-202">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1b690-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="1b690-203">Debería ver una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b690-203">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="1b690-204">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="1b690-204">See also</span></span>
* [<span data-ttu-id="1b690-205">Abrir aplicaciones Big Data de origen que funcionan con el Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1b690-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

