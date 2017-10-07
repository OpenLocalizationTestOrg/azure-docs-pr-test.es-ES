---
title: un informe en Azure Power BI Embedded aaaEmbed | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooembed un informe que se encuentra en Power BI Embedded en la aplicación."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a>Inserción de un informe en Power BI Embedded

Obtenga información acerca de cómo tooembed un informe que se encuentra en Power BI Embedded en la aplicación.

Veremos cómo tooactually incrustar un informe en la aplicación. Aquí se asume que ya tiene un informe que existe en un área de trabajo de su colección de áreas de trabajo. Si aún no ha dado ese paso, consulte [Introducción a Microsoft Power BI Embedded](power-bi-embedded-get-started.md).

Puede usar .NET hello (C#) o el SDK de Node.js, junto con JavaScript, tooeasily Compile su aplicación con Power BI Embedded. 

## <a name="using-hello-access-keys-toouse-rest-apis"></a>Uso de toouse de claves de acceso de hello las API de REST

Hola de orden toocall API de REST, puede pasar clave de acceso de Hola que puede obtener de hello portal de Azure para una colección de área de trabajo determinado. Para más información, consulte [Introducción a Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="get-a-report-id"></a>Obtención de un identificador de informe

Todos los tokens de acceso se basan en algún informe. Necesitará hello tooget determinado Id. de informe para los informes de Hola que desea tooembed. Esto puede hacerse en función de las llamadas toohello [obtener informes](https://msdn.microsoft.com/library/azure/mt711510.aspx) API de REST. Esto devolverá informe Hola hello y el Id. de incrustan la dirección url. Esto puede hacerse mediante Hola Power BI .NET SDK o llamar directamente a API de REST de Hola.

### <a name="using-hello-power-bi-net-sdk"></a>Uso de hello Power BI .NET SDK

Cuando se usa Hola .NET SDK, deberá toocreate una credencial de token que se basa en la clave de acceso de hello que obtendrá de hello portal de Azure. Esto requiere que instale hello [paquete API NuGet de Power BI](https://www.nuget.org/profiles/powerbi).

**Instalación de un paquete NuGet**

```
Install-Package Microsoft.PowerBI.Api
```

**Código de C#**

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a>Hola de llamar a API de REST directamente

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a>Creación de un token de acceso

Power BI Embedded usa tokens de inserción, que son JSON Web Tokens con forma HMAC. Hola tokens se firman con la clave de acceso de hello en su colección Azure Power BI Embedded de área de trabajo. Inserte tokens, de forma predeterminada, se usa tooprovide leer solo acceso tooa informe tooembed en una aplicación. Los tokens de inserción se emiten para un informe concreto y se deben asociar a una dirección URL de inserción.

Tokens de acceso deben crearse en el servidor de hello como teclas de acceso de hello son tokens de hello toosign/encrypt usado. Para obtener información acerca de cómo toocreate un token de acceso, consulte [autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md). También puede revisar hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) método. Este es un ejemplo de este aspecto usando Hola .NET SDK para Power BI.

Va a usar el Id. de informe de Hola que recuperó anteriormente. Una vez Hola incrustar símbolo (token) se crea, a continuación, usará Hola acceso toogenerate clave Hola símbolo (token) que se puede utilizar desde la perspectiva de javascript de Hola. Hola *PowerBIToken clase* requiere que instale hello [Power BI Core NuGut paquete](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Instalación de un paquete NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Código de C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a>Adición de tokens de tooembed de ámbitos de permiso

Cuando se usa tokens de insertar, puede que desee toorestrict uso de recursos de hello a que ofrecen acceso. Por este motivo, puede generar un token con permisos con ámbito. Para más información, consulte [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ámbitos)

## <a name="embed-using-javascript"></a>Inserción mediante JavaScript

Una vez que el token de acceso de Hola y el identificador del informe de hello, se puede incrustar informe de hello con JavaScript. Esto requiere que instale Hola nuget [paquete de Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Hola embedUrl solo será https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Puede usar hello [incrustar el informe de ejemplo JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funcionalidad. También proporciona ejemplos de código para las operaciones diferentes de Hola que están disponibles.

**Instalación de un paquete NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Código JavaScript**

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-hello-size-of-embedded-elements"></a>Establecer tamaño de Hola de los elementos incrustados

informe de Hola se incrustarán automáticamente en función de tamaño de Hola de su contenedor. tamaño de toooverride Hola predeterminado de hello incrusta basta con agregar un estilos de atributo o en línea de la clase CSS de ancho y alto.

## <a name="see-also"></a>Otras referencias

[Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)](power-bi-embedded-get-started-sample.md)  
[Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)  
[Paquete Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
[Paquete NuGet Power BI API](https://www.nuget.org/profiles/powerbi)
[Paquete NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Repositorio GIT PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Repositorio GIT PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
¿Tiene más preguntas? [Intente Hola Comunidad de Power BI](http://community.powerbi.com/)
