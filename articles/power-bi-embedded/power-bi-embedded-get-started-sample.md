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
# <a name="get-started-with-power-bi-embedded-sample"></a>Introducción a un ejemplo de Power BI Embedded

Con **Microsoft Power BI Embedded**, puede integrar informes de Power BI directamente en las aplicaciones web o móviles. En este artículo, le presentaremos toohello **Power BI Embedded** ejemplo de introducción de get.

Antes de que sigamos avanzando, probablemente deseará hello toosave recursos siguientes. Podrá ayudarle al integrar informes de Power BI en la aplicación de ejemplo de Hola y sus propias aplicaciones demasiado.

* [Aplicación web de área de trabajo de ejemplo](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Referencia de API Power BI Embedded](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [SDK de .NET de Power BI Embedded ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponible a través de NuGet)
* [Ejemplo de inserción de informe de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> Antes de que se puede configurar y ejemplo de introducción de ejecución Hola obtener Power BI Embedded, necesita toocreate al menos una **colección de área de trabajo** en su suscripción de Azure. toolearn cómo toocreate una **colección de área de trabajo** Hola Portal de Azure vea [Introducción a Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="configure-hello-sample-app"></a>Configurar la aplicación de ejemplo de Hola

Analicemos configurar la aplicación de ejemplo Visual Studio desarrollo entorno tooaccess Hola componentes necesarios toorun Hola.

1. Descargue y descomprima hello [Power BI Embedded - integrar un informe en una aplicación web](http://go.microsoft.com/fwlink/?LinkId=761493) muestras en GitHub.
2. Abra **PowerBI embedded.sln** en Visual Studio. Puede que necesite hello tooexecute **paquete de actualización** comando hello consola del Administrador de paquetes de NuGET en paquetes de hello tooupdate orden utilizado en esta solución.
3. Compile la solución de Hola.
4. Ejecute hello **ProvisionSample** aplicación de consola. En la aplicación de consola de ejemplo de Hola, aprovisionar un área de trabajo e importar un archivo PBIX.
5. tooprovision un nuevo **área de trabajo**, seleccione la opción 1, **administración de colecciones de**y, a continuación, seleccione la opción 6, **aprovisionar una nueva área de trabajo**
6. tooimport un nuevo **informe**, seleccione la opción 2, **administración de informes**y, a continuación, seleccione la opción 3, **archivo de importación PBIX escritorio en un área de trabajo**.

7. Escriba el nombre de su **colección de área de trabajo** y la **clave de acceso**. Puede obtener estas opciones en hello **Portal de Azure**. toolearn más información acerca de cómo tooget su **clave de acceso**, consulte [teclas de acceso de API de vista de Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) en empezar a trabajar con Microsoft Power BI Embedded.

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. Copie y guarde Hola recién creado **Id. de área de trabajo** toouse más adelante en este artículo. Después de hello **Id. de área de trabajo** está creado, puede encontrarlo hello **Portal de Azure**.

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. el archivo de tooimport un PBIX en su **área de trabajo**, seleccione la opción **6. Importe el archivo de escritorio PBIX en un área de trabajo existente**. Si no tienes un PBIX archivo útil, puede descargar hello [PBIX de ejemplo de análisis de minoristas](http://go.microsoft.com/fwlink/?LinkID=780547).
10. Si se le solicita, escriba un nombre descriptivo para su **Dataset**.

Debería obtener una respuesta similar a la siguiente:

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> Si el archivo PBIX contiene las conexiones de consulta directa, ejecute las cadenas de conexión de opción 7 tooupdate Hola.

En este momento, tiene un informe PBIX de Power BI importado en su **área de trabajo**. Ahora, echemos un vistazo a cómo hello toorun **Power BI Embedded** obtener la aplicación web de ejemplo de introducción.

## <a name="run-hello-sample-web-app"></a>Ejecutar la aplicación web de ejemplo de Hola
ejemplo de aplicación web de Hello es una aplicación de ejemplo que representa los informes que se importan en su **área de trabajo**. Le mostramos cómo tooconfigure Hola ejemplo de aplicación web.

1. Hola **incrustadas PowerBI** solución de Visual Studio, derecho, haga clic en hello **EmbedSample** aplicación web y elija **establecer como proyecto de inicio**.
2. En **web.config**, Hola **EmbedSample** aplicación web, edite hello **appSettings**: **AccessKey**,  **WorkspaceCollection** nombre, y **WorkspaceId**.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Ejecute hello **EmbedSample** aplicación web.

Una vez que ejecute hello **EmbedSample** aplicación web, el panel de navegación izquierdo de hello debe contener una **informes** menú. informe de hello tooview importado, expanda **informes**y haga clic en un informe. Si importó hello [PBIX de ejemplo de análisis de minoristas](http://go.microsoft.com/fwlink/?LinkID=780547), aplicación web de ejemplo de Hola sería similar al siguiente:

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

Tras hacer clic en un informe, Hola **EmbedSample** aplicación web debe tener un aspecto esto:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a>Explorar el código de ejemplo de Hola

Hola **Microsoft Power BI Embedded** ejemplo es una aplicación web de ejemplo que muestra cómo toointegrate **Power BI** informes en la aplicación. Utiliza un Model-View-Controller (MVC) patrón toodemonstrate mejores prácticas de diseño. Esta sección resalta las partes del código de ejemplo de Hola que puede explorar en hello **PowerBI incrustadas** solución de aplicación web. Hello modelo Model-View-Controller (MVC) separa el modelo de Hola de dominio hello, presentación de Hola y acciones de hello según los proporcionados por el usuario en tres clases independientes: modelo, ver y controlar. toolearn más información acerca de MVC, vea [obtener información sobre ASP.NET](http://www.asp.net/mvc).

Hola **Microsoft Power BI Embedded** código de ejemplo está separado como se indica a continuación. Cada sección incluye el nombre de archivo de Hola Hola PowerBI embedded.sln solución para que puedan encontrar fácilmente el código de hello en el ejemplo de Hola.

> [!NOTE]
> Esta sección es un resumen de código de ejemplo de Hola que muestra cómo se escribe código de hello. Hola tooview completo de ejemplo, cargue la solución hello embedded.sln Power BI en Visual Studio.

### <a name="model"></a>Modelo

ejemplo de Hola tiene un **ReportsViewModel** y **ReportViewModel**.

**ReportsViewModel.cs**: representa los informes de Power BI.

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

**ReportViewModel.cs**: representa un informe de Power BI.

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a>Cadena de conexión

cadena de conexión de Hello debe Hola siguiendo el formato:

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

No se podrán utilizar correctamente los atributos comunes de servidor y base de datos. Por ejemplo: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>Ver

Hola **vista** administra la presentación de Hola de Power BI **informes** y Power BI **informe**.

**Reports.cshtml**: recorrer en iteración **Model.Reports** toocreate una **ActionLink**. Hola **ActionLink** se compone de los siguientes:

| Elemento | Descripción |
| --- | --- |
| Título |Nombre del programa Hola a informes. |
| QueryString |Un toohello vínculo ID de informe. |

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

Report.cshtml: Establecer hello **Model.AccessToken**, y Hola expresión Lambda para **PowerBIReportFor**.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Controller

**DashboardController.cs**: crea una clase PowerBIClient que pasa un **token de aplicación**. Se genera un Token de Web de JSON (JWT) de hello **clave de firma de** tooget hello **credenciales**. Hola **credenciales** es toocreate usa una instancia de **PowerBIClient**. Cuando tenga una instancia de **PowerBIClient**, puede llamar a GetReports() y GetReportsAsync().

CreatePowerBIClient()

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

ActionResult Reports()

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


Tarea<ActionResult> Report(string reportId)

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

### <a name="integrate-a-report-into-your-app"></a>Integración de un informe en la aplicación

Una vez que tenga un **informe**, utiliza un **IFrame** tooembed Hola Power BI **informe**. Este es un fragmento de código de powerbi.js Hola **Microsoft Power BI Embedded** ejemplo.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>Filtro de informes incrustados en la aplicación

Puede filtrar un informe incrustado mediante una sintaxis de dirección URL. toodo, agregará un **$filter** consultar el parámetro de cadena con un **eq** operador tooyour iFrame src url con filtro de hello especificado. Esta es la sintaxis de consulta de filtro de hello:

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName} no puede incluir espacios ni caracteres especiales. Hola {fieldValue} acepta un único valor de categoría.  

## <a name="see-also"></a>Otras referencias

[Common Microsoft Power BI Embedded scenarios (Escenarios comunes de Microsoft Power BI Embedded)](power-bi-embedded-scenarios.md)  
[Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Embed a report in Power BI Embedded](power-bi-embedded-embed-report.md) (Inserción de un informe en Power BI Embedded)  
[Creación de un nuevo informe a partir de un conjunto de datos](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)  
¿Tiene más preguntas? [Intente Hola Comunidad de Power BI](http://community.powerbi.com/)
