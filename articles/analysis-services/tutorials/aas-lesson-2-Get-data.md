---
título: aaa "lección de Azure Analysis Services tutorial 2: obtener datos | Descripción de Microsoft Docs": describe cómo tooget e importar datos en Hola proyecto tutorial de Analysis Services de Azure. servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 01/06/2017 ms.author: owend
---

# <a name="lesson-2-get-data"></a>Lección 2: Obtención de datos

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, usa obtener datos de la base de datos de ejemplo de tooconnect toohello AdventureWorksDW2014 SSDT, seleccione datos, vista previa y filtrar y, a continuación, importar el área de trabajo del modelo.  
  
Al usar Obtención de datos, puede importar datos de diversos de orígenes: Azure SQL Database, Oracle, Sybase, fuente OData, Teradata, archivos y mucho más. También puede consultar datos mediante una expresión de fórmula de Power Query M.
  
Estimado toocomplete de tiempo en esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 1: crear un nuevo proyecto de modelo tabular](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Crear una conexión  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>una base de datos de conexión toohello AdventureWorksDW2014 toocreate  
  
1.  En el Explorador de modelos tabulares, haga clic con el botón derecho en **Orígenes de datos** > **Importar desde el origen de datos**.  
  
    Esto inicia obtener datos, que le guiará por el origen de datos de conexión tooa. Si no ve el Explorador de modelos tabulares, en **el Explorador de soluciones**, haga doble clic en **Model.bim** tooopen modelo de hello en el Diseñador de Hola. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  En Obtención de datos, haga clic en **Base de datos** > **Base de datos de SQL Server** > **Conectar**.  
  
3.  Hola **base de datos de SQL Server** cuadro de diálogo, en **Server**, escriba nombre de saludo del servidor de Hola donde instaló la base de datos de hello AdventureWorksDW2014 y, a continuación, haga clic en **conectar**.  

4.  Cuando se le solicite credenciales tooenter, necesita credenciales de hello toospecify Analysis Services utiliza el origen de datos de toohello tooconnect al importar y procesar datos. En **Modo de suplantación**, seleccione **Suplantar cuenta**, escriba las credenciales y haga clic en **Conectar**. Se recomienda que usar una cuenta que no expire contraseña Hola.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > Mediante una cuenta de usuario de Windows y una contraseña proporciona el método más seguro de hello conexión tooa del origen de datos.
  
5.  En el navegador, seleccione hello **AdventureWorksDW2014** la base de datos y, a continuación, haga clic en **Aceptar**. Esto crea la base de datos de hello conexión toohello. 
  
6.  En el navegador, seleccione Hola casilla de verificación de hello las tablas siguientes: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, y **FactInternetSales**.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
Después de hacer clic en Aceptar, se abre el Editor de consultas. En la siguiente sección hello, seleccione solo los datos de Hola que desea tooimport.

  
## <a name="filter-hello-table-data"></a>Filtrar datos de la tabla de Hola  
Tablas de base de datos de ejemplo de Hola AdventureWorksDW2014 tienen datos que no es necesario tooinclude en el modelo. Cuando sea posible, desea toofilter espacio de datos innecesarios toosave en la memoria utilizada por el modelo de Hola. Filtra algunas de las columnas de Hola de tablas por lo que no está importados en la base de datos de área de trabajo de Hola o base de datos de modelo de hello después de que se haya implementado. 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>datos de la tabla toofilter Hola antes de importar  
  
1.  En el Editor de consultas, seleccione hello **DimCustomer** tabla. Aparece una vista de tabla de DimCustomer hello en el origen de datos de hello (la base de datos de ejemplo AdventureWorksDWQ2014). 
  
2.  Seleccione al mismo tiempo (Ctrl+clic) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, haga clic con el botón derecho y, después, haga clic en **Quitar columnas**. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    Puesto que los valores de hello para estas columnas no son relevantes tooInternet análisis de ventas, no hay necesidad de tooimport estas columnas. Si elimina las columnas innecesarias, el modelo será más pequeño y eficaz.  
  
4.  Filtrar Hola restantes tablas mediante la eliminación de hello después de las columnas de cada tabla:  
    
    **DimDate**
    
      |Columna|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Columna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Columna|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |Columna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Columna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |Columna|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Importar datos de las columnas y las tablas de hello seleccionado  
Ahora que ha obtenido una vista previa y filtran los datos innecesarios, puede importar el resto de Hola de datos de Hola que desea. Asistente de Hello importa datos de la tabla de hello junto con las relaciones entre tablas. Las nuevas tablas y columnas se crean en el modelo de Hola y datos que filtró no se importará.  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>Hola tooimport seleccionado tablas y los datos de columna  
  
1.  Revise lo que ha seleccionado. Si todo es correcto, haga clic en **Importar**. cuadro de diálogo de procesamiento de datos de Hello muestra estado Hola de datos que se va a importar desde el origen de datos en la base de datos del área de trabajo.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  Haga clic en **Cerrar**.  

  
## <a name="save-your-model-project"></a>Guardar el proyecto de modelo  
Es importante toofrequently guardar el proyecto de modelo.  
  
#### <a name="toosave-hello-model-project"></a>proyecto de modelos de hello toosave  
  
-   Haga clic en **Archivo** > **Guardar todo**.  
  
## <a name="whats-next"></a>Pasos siguientes
[Lección 3: Marcado como tabla de fechas](../tutorials/aas-lesson-3-mark-as-date-table.md)

  
  
