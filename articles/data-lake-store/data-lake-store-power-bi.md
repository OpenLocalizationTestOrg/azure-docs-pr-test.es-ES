---
title: "datos de aaaAnalyze en el almacén de Data Lake mediante Power BI | Documentos de Microsoft"
description: "Usar Power BI tooanalyze datos almacenados en el almacén de Azure Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a>Análisis de datos en Almacén de Data Lake mediante Power BI
En este artículo, aprenderá cómo toouse Power BI Desktop tooanalyze y visualizar los datos almacenados en el almacén de Azure Data Lake.

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Cuenta del Almacén de Azure Data Lake**. Siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](data-lake-store-get-started-portal.md). En este artículo se da por supuesto que ya ha creado una cuenta de almacén de Data Lake, denominada **mybidatalakestore**y cargar un archivo de datos de ejemplo (**Drivers.txt**) tooit. Este archivo de ejemplo está disponible para su descarga en [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)(Repositorio Git de Azure Data Lake).
* **Power BI Desktop**. Puede descargarla del [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=45331). 

## <a name="create-a-report-in-power-bi-desktop"></a>Creación de un informe en Power BI Desktop
1. Inicie Power BI Desktop en el equipo.
2. De hello **inicio** la cinta de opciones, haga clic en **obtener datos**y, a continuación, haga clic en más. Hola **obtener datos** cuadro de diálogo, haga clic en **Azure**, haga clic en **almacén de Azure Data Lake**y, a continuación, haga clic en **conectar**.
   
    ![Conecte el almacén de Lake tooData](./media/data-lake-store-power-bi/get-data-lake-store-account.png "conectar tooData Lake almacén")
3. Si ve un cuadro de diálogo acerca de conector de hello en una fase de desarrollo, optar por toocontinue.
4. Hola **Store de Microsoft Azure Data Lake** cuadro de diálogo, proporcione Hola URL tooyour almacén de Data Lake cuenta y, a continuación, haga clic en **Aceptar**.
   
    ![Dirección URL de Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "Dirección URL de Data Lake Store")
5. En el siguiente cuadro de diálogo hello, haga clic en **iniciar sesión en** toosign en cuenta de almacén de Data Lake. Será redirigido el inicio de sesión de la organización de tooyour en la página. Siga toosign de mensajes de Hola en cuenta Hola.
   
    ![Iniciar sesión en Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Iniciar sesión en Data Lake Store")
6. Cuando haya iniciado sesión correctamente, haga clic en **Conectar**.
   
    ![Conecte el almacén de Lake tooData](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "conectar tooData Lake almacén")
7. cuadro de diálogo siguiente Hello muestra archivo hello que cargan tooyour cuenta de almacén de Data Lake. Compruebe la información de hello y, a continuación, haga clic en **carga**.
   
    ![Cargar datos desde Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Cargar datos desde Data Lake Store")
8. Después de haberse cargados correctamente datos de hello en Power BI, verá Hola después de campos de hello **campos** ficha.
   
    ![Campos importados](./media/data-lake-store-power-bi/imported-fields.png "Campos importados")
   
    Sin embargo, toovisualize y analizar datos de hello, se prefiere Hola datos toobe disponible por hello después de campos
   
    ![Campos deseados](./media/data-lake-store-power-bi/desired-fields.png "Campos deseados")
   
    En pasos de hello, actualizaremos Hola consultar tooconvert Hola importado los datos en formato deseado Hola.
9. De hello **inicio** la cinta de opciones, haga clic en **editar consultas**.
   
    ![Editar consultas](./media/data-lake-store-power-bi/edit-queries.png "Editar consultas")
10. Hola, el Editor de consultas en hello **contenido** columna, haga clic en **binario**.
    
    ![Editar consultas](./media/data-lake-store-power-bi/convert-query1.png "Editar consultas")
11. Verá un icono de archivo, que representa hello **Drivers.txt** archivo que ha cargado. Haga clic en el archivo de Hola y haga clic en **CSV**.    
    
    ![Editar consultas](./media/data-lake-store-power-bi/convert-query2.png "Editar consultas")
12. Debería ver una salida como la siguiente. Los datos ahora están disponibles en un formato que se pueden usar toocreate visualizaciones.
    
    ![Editar consultas](./media/data-lake-store-power-bi/convert-query3.png "Editar consultas")
13. De hello **inicio** la cinta de opciones, haga clic en **cerrar y aplicar**y, a continuación, haga clic en **cerrar y aplicar**.
    
    ![Editar consultas](./media/data-lake-store-power-bi/load-edited-query.png "Editar consultas")
14. Una vez que se actualiza la consulta de hello, Hola **campos** ficha mostrará Hola nuevos campos disponibles para la visualización.
    
    ![Campos actualizados](./media/data-lake-store-power-bi/updated-query-fields.png "Campos actualizados")
15. Permítanos crear un gráfico circular toorepresent controladores hello en cada ciudad de un país determinado. toodo por lo tanto, asegúrese de hello las selecciones siguientes.
    
    1. Desde la pestaña de visualizaciones de hello, haga clic en el símbolo de Hola para un gráfico circular.
       
        ![Crear gráfico circular](./media/data-lake-store-power-bi/create-pie-chart.png "Crear gráfico circular")
    2. columnas de Hola que vamos a toouse son **columna 4** (nombre de ciudad de Hola) y **7 de la columna** (nombre del país Hola). Arrastre estas columnas de **campos** pestaña demasiado**visualizaciones** pestaña tal y como se muestra a continuación.
       
        ![Creación de visualizaciones](./media/data-lake-store-power-bi/create-visualizations.png "Creación de visualizaciones")
    3. gráfico circular de Hello debería parecerse como Hola se muestra a continuación.
       
        ![Gráfico circular](./media/data-lake-store-power-bi/pie-chart.png "Crear visualizaciones")
16. Seleccionando un país específico de los filtros de nivel de página hello, ahora puede ver número Hola de controladores en cada ciudad de país de hello seleccionado. Por ejemplo, en hello **visualizaciones** ficha **página filtros de nivel de**, seleccione **Brasil**.
    
    ![Seleccionar un país](./media/data-lake-store-power-bi/select-country.png "Seleccionar un país")
17. gráfico circular de Hello es toodisplay actualizan automáticamente controladores de hello en ciudades Hola de Brasil.
    
    ![Controladores en un país](./media/data-lake-store-power-bi/driver-per-country.png "Controladores por país")
18. De hello **archivo** menú, haga clic en **guardar** visualización de hello toosave como un archivo de Power BI Desktop.

## <a name="publish-report-toopower-bi-service"></a>Publicar el servicio de informes de BI tooPower
Una vez haya creado las visualizaciones de hello en Power BI Desktop, puede compartir con otros usuarios mediante la publicación de servicio de Power BI toohello. Para obtener instrucciones sobre cómo toodo que vea [publicar desde Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).

## <a name="see-also"></a>Otras referencias
* [Análisis de datos en el Almacén de Data Lake con Análisis de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

