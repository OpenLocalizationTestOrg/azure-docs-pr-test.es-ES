---
title: "aaaGet a trabajar con búsqueda de Azure en Java | Documentos de Microsoft"
description: "¿Cómo toobuild una nube hospedada Buscar aplicación en Azure con Java como el lenguaje de programación."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="c5e90-103">Introducción a Búsqueda de Azure en Java</span><span class="sxs-lookup"><span data-stu-id="c5e90-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5e90-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c5e90-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="c5e90-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c5e90-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="c5e90-106">Obtenga información acerca de cómo buscar los toobuild personalizadas de Java en la aplicación que utiliza la búsqueda de Azure para su experiencia de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="c5e90-106">Learn how toobuild a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="c5e90-107">Este tutorial usa hello [API de REST de servicio de búsqueda de Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Hola objetos y operaciones que se usan en este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="c5e90-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="c5e90-108">toorun en este ejemplo, debe tener un servicio de búsqueda de Azure, que pueden suscribirse a Hola [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c5e90-108">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="c5e90-109">Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="c5e90-109">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="c5e90-110">Se usa Hola después toobuild de software y probar este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c5e90-110">We used hello following software toobuild and test this sample:</span></span>

* <span data-ttu-id="c5e90-111">[IDE de Eclipse para desarrolladores de Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="c5e90-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="c5e90-112">Ser seguro toodownload Hola EE versión.</span><span class="sxs-lookup"><span data-stu-id="c5e90-112">Be sure toodownload hello EE version.</span></span> <span data-ttu-id="c5e90-113">Uno de los pasos de comprobación de hello requiere una característica que se encuentra solo en esta edición.</span><span class="sxs-lookup"><span data-stu-id="c5e90-113">One of hello verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="c5e90-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="c5e90-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="c5e90-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="c5e90-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a><span data-ttu-id="c5e90-116">Acerca de los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="c5e90-116">About hello data</span></span>
<span data-ttu-id="c5e90-117">Esta aplicación de ejemplo utiliza datos de hello [servicios geológicas de Estados Unidos (USG)](http://geonames.usgs.gov/domestic/download_data.htm)y filtrado en el tamaño de conjunto de datos de hello estado de Rhode Island tooreduce Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-117">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="c5e90-118">Usaremos esta toobuild una aplicación de búsqueda que devuelve edificios de punto de referencia como hospitales y varios centros escolares, así como características geológicas como secuencias, lagos y cumbres de datos.</span><span class="sxs-lookup"><span data-stu-id="c5e90-118">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="c5e90-119">En esta aplicación, Hola **SearchServlet.java** programa genera y cargas Hola índice usando un [indizador](https://msdn.microsoft.com/library/azure/dn798918.aspx) construcción, recuperar Hola filtra USG conjunto de datos de una base de datos de SQL Azure pública.</span><span class="sxs-lookup"><span data-stu-id="c5e90-119">In this application, hello **SearchServlet.java** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="c5e90-120">Se proporcionan credenciales predefinidas y origen de datos en línea de toohello de información de conexión en el código de programa Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-120">Predefined credentials and connection  information toohello online data source are provided in hello program code.</span></span> <span data-ttu-id="c5e90-121">En términos de acceso a datos, no es necesario realizar ninguna otra configuración.</span><span class="sxs-lookup"><span data-stu-id="c5e90-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="c5e90-122">Se aplica un filtro en este toostay de conjunto de datos en límite del documento 10.000 Hola de hello libre de nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="c5e90-122">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="c5e90-123">Si usas nivel estándar de hello, este límite no se aplica, y puede modificar este toouse código un conjunto de datos más grande.</span><span class="sxs-lookup"><span data-stu-id="c5e90-123">If you use hello standard tier, this limit does not apply, and you can modify this code toouse a bigger dataset.</span></span> <span data-ttu-id="c5e90-124">Para obtener más información acerca de la capacidad de cada nivel de precios, consulte [Límites y restricciones](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="c5e90-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-hello-program-files"></a><span data-ttu-id="c5e90-125">Acerca de los archivos de programa Hola</span><span class="sxs-lookup"><span data-stu-id="c5e90-125">About hello program files</span></span>
<span data-ttu-id="c5e90-126">Hello lista siguiente describen los archivos de Hola que son relevantes toothis muestra.</span><span class="sxs-lookup"><span data-stu-id="c5e90-126">hello following list describes hello files that are relevant toothis sample.</span></span>

* <span data-ttu-id="c5e90-127">Search.jsp: Proporciona la interfaz de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="c5e90-127">Search.jsp: Provides hello user interface</span></span>
* <span data-ttu-id="c5e90-128">SearchServlet.java: Proporciona métodos (controlador de tooa similar en MVC)</span><span class="sxs-lookup"><span data-stu-id="c5e90-128">SearchServlet.java: Provides methods (similar tooa controller in MVC)</span></span>
* <span data-ttu-id="c5e90-129">SearchServiceClient.java: controla las solicitudes HTTP</span><span class="sxs-lookup"><span data-stu-id="c5e90-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="c5e90-130">SearchServiceHelper.java: clase auxiliar que proporciona métodos estáticos</span><span class="sxs-lookup"><span data-stu-id="c5e90-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="c5e90-131">Document.Java: Proporciona el modelo de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="c5e90-131">Document.java: Provides hello data model</span></span>
* <span data-ttu-id="c5e90-132">config.Properties: establece la dirección URL del servicio de búsqueda de Hola y clave de api</span><span class="sxs-lookup"><span data-stu-id="c5e90-132">config.properties: Sets hello Search service URL and api-key</span></span>
* <span data-ttu-id="c5e90-133">Pom.xml: una dependencia de Maven</span><span class="sxs-lookup"><span data-stu-id="c5e90-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="c5e90-134">Buscar el nombre del servicio de Hola y clave de api del servicio en la búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="c5e90-134">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="c5e90-135">Todas las llamadas de API de REST en búsqueda de Azure requieren que proporcione la dirección URL del servicio de hello y una clave de api.</span><span class="sxs-lookup"><span data-stu-id="c5e90-135">All REST API calls into Azure Search require that you provide hello service URL and an api-key.</span></span> 

1. <span data-ttu-id="c5e90-136">Inicie sesión en toohello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c5e90-136">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c5e90-137">En la barra de salto de hello, haga clic en **servicio de búsqueda** toolist todos los servicios de búsqueda de Azure Hola aprovisionados para su suscripción.</span><span class="sxs-lookup"><span data-stu-id="c5e90-137">In hello jump bar, click **Search service** toolist all of hello Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="c5e90-138">Seleccione servicio de Hola que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="c5e90-138">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="c5e90-139">En el panel de servicio de hello, podrá ver iconos para obtener información esencial, así como icono de llave hello para tener acceso a las claves de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-139">On hello service dashboard, you'll see tiles for essential information as well as hello key icon for accessing hello admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="c5e90-140">Copiar dirección URL del servicio de hello y una clave de administración.</span><span class="sxs-lookup"><span data-stu-id="c5e90-140">Copy hello service URL and an admin key.</span></span> <span data-ttu-id="c5e90-141">Los necesitará más adelante, cuando se agrega toohello **config.properties** archivo.</span><span class="sxs-lookup"><span data-stu-id="c5e90-141">You will need them later, when you add them toohello **config.properties** file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="c5e90-142">Descargar archivos de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="c5e90-142">Download hello sample files</span></span>
1. <span data-ttu-id="c5e90-143">Vaya demasiado[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c5e90-143">Go too[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="c5e90-144">Haga clic en **Download ZIP**, guardar toodisk de archivo .zip de hello y, a continuación, extraer todos los archivos de Hola que contiene.</span><span class="sxs-lookup"><span data-stu-id="c5e90-144">Click **Download ZIP**, save hello .zip file toodisk, and then extract all hello files it contains.</span></span> <span data-ttu-id="c5e90-145">Considere la posibilidad de extraer Hola proyecto de archivos en su toomake de área de trabajo de Java sea más fácil toofind hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="c5e90-145">Consider extracting hello files into your Java workspace toomake it easier toofind hello project later.</span></span>
3. <span data-ttu-id="c5e90-146">archivos de ejemplo de Hola son de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="c5e90-146">hello sample files are read-only.</span></span> <span data-ttu-id="c5e90-147">Haga clic en Propiedades de la carpeta y el atributo de solo lectura de hello desactive.</span><span class="sxs-lookup"><span data-stu-id="c5e90-147">Right-click folder properties and clear hello read-only attribute.</span></span>

<span data-ttu-id="c5e90-148">Todas las modificaciones y las instrucciones de ejecución subsiguientes se realizarán en los archivos de esta carpeta.</span><span class="sxs-lookup"><span data-stu-id="c5e90-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="c5e90-149">Importación del proyecto</span><span class="sxs-lookup"><span data-stu-id="c5e90-149">Import project</span></span>
1. <span data-ttu-id="c5e90-150">En Eclipse, elija **Archivo** > **Importar** > **General** > **Proyectos existentes al área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="c5e90-151">En **directorio raíz seleccione**, busque la carpeta toohello que contiene los archivos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c5e90-151">In **Select root directory**, browse toohello folder containing sample files.</span></span> <span data-ttu-id="c5e90-152">Seleccione la carpeta de Hola que contiene la carpeta de .project Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-152">Select hello folder that contains hello .project folder.</span></span> <span data-ttu-id="c5e90-153">proyecto de Hello debe aparecer en hello **proyectos** lista como un elemento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="c5e90-153">hello project should appear in hello **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="c5e90-154">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="c5e90-154">Click **Finish**.</span></span>
4. <span data-ttu-id="c5e90-155">Use **el Explorador de proyectos** tooview y editar archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-155">Use **Project Explorer** tooview and edit hello files.</span></span> <span data-ttu-id="c5e90-156">Si no está ya abierto, haga clic en **ventana** > **Mostrar vista** > **el Explorador de proyectos** o usar Hola contextual tooopen lo.</span><span class="sxs-lookup"><span data-stu-id="c5e90-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use hello shortcut tooopen it.</span></span>

## <a name="configure-hello-service-url-and-api-key"></a><span data-ttu-id="c5e90-157">Configurar la dirección URL del servicio de Hola y clave de api</span><span class="sxs-lookup"><span data-stu-id="c5e90-157">Configure hello service URL and api-key</span></span>
1. <span data-ttu-id="c5e90-158">En **el Explorador de proyectos**, haga doble clic en **config.properties** tooedit Hola configuración que contiene el nombre del servidor de Hola y clave de api.</span><span class="sxs-lookup"><span data-stu-id="c5e90-158">In **Project Explorer**, double-click **config.properties** tooedit hello configuration settings containing hello server name and api-key.</span></span>
2. <span data-ttu-id="c5e90-159">Consulte los pasos toohello anteriormente en este artículo, donde se encuentra Hola dirección URL del servicio y la clave de api en hello [Portal de Azure](https://portal.azure.com), valores de hello tooget ahora entrará en **config.properties**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-159">Refer toohello steps earlier in this article, where you found hello service URL and api-key in hello [Azure Portal](https://portal.azure.com), tooget hello values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="c5e90-160">En **config.properties**, reemplace "Clave de Api" con la clave de api de hello para el servicio.</span><span class="sxs-lookup"><span data-stu-id="c5e90-160">In **config.properties**, replace "Api Key" with hello api-key for your service.</span></span> <span data-ttu-id="c5e90-161">A continuación, el nombre de servicio (Hola primer componente de hello URL http://servicename.search.windows.net) reemplaza "nombre del servicio" Hola mismo archivo.</span><span class="sxs-lookup"><span data-stu-id="c5e90-161">Next, service name (hello first component of hello URL http://servicename.search.windows.net) replaces "service name" in hello same file.</span></span>
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a><span data-ttu-id="c5e90-162">Configurar entornos de proyecto de compilación y en tiempo de ejecución de Hola</span><span class="sxs-lookup"><span data-stu-id="c5e90-162">Configure hello project, build and runtime environments</span></span>
1. <span data-ttu-id="c5e90-163">En Eclipse, en el Explorador de proyectos, haga clic en proyecto de hello > **propiedades** > **proyecto facetas**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-163">In Eclipse, in Project Explorer, right-click hello project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="c5e90-164">Seleccione **Dynamic Web Module**, **Java** y **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="c5e90-165">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-165">Click **Apply**.</span></span>
4. <span data-ttu-id="c5e90-166">Seleccione **Ventana** > **Preferencias** > **Servidor** > **Entornos en tiempo de ejecución** > **Agregar...**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="c5e90-167">Expanda Apache y seleccione la versión de Hola de servidor de Apache Tomcat Hola que instaló anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c5e90-167">Expand Apache and select hello version of hello Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="c5e90-168">En nuestro sistema, se instala la versión 8.</span><span class="sxs-lookup"><span data-stu-id="c5e90-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="c5e90-169">En la página siguiente de hello, especifique el directorio de instalación de Tomcat Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-169">On hello next page, specify hello Tomcat installation directory.</span></span> <span data-ttu-id="c5e90-170">En un equipo Windows, probablemente será C:\Program Files\Apache Software Foundation\Tomcat *versión*.</span><span class="sxs-lookup"><span data-stu-id="c5e90-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="c5e90-171">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="c5e90-171">Click **Finish**.</span></span>
8. <span data-ttu-id="c5e90-172">Seleccione **Ventana** > **Preferencias** > **Java** > **JRE instalados** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="c5e90-173">En **Add JRE** (Agregar JRE), seleccione **Standard VM** (VM estándar).</span><span class="sxs-lookup"><span data-stu-id="c5e90-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="c5e90-174">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-174">Click **Next**.</span></span>
11. <span data-ttu-id="c5e90-175">En JRE Definition (Definición de JRE), en JRE home (Directorio de JRE), haga clic en **Directory**(Directorio).</span><span class="sxs-lookup"><span data-stu-id="c5e90-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="c5e90-176">Navegue demasiado**archivos de programa** > **Java** y seleccione Hola JDK que se instaló anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c5e90-176">Navigate too**Program Files** > **Java** and select hello JDK you previously installed.</span></span> <span data-ttu-id="c5e90-177">Es importante tooselect Hola JDK como Hola JRE.</span><span class="sxs-lookup"><span data-stu-id="c5e90-177">It's important tooselect hello JDK as hello JRE.</span></span>
13. <span data-ttu-id="c5e90-178">En versiones de JRE instalada, elija hello **JDK**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-178">In Installed JREs, choose hello **JDK**.</span></span> <span data-ttu-id="c5e90-179">La configuración debe tener un aspecto similar toohello siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="c5e90-179">Your settings should look similar toohello following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="c5e90-180">Si lo desea, seleccione **ventana** > **explorador Web** > **Internet Explorer** tooopen aplicación de hello en una ventana del explorador externo.</span><span class="sxs-lookup"><span data-stu-id="c5e90-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** tooopen hello application in an external browser window.</span></span> <span data-ttu-id="c5e90-181">Utilizar un explorador externo proporciona una mejor experiencia de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c5e90-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="c5e90-182">Ahora ha completado las tareas de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-182">You have now completed hello configuration tasks.</span></span> <span data-ttu-id="c5e90-183">A continuación, podrá crear y ejecutar el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-183">Next, you'll build and run hello project.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="c5e90-184">Compile el proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="c5e90-184">Build hello project</span></span>
1. <span data-ttu-id="c5e90-185">En el Explorador de proyectos, haga clic en el nombre del proyecto de Hola y elija **ejecución** > **compilación de Maven...**  tooconfigure proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-185">In Project Explorer, right-click hello project name and choose **Run As** > **Maven build...** tooconfigure hello project.</span></span>
   
    ![][10]
2. <span data-ttu-id="c5e90-186">En Edit Configuration (Editar configuración), en la sección Goals (Objetivos), escriba "clean install" y, a continuación, haga clic en **Run**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="c5e90-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="c5e90-187">Mensajes de estado son la ventana de la consola de salida toohello.</span><span class="sxs-lookup"><span data-stu-id="c5e90-187">Status messages are output toohello console window.</span></span> <span data-ttu-id="c5e90-188">Debería ver compilaciones correctas e indica Hola proyecto sin errores.</span><span class="sxs-lookup"><span data-stu-id="c5e90-188">You should see BUILD SUCCESS indicating hello project built without errors.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="c5e90-189">Ejecutar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="c5e90-189">Run hello app</span></span>
<span data-ttu-id="c5e90-190">En este último paso, ejecutará la aplicación hello en un entorno de tiempo de ejecución del servidor local.</span><span class="sxs-lookup"><span data-stu-id="c5e90-190">In this last step, you will run hello application in a local server runtime environment.</span></span>

<span data-ttu-id="c5e90-191">Si aún no ha especificado un entorno de tiempo de ejecución de servidor en Eclipse, necesitará toodo primero este último.</span><span class="sxs-lookup"><span data-stu-id="c5e90-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need toodo that first.</span></span>

1. <span data-ttu-id="c5e90-192">En Project Explorer, expanda **WebContent**(Contenido web).</span><span class="sxs-lookup"><span data-stu-id="c5e90-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="c5e90-193">Haga clic con el botón secundario en **Search.jsp** > **Ejecutar como** > **Ejecutar en el servidor**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="c5e90-194">Seleccione el servidor Apache Tomcat de hello y, a continuación, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-194">Select hello Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="c5e90-195">Si ha usado un área de trabajo no predeterminado toostore el proyecto, deberá toomodify **configuración de ejecución de** toopoint toohello proyecto ubicación tooavoid un error de inicio del servidor.</span><span class="sxs-lookup"><span data-stu-id="c5e90-195">If you used a non-default workspace toostore your project, you'll need toomodify **Run Configuration** toopoint toohello project location tooavoid a server start-up error.</span></span> <span data-ttu-id="c5e90-196">En el Explorador de proyectos, haga clic en **Search.jsp** > **Ejecutar como** > **Configuraciones de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="c5e90-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="c5e90-197">Seleccione el servidor de hello Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c5e90-197">Select hello Apache Tomcat server.</span></span> <span data-ttu-id="c5e90-198">Haga clic en **Arguments**(Argumentos).</span><span class="sxs-lookup"><span data-stu-id="c5e90-198">Click **Arguments**.</span></span> <span data-ttu-id="c5e90-199">Haga clic en **área de trabajo** o **sistema de archivos** tooset carpeta de Hola que contiene el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-199">Click **Workspace** or **File System** tooset hello folder containing hello project.</span></span>
> 
> 

<span data-ttu-id="c5e90-200">Cuando se ejecuta la aplicación hello, debería ver una ventana del explorador, que proporciona un cuadro de búsqueda para introducir términos.</span><span class="sxs-lookup"><span data-stu-id="c5e90-200">When you run hello application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="c5e90-201">Espere aproximadamente un minuto antes de hacer clic **búsqueda** toogive Hola servicio tiempo toocreate y carga Hola el índice.</span><span class="sxs-lookup"><span data-stu-id="c5e90-201">Wait about one minute before clicking **Search** toogive hello service time toocreate and load hello index.</span></span> <span data-ttu-id="c5e90-202">Si recibe un error HTTP 404, solo tiene toowait un poco más larga antes de intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c5e90-202">If you get an HTTP 404 error, you just need toowait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="c5e90-203">Buscar en los datos de USGS</span><span class="sxs-lookup"><span data-stu-id="c5e90-203">Search on USGS data</span></span>
<span data-ttu-id="c5e90-204">conjunto de datos de Hello USG incluye registros de estado toohello relevante de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="c5e90-204">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="c5e90-205">Si hace clic en **búsqueda** en un cuadro de búsqueda vacío, obtendrá entradas de 50 primeras hello, que es el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-205">If you click **Search** on an empty search box, you will get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="c5e90-206">Escriba un término de búsqueda le dará el motor de búsqueda de hello algo toogo en.</span><span class="sxs-lookup"><span data-stu-id="c5e90-206">Entering a search term will give hello search engine something toogo on.</span></span> <span data-ttu-id="c5e90-207">Pruebe a escribir un nombre regional.</span><span class="sxs-lookup"><span data-stu-id="c5e90-207">Try entering a regional name.</span></span> <span data-ttu-id="c5e90-208">"Roger Williams" era gobernador primera Hola de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="c5e90-208">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="c5e90-209">Hay numerosos parques, edificios y escuelas que llevan su nombre.</span><span class="sxs-lookup"><span data-stu-id="c5e90-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="c5e90-210">También puede probar con alguno de estos términos:</span><span class="sxs-lookup"><span data-stu-id="c5e90-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="c5e90-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="c5e90-211">Pawtucket</span></span>
* <span data-ttu-id="c5e90-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="c5e90-212">Pembroke</span></span>
* <span data-ttu-id="c5e90-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="c5e90-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5e90-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5e90-214">Next steps</span></span>
<span data-ttu-id="c5e90-215">Se trata del primer tutorial de búsqueda de Azure hello en función de hello USG dataset y Java.</span><span class="sxs-lookup"><span data-stu-id="c5e90-215">This is hello first Azure Search tutorial based on Java and hello USGS dataset.</span></span> <span data-ttu-id="c5e90-216">Con el tiempo, ampliaremos esta tutorial toodemonstrate características de búsqueda adicional puede toouse en sus soluciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="c5e90-216">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="c5e90-217">Si ya tiene conocimientos básicos en búsqueda de Azure, puede utilizar este ejemplo como un springboard para experimentación adicional, quizás aumentar hello [página de búsqueda](search-pagination-page-layout.md), o implementando [la navegación por facetas](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="c5e90-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting hello [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="c5e90-218">También puede mejorar en la página de resultados de búsqueda de hello agregando los recuentos y procesamiento por lotes de documentos para que los usuarios pueden desplazarse a través de los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5e90-218">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="c5e90-219">¿TooAzure nueva búsqueda?</span><span class="sxs-lookup"><span data-stu-id="c5e90-219">New tooAzure Search?</span></span> <span data-ttu-id="c5e90-220">Se recomienda intentar otra toodevelop tutoriales una descripción de lo que puede crear.</span><span class="sxs-lookup"><span data-stu-id="c5e90-220">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="c5e90-221">Visite nuestro [página de documentación](https://azure.microsoft.com/documentation/services/search/) toofind más recursos.</span><span class="sxs-lookup"><span data-stu-id="c5e90-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="c5e90-222">También puede ver los vínculos de hello en nuestro [lista de vídeo y un Tutorial](search-video-demo-tutorial-list.md) tooaccess obtener más información.</span><span class="sxs-lookup"><span data-stu-id="c5e90-222">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
