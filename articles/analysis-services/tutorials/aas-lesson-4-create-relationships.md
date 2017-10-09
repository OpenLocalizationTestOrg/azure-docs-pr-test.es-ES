---
título: aaa "lección de Azure Analysis Services tutorial 4: crear relaciones | Descripción de Microsoft Docs": describe cómo toocreate relaciones en Hola proyecto tutorial de Analysis Services de Azure. servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-4-create-relationships"></a>Lección 4: Creación de relaciones

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, compruebe las relaciones de Hola que se crearon automáticamente cuando importó los datos y agregar nuevas relaciones entre tablas diferentes. Una relación es una conexión entre dos tablas que establece cómo se deben relacionar datos de hello en esas tablas. Por ejemplo, tablas de DimProduct de Hola y Hola DimProductSubcategory tienen una relación basada en hechos de Hola que pertenece cada producto tooa subcategoría. más información, consulte toolearn [relaciones](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular).
  
Estimado toocomplete de tiempo en esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 3: marcar como tabla de fechas](../tutorials/aas-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Revisión de las relaciones existentes e incorporación de nuevas relaciones  
Cuando importa datos mediante obtener datos, tenemos siete tablas de base de datos de hello AdventureWorksDW2014. Por lo general, al importar datos desde un origen relacional, las relaciones existentes se importan automáticamente junto con datos de Hola. Sin embargo, antes de continuar creando el modelo, debe comprobar que las relaciones entre tablas se crearon correctamente. En este tutorial, agregará tres relaciones nuevas.  
  
#### <a name="tooreview-existing-relationships"></a>relaciones existentes de tooreview  
  
1.  Haga clic en hello **modelo** menú > **vista de modelo** > **vista de diagrama**.  

    Hello Diseñador de modelos aparece ahora en la vista de diagrama, un formato gráfico para mostrar todas las tablas de Hola que importó con líneas entre ellos. líneas de Hello entre tablas indican las relaciones de Hola que se crearon automáticamente cuando importó los datos de Hola.
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    Incluir tantas tablas hello como sea posible mediante el uso de controles de minimapa situados en la esquina inferior derecha de hello del Diseñador de modelos de Hola. También puede haga clic y arrastre ubicaciones de toodifferent de tablas, aunando las tablas o colocándolas en un orden concreto. Mover tablas no afecta a las relaciones de hello ya entre las tablas de Hola. tooview todas las columnas de hello en una tabla determinada, haga clic y arrastre en un tooexpand de borde de tabla o que sea menor.  
  
2.  Haga clic en la línea continua de hello entre hello **DimCustomer** hello y tabla **DimGeography** tabla. Hola la línea sólida entre estas dos tablas muestra que esta relación está activa, es decir, se utiliza de forma predeterminada al calcular las fórmulas de DAX.  
  
    Hola aviso **GeographyKey** columna Hola **DimCustomer** hello y tabla **GeographyKey** columna Hola **DimGeography** tabla aparecen ahora dentro de un cuadro. Estas columnas se utilizan en la relación de Hola. Hello propiedades de la relación aparecen ahora también en hello **propiedades** ventana.  
  
    > [!TIP]  
    > Además toousing Hola Diseñador de modelos en la vista de diagrama, también puede usar Hola administrar relaciones diálogo cuadro tooshow hello las relaciones entre todas las tablas en un formato de tabla. En el Explorador de modelos tabulares, haga clic con el botón derecho en **Relaciones** > **Administrar relaciones**.
  
3.  Comprobar Hola siguiendo las relaciones que se crearon cuando cada una de las tablas de Hola se importaron desde la base de datos de hello AdventureWorksDW:  
  
    |Active|Tabla|Tabla de búsquedas relacionadas|  
    |----------|---------|------------------------|  
    |Sí|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Sí|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Sí|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Sí|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Sí|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Si falta cualquiera de las relaciones de hello, compruebe que el modelo incluye hello las tablas siguientes: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory y FactInternetSales. Si las tablas de Hola se importan en la misma conexión de origen de datos independientes veces, las relaciones entre esas tablas no se crean y deben crearse manualmente.  

### <a name="take-a-closer-look"></a>Un examen más profundo
En la vista de diagrama, tenga en cuenta una flecha, un asterisco y un número de líneas de Hola que mostrar hello relaciones entre tablas.

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

flecha de Hello muestra la dirección del filtro Hola. asterisco de Hello muestra que esta tabla es Hola lado "varios" en la cardinalidad de la relación de Hola y Hola uno muestra que esta tabla es un extremo de Hola de relación de Hola. Si necesita tooedit una relación; Por ejemplo, cambiar la dirección del filtro o la cardinalidad de la relación de hello, haga doble clic en el cuadro de diálogo de hello relación línea tooopen Hola Editar relación.

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

Estas características están diseñadas para modelado de datos avanzados y estén fuera Hola el ámbito de este tutorial. más información, consulte toolearn [bidireccional entre los filtros para modelos tabulares de Analysis Services](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services).

En algunos casos, deberá toocreate relaciones adicionales entre las tablas en el modelo toosupport determinada lógica empresarial. Para este tutorial, necesita toocreate tres relaciones adicionales entre tablas de FactInternetSales de Hola y Hola DimDate.  
  
#### <a name="tooadd-new-relationships-between-tables"></a>tooadd nuevas relaciones entre tablas  
  
1.  En Diseñador de modelos de Hola Hola **FactInternetSales** de tabla, haga clic y mantenga en hello **OrderDate** columna y, a continuación, arrastre Hola cursor toohello **fecha** columna Hola  **DimDate** de tabla y, a continuación, la versión.  

    Aparece una línea sólida que indica que ha creado una relación activa entre hello **OrderDate** columna Hola **venta por Internet** hello y tabla **fecha** columna Hola **Fecha** tabla. 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > Al crear relaciones, dirección de la cardinalidad y filtro de hello entre tabla principal de Hola y Hola relacionadas con la búsqueda se selecciona automáticamente.  
  
2.  Hola **FactInternetSales** de tabla, haga clic y mantenga en hello **DueDate** columna y, a continuación, arrastre Hola cursor toohello **fecha** columna Hola **DimDate** de tabla y, a continuación, la versión.  
  
    Aparecerá una línea punteada que indica que ha creado una relación inactiva entre hello **DueDate** columna Hola **FactInternetSales** hello y tabla **fecha** columna Hola **DimDate** tabla. Puede tener varias relaciones entre tablas, pero solo una relación puede estar activa simultáneamente. Las relaciones inactivas se pueden realizar agregaciones especiales de active tooperform en expresiones de DAX personalizadas.  
  
3.  Finalmente, cree una relación más. Hola **FactInternetSales** de tabla, haga clic y mantenga en hello **ShipDate** columna y, a continuación, arrastre Hola cursor toohello **fecha** columna Hola **DimDate** de tabla y, a continuación, la versión.  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Pasos siguientes
[Lección 5: Creación de columnas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md)
  
  
  
