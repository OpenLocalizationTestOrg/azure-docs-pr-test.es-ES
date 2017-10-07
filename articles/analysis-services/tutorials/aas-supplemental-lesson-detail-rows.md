---
título: aaa "lección complementaria tutorial de Analysis Services de Azure: filas de detalles | Descripción de Microsoft Docs": describe cómo toocreate una expresión de filas de detalle de Hola tutorial de Azure de Analysis Services.
servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="supplemental-lesson---detail-rows"></a>Lección complementaria: Filas de detalles

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección complementaria, utilice Hola Editor DAX toodefine una expresión personalizada de filas de detalle. Una expresión de filas de detalles es una propiedad en una medida, proporciona más información acerca de los resultados de hello agregado de una medida de los usuarios finales. 
  
Estimado toocomplete de tiempo en esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Esta lección complementaria forma parte de un tutorial de modelado tabular. Antes de realizar tareas de hello en esta lección complementaria, deberá haber finalizado todas las lecciones anteriores o tiene un proyecto de modelo de ejemplo Adventure Works Internet Sales completado.  
  
## <a name="what-do-we-need-toosolve"></a>¿Qué debemos toosolve?
Echemos un vistazo a los detalles de hello de la medida InternetTotalSales, antes de agregar una expresión de filas de detalle.

1.  En SSDT, haga clic en hello **modelo** menú > **analizar en Excel** tooopen Excel y cree una tabla dinámica en blanco.
  
2.  En **PivotTable Fields**, agregar hello **InternetTotalSales** demasiado de medida de la tabla de hello FactInternetSales**valores**, **CalendarYear**de hello DimDate tabla demasiado**columnas**, y **Spanishcountryregionname** demasiado**filas**. La tabla dinámica ahora obtenemos resultados agregados de medida de hello InternetTotalSales por regiones y año. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. Hola tabla dinámica, haga doble clic en un valor agregado para un año y un nombre de región. A continuación se hace doble clic en valor de Hola para hello y Australia año 2014. Se abre una nueva hoja que contiene datos, pero los datos no resultan de utilidad.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
¿Qué le gustaría toosee aquí es una tabla que contiene columnas y filas de datos que contribuyen toohello agrega el resultado de la medida InternetTotalSales. toodo que, podemos agregar una expresión de filas de detalles como una propiedad de medida de Hola.

## <a name="add-a-detail-rows-expression"></a>Adición de una expresión de filas de detalles

#### <a name="toocreate-a-detail-rows-expression"></a>toocreate una expresión de filas de detalle 
  
1. En SSDT, en la cuadrícula de medidas de la tabla de hello FactInternetSales, haga clic en hello **InternetTotalSales** medida. 

2. En **propiedades** > **expresión de filas de detalle**, haga clic en Hola de tooopen de botón Hola editor Editor de DAX.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. En el Editor de DAX, escriba Hola siguiente expresión:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Esta expresión especifica nombres de columnas, y se devuelven resultados de medida de la tabla FactInternetSales de Hola y las tablas relacionadas cuando un usuario hace doble clic en un resultado agregado en una tabla dinámica o informe.

4. En Excel, eliminar hoja Hola creado en el paso 3, a continuación, haga doble clic en un valor agregado. Esta vez, con una propiedad de expresión de filas de detalle definida para la medida de hello, una nueva hoja abre que contienen datos mucho más útiles.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Vuelva a implementar el modelo.

  
## <a name="see-also"></a>Otras referencias  
[Función SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[Lección complementaria: Seguridad dinámica](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lección complementaria: Jerarquías desiguales](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
