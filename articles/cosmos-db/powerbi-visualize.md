---
title: tutorial de BI de aaaPower de conector de base de datos de Azure Cosmos | Documentos de Microsoft
description: Utilice este tooimport de tutorial de Power BI JSON, crear informes precisos y visualizar datos mediante el conector de base de datos de Azure Cosmos y Power BI Hola.
keywords: tutorial de power bi, visualizar datos, conector de power bi
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a>Tutorial de Power BI para base de datos de Azure Cosmos: visualizar datos mediante el conector de Power BI Hola
[PowerBI.com](https://powerbi.microsoft.com/) es un servicio en línea, donde puede crear y compartir paneles e informes con los datos que es importante tooyou y su organización.  Power BI Desktop es dedicada datos de informe herramienta de creación que le permite tooretrieve de varios orígenes de datos, combinar y transformar datos de hello, crear visualizaciones e informes eficaces y publicar informes de hello tooPower BI.  Con la versión más reciente de Hola de Power BI Desktop, ahora puede conectarse tooyour Cosmos DB cuenta mediante el conector de base de datos de Cosmos Hola para Power BI.   

En este tutorial de Power BI, se recorra Hola pasos tooconnect tooa cuenta de base de datos de Cosmos en Power BI Desktop, navegar por colección tooa donde los deseamos tooextract Hola datos mediante Hola navegador, transformación de datos JSON en formato tabular con Power BI Desktop Query El Editor y crear y publicar un informe tooPowerBI.com.

Después de completar este tutorial de Power BI, podrá hello tooanswer pueda siguientes preguntas:  

* ¿Cómo genero informes con datos de Cosmos DB con Power BI Desktop?
* ¿Cómo se puede conectar tooa cuenta de base de datos de Cosmos en Power BI Desktop?
* ¿Cómo puedo recuperar datos de una colección en Power BI Desktop?
* ¿Cómo puedo transformar datos JSON anidados en Power BI Desktop?
* ¿Cómo puedo publicar y compartir mis informes en PowerBI.com?

> [!NOTE]
> Conector de Power BI de Hello para la base de datos de Azure Cosmos conecta tooPower BI Desktop para la extracción y transformación de datos. Los informes creados en Power BI Desktop se pueden tooPowerBI.com publicado. No se puede realizar la extracción directa y la transformación de datos de Azure Cosmos DB en PowerBI.com. 

## <a name="prerequisites"></a>Requisitos previos
Antes de seguir las instrucciones de hello en este tutorial de Power BI, asegúrese de que tiene toohello de acceso a recursos siguientes:

* [versión más reciente de Hola de Power BI Desktop](https://powerbi.microsoft.com/desktop).
* Cuenta de acceso de demostración tooour o datos de la cuenta de base de datos de Cosmos.
  * cuenta de demostración de Hello se rellena con datos de volcano de Hola que se muestra en este tutorial. Esta cuenta de demostración no está vinculada a ningún SLA y está pensada únicamente con fines de demostración.  Nos reservamos hello toomake derecho modificaciones toothis demostración cuenta incluido pero sin limitarse a, terminar Hola cuenta, cambiar la clave de hello, restringir el acceso, cambiar y eliminar datos de hello, en cualquier momento sin aviso por adelantado o el motivo.
    * Dirección URL: https://analytics.documents.azure.com
    * Clave de solo lectura: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==
  * O bien, toocreate su propia cuenta, consulte [crear una cuenta de base de datos de la base de datos de Azure Cosmos utilizando Hola portal de Azure](https://azure.microsoft.com/documentation/articles/create-account/). A continuación, tooget ejemplo volcano datos similar toowhat usan en este tutorial (pero no contienen bloques de GeoJSON Hola), vea hello [sitio NOAA](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) y, a continuación, importar datos de hello mediante hello [migración de datos de la base de datos de Azure Cosmos herramienta](import-data.md).

tooshare los informes en PowerBI.com, debe tener una cuenta en PowerBI.com.  toolearn más información acerca de Power BI para Free y Power BI Pro, visite [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).

## <a name="lets-get-started"></a>Comencemos.
En este tutorial, imaginemos que son un geologist estudiando libro alrededor de Hola a todos.  datos de volcano Hola se almacenan en una cuenta de base de datos de Cosmos y documentos JSON de hello el aspecto siguiente documento de ejemplo de Hola.

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

Desea datos tooretrieve Hola volcano Hola DB Cosmos cuenta y visualización los datos en un informe de Power BI interactivo como Hola después de informe.

![Al completar este tutorial de Power BI con el conector de Power BI hello, podrá toovisualize capaz de datos con informes de Power BI Desktop volcano hello](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

¿Toogive listo TI a intentarlo? Comencemos.

1. Ejecute Power BI Desktop en su estación de trabajo.
2. Una vez iniciado Power BI Desktop, se muestra la pantalla de *inicio de sesión* .
   
    ![Pantalla de inicio de sesión de Power BI Desktop: conector de Power BI](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. También puede **obtener datos**, consulte **orígenes recientes**, o **abrir otros informes** directamente desde hello *bienvenida* pantalla.  Haga clic en hello X en pantalla de bienvenida de tooclose Hola esquina superior derecha. Hola **informe** se muestra la vista de Power BI Desktop.
   
    ![Vista de informes de Power BI Desktop: conector de Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. Seleccione hello **inicio** la cinta de opciones, a continuación, haga clic en **obtener datos**.  Hola **obtener datos** debe aparecer la ventana.
5. Haga clic en **Azure**, seleccione **Microsoft Azure DocumentDB (Beta)** y, a continuación, haga clic en **Conectar**. 

    ![Obtención de datos de Power BI Desktop: conector de Power BI](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. En hello **conector de vista previa** página, haga clic en **continuar**. Hola **documentos de Microsoft Azure Connect** aparecerá la ventana.
7. Especificar Hola DB Cosmos cuenta dirección URL del extremo que desee tooretrieve datos de saludo de tal y como se muestra a continuación y, a continuación, haga clic en **Aceptar**. toouse su propia cuenta, puede recuperar Hola cuadro Dirección URL de URI de Hola Hola  **[claves](manage-account.md#keys)**  hoja de hello portal de Azure. Hola toouse demo cuenta, escriba `https://analytics.documents.azure.com` para la dirección URL de Hola. 
   
    Deje en blanco los nombre de base de datos de hello, el nombre de la colección y la instrucción SQL a como estos campos son opcionales.  En su lugar, se usará Hola navegador tooselect Hola base de datos y la colección tooidentify procedencia de los datos de Hola.
   
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Ventana de conexión de Desktop](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. Si se está conectando a punto de conexión de toothis para hello primera vez, le pediremos clave de la cuenta de hello. Para su propia cuenta, recuperar la clave de Hola de hello **Primary Key** cuadro hello  **[claves de solo lectura](manage-account.md#keys)**  hoja de hello portal de Azure. Para la cuenta de demostración de hello, clave de hello es `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`. Escriba la clave adecuada de hello y, a continuación, haga clic en **conectar**.
   
    Se recomienda usar clave Hola de solo lectura al generar informes.  Esto evitará que una exposición innecesaria Hola clave maestra toopotential de riesgos de seguridad. clave de solo lectura de Hello está disponible en hello [claves](manage-account.md#keys) hoja de hello portal de Azure o puede usar la información de cuenta de demostración de hello proporcionado anteriormente.
   
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Clave de cuenta](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > Si se produce un error que dice "base de datos especificada de hello no se encontró." Consulte los pasos de solución de hello en este [problema de Power BI](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).
    
9. Cuando está conectado correctamente la cuenta de hello, Hola **navegador** aparecerá.  Hola **navegador** mostrará una lista de bases de datos en la cuenta de hello.
10. Haga clic en y se expanden en la base de datos de Hola donde hello datos para informes de hello procederán de, si usa la cuenta de demostración de hello, seleccione **volcanodb**.   
11. Ahora, seleccione una recopilación que se recuperarán los datos de Hola de. Si está utilizando la cuenta de demostración de hello, seleccione **volcano1**.
    
    panel de vista previa de Hello muestra una lista de **registro** elementos.  Un documento se representa como un tipo **Registro** en Power BI. De forma similar, un bloque JSON anidado dentro de un documento también es un **Registro**.
    
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Ventana del navegador](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. Haga clic en **editar** toolaunch Hola Editor de consultas en una nueva ventana tootransform Hola de datos.

## <a name="flattening-and-transforming-json-documents"></a>Eliminación de formato y transformación de documentos JSON
1. Cambiar la ventana del Editor de consultas de Power BI toohello, donde hello **documento** columna en el panel central de Hola.
   ![Editor de consultas de Power BI Desktop](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Haga clic en Ampliador hello en hello derecha del programa Hola a **documento** encabezado de columna.  Aparecerá el menú contextual de Hello con una lista de campos.  Seleccione los campos de hello necesarios para el informe, por ejemplo, nombre de Volcano, país, región, ubicación, elevación, tipo, estado y última lectura conocer y, a continuación, haga clic en **Aceptar**.
   
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Expandir documentos](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. panel de centro de Hola se mostrará una vista previa del resultado de hello con campos de hello seleccionados.
   
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Resultados sin formato](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. En nuestro ejemplo, hello propiedad de ubicación es un bloque de GeoJSON en un documento.  Como puede ver, la ubicación se representa como un tipo **Registro** en Power BI Desktop.  
5. Haga clic en Ampliador hello en hello derecha del encabezado de columna de ubicación de Hola.  Aparecerá el menú contextual de Hello con campos de tipo y las coordenadas.  Vamos a seleccionar el campo de coordenadas de Hola y haga clic en **Aceptar**.
   
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Registro de ubicación](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. Hello panel central muestra ahora una columna de coordenadas de **lista** tipo.  Tal como se muestra en principio Hola de tutorial de hello, Hola datos GeoJSON en este tutorial es de tipo Point con valores de latitud y longitud registrados en la matriz de coordenadas de Hola.
   
    elemento de Hello coordenadas [0] representa longitud mientras coordenadas [1] representa la latitud.
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Lista de coordenadas](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. Hola tooflatten coordina la matriz, se creará un **columna personalizada** denominado LatLong.  Seleccione hello **Agregar columna** la cinta de opciones y haga clic en **Agregar columna personalizada**.  Hola **Agregar columna personalizada** debe aparecer la ventana.
8. Proporcione un nombre para la nueva columna hello, por ejemplo, LatLong.
9. A continuación, especifique la fórmula personalizada de Hola para hello nueva columna.  En nuestro ejemplo, concatenaremos valores de latitud y longitud de hello separados por comas, como se muestra a continuación con hello siguiente fórmula: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`. Haga clic en **Aceptar**.
   
    Para más información sobre Expresiones de análisis de datos (DAX), incluidas las funciones DAX, visite [DAX Basic en Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).
   
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Agregar columna personalizada](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. Ahora, el panel del centro de hello mostrará Hola nueva LatLong columna rellenado con hello latitud y separados por comas de valores de longitud.
    
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Columna LatLong personalizada](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Si recibe un Error en la nueva columna de hello, asegúrese de que pasos de Hola aplica la configuración de consulta coincide con hello figura siguiente:
    
    ![Los pasos aplicados deben ser los siguientes: Source, Navigation, Expanded Document, Expanded Document.Location, Added Custom](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    Si los pasos son diferentes, eliminar Hola pasos adicionales e intente agregar columna personalizada Hola de nuevo. 
11. Ahora hemos completado datos sin formato de hello en formato tabular.  Puede aprovechar todas las características de hello disponibles en hello tooshape del Editor de consultas y transformar datos en la base de datos de Cosmos.  Si usa el ejemplo hello, cambiar tipo de datos de hello para la elevación demasiado**número entero** cambiando hello **tipo de datos** en hello **inicio** la cinta de opciones.
    
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Cambiar tipo de columna](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. Haga clic en **cerrar y aplicar** modelo de datos de toosave Hola.
    
    ![Tutorial de Power BI para conector de Power BI de Azure Cosmos DB - Cerrar y aplicar](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a>Generar informes de Hola
Power BI Desktop informe view es donde puede empezar a crear informes toovisualize datos.  Puede crear informes arrastrando y soltando campos en hello **informe** lienzo.

![Vista de informes de Power BI Desktop: conector de Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

Hola vista de informe, debe buscar:

1. Hola **campos** panel, esto es donde podrá ver una lista de modelos de datos con campos que puede usar para los informes.
2. Hola **visualizaciones** panel. Un informe puede contener una o varias visualizaciones.  Elegir tipos de objeto visual Hola ajustar sus necesidades de hello **visualizaciones** panel.
3. Hola **informe** lienzo, esto es donde creará objetos visuales de hello para el informe.
4. Hola **informe** página. Puede agregar varias páginas de informes en Power BI Desktop.

siguiente Hello muestra hello indican pasos básicos para crear un informe de vista de mapa interactivo sencillo.

1. En nuestro ejemplo, se creará una vista del mapa que muestra la ubicación de Hola de cada Volcán.  Hola **visualizaciones** panel, haga clic en el tipo visual de mapa de hello como se resalta en Hola de captura de pantalla anterior.  Debería ver Hola mapa tipo de objeto visual pintado sobre hello **informe** lienzo.  Hola **visualización** panel también debe mostrar un conjunto de propiedades relacionadas toohello tipo visual de mapa.
2. Ahora, arrastre y coloque el campo de LatLong Hola desde hello **campos** panel toohello **ubicación** propiedad en **visualizaciones** panel.
3. A continuación, arrastre y coloque Hola Volcano nombre campo toohello **leyenda** propiedad.  
4. A continuación, arrastre y coloque Hola elevación campo toohello **tamaño** propiedad.  
5. Ahora debería ver Hola mapa visual que muestra un conjunto de burbujas que indica la ubicación de Hola de cada volcano con tamaño de Hola de burbuja de hello correlacionar toohello elevación de volcano Hola.
6. Ahora ha creado un informe básico.  Puede personalizar aún más el informe de hello agregando más visualizaciones.  En nuestro caso, hemos agregado un informe de segmentación de datos toomake Hola de tipo Volcano interactivo.  
   
    ![Captura de pantalla de informe de Power BI Desktop final Hola tras la finalización de tutorial de Power BI de hello para la base de datos de Azure Cosmos](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>Publicación y uso compartido del informe
tooshare el informe, debe tener una cuenta en PowerBI.com.

1. Hola Power BI Desktop, haga clic en hello **inicio** la cinta de opciones.
2. Haga clic en **Publicar**.  Será tooenter solicitadas Hola nombre y contraseña para su cuenta de PowerBI.com.
3. Una vez que se ha autenticado la credencial de hello, informe de hello es destino tooyour publicados que seleccionó.
4. Haga clic en **'PowerBITutorial.pbix' Abrir en Power BI** toosee y compartir el informe en PowerBI.com.
   
    ![Publicación tooPower correcto de BI. Abrir tutorial de Power BI](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>Creación de un panel en PowerBi.com
Ahora que tiene un informe, vamos a compartirlo en PowerBi.com

Al publicar el informe de Power BI Desktop tooPowerBI.com, genera un **informe** y un **conjunto de datos** en su inquilino de PowerBI.com. Por ejemplo, una vez publicado un informe denominado **PowerBITutorial** tooPowerBI.com, verá PowerBITutorial en ambos hello **informes** y **conjuntos de datos** secciones en PowerBI.com.

   ![Captura de pantalla de Hola nuevo informe y conjunto de datos en PowerBI.com](./media/powerbi-visualize/powerbi-reports-datasets.png)

toocreate un panel puede compartirse, haga clic en hello **página Anclar elemento activo** botón en el informe en PowerBI.com.

   ![Captura de pantalla de Hola nuevo informe y conjunto de datos en PowerBI.com](./media/powerbi-visualize/power-bi-pin-live-tile.png)

A continuación, siga las instrucciones de hello en [anclar un icono desde un informe](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate un nuevo panel. 

También puede hacer modificaciones ad hoc tooreport antes de crear un panel. Sin embargo, se recomienda que utilice las modificaciones de Power BI Desktop tooperform hello y volver a publicar Hola informe tooPowerBI.com.

## <a name="refresh-data-in-powerbicom"></a>Actualización de datos en PowerBI.com
Hay dos formas de datos de toorefresh, ad hoc y programadas.

Para una actualización de ad hoc, simplemente haga clic en eclipses hello (...) por hello **conjunto de datos**, por ejemplo, PowerBITutorial. Debería ver una lista de acciones, incluyendo **Actualizar ahora**. Haga clic en **actualizar ahora** toorefresh datos de saludo.

![Captura de pantalla de Actualizar ahora en PowerBI.com](./media/powerbi-visualize/power-bi-refresh-now.png)

Para una actualización programada, Hola después.

1. Haga clic en **Programar actualización** en la lista de acciones de Hola. 

    ![Captura de pantalla de hello Programar actualización en PowerBI.com](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. Hola **configuración** página, expanda **las credenciales del origen de datos**. 
3. Haga clic en **Editar credenciales**. 
   
    aparece en la ventana emergente de configurar Hola. 
4. Escriba la cuenta de base de datos de Cosmos de hello tooconnect clave toohello para ese conjunto de datos, a continuación, haga clic en **iniciar sesión en**. 
5. Expanda **Programar actualización** y configurar la programación de hello desea que el conjunto de datos de toorefresh Hola. 
6. Haga clic en **aplicar** y haya terminado de configurar la actualización programada de Hola.

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de Power BI, consulte [empezar a trabajar con Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).
* toolearn más información acerca de la base de datos de Cosmos, vea hello [página de aterrizaje de documentación de base de datos de Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

