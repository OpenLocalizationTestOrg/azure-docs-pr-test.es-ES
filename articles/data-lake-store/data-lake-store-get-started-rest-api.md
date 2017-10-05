---
title: "Uso del SDK de Python como introducción a Azure Data Lake Store | Microsoft Docs"
description: "Usar las API de REST de WebHDFS para realizar operaciones en el Almacén de Data Lake"
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
ms.openlocfilehash: dc2c8f58e0a2faf1b00f4903148328a5141a8637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="dc657-103">Introducción al Almacén de Azure Data Lake mediante las API de REST</span><span class="sxs-lookup"><span data-stu-id="dc657-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc657-104">Portal</span><span class="sxs-lookup"><span data-stu-id="dc657-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="dc657-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc657-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="dc657-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="dc657-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="dc657-107">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="dc657-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="dc657-108">API de REST</span><span class="sxs-lookup"><span data-stu-id="dc657-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="dc657-109">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dc657-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="dc657-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="dc657-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="dc657-111">Python</span><span class="sxs-lookup"><span data-stu-id="dc657-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="dc657-112">En este artículo, obtendrá información sobre cómo usar las API de REST de WebHDFS y las API de REST del Almacén de Data Lake para realizar la administración de cuentas así como las operaciones del sistema de archivos del Almacén de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="dc657-112">In this article, you will learn how to use WebHDFS REST APIs and Data Lake Store REST APIs to perform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="dc657-113">El Almacén de Azure Data Lake expone sus propias API de REST para operaciones de administración de cuentas.</span><span class="sxs-lookup"><span data-stu-id="dc657-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="dc657-114">Sin embargo, como el Almacén de Data Lake es compatible con el ecosistema de HDFS y Hadoop, admite el uso de las API de REST de WebHDFS para las operaciones del sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="dc657-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="dc657-115">Para obtener información detallada sobre la compatibilidad de la API de REST con el Almacén de Data Lake, consulte [Referencia de la API de REST en el Almacén de Azure Data Lake](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc657-115">For detailed information on the REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="dc657-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dc657-116">Prerequisites</span></span>
* <span data-ttu-id="dc657-117">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="dc657-117">**An Azure subscription**.</span></span> <span data-ttu-id="dc657-118">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc657-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="dc657-119">**Cree una aplicación de Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc657-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="dc657-120">Utilice la aplicación Azure AD para autenticar la aplicación Data Lake Store con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc657-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="dc657-121">Existen diferentes enfoques para realizar la autenticación con Azure AD, que son la **autenticación de usuario final** o la **autenticación de servicio a servicio**.</span><span class="sxs-lookup"><span data-stu-id="dc657-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="dc657-122">Para obtener instrucciones y más información acerca de cómo realizar la autenticación, consulte [Autenticación de usuario final con Data Lake Store mediante Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticación entre servicios con Data Lake Store mediante Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="dc657-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="dc657-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="dc657-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="dc657-124">En este artículo se usa cURL para demostrar cómo realizar llamadas de la API de REST en una cuenta de Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="dc657-124">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="dc657-125">¿Cómo se puede autenticar mediante Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc657-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="dc657-126">Puede usar dos enfoques para autenticar con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dc657-126">You can use two approaches to authenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="dc657-127">Autenticación de usuario final (interactiva)</span><span class="sxs-lookup"><span data-stu-id="dc657-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="dc657-128">En este escenario, la aplicación pide al usuario que inicie sesión y todas las operaciones se realizan en el contexto del usuario.</span><span class="sxs-lookup"><span data-stu-id="dc657-128">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span></span> <span data-ttu-id="dc657-129">Realice los pasos siguientes para realizar la autenticación interactiva.</span><span class="sxs-lookup"><span data-stu-id="dc657-129">Perform the following steps for interactive authentication.</span></span>

