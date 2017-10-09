---
title: "aaaGet a trabajar con búsqueda de Azure en Node.js | Documentos de Microsoft"
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
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="1e0d6-103">Introducción a Azure Search en Node.js</span><span class="sxs-lookup"><span data-stu-id="1e0d6-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e0d6-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1e0d6-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="1e0d6-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1e0d6-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="1e0d6-106">Obtenga información acerca de cómo buscar los toobuild un Node.js personalizado en la aplicación que utiliza la búsqueda de Azure para su experiencia de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="1e0d6-107">Este tutorial usa hello [API de REST de servicio de búsqueda de Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Hola objetos y operaciones que se usan en este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="1e0d6-108">Utilizamos [Node.js](https://Nodejs.org) y NPM, [fundamentales 3 texto](http://www.sublimetext.com/3)y Windows PowerShell en Windows 8.1 toodevelop y pruebe este código.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="1e0d6-109">toorun en este ejemplo, debe tener un servicio de búsqueda de Azure, que pueden suscribirse a Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1e0d6-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1e0d6-110">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="1e0d6-111">Acerca de los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="1e0d6-111">About hello data</span></span>
<span data-ttu-id="1e0d6-112">Esta aplicación de ejemplo utiliza datos de hello [servicios geológicas de Estados Unidos (USG)](http://geonames.usgs.gov/domestic/download_data.htm)y filtrado en el tamaño de conjunto de datos de hello estado de Rhode Island tooreduce Hola.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="1e0d6-113">Usaremos esta toobuild una aplicación de búsqueda que devuelve edificios de punto de referencia como hospitales y varios centros escolares, así como características geológicas como secuencias, lagos y cumbres de datos.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="1e0d6-114">En esta aplicación, Hola **DataIndexer** programa genera y cargas Hola índice usando un [indizador](https://msdn.microsoft.com/library/azure/dn798918.aspx) construcción, recuperar Hola filtra USG conjunto de datos de una base de datos de SQL Azure pública.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="1e0d6-115">Las credenciales y conexión de origen de datos en línea de toohello de información se proporciona en el código de programa Hola.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="1e0d6-116">No es necesario realizar ninguna otra configuración.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="1e0d6-117">Se aplica un filtro en este toostay de conjunto de datos en límite del documento 10.000 Hola de hello libre de nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="1e0d6-118">Si utiliza el nivel estándar de hello, este límite no se aplica.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="1e0d6-119">Para obtener información más detallada sobre las características de cada plan de tarifa, consulte [Límites de servicio en la Búsqueda de Azure](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="1e0d6-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="1e0d6-120">Buscar el nombre del servicio de Hola y clave de api del servicio en la búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="1e0d6-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="1e0d6-121">Después de crear el servicio de hello, devolver toohello tooget portal Hola URL o `api-key`.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="1e0d6-122">Conexiones tooyour servicio de búsqueda requieren que tenga las URL de Hola y un `api-key` llamada de hello tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="1e0d6-123">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1e0d6-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1e0d6-124">En la barra de salto de hello, haga clic en **servicio de búsqueda** toolist todos los servicios de búsqueda de Azure aprovisionados para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="1e0d6-125">Seleccione servicio de Hola que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="1e0d6-126">En el panel de servicio de hello, debería ver iconos para obtener información esencial, como icono de llave hello para tener acceso a las claves de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="1e0d6-127">Copiar dirección URL del servicio de hello, una clave de administración y una clave de consulta.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="1e0d6-128">Necesita las tres más adelante al agregarlas toohello config.js archivo.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="1e0d6-129">Descargar archivos de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="1e0d6-129">Download hello sample files</span></span>
<span data-ttu-id="1e0d6-130">Use uno de hello según enfoques toodownload hello muestra.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="1e0d6-131">Vaya demasiado[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="1e0d6-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="1e0d6-132">Haga clic en **Download ZIP**, guarde el archivo .zip de hello y, a continuación, extraer todos los archivos de Hola que contiene.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="1e0d6-133">Todas las modificaciones y las instrucciones de ejecución del archivo posteriores se realizan en los archivos de esta carpeta.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="1e0d6-134">Actualizar config.js Hola.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-134">Update hello config.js.</span></span> <span data-ttu-id="1e0d6-135">con la dirección URL del servicio de búsqueda y la clave de API</span><span class="sxs-lookup"><span data-stu-id="1e0d6-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="1e0d6-136">Usar Hola dirección URL y la clave de api que copió anteriormente, especifique Hola dirección URL, clave de administración y la clave de consulta en el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="1e0d6-137">La clave de administración concede control total sobre las operaciones de servicio, incluidas la creación o eliminación de un índice y la carga de documentos.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="1e0d6-138">En cambio, las claves de consulta son para operaciones de solo lectura, que suelen usadas las aplicaciones de cliente que se conectan tooAzure búsqueda.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="1e0d6-139">En este ejemplo, se incluyen consultas de hello toohelp clave reforzar el procedimiento recomendado de hello del uso de clave de consulta de hello en aplicaciones cliente.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="1e0d6-140">Hola siguiente captura de pantalla muestra **config.js** abierto en un editor de texto, con hello las entradas pertinentes delimitadas para que puedan ver donde archivo de hello tooupdate con hello valores que son válidas para el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="1e0d6-141">Hospedar un entorno en tiempo de ejecución de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="1e0d6-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="1e0d6-142">ejemplo de Hola requiere un servidor HTTP, que se puede instalar mediante global npm.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="1e0d6-143">Utilice una ventana de PowerShell para hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="1e0d6-144">Desplazarse por las carpetas de toohello que contiene Hola **package.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="1e0d6-145">Escriba `npm install`.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-145">Type `npm install`.</span></span>
3. <span data-ttu-id="1e0d6-146">Escriba `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="1e0d6-147">Generar índice hello y ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="1e0d6-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="1e0d6-148">Escriba `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="1e0d6-149">Escriba `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="1e0d6-150">Escriba `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="1e0d6-151">Dirija el explorador a `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="1e0d6-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="1e0d6-152">Buscar en los datos de USGS</span><span class="sxs-lookup"><span data-stu-id="1e0d6-152">Search on USGS data</span></span>
<span data-ttu-id="1e0d6-153">conjunto de datos de Hello USG incluye registros de estado toohello relevante de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="1e0d6-154">Si hace clic en **búsqueda** en un cuadro de búsqueda vacío, obtendrá entradas de 50 primeras hello, que es el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="1e0d6-155">Escriba un término de búsqueda proporciona el motor de búsqueda de hello algo toogo en.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="1e0d6-156">Pruebe a escribir un nombre regional.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-156">Try entering a regional name.</span></span> <span data-ttu-id="1e0d6-157">"Roger Williams" era gobernador primera Hola de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="1e0d6-158">Hay numerosos parques, edificios y escuelas que llevan su nombre.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="1e0d6-159">También puede probar con alguno de estos términos:</span><span class="sxs-lookup"><span data-stu-id="1e0d6-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="1e0d6-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="1e0d6-160">Pawtucket</span></span>
* <span data-ttu-id="1e0d6-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="1e0d6-161">Pembroke</span></span>
* <span data-ttu-id="1e0d6-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="1e0d6-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e0d6-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e0d6-163">Next steps</span></span>
<span data-ttu-id="1e0d6-164">Se trata del primer tutorial de búsqueda de Azure hello en función de hello USG dataset y Node.js.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="1e0d6-165">Con el tiempo, ampliaremos esta tutorial toodemonstrate características de búsqueda adicional puede toouse en sus soluciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="1e0d6-166">Si ya tiene conocimientos sobre Búsqueda de Azure, puede usar este ejemplo como punto de partida para probar proveedores de sugerencias (escritura automática o autocompletar consultas), filtros y navegación por facetas.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="1e0d6-167">También puede mejorar en la página de resultados de búsqueda de hello agregando los recuentos y procesamiento por lotes de documentos para que los usuarios pueden desplazarse a través de los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="1e0d6-168">¿TooAzure nueva búsqueda?</span><span class="sxs-lookup"><span data-stu-id="1e0d6-168">New tooAzure Search?</span></span> <span data-ttu-id="1e0d6-169">Se recomienda intentar otra toodevelop tutoriales una descripción de lo que puede crear.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="1e0d6-170">Visite nuestro [página de documentación](https://azure.microsoft.com/documentation/services/search/) toofind más recursos.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="1e0d6-171">También puede ver los vínculos de hello en nuestro [lista de vídeo y un Tutorial](search-video-demo-tutorial-list.md) tooaccess obtener más información.</span><span class="sxs-lookup"><span data-stu-id="1e0d6-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
