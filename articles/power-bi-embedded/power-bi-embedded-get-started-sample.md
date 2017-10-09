---
title: trabajar con un ejemplo de aaaGet
description: "Power BI Embedded, use tooadd SDK interactivo de Power BI informa a la aplicación de business intelligence"
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
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="3afd9-103">Introducción a un ejemplo de Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3afd9-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="3afd9-104">Con **Microsoft Power BI Embedded**, puede integrar informes de Power BI directamente en las aplicaciones web o móviles.</span><span class="sxs-lookup"><span data-stu-id="3afd9-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="3afd9-105">En este artículo, le presentaremos toohello **Power BI Embedded** ejemplo de introducción de get.</span><span class="sxs-lookup"><span data-stu-id="3afd9-105">In this article, we'll introduce you toohello **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="3afd9-106">Antes de que sigamos avanzando, probablemente deseará hello toosave recursos siguientes.</span><span class="sxs-lookup"><span data-stu-id="3afd9-106">Before we go any further, you'll probably want toosave hello following resources.</span></span> <span data-ttu-id="3afd9-107">Podrá ayudarle al integrar informes de Power BI en la aplicación de ejemplo de Hola y sus propias aplicaciones demasiado.</span><span class="sxs-lookup"><span data-stu-id="3afd9-107">They'll help you when integrating Power BI reports into hello sample app and your own apps too.</span></span>

