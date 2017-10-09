---
title: informes de aaaSave en Azure Power BI Embedded | Documentos de Microsoft
description: "Obtenga información acerca de cómo incrustan informes toosave dentro de Power BI. Esto requiere los permisos adecuados en orden toowork correctamente."
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
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a>Guardado de informes en Power BI Embedded

Obtenga información acerca de cómo incrustan informes toosave dentro de Power BI. Esto requiere los permisos adecuados en orden toowork correctamente.

En Power BI Embedded, es posible editar los informes existentes y guardarlos. También puede crear un nuevo informe y guardar como un nuevo toocreate de informe uno.

En orden toosave un informe primero debe toocreate un token para el informe específico de hello con ámbitos derecho hello:

* se requiere tooenable guardar Report.ReadWrite ámbito
* tooenable Guardar como, ámbitos Report.Read y Workspace.Report.Copy son necesarios
* tooenable son Guardar y guardar como, Report.ReadWrite y Workspace.Report.Copy requierd

Respectivamente en hello tooenable de orden derecho guardar o guardar como botones en el menú archivo necesita tooprovide Hola derecho permiso en la configuración de insertar hello cuando se insertar Hola informe:

* models.Permissions.ReadWrite
* models.Permissions.Copy
* models.Permissions.All

> [!NOTE]
> El token de acceso también debe ámbitos adecuados de Hola. Para más información, consulte [Scopes](power-bi-embedded-app-token-flow.md#scopes) (Ámbitos).

## <a name="embed-report-in-edit-mode"></a>Inserción de informes en modo de edición

Vamos a decir que desee tooEmbed un informe en modo de edición dentro de la aplicación, toodo así que puede pasar propiedades de derecho de hello en la configuración de insertar y llamar a powerbi.embed(). Necesitará permisos de toosupply y un viewMode Hola de orden toosee guardar y guardar como botones en el modo de edición. Para más información, consulte [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details) (Detalles de configuración de la inserción).

Por ejemplo, en JavaScript:

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

Ahora, se insertará un informe en la aplicación en modo de edición.

## <a name="save-report"></a>Guardar informe

Después de que el modo con hello token derechos y permisos de edición de informes de hello Embbeding en puede guardar informe de Hola de menú archivo de Hola o de javascript:

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>Guardar como

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
> Solo después de *save as* se crea un informe nuevo. Después de guardar hello, lienzo Hola se sigue mostrando informe anterior hello en edición no hello y modo de informe nuevo. Necesitará tooembed Hola nuevo informe que se creó. Esto requiere un nuevo token de acceso, ya que se crean por informe.

A continuación, se necesita tooload Hola nuevo informe después de un *Guardar como*. Esto es similar tooembedding cualquier informe.

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

## <a name="see-also"></a>Otras referencias

[Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)](power-bi-embedded-get-started-sample.md)  
[Embed a report in Power BI Embedded](power-bi-embedded-embed-report.md) (Inserción de un informe en Power BI Embedded)  
[Creación de un nuevo informe a partir de un conjunto de datos](power-bi-embedded-create-report-from-dataset.md)  
[Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)  
¿Tiene más preguntas? [Intente Hola Comunidad de Power BI](http://community.powerbi.com/)

