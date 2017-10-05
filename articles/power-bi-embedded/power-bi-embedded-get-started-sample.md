---
title: "Introducción a un ejemplo"
description: "Power BI Embedded, usar el SDK para agregar informes interactivos de Power BI a la aplicación de inteligencia empresarial"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: c3cb1763f807220a4a829f410d7eb77974b25776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="65f6c-103">Introducción a un ejemplo de Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="65f6c-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="65f6c-104">Con **Microsoft Power BI Embedded**, puede integrar informes de Power BI directamente en las aplicaciones web o móviles.</span><span class="sxs-lookup"><span data-stu-id="65f6c-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="65f6c-105">En este artículo, ofreceremos el ejemplo introductorio de **Power BI Embedded** .</span><span class="sxs-lookup"><span data-stu-id="65f6c-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="65f6c-106">Antes de avanzar, probablemente deseará guardar los recursos siguientes.</span><span class="sxs-lookup"><span data-stu-id="65f6c-106">Before we go any further, you'll probably want to save the following resources.</span></span> <span data-ttu-id="65f6c-107">Nos permitirán integrar informes de Power BI en la aplicación de ejemplo y también sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="65f6c-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span></span>

* [<span data-ttu-id="65f6c-108">Aplicación web de área de trabajo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="65f6c-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="65f6c-109">Referencia de API Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="65f6c-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="65f6c-110">[SDK de .NET de Power BI Embedded ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponible a través de NuGet)</span><span class="sxs-lookup"><span data-stu-id="65f6c-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="65f6c-111">Ejemplo de inserción de informe de JavaScript</span><span class="sxs-lookup"><span data-stu-id="65f6c-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="65f6c-112">Para poder configurar y ejecutar el ejemplo introductorio de Power BI Embedded, debe crear al menos una **colección de área de trabajo** en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="65f6c-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="65f6c-113">Para ver cómo crear una **colección de áreas de trabajo** en Azure Portal, consulte [Introducción a la versión preliminar de Microsoft Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="65f6c-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-the-sample-app"></a><span data-ttu-id="65f6c-114">Configuración de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="65f6c-114">Configure the sample app</span></span>

<span data-ttu-id="65f6c-115">Veamos la configuración del entorno de desarrollo de Visual Studio para acceder a los componentes necesarios para ejecutar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="65f6c-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span></span>

1. <span data-ttu-id="65f6c-116">Descargue y descomprima el ejemplo [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) (Power BI Embedded - Integración de un informe en una aplicación web) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="65f6c-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="65f6c-117">Abra **PowerBI embedded.sln** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65f6c-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="65f6c-118">Puede que necesite ejecutar el comando **Update-Package** en la Consola del Administrador de paquetes NuGET para actualizar los paquetes utilizados en esta solución.</span><span class="sxs-lookup"><span data-stu-id="65f6c-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span></span>
3. <span data-ttu-id="65f6c-119">Compile la solución.</span><span class="sxs-lookup"><span data-stu-id="65f6c-119">Build the solution.</span></span>
4. <span data-ttu-id="65f6c-120">Ejecute la aplicación de consola **ProvisionSample** .</span><span class="sxs-lookup"><span data-stu-id="65f6c-120">Run the **ProvisionSample** console app.</span></span> <span data-ttu-id="65f6c-121">En la aplicación de consola del ejemplo, aprovisione un área de trabajo e importe un archivo PBIX.</span><span class="sxs-lookup"><span data-stu-id="65f6c-121">In the sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="65f6c-122">Para aprovisionar una nueva **área de trabajo**, seleccione la opción 1, **Collection management** (Administración de colecciones), y luego seleccione la opción 6, **Provision a new Workspace** (Aprovisionar una nueva área de trabajo).</span><span class="sxs-lookup"><span data-stu-id="65f6c-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="65f6c-123">Para importar un nuevo **informe**, seleccione la opción 2, **Report management** (Administración de informes) y luego seleccione la opción 3, **Import PBIX Desktop file into a workspace** (Importar archivo PBIX de Desktop en un área de trabajo).</span><span class="sxs-lookup"><span data-stu-id="65f6c-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="65f6c-124">Escriba el nombre de su **colección de área de trabajo** y la **clave de acceso**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="65f6c-125">Puede obtener las claves en **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-125">You can get these in the **Azure Portal**.</span></span> <span data-ttu-id="65f6c-126">Para obtener más información sobre cómo obtener la **clave de acceso**, consulte [Visualización de las claves de acceso de API de Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) en Introducción a la versión preliminar de Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="65f6c-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="65f6c-127">Copie y guarde el recién creado **identificador del área de trabajo** para utilizarlo más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="65f6c-127">Copy and save the newly created **Workspace ID** to use later in this article.</span></span> <span data-ttu-id="65f6c-128">Una vez creado el **identificador del área de trabajo**, **Azure Portal** puede encontrarlo.</span><span class="sxs-lookup"><span data-stu-id="65f6c-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="65f6c-129">Para importar un archivo PBIX en su **área de trabajo**, seleccione la opción **6. Importe el archivo de escritorio PBIX en un área de trabajo existente**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="65f6c-130">Si no tiene una archivo PBIX a mano, puede descargar la [muestra de PBIX de análisis comercial](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="65f6c-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="65f6c-131">Si se le solicita, escriba un nombre descriptivo para su **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="65f6c-132">Debería obtener una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="65f6c-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="65f6c-133">Si el archivo PBIX contiene las conexiones de consulta directa, ejecute la opción 7 para actualizar las cadenas de conexión.</span><span class="sxs-lookup"><span data-stu-id="65f6c-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span></span>

<span data-ttu-id="65f6c-134">En este momento, tiene un informe PBIX de Power BI importado en su **área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="65f6c-135">Ahora, veamos cómo ejecutar la aplicación web de ejemplo introductorio de **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-the-sample-web-app"></a><span data-ttu-id="65f6c-136">Ejecución de la aplicación web de ejemplo</span><span class="sxs-lookup"><span data-stu-id="65f6c-136">Run the sample web app</span></span>
<span data-ttu-id="65f6c-137">El ejemplo de aplicación web es una aplicación de ejemplo que representa los informes importados a su **área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="65f6c-138">Vea cómo configurar el ejemplo de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="65f6c-138">Here's how to configure the web app sample.</span></span>

1. <span data-ttu-id="65f6c-139">En la solución de Visual Studio **PowerBI-embedded**, haga clic con el botón derecho en la aplicación web **EmbedSample** y elija **Establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="65f6c-140">En **web.config**, en la aplicación web **EmbedSample**, edite los valores de **appSettings**: **AccessKey**, nombre de **WorkspaceCollection** y **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="65f6c-141">Ejecute la aplicación web **EmbedSample**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-141">Run the **EmbedSample** web application.</span></span>

<span data-ttu-id="65f6c-142">Una vez ejecutada la aplicación web **EmbedSample**, el panel de navegación izquierdo debe contener un menú **Informes** menú.</span><span class="sxs-lookup"><span data-stu-id="65f6c-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="65f6c-143">Para ver el informe que ha importado, expanda **Informes** y haga clic en un informe.</span><span class="sxs-lookup"><span data-stu-id="65f6c-143">To view the report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="65f6c-144">Por ejemplo, si ha importado la [muestra de PBIX de análisis comercial](http://go.microsoft.com/fwlink/?LinkID=780547), la aplicación web de muestra tendría el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="65f6c-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="65f6c-145">Tras hacer clic en un informe, la aplicación web **EmbedSample** debe tener un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="65f6c-145">After you click a report, the **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a><span data-ttu-id="65f6c-146">Exploración del código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="65f6c-146">Explore the sample code</span></span>

<span data-ttu-id="65f6c-147">El ejemplo de **Microsoft Power BI Embedded** es una aplicación web de panel de ejemplo que muestra cómo integrar informes de **Power BI** en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="65f6c-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span></span> <span data-ttu-id="65f6c-148">Usa un modelo de diseño Model-View-Controller (MVC) para demostrar las prácticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="65f6c-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span></span> <span data-ttu-id="65f6c-149">En esta sección se destacan las partes del ejemplo de código que puede explorar dentro de la solución de aplicación web **PowerBI-embedded**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="65f6c-150">El modelo Model-View-Controller (MVC) separa el modelado de dominio, la presentación y las acciones basadas en la entrada del usuario en tres clases distintas: Model, View y Control.</span><span class="sxs-lookup"><span data-stu-id="65f6c-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="65f6c-151">Para más información sobre MVC, consulte [Learn About ASP.NET](http://www.asp.net/mvc) (Más información sobre ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="65f6c-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="65f6c-152">El ejemplo de código de **Microsoft Power BI Embedded** se divide de la forma siguiente.</span><span class="sxs-lookup"><span data-stu-id="65f6c-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="65f6c-153">Cada sección incluye el nombre de archivo de la solución PowerBI-embedded.sln para que pueda encontrar fácilmente el código en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="65f6c-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span></span>

> [!NOTE]
> <span data-ttu-id="65f6c-154">Esta sección es un resumen del código de ejemplo que muestra cómo se escribe el código.</span><span class="sxs-lookup"><span data-stu-id="65f6c-154">This section is a summary of the sample code that shows how the code was written.</span></span> <span data-ttu-id="65f6c-155">Para ver el ejemplo completo, cargue la solución PowerBI-embedded.sln en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="65f6c-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="65f6c-156">Modelo</span><span class="sxs-lookup"><span data-stu-id="65f6c-156">Model</span></span>

<span data-ttu-id="65f6c-157">El ejemplo incluye las clases **ReportsViewModel** y **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="65f6c-158">**ReportsViewModel.cs**: representa los informes de Power BI.</span><span class="sxs-lookup"><span data-stu-id="65f6c-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="65f6c-159">**ReportViewModel.cs**: representa un informe de Power BI.</span><span class="sxs-lookup"><span data-stu-id="65f6c-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="65f6c-160">Cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="65f6c-160">Connection string</span></span>

<span data-ttu-id="65f6c-161">La cadena de conexión debe tener el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="65f6c-161">The connection string must be in the following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="65f6c-162">No se podrán utilizar correctamente los atributos comunes de servidor y base de datos.</span><span class="sxs-lookup"><span data-stu-id="65f6c-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="65f6c-163">Por ejemplo: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="65f6c-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="65f6c-164">Ver</span><span class="sxs-lookup"><span data-stu-id="65f6c-164">View</span></span>

<span data-ttu-id="65f6c-165">En la **vista** se administra la presentación de los **informes** de Power BI y de un **informe** de Power BI.</span><span class="sxs-lookup"><span data-stu-id="65f6c-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="65f6c-166">**Reports.cshtml**: recorre en iteración **Model.Reports** para crear un **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span></span> <span data-ttu-id="65f6c-167">**ActionLink** se compone de los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="65f6c-167">The **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="65f6c-168">Elemento</span><span class="sxs-lookup"><span data-stu-id="65f6c-168">Part</span></span> | <span data-ttu-id="65f6c-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="65f6c-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="65f6c-170">Título</span><span class="sxs-lookup"><span data-stu-id="65f6c-170">Title</span></span> |<span data-ttu-id="65f6c-171">Nombre del informe.</span><span class="sxs-lookup"><span data-stu-id="65f6c-171">Name of the Report.</span></span> |
| <span data-ttu-id="65f6c-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="65f6c-172">QueryString</span></span> |<span data-ttu-id="65f6c-173">Vínculo al identificador del informe.</span><span class="sxs-lookup"><span data-stu-id="65f6c-173">A link to the Report ID.</span></span> |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

<span data-ttu-id="65f6c-174">Report.cshtml: establece **Model.AccessToken** y la expresión lambda para **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="65f6c-175">Controller</span><span class="sxs-lookup"><span data-stu-id="65f6c-175">Controller</span></span>

<span data-ttu-id="65f6c-176">**DashboardController.cs**: crea una clase PowerBIClient que pasa un **token de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="65f6c-177">Se genera un token JSON Web Token (JWT) a partir de la **clave de firma** para obtener las **credenciales**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span></span> <span data-ttu-id="65f6c-178">Las **credenciales** se usan para crear una instancia de **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span></span> <span data-ttu-id="65f6c-179">Cuando tenga una instancia de **PowerBIClient**, puede llamar a GetReports() y GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="65f6c-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="65f6c-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="65f6c-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="65f6c-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="65f6c-181">ActionResult Reports()</span></span>

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


<span data-ttu-id="65f6c-182">Tarea<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="65f6c-182">Task<ActionResult> Report(string reportId)</span></span>

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="65f6c-183">Integración de un informe en la aplicación</span><span class="sxs-lookup"><span data-stu-id="65f6c-183">Integrate a report into your app</span></span>

<span data-ttu-id="65f6c-184">Cuando tenga un **informe**, puede usar **IFrame** para insertar el **informe** de Power BI.</span><span class="sxs-lookup"><span data-stu-id="65f6c-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span></span> <span data-ttu-id="65f6c-185">Este es un fragmento de código de powerbi.js en el ejemplo de versión preliminar de **Microsoft Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="65f6c-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="65f6c-186">Filtro de informes incrustados en la aplicación</span><span class="sxs-lookup"><span data-stu-id="65f6c-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="65f6c-187">Puede filtrar un informe incrustado mediante una sintaxis de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="65f6c-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="65f6c-188">Para ello, agregue un parámetro de cadena de consulta **$filter** con un operador **eq** a la dirección URL de src de iFrame con el filtro especificado.</span><span class="sxs-lookup"><span data-stu-id="65f6c-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span></span> <span data-ttu-id="65f6c-189">Esta es la sintaxis de consulta de filtro:</span><span class="sxs-lookup"><span data-stu-id="65f6c-189">Here is the filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="65f6c-190">{tableName/fieldName} no puede incluir espacios ni caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="65f6c-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="65f6c-191">{fieldValue} acepta un único valor de categoría.</span><span class="sxs-lookup"><span data-stu-id="65f6c-191">The {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="65f6c-192">Consulte también</span><span class="sxs-lookup"><span data-stu-id="65f6c-192">See also</span></span>

[<span data-ttu-id="65f6c-193">Common Microsoft Power BI Embedded scenarios (Escenarios comunes de Microsoft Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="65f6c-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="65f6c-194">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="65f6c-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
<span data-ttu-id="65f6c-195">[Embed a report in Power BI Embedded](power-bi-embedded-embed-report.md) (Inserción de un informe en Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="65f6c-195">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="65f6c-196">Creación de un nuevo informe a partir de un conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="65f6c-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="65f6c-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="65f6c-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
<span data-ttu-id="65f6c-198">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="65f6c-198">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)</span></span>  
<span data-ttu-id="65f6c-199">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="65f6c-199">More questions?</span></span> [<span data-ttu-id="65f6c-200">Pruebe la comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="65f6c-200">Try the Power BI Community</span></span>](http://community.powerbi.com/)
