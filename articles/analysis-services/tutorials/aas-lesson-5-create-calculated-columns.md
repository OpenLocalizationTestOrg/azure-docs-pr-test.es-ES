---
título: aaa "lección de Azure Analysis Services tutorial 5: crear columnas calculadas | Descripción de Microsoft Docs": describe cómo toocreate calcula las columnas en el proyecto tutorial de hello Azure Analysis Services. servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 01/06/2017 ms.author: owend
---
# <a name="lesson-5-create-calculated-columns"></a>Lección 5: Creación de columnas calculadas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, se crean datos en el modelo mediante la adición de columnas calculadas. Puede crear columnas calculadas (como columnas personalizadas) cuando se usa obtener datos, utilizando el Editor de consultas Hola o, más adelante en el tipo de diseñador de modelo de hello hacer aquí. más información, consulte toolearn [columnas calculadas](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).
  
Creará cinco columnas calculadas en tres tablas diferentes. Hola pasos son ligeramente diferentes para cada tarea que muestra que hay varias maneras de toocreate columnas, cambiarles el nombre y colocarlos en varias ubicaciones en una tabla.  

En esta lección también usará por primera vez Expresiones de análisis de datos (DAX). DAX es un lenguaje especial para crear expresiones de fórmula altamente personalizables para modelos tabulares. En este tutorial, utilice DAX toocreate calculado columnas, medidas y filtros de rol. más información, consulte toolearn [DAX en modelos tabulares](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular). 
  
Estimado toocomplete de tiempo en esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 4: crear relaciones](../tutorials/aas-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Crear columnas calculadas  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>Crear una columna calculada MonthCalendar en la tabla DimDate de Hola  
  
1.  Haga clic en hello **modelo** menú > **vista de modelo** > **vista de datos**.  
  
    Las columnas calculadas solo pueden crearse mediante el Diseñador de modelo de hello en la vista de datos.  
  
2.  En el Diseñador de modelos de hello, haga clic en hello **DimDate** tabla (pestaña).  
  
3.  Menú contextual hello **CalendarQuarter** encabezado de columna y, a continuación, haga clic en **Insertar columna**.  
  
    Una nueva columna denominada **calcula columna 1** quede toohello insertado de hello **Calendar Quarter** columna.  
  
4.  En la barra de fórmulas de Hola por encima de la tabla de hello, escriba Hola después de la fórmula DAX: Hola de Autocompletar le ayuda a escribir los nombres completos de columnas y tablas y listas de Hola funciones que están disponibles.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    A continuación, se rellenan valores para todas las filas de hello en la columna calculada Hola. Si se desplaza hacia abajo por la tabla hello, verá las filas pueden tener valores diferentes para esta columna se basa en datos de hello en cada fila.    
  
5.  Cambiar el nombre de esta columna demasiado**MonthCalendar**. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
columna calculada de Hello MonthCalendar proporciona un nombre que se puede ordenar por mes.  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>Crear una columna calculada DayOfWeek de tabla de DimDate Hola  
  
1.  Con hello **DimDate** tabla sigue activa, haga clic en hello **columna** menú y, a continuación, haga clic en **Agregar columna**.  
  
2.  En la barra de fórmulas de hello, escriba Hola siguiente fórmula:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Cuando haya terminado de crear Hola fórmula, presione ENTRAR. Hola nueva columna se agrega más a la derecha de la tabla de hello toohello.  
  
3.  Cambiar el nombre de columna de hello demasiado**DayOfWeek**.  
  
4.  Haga clic en el encabezado de columna de Hola y a continuación, arrastre la columna Hola entre hello **EnglishDayNameOfWeek** hello y columna **DayNumberOfMonth** columna.  
  
    > [!TIP]  
    > Movimiento de columnas en la tabla hace más fácil toonavigate.  
  
columna calculada de Hello DayOfWeek proporciona un nombre ordenable del día de saludo de la semana.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>Crear una columna calculada ProductSubcategoryName en la tabla DimProduct de Hola  
  
  
1.  Hola **DimProduct** tabla, desplácese toohello más a la derecha de la tabla de Hola. Columna del extremo derecho de Hola de aviso se denomina **Agregar columna** (en cursiva), haga clic en el encabezado de columna de Hola.  
  
2.  En la barra de fórmulas de hello, escriba Hola siguiente fórmula:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Cambiar el nombre de columna de hello demasiado**ProductSubcategoryName**.  
  
columna calculada de Hello ProductSubcategoryName es toocreate usa una jerarquía en la tabla DimProduct de hello, que incluye datos de columna de hello EnglishProductSubcategoryName en la tabla DimProductSubcategory de Hola. Las jerarquías no pueden abarcar más de una tabla. Creará jerarquías más adelante en la lección 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>Crear una columna calculada ProductCategoryName en la tabla DimProduct de Hola  
  
1.  Con hello **DimProduct** tabla sigue activa, haga clic en hello **columna** menú y, a continuación, haga clic en **Agregar columna**.  
  
2.  En la barra de fórmulas de hello, escriba Hola siguiente fórmula:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Cambiar el nombre de columna de hello demasiado**ProductCategoryName**.  
  
columna calculada de Hello ProductCategoryName es toocreate usa una jerarquía en la tabla DimProduct de hello, que incluye datos de columna de hello EnglishProductCategoryName en la tabla de DimProductCategory Hola. Las jerarquías no pueden abarcar más de una tabla.  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>Crear una columna calculada margen en la tabla FactInternetSales de Hola  
  
1.  En el Diseñador de modelos de hello, seleccione hello **FactInternetSales** tabla.  
  
2.  Crear una nueva columna calculada entre hello **SalesAmount** hello y columna **TaxAmt** columna.  
  
3.  En la barra de fórmulas de hello, escriba Hola siguiente fórmula:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Cambiar el nombre de columna de hello demasiado**margen**.  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    columna calculada de margen de Hello es tooanalyze usado los márgenes de beneficios de cada venta.  
  
## <a name="whats-next"></a>Pasos siguientes
[Lección 6: Creación de medidas](../tutorials/aas-lesson-6-create-measures.md)
  
  
  
