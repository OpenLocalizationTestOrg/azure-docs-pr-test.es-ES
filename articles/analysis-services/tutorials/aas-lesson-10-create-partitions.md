---
título: aaa "lección tutorial de Analysis Services de Azure 10: crear particiones | Descripción de Microsoft Docs": describe cómo toocreate particiones en el proyecto tutorial de hello Azure Analysis Services. servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-10-create-partitions"></a>Lección 10: Creación de particiones

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, creará la tabla de particiones toodivide hello FactInternetSales en piezas lógicas más pequeñas que pueden ser procesado independiente (actualizar) de las demás particiones. De forma predeterminada, cada tabla que se incluye en el modelo tiene una partición, lo que incluye la tabla Hola todas las columnas y filas. Para la tabla FactInternetSales de hello, queremos que los datos de hello toodivide por año; una partición para cada uno de los cinco años de la tabla de Hola. Así, cada partición se podrá procesar de manera independiente. más información, consulte toolearn [particiones](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular). 
  
Estimado toocomplete de tiempo en esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 9: crear jerarquías](../tutorials/aas-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Creación de particiones  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a>toocreate particiones de tabla de hello FactInternetSales  
  
1.  En el Explorador de modelos tabulares, expanda **Tablas** y haga clic con el botón derecho en **FactInternetSales** > **Particiones**.  
  
2.  En el Administrador de particiones, haga clic en **copia**y, a continuación, cambiar nombre de hello demasiado**FactInternetSales2010**.
  
    Porque desea Hola partición tooinclude sólo aquellas filas en un período determinado, para el año 2010, de hello debe modificar la expresión de consulta de Hola.
  
4.  Haga clic en **diseño** tooopen Editor de consultas y, a continuación, haga clic en hello **FactInternetSales2010** consulta.

5.  En la vista previa, haga clic en hello flecha abajo en hello **OrderDate** encabezado de columna y, a continuación, haga clic en **filtros de fecha y hora** > **entre**.

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  En el cuadro de diálogo Filtrar filas de hello, en **mostrar filas donde: OrderDate**, deje **es posterior o igual a**y, a continuación, en el campo de fecha de hello, escriba **1/1/2010**. Deje hello **y** operador seleccionado, a continuación, seleccione **antes**, a continuación, en el campo de fecha de hello, escriba **/1/1/2011**y, a continuación, haga clic en **Aceptar**.

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    Observe que en PASOS APLICADOS del Editor de consultas encontrará otro paso denominado Filas filtradas. Este filtro es tooselect solo las fechas de pedidos de 2010.

8.  Haga clic en **Import**.

    En el Administrador de particiones, tenga en cuenta consulta Hola expresión ahora tiene una cláusula de filtrado de filas adicional.

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    Esta instrucción especifica que esta partición debe incluir solo datos de hello en las filas donde hello OrderDate es Hola año 2010 tal como se especifica en la cláusula de filtrado de filas de Hola.  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a>toocreate una partición para hello año 2011  
  
1.  En la lista de particiones de hello, haga clic en hello **FactInternetSales2010** de partición que creó y, a continuación, haga clic en **copia**.  Cambiar el nombre de la partición de hello demasiado**FactInternetSales2011**. 

    No es necesario toouse Editor de consultas toocreate una nueva cláusula de filtrado de filas. Porque se ha creado una copia de la consulta de Hola para 2010, todo lo que necesita toodo es realizar un pequeño cambio en consulta Hola de 2011.
  
2.  En **expresión de consulta**, en orden para esta partición tooinclude sólo aquellas filas para hello año 2011, reemplace los años Hola de cláusula de filtrado de filas de hello tiene **2011** y **2012**, respectivamente, al igual que:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a>particiones de toocreate de 2012, 2013 y 2014.  
  
- Siga los pasos anteriores hello, creación de particiones de 2012, 2013 y 2014, cambiar años de hello en hello filtrar filas cláusula tooinclude solo las filas correspondientes a ese año. 
  

## <a name="delete-hello-factinternetsales-partition"></a>Eliminar hello FactInternetSales partición
Ahora que tiene particiones para cada año, puede eliminar la partición de hello FactInternetSales; al elegir todos los procesos cuando el procesamiento de particiones, que impiden que se superponen.

#### <a name="toodelete-hello-factinternetsales-partition"></a>Hola toodelete FactInternetSales partición
-  Haga clic en hello FactInternetSales partición y, a continuación, haga clic en **eliminar**.



## <a name="process-partitions"></a>Procesar las particiones  
En el Administrador de particiones, tenga en cuenta hello **procesa última** columna para cada una de las nuevas particiones Hola creaste muestra estas particiones nunca se han procesado. Al crear particiones, se deben ejecutar un procesar particiones o datos de tabla de proceso operación toorefresh hello en esas particiones.  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a>tooprocess Hola FactInternetSales particiones  
  
1.  Haga clic en **Aceptar** tooclose Administrador de particiones.  
  
2.  Haga clic en hello **FactInternetSales** de tabla, a continuación, haga clic en hello **modelo** menú > **proceso** > **procesar particiones**.  
  
3.  En el cuadro de diálogo procesar particiones de hello, compruebe **modo** se establece demasiado**proceso predeterminado**.  
  
4.  Active la casilla de verificación de Hola Hola **proceso** columna para cada uno de hello cinco particiones que ha creado y, a continuación, haga clic en **Aceptar**.  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    Si se le pide las credenciales de suplantación, escriba el nombre de usuario de Windows hello y la contraseña que especificó en la lección 2.  
  
    Hola **procesamiento de datos** cuadro de diálogo aparece y muestra los detalles del proceso para cada partición. Tenga en cuenta que se transfiere un número de filas diferente para cada partición. Cada partición incluye solamente las filas para el año de hello especificado en la cláusula WHERE de la instrucción SQL Hola Hola. Cuando finalice el procesamiento, continúe y cerrar el cuadro de diálogo de procesamiento de datos de Hola.  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>Pasos siguientes
Vaya toohello siguiente lección: [lección 11: crear Roles](../tutorials/aas-lesson-11-create-roles.md). 
