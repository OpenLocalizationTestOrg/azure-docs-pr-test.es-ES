---
title: aaaCreate un nuevo informe a partir de un conjunto de datos en Azure Power BI Embedded | Documentos de Microsoft
description: "Los informes de Power BI Embedded ahora se puede crear a partir de un conjunto de datos de su propia aplicación."
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Creación de un nuevo informe a partir de un conjunto de datos en Power BI Embedded

Los informes de Power BI Embedded ahora se puede crear a partir de un conjunto de datos de su propia aplicación. 

Hello método de autenticación es similar incrustar toothat del informe. Se basa en tokens de acceso que están el conjunto de datos de tooa específico. Los tokens que se usan para PowerBI.com los emite Azure Active Directory (AAD), mientras que los de Power BI Embedded los emite su propio servicio.

Cuando un informe incrustado, creación Hola son tokens emitidos para un conjunto de datos específico. Símbolos (tokens) debe asociarse con hello incrustar la dirección URL en hello mismo tooensure elemento tiene un token único. En Ordenar toocreate un informe incrustado, *Dataset.Read y Workspace.Report.Create* ámbitos deben indicarse en el token de acceso de Hola.

## <a name="create-access-token-needed-toocreate-new-report"></a>Crear nuevo informe de access token toocreate necesarios

Power BI Embedded usa tokens de inserción, que son JSON Web Tokens con forma HMAC. Hola tokens se firman con la clave de acceso de hello en su colección Azure Power BI Embedded de área de trabajo. Inserte tokens, de forma predeterminada, se usa tooprovide leer solo acceso tooa informe tooembed en una aplicación. Los tokens de inserción se emiten para un informe concreto y se deben asociar a una dirección URL de inserción.

Tokens de acceso deben crearse en el servidor de hello como teclas de acceso de hello son tokens de hello toosign/encrypt usado. Para obtener información acerca de cómo toocreate un token de acceso, consulte [autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md). También puede revisar hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) método. Este es un ejemplo de este aspecto usando Hola .NET SDK para Power BI.

En este ejemplo, tenemos nuestro Id. de conjunto de datos que se desea obtener toocreat Hola nuevo informe en. También es necesario ámbitos de hello tooadd para *Dataset.Read y Workspace.Report.Create*.

Hola *PowerBIToken clase* requiere que instale hello [Power BI Core NuGut paquete](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Instalación de un paquete NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Código de C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>Creación de un informe en blanco nuevo

En orden toocreate un nuevo informe, crear Hola se debe proporcionar la configuración. Debe incluir token de acceso de hello, embedURL de Hola y Hola datasetID que queremos toocreate informe Hola. Esto requiere que instale Hola nuget [paquete de Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Hola embedUrl solo será https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Puede usar hello [incrustar el informe de ejemplo JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funcionalidad. También proporciona ejemplos de código para las operaciones diferentes de Hola que están disponibles.

**Instalación de un paquete NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Código JavaScript**

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

Al llamar a *powerbi.createReport()* hará que un lienzo en blanco en modo de edición aparecen en hello *div* elemento.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Guardado de informes nuevos

informe Hello no se creará realmente hasta que se llama a hello **Guardar como** operación. lo que se puede hacer desde el menú archivo o desde JavaScript.

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> Los informes nuevo solo se pueden crear después de llamar a **save as**. Después de guardar, lienzo Hola seguirá mostrando el conjunto de datos de hello en informe de no hello y el modo de edición. Necesitará el nuevo informe de tooreload hello como lo haría con cualquier otro informe.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>Carga Hola nuevo informe

En orden toointeract con nuevo informe de hello debe tooembed en hello llamada Hola igual aplicación hello incrusta un normal de informe, es decir, un nuevo token debe emitirse específicamente para el nuevo informe de hello y, a continuación, insertar el método.

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>Automatizar guardar y cargar de un nuevo informe utilizando Hola "guarda" evento

Proceso de pedido tooautomate Hola de "Guardar como..." y, a continuación, cargar nuevo informe de hello hacer que el uso de Hola "Guardar" evento. Este evento se desencadena cuando se completa Hola operación de guardado y devuelve un objeto Json que contiene identificador nuevo informe, Hola que, el nombre del informe, el identificador informe anterior, que hello (si hay alguna) y si la operación de hello era saveAs o en Guardar.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

proceso de hello tooAutomate puede escuchar en el evento Hola "guarda", tomar identificador nuevo informe, Hola que, crear nuevo token de Hola e incrustar informes nuevos de hello con él.

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a>Otras referencias

[Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)](power-bi-embedded-get-started-sample.md)  
[Almacenamiento de informes](power-bi-embedded-save-reports.md)  
[Embed a report in Power BI Embedded](power-bi-embedded-embed-report.md) (Inserción de un informe en Power BI Embedded)  
[Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)  
[Paquete NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Paquete Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
¿Tiene más preguntas? [Intente Hola Comunidad de Power BI](http://community.powerbi.com/)
