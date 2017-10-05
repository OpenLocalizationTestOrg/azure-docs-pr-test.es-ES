---
title: "Introducción a Azure Search en Java | Microsoft Docs"
description: "Cómo crear una aplicación de búsqueda hospedada en la nube en Azure con Java como lenguaje de programación."
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
ms.openlocfilehash: f6ca06a0349def97b38a1bf6d0d8f36236077e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="3cc13-103">Introducción a Búsqueda de Azure en Java</span><span class="sxs-lookup"><span data-stu-id="3cc13-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3cc13-104">Portal</span><span class="sxs-lookup"><span data-stu-id="3cc13-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="3cc13-105">.NET</span><span class="sxs-lookup"><span data-stu-id="3cc13-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="3cc13-106">Aprenda a crear una aplicación de búsqueda de Java personalizada que utiliza Búsqueda de Azure para la experiencia de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="3cc13-106">Learn how to build a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="3cc13-107">Este tutorial usa la [API de REST del servicio Búsqueda de Azure](https://msdn.microsoft.com/library/dn798935.aspx) para construir los objetos y las operaciones que se utilizan en este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="3cc13-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="3cc13-108">Para ejecutar este ejemplo, debe tener un servicio Búsqueda de Azure, al que puede suscribirse en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3cc13-108">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="3cc13-109">Para obtener instrucciones detalladas, consulte [Creación de un servicio Búsqueda de Azure en el Portal de Azure](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="3cc13-109">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="3cc13-110">Hemos usado el siguiente software para compilar y probar este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3cc13-110">We used the following software to build and test this sample:</span></span>

* <span data-ttu-id="3cc13-111">[IDE de Eclipse para desarrolladores de Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="3cc13-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="3cc13-112">Asegúrese de descargar la versión EE.</span><span class="sxs-lookup"><span data-stu-id="3cc13-112">Be sure to download the EE version.</span></span> <span data-ttu-id="3cc13-113">Uno de los pasos de comprobación requiere una característica que solo se encuentra en esta edición.</span><span class="sxs-lookup"><span data-stu-id="3cc13-113">One of the verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="3cc13-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="3cc13-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="3cc13-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="3cc13-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-the-data"></a><span data-ttu-id="3cc13-116">Acerca de los datos</span><span class="sxs-lookup"><span data-stu-id="3cc13-116">About the data</span></span>
<span data-ttu-id="3cc13-117">Esta aplicación de ejemplo usa los datos del [Servicio geológico de Estados Unidos (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrados por el estado de Rhode Island para reducir el tamaño del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="3cc13-117">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="3cc13-118">Vamos a usar estos datos para crear una aplicación de búsqueda que devuelva edificios de referencia como hospitales y escuelas, además de características geológicas como ríos, lagos y montes.</span><span class="sxs-lookup"><span data-stu-id="3cc13-118">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="3cc13-119">En esta aplicación, el programa **SearchServlet.java** compila y carga el índice utilizando un constructo de [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) y obtiene el conjunto de datos filtrado de USGS desde una base de datos SQL pública de Azure.</span><span class="sxs-lookup"><span data-stu-id="3cc13-119">In this application, the **SearchServlet.java** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="3cc13-120">En el código del programa se proporcionan credenciales predefinidas e información de conexión al origen de datos en línea.</span><span class="sxs-lookup"><span data-stu-id="3cc13-120">Predefined credentials and connection  information to the online data source are provided in the program code.</span></span> <span data-ttu-id="3cc13-121">En términos de acceso a datos, no es necesario realizar ninguna otra configuración.</span><span class="sxs-lookup"><span data-stu-id="3cc13-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="3cc13-122">Se aplicó un filtro a este conjunto de datos para no sobrepasar el límite de 10.000 documentos del nivel de precios gratuito.</span><span class="sxs-lookup"><span data-stu-id="3cc13-122">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="3cc13-123">Si utiliza el nivel estándar, este límite no se aplica y puede modificar el código para utilizar un conjunto de datos más grande.</span><span class="sxs-lookup"><span data-stu-id="3cc13-123">If you use the standard tier, this limit does not apply, and you can modify this code to use a bigger dataset.</span></span> <span data-ttu-id="3cc13-124">Para obtener más información acerca de la capacidad de cada nivel de precios, consulte [Límites y restricciones](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="3cc13-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-the-program-files"></a><span data-ttu-id="3cc13-125">Acerca de los archivos del programa</span><span class="sxs-lookup"><span data-stu-id="3cc13-125">About the program files</span></span>
<span data-ttu-id="3cc13-126">La lista siguiente describe los archivos que son relevantes para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3cc13-126">The following list describes the files that are relevant to this sample.</span></span>

* <span data-ttu-id="3cc13-127">Search.jsp: proporciona la interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="3cc13-127">Search.jsp: Provides the user interface</span></span>
* <span data-ttu-id="3cc13-128">SearchServlet.java: proporciona métodos (similar a un controlador de MVC)</span><span class="sxs-lookup"><span data-stu-id="3cc13-128">SearchServlet.java: Provides methods (similar to a controller in MVC)</span></span>
* <span data-ttu-id="3cc13-129">SearchServiceClient.java: controla las solicitudes HTTP</span><span class="sxs-lookup"><span data-stu-id="3cc13-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="3cc13-130">SearchServiceHelper.java: clase auxiliar que proporciona métodos estáticos</span><span class="sxs-lookup"><span data-stu-id="3cc13-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="3cc13-131">Document.java: proporciona el modelo de datos</span><span class="sxs-lookup"><span data-stu-id="3cc13-131">Document.java: Provides the data model</span></span>
* <span data-ttu-id="3cc13-132">config.properties: establece la dirección URL del servicio de búsqueda y la clave de API</span><span class="sxs-lookup"><span data-stu-id="3cc13-132">config.properties: Sets the Search service URL and api-key</span></span>
* <span data-ttu-id="3cc13-133">Pom.xml: una dependencia de Maven</span><span class="sxs-lookup"><span data-stu-id="3cc13-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="3cc13-134">Buscar el nombre del servicio y la clave de API del servicio Búsqueda de Azure</span><span class="sxs-lookup"><span data-stu-id="3cc13-134">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="3cc13-135">Todas las llamadas de API de REST en Búsqueda de Azure requieren que proporcione la dirección URL del servicio y una clave de API.</span><span class="sxs-lookup"><span data-stu-id="3cc13-135">All REST API calls into Azure Search require that you provide the service URL and an api-key.</span></span> 

1. <span data-ttu-id="3cc13-136">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3cc13-136">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3cc13-137">En la barra de acceso rápido, haga clic en **Servicio de búsqueda** para enumerar todos los servicios de Búsqueda de Azure aprovisionados para la suscripción.</span><span class="sxs-lookup"><span data-stu-id="3cc13-137">In the jump bar, click **Search service** to list all of the Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="3cc13-138">Seleccione el servicio que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="3cc13-138">Select the service you want to use.</span></span>
4. <span data-ttu-id="3cc13-139">En el panel del servicio verá mosaicos con información esencial, así como el icono de llave para tener acceso a las claves de administrador.</span><span class="sxs-lookup"><span data-stu-id="3cc13-139">On the service dashboard, you'll see tiles for essential information as well as the key icon for accessing the admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="3cc13-140">Copie la dirección URL del servicio y una clave de administración.</span><span class="sxs-lookup"><span data-stu-id="3cc13-140">Copy the service URL and an admin key.</span></span> <span data-ttu-id="3cc13-141">Las necesitará más adelante para agregarlas al archivo **config.properties** .</span><span class="sxs-lookup"><span data-stu-id="3cc13-141">You will need them later, when you add them to the **config.properties** file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="3cc13-142">Descarga de los archivos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3cc13-142">Download the sample files</span></span>
1. <span data-ttu-id="3cc13-143">Vaya a [AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="3cc13-143">Go to [AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="3cc13-144">Haga clic en **Download ZIP**, guarde el archivo .zip en el disco y extraiga todos los archivos que contiene.</span><span class="sxs-lookup"><span data-stu-id="3cc13-144">Click **Download ZIP**, save the .zip file to disk, and then extract all the files it contains.</span></span> <span data-ttu-id="3cc13-145">Es recomendable que extraiga los archivos en su área de trabajo de Java para que le resulte más fácil encontrar el proyecto más adelante.</span><span class="sxs-lookup"><span data-stu-id="3cc13-145">Consider extracting the files into your Java workspace to make it easier to find the project later.</span></span>
3. <span data-ttu-id="3cc13-146">Los archivos de ejemplo son de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="3cc13-146">The sample files are read-only.</span></span> <span data-ttu-id="3cc13-147">Haga clic con el botón secundario en las propiedades de la carpeta y borre el atributo de sólo lectura.</span><span class="sxs-lookup"><span data-stu-id="3cc13-147">Right-click folder properties and clear the read-only attribute.</span></span>

<span data-ttu-id="3cc13-148">Todas las modificaciones y las instrucciones de ejecución subsiguientes se realizarán en los archivos de esta carpeta.</span><span class="sxs-lookup"><span data-stu-id="3cc13-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="3cc13-149">Importación del proyecto</span><span class="sxs-lookup"><span data-stu-id="3cc13-149">Import project</span></span>
1. <span data-ttu-id="3cc13-150">En Eclipse, elija **Archivo** > **Importar** > **General** > **Proyectos existentes al área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="3cc13-151">En **Select root directory**(Seleccionar directorio raíz), vaya a la carpeta que contiene los archivos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3cc13-151">In **Select root directory**, browse to the folder containing sample files.</span></span> <span data-ttu-id="3cc13-152">Seleccione la carpeta que contiene la carpeta .project.</span><span class="sxs-lookup"><span data-stu-id="3cc13-152">Select the folder that contains the .project folder.</span></span> <span data-ttu-id="3cc13-153">El proyecto debe aparecer en la lista **Projects** (Proyectos) como elemento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="3cc13-153">The project should appear in the **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="3cc13-154">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="3cc13-154">Click **Finish**.</span></span>
4. <span data-ttu-id="3cc13-155">Utilice **Project Explorer** (Explorador de proyectos) para ver y editar los archivos.</span><span class="sxs-lookup"><span data-stu-id="3cc13-155">Use **Project Explorer** to view and edit the files.</span></span> <span data-ttu-id="3cc13-156">Si aún no está abierto, haga clic en **Ventana** > **Mostrar vista** > **Explorador de proyectos** o use el método abreviado para abrirlo.</span><span class="sxs-lookup"><span data-stu-id="3cc13-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use the shortcut to open it.</span></span>

## <a name="configure-the-service-url-and-api-key"></a><span data-ttu-id="3cc13-157">Configuración de la dirección URL del servicio y api-key</span><span class="sxs-lookup"><span data-stu-id="3cc13-157">Configure the service URL and api-key</span></span>
1. <span data-ttu-id="3cc13-158">En **Project Explorer** (Explorador de proyectos), haga doble clic en **config.properties** para editar los valores de configuración que contienen el nombre del servidor y la clave de API.</span><span class="sxs-lookup"><span data-stu-id="3cc13-158">In **Project Explorer**, double-click **config.properties** to edit the configuration settings containing the server name and api-key.</span></span>
2. <span data-ttu-id="3cc13-159">Consulte los pasos anteriores de este artículo, donde encontró la dirección URL del servicio y la clave de API en el [Portal de Azure](https://portal.azure.com), para obtener los valores que va a especificar en **config.properties**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-159">Refer to the steps earlier in this article, where you found the service URL and api-key in the [Azure Portal](https://portal.azure.com), to get the values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="3cc13-160">En **config.properties**, reemplace "Api Key" con la clave de API del servicio.</span><span class="sxs-lookup"><span data-stu-id="3cc13-160">In **config.properties**, replace "Api Key" with the api-key for your service.</span></span> <span data-ttu-id="3cc13-161">A continuación, utilice el nombre de servicio (el primer componente de la dirección URL http://servicename.search.windows.net) para reemplazar "service name" en el mismo archivo.</span><span class="sxs-lookup"><span data-stu-id="3cc13-161">Next, service name (the first component of the URL http://servicename.search.windows.net) replaces "service name" in the same file.</span></span>
   
    ![][5]

## <a name="configure-the-project-build-and-runtime-environments"></a><span data-ttu-id="3cc13-162">Configuración de los entornos de proyecto, compilación y tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="3cc13-162">Configure the project, build and runtime environments</span></span>
1. <span data-ttu-id="3cc13-163">En Eclipse, en Project Explorer, haga clic con el botón secundario en el proyecto > **Propiedades** > **Facetas del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-163">In Eclipse, in Project Explorer, right-click the project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="3cc13-164">Seleccione **Dynamic Web Module**, **Java** y **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="3cc13-165">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-165">Click **Apply**.</span></span>
4. <span data-ttu-id="3cc13-166">Seleccione **Ventana** > **Preferencias** > **Servidor** > **Entornos en tiempo de ejecución** > **Agregar...**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="3cc13-167">Expanda Apache y seleccione la versión del servidor Apache Tomcat que ha instalado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3cc13-167">Expand Apache and select the version of the Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="3cc13-168">En nuestro sistema, se instala la versión 8.</span><span class="sxs-lookup"><span data-stu-id="3cc13-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="3cc13-169">En la página siguiente, especifique el directorio de instalación de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="3cc13-169">On the next page, specify the Tomcat installation directory.</span></span> <span data-ttu-id="3cc13-170">En un equipo Windows, probablemente será C:\Program Files\Apache Software Foundation\Tomcat *versión*.</span><span class="sxs-lookup"><span data-stu-id="3cc13-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="3cc13-171">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="3cc13-171">Click **Finish**.</span></span>
8. <span data-ttu-id="3cc13-172">Seleccione **Ventana** > **Preferencias** > **Java** > **JRE instalados** > **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="3cc13-173">En **Add JRE** (Agregar JRE), seleccione **Standard VM** (VM estándar).</span><span class="sxs-lookup"><span data-stu-id="3cc13-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="3cc13-174">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-174">Click **Next**.</span></span>
11. <span data-ttu-id="3cc13-175">En JRE Definition (Definición de JRE), en JRE home (Directorio de JRE), haga clic en **Directory**(Directorio).</span><span class="sxs-lookup"><span data-stu-id="3cc13-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="3cc13-176">Vaya a **Archivos de programa** > **Java** y seleccione el JDK instalado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3cc13-176">Navigate to **Program Files** > **Java** and select the JDK you previously installed.</span></span> <span data-ttu-id="3cc13-177">Es importante seleccionar el JDK como JRE.</span><span class="sxs-lookup"><span data-stu-id="3cc13-177">It's important to select the JDK as the JRE.</span></span>
13. <span data-ttu-id="3cc13-178">En Installed JREs, elija el **JDK**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-178">In Installed JREs, choose the **JDK**.</span></span> <span data-ttu-id="3cc13-179">Su configuración debería ser similar a la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="3cc13-179">Your settings should look similar to the following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="3cc13-180">Opcionalmente, seleccione **Ventana** > **Explorador web** > **Internet Explorer** para abrir la aplicación en una ventana del explorador externo.</span><span class="sxs-lookup"><span data-stu-id="3cc13-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** to open the application in an external browser window.</span></span> <span data-ttu-id="3cc13-181">Utilizar un explorador externo proporciona una mejor experiencia de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3cc13-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="3cc13-182">Ahora ha completado las tareas de configuración.</span><span class="sxs-lookup"><span data-stu-id="3cc13-182">You have now completed the configuration tasks.</span></span> <span data-ttu-id="3cc13-183">A continuación, podrá compilar y ejecutar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3cc13-183">Next, you'll build and run the project.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="3cc13-184">Compilación del proyecto</span><span class="sxs-lookup"><span data-stu-id="3cc13-184">Build the project</span></span>
1. <span data-ttu-id="3cc13-185">En el Explorador de proyectos, haga clic con el botón secundario en el nombre del proyecto y elija **Ejecutar como** > **Compilación de Maven...** para configurar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3cc13-185">In Project Explorer, right-click the project name and choose **Run As** > **Maven build...** to configure the project.</span></span>
   
    ![][10]
2. <span data-ttu-id="3cc13-186">En Edit Configuration (Editar configuración), en la sección Goals (Objetivos), escriba "clean install" y, a continuación, haga clic en **Run**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="3cc13-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="3cc13-187">Los mensajes de estado se envían a la ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="3cc13-187">Status messages are output to the console window.</span></span> <span data-ttu-id="3cc13-188">Debería ver BUILD SUCCESS, lo que indica que el proyecto se ha compilado sin errores.</span><span class="sxs-lookup"><span data-stu-id="3cc13-188">You should see BUILD SUCCESS indicating the project built without errors.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="3cc13-189">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="3cc13-189">Run the app</span></span>
<span data-ttu-id="3cc13-190">En este último paso, ejecutará la aplicación en un entorno de tiempo de ejecución del servidor local.</span><span class="sxs-lookup"><span data-stu-id="3cc13-190">In this last step, you will run the application in a local server runtime environment.</span></span>

<span data-ttu-id="3cc13-191">Si todavía no ha especificado un entorno de tiempo de ejecución del servidor en Eclipse, deberá hacerlo en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="3cc13-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need to do that first.</span></span>

1. <span data-ttu-id="3cc13-192">En Project Explorer, expanda **WebContent**(Contenido web).</span><span class="sxs-lookup"><span data-stu-id="3cc13-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="3cc13-193">Haga clic con el botón secundario en **Search.jsp** > **Ejecutar como** > **Ejecutar en el servidor**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="3cc13-194">Seleccione el servidor Apache Tomcat y, a continuación, haga clic en **Run**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="3cc13-194">Select the Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="3cc13-195">Si ha usado un área de trabajo distinta de la predeterminada para almacenar el proyecto, tendrá que modificar **Configuración de ejecución** para que apunte a la ubicación del proyecto y evitar un error de inicio del servidor.</span><span class="sxs-lookup"><span data-stu-id="3cc13-195">If you used a non-default workspace to store your project, you'll need to modify **Run Configuration** to point to the project location to avoid a server start-up error.</span></span> <span data-ttu-id="3cc13-196">En el Explorador de proyectos, haga clic en **Search.jsp** > **Ejecutar como** > **Configuraciones de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="3cc13-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="3cc13-197">Seleccione el servidor Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="3cc13-197">Select the Apache Tomcat server.</span></span> <span data-ttu-id="3cc13-198">Haga clic en **Arguments**(Argumentos).</span><span class="sxs-lookup"><span data-stu-id="3cc13-198">Click **Arguments**.</span></span> <span data-ttu-id="3cc13-199">Haga clic en **Workspace** (Área de trabajo) o en **File System** (Sistema de archivos) para definir la carpeta que contiene el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3cc13-199">Click **Workspace** or **File System** to set the folder containing the project.</span></span>
> 
> 

<span data-ttu-id="3cc13-200">Al ejecutar la aplicación, aparecerá una ventana del explorador que ofrece un cuadro de búsqueda para introducir términos.</span><span class="sxs-lookup"><span data-stu-id="3cc13-200">When you run the application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="3cc13-201">Aguarde un minuto antes de hacer clic en **Search** (Buscar) para que el servicio tenga tiempo de crear y cargar el índice.</span><span class="sxs-lookup"><span data-stu-id="3cc13-201">Wait about one minute before clicking **Search** to give the service time to create and load the index.</span></span> <span data-ttu-id="3cc13-202">Si obtiene un error HTTP 404, sólo necesitará esperar un poco más antes de intentarlo.</span><span class="sxs-lookup"><span data-stu-id="3cc13-202">If you get an HTTP 404 error, you just need to wait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="3cc13-203">Buscar en los datos de USGS</span><span class="sxs-lookup"><span data-stu-id="3cc13-203">Search on USGS data</span></span>
<span data-ttu-id="3cc13-204">El conjunto de datos de USGS incluye los registros que son relevantes para el estado de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="3cc13-204">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="3cc13-205">Si hace clic en **Search** en un cuadro de búsqueda vacío, obtendrá las 50 primeras entradas (es el valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="3cc13-205">If you click **Search** on an empty search box, you will get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="3cc13-206">Escriba un término de búsqueda para que el motor de búsqueda tenga con qué trabajar.</span><span class="sxs-lookup"><span data-stu-id="3cc13-206">Entering a search term will give the search engine something to go on.</span></span> <span data-ttu-id="3cc13-207">Pruebe a escribir un nombre regional.</span><span class="sxs-lookup"><span data-stu-id="3cc13-207">Try entering a regional name.</span></span> <span data-ttu-id="3cc13-208">"Roger Williams" fue el primer gobernador de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="3cc13-208">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="3cc13-209">Hay numerosos parques, edificios y escuelas que llevan su nombre.</span><span class="sxs-lookup"><span data-stu-id="3cc13-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="3cc13-210">También puede probar con alguno de estos términos:</span><span class="sxs-lookup"><span data-stu-id="3cc13-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="3cc13-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="3cc13-211">Pawtucket</span></span>
* <span data-ttu-id="3cc13-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="3cc13-212">Pembroke</span></span>
* <span data-ttu-id="3cc13-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="3cc13-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cc13-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3cc13-214">Next steps</span></span>
<span data-ttu-id="3cc13-215">Este es el primer tutorial de Búsqueda de Azure basada en Java y en el conjunto de datos de USGS.</span><span class="sxs-lookup"><span data-stu-id="3cc13-215">This is the first Azure Search tutorial based on Java and the USGS dataset.</span></span> <span data-ttu-id="3cc13-216">Con el tiempo, ampliaremos este tutorial para mostrar otras características de búsqueda que podría querer usar en sus soluciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="3cc13-216">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="3cc13-217">Si ya Tiene alguna experiencia con Azure Search, puede utilizar este ejemplo como punto de partida para experimentación adicional, por ejemplo, aumentando la [página de búsqueda](search-pagination-page-layout.md), o implementando la [navegación por facetas](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="3cc13-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting the [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="3cc13-218">También puede mejorar la página de resultados de búsqueda si agrega recuentos y procesamiento por lotes de documentos para que los usuarios puedan navegar por las páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="3cc13-218">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="3cc13-219">¿Es la primera vez que usa Búsqueda de Azure?</span><span class="sxs-lookup"><span data-stu-id="3cc13-219">New to Azure Search?</span></span> <span data-ttu-id="3cc13-220">Le recomendamos que pruebe otros tutoriales para comprender mejor lo que puede crear.</span><span class="sxs-lookup"><span data-stu-id="3cc13-220">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="3cc13-221">Visite nuestra [página de documentación](https://azure.microsoft.com/documentation/services/search/) para encontrar más recursos.</span><span class="sxs-lookup"><span data-stu-id="3cc13-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="3cc13-222">También puede ver los vínculos en nuestra [lista de vídeos y tutoriales](search-video-demo-tutorial-list.md) para tener acceso a más información.</span><span class="sxs-lookup"><span data-stu-id="3cc13-222">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

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
