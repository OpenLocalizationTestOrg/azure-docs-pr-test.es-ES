---
título: aaa "lección tutorial de Analysis Services de Azure 7: crear indicadores clave de rendimiento | Descripción de Microsoft Docs": describe cómo toocreate los indicadores clave de rendimiento en Hola proyecto tutorial de Analysis Services de Azure. servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend
---
# <a name="lesson-7-create-key-performance-indicators"></a>Lección 7: Creación de indicadores clave de rendimiento

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, creará indicadores clave de rendimiento (KPI). Los KPI son utilizados toogauge rendimiento de un valor definido por una *Base* medida, con un *destino* valor también se define una medida o un valor absoluto. En aplicaciones cliente de informes, los KPI pueden proporcionar a los profesionales de negocios un toounderstand de manera rápida y sencilla un resumen de las tendencias empresariales de éxito o tooidentify. más información, consulte toolearn [KPI](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
Estimado toocomplete de tiempo en esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 6: crear medidas](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Creación de indicadores clave de rendimiento  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a>un KPI InternetCurrentQuarterSalesPerformance toocreate  
  
1.  En el Diseñador de modelos de hello, haga clic en hello **FactInternetSales** tabla.  
  
2.  En la cuadrícula de medidas de hello, haga clic en una celda vacía.  
  
3.  En la barra de fórmulas de hello, encima de la tabla hello, escriba Hola siguiente fórmula: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Esta medida actúa como medida Base Hola Hola KPI.  
  
4.  Haga clic en **InternetCurrentQuarterSalesPerformance** > **Crear KPI**.   
  
5.  En el cuadro de diálogo del indicador clave de rendimiento (KPI) de hello en **destino** seleccione **valor absoluto**y, a continuación, escriba **1.1**.  
  
7.  En el campo de control deslizante (baja) izquierdo hello, escriba **1**y, a continuación, en el control deslizante de hello derecha (alto), escriba **1.07**.  
  
8.  En **Seleccionar estilo de icono**, Hola rombo (rojo), triángulo (amarillo), círculo tipo de icono (verde).
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Hola aviso expandible **descripciones** etiqueta debajo de los estilos de icono disponibles Hola. Usar descripciones para saludo diversos toomake de elementos KPI ellos más fáciles de identificar en las aplicaciones cliente.  
  
9. Haga clic en **Aceptar** toocomplete Hola KPI.  
  
    En la cuadrícula de medidas de hello, tenga en cuenta Hola icono siguiente toohello **InternetCurrentQuarterSalesPerformance** medida. Este icono indica que esta medida sirve como un valor base para un KPI.  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a>un KPI InternetCurrentQuarterMarginPerformance toocreate  
  
1.  En la cuadrícula de medidas de Hola de hello **FactInternetSales** de tabla, haga clic en una celda vacía.  
  
2.  En la barra de fórmulas de hello, encima de la tabla hello, escriba Hola siguiente fórmula:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Haga clic con el botón derecho en **InternetCurrentQuarterMarginPerformance** > **Crear KPI**.  
  
4.  En el cuadro de diálogo del indicador clave de rendimiento (KPI) de hello en **destino** seleccione **valor absoluto**y, a continuación, escriba **1.25**.   
  
5.  En el campo de control deslizante (baja) izquierdo hello, deslice hasta que muestre el campo de hello **0,8**, Hola de diapositiva, a continuación, este campo de control deslizante (alto), hasta que muestre el campo de Hola y **1.03**.  
  
6.  En **Seleccionar estilo de icono**, seleccione el rombo de hello (rojo), triángulo (amarillo), el tipo de icono de círculo (verde) y, a continuación, haga clic en **Aceptar**.  
  
## <a name="whats-next"></a>Pasos siguientes
[Lección 8: Creación de perspectivas](../tutorials/aas-lesson-8-create-perspectives.md)
  
  
