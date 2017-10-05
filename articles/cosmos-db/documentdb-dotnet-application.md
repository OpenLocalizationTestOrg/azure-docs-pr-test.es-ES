---
title: 'Tutorial de ASP.NET MVC para Azure Cosmos DB: desarrollo de aplicaciones web | Microsoft Docs'
description: "Tutorial de ASP.NET MVC para crear una aplicación web MVC con Azure Cosmos DB. Almacenará el código JSON y accederá a los datos desde una aplicación ToDo hospedada en Sitios web de Azure. Tutorial de ASP NET MVC paso a paso."
keywords: "tutorial de asp.net mvc, desarrollo de aplicaciones web, aplicación web de mvc, tutorial de asp net mvc paso a paso"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: 3f2950fe25feb8f3ee81cc0a79bf624f0ee33bd5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="2860b-105"><a name="_Toc395809351"></a>Tutorial de ASP.NET MVC: desarrollo de aplicaciones web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2860b-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2860b-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2860b-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="2860b-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="2860b-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="2860b-108">Java</span><span class="sxs-lookup"><span data-stu-id="2860b-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="2860b-109">Python</span><span class="sxs-lookup"><span data-stu-id="2860b-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="2860b-110">Para resaltar cómo puede aprovechar eficazmente Azure Cosmos DB para almacenar y consultar documentos JSON, este artículo proporciona un tutorial completo que muestra cómo crear una aplicación ToDo con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2860b-110">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="2860b-111">En Azure Cosmos DB, las tareas se almacenarán como documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="2860b-111">The tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Captura de pantalla de la aplicación web MVC de lista ToDo creada por este tutorial: tutorial ASP NET MVC paso a paso](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="2860b-113">Este tutorial muestra cómo utilizar el servicio Azure Cosmos DB para almacenar y acceder a datos desde una aplicación web MVC de ASP.NET hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="2860b-113">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="2860b-114">Si busca un tutorial que se centre solo en Azure Cosmos DB, no en los componentes de ASP.NET MVC, consulte el artículo sobre la [Creación de una aplicación de consola de C# con Azure Cosmos DB](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2860b-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="2860b-115">En este tutorial se supone que tiene experiencia previa con ASP.NET MVC y Sitios web Azure.</span><span class="sxs-lookup"><span data-stu-id="2860b-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="2860b-116">Si no está familiarizado con ASP.NET o con las [herramientas de requisitos previos](#_Toc395637760), le recomendamos que descargue el proyecto de ejemplo completo de [GitHub][GitHub] y siga las instrucciones de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2860b-116">If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample.</span></span> <span data-ttu-id="2860b-117">Una vez compilado, puede revisar este artículo para obtener información sobre el código en el contexto del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2860b-117">Once you have it built, you can review this article to gain insight on the code in the context of the project.</span></span>
> 
> 

## <span data-ttu-id="2860b-118"><a name="_Toc395637760"></a>Requisitos previos del tutorial de base de datos</span><span class="sxs-lookup"><span data-stu-id="2860b-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="2860b-119">Antes de seguir las instrucciones del presente artículo, debe asegurarse de tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2860b-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="2860b-120">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2860b-120">An active Azure account.</span></span> <span data-ttu-id="2860b-121">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="2860b-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2860b-122">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2860b-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="2860b-123">OR</span><span class="sxs-lookup"><span data-stu-id="2860b-123">OR</span></span>

    <span data-ttu-id="2860b-124">Una instalación local del [Emulador de Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="2860b-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="2860b-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="2860b-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="2860b-126">Microsoft Azure SDK para .NET de Visual Studio 2017, disponible a través del instalador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2860b-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span></span>

<span data-ttu-id="2860b-127">Se han realizado todas las capturas de pantalla de este artículo mediante Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="2860b-127">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="2860b-128">Si el sistema está configurado con una versión diferente, es probable que las pantallas y las opciones no coincidan completamente, pero si cumple los requisitos previos mencionados, esta solución debe funcionar.</span><span class="sxs-lookup"><span data-stu-id="2860b-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <span data-ttu-id="2860b-129"><a name="_Toc395637761"></a>Paso 1: Creación de una cuenta de base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2860b-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="2860b-130">Para comenzar, creemos una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2860b-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="2860b-131">Si ya tiene una cuenta de SQL (DocumentDB) para Azure Cosmos DB o si usa el emulador de Azure Cosmos DB para este tutorial, puede ir directamente a [Creación de una nueva aplicación MVC de ASP.NET](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="2860b-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="2860b-132">Ahora veremos cómo crear una aplicación ASP.NET MVC nueva desde el principio.</span><span class="sxs-lookup"><span data-stu-id="2860b-132">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <span data-ttu-id="2860b-133"><a name="_Toc395637762"></a>Paso 2: Creación de una aplicación ASP.NET MVC nueva</span><span class="sxs-lookup"><span data-stu-id="2860b-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="2860b-134">En Visual Studio, en el menú **Archivo**, seleccione **Nuevo** y luego haga clic en **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="2860b-134">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="2860b-135">Aparecerá el cuadro de diálogo **Nuevo proyecto** .</span><span class="sxs-lookup"><span data-stu-id="2860b-135">The **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="2860b-136">En el panel **Tipos de proyecto**, expanda **Plantillas**, **Visual C#**, **Web** y, a continuación, seleccione **Aplicación web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="2860b-136">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Captura de pantalla del cuadro de diálogo Nuevo proyecto con el tipo de proyecto Aplicación web ASP.NET resaltado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="2860b-138">En el cuadro **Nombre** , escriba el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2860b-138">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="2860b-139">Este tutorial utiliza el nombre "todo".</span><span class="sxs-lookup"><span data-stu-id="2860b-139">This tutorial uses the name "todo".</span></span> <span data-ttu-id="2860b-140">Si decide usar otro nombre distinto, siempre que en el tutorial se hable del espacio de nombres todo, deberá adaptar los ejemplos de código proporcionados para usar el nombre que haya dado a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2860b-140">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="2860b-141">Haga clic en **Examinar** para navegar hasta la carpeta donde desea crear el proyecto y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2860b-141">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="2860b-142">Aparece el cuadro de diálogo **Nueva aplicación web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="2860b-142">The **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Captura de pantalla del cuadro de diálogo Nueva aplicación web ASP.NET con la plantilla de aplicación MVC resaltada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="2860b-144">En el panel Plantillas, seleccione **MVC**.</span><span class="sxs-lookup"><span data-stu-id="2860b-144">In the templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="2860b-145">Haga clic en **Aceptar** y deje que Visual Studio realice la tarea de scaffolding de la plantilla ASP.NET MVC vacía.</span><span class="sxs-lookup"><span data-stu-id="2860b-145">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="2860b-146">Después de que Visual Studio haya terminado de crear la aplicación MVC reutilizable, tiene una aplicación ASP.NET vacía que puede ejecutar de manera local.</span><span class="sxs-lookup"><span data-stu-id="2860b-146">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="2860b-147">Omitiremos la ejecución del proyecto localmente, ya que estoy seguro de que todos hemos visto la aplicación "Hola a todos" de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2860b-147">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="2860b-148">Vayamos directamente a agregar Azure Cosmos DB a este proyecto y a compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2860b-148">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span></span>

## <span data-ttu-id="2860b-149"><a name="_Toc395637767"></a>Paso 3: Incorporación de Azure Cosmos DB al proyecto de aplicación web MVC</span><span class="sxs-lookup"><span data-stu-id="2860b-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB to your MVC web application project</span></span>
<span data-ttu-id="2860b-150">Ahora que ya tenemos la mayoría de los mecanismos de ASP.NET MVC que necesitamos para esta solución, vayamos al objetivo real de este tutorial, la incorporación de Azure Cosmos DB a nuestra aplicación web MVC.</span><span class="sxs-lookup"><span data-stu-id="2860b-150">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span></span>

1. <span data-ttu-id="2860b-151">El SDK de .NET para Azure Cosmos DB se empaquete y distribuye como un paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="2860b-151">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="2860b-152">Para obtener el paquete de NuGet en Visual Studio, utilice el Administrador de paquetes de NuGet en Visual Studio haciendo clic con el botón derecho en el proyecto en el **Explorador de soluciones** y, a continuación, haciendo clic en **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2860b-152">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Captura de pantalla de las opciones del botón secundario para el proyecto de aplicación web en el Explorador de soluciones, con Administrar paquetes NuGet resaltado.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="2860b-154">Aparecerá el cuadro de diálogo **Administrar paquetes de NuGet** .</span><span class="sxs-lookup"><span data-stu-id="2860b-154">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="2860b-155">En el cuadro **Browse** (Examinar) de NuGet, escriba ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="2860b-155">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="2860b-156">(El nombre del paquete no se ha actualizado a Azure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="2860b-156">(The package name has not been updated to Azure Cosmos DB.)</span></span>
   
    <span data-ttu-id="2860b-157">En los resultados, instale el paquete **Microsoft.Azure.DocumentDB de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2860b-157">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="2860b-158">De esta manera se descarga e instala el paquete de Azure Cosmos DB además de todas las dependencias, como Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="2860b-158">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="2860b-159">Haga clic en **OK** (Aceptar) en el ventana **Preview** (Vista previa) y **I Accept** (Acepto) en la ventana **License Acceptance** (Aceptación de licencia) para completar la instalación.</span><span class="sxs-lookup"><span data-stu-id="2860b-159">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
    ![Captura de pantalla de la ventana Administrar paquetes de NuGet, con la biblioteca de cliente de Microsoft Azure DocumentDB resaltada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="2860b-161">También puede usar la Consola del Administrador de paquetes para instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="2860b-161">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="2860b-162">Para ello, en el menú **Herramientas**, haga clic en **Administrador de paquetes NuGet** y, a continuación, haga clic en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="2860b-162">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="2860b-163">En el símbolo del sistema, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2860b-163">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="2860b-164">Una vez instalado el paquete, la solución de Visual Studio debe ser similar a lo siguiente con dos nuevas referencias agregadas, Microsoft.Azure.Documents.Client y Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="2860b-164">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Captura de pantalla de las dos referencias agregadas al proyecto de datos JSON en el Explorador de soluciones](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="2860b-166"><a name="_Toc395637763"></a>Paso 4: Configuración de la aplicación ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="2860b-166"><a name="_Toc395637763"></a>Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="2860b-167">Ahora vamos a agregar a esta aplicación de MVC modelos, vistas y controladores:</span><span class="sxs-lookup"><span data-stu-id="2860b-167">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="2860b-168">[Adición de un modelo](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="2860b-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="2860b-169">[Adición de un controlador](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="2860b-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="2860b-170">[Adición de vistas](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="2860b-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="2860b-171"><a name="_Toc395637764"></a>Adición de un modelo de datos JSON</span><span class="sxs-lookup"><span data-stu-id="2860b-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="2860b-172">Comencemos creando la **M** en MVC, el modelo.</span><span class="sxs-lookup"><span data-stu-id="2860b-172">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="2860b-173">En el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta **Modelos**, haga clic en **Agregar** y después en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="2860b-173">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="2860b-174">Aparecerá el cuadro de diálogo **Agregar nuevo elemento** .</span><span class="sxs-lookup"><span data-stu-id="2860b-174">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="2860b-175">Ponga a la nueva clase el nombre **Item.cs** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2860b-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="2860b-176">En este nuevo archivo **Item.cs** , agregue lo siguiente después de la última *instrucción using*.</span><span class="sxs-lookup"><span data-stu-id="2860b-176">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="2860b-177">Ahora, reemplace este código</span><span class="sxs-lookup"><span data-stu-id="2860b-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="2860b-178">por el siguiente.</span><span class="sxs-lookup"><span data-stu-id="2860b-178">with the following code.</span></span>
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    <span data-ttu-id="2860b-179">Todos los datos de Azure Cosmos DB se transmiten mediante la conexión y se almacenan como JSON.</span><span class="sxs-lookup"><span data-stu-id="2860b-179">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="2860b-180">Para controlar la forma en la que JSON.NET serializa y deserializa los objetos, puede usar el atributo **JsonProperty** como se mostró en la clase de **elemento** que acabamos de crear.</span><span class="sxs-lookup"><span data-stu-id="2860b-180">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="2860b-181">No **tiene** que hacer esto pero quería asegurarme de que mis propiedades siguen las convenciones de nomenclatura de mezcla de mayúsculas y minúsculas de JSON.</span><span class="sxs-lookup"><span data-stu-id="2860b-181">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="2860b-182">No solo puede controlar el formato del nombre de propiedad cuando va en JSON, sino que puede cambiar el nombre por completo de las propiedades de .NET como hice con la propiedad **Description** .</span><span class="sxs-lookup"><span data-stu-id="2860b-182">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <span data-ttu-id="2860b-183"><a name="_Toc395637765"></a>Adición de un controlador</span><span class="sxs-lookup"><span data-stu-id="2860b-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="2860b-184">Esto se encarga de **M**. Creemos ahora la **C** de MVC, una clase de controlador.</span><span class="sxs-lookup"><span data-stu-id="2860b-184">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="2860b-185">En el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta **Controladores** y, a continuación, haga clic en **Agregar** y, por último, en **Controlador**.</span><span class="sxs-lookup"><span data-stu-id="2860b-185">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="2860b-186">Aparecerá el cuadro de diálogo **Agregar scaffold** .</span><span class="sxs-lookup"><span data-stu-id="2860b-186">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="2860b-187">Seleccione **Controlador MVC 5 - Vacío** y, a continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2860b-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Captura de pantalla del cuadro de diálogo Agregar scaffold con la opción Controlador MVC 5 - Vacío resaltada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="2860b-189">Asigne un nombre al nuevo controlador, **ItemController.**</span><span class="sxs-lookup"><span data-stu-id="2860b-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Captura de pantalla del cuadro de diálogo Agregar controlador](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="2860b-191">Una vez creado el archivo, la solución de Visual Studio debe ser similar a lo siguiente con el nuevo archivo ItemController.cs en el **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="2860b-191">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="2860b-192">También se muestra el nuevo archivo Item.cs creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2860b-192">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Captura de pantalla de la solución de Visual Studio - Explorador de soluciones con los nuevos archivos ItemController.cs e Item.cs resaltados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="2860b-194">Puede cerrar ItemController.cs, volveremos a él más tarde.</span><span class="sxs-lookup"><span data-stu-id="2860b-194">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <span data-ttu-id="2860b-195"><a name="_Toc395637766"></a>Adición de vistas</span><span class="sxs-lookup"><span data-stu-id="2860b-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="2860b-196">Por último, vamos a crear la **V** de MVC, las vistas.</span><span class="sxs-lookup"><span data-stu-id="2860b-196">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="2860b-197">[Adición de una vista de índice de elementos](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="2860b-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="2860b-198">[Adición de una vista de elementos nuevos](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="2860b-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="2860b-199">[Adición de una vista de edición de elementos](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="2860b-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="2860b-200"><a name="AddItemIndexView"></a>Adición de una vista de índice de elementos</span><span class="sxs-lookup"><span data-stu-id="2860b-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="2860b-201">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en la carpeta **Elemento** vacía que ha creado Visual Studio para usted cuando agregó **ItemController** anteriormente, haga clic en **Agregar** y, a continuación, haga clic en **Vista**.</span><span class="sxs-lookup"><span data-stu-id="2860b-201">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Captura de pantalla del Explorador de soluciones que muestra la carpeta Elemento con los comandos Agregar vista resaltados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="2860b-203">En el cuadro de diálogo **Agregar vista** , realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2860b-203">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="2860b-204">En el cuadro **Nombre de vista**, escriba ***Índice***.</span><span class="sxs-lookup"><span data-stu-id="2860b-204">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="2860b-205">En el cuadro **Plantilla**, seleccione ***Lista***.</span><span class="sxs-lookup"><span data-stu-id="2860b-205">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="2860b-206">En el cuadro **Clase de modelo**, seleccione ***Elemento (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="2860b-206">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="2860b-207">En el cuadro de página de diseño, escriba ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="2860b-207">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Captura de pantalla que muestra el cuadro de diálogo Agregar vista](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="2860b-209">Después de que se hayan establecido todos estos valores, haga clic en **Agregar** y permita que Visual Studio cree una nueva vista de plantilla.</span><span class="sxs-lookup"><span data-stu-id="2860b-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="2860b-210">Después de esto, se abrirá el archivo cshtml que se creó.</span><span class="sxs-lookup"><span data-stu-id="2860b-210">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="2860b-211">Podemos cerrar este archivo en Visual Studio, ya que volveremos a él más tarde.</span><span class="sxs-lookup"><span data-stu-id="2860b-211">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <span data-ttu-id="2860b-212"><a name="AddNewIndexView"></a>Adición de una vista de elementos nuevos</span><span class="sxs-lookup"><span data-stu-id="2860b-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="2860b-213">De forma parecida a cómo se crea una vista de **índice de elementos**, crearemos ahora una nueva vista para crear nuevos **elementos**.</span><span class="sxs-lookup"><span data-stu-id="2860b-213">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="2860b-214">En el **Explorador de soluciones**, vuelva a hacer clic con el botón derecho en la carpeta **Elemento**, haga clic en **Agregar** y después en **Vista**.</span><span class="sxs-lookup"><span data-stu-id="2860b-214">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="2860b-215">En el cuadro de diálogo **Agregar vista** , realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2860b-215">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="2860b-216">En el cuadro **Nombre de vista**, escriba ***Crear***.</span><span class="sxs-lookup"><span data-stu-id="2860b-216">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="2860b-217">En el cuadro **Plantilla**, seleccione ***Crear***.</span><span class="sxs-lookup"><span data-stu-id="2860b-217">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="2860b-218">En el cuadro **Clase de modelo**, seleccione ***Elemento (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="2860b-218">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="2860b-219">En el cuadro de página de diseño, escriba ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="2860b-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="2860b-220">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2860b-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="2860b-221"><a name="_Toc395888515"></a>Adición de una vista de edición de elementos</span><span class="sxs-lookup"><span data-stu-id="2860b-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="2860b-222">Finalmente, agregue una última vista para editar un **elemento** como se hizo anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2860b-222">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="2860b-223">En el **Explorador de soluciones**, vuelva a hacer clic con el botón derecho en la carpeta **Elemento**, haga clic en **Agregar** y después en **Vista**.</span><span class="sxs-lookup"><span data-stu-id="2860b-223">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="2860b-224">En el cuadro de diálogo **Agregar vista** , realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2860b-224">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="2860b-225">En el cuadro **Nombre de vista**, escriba ***Editar***.</span><span class="sxs-lookup"><span data-stu-id="2860b-225">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="2860b-226">En el cuadro **Plantilla**, seleccione ***Editar***.</span><span class="sxs-lookup"><span data-stu-id="2860b-226">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="2860b-227">En el cuadro **Clase de modelo**, seleccione ***Elemento (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="2860b-227">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="2860b-228">En el cuadro de página de diseño, escriba ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="2860b-228">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="2860b-229">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2860b-229">Click **Add**.</span></span>

<span data-ttu-id="2860b-230">Una vez hecho esto, cierre todos los documentos cshtml en Visual Studio, ya que volveremos a estas vistas más tarde.</span><span class="sxs-lookup"><span data-stu-id="2860b-230">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <span data-ttu-id="2860b-231"><a name="_Toc395637769"></a>Paso 5: Conexión de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2860b-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="2860b-232">Ahora que ya nos hemos ocupado de los elementos estándar de MVC, agreguemos el código para Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2860b-232">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="2860b-233">En esta sección, agregaremos código para controlar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2860b-233">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="2860b-234">[Lista de elementos incompletos](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="2860b-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="2860b-235">[Adición de elementos](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="2860b-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="2860b-236">[Edición de elementos](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="2860b-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="2860b-237"><a name="_Toc395637770"></a>Lista de elementos incompletos en la aplicación web MVC</span><span class="sxs-lookup"><span data-stu-id="2860b-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="2860b-238">Lo primero que debe hacerse es agregar una clase que contenga toda la lógica para conectarse a Azure Cosmos DB y utilizarlo.</span><span class="sxs-lookup"><span data-stu-id="2860b-238">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span></span> <span data-ttu-id="2860b-239">Para este tutorial, encapsularemos toda esta lógica en una clase de repositorio denominada DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="2860b-239">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="2860b-240">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto, haga clic en **Agregar** y después en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="2860b-240">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="2860b-241">Ponga a la nueva clase el nombre **DocumentDBRepository** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2860b-241">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="2860b-242">En la recién creada **DocumentDBRepository**, clasifique y agregue las *instrucciones using* siguientes sobre la declaración *namespace*</span><span class="sxs-lookup"><span data-stu-id="2860b-242">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="2860b-243">Ahora, reemplace este código</span><span class="sxs-lookup"><span data-stu-id="2860b-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="2860b-244">por el siguiente.</span><span class="sxs-lookup"><span data-stu-id="2860b-244">with the following code.</span></span>
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. <span data-ttu-id="2860b-245">Estamos leyendo algunos valores de la configuración; por tanto, abra el archivo **Web.config** de su aplicación y agregue las siguientes líneas debajo de la sección `<AppSettings>`.</span><span class="sxs-lookup"><span data-stu-id="2860b-245">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="2860b-246">Ahora, actualice los valores de *endpoint* y *authKey* mediante la hoja Claves de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2860b-246">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="2860b-247">Utilice el **URI** de la hoja Claves como el valor de la configuración de endpoint y utilice **CLAVE PRINCIPAL** o **CLAVE SECUNDARIA** de la hoja Claves como el valor de la configuración de authKey.</span><span class="sxs-lookup"><span data-stu-id="2860b-247">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="2860b-248">Se encarga del cableado del repositorio de Azure Cosmos DB; agreguemos ahora la lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="2860b-248">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="2860b-249">Lo primero que queremos poder hacer con una aplicación de lista todo es mostrar los elementos incompletos.</span><span class="sxs-lookup"><span data-stu-id="2860b-249">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="2860b-250">Copie y pegue el siguiente fragmento de código en cualquier parte dentro de la clase **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="2860b-250">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. <span data-ttu-id="2860b-251">Abra **ItemController** que agregamos anteriormente y agregue las *instrucciones using* siguientes sobre la declaración namespace.</span><span class="sxs-lookup"><span data-stu-id="2860b-251">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="2860b-252">Si el proyecto no se denomina "todo", deberá actualizar con "todo. Models"; para reflejar el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="2860b-252">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="2860b-253">Ahora, reemplace este código</span><span class="sxs-lookup"><span data-stu-id="2860b-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="2860b-254">por el siguiente.</span><span class="sxs-lookup"><span data-stu-id="2860b-254">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="2860b-255">Abra **Global.asax.cs** y agregue la siguiente línea al método **Application_Start**</span><span class="sxs-lookup"><span data-stu-id="2860b-255">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="2860b-256">En este punto, la solución debe ser capaz de compilar sin errores.</span><span class="sxs-lookup"><span data-stu-id="2860b-256">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="2860b-257">Si ejecuta la aplicación ahora, irá a **HomeController** y a la vista de **índice** de ese controlador.</span><span class="sxs-lookup"><span data-stu-id="2860b-257">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="2860b-258">Este es el comportamiento predeterminado para el proyecto de plantillas MVC que seleccionamos al comienzo, pero no queremos eso.</span><span class="sxs-lookup"><span data-stu-id="2860b-258">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="2860b-259">Cambiemos el enrutamiento en esta aplicación MVC para modificar este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="2860b-259">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="2860b-260">Abra ***App\_Start\RouteConfig.cs***, busque la línea que empieza con "defaults:" y cámbiela para que se parezca a lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="2860b-260">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="2860b-261">Esto indica ahora a ASP.NET MVC que si no ha especificado un valor en la dirección URL para controlar el comportamiento de enrutamiento que, en lugar de **Inicio**, usa **Elemento** como controlador e **Índice** de usuario como vista.</span><span class="sxs-lookup"><span data-stu-id="2860b-261">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="2860b-262">Si ejecuta la aplicación, llamará a su **ItemController**, que llamará a la clase de repositorio y usará el método GetItems para devolver todos los elementos incompletos a la vista **Vistas**\\**Elemento**\\**Índice**.</span><span class="sxs-lookup"><span data-stu-id="2860b-262">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="2860b-263">Si crea y ejecuta este proyecto ahora, deberá ver algo parecido a esto.</span><span class="sxs-lookup"><span data-stu-id="2860b-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Captura de pantalla de la aplicación web de lista de tareas pendientes creada con este tutorial](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="2860b-265"><a name="_Toc395637771"></a>Adición de elementos</span><span class="sxs-lookup"><span data-stu-id="2860b-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="2860b-266">Pongamos algunos elementos en nuestra base de datos de modo que tengamos algo más que una cuadrícula vacía que ver.</span><span class="sxs-lookup"><span data-stu-id="2860b-266">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="2860b-267">Agreguemos algo de código a Azure Cosmos DBRepository e ItemController para mantener el registro en Azure cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2860b-267">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="2860b-268">Agregue el siguiente método a su clase **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="2860b-268">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="2860b-269">Este método simplemente toma un objeto que se le haya pasado y lo mantiene en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2860b-269">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="2860b-270">Abra el archivo ItemController.cs y agregue el siguiente fragmento de código en la clase.</span><span class="sxs-lookup"><span data-stu-id="2860b-270">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="2860b-271">Así es cómo ASP.NET MVC sabe qué hacer para la acción **Crear** .</span><span class="sxs-lookup"><span data-stu-id="2860b-271">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="2860b-272">En este caso basta con presentar la vista Create.cshtml asociada creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2860b-272">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="2860b-273">Ahora necesitamos un poco más de código en este controlador que aceptará el envío desde la vista **Crear** .</span><span class="sxs-lookup"><span data-stu-id="2860b-273">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="2860b-274">Agregue el siguiente bloque de código a la clase ItemController.cs que le indica a ASP.NET MVC lo que debe hacer con un formulario POST para este controlador.</span><span class="sxs-lookup"><span data-stu-id="2860b-274">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    <span data-ttu-id="2860b-275">Este código llama a DocumentDBRepository y usa el método CreateItemAsync para conservar el nuevo elemento todo en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="2860b-275">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="2860b-276">**Nota de seguridad**: El atributo **ValidateAntiForgeryToken** se usa aquí para ayudarle a proteger esta aplicación contra ataques de falsificación de solicitud entre sitios.</span><span class="sxs-lookup"><span data-stu-id="2860b-276">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="2860b-277">Es más que solo agregar este atributo, sus vistas también necesitan trabajar con este token antifalsificación.</span><span class="sxs-lookup"><span data-stu-id="2860b-277">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="2860b-278">Para más información acerca del tema, así como ejemplos de cómo implementarlo correctamente, consulte el artículo sobre la [prevención de la falsificación de solicitud entre sitios][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="2860b-278">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="2860b-279">El código fuente proporcionado en [GitHub][GitHub] tiene la implementación completa.</span><span class="sxs-lookup"><span data-stu-id="2860b-279">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="2860b-280">**Nota de seguridad**: También usamos el atributo **Bind** en el parámetro de método para ayudar a proteger contra ataques de publicación en exceso.</span><span class="sxs-lookup"><span data-stu-id="2860b-280">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="2860b-281">Para más información, consulte el artículo sobre [operaciones CRUD básicas en ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="2860b-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="2860b-282">Esto finaliza el código necesario para agregar elementos nuevos en nuestra base de datos.</span><span class="sxs-lookup"><span data-stu-id="2860b-282">This concludes the code required to add new Items to our database.</span></span>

### <span data-ttu-id="2860b-283"><a name="_Toc395637772"></a>Edición de elementos</span><span class="sxs-lookup"><span data-stu-id="2860b-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="2860b-284">Hay una última cosa que tenemos que hacer, que es agregar la capacidad de editar **elementos** en la base de datos y marcarlos como completados.</span><span class="sxs-lookup"><span data-stu-id="2860b-284">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="2860b-285">La vista de edición ya se ha agregado al proyecto, por lo que necesitamos agregar código a nuestro controlador y a la clase **DocumentDBRepository** de nuevo.</span><span class="sxs-lookup"><span data-stu-id="2860b-285">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="2860b-286">Agregue lo siguiente a la clase **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="2860b-286">Add the following to the **DocumentDBRepository** class.</span></span>
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    <span data-ttu-id="2860b-287">El primero de estos métodos, **GetItem** captura un elemento de Azure cosmos DB que se devuelve a **ItemController** y luego continúa hasta la vista de **edición**.</span><span class="sxs-lookup"><span data-stu-id="2860b-287">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="2860b-288">El segundo de los métodos que acabamos de agregar reemplaza el **documento** de Azure cosmos DB con la versión del **documento** que se transmitió desde **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="2860b-288">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="2860b-289">Agregue lo siguiente a la clase **ItemController** .</span><span class="sxs-lookup"><span data-stu-id="2860b-289">Add the following to the **ItemController** class.</span></span>
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    <span data-ttu-id="2860b-290">El primer método controla el Http GET que ocurrirá cuando el usuario haga clic en el vínculo de **edición** en la vista de **índice**.</span><span class="sxs-lookup"><span data-stu-id="2860b-290">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="2860b-291">Este método captura un [**documento**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) de Azure cosmos DB y lo transmite a la vista de **edición**.</span><span class="sxs-lookup"><span data-stu-id="2860b-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="2860b-292">La vista de **edición** realizará un Http POST en **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="2860b-292">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="2860b-293">El segundo método que agregamos controla la transmisión del objeto actualizado a Azure cosmos DB para que se conserve en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="2860b-293">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span></span>

<span data-ttu-id="2860b-294">Esto es todo lo que necesitamos para ejecutar la aplicación, enumerar **elementos** incompletos, agregar nuevos **elementos** y editar **elementos**.</span><span class="sxs-lookup"><span data-stu-id="2860b-294">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="2860b-295"><a name="_Toc395637773"></a>Paso 6: Ejecución de la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="2860b-295"><a name="_Toc395637773"></a>Step 6: Run the application locally</span></span>
<span data-ttu-id="2860b-296">Lleve a cabo los siguientes pasos para probar la aplicación en su máquina local:</span><span class="sxs-lookup"><span data-stu-id="2860b-296">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="2860b-297">Presione F5 en Visual Studio para compilar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="2860b-297">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="2860b-298">De esa forma, se debe compilar la aplicación e iniciar un explorador con la página de cuadrícula vacía que vimos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="2860b-298">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![Captura de pantalla de la aplicación web de lista de tareas pendientes creada con este tutorial](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="2860b-300">Haga clic en el vínculo **Crear nuevo** y agregue valores a los campos **Nombre** y **Descripción**.</span><span class="sxs-lookup"><span data-stu-id="2860b-300">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="2860b-301">Deje la casilla **Completado** sin seleccionar; de lo contrario, el **elemento** nuevo se agregará en estado completado y no aparecerá en la lista inicial.</span><span class="sxs-lookup"><span data-stu-id="2860b-301">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![Captura de pantalla de la vista Crear](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="2860b-303">Haga clic en **Crear**, se le redirigirá a la vista de **índice** y aparecerá el **elemento** en la lista.</span><span class="sxs-lookup"><span data-stu-id="2860b-303">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![Captura de pantalla de la vista de índice](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="2860b-305">Puede agregar algunos **elementos** más en su lista todo.</span><span class="sxs-lookup"><span data-stu-id="2860b-305">Feel free to add a few more **Items** to your todo list.</span></span>
    
4. <span data-ttu-id="2860b-306">Haga clic en **Editar** junto a un **elemento** de la lista y llegará a la vista de **edición**, donde puede actualizar cualquier propiedad de su objeto, incluida la marca **Completado**.</span><span class="sxs-lookup"><span data-stu-id="2860b-306">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="2860b-307">Si selecciona la marca **Completado** y hace clic en **Guardar**, el **elemento** se quita de la lista de tareas incompletas.</span><span class="sxs-lookup"><span data-stu-id="2860b-307">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![Captura de pantalla de la vista de índice con el cuadro Completado activado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="2860b-309">Una vez que haya probado la aplicación, presione Ctrl+F5 para detener la depuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2860b-309">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="2860b-310">Está listo para la implementación.</span><span class="sxs-lookup"><span data-stu-id="2860b-310">You're ready to deploy!</span></span>

## <span data-ttu-id="2860b-311"><a name="_Toc395637774"></a>Paso 7: Implementación de la aplicación en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="2860b-311"><a name="_Toc395637774"></a>Step 7: Deploy the application to Azure App Service</span></span> 
<span data-ttu-id="2860b-312">Ahora que toda la aplicación funciona correctamente con Azure Cosmos DB, vamos a implementar esta aplicación web en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2860b-312">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span></span>  

1. <span data-ttu-id="2860b-313">Para publicar esta aplicación, todo lo que necesita hacer es hacer clic con el botón derecho en el proyecto en el **Explorador de soluciones** y hacer clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="2860b-313">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Captura de pantalla de la opción Publicar en el Explorador de soluciones](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="2860b-315">En el cuadro de diálogo **Publicar**, haga clic en **Microsoft Azure App Service** y, a continuación, seleccione **Crear nuevo** para crear un perfil de App Service o haga clic en **Seleccione existente** para utilizar un perfil existente.</span><span class="sxs-lookup"><span data-stu-id="2860b-315">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span></span>

    ![Cuadro de diálogo Publicar en Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="2860b-317">Si tiene un perfil de Azure App Service existente, escriba el nombre de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="2860b-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="2860b-318">Use el filtro **Vista** para ordenar por tipo de recurso o grupo de recursos y, a continuación, seleccione la instancia de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2860b-318">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Cuadro de diálogo App Service en Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="2860b-320">Para crear un nuevo perfil de Azure App Service, haga clic en **Crear nuevo** en el cuadro de diálogo **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="2860b-320">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span></span> <span data-ttu-id="2860b-321">En el cuadro de diálogo **Crear App Service**, escriba el nombre de la aplicación web, la suscripción adecuada, el grupo de recursos, el plan de App Service y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2860b-321">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Cuadro de diálogo Crear App Service en Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="2860b-323">En pocos segundos, Visual Studio terminará de publicar la aplicación web y ejecutará un explorador donde podrá ver su trabajo ejecutándose en Azure.</span><span class="sxs-lookup"><span data-stu-id="2860b-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="2860b-324"><a name="_Toc395637775"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2860b-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="2860b-325">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2860b-325">Congratulations!</span></span> <span data-ttu-id="2860b-326">Acaba de compilar su primera aplicación web MVC de ASP.NET con Azure Cosmos DB y la ha publicado en Azure.</span><span class="sxs-lookup"><span data-stu-id="2860b-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span></span> <span data-ttu-id="2860b-327">El código fuente de la aplicación completa, incluida la funcionalidad de detalle y eliminación, que no se incluyeron en este tutorial, se puede descargar o clonar desde [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="2860b-327">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="2860b-328">Por lo tanto, si está interesado en agregarlo a la aplicación, seleccione el código y agréguelo a esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="2860b-328">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="2860b-329">Para agregar funcionalidad adicional a la aplicación, revise las API disponibles en la [biblioteca de .NET para Microsoft Azure Cosmos DB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) y haga sus aportaciones libremente a la biblioteca de .NET para Azure Cosmos DB en [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="2860b-329">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