1. <span data-ttu-id="dc657-130">A través de la aplicación, redirija al usuario a la siguiente dirección URL:</span><span class="sxs-lookup"><span data-stu-id="dc657-130">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="dc657-131">\<REDIRECT-URI> debe codificarse para utilizarse en una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="dc657-131">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="dc657-132">Por lo tanto, para https://localhost, use `https%3A%2F%2Flocalhost`).</span><span class="sxs-lookup"><span data-stu-id="dc657-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="dc657-133">Para este tutorial, puede sustituir los valores de marcador de posición de la dirección URL anterior y pegarlos en la barra de direcciones del explorador web.</span><span class="sxs-lookup"><span data-stu-id="dc657-133">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="dc657-134">Se le redirigirá a una página autenticarse con sus datos de inicio de sesión de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc657-134">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="dc657-135">Una vez que haya iniciado sesión correctamente, la respuesta se muestra en la barra de direcciones del explorador.</span><span class="sxs-lookup"><span data-stu-id="dc657-135">Once you successfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="dc657-136">La respuesta estará en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc657-136">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="dc657-137">Obtenga el código de autorización de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="dc657-137">Capture the authorization code from the response.</span></span> <span data-ttu-id="dc657-138">Para este tutorial, puede copiar el código de autorización de la barra de direcciones del explorador web y pasarlo en la solicitud POST al punto de conexión de token, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="dc657-138">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="dc657-139">En este caso, no se necesita codificar \<REDIRECT-URI>.</span><span class="sxs-lookup"><span data-stu-id="dc657-139">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="dc657-140">La respuesta es un objeto JSON que contiene un token de acceso (por ejemplo, `"access_token": "<ACCESS_TOKEN>"`) y uno de actualización (por ejemplo, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="dc657-140">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="dc657-141">La aplicación usa el token de acceso al acceder al Almacén de Azure Data Lake y el token de actualización para obtener otro token de acceso cuando expira un token de acceso.</span><span class="sxs-lookup"><span data-stu-id="dc657-141">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="dc657-142">Cuando expira el token de acceso, puede solicitar uno nuevo con el token de actualización, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="dc657-142">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="dc657-143">Para más información sobre la autenticación interactiva de usuarios, consulte el [flujo de concesión de un código de autorización](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc657-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="dc657-144">Autenticación de servicio a servicio (no interactiva)</span><span class="sxs-lookup"><span data-stu-id="dc657-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="dc657-145">En este escenario, la aplicación proporciona sus propias credenciales para realizar las operaciones.</span><span class="sxs-lookup"><span data-stu-id="dc657-145">In this scenario, the the application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="dc657-146">Para ello, debe emitir una solicitud POST como la que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="dc657-146">For this, you must issue a POST request like the one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="dc657-147">El resultado de esta solicitud incluirá un token de autorización (que se indica mediante `access-token` en el siguiente resultado) que pasará posteriormente con las llamadas de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="dc657-147">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="dc657-148">Guarde este token de autenticación en un archivo de texto; lo necesitará más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="dc657-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="dc657-149">En este artículo se usa el enfoque **no interactivo** .</span><span class="sxs-lookup"><span data-stu-id="dc657-149">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="dc657-150">Para más información sobre el enfoque no interactivo (llamadas de servicio a servicio), consulte el tema sobre [llamadas de servicio a servicio utilizando las credenciales del cliente](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc657-150">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="dc657-151">Crear una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc657-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="dc657-152">Esta operación se basa en la llamada de la API de REST que se define [aquí](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc657-152">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="dc657-153">Use el siguiente comando cURL.</span><span class="sxs-lookup"><span data-stu-id="dc657-153">Use the following cURL command.</span></span> <span data-ttu-id="dc657-154">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc657-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="dc657-155">En el comando anterior, reemplace \<`REDACTED`\> por el token de autorización que recuperó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dc657-155">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="dc657-156">La carga útil de la solicitud de este comando se encuentra en el archivo **input.json** que se proporciona para el parámetro `-d` anterior.</span><span class="sxs-lookup"><span data-stu-id="dc657-156">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="dc657-157">El contenido del archivo input.json es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc657-157">The contents of the input.json file resemble the following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="dc657-158">Crear carpetas en una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc657-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="dc657-159">Esta operación se basa en la llamada de la API de REST de WebHDFS que se define [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="dc657-159">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="dc657-160">Use el siguiente comando cURL.</span><span class="sxs-lookup"><span data-stu-id="dc657-160">Use the following cURL command.</span></span> <span data-ttu-id="dc657-161">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc657-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="dc657-162">En el comando anterior, reemplace \<`REDACTED`\> por el token de autorización que recuperó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dc657-162">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="dc657-163">Este comando crea un directorio denominado **mytempdir** bajo la carpeta raíz de su cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc657-163">This command creates a directory called **mytempdir** under the root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="dc657-164">Si la operación se completa correctamente, verá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc657-164">You should see a response like this if the operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="dc657-165">Mostrar carpetas en una cuenta de Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc657-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="dc657-166">Esta operación se basa en la llamada de la API de REST de WebHDFS que se define [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="dc657-166">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="dc657-167">Use el siguiente comando cURL.</span><span class="sxs-lookup"><span data-stu-id="dc657-167">Use the following cURL command.</span></span> <span data-ttu-id="dc657-168">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc657-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="dc657-169">En el comando anterior, reemplace \<`REDACTED`\> por el token de autorización que recuperó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dc657-169">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span>

