---
título: aaa "lección tutorial de Analysis Services de Azure 6: crear medidas | Descripción de Microsoft Docs": describe cómo toocreate se mide en el proyecto tutorial de hello Azure Analysis Services. servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 01/06/2017 ms.author: owend
---
# <a name="lesson-6-create-measures"></a>Lección 6: Creación de medidas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, creará toobe medidas incluida en el modelo. Toohello similar calcula columnas que creó, una medida es un cálculo creado usando una fórmula DAX. Sin embargo, a diferencia de las columnas calculadas, las medidas se evalúan en función de un *filtro* seleccionado por el usuario. Por ejemplo, una columna o una segmentación agrega toohello campo de etiquetas de fila en una tabla dinámica. A continuación, se calcula un valor para cada celda de filtro de Hola por medida Hola aplicado. Las medidas son cálculos eficaces y flexibles que desea tooinclude en casi todos los modelos tabulares tooperform dinámica los cálculos sobre datos numéricos. más información, consulte toolearn [medidas](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).
  
medidas de toocreate, usas Hola *cuadrícula de medidas*. De forma predeterminada, cada tabla tiene una cuadrícula de medidas vacía, aunque en principio no se crean medidas para todas las tablas. cuadrícula de medidas de Hello aparece debajo de una tabla en el Diseñador de modelos de hello en la vista de datos. toohide o mostrar cuadrícula de medidas de Hola para una tabla, haga clic en hello **tabla** menú y, a continuación, haga clic en **Mostrar cuadrícula de medidas**.  
  
Puede crear una medida haciendo clic en una celda vacía de la cuadrícula de medidas de Hola y, a continuación, escribiendo una fórmula DAX en la barra de fórmulas de Hola. Cuando haga clic en entrar toocomplete Hola fórmula, medida de Hola y aparece en la celda de Hola. También puede crear medidas mediante una función de agregación estándar haciendo clic en una columna y, a continuación, haga clic en Hola botón de Autosuma (**∑**) en la barra de herramientas de Hola. Las medidas creadas mediante la característica de Autosuma Hola aparecen en la celda de cuadrícula de medida de hello directamente debajo de la columna de hello, pero se pueden mover.  
  
En esta lección, creará medidas escribiendo una fórmula DAX en la barra de fórmulas de Hola y mediante el uso de la característica de Autosuma Hola.  
  
Estimado toocomplete de tiempo en esta lección: **30 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 5: crear columnas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Crear medidas  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a>una medida DaysCurrentQuarterToDate en la tabla DimDate de hello toocreate  
  
1.  En el Diseñador de modelos de hello, haga clic en hello **DimDate** tabla.  
  
2.  En la cuadrícula de medidas de hello, haga clic en celda vacía superior izquierda de Hola.  
  
3.  En la barra de fórmulas de hello, escriba Hola siguiente fórmula:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Celda superior izquierda de anuncio Hola ahora contiene un nombre de medida, **DaysCurrentQuarterToDate**, seguido del resultado de hello, **92**.
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    A diferencia de las columnas calculadas, con fórmulas de medida puede escribir nombre de medida de hello, seguido de dos puntos, seguido por la expresión de la fórmula Hola.

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a>una medida DaysInCurrentQuarter en la tabla DimDate de hello toocreate  
  
1.  Con hello **DimDate** tabla sigue activa en el Diseñador de modelos de hello, en la cuadrícula de medidas de hello, haga clic en la celda vacía de hello debajo de la medida de Hola que ha creado.  
  
2.  En la barra de fórmulas de hello, escriba Hola siguiente fórmula:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Al crear una relación de comparación entre un período incompleto y Hola período anterior. fórmula de Hello debe calcular la proporción de Hola de período de Hola que ha transcurrido y compararla toohello igual proporción Hola del período anterior. En este caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] proporciona Hola proporción transcurrido en hello período actual.  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a>una medida de InternetDistinctCountSalesOrder en la tabla FactInternetSales de hello toocreate  
  
1.  Haga clic en hello **FactInternetSales** tabla.   
  
2.  Haga clic en hello **SalesOrderNumber** encabezado de columna.  
  
3.  En la barra de herramientas de hello, haga clic en hello flecha abajo siguiente toohello Autosuma (**∑**) y, a continuación, seleccione **DistinctCount**.  
  
    característica de Autosuma Hola automáticamente crea una medida para la columna seleccionada de hello mediante la fórmula de agregación estándar de hello DistinctCount.  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  En la cuadrícula de medidas de hello, haga clic en nueva medida hello y, a continuación, en hello **propiedades** ventana, en **nombre de medida**, cambiar el nombre de medida de hello demasiado**InternetDistinctCountSalesOrder**. 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a>toocreate saber qué medidas adicionales en la tabla FactInternetSales de Hola  
  
1.  Mediante la característica de Autosuma de hello, crear y asigne un nombre hello siguientes medidas:  

    |Columna|Nombre de la medida|Autosuma (∑)|Fórmula|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Recuento|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Suma|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Suma|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Suma|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Suma|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|Suma|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Suma|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|Suma|=SUM([Freight])|  
  
2.  Haciendo clic en crear una celda vacía en la cuadrícula de medidas de Hola y mediante el uso de la barra de fórmulas de hello, y mide el nombre detrás de hello en orden:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Las medidas creadas para la tabla FactInternetSales de hello pueden ser usado tooanalyze de datos financieros críticos como ventas, costos y margen de beneficio para los elementos definidos por el filtro seleccionado de usuario de Hola.  
  
## <a name="whats-next"></a>Pasos siguientes
[Lección 7: Creación de indicadores clave de rendimiento](../tutorials/aas-lesson-7-create-key-performance-indicators.md)  

  
