Ahora puede usar la colección y la herramienta de explorador de datos de Hola Hola toocreate portal Azure una base de datos. 

1. Hola portal de Azure, en el menú de navegación izquierdo de hello, haga clic en **Explorador de datos (vista previa)**. 

2. En hello **Explorador de datos (vista previa)** hoja, haga clic en **nueva colección**y, a continuación, proporcionar Hola siguiente información:

    ![Hola portal Azure, hoja de explorador de datos](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    Configuración|Valor sugerido|Descripción
    ---|---|---
    Id. de base de datos|Tareas|nombre de Hello para la nueva base de datos. Los nombres de base de datos tiene que tener entre 1 y 255 caracteres y no pueden contener /, \\; #, ?, o un espacio al final.
    Id. de colección|Elementos|nombre de Hello para la nueva colección. Nombres de la colección tienen Hola mismo requisitos como identificadores de base de datos de caracteres.
    Capacidad de almacenamiento| Fija (10 GB)|Usar valor predeterminado de Hola. Este valor es la capacidad de almacenamiento de Hola de base de datos de Hola.
    Rendimiento|400 RU|Usar valor predeterminado de Hola. Si desea tooreduce latencia, se puede escalar el rendimiento de hello más tarde.
    Clave de partición|/categoría|Una clave de partición que distribuye los datos uniformemente tooeach partición. Seleccionar clave de partición correcta de hello es importante en la creación de una colección de rendimiento. más información, consulte toolearn [diseñar para la partición](../articles/cosmos-db/partition-data.md#designing-for-partitioning).    
3. Después de haber completado el formulario de hello, haga clic en **Aceptar**.

Explorador de datos muestra Hola nueva base de datos y la colección. 