* [<span data-ttu-id="3afd9-108">Aplicación web de área de trabajo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="3afd9-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="3afd9-109">Referencia de API Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3afd9-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="3afd9-110">[SDK de .NET de Power BI Embedded ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponible a través de NuGet)</span><span class="sxs-lookup"><span data-stu-id="3afd9-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="3afd9-111">Ejemplo de inserción de informe de JavaScript</span><span class="sxs-lookup"><span data-stu-id="3afd9-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="3afd9-112">Antes de que se puede configurar y ejemplo de introducción de ejecución Hola obtener Power BI Embedded, necesita toocreate al menos una **colección de área de trabajo** en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3afd9-112">Before you can configure and run hello Power BI Embedded get started sample, you need toocreate at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="3afd9-113">toolearn cómo toocreate una **colección de área de trabajo** Hola Portal de Azure vea [Introducción a Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3afd9-113">toolearn how toocreate a **Workspace Collection** in hello Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-hello-sample-app"></a><span data-ttu-id="3afd9-114">Configurar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="3afd9-114">Configure hello sample app</span></span>

<span data-ttu-id="3afd9-115">Analicemos configurar la aplicación de ejemplo Visual Studio desarrollo entorno tooaccess Hola componentes necesarios toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="3afd9-115">Let's walk through setting up your Visual Studio development environment tooaccess hello  components needed toorun hello sample app.</span></span>

1. <span data-ttu-id="3afd9-116">Descargue y descomprima hello [Power BI Embedded - integrar un informe en una aplicación web](http://go.microsoft.com/fwlink/?LinkId=761493) muestras en GitHub.</span><span class="sxs-lookup"><span data-stu-id="3afd9-116">Download and unzip hello [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="3afd9-117">Abra **PowerBI embedded.sln** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3afd9-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="3afd9-118">Puede que necesite hello tooexecute **paquete de actualización** comando hello consola del Administrador de paquetes de NuGET en paquetes de hello tooupdate orden utilizado en esta solución.</span><span class="sxs-lookup"><span data-stu-id="3afd9-118">You may need tooexecute hello **Update-Package** command in hello NuGET Package Manager Console in order tooupdate hello packages used in this solution.</span></span>
3. <span data-ttu-id="3afd9-119">Compile la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="3afd9-119">Build hello solution.</span></span>
4. <span data-ttu-id="3afd9-120">Ejecute hello **ProvisionSample** aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="3afd9-120">Run hello **ProvisionSample** console app.</span></span> <span data-ttu-id="3afd9-121">En la aplicación de consola de ejemplo de Hola, aprovisionar un área de trabajo e importar un archivo PBIX.</span><span class="sxs-lookup"><span data-stu-id="3afd9-121">In hello sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="3afd9-122">tooprovision un nuevo **área de trabajo**, seleccione la opción 1, **administración de colecciones de**y, a continuación, seleccione la opción 6, **aprovisionar una nueva área de trabajo**</span><span class="sxs-lookup"><span data-stu-id="3afd9-122">tooprovision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="3afd9-123">tooimport un nuevo **informe**, seleccione la opción 2, **administración de informes**y, a continuación, seleccione la opción 3, **archivo de importación PBIX escritorio en un área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-123">tooimport a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="3afd9-124">Escriba el nombre de su **colección de área de trabajo** y la **clave de acceso**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="3afd9-125">Puede obtener estas opciones en hello **Portal de Azure**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-125">You can get these in hello **Azure Portal**.</span></span> <span data-ttu-id="3afd9-126">toolearn más información acerca de cómo tooget su **clave de acceso**, consulte [teclas de acceso de API de vista de Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) en empezar a trabajar con Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="3afd9-126">toolearn more about how tooget your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="3afd9-127">Copie y guarde Hola recién creado **Id. de área de trabajo** toouse más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="3afd9-127">Copy and save hello newly created **Workspace ID** toouse later in this article.</span></span> <span data-ttu-id="3afd9-128">Después de hello **Id. de área de trabajo** está creado, puede encontrarlo hello **Portal de Azure**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-128">After hello **Workspace ID** is created, you can find it hello **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="3afd9-129">el archivo de tooimport un PBIX en su **área de trabajo**, seleccione la opción **6. Importe el archivo de escritorio PBIX en un área de trabajo existente**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-129">tooimport a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="3afd9-130">Si no tienes un PBIX archivo útil, puede descargar hello [PBIX de ejemplo de análisis de minoristas](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="3afd9-130">If you don't have a PBIX file handy, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="3afd9-131">Si se le solicita, escriba un nombre descriptivo para su **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="3afd9-132">Debería obtener una respuesta similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="3afd9-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="3afd9-133">Si el archivo PBIX contiene las conexiones de consulta directa, ejecute las cadenas de conexión de opción 7 tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="3afd9-133">If your PBIX file contains any direct query connections, run option 7 tooupdate hello connection strings.</span></span>

<span data-ttu-id="3afd9-134">En este momento, tiene un informe PBIX de Power BI importado en su **área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="3afd9-135">Ahora, echemos un vistazo a cómo hello toorun **Power BI Embedded** obtener la aplicación web de ejemplo de introducción.</span><span class="sxs-lookup"><span data-stu-id="3afd9-135">Now, let's look at how toorun hello **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-hello-sample-web-app"></a><span data-ttu-id="3afd9-136">Ejecutar la aplicación web de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="3afd9-136">Run hello sample web app</span></span>
<span data-ttu-id="3afd9-137">ejemplo de aplicación web de Hello es una aplicación de ejemplo que representa los informes que se importan en su **área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-137">hello web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="3afd9-138">Le mostramos cómo tooconfigure Hola ejemplo de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3afd9-138">Here's how tooconfigure hello web app sample.</span></span>

1. <span data-ttu-id="3afd9-139">Hola **incrustadas PowerBI** solución de Visual Studio, derecho, haga clic en hello **EmbedSample** aplicación web y elija **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-139">In hello **PowerBI-embedded** Visual Studio solution, right click hello **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="3afd9-140">En **web.config**, Hola **EmbedSample** aplicación web, edite hello **appSettings**: **AccessKey**,  **WorkspaceCollection** nombre, y **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-140">In **web.config**, in hello **EmbedSample** web application, edit hello **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="3afd9-141">Ejecute hello **EmbedSample** aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3afd9-141">Run hello **EmbedSample** web application.</span></span>

<span data-ttu-id="3afd9-142">Una vez que ejecute hello **EmbedSample** aplicación web, el panel de navegación izquierdo de hello debe contener una **informes** menú.</span><span class="sxs-lookup"><span data-stu-id="3afd9-142">Once you run hello **EmbedSample** web application, hello left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="3afd9-143">informe de hello tooview importado, expanda **informes**y haga clic en un informe.</span><span class="sxs-lookup"><span data-stu-id="3afd9-143">tooview hello report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="3afd9-144">Si importó hello [PBIX de ejemplo de análisis de minoristas](http://go.microsoft.com/fwlink/?LinkID=780547), aplicación web de ejemplo de Hola sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="3afd9-144">If you imported hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="3afd9-145">Tras hacer clic en un informe, Hola **EmbedSample** aplicación web debe tener un aspecto esto:</span><span class="sxs-lookup"><span data-stu-id="3afd9-145">After you click a report, hello **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a><span data-ttu-id="3afd9-146">Explorar el código de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="3afd9-146">Explore hello sample code</span></span>

<span data-ttu-id="3afd9-147">Hola **Microsoft Power BI Embedded** ejemplo es una aplicación web de ejemplo que muestra cómo toointegrate **Power BI** informes en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3afd9-147">hello **Microsoft Power BI Embedded** sample is an example web app that shows you how toointegrate **Power BI** reports into your app.</span></span> <span data-ttu-id="3afd9-148">Utiliza un Model-View-Controller (MVC) patrón toodemonstrate mejores prácticas de diseño.</span><span class="sxs-lookup"><span data-stu-id="3afd9-148">It uses a Model-View-Controller (MVC) design pattern toodemonstrate best practices.</span></span> <span data-ttu-id="3afd9-149">Esta sección resalta las partes del código de ejemplo de Hola que puede explorar en hello **PowerBI incrustadas** solución de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="3afd9-149">This section highlights parts of hello sample code that you can explore within hello **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="3afd9-150">Hello modelo Model-View-Controller (MVC) separa el modelo de Hola de dominio hello, presentación de Hola y acciones de hello según los proporcionados por el usuario en tres clases independientes: modelo, ver y controlar.</span><span class="sxs-lookup"><span data-stu-id="3afd9-150">hello Model-View-Controller (MVC) pattern separates hello modeling of hello domain, hello presentation, and hello actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="3afd9-151">toolearn más información acerca de MVC, vea [obtener información sobre ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="3afd9-151">toolearn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="3afd9-152">Hola **Microsoft Power BI Embedded** código de ejemplo está separado como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="3afd9-152">hello **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="3afd9-153">Cada sección incluye el nombre de archivo de Hola Hola PowerBI embedded.sln solución para que puedan encontrar fácilmente el código de hello en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3afd9-153">Each section includes hello file name in hello PowerBI-embedded.sln solution so that you can easily find hello code in hello sample.</span></span>

> [!NOTE]
> <span data-ttu-id="3afd9-154">Esta sección es un resumen de código de ejemplo de Hola que muestra cómo se escribe código de hello.</span><span class="sxs-lookup"><span data-stu-id="3afd9-154">This section is a summary of hello sample code that shows how hello code was written.</span></span> <span data-ttu-id="3afd9-155">Hola tooview completo de ejemplo, cargue la solución hello embedded.sln Power BI en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3afd9-155">tooview hello complete sample, please load hello PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="3afd9-156">Modelo</span><span class="sxs-lookup"><span data-stu-id="3afd9-156">Model</span></span>

<span data-ttu-id="3afd9-157">ejemplo de Hola tiene un **ReportsViewModel** y **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-157">hello sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="3afd9-158">**ReportsViewModel.cs**: representa los informes de Power BI.</span><span class="sxs-lookup"><span data-stu-id="3afd9-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="3afd9-159">**ReportViewModel.cs**: representa un informe de Power BI.</span><span class="sxs-lookup"><span data-stu-id="3afd9-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="3afd9-160">Cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="3afd9-160">Connection string</span></span>

<span data-ttu-id="3afd9-161">cadena de conexión de Hello debe Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="3afd9-161">hello connection string must be in hello following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="3afd9-162">No se podrán utilizar correctamente los atributos comunes de servidor y base de datos.</span><span class="sxs-lookup"><span data-stu-id="3afd9-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="3afd9-163">Por ejemplo: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="3afd9-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="3afd9-164">Ver</span><span class="sxs-lookup"><span data-stu-id="3afd9-164">View</span></span>

<span data-ttu-id="3afd9-165">Hola **vista** administra la presentación de Hola de Power BI **informes** y Power BI **informe**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-165">hello **View** manages hello display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="3afd9-166">**Reports.cshtml**: recorrer en iteración **Model.Reports** toocreate una **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-166">**Reports.cshtml**: Iterate over **Model.Reports** toocreate an **ActionLink**.</span></span> <span data-ttu-id="3afd9-167">Hola **ActionLink** se compone de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="3afd9-167">hello **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="3afd9-168">Elemento</span><span class="sxs-lookup"><span data-stu-id="3afd9-168">Part</span></span> | <span data-ttu-id="3afd9-169">Descripción</span><span class="sxs-lookup"><span data-stu-id="3afd9-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3afd9-170">Título</span><span class="sxs-lookup"><span data-stu-id="3afd9-170">Title</span></span> |<span data-ttu-id="3afd9-171">Nombre del programa Hola a informes.</span><span class="sxs-lookup"><span data-stu-id="3afd9-171">Name of hello Report.</span></span> |
| <span data-ttu-id="3afd9-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="3afd9-172">QueryString</span></span> |<span data-ttu-id="3afd9-173">Un toohello vínculo ID de informe.</span><span class="sxs-lookup"><span data-stu-id="3afd9-173">A link toohello Report ID.</span></span> |

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

<span data-ttu-id="3afd9-174">Report.cshtml: Establecer hello **Model.AccessToken**, y Hola expresión Lambda para **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-174">Report.cshtml: Set hello **Model.AccessToken**, and hello Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="3afd9-175">Controller</span><span class="sxs-lookup"><span data-stu-id="3afd9-175">Controller</span></span>

<span data-ttu-id="3afd9-176">**DashboardController.cs**: crea una clase PowerBIClient que pasa un **token de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="3afd9-177">Se genera un Token de Web de JSON (JWT) de hello **clave de firma de** tooget hello **credenciales**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-177">A JSON Web Token (JWT) is generated from hello **Signing Key** tooget hello **Credentials**.</span></span> <span data-ttu-id="3afd9-178">Hola **credenciales** es toocreate usa una instancia de **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-178">hello **Credentials** are used toocreate an instance of **PowerBIClient**.</span></span> <span data-ttu-id="3afd9-179">Cuando tenga una instancia de **PowerBIClient**, puede llamar a GetReports() y GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="3afd9-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="3afd9-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="3afd9-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="3afd9-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="3afd9-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="3afd9-182">Tarea<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="3afd9-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="3afd9-183">Integración de un informe en la aplicación</span><span class="sxs-lookup"><span data-stu-id="3afd9-183">Integrate a report into your app</span></span>

<span data-ttu-id="3afd9-184">Una vez que tenga un **informe**, utiliza un **IFrame** tooembed Hola Power BI **informe**.</span><span class="sxs-lookup"><span data-stu-id="3afd9-184">Once you have a **Report**, you use an **IFrame** tooembed hello Power BI **Report**.</span></span> <span data-ttu-id="3afd9-185">Este es un fragmento de código de powerbi.js Hola **Microsoft Power BI Embedded** ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3afd9-185">Here is a code snippet from  powerbi.js in hello **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="3afd9-186">Filtro de informes incrustados en la aplicación</span><span class="sxs-lookup"><span data-stu-id="3afd9-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="3afd9-187">Puede filtrar un informe incrustado mediante una sintaxis de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="3afd9-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="3afd9-188">toodo, agregará un **$filter** consultar el parámetro de cadena con un **eq** operador tooyour iFrame src url con filtro de hello especificado.</span><span class="sxs-lookup"><span data-stu-id="3afd9-188">toodo this, you add a **$filter** query string parameter with an **eq** operator tooyour iFrame src url with hello filter specified.</span></span> <span data-ttu-id="3afd9-189">Esta es la sintaxis de consulta de filtro de hello:</span><span class="sxs-lookup"><span data-stu-id="3afd9-189">Here is hello filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="3afd9-190">{tableName/fieldName} no puede incluir espacios ni caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="3afd9-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="3afd9-191">Hola {fieldValue} acepta un único valor de categoría.</span><span class="sxs-lookup"><span data-stu-id="3afd9-191">hello {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="3afd9-192">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3afd9-192">See also</span></span>

[<span data-ttu-id="3afd9-193">Common Microsoft Power BI Embedded scenarios (Escenarios comunes de Microsoft Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="3afd9-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="3afd9-194">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3afd9-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
<span data-ttu-id="3afd9-195">[Embed a report in Power BI Embedded](power-bi-embedded-embed-report.md) (Inserción de un informe en Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="3afd9-195">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="3afd9-196">Creación de un nuevo informe a partir de un conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="3afd9-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="3afd9-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3afd9-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
<span data-ttu-id="3afd9-198">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="3afd9-198">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)</span></span>  
<span data-ttu-id="3afd9-199">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="3afd9-199">More questions?</span></span> [<span data-ttu-id="3afd9-200">Intente Hola Comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="3afd9-200">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
