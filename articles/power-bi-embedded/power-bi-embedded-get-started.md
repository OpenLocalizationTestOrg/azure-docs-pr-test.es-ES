---
title: aaaGet a trabajar con Microsoft Power BI Embedded
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
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Introducción a Microsoft Power BI Embedded

**Power BI Embedded** es un servicio de Azure ese tooadd de los desarrolladores de aplicaciones permite informes interactivos Power BI en sus propias aplicaciones. **Power BI Embedded** funciona con aplicaciones existentes sin necesidad de cambiar el diseño o cambiar los usuarios de manera Hola iniciar sesión.

Recursos para **Microsoft Power BI Embedded** se aprovisionan mediante hello [API de Azure ARM](https://msdn.microsoft.com/library/mt712306.aspx). En este caso, es el recurso Hola se aprovisiona un **colección de área de trabajo de Power BI**.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>Creación de una colección de áreas de trabajo

A **colección de área de trabajo** es el recurso de Azure de nivel superior de Hola y un contenedor para el contenido de Hola que se incrustarán en la aplicación. Las **colecciones de áreas de trabajo** se pueden crear de dos maneras:

* Manualmente mediante Hola Portal de Azure
* Mediante programación con hello las API Manager(ARM) de recursos de Azure

Analicemos Hola pasos toobuild una **colección de área de trabajo** utilizando Hola Portal de Azure.

1. Abra el **Portal de Azure**, [http://portal.azure.com](http://portal.azure.com), e inicie sesión.
2. Haga clic en **+ nuevo** en el panel superior de Hola.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. En **Datos y análisis**, haga clic en **Power BI Embedded**.
4. En hello **hoja de la colección de área de trabajo**, escriba información de hello necesario. En **Precios**, consulte los [precios de Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. Haga clic en **Crear**.

Hola **colección de área de trabajo** tardará tooprovision unos instantes. Cuando haya completado, se le dirigirá toohello **hoja de la colección de área de trabajo**.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

Hola **hoja de creación** contiene información de Hola que necesita toocall Hola API creen áreas de trabajo y que implemente contenido toothem.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Visualización de las claves de acceso de API de Power BI

Uno de hello más importante fragmentos de información necesaria toocall Hola API de REST de Power BI son hello **teclas de acceso**. Se trata de hello toogenerate usado **tokens de aplicación** que son utilizado tooauthenticate las solicitudes de API. tooview su **teclas de acceso**, haga clic en **teclas de acceso** en hello **hoja de configuración**. Para más información sobre los **tokens de aplicación**, consulte [Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md).

   ![](media/power-bi-embedded-get-started/access-keys.png)

Verá que tiene dos claves.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

Copie estas claves y almacénelas de forma segura en la aplicación. Es muy importante tratar estas claves como lo haría con una contraseña, ya que le proporcionan acceso tooall Hola contenido en su **colección de área de trabajo**.

Aunque se muestran dos claves, solo se necesita una cada vez. segunda clave de Hola se proporciona de manera que puede regenerar periódicamente las claves sin interrumpir el servicio de acceso toohello.

Ahora que tiene una instancia de Power BI para la aplicación y las **claves de acceso**, puede importar un informe en la propia aplicación. Antes de aprender a cómo tooimport un informe, la siguiente sección de hello describe tooembed creación de conjuntos de datos e informes de Power BI en una aplicación.

## <a name="working-with-workspaces"></a>Trabajo con áreas de trabajo

Después de haber creado la colección de área de trabajo, deberá toocreate un área de trabajo que hospedará los informes y conjuntos de datos. toocreate un área de trabajo, deberá hello toouse [API de REST de área de trabajo de Post](https://msdn.microsoft.com/library/azure/mt711503.aspx).

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a>Crear tooembed de conjuntos de datos e informes de Power BI en una aplicación con Power BI Desktop

Ahora que ha creado una instancia de Power BI para su aplicación y tiene **teclas de acceso**, necesitará los conjuntos de datos de toocreate Hola Power BI e informes que desea tooembed. Los conjuntos de datos y los informes se pueden crear con **Power BI Desktop**. Puede descargar [Power BI Desktop gratis](https://go.microsoft.com/fwlink/?LinkId=521662). O bien, tooquickly empezar a trabajar, puede descargar hello [PBIX de ejemplo de análisis de minoristas](http://go.microsoft.com/fwlink/?LinkID=780547).

> [!NOTE]
> más información acerca de cómo toolearn toouse **Power BI Desktop**, consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).

Con **Power BI Desktop**, conectar tooyour origen de datos mediante la importación de una copia de datos de hello en **Power BI Desktop** o conectar directamente toohello de datos de origen mediante **DirectQuery**.

Estas son Hola diferencias entre el uso de **importación** y **DirectQuery**.

| Importación | DirectQuery |
| --- | --- |
| Las tablas, las columnas y los *datos* se importan o se copian en **Power BI Desktop**. Cuando se trabaja con visualizaciones, **Power BI Desktop** consulta una copia de datos de Hola. toosee los cambios de datos subyacente toohello se produjo, debe actualizar o importar un completo actual conjunto de datos nuevo. |En *Power BI Desktop* , solo se importan o copian **tablas y columnas**. Cuando se trabaja con visualizaciones, **Power BI Desktop** consultas Hola el origen de datos subyacente, lo que significa que siempre está viendo los datos actuales. |

Para obtener más información sobre el origen de datos de conexión tooa, consulte [Conectar origen de datos de tooa](power-bi-embedded-connect-datasource.md).

Cuando guarde el trabajo en **Power BI Desktop**, se creará un archivo PBIX. Este archivo contiene el informe. Además, si importa Hola de datos contiene PBIX Hola conjunto de datos completo, o si utiliza **DirectQuery**, hello PBIX contiene solo un esquema de conjunto de datos. Implementar mediante programación hello PBIX en el área de trabajo con hello [API de importación de Power BI](https://msdn.microsoft.com/library/mt711504.aspx).

> [!NOTE]
> **Power BI Embedded** tiene adicionales API toochange Hola servidor y base de datos que el conjunto de datos está señalando tooand conjunto una credencial de cuenta de servicio que Hola conjunto de datos usará la base de datos de tooconnect tooyour. Consulte [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) y [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx) (Revisión de origen de datos de puerta de enlace).

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>Creación de conjuntos de datos e informes de Power BI con las API

### <a name="datsets"></a>Conjuntos de datos

Puede crear conjuntos de datos en Power BI Embedded mediante Hola API de REST. Luego, puede insertar datos en el conjunto de datos. Esto le permite toowork con datos sin necesidad de Hola de Power BI Desktop. Para más información, consulte [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Publicación de conjuntos de datos).

### <a name="reports"></a>Informes

Puede crear un informe desde un conjunto de datos directamente en la aplicación con hello API de JavaScript. Para más información, consulte [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creación de un nuevo informe a partir de un conjunto de datos en Power BI Embedded).

## <a name="see-also"></a>Otras referencias

[Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)](power-bi-embedded-get-started-sample.md)  
[Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Inserción de un informe](power-bi-embedded-embed-report.md)  
[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creación de un nuevo informe a partir de un conjunto de datos en Power BI Embedded) 
[Save reports](power-bi-embedded-save-reports.md) (Guardar informes)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)  
¿Tiene más preguntas? [Intente Hola Comunidad de Power BI](http://community.powerbi.com/)