<span data-ttu-id="dc657-170">Si la operación se completa correctamente, verá una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc657-170">You should see a response like this if the operation completes successfully:</span></span>

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

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="dc657-171">Cargar datos en una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc657-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="dc657-172">Esta operación se basa en la llamada de la API de REST de WebHDFS que se define [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="dc657-172">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="dc657-173">Use el siguiente comando cURL.</span><span class="sxs-lookup"><span data-stu-id="dc657-173">Use the following cURL command.</span></span> <span data-ttu-id="dc657-174">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc657-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="dc657-175">En la sintaxis anterior el parámetro **-T** es la ubicación del archivo que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="dc657-175">In the above syntax **-T** parameter is the location of the file you are uploading.</span></span>

<span data-ttu-id="dc657-176">La salida será similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc657-176">The output is similar to the following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="dc657-177">Leer datos de una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc657-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="dc657-178">Esta operación se basa en la llamada de la API de REST de WebHDFS que se define [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="dc657-178">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="dc657-179">La lectura de datos desde una cuenta del Almacén de Data Lake es un proceso de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="dc657-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="dc657-180">Primero, envíe una solicitud GET en el punto de conexión `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="dc657-180">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="dc657-181">Esto devolverá una ubicación a la que se debe enviar la siguiente solicitud GET.</span><span class="sxs-lookup"><span data-stu-id="dc657-181">This will return a location to submit the next GET request to.</span></span>
* <span data-ttu-id="dc657-182">Después, envíe la solicitud GET en el punto de conexión `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="dc657-182">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="dc657-183">Se mostrará el contenido del archivo.</span><span class="sxs-lookup"><span data-stu-id="dc657-183">This will display the contents of the file.</span></span>

<span data-ttu-id="dc657-184">Sin embargo, como no existe ninguna diferencia en los parámetros de entrada entre el primer y el segundo paso, puede usar el parámetro `-L` para enviar la primera solicitud.</span><span class="sxs-lookup"><span data-stu-id="dc657-184">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span></span> <span data-ttu-id="dc657-185">`-L` combina dos solicitudes en una y provocará que cURL vuelva a realizar la solicitud en la nueva ubicación.</span><span class="sxs-lookup"><span data-stu-id="dc657-185">`-L` option essentially combines two requests into one and will make cURL redo the request on the new location.</span></span> <span data-ttu-id="dc657-186">Por último, se muestra el resultado de todas las llamadas de solicitud, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="dc657-186">Finally, the output from all the request calls is displayed, like shown below.</span></span> <span data-ttu-id="dc657-187">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc657-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="dc657-188">Debería ver una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc657-188">You should see an output similar to the following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="dc657-189">Cambiar el nombre de un archivo en una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc657-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="dc657-190">Esta operación se basa en la llamada de la API de REST de WebHDFS que se define [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="dc657-190">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="dc657-191">Para cambiar el nombre de un archivo, use el siguiente comando cURL.</span><span class="sxs-lookup"><span data-stu-id="dc657-191">Use the following cURL command to rename a file.</span></span> <span data-ttu-id="dc657-192">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc657-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="dc657-193">Debería ver una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc657-193">You should see an output similar to the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="dc657-194">Eliminar un archivo de una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc657-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="dc657-195">Esta operación se basa en la llamada de la API de REST de WebHDFS que se define [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="dc657-195">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="dc657-196">Para eliminar un archivo, use el siguiente comando cURL.</span><span class="sxs-lookup"><span data-stu-id="dc657-196">Use the following cURL command to delete a file.</span></span> <span data-ttu-id="dc657-197">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc657-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="dc657-198">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc657-198">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="dc657-199">Eliminar una cuenta del Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc657-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="dc657-200">Esta operación se basa en la llamada de la API de REST que se define [aquí](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc657-200">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="dc657-201">Use el siguiente comando cURL para eliminar la cuenta del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="dc657-201">Use the following cURL command to delete a Data Lake Store account.</span></span> <span data-ttu-id="dc657-202">Reemplace **\<yourstorename>** por el nombre de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc657-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="dc657-203">Debe ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc657-203">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="dc657-204">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="dc657-204">See also</span></span>
* [<span data-ttu-id="dc657-205">Abrir aplicaciones Big Data de origen que funcionan con el Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="dc657-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

