---
título: aaa "lección de Azure Analysis Services tutorial 3: marcar como tabla de fechas | Descripción de Microsoft Docs": describe cómo toomark tabla de una fecha en el proyecto tutorial de hello Azure Analysis Services. servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 01/06/2017 ms.author: owend
---
# <a name="lesson-3-mark-as-date-table"></a>Lección 3: Marcar como tabla de fechas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En la lección 2: Obtención de datos, importó una tabla de dimensiones denominada DimDate. Mientras que en su modelo esta tabla se denomina DimDate, también se conoce como *tabla de fechas* porque contiene datos de fecha y hora.  
  
Cada vez que se usan funciones de inteligencia de tiempo de DAX, igual que hará cuando cree medidas un poco más tarde, debe especificar propiedades que incluyan una *tabla de fechas* y un identificador único de *columna de fecha* en esa tabla.
  
En esta lección, se marca la tabla de DimDate de hello como hello *tabla de fechas* y la columna de fecha de hello (en la tabla de fechas de hello) como hello *columna de fecha* (identificador único).  

Antes de marcar la columna de tabla y la fecha de la fecha de hello, es un toodo buen momento un poco de limpieza toomake su toounderstand sea más fácil de modelo. Observe que en la tabla de hello DimDate una columna denominada **FullDateAlternateKey**. Esta columna contiene una fila por cada día de cada año de calendario incluido en la tabla de Hola. Esta columna se usa mucho en las fórmulas de medida y los informes. Sin embargo, FullDateAlternateKey no es realmente un buen identificador en esta columna. Cámbiele demasiado**fecha**, lo que sea más fácil tooidentify e incluir en las fórmulas. Siempre que sea posible, es una buena idea toorename objetos como tablas y columnas toomake les sea más fácil tooidentify en SSDT y las aplicaciones como Power BI y Excel de informes. 
  
Estimado toocomplete de tiempo en esta lección: **tres minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 2: obtener datos](../tutorials/aas-lesson-2-get-data.md). 

### <a name="toorename-hello-fulldatealternatekey-column"></a>columna de toorename hello FullDateAlternateKey

1.  En el Diseñador de modelos de hello, haga clic en hello **DimDate** tabla.

2.  Haga doble clic en el encabezado de Hola para hello **FullDateAlternateKey** columna y, a continuación, cambie su nombre demasiado**fecha**.

  
### <a name="tooset-mark-as-date-table"></a>tooset marcar como tabla de fechas  
  
1.  Seleccione hello **fecha** columna y, a continuación, en hello **propiedades** ventana, en **tipo de datos**, asegúrese de que **fecha** está seleccionada.  
  
2.  Haga clic en hello **tabla** menú, a continuación, haga clic en **fecha**y, a continuación, haga clic en **marcar como tabla de fechas**.  
  
3.  Hola **marcar como tabla de fechas** cuadro de diálogo hello **fecha** cuadro de lista, seleccione hello **fecha** columna como identificador único de Hola. Normalmente se selecciona de forma predeterminada. Haga clic en **Aceptar**. 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>Pasos siguientes
[Lección 4: Creación de relaciones](../tutorials/aas-lesson-4-create-relationships.md).
  
