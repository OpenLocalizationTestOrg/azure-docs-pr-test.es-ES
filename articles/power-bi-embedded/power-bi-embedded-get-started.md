---
title: "Introducción a Microsoft Power BI Embedded"
description: "Power BI Embedded, agregar informes interactivos de Power BI a la aplicación de inteligencia empresarial"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 4afa8d2c7f8ec1942521ba5fa131967dfd581c91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="1a304-103">Introducción a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="1a304-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="1a304-104">**Power BI Embedded** es un servicio de Azure que permite a los desarrolladores de aplicaciones agregar informes de Power BI interactivos a sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1a304-104">**Power BI Embedded** is an Azure service that enables application developers to add interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="1a304-105">**Power BI Embedded** se puede utilizar con las aplicaciones existentes sin necesidad de modificar el diseño ni de cambiar el modo en que los usuarios inician sesión.</span><span class="sxs-lookup"><span data-stu-id="1a304-105">**Power BI Embedded** works with existing applications without needing redesign or changing the way users sign in.</span></span>

<span data-ttu-id="1a304-106">Los recursos de **Microsoft Power BI Embedded** se aprovisionan mediante las [API de ARM de Azure](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a304-106">Resources for **Microsoft Power BI Embedded** are provisioned through the [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="1a304-107">En este caso, el recurso que se aprovisiona es una **colección de áreas de trabajo de Power BI**.</span><span class="sxs-lookup"><span data-stu-id="1a304-107">In this case, the resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="1a304-108">Creación de una colección de áreas de trabajo</span><span class="sxs-lookup"><span data-stu-id="1a304-108">Create a workspace collection</span></span>

<span data-ttu-id="1a304-109">Una **colección de áreas de trabajo** es el recurso de Azure de nivel superior, y funciona como un contenedor del contenido que se insertará en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a304-109">A **Workspace Collection** is the top-level Azure resource and a container for the content that will be embedded in your application.</span></span> <span data-ttu-id="1a304-110">Las **colecciones de áreas de trabajo** se pueden crear de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="1a304-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="1a304-111">Manualmente mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a304-111">Manually using the Azure Portal</span></span>
* <span data-ttu-id="1a304-112">Mediante programación con la API de Azure Resource Manager (ARM).</span><span class="sxs-lookup"><span data-stu-id="1a304-112">Programmatically using the Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="1a304-113">Vamos a ver cuáles son los pasos necesarios para crear una **colección de áreas de trabajo** mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1a304-113">Let's walk through the steps to build a **Workspace Collection** using the Azure Portal.</span></span>

1. <span data-ttu-id="1a304-114">Abra el **Portal de Azure**, [http://portal.azure.com](http://portal.azure.com), e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="1a304-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="1a304-115">En el panel superior, haga clic en **+ Nuevo** .</span><span class="sxs-lookup"><span data-stu-id="1a304-115">Click **+ New** on the top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="1a304-116">En **Datos y análisis**, haga clic en **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="1a304-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="1a304-117">En la **hoja Colección de áreas de trabajo de Power BI**, escriba la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="1a304-117">On the **Workspace Collection Blade**, enter the required information.</span></span> <span data-ttu-id="1a304-118">En **Precios**, consulte los [precios de Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="1a304-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="1a304-119">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1a304-119">Click **Create**.</span></span>

<span data-ttu-id="1a304-120">La **colección de áreas de trabajo** tarda un poco en aprovisionarse.</span><span class="sxs-lookup"><span data-stu-id="1a304-120">The **Workspace Collection** will take a few moments to provision.</span></span> <span data-ttu-id="1a304-121">Cuando la operación finalice, accederá automáticamente a la hoja **Colección de áreas de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="1a304-121">When completed, you'll be taken to the **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="1a304-122">La hoja **Creación** contiene la información que necesita para llamar a las API que crean las áreas de trabajo e implementan contenido en ellas.</span><span class="sxs-lookup"><span data-stu-id="1a304-122">The **Creation Blade** contains the information you need to call the APIs that create workspaces and deploy content to them.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="1a304-123">Visualización de las claves de acceso de API de Power BI</span><span class="sxs-lookup"><span data-stu-id="1a304-123">View Power BI API access keys</span></span>

<span data-ttu-id="1a304-124">Uno de los datos más importantes que se necesitan para llamar a las API de REST de Power BI son las **claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="1a304-124">One of the most important pieces of information needed to call the Power BI REST APIs are the **Access Keys**.</span></span> <span data-ttu-id="1a304-125">Las claves de acceso se utilizan para generar los **tokens de aplicación** que se emplean para autenticar las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="1a304-125">These are used to generate the **app tokens** that are used to authenticate your API requests.</span></span> <span data-ttu-id="1a304-126">Para ver las **claves de acceso**, haga clic en **Claves de acceso** en la hoja **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="1a304-126">To view your **Access Keys**, click **Access Keys** on the **Settings Blade**.</span></span> <span data-ttu-id="1a304-127">Para más información sobre los **tokens de aplicación**, consulte [Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="1a304-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="1a304-128">Verá que tiene dos claves.</span><span class="sxs-lookup"><span data-stu-id="1a304-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="1a304-129">Copie estas claves y almacénelas de forma segura en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a304-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="1a304-130">Es muy importante tratar estas claves igual que una contraseña, ya que proporcionan acceso a todo el contenido de la **colección de áreas de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="1a304-130">It's very important that you treat these keys as you would a password, because they'll provide access to all the content in your **Workspace Collection**.</span></span>

<span data-ttu-id="1a304-131">Aunque se muestran dos claves, solo se necesita una cada vez.</span><span class="sxs-lookup"><span data-stu-id="1a304-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="1a304-132">La segunda clave se proporciona para que pueda regenerar periódicamente las claves sin interrumpir el acceso al servicio.</span><span class="sxs-lookup"><span data-stu-id="1a304-132">The second key is provided so you can periodically regenerate keys without interrupting access to the service.</span></span>

<span data-ttu-id="1a304-133">Ahora que tiene una instancia de Power BI para la aplicación y las **claves de acceso**, puede importar un informe en la propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a304-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="1a304-134">Antes de aprender a importar un informe, en la sección siguiente se describe la creación de conjuntos de datos e informes de Power BI para insertar en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a304-134">Before you learn how to import a report, the next section describes creating Power BI datasets and reports to embed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="1a304-135">Trabajo con áreas de trabajo</span><span class="sxs-lookup"><span data-stu-id="1a304-135">Working with workspaces</span></span>

<span data-ttu-id="1a304-136">Después de haber creado la colección de áreas de trabajo, debe crear un área de trabajo que hospede los informes y conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="1a304-136">After you have created your workspace collection, you will need to create a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="1a304-137">Para crear un área de trabajo, debe usar la [API de REST de Post Workspace](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a304-137">To create a workspace, you will need to use the [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="1a304-138">Creación de conjuntos de datos e informes de Power BI para insertar en una aplicación mediante Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="1a304-138">Create Power BI datasets and reports to embed into an app using Power BI Desktop</span></span>

<span data-ttu-id="1a304-139">Ahora que ha creado una instancia de Power BI para su aplicación y tiene las **claves de acceso**, deberá crear los conjuntos de datos y los informes de Power BI que quiere insertar.</span><span class="sxs-lookup"><span data-stu-id="1a304-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need to create the Power BI datasets and reports that you want to embed.</span></span> <span data-ttu-id="1a304-140">Los conjuntos de datos y los informes se pueden crear con **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="1a304-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="1a304-141">Puede descargar [Power BI Desktop gratis](https://go.microsoft.com/fwlink/?LinkId=521662).</span><span class="sxs-lookup"><span data-stu-id="1a304-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="1a304-142">Por otro lado, si desea empezar a trabajar rápidamente, también puede descargar el [archivo PBIX con un ejemplo de análisis de minoristas](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="1a304-142">Or, to quickly get started, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="1a304-143">Para aprender más acerca de cómo usar **Power BI Desktop**, consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="1a304-143">To learn more about how to use **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="1a304-144">Con **Power BI Desktop**, para conectarse al origen de datos, puede importar una copia de los datos en **Power BI Desktop** o conectarse directamente al origen de datos mediante **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="1a304-144">With **Power BI Desktop**, you connect to your data source by importing a copy of the data into **Power BI Desktop** or connecting directly to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="1a304-145">Estas son las diferencias entre usar **Importación** y **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="1a304-145">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="1a304-146">Importar</span><span class="sxs-lookup"><span data-stu-id="1a304-146">Import</span></span> | <span data-ttu-id="1a304-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="1a304-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="1a304-148">Las tablas, las columnas y los *datos* se importan o se copian en **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="1a304-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="1a304-149">Mientras trabaja con visualizaciones, **Power BI Desktop** consulta una copia de los datos.</span><span class="sxs-lookup"><span data-stu-id="1a304-149">As you work with visualizations, **Power BI Desktop** queries a copy of the data.</span></span> <span data-ttu-id="1a304-150">Para ver los cambios que se han producido en los datos subyacentes, debe actualizar o importar de nuevo un conjunto de datos actual completo.</span><span class="sxs-lookup"><span data-stu-id="1a304-150">To see any changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="1a304-151">En *Power BI Desktop* , solo se importan o copian **tablas y columnas**.</span><span class="sxs-lookup"><span data-stu-id="1a304-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="1a304-152">Mientras trabaja con visualizaciones, **Power BI Desktop** consulta el origen de datos subyacente, lo que significa que siempre verá los datos actuales.</span><span class="sxs-lookup"><span data-stu-id="1a304-152">As you work with visualizations, **Power BI Desktop** queries the underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="1a304-153">Para más información acerca de cómo conectarse a un origen de datos, consulte [Conectarse a un origen de datos](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="1a304-153">For more about connecting to a data source, see [Connect to a data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="1a304-154">Cuando guarde el trabajo en **Power BI Desktop**, se creará un archivo PBIX.</span><span class="sxs-lookup"><span data-stu-id="1a304-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="1a304-155">Este archivo contiene el informe.</span><span class="sxs-lookup"><span data-stu-id="1a304-155">This file contains your report.</span></span> <span data-ttu-id="1a304-156">Además, si los datos se han importado, el archivo PBIX contendrá el conjunto de datos completo, mientras que, si se ha utilizado **DirectQuery**, el archivo PBIX solamente contendrá un esquema del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a304-156">In addition, if you import data the PBIX contains the complete dataset, or if you use **DirectQuery**, the PBIX contains just a dataset schema.</span></span> <span data-ttu-id="1a304-157">Puede implementar el archivo PBIX mediante programación en su área de trabajo con la [API de importación de Power BI](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a304-157">You programmatically deploy the PBIX into your workspace using the [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="1a304-158">**Power BI Embedded** incluye API adicionales que permiten cambiar el servidor y la base de datos a los que apunta el conjunto de datos y definir una credencial de cuenta de servicio, que será la que use el conjunto de datos para conectarse a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="1a304-158">**Power BI Embedded** has additional APIs to change the server and database that your dataset is pointing to and set a service account credential that the dataset will use to connect to your database.</span></span> <span data-ttu-id="1a304-159">Consulte [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) y [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx) (Revisión de origen de datos de puerta de enlace).</span><span class="sxs-lookup"><span data-stu-id="1a304-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="1a304-160">Creación de conjuntos de datos e informes de Power BI con las API</span><span class="sxs-lookup"><span data-stu-id="1a304-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="1a304-161">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="1a304-161">Datsets</span></span>

<span data-ttu-id="1a304-162">Puede crear conjuntos de datos en Power BI Embedded mediante la API de REST.</span><span class="sxs-lookup"><span data-stu-id="1a304-162">You can create datasets within Power BI Embedded using the REST API.</span></span> <span data-ttu-id="1a304-163">Luego, puede insertar datos en el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="1a304-163">You can then push data into your dataset.</span></span> <span data-ttu-id="1a304-164">De esta forma puede trabajar con datos sin necesidad de Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="1a304-164">This allows you to work with data without the need of Power BI Desktop.</span></span> <span data-ttu-id="1a304-165">Para más información, consulte [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Publicación de conjuntos de datos).</span><span class="sxs-lookup"><span data-stu-id="1a304-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="1a304-166">Informes</span><span class="sxs-lookup"><span data-stu-id="1a304-166">Reports</span></span>

<span data-ttu-id="1a304-167">Puede crear un informe a partir de un conjunto de datos directamente en la aplicación mediante la API de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1a304-167">You can create a report from a dataset directly in your application using the JavaScript API.</span></span> <span data-ttu-id="1a304-168">Para más información, consulte [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creación de un nuevo informe a partir de un conjunto de datos en Power BI Embedded).</span><span class="sxs-lookup"><span data-stu-id="1a304-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1a304-169">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="1a304-169">See Also</span></span>

[<span data-ttu-id="1a304-170">Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)</span><span class="sxs-lookup"><span data-stu-id="1a304-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="1a304-171">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="1a304-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="1a304-172">Inserción de un informe</span><span class="sxs-lookup"><span data-stu-id="1a304-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="1a304-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creación de un nuevo informe a partir de un conjunto de datos en Power BI Embedded) 
[Save reports](power-bi-embedded-save-reports.md) (Guardar informes)</span><span class="sxs-lookup"><span data-stu-id="1a304-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="1a304-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="1a304-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
<span data-ttu-id="1a304-175">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="1a304-175">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)</span></span>  
<span data-ttu-id="1a304-176">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="1a304-176">More questions?</span></span> [<span data-ttu-id="1a304-177">Pruebe la comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="1a304-177">Try the Power BI Community</span></span>](http://community.powerbi.com/)

