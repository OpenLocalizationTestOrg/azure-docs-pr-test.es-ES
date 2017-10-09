---
title: aaaMove datos de la tabla de Web mediante Data Factory de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo usar Data Factory de Azure de páginas de datos de toomove de una tabla en un servidor Web."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>Movimiento de datos de un origen de tabla web mediante Factoría de datos de Azure
En este artículo se describe cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure de una tabla en una página Web tooa admite el almacén de datos del receptor. En este artículo se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo que presenta una visión general de movimiento de datos con la lista de hello y actividad de copia de almacenes de datos que se admiten como orígenes y receptores.

Factoría de datos admite actualmente solo almacena la migración de datos de un tooother de datos de la tabla de Web, pero no mover los datos de otros datos almacena el destino de tabla de tooa Web.

> [!IMPORTANT]
> Actualmente, este conector web solo permite extraer contenido de tablas de una página HTML. tooretrieve de datos desde un punto de conexión HTTP/s, utilizar [conector HTTP](data-factory-http-connector.md) en su lugar.

## <a name="getting-started"></a>Introducción
Puede crear una canalización con una actividad de copia que mueva los datos desde un almacén de datos Cassandra local mediante el uso de diferentes herramientas o API. 

- toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**. Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido. 
- También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**. Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia. 

Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:

1. Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.
2. Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola. 
3. Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida. 

Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted. Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.  Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son toocopy usa datos de una tabla de web, consulte [ejemplo de JSON: copiar los datos de Web tabla tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) sección de este artículo. 

Hola las secciones siguientes proporciona detalles acerca de propiedades JSON de tabla de toodefine usado factoría de datos entidades específicas tooa Web:

## <a name="linked-service-properties"></a>Propiedades del servicio vinculado
Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooWeb vinculado.

| Propiedad | Descripción | Obligatorio |
| --- | --- | --- |
| type |propiedad de tipo Hello debe establecerse en: **Web** |Sí |
| URL |Origen de dirección URL toohello Web |Sí |
| authenticationType |Anonymous. |Sí |

### <a name="using-anonymous-authentication"></a>Uso de autenticación anónima

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>Propiedades del conjunto de datos
Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo. Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).

Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos. sección typeProperties Hello para el conjunto de datos de tipo **WebTable** tiene Hola propiedades siguientes

| Propiedad | Descripción | Obligatorio |
|:--- |:--- |:--- |
| type |Tipo de conjunto de datos de Hola. debe establecerse demasiado**WebTable** |Sí |
| path |Un recurso de toohello de dirección URL relativo al que contiene la tabla de Hola. |No. Cuando no se especifica la ruta de acceso, se usa solo dirección URL de hello especificada en definición de servicio vinculado de Hola. |
| index |índice de Hola de tabla de hello en recursos de Hola. Vea [Get índice de una tabla en una página HTML](#get-index-of-a-table-in-an-html-page) sección índice toogetting de pasos de una tabla en una página HTML. |Sí |

**Ejemplo:**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propiedades de la actividad de copia
Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo. Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.

Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad. Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.

Actualmente, al origen de hello en la actividad de copia es de tipo **WebSource**, no se admiten propiedades adicionales.


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>Ejemplo de JSON: copiar los datos de Web tabla tooAzure Blob
Hola el siguiente ejemplo se muestra:

1. Un servicio vinculado de tipo [Web](#linked-service-properties).
2. Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
3. Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [WebTable](#dataset-properties).
4. Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [WebSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

ejemplo de Hola copia datos de un tooan de tabla Web blobs de Azure cada hora. propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.

Hola siguiente ejemplo muestra cómo toocopy datos desde un tooan de tabla Web Azure blob. Sin embargo, los datos pueden copiarse directamente Hola indicado en los receptores de tooany de hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo usando Hola actividad de copia de Data Factory de Azure.

**Servicio vinculado de Web** en este ejemplo usa hello Web vinculado servicio con la autenticación anónima. Consulte la sección [Propiedades del servicio vinculado de Web](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

**Servicio vinculado de Almacenamiento de Azure**

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Conjunto de datos de entrada de WebTable** configuración **externo** demasiado**true** informa a servicio de factoría de datos de Hola ese conjunto de datos de hello es factoría de datos de toohello externo y no se generará una actividad en hello factoría de datos.

> [!NOTE]
> Vea [Get índice de una tabla en una página HTML](#get-index-of-a-table-in-an-html-page) sección índice toogetting de pasos de una tabla en una página HTML.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


**Conjunto de datos de salida de blob de Azure**

Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



**Canalización con actividad de copia**

Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora. En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**WebSource** y **receptor** tipo está establecido demasiado**BlobSink**.

Vea [propiedades de tipo WebSource](#copy-activity-type-properties) para lista de Hola de propiedades admitidas por hello WebSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="get-index-of-a-table-in-an-html-page"></a>Obtención de índice de una tabla en una página HTML
1. Iniciar **Excel 2016** y cambiar toohello **datos** ficha.  
2. Haga clic en **nueva consulta** en la barra de herramientas de hello, seleccione demasiado**desde otros orígenes** y haga clic en **de Web**.

    ![Menú de Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. Hola **desde Web** diálogo cuadro, escriba **URL** que usaría en servicio JSON vinculado (por ejemplo: https://en.wikipedia.org/wiki/) junto con la ruta de acceso que se debe especificar para el conjunto de datos de hello (por ejemplo: AFI % 27s_100_Years... 100_Movies) y haga clic en **Aceptar**.

    ![Cuadro de diálogo Desde Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    Dirección URL usada en este ejemplo: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. Si ve **contenido Web Access** cuadro de diálogo, derecha seleccione hello **URL**, **autenticación**y haga clic en **conectar**.

   ![Cuadro de diálogo Acceso a contenido web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. Haga clic en un **tabla** elemento de contenido de toosee de Hola árbol de la vista de tabla de hello y, a continuación, haga clic en **editar** situado en la parte inferior de Hola.  

   ![Cuadro de diálogo Navegador](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. Hola **Editor de consultas** ventana, haga clic en **Editor avanzado** botón de barra de herramientas de Hola.

    ![Botón Editor avanzado](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. En el cuadro de diálogo del Editor avanzado de Hola Hola número junto demasiado "Origen" es el índice de Hola.

    ![Editor avanzado - Índice](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

Si usa Excel 2013, use [Microsoft Power Query para Excel](https://www.microsoft.com/download/details.aspx?id=39379) índice de hello tooget. Vea [página web de Connect tooa](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artículo para obtener más información. Hola pasos son similares si utilizas [Microsoft Power BI para escritorio](https://powerbi.microsoft.com/desktop/).

> [!NOTE]
> columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Rendimiento y optimización
Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.
