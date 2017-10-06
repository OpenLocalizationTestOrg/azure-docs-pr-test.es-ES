---
título: aaa "lección tutorial de Analysis Services de Azure 12: analizar en Excel | Descripción de Microsoft Docs": describe cómo toouse analizar en Excel en hello Azure Analysis Services proyecto tutorial. servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-12-analyze-in-excel"></a>Lección 12: Analizar en Excel

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, usar hello analizar en Excel característica tooopen Microsoft Excel, crear automáticamente un área de trabajo del modelo de toohello de conexión y agregar automáticamente una hoja de cálculo de toohello de tabla dinámica. Hola analizar esta característica está pensado tooprovide una eficacia de hello tootest de manera rápida y sencilla del modelo de diseño anterior toodeploying el modelo. En esta lección no se realizan análisis de datos. propósito de Hola de esta lección es toofamiliarize, crear modelo hello, con herramientas de hello puede utilizar tootest el diseño del modelo.   
  
toocomplete en esta lección, Excel debe instalarse en hello mismo equipo que SSDT.
  
Estimado toocomplete de tiempo en esta lección: **cinco minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 11: crear roles](../tutorials/aas-lesson-11-create-roles.md).  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a>Examinar con perspectivas de hello predeterminada y venta por Internet  
En estas primeras tareas, examinar el modelo mediante el uso de ambos perspectiva predeterminada hello, que incluye todos los objetos del modelo, y también mediante el uso de la perspectiva de ventas por Internet de Hola que anteriormente. Hola perspectiva venta por Internet excluye el objeto de tabla de cliente de Hola.  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a>toobrowse con perspectiva predeterminada de Hola  
  
1.  Haga clic en hello **modelo** menú > **analizar en Excel**.  
  
2.  Hola **analizar en Excel** cuadro de diálogo, haga clic en **Aceptar**.  
  
    Excel se abre con un nuevo libro. Se crea una conexión de origen de datos mediante la cuenta de usuario actual de Hola y Hola perspectiva predeterminada es campos visibles toodefine usado. Una tabla dinámica se agrega automáticamente la hoja de cálculo toohello.  
  
3.  En Excel, en hello **lista de campos de tabla dinámica**, observe hello **DimDate** y **FactInternetSales** aparecen los grupos de medida. Hola **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, y **FactInternetSales** también aparezcan las tablas con sus respectivas columnas.  
  
4.  Cierre Excel sin guardar el libro de Hola.  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a>toobrowse con hello perspectiva de ventas por Internet  
  
1.  Haga clic en hello **modelo** menú y, a continuación, haga clic en **analizar en Excel**.  
  
2.  Hola **analizar en Excel** cuadro de diálogo, deje **usuario de Windows actual** seleccionado, a continuación, en hello **perspectiva** cuadro de lista desplegable, seleccione **venta por Internet** y, a continuación, haga clic en **Aceptar**. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  En Excel, en **PivotTable Fields**, observe la tabla DimCustomer de Hola se excluye de la lista de campos de Hola.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Cierre Excel sin guardar el libro de Hola.  
  
## <a name="browse-by-using-roles"></a>Examinar mediante roles  
Los roles son una parte importante de los modelos tabulares. Sin al menos un rol toowhich usuarios se agregarán como miembros, los usuarios no se pueden tener acceso a y analizar datos con el modelo. Hola analizar esta característica proporciona una manera de roles de hello tootest que ha definido.  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a>toobrowse mediante el uso de rol de usuario de administrador de ventas de Hola  
  
1.  En SSDT, haga clic en hello **modelo** menú y, a continuación, haga clic en **analizar en Excel**.  
  
2.  En **especificar Hola nombre o rol toouse tooconnect toohello modelo de usuario**, seleccione **rol**y, a continuación, en el cuadro de lista desplegable de hello, seleccione **jefa de ventas**y, a continuación, haga clic en  **Aceptar**.  
  
    Excel se abre con un nuevo libro. Automáticamente se crea una tabla dinámica. Hola lista de campos de tabla dinámica incluye todos los campos de datos de hello disponibles en el nuevo modelo.  
      
3.  Cierre Excel sin guardar el libro de Hola.  
  
## <a name="whats-next"></a>Pasos siguientes
Vaya toohello siguiente lección: [lección 13: implementar](../tutorials/aas-lesson-13-deploy.md).

  
  
  
