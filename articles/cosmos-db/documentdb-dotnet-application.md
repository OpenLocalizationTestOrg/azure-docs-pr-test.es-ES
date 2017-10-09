---
title: 'Tutorial de ASP.NET MVC para Azure Cosmos DB: desarrollo de aplicaciones web | Microsoft Docs'
description: "ASP.NET MVC tutorial toocreate una aplicación web MVC con base de datos de Azure Cosmos. Almacenará el código JSON y accederá a los datos desde una aplicación ToDo hospedada en Sitios web de Azure. Tutorial de ASP NET MVC paso a paso."
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
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="c9d5a-105"><a name="_Toc395809351"></a>Tutorial de ASP.NET MVC: desarrollo de aplicaciones web con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9d5a-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9d5a-106">.NET</span><span class="sxs-lookup"><span data-stu-id="c9d5a-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="c9d5a-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="c9d5a-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="c9d5a-108">Java</span><span class="sxs-lookup"><span data-stu-id="c9d5a-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="c9d5a-109">Python</span><span class="sxs-lookup"><span data-stu-id="c9d5a-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="c9d5a-110">toohighlight cómo puede aprovechar la base de datos de Azure Cosmos toostore y consultar documentos JSON eficazmente, este artículo proporciona un ejemplo paso a paso to-end que se muestra cómo una aplicación de lista de tareas con la base de datos de Azure Cosmos toobuild.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-110">toohighlight how you can efficiently leverage Azure Cosmos DB toostore and query JSON documents, this article provides an end-to-end walk-through showing you how toobuild a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="c9d5a-111">tareas de Hola se almacenará como documentos JSON en la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-111">hello tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Captura de pantalla de lista de tareas de hello aplicación web MVC creado por este tutorial: tutorial paso a paso de ASP NET MVC](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="c9d5a-113">Este tutorial muestra cómo toouse Hola base de datos de Azure Cosmos servicio toostore y acceso a los datos desde una aplicación web de MVC de ASP.NET hospedado en Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-113">This walk-through shows you how toouse hello Azure Cosmos DB service toostore and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="c9d5a-114">Si desea obtener un tutorial que se centra en la base de datos de Azure Cosmos y no hello componentes de MVC de ASP.NET, vea [compilar una aplicación de consola de C# de Azure Cosmos DB](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not hello ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="c9d5a-115">En este tutorial se supone que tiene experiencia previa con ASP.NET MVC y Sitios web Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="c9d5a-116">Si es nuevo tooASP.NET o hello [herramientas requisitos previos](#_Toc395637760), le recomendamos que descargue el proyecto de ejemplo completo de Hola de [GitHub] [ GitHub] y siga las instrucciones de hello en en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-116">If you are new tooASP.NET or hello [prerequisite tools](#_Toc395637760), we recommend downloading hello complete sample project from [GitHub][GitHub] and following hello instructions in this sample.</span></span> <span data-ttu-id="c9d5a-117">Una vez que se generan, puede revisar esta información de toogain de artículo en el código de hello en contexto de Hola de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-117">Once you have it built, you can review this article toogain insight on hello code in hello context of hello project.</span></span>
> 
> 

## <span data-ttu-id="c9d5a-118"><a name="_Toc395637760"></a>Requisitos previos del tutorial de base de datos</span><span class="sxs-lookup"><span data-stu-id="c9d5a-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="c9d5a-119">Antes de seguir las instrucciones de hello en este artículo, debe asegurarse de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9d5a-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="c9d5a-120">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-120">An active Azure account.</span></span> <span data-ttu-id="c9d5a-121">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c9d5a-122">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="c9d5a-123">OR</span><span class="sxs-lookup"><span data-stu-id="c9d5a-123">OR</span></span>

    <span data-ttu-id="c9d5a-124">Una instalación local de hello [emulador de base de datos de Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="c9d5a-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="c9d5a-126">Microsoft Azure SDK para .NET de Visual Studio de 2017 disponible a través de hello instalador de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through hello Visual Studio Installer.</span></span>

<span data-ttu-id="c9d5a-127">Se han realizado todas las capturas de pantalla de hello en este artículo mediante Microsoft Visual Studio Comunidad 2017.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-127">All hello screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="c9d5a-128">Si el sistema está configurado con una versión diferente, es posible que los filtros y opciones no coincidirán completamente, pero si Hola por encima de los requisitos previos se cumplen esta solución debería funcionar.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet hello above prerequisites this solution should work.</span></span>

## <span data-ttu-id="c9d5a-129"><a name="_Toc395637761"></a>Paso 1: Creación de una cuenta de base de datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9d5a-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="c9d5a-130">Para comenzar, creemos una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="c9d5a-131">Si ya tiene una cuenta SQL (documentos) de la base de datos de Azure Cosmos o si usas Hola emulador de base de datos de Azure Cosmos para este tutorial, puede omitir demasiado[crear una nueva aplicación MVC de ASP.NET](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="c9d5a-132">Se le indicará cómo toocreate una nueva aplicación de MVC de ASP.NET de hello principio a fin.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-132">We will now walk through how toocreate a new ASP.NET MVC application from hello ground-up.</span></span> 

## <span data-ttu-id="c9d5a-133"><a name="_Toc395637762"></a>Paso 2: Creación de una aplicación ASP.NET MVC nueva</span><span class="sxs-lookup"><span data-stu-id="c9d5a-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="c9d5a-134">En Visual Studio, en hello **archivo** menú, seleccione demasiado**New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-134">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span> <span data-ttu-id="c9d5a-135">Hola **nuevo proyecto** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-135">hello **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="c9d5a-136">Hola **tipos de proyecto** panel, expanda **plantillas**, **Visual C#**, **Web**y, a continuación, seleccione **aplicación Web ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="c9d5a-136">In hello **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Captura de pantalla del cuadro de diálogo nuevo proyecto de hello con el tipo de proyecto de aplicación Web ASP.NET de hello resaltado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="c9d5a-138">Hola **nombre** cuadro, escriba un nombre hello del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-138">In hello **Name** box, type hello name of hello project.</span></span> <span data-ttu-id="c9d5a-139">Este tutorial usa Hola nombre "todo".</span><span class="sxs-lookup"><span data-stu-id="c9d5a-139">This tutorial uses hello name "todo".</span></span> <span data-ttu-id="c9d5a-140">Si elige un valor distinto de esto toouse, siempre que este tutorial se habla de espacio de nombres de tareas de hello, deberá toouse de ejemplos de código de hello proporciona tooadjust lo que se denomina la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-140">If you choose toouse something other than this, then wherever this tutorial talks about hello todo namespace, you need tooadjust hello provided code samples toouse whatever you named your application.</span></span> 
4. <span data-ttu-id="c9d5a-141">Haga clic en **examinar** toonavigate toohello carpeta donde como proyecto de hello toocreate y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-141">Click **Browse** toonavigate toohello folder where you would like toocreate hello project, and then click **OK**.</span></span>
   
      <span data-ttu-id="c9d5a-142">Hola **nueva aplicación Web ASP.NET** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-142">hello **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Captura de pantalla del cuadro de diálogo nueva aplicación Web ASP.NET de Hola a plantilla de aplicación de MVC Hola resaltado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="c9d5a-144">En el panel de plantillas de hello, seleccione **MVC**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-144">In hello templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="c9d5a-145">Haga clic en **Aceptar** y dejar que Visual Studio lo alrededor de la plantilla vacía de ASP.NET MVC de scaffolding Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-145">Click **OK** and let Visual Studio do its thing around scaffolding hello empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="c9d5a-146">Una vez que Visual Studio ha terminado de crear la aplicación de MVC reutilizable de hello tiene una aplicación de ASP.NET vacía que se puede ejecutar localmente.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-146">Once Visual Studio has finished creating hello boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="c9d5a-147">Se podrá omitir ejecución proyecto Hola localmente porque estoy seguro de que hemos Hola visto todos los ASP.NET "¡Hello World" aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-147">We'll skip running hello project locally because I'm sure we've all seen hello ASP.NET "Hello World" application.</span></span> <span data-ttu-id="c9d5a-148">Vamos a tooadding recta base de datos de Azure Cosmos toothis proyecto y compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-148">Let's go straight tooadding Azure Cosmos DB toothis project and building our application.</span></span>

## <span data-ttu-id="c9d5a-149"><a name="_Toc395637767"></a>Paso 3: Agregar proyecto de aplicación web de base de datos de Azure Cosmos tooyour MVC</span><span class="sxs-lookup"><span data-stu-id="c9d5a-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB tooyour MVC web application project</span></span>
<span data-ttu-id="c9d5a-150">Ahora que tenemos la mayoría de establecimiento de ASP.NET MVC Hola que necesitamos para esta solución, vamos a obtener toohello real propósito de este tutorial, para agregar la aplicación web de base de datos de Azure Cosmos tooour MVC.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-150">Now that we have most of hello ASP.NET MVC plumbing that we need for this solution, let's get toohello real purpose of this tutorial, adding Azure Cosmos DB tooour MVC web application.</span></span>

1. <span data-ttu-id="c9d5a-151">Hello Azure Cosmos DB .NET SDK se empaqueta y distribuye como un paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-151">hello Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="c9d5a-152">tooget Hola paquete de NuGet en Visual Studio, use el Administrador de paquetes de NuGet hello en Visual Studio con el botón secundario en el proyecto de hello en **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-152">tooget hello NuGet package in Visual Studio, use hello NuGet package manager in Visual Studio by right-clicking on hello project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Captura de pantalla de hello haga clic en Opciones de proyecto de aplicación web de hello en el Explorador de soluciones, con administrar paquetes de NuGet resaltado.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="c9d5a-154">Hola **administrar paquetes de NuGet** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-154">hello **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="c9d5a-155">Hola NuGet **examinar** , escriba ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-155">In hello NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="c9d5a-156">(nombre del paquete hello no ha sido actualizada tooAzure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="c9d5a-156">(hello package name has not been updated tooAzure Cosmos DB.)</span></span>
   
    <span data-ttu-id="c9d5a-157">Desde los resultados de hello, instalar hello **Microsoft.Azure.DocumentDB Microsoft** paquete.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-157">From hello results, install hello **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="c9d5a-158">Esto descargará e instalará el paquete de la base de datos de Azure Cosmos de hello, así como todas las dependencias, como Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-158">This will download and install hello Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="c9d5a-159">Haga clic en **Aceptar** en hello **vista previa** ventana, y **acepto** en hello **la aceptación de licencia** ventana toocomplete Hola install.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-159">Click **OK** in hello **Preview** window, and **I Accept** in hello **License Acceptance** window toocomplete hello install.</span></span>
   
    ![Captura de pantalla de la ventana Administrar paquetes de NuGet de hello, con hello resaltado de la biblioteca del cliente de documentos de Microsoft Azure](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="c9d5a-161">O bien puede usar Hola paquete de hello tooinstall Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-161">Alternatively you can use hello Package Manager Console tooinstall hello package.</span></span> <span data-ttu-id="c9d5a-162">toodo así, sucesivamente hello **herramientas** menú, haga clic en **Administrador de paquetes de NuGet**y, a continuación, haga clic en **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-162">toodo so, on hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="c9d5a-163">En el símbolo del sistema de hello, escriba Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-163">At hello prompt, type hello following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="c9d5a-164">Una vez instalado el paquete de hello, la solución de Visual Studio debe parecerse al siguiente de hello con dos nuevas referencias de agregado, Microsoft.Azure.Documents.Client y Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-164">Once hello package is installed, your Visual Studio solution should resemble hello following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Captura de pantalla de dos referencias de hello agrega proyecto de datos JSON de toohello en el Explorador de soluciones](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="c9d5a-166"><a name="_Toc395637763"></a>Paso 4: Configurar Hola aplicación ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="c9d5a-166"><a name="_Toc395637763"></a>Step 4: Set up hello ASP.NET MVC application</span></span>
<span data-ttu-id="c9d5a-167">Ahora vamos a Agregar aplicación de MVC de toothis de modelos, vistas y controladores de hello:</span><span class="sxs-lookup"><span data-stu-id="c9d5a-167">Now let's add hello models, views, and controllers toothis MVC application:</span></span>

* <span data-ttu-id="c9d5a-168">[Adición de un modelo](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="c9d5a-169">[Adición de un controlador](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="c9d5a-170">[Adición de vistas](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="c9d5a-171"><a name="_Toc395637764"></a>Adición de un modelo de datos JSON</span><span class="sxs-lookup"><span data-stu-id="c9d5a-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="c9d5a-172">Empecemos creando hello **M** en MVC, Hola modelo.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-172">Let's begin by creating hello **M** in MVC, hello model.</span></span> 

1. <span data-ttu-id="c9d5a-173">En **el Explorador de soluciones**, contextual hello **modelos** carpeta, haga clic en **agregar**y, a continuación, haga clic en **clase**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-173">In **Solution Explorer**, right-click hello **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="c9d5a-174">Hola **Agregar nuevo elemento** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-174">hello **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="c9d5a-175">Ponga a la nueva clase el nombre **Item.cs** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="c9d5a-176">En este nuevo **Item.cs** , agregue el siguiente Hola después Hola última *mediante la instrucción*.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-176">In this new **Item.cs** file, add hello following after hello last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="c9d5a-177">Ahora, reemplace este código</span><span class="sxs-lookup"><span data-stu-id="c9d5a-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="c9d5a-178">con hello al siguiente código.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-178">with hello following code.</span></span>
   
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
   
    <span data-ttu-id="c9d5a-179">Todos los datos de la base de datos de Azure Cosmos se pasan a través de conexión de Hola y almacenar como JSON.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-179">All data in Azure Cosmos DB is passed over hello wire and stored as JSON.</span></span> <span data-ttu-id="c9d5a-180">manera de Hola de toocontrol los objetos se serializan/deserializar JSON.NET puede usar hello **JsonProperty** atributo como se muestra en hello **elemento** clase que acabamos de crear.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-180">toocontrol hello way your objects are serialized/deserialized by JSON.NET you can use hello **JsonProperty** attribute as demonstrated in hello **Item** class we just created.</span></span> <span data-ttu-id="c9d5a-181">No se cuentan **tienen** toodo esto pero desea tooensure que mi propiedades sigan convenciones de nomenclatura de hello JSON camelCase.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-181">You don't **have** toodo this but I want tooensure that my properties follow hello JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="c9d5a-182">No solo puede controlar formato Hola Hola del nombre de propiedad cuando entra en JSON, pero puede cambiar completamente las propiedades de .NET como hizo con hello **descripción** propiedad.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-182">Not only can you control hello format of hello property name when it goes into JSON, but you can entirely rename your .NET properties like I did with hello **Description** property.</span></span> 

### <span data-ttu-id="c9d5a-183"><a name="_Toc395637765"></a>Adición de un controlador</span><span class="sxs-lookup"><span data-stu-id="c9d5a-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="c9d5a-184">Que se encarga de hello **M**, ahora vamos a crear hello **C** en MVC, una clase de controlador.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-184">That takes care of hello **M**, now let's create hello **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="c9d5a-185">En **el Explorador de soluciones**, contextual hello **controladores** carpeta, haga clic en **agregar**y, a continuación, haga clic en **controlador**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-185">In **Solution Explorer**, right-click hello **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="c9d5a-186">Hola **agregar scaffolding** aparece el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-186">hello **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="c9d5a-187">Seleccione **Controlador MVC 5 - Vacío** y, a continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Captura de pantalla del cuadro de diálogo Agregar scaffolding Hola con hello controlador de MVC 5 - opción vacía resaltada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="c9d5a-189">Asigne un nombre al nuevo controlador, **ItemController.**</span><span class="sxs-lookup"><span data-stu-id="c9d5a-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Captura de pantalla del cuadro de diálogo Agregar controlador Hola](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="c9d5a-191">Una vez que se crea el archivo hello, debe ser similar a la solución de Visual Studio siguiente Hola con nuevo archivo de ItemController.cs hello en **el Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-191">Once hello file is created, your Visual Studio solution should resemble hello following with hello new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="c9d5a-192">También se muestra el nuevo archivo de Item.cs Hola creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-192">hello new Item.cs file created earlier is also shown.</span></span>
   
    ![Captura de pantalla de hello solución de Visual Studio - Explorador de soluciones con el archivo ItemController.cs nuevo de Hola y Item.cs resaltado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="c9d5a-194">Puede cerrar ItemController.cs, volveremos tooit más tarde.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-194">You can close ItemController.cs, we'll come back tooit later.</span></span> 

### <span data-ttu-id="c9d5a-195"><a name="_Toc395637766"></a>Adición de vistas</span><span class="sxs-lookup"><span data-stu-id="c9d5a-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="c9d5a-196">Ahora, vamos a crear hello **V** en MVC, Hola vistas:</span><span class="sxs-lookup"><span data-stu-id="c9d5a-196">Now, let's create hello **V** in MVC, hello views:</span></span>

* <span data-ttu-id="c9d5a-197">[Adición de una vista de índice de elementos](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="c9d5a-198">[Adición de una vista de elementos nuevos](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="c9d5a-199">[Adición de una vista de edición de elementos](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="c9d5a-200"><a name="AddItemIndexView"></a>Adición de una vista de índice de elementos</span><span class="sxs-lookup"><span data-stu-id="c9d5a-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="c9d5a-201">En **el Explorador de soluciones**, expanda hello **vistas** carpeta, contextual Hola vacía **elemento** carpeta que Visual Studio crea automáticamente cuando se agrega hello  **ItemController** anterior, haga clic en **agregar**y, a continuación, haga clic en **vista**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-201">In **Solution Explorer**, expand hello **Views**  folder, right-click hello empty **Item** folder that Visual Studio created for you when you added hello **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Captura de pantalla del explorador de soluciones con la carpeta de elementos de hello creados por Visual Studio con comandos de agregar vista Hola resaltados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="c9d5a-203">Hola **agregar vista** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9d5a-203">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="c9d5a-204">Hola **nombre de la vista** , escriba ***índice***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-204">In hello **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="c9d5a-205">Hola **plantilla** cuadro, seleccione ***lista***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-205">In hello **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="c9d5a-206">Hola **clase modelo** cuadro, seleccione ***elemento (lista de tareas. Modelos)***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-206">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="c9d5a-207">En el cuadro de página de diseño de hello, escriba ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-207">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Cuadro de diálogo Agregar vista de captura de pantalla que muestra hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="c9d5a-209">Después de que se hayan establecido todos estos valores, haga clic en **Agregar** y permita que Visual Studio cree una nueva vista de plantilla.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="c9d5a-210">Una vez que se hace esto, se abrirá el archivo cshtml hello que se creó.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-210">Once it is done, it will open hello cshtml file  that was created.</span></span> <span data-ttu-id="c9d5a-211">Podemos cerrar ese archivo en Visual Studio como se volverá tooit más tarde.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-211">We can close that file in Visual Studio as we will come back tooit later.</span></span>

#### <span data-ttu-id="c9d5a-212"><a name="AddNewIndexView"></a>Adición de una vista de elementos nuevos</span><span class="sxs-lookup"><span data-stu-id="c9d5a-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="c9d5a-213">Toohow similar que hemos creado un **índice del elemento** vista, ahora crearemos una nueva vista para crear nuevas **elementos**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-213">Similar toohow we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="c9d5a-214">En **el Explorador de soluciones**, contextual hello **elemento** de nuevo, haga clic en la carpeta **agregar**y, a continuación, haga clic en **vista**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-214">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="c9d5a-215">Hola **agregar vista** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9d5a-215">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="c9d5a-216">Hola **nombre de la vista** , escriba ***crear***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-216">In hello **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="c9d5a-217">Hola **plantilla** cuadro, seleccione ***crear***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-217">In hello **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="c9d5a-218">Hola **clase modelo** cuadro, seleccione ***elemento (lista de tareas. Modelos)***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-218">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="c9d5a-219">En el cuadro de página de diseño de hello, escriba ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-219">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="c9d5a-220">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="c9d5a-221"><a name="_Toc395888515"></a>Adición de una vista de edición de elementos</span><span class="sxs-lookup"><span data-stu-id="c9d5a-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="c9d5a-222">Por último, agregue una última vista para editar un **elemento** Hola igual que antes.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-222">And finally, add one last view for editing an **Item** in hello same way as before.</span></span>

1. <span data-ttu-id="c9d5a-223">En **el Explorador de soluciones**, contextual hello **elemento** de nuevo, haga clic en la carpeta **agregar**y, a continuación, haga clic en **vista**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-223">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="c9d5a-224">Hola **agregar vista** diálogo cuadro, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9d5a-224">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="c9d5a-225">Hola **nombre de la vista** , escriba ***editar***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-225">In hello **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="c9d5a-226">Hola **plantilla** cuadro, seleccione ***editar***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-226">In hello **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="c9d5a-227">Hola **clase modelo** cuadro, seleccione ***elemento (lista de tareas. Modelos)***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-227">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="c9d5a-228">En el cuadro de página de diseño de hello, escriba ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-228">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="c9d5a-229">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-229">Click **Add**.</span></span>

<span data-ttu-id="c9d5a-230">Una vez hecho esto, cierre todos los documentos de cshtml de hello en Visual Studio como se devolverán vistas toothese más tarde.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-230">Once this is done, close all hello cshtml documents in Visual Studio as we will return toothese views later.</span></span>

## <span data-ttu-id="c9d5a-231"><a name="_Toc395637769"></a>Paso 5: Conexión de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9d5a-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="c9d5a-232">Ahora que se prepara material MVC estándar hello, vamos a activar el código de hello tooadding para la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-232">Now that hello standard MVC stuff is taken care of, let's turn tooadding hello code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="c9d5a-233">En esta sección, se agregará código que sigue Hola toohandle:</span><span class="sxs-lookup"><span data-stu-id="c9d5a-233">In this section, we'll add code toohandle hello following:</span></span>

* <span data-ttu-id="c9d5a-234">[Lista de elementos incompletos](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="c9d5a-235">[Adición de elementos](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="c9d5a-236">[Edición de elementos](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="c9d5a-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="c9d5a-237"><a name="_Toc395637770"></a>Lista de elementos incompletos en la aplicación web MVC</span><span class="sxs-lookup"><span data-stu-id="c9d5a-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="c9d5a-238">Hello primer toodo de lo aquí es agregar una clase que contiene todos los tooconnect tooand usar base de datos de Azure Cosmos lógica de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-238">hello first thing toodo here is add a class that contains all hello logic tooconnect tooand use Azure Cosmos DB.</span></span> <span data-ttu-id="c9d5a-239">En este tutorial se a encapsular toda esta lógica en la clase de repositorio de tooa denominada DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-239">For this tutorial we'll encapsulate all this logic in tooa repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="c9d5a-240">En **el Explorador de soluciones**, haga doble clic en el proyecto de hello, haga clic en **agregar**y, a continuación, haga clic en **clase**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-240">In **Solution Explorer**, right-click on hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="c9d5a-241">Hola nueva clase el nombre **DocumentDBRepository** y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-241">Name hello new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="c9d5a-242">Hola recién creado **DocumentDBRepository** clase y agregue Hola siguiente *mediante instrucciones* anteriormente hello *espacio de nombres* declaración</span><span class="sxs-lookup"><span data-stu-id="c9d5a-242">In hello newly created **DocumentDBRepository** class and add hello following *using statements* above hello *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="c9d5a-243">Ahora, reemplace este código</span><span class="sxs-lookup"><span data-stu-id="c9d5a-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="c9d5a-244">con hello al siguiente código.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-244">with hello following code.</span></span>
   
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
   
    
3. <span data-ttu-id="c9d5a-245">Le estamos leer algunos valores de configuración, abra hello **Web.config** archivo de la aplicación y agregue Hola después de líneas que aparecen bajo hello `<AppSettings>` sección.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-245">We're reading some values from configuration, so open hello **Web.config** file of your application and add hello following lines under hello `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="c9d5a-246">Ahora, actualice los valores de hello de *extremo* y *SFF* mediante la hoja de claves de Hola de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-246">Now, update hello values for *endpoint* and *authKey* using hello Keys blade of hello Azure Portal.</span></span> <span data-ttu-id="c9d5a-247">Usar hello **URI** de hoja de claves de hello como valor de Hola de configuración de punto de conexión de Hola y Hola de uso **PRIMARY KEY**, o **clave secundaria** de hoja de claves de hello como valor de Hola Hola configuración de SFF.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-247">Use hello **URI** from hello Keys blade as hello value of hello endpoint setting, and use hello **PRIMARY KEY**, or **SECONDARY KEY** from hello Keys blade as hello value of hello authKey setting.</span></span>

    <span data-ttu-id="c9d5a-248">Que se encarga de cableado de repositorio de base de datos de Azure Cosmos hello, ahora vamos a agrega la lógica de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-248">That takes care of wiring up hello Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="c9d5a-249">Hello lo primero que queremos toobe puede toodo con una aplicación de lista de tareas es elementos incompleta de toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-249">hello first thing we want toobe able toodo with a todo list application is toodisplay hello incomplete items.</span></span>  <span data-ttu-id="c9d5a-250">Copie y pegue Hola siguiente fragmento de código en cualquier lugar de hello **DocumentDBRepository** clase.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-250">Copy and paste hello following code snippet anywhere within hello **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="c9d5a-251">Abra hello **ItemController** se agregó anteriormente y agregue los siguientes hello *mediante instrucciones* por encima de la declaración de espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-251">Open hello **ItemController** we added earlier and add hello following *using statements* above hello namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="c9d5a-252">Si el proyecto no se denomina "todo", a continuación, necesita tooupdate con "lista de tareas. Modelos"; nombre de hello tooreflect del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-252">If your project is not named "todo", then you need tooupdate using "todo.Models"; tooreflect hello name of your project.</span></span>
   
    <span data-ttu-id="c9d5a-253">Ahora, reemplace este código</span><span class="sxs-lookup"><span data-stu-id="c9d5a-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="c9d5a-254">con hello al siguiente código.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-254">with hello following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="c9d5a-255">Abra **Global.asax.cs** y agregue Hola después línea toohello **Application_Start** (método)</span><span class="sxs-lookup"><span data-stu-id="c9d5a-255">Open **Global.asax.cs** and add hello following line toohello **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="c9d5a-256">En este momento la solución debe ser capaz de toobuild sin errores.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-256">At this point your solution should be able toobuild without any errors.</span></span>

<span data-ttu-id="c9d5a-257">Si ha ejecutado ahora la aplicación hello, quedarían toohello **HomeController** hello y **índice** vista de ese controlador.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-257">If you ran hello application now, you would go toohello **HomeController** and hello **Index** view of that controller.</span></span> <span data-ttu-id="c9d5a-258">Se trata de comportamiento predeterminado de Hola para proyecto de plantilla MVC Hola que elegimos al principio de hello pero no queremos!</span><span class="sxs-lookup"><span data-stu-id="c9d5a-258">This is hello default behavior for hello MVC template project we chose at hello start but we don't want that!</span></span> <span data-ttu-id="c9d5a-259">Vamos a cambiar Hola enrutamiento en este tooalter de aplicación de MVC este comportamiento.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-259">Let's change hello routing on this MVC application tooalter this behavior.</span></span>

<span data-ttu-id="c9d5a-260">Abra ***aplicación\_Start\RouteConfig.cs*** y busque la línea hello a partir de "valores predeterminados:" y cámbielo hello tooresemble después.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-260">Open ***App\_Start\RouteConfig.cs*** and locate hello line starting with "defaults:" and change it tooresemble hello following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="c9d5a-261">Ahora Esto indica a ASP.NET MVC que si no ha especificado un valor en toocontrol de dirección URL de Hola Hola comportamiento de enrutamiento que, en lugar de **inicio**, use **elemento** como controlador de Hola y usuario **índice** como vista de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-261">This now tells ASP.NET MVC that if you have not specified a value in hello URL toocontrol hello routing behavior that instead of **Home**, use **Item** as hello controller and user **Index** as hello view.</span></span>

<span data-ttu-id="c9d5a-262">Ahora si ejecuta la aplicación hello, llamará a su **ItemController** que se llame en clase de repositorio toohello y use Hola GetItems método tooreturn todos Hola elementos incompletos toohello **vistas** \\ **Elemento**\\**índice** vista.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-262">Now if you run hello application, it will call into your **ItemController** which will call in toohello repository class and use hello GetItems method tooreturn all hello incomplete items toohello **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="c9d5a-263">Si crea y ejecuta este proyecto ahora, deberá ver algo parecido a esto.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Captura de pantalla de creados por este tutorial de base de datos de aplicación del web de lista de tareas Hola](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="c9d5a-265"><a name="_Toc395637771"></a>Adición de elementos</span><span class="sxs-lookup"><span data-stu-id="c9d5a-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="c9d5a-266">Pongamos algunos elementos en nuestra base de datos, así tendremos algo más que un toolook cuadrícula vacía en.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-266">Let's put some items into our database so we have something more than an empty grid toolook at.</span></span>

<span data-ttu-id="c9d5a-267">Agreguemos algún código de registro de hello toopersist Azure Cosmos DBRepository y ItemController en la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-267">Let's add some code too Azure Cosmos DBRepository and ItemController toopersist hello record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="c9d5a-268">Agregar Hola siguiendo el método tooyour **DocumentDBRepository** clase.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-268">Add hello following method tooyour **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="c9d5a-269">Este método simplemente toma un objeto pasado tooit y lo almacena en la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-269">This method simply takes an object passed tooit and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="c9d5a-270">Abra el archivo de ItemController.cs hello y agregue Hola siguiente fragmento de código dentro de la clase hello.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-270">Open hello ItemController.cs file and add hello following code snippet within hello class.</span></span> <span data-ttu-id="c9d5a-271">Se trata cómo ASP.NET MVC sabe qué toodo para hello **crear** acción.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-271">This is how ASP.NET MVC knows what toodo for hello **Create** action.</span></span> <span data-ttu-id="c9d5a-272">En este caso simplemente representación Hola asociado vista Create.cshtml que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-272">In this case just render hello associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="c9d5a-273">Ahora necesitamos algunos más código de este controlador que acepte el envío de Hola Hola **crear** vista.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-273">We now need some more code in this controller that will accept hello submission from hello **Create** view.</span></span>
3. <span data-ttu-id="c9d5a-274">Agregar Hola siguiente bloque de código toohello clase ItemController.cs que indica qué toodo con un formulario POST para este controlador de MVC de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-274">Add hello next block of code toohello ItemController.cs class that tells ASP.NET MVC what toodo with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="c9d5a-275">Este código llama en toohello DocumentDBRepository y utiliza hello CreateItemAsync método toopersist Hola todo elemento toohello base de datos nueva.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-275">This code calls in toohello DocumentDBRepository and uses hello CreateItemAsync method toopersist hello new todo item toohello database.</span></span> 
   
    <span data-ttu-id="c9d5a-276">**Nota de seguridad**: Hola **ValidateAntiForgeryToken** atributo se utiliza aquí toohelp proteger esta aplicación frente a ataques de falsificación de solicitud entre sitios.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-276">**Security Note**: hello **ValidateAntiForgeryToken** attribute is used here toohelp protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="c9d5a-277">Hay más tooit que limitarse a agregar este atributo, las vistas necesitan toowork con este token antifalsificación así.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-277">There is more tooit than just adding this attribute, your views need toowork with this anti-forgery token as well.</span></span> <span data-ttu-id="c9d5a-278">Para obtener más información sobre el sujeto de Hola y ejemplos de cómo tooimplement esto correctamente, vea [evitar falsificación de solicitud entre sitios][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="c9d5a-278">For more on hello subject, and examples of how tooimplement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="c9d5a-279">Hola código fuente ofrecido en [GitHub] [ GitHub] tiene implementación completa de hello en su lugar.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-279">hello source code provided on [GitHub][GitHub] has hello full implementation in place.</span></span>
   
    <span data-ttu-id="c9d5a-280">**Nota de seguridad**: También utilizamos hello **enlazar** atributo toohelp de parámetro de método hello protegerse exceso contabilización ataques.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-280">**Security Note**: We also use hello **Bind** attribute on hello method parameter toohelp protect against over-posting attacks.</span></span> <span data-ttu-id="c9d5a-281">Para más información, consulte el artículo sobre [operaciones CRUD básicas en ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="c9d5a-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="c9d5a-282">Esto concluye Hola código necesario tooadd nueva elementos tooour base de datos.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-282">This concludes hello code required tooadd new Items tooour database.</span></span>

### <span data-ttu-id="c9d5a-283"><a name="_Toc395637772"></a>Edición de elementos</span><span class="sxs-lookup"><span data-stu-id="c9d5a-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="c9d5a-284">Hay una última cosa que nos toodo, y que es tooadd Hola capacidad tooedit **elementos** en la base de datos de Hola y toomark como completa.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-284">There is one last thing for us toodo, and that is tooadd hello ability tooedit **Items** in hello database and toomark them as complete.</span></span> <span data-ttu-id="c9d5a-285">Hello vista de edición ya se ha agregado toohello proyecto, por lo que debemos tooadd algunos código controlador tooour y toohello **DocumentDBRepository** clase de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-285">hello view for editing was already added toohello project, so we just need tooadd some code tooour controller and toohello **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="c9d5a-286">Agregar Hola después toohello **DocumentDBRepository** clase.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-286">Add hello following toohello **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="c9d5a-287">Hola primero de estos métodos, **GetItem** captura un elemento de la base de datos de Cosmos de Azure que se pasa toohello Atrás **ItemController** y, a continuación, en toohello **editar** vista.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-287">hello first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back toohello **ItemController** and then on toohello **Edit** view.</span></span>
   
    <span data-ttu-id="c9d5a-288">Hola segundo de los métodos de Hola que acabamos de agregar reemplaza hello **documento** en la base de datos de Azure Cosmos con la versión de Hola de hello **documento** pasados desde hello **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-288">hello second of hello methods we just added replaces hello **Document** in Azure Cosmos DB with hello version of hello **Document** passed in from hello **ItemController**.</span></span>
2. <span data-ttu-id="c9d5a-289">Agregar Hola después toohello **ItemController** clase.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-289">Add hello following toohello **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="c9d5a-290">Hello primer método controla Hola Http GET que se produce cuando hace clic en usuario de hello en hello **editar** vínculo de hello **índice** vista.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-290">hello first method handles hello Http GET that happens when hello user clicks on hello **Edit** link from hello **Index** view.</span></span> <span data-ttu-id="c9d5a-291">Este método captura un [ **documento** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) de base de datos de Azure Cosmos y pasa toohello **editar** vista.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it toohello **Edit** view.</span></span>
   
    <span data-ttu-id="c9d5a-292">Hola **editar** vista, a continuación, realizará un Http POST toohello **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-292">hello **Edit** view will then do an Http POST toohello **IndexController**.</span></span> 
   
    <span data-ttu-id="c9d5a-293">segundo método de Hello agregamos identificadores pasar Hola actualizar objeto tooAzure Cosmos DB toobe se conserva en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-293">hello second method we added handles passing hello updated object tooAzure Cosmos DB toobe persisted in hello database.</span></span>

<span data-ttu-id="c9d5a-294">¡Eso es todo, que es todo lo necesario toorun nuestra aplicación, se muestran incompletos **elementos**, agregar nuevas **elementos**y editar **elementos**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-294">That's it, that is everything we need toorun our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="c9d5a-295"><a name="_Toc395637773"></a>Paso 6: Ejecutar aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="c9d5a-295"><a name="_Toc395637773"></a>Step 6: Run hello application locally</span></span>
<span data-ttu-id="c9d5a-296">aplicación de hello tootest en el equipo local, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9d5a-296">tootest hello application on your local machine, do hello following:</span></span>

1. <span data-ttu-id="c9d5a-297">Presione F5 en la aplicación de Visual Studio toobuild hello en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-297">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span> <span data-ttu-id="c9d5a-298">Debe compilar la aplicación hello e iniciar un explorador con la página de cuadrícula vacía Hola que hemos visto antes:</span><span class="sxs-lookup"><span data-stu-id="c9d5a-298">It should build hello application and launch a browser with hello empty grid page we saw before:</span></span>
   
    ![Captura de pantalla de creados por este tutorial de base de datos de aplicación del web de lista de tareas Hola](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="c9d5a-300">Haga clic en hello **crear nuevo** vincular y agregar valores toohello **nombre** y **descripción** campos.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-300">Click hello **Create New** link and add values toohello **Name** and **Description** fields.</span></span> <span data-ttu-id="c9d5a-301">Deje hello **completado** casilla de verificación no está seleccionada en caso contrario Hola de nuevo **elemento** se agregarán en un estado completado y no aparecerán en la lista inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-301">Leave hello **Completed** check box unselected otherwise hello new **Item** will be added in a completed state and will not appear on hello initial list.</span></span>
   
    ![Captura de pantalla de hello Crear vista](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="c9d5a-303">Haga clic en **crear** y es redirigido toohello Atrás **índice** vista y su **elemento** aparece en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-303">Click **Create** and you are redirected back toohello **Index** view and your **Item** appears in hello list.</span></span>
   
    ![Captura de pantalla de hello vista de índice](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="c9d5a-305">Sentirse tooadd libre más unos **elementos** tooyour lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-305">Feel free tooadd a few more **Items** tooyour todo list.</span></span>
    
4. <span data-ttu-id="c9d5a-306">Haga clic en **editar** tooan siguiente **elemento** en la lista de Hola y se toman toohello **editar** vista en la que puede actualizar cualquier propiedad de su objeto, incluidos hello  **Completado** marca.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-306">Click **Edit** next tooan **Item** on hello list and you are taken toohello **Edit** view where you can update any property of your object, including hello **Completed** flag.</span></span> <span data-ttu-id="c9d5a-307">Si marca hello **completar** marca y haga clic en **guardar**, hello **elemento** se quita de la lista de Hola de tareas incompletas.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-307">If you mark hello **Complete** flag and click **Save**, hello **Item** is removed from hello list of incomplete tasks.</span></span>
   
    ![Captura de pantalla de hello vista de índice con hello completado casilla activada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="c9d5a-309">Una vez que ha probado la aplicación hello, presione toostop Ctrl + F5 para depurar aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-309">Once you've tested hello app, press Ctrl+F5 toostop debugging hello app.</span></span> <span data-ttu-id="c9d5a-310">Está listo toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-310">You're ready toodeploy!</span></span>

## <span data-ttu-id="c9d5a-311"><a name="_Toc395637774"></a>Paso 7: Implementar Hola aplicación tooAzure servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c9d5a-311"><a name="_Toc395637774"></a>Step 7: Deploy hello application tooAzure App Service</span></span> 
<span data-ttu-id="c9d5a-312">Ahora que tiene la aplicación completa de hello funciona correctamente con la base de datos de Azure Cosmos vamos toodeploy esta tooAzure de aplicación web servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-312">Now that you have hello complete application working correctly with Azure Cosmos DB we're going toodeploy this web app tooAzure App Service.</span></span>  

1. <span data-ttu-id="c9d5a-313">Esta aplicación todos los necesita toodo no toopublish es haga doble clic en el proyecto de hello en **el Explorador de soluciones** y haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-313">toopublish this application all you need toodo is right-click on hello project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Captura de pantalla de hello opción Publicar en el Explorador de soluciones](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="c9d5a-315">Hola **publicar** cuadro de diálogo, haga clic en **servicio de aplicaciones de Microsoft Azure**, a continuación, seleccione **crear nuevo** toocreate un servicio de aplicaciones de perfil, o haga clic en **seleccionar Existente** toouse un perfil existente.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-315">In hello **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** toocreate an App Service profile, or click **Select Existing** toouse an existing profile.</span></span>

    ![Cuadro de diálogo Publicar en Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="c9d5a-317">Si tiene un perfil de Azure App Service existente, escriba el nombre de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="c9d5a-318">Hola de uso **vista** filtrar toosort por tipo de recurso o grupo de recursos, a continuación, seleccione el servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-318">Use hello **View** filter toosort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Cuadro de diálogo App Service en Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="c9d5a-320">toocreate un nuevo perfil de servicio de aplicaciones de Azure, haga clic en **crear nuevo** en hello **publicar** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-320">toocreate a new Azure App Service profile, click **Create New** in hello **Publish** dialog box.</span></span> <span data-ttu-id="c9d5a-321">Hola **crear servicio en la aplicación** cuadro de diálogo, escriba el nombre de la aplicación Web y la suscripción adecuada, el grupo de recursos y el plan de servicio de aplicaciones, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-321">In hello **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Cuadro de diálogo Crear App Service en Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="c9d5a-323">En pocos segundos, Visual Studio terminará de publicar la aplicación web y ejecutará un explorador donde podrá ver su trabajo ejecutándose en Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="c9d5a-324"><a name="_Toc395637775"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9d5a-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="c9d5a-325">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="c9d5a-325">Congratulations!</span></span> <span data-ttu-id="c9d5a-326">Simplemente había creado su primer ASP.NET MVC de aplicación web mediante la base de datos de Azure Cosmos y haberlo publicado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it tooAzure.</span></span> <span data-ttu-id="c9d5a-327">Hola código fuente de la aplicación completa de hello, incluidos los detalles de Hola y eliminar funciones que no se incluyeron en este tutorial se puede descargar o clonado a partir de [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="c9d5a-327">hello source code for hello complete application, including hello detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="c9d5a-328">Por lo que si está interesado en Agregar aplicación tooyour, agarre el código de hello y Agregar aplicación toothis.</span><span class="sxs-lookup"><span data-stu-id="c9d5a-328">So if you're interested in adding that tooyour app, grab hello code and add it toothis app.</span></span>

<span data-ttu-id="c9d5a-329">aplicación de tooyour tooadd funcionalidad adicional, revisión Hola API disponibles en hello [biblioteca de .NET de base de datos de Azure Cosmos](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) y Siéntase libre toocontribute toohello Azure Cosmos DB .NET Library en [GitHub] [GitHub].</span><span class="sxs-lookup"><span data-stu-id="c9d5a-329">tooadd additional functionality tooyour application, review hello APIs available in hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free toocontribute toohello Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
