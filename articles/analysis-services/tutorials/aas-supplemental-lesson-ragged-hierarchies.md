---
título: aaa "lección complementaria tutorial de Analysis Services de Azure: jerarquías desiguales | Descripción de Microsoft Docs": describe cómo toofix jerarquías desiguales hello Azure tutorial de Analysis Services.
servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lección complementaria: Jerarquías desiguales

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección complementaria, resolverá un problema común que se produce al dinamizar en jerarquías que contienen valores en blanco (miembros) en distintos niveles. Un ejemplo de esto sería una organización donde un director de alto nivel tiene como subordinados directos a directores de departamento y a trabajadores que no son directores. O bien, las jerarquías geográficas formadas por país-región-ciudad, donde algunas ciudades no tienen un elemento primario de estado o provincia, como Washington D. C. o Ciudad del Vaticano. Cuando una jerarquía tiene miembros en blanco, a menudo desciende toodifferent o desigual, niveles.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

Los modelos tabulares en el nivel de compatibilidad de hello 1400 tienen más **ocultar miembros** propiedad para las jerarquías. Hola **predeterminado** configuración supone que no hay ningún miembro en blanco en cualquier nivel. Hola **ocultar miembros en blanco** configuración excluye los miembros en blanco de jerarquía de hello cuando agrega tooa tabla dinámica o informe.  
  
Estimado toocomplete de tiempo en esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Esta lección complementaria forma parte de un tutorial de modelado tabular. Antes de realizar tareas de hello en esta lección complementaria, deberá haber finalizado todas las lecciones anteriores o tiene un proyecto de modelo de ejemplo Adventure Works Internet Sales completado. 

Si ha creado el proyecto de hello AW Internet Sales como parte del tutorial de hello, el modelo no contiene aún los datos o jerarquías desiguales. toocomplete esta lección complementaria, primero tienes toocreate Hola problema agregando algunas tablas adicionales, crear una nueva jerarquía de organización, una medida, las columnas calculadas y relaciones. Solo tardará unos 15 minutos en hacerlo. A continuación, obtener toosolve en tan solo unos minutos.  

## <a name="add-tables-and-objects"></a>Agregar tablas y objetos
  
### <a name="tooadd-new-tables-tooyour-model"></a>nuevo modelo de tooyour tablas tooadd
  
1.  En el Explorador de modelos tabulares, expanda **Orígenes de datos** y haga clic con el botón derecho en la conexión > **Importar nuevas tablas**.
  
2.  En el navegador, seleccione **DimEmployee** y **FactResellerSales** y, después, haga clic en **Aceptar**.

3.  En el Editor de consultas, haga clic en **Importar**.

4.  Cree Hola siguiente [relaciones](../tutorials/aas-lesson-4-create-relationships.md):

    | Tabla 1           | Columna       | Dirección del filtro   | Tabla 2     | Columna      | Active |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Valor predeterminado            | DimDate     | Date        | Sí    |
    | FactResellerSales | DueDate      | Valor predeterminado            | DimDate     | Date        | No     |
    | FactResellerSales | ShipDateKey  | Valor predeterminado            | DimDate     | Date        | No     |
    | FactResellerSales | ProductKey   | Valor predeterminado            | DimProduct  | ProductKey  | Sí    |
    | FactResellerSales | EmployeeKey  | Tablas de tooBoth | DimEmployee | EmployeeKey | Sí    |

5. Hola **DimEmployee** de tabla, cree Hola siguiente [columnas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md): 

    **Ruta de acceso** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  Hola **DimEmployee** de tabla, cree un [jerarquía](../tutorials/aas-lesson-9-create-hierarchies.md) denominado **organización**. Agregar Hola siguiendo en orden de columnas: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  Hola **FactResellerSales** de tabla, cree Hola siguiente [medida](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Use [analizar en Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel y crear automáticamente una tabla dinámica.

9.  En **PivotTable Fields**, agregar hello **organización** jerarquía de hello **DimEmployee** tabla demasiado**filas**, hello y**ResellerTotalSales** medida de hello **FactResellerSales** tabla demasiado**valores**.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Como puede ver en la tabla dinámica de hello, jerarquía de hello muestra las filas que son desiguales. Hay muchas filas en las que se muestran miembros en blanco.

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a>Hola toofix jerarquía desigual estableciendo los miembros de ocultación de hello, propiedad

1.  En el **Explorador de modelos tabulares**, expanda **Tablas** > **DimEmployee** > **Jerarquías** > **Organización**.

2.  En **Propiedades** > **Ocultar miembros**, seleccione **Ocultar miembros en blanco**. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  En Excel, actualizar Hola tabla dinámica. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Ahora el aspecto es mucho mejor.

## <a name="see-also"></a>Otras referencias   
[Lección 9: Creación de jerarquías](../tutorials/aas-lesson-9-create-hierarchies.md)  
[Lección complementaria: Seguridad dinámica](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lección complementaria: Filas de detalles](../tutorials/aas-supplemental-lesson-detail-rows.md)  