---
title: "Introducción a Azure Search en Node.js | Microsoft Docs"
description: "Siga todos los pasos para realizar una aplicación de búsqueda en un servicio de búsqueda hospedado en la nube en Azure con Node.js como lenguaje de programación."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: 32865ed986f5eea961ef2c3813dcc6531498c90a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="6d923-103">Introducción a Azure Search en Node.js</span><span class="sxs-lookup"><span data-stu-id="6d923-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d923-104">Portal</span><span class="sxs-lookup"><span data-stu-id="6d923-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="6d923-105">.NET</span><span class="sxs-lookup"><span data-stu-id="6d923-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="6d923-106">Aprenda a compilar una aplicación de búsqueda personalizada en Node.js personalizada que utilice Azure Search para la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="6d923-106">Learn how to build a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="6d923-107">Este tutorial usa la [API de REST del servicio Búsqueda de Azure](https://msdn.microsoft.com/library/dn798935.aspx) para construir los objetos y las operaciones que se utilizan en este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="6d923-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="6d923-108">Hemos usado [Node.js](https://Nodejs.org) y NPM, [Sublime Text 3](http://www.sublimetext.com/3) y Windows PowerShell en Windows 8.1 para desarrollar y probar el código.</span><span class="sxs-lookup"><span data-stu-id="6d923-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 to develop and test this code.</span></span>

<span data-ttu-id="6d923-109">Para ejecutar este ejemplo, debe tener un servicio Azure Search, al que puede suscribirse en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6d923-109">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6d923-110">Para obtener instrucciones detalladas, consulte [Creación de un servicio Búsqueda de Azure en el Portal de Azure](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="6d923-110">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-the-data"></a><span data-ttu-id="6d923-111">Acerca de los datos</span><span class="sxs-lookup"><span data-stu-id="6d923-111">About the data</span></span>
<span data-ttu-id="6d923-112">Esta aplicación de ejemplo usa los datos del [Servicio geológico de Estados Unidos (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrados por el estado de Rhode Island para reducir el tamaño del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="6d923-112">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="6d923-113">Vamos a usar estos datos para crear una aplicación de búsqueda que devuelva edificios de referencia, como hospitales y escuelas, además de características geológicas como ríos, lagos y montes.</span><span class="sxs-lookup"><span data-stu-id="6d923-113">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="6d923-114">En esta aplicación, el programa **DataIndexer** compila y carga el índice usando una construcción [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) , y obtiene el conjunto de datos filtrado de USGS desde una base de datos SQL pública de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d923-114">In this application, the **DataIndexer** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="6d923-115">En el código del programa se proporcionan las credenciales y la información de conexión al origen de datos en línea.</span><span class="sxs-lookup"><span data-stu-id="6d923-115">Credentials and connection information to the online data source is provided in the program code.</span></span> <span data-ttu-id="6d923-116">No es necesario realizar ninguna otra configuración.</span><span class="sxs-lookup"><span data-stu-id="6d923-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="6d923-117">Se aplicó un filtro a este conjunto de datos para no sobrepasar el límite de 10.000 documentos del nivel de precios gratuito.</span><span class="sxs-lookup"><span data-stu-id="6d923-117">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="6d923-118">Si usa el nivel estándar, este límite no se aplica.</span><span class="sxs-lookup"><span data-stu-id="6d923-118">If you use the standard tier, this limit does not apply.</span></span> <span data-ttu-id="6d923-119">Para obtener información más detallada sobre las características de cada plan de tarifa, consulte [Límites de servicio en la Búsqueda de Azure](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="6d923-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="6d923-120">Buscar el nombre del servicio y la clave de API del servicio Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="6d923-120">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="6d923-121">Después de crear el servicio, vuelva al portal para obtener la dirección URL o la `api-key`.</span><span class="sxs-lookup"><span data-stu-id="6d923-121">After you create the service, return to the portal to get the URL or `api-key`.</span></span> <span data-ttu-id="6d923-122">Las conexiones con el servicio de búsqueda requieren que tenga la URL y una `api-key` para autenticar la llamada.</span><span class="sxs-lookup"><span data-stu-id="6d923-122">Connections to your Search service require that you have both the URL and an `api-key` to authenticate the call.</span></span>

1. <span data-ttu-id="6d923-123">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6d923-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6d923-124">En la barra de acceso rápido, haga clic en **Servicio de búsqueda** para enumerar todos los servicios de Azure Search aprovisionados para la suscripción.</span><span class="sxs-lookup"><span data-stu-id="6d923-124">In the jump bar, click **Search service** to list all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="6d923-125">Seleccione el servicio que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="6d923-125">Select the service you want to use.</span></span>
4. <span data-ttu-id="6d923-126">En el panel del servicio verá iconos con información esencial, como el icono de la llave para acceder a las claves de administrador.</span><span class="sxs-lookup"><span data-stu-id="6d923-126">On the service dashboard, you should see tiles for essential information, such as the key icon for accessing the admin keys.</span></span>
5. <span data-ttu-id="6d923-127">Copie la dirección URL del servicio, una clave de administración y una clave de consulta.</span><span class="sxs-lookup"><span data-stu-id="6d923-127">Copy the service URL, an admin key, and a query key.</span></span> <span data-ttu-id="6d923-128">Necesitará las tres más adelante para agregarlas al archivo config.js.</span><span class="sxs-lookup"><span data-stu-id="6d923-128">You need all three later when you add them to the config.js file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="6d923-129">Descarga de los archivos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d923-129">Download the sample files</span></span>
<span data-ttu-id="6d923-130">Use uno de los siguientes métodos para descargar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6d923-130">Use either one of the following approaches to download the sample.</span></span>

1. <span data-ttu-id="6d923-131">Vaya a [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="6d923-131">Go to [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="6d923-132">Haga clic en **Download ZIP**, guarde el archivo .zip y extraiga todos los archivos que contiene.</span><span class="sxs-lookup"><span data-stu-id="6d923-132">Click **Download ZIP**, save the .zip file, and then extract all the files it contains.</span></span>

<span data-ttu-id="6d923-133">Todas las modificaciones y las instrucciones de ejecución del archivo posteriores se realizan en los archivos de esta carpeta.</span><span class="sxs-lookup"><span data-stu-id="6d923-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-the-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="6d923-134">Actualización del archivo config.js.</span><span class="sxs-lookup"><span data-stu-id="6d923-134">Update the config.js.</span></span> <span data-ttu-id="6d923-135">con la dirección URL del servicio de búsqueda y la clave de API</span><span class="sxs-lookup"><span data-stu-id="6d923-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="6d923-136">Utilizando la dirección URL y la api-key que copió anteriormente, especifique la dirección URL, la clave de administración y la clave de consulta en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="6d923-136">Using the URL and api-key that you copied earlier, specify the URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="6d923-137">La clave de administración concede control total sobre las operaciones de servicio, incluidas la creación o eliminación de un índice y la carga de documentos.</span><span class="sxs-lookup"><span data-stu-id="6d923-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="6d923-138">En cambio, las claves de consulta son para operaciones de solo lectura, utilizadas normalmente por las aplicaciones cliente que se conectan a Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d923-138">In contrast, query keys are for read-only operations, typically used by client applications that connect to Azure Search.</span></span>

<span data-ttu-id="6d923-139">En este ejemplo, se incluye la clave de consulta para ayudar a reforzar la práctica recomendada de usar la clave de consulta en aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="6d923-139">In this sample, we include the query key to help reinforce the best practice of using the query key in client applications.</span></span>

<span data-ttu-id="6d923-140">La siguiente captura de pantalla muestra el archivo **config.js** abierto en un editor de texto, con las entradas pertinentes enmarcadas para que pueda ver dónde actualizar el archivo con los valores válidos para el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="6d923-140">The following screenshot shows **config.js** open in a text editor, with the relevant entries demarcated so that you can see where to update the file with the values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-the-sample"></a><span data-ttu-id="6d923-141">Hospedar un entorno de tiempo de ejecución para el ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d923-141">Host a runtime environment for the sample</span></span>
<span data-ttu-id="6d923-142">El ejemplo requiere un servidor HTTP, que puede instalar globalmente mediante npm.</span><span class="sxs-lookup"><span data-stu-id="6d923-142">The sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="6d923-143">Ejecute los comandos siguientes en una ventana de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d923-143">Use a PowerShell window for the following commands.</span></span>

1. <span data-ttu-id="6d923-144">Navegue hasta la carpeta que contiene el archivo **package.json** .</span><span class="sxs-lookup"><span data-stu-id="6d923-144">Navigate to the folder that contains the **package.json** file.</span></span>
2. <span data-ttu-id="6d923-145">Escriba `npm install`.</span><span class="sxs-lookup"><span data-stu-id="6d923-145">Type `npm install`.</span></span>
3. <span data-ttu-id="6d923-146">Escriba `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="6d923-146">Type `npm install -g http-server`.</span></span>

## <a name="build-the-index-and-run-the-application"></a><span data-ttu-id="6d923-147">Compilación del índice y ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="6d923-147">Build the index and run the application</span></span>
1. <span data-ttu-id="6d923-148">Escriba `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="6d923-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="6d923-149">Escriba `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="6d923-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="6d923-150">Escriba `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="6d923-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="6d923-151">Dirija el explorador a `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="6d923-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="6d923-152">Buscar en los datos de USGS</span><span class="sxs-lookup"><span data-stu-id="6d923-152">Search on USGS data</span></span>
<span data-ttu-id="6d923-153">El conjunto de datos de USGS incluye los registros que son relevantes para el estado de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="6d923-153">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="6d923-154">Si hace clic en **Search** en un cuadro de búsqueda vacío, obtiene las 50 primeras entradas (es el valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="6d923-154">If you click **Search** on an empty search box, you get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="6d923-155">Al escribir un término de búsqueda se da al motor de búsqueda algo con qué trabajar.</span><span class="sxs-lookup"><span data-stu-id="6d923-155">Entering a search term gives the search engine something to go on.</span></span> <span data-ttu-id="6d923-156">Pruebe a escribir un nombre regional.</span><span class="sxs-lookup"><span data-stu-id="6d923-156">Try entering a regional name.</span></span> <span data-ttu-id="6d923-157">"Roger Williams" fue el primer gobernador de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="6d923-157">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="6d923-158">Hay numerosos parques, edificios y escuelas que llevan su nombre.</span><span class="sxs-lookup"><span data-stu-id="6d923-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="6d923-159">También puede probar con alguno de estos términos:</span><span class="sxs-lookup"><span data-stu-id="6d923-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="6d923-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="6d923-160">Pawtucket</span></span>
* <span data-ttu-id="6d923-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="6d923-161">Pembroke</span></span>
* <span data-ttu-id="6d923-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="6d923-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d923-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d923-163">Next steps</span></span>
<span data-ttu-id="6d923-164">Este es el primer tutorial de Azure Search basado en Node.js y en el conjunto de datos de USGS.</span><span class="sxs-lookup"><span data-stu-id="6d923-164">This is the first Azure Search tutorial based on Node.js and the USGS dataset.</span></span> <span data-ttu-id="6d923-165">Con el tiempo, ampliaremos este tutorial para mostrar otras características de búsqueda que podría querer usar en sus soluciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="6d923-165">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="6d923-166">Si ya tiene conocimientos sobre Búsqueda de Azure, puede usar este ejemplo como punto de partida para probar proveedores de sugerencias (escritura automática o autocompletar consultas), filtros y navegación por facetas.</span><span class="sxs-lookup"><span data-stu-id="6d923-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="6d923-167">También puede mejorar la página de resultados de búsqueda si agrega recuentos y procesamiento por lotes de documentos para que los usuarios puedan navegar por las páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="6d923-167">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="6d923-168">¿Es la primera vez que usa Búsqueda de Azure?</span><span class="sxs-lookup"><span data-stu-id="6d923-168">New to Azure Search?</span></span> <span data-ttu-id="6d923-169">Le recomendamos que pruebe otros tutoriales para comprender mejor lo que puede crear.</span><span class="sxs-lookup"><span data-stu-id="6d923-169">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="6d923-170">Visite nuestra [página de documentación](https://azure.microsoft.com/documentation/services/search/) para encontrar más recursos.</span><span class="sxs-lookup"><span data-stu-id="6d923-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="6d923-171">También puede ver los vínculos en nuestra [lista de vídeos y tutoriales](search-video-demo-tutorial-list.md) para tener acceso a más información.</span><span class="sxs-lookup"><span data-stu-id="6d923-171">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
