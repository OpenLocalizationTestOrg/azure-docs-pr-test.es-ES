---
título: aaa "lección tutorial de Analysis Services de Azure 9: crear jerarquías | Descripción de Microsoft Docs": servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-9-create-hierarchies"></a>Lección 9: Creación de jerarquías

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, creará jerarquías. Las jerarquías son grupos de columnas dispuestas en niveles; por ejemplo, una jerarquía geografía puede tener subniveles de país, estado, provincia y ciudad. Jerarquías pueden aparecer por separado de otras columnas en una lista de campos de aplicación de cliente informes, facilitando de cliente a los usuarios toonavigate e incluya en un informe. más información, consulte toolearn [jerarquías](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
las jerarquías de toocreate, use el Diseñador de modelo de Hola de *vista de diagrama*. La creación y la administración de jerarquías no se admiten en vista de datos.  
  
Estimado toocomplete de tiempo en esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 8: crear perspectivas](../tutorials/aas-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Creación de jerarquías  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a>una jerarquía de categorías en la tabla DimProduct de hello toocreate  
  
1.  En el Diseñador de modelos de hello (vista de diagrama), haga clic en hello **DimProduct** tabla > **crear jerarquía**. Aparece una nueva jerarquía final Hola de ventana de la tabla de Hola. Cambiar el nombre de la jerarquía de hello **categoría**.  
  
2.  Haga clic y arrastre hello **ProductCategoryName** toohello de columna nuevo **categoría** jerarquía.  
  
3.  Hola **categoría** jerarquía, contextual hello **ProductCategoryName** > **cambiar el nombre de**y, a continuación, escriba **categoría**.  
  
    > [!NOTE]  
    > Cambiar el nombre de una columna en una jerarquía no cambiar el nombre de esa columna en tabla Hola. Una columna de una jerarquía es simplemente una representación de la columna de hello en la tabla de Hola.  
  
4.  Haga clic y arrastre hello **ProductSubcategoryName** columna toohello **categoría** jerarquía. Cambie su nombre por **Subcategoría**. 
  
5.  Menú contextual hello **ModelName** columna > **agregar toohierarchy**y, a continuación, seleccione **categoría**. Cambie su nombre por **Modelo**.

6.  Por último, agregue **EnglishProductName** toohello jerarquía de categorías. Cambie su nombre por **Producto**.  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a>jerarquías de toocreate en la tabla DimDate de Hola  
  
1.  Hola **DimDate** de tabla, cree una jerarquía denominada **calendario**.  
  
3.  Agregue Hola siguiendo en orden de columnas:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  Hola **DimDate** de tabla, cree un **Fiscal** jerarquía. Hola siguiendo en orden de columnas se incluyen:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Por último, en hello **DimDate** de tabla, cree un **ProductionCalendar** jerarquía. Hola siguiendo en orden de columnas se incluyen:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>Pasos siguientes
[Lección 10: Creación de particiones](../tutorials/aas-lesson-10-create-partitions.md) 
  
  
