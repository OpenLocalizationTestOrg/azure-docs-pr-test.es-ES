---
título: aaa "lección de Azure Analysis Services tutorial 1: crear un nuevo proyecto de modelo tabular | Descripción de Microsoft Docs": describe cómo toocreate un nuevo análisis Azure Services proyecto tutorial. servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''

MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 01/06/2017 ms.author: owend
---
# <a name="lesson-1-create-a-tabular-model-project"></a>Lección 1: Creación de un proyecto de modelo tabular

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, utilizará toocreate un nuevo proyecto de modelos tabulares de SQL Server Data Tools (SSDT) Hola 1400 el nivel de compatibilidad. Una vez creado el proyecto, puede empezar a agregar datos y a crear el modelo. En esta lección también se ofrece una breve introducción toohello creación de modelos tabulares entorno en SSDT.  
  
Estimado toocomplete de tiempo en esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es la primera lección de hello en un tutorial de creación de modelos tabulares. toocomplete esta lección, hay varios requisitos previos que necesita toohave in situ. más información, consulte toolearn [Azure Analysis Services - tutorial de Adventure Works](../tutorials/aas-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Crear un proyecto de modelo tabular  
  
#### <a name="toocreate-a-new-tabular-model-project"></a>toocreate un nuevo proyecto de modelo tabular  
  
1.  En SSDT, en hello **archivo** menú, haga clic en **New** > **proyecto**.  
  
2.  Hola **nuevo proyecto** cuadro de diálogo, expanda **instalado** > **Business Intelligence** > **deAnalysisServices**y, a continuación, haga clic en **proyecto Tabular de Analysis Services**.  
  
3.  En **nombre**, tipo **AW Internet Sales**y, a continuación, especifique una ubicación para los archivos de proyecto de Hola.  
  
    De forma predeterminada, **nombre de la solución** Hola igual como nombre del proyecto Hola; sin embargo, puede escribir un nombre de solución diferente.  
  
4.  Haga clic en **Aceptar**.  
  
5.  Hola **Diseñador de modelos tabulares** cuadro de diálogo, seleccione **área de trabajo integrado**.  
  
    área de trabajo de Hello hospeda una base de datos de modelo tabular con hello mismo nombre como proyecto de Hola durante la creación del modelo. Área de trabajo integrado significa que SSDT usa una instancia integrada, lo que elimina la necesidad de hello tooinstall una instancia de servidor de Analysis Services independiente solo para la creación de modelos.
      
6.  En **nivel de compatibilidad**, seleccione **SQL Server 2017 / Azure Analysis Services (1400)**.   
 
    ![aas-lesson1-tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    Si no ve 2017 / Azure Analysis Services de SQL Server (1400) en el cuadro de lista de nivel de compatibilidad hello, no está utilizando la versión más reciente de Hola de SQL Server Data Tools. versión más reciente de tooget hello, consulte [instalar SQL Server Data tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-hello-ssdt-tabular-model-authoring-environment"></a>Descripción de los modelos tabulares de hello SSDT entorno de creación  
Ahora que ha creado un nuevo proyecto de modelo tabular, dedique un momento tooexplore Hola creación de modelos tabulares entorno en SSDT.  
  
Una vez creado el proyecto, se abrirá en SSDT. En hello a la derecha, en **Explorador de modelos tabulares**, verá una vista de árbol de objetos de hello en el modelo. Puesto que aún no ha importado datos, carpetas de hello están vacías. Puede hacer clic un objeto acciones de carpeta tooperform, barra de menús de toohello similar. Paso a paso a través de este tutorial, utilice toonavigate diferentes objetos de explorador de modelos tabulares de hello en el proyecto de modelos.

![aas-lesson1-tme](../tutorials/media/aas-lesson1-tme.png)

Haga clic en hello **el Explorador de soluciones** ficha. Aquí se encuentra el archivo **Model.bim**. Si no ve izquierda toohello de hello ventana del diseñador (Hola ventana vacía con pestaña de hello Model.bim), en **el Explorador de soluciones**, en **AW Internet Sales proyecto**, haga doble clic en hello  **Model.BIM** archivo. archivo Model.bim de Hello contiene metadatos de hello para el proyecto de modelos. 

![aas-lesson1-se](../tutorials/media/aas-lesson1-se.png)
  
Haga clic en **Model.bim**. Hola **propiedades** ventana, verá las propiedades de modelo de hello, más importantes que es hello **Directquerymode** propiedad. Esta propiedad especifica si se implementa el modelo de hello en modo In-Memory (Off) o en modo de DirectQuery (activado). En este tutorial se crea y se implementa el modelo en modo en memoria.

![aas-lesson1-properties](../tutorials/media/aas-lesson1-properties.png)
  
Cuando crea un proyecto de modelo, algunas propiedades del modelo se establecen automáticamente según toohello valores de modelado de datos que se pueden especificar en hello **herramientas** menú > **opciones** cuadro de diálogo. Propiedades del servidor de área de trabajo, retención de área de trabajo y copia de seguridad de datos especifican cómo y dónde base de datos del área de trabajo de hello (la base de datos de creación de modelos) copia de seguridad, conserva en memoria y compilado. Si es necesario, puede cambiar estas opciones más adelante, pero de momento las dejaremos tal como están.  

En el **Explorador de soluciones**, haga clic con el botón derecho en **Ventas por Internet AW** (proyecto) y haga clic en **Propiedades**. Hola **páginas de propiedades de ventas de Internet de AW** aparece el cuadro de diálogo. Al implementar el modelo más adelante, se establecen algunas de estas propiedades.  
  
Al instalar SSDT, varios elementos de menú nuevos se agregaron toohello entorno de Visual Studio. Haga clic en hello **modelo** menú. Desde aquí, puede importar datos, actualizar los datos del área de trabajo, examinar el modelo en Excel, crear perspectivas y roles, vista de modelo de hello seleccione y establecer las opciones de cálculo. Haga clic en hello **tabla** menú. Desde aquí puede crear y administrar las relaciones, especificar la configuración de las tablas de fecha, crear particiones y editar las propiedades de las tablas. Si hace clic en hello **columna** menú, puede agregar y eliminar columnas de una tabla, Inmovilizar columnas y especificar el criterio de ordenación. SSDT también agrega algunas barras de toohello de botones. Hola Autosuma característica toocreate una medida de agregación estándar para una columna seleccionada es más útil. Otros botones de barra de herramientas proporcionan acceso rápido toofrequently usa características y comandos.  
  
Explore algunos de los cuadros de diálogo de Hola y ubicaciones para diversos modelos de tabulares tooauthoring específicos de características. Aunque algunos elementos aún no están activos, puede obtener una idea del entorno de creación de modelos tabulares de Hola.  
  

## <a name="whats-next"></a>Pasos siguientes
[Lección 2: Obtención de datos](../tutorials/aas-lesson-2-get-data.md)

  
  
  
