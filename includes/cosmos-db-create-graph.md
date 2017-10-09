Ahora puede usar la herramienta de exploración de datos de Hola Hola toocreate portal Azure una base de datos del gráfico. 

1. Hola portal de Azure, en el menú de navegación izquierdo de hello, haga clic en **Explorador de datos (vista previa)**. 
2. Hola **Explorador de datos (vista previa)** hoja, haga clic en **nuevo gráfico**, a continuación, rellene la página de hello mediante Hola siguiente información.

    ![Explorador de datos en hello portal de Azure](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer.png)

    Configuración|Valor sugerido|Descripción
    ---|---|---
    Id. de base de datos|sample-database|Id. de Hello para la nueva base de datos. Los nombres de bases de datos deben tener entre 1 y 255 caracteres y no pueden contener `/ \ # ?` o un espacio al final.
    Graph id (Id. de grafo)|sample-graph|Id. de Hello para el nuevo gráfico. Los nombres de gráfico tienen Hola mismo carácter requisitos como identificadores de base de datos.
    Capacidad de almacenamiento| 10 GB|Deje el valor predeterminado de Hola. Se trata de capacidad de almacenamiento de Hola de base de datos de Hola.
    Rendimiento|400 RU|Deje el valor predeterminado de Hola. Se puede escalar el rendimiento de hello más tarde si desea que la latencia tooreduce.
    Clave de partición|/userid|Una clave de partición que se encargará de distribuir datos uniformemente tooeach partición. Seleccionar Hola correcto es importante en la creación de un rendimiento clave de partición del gráfico, obtenga más información acerca de él en [diseñar para la partición](../articles/cosmos-db/partition-data.md#designing-for-partitioning).

3. Una vez que se rellena el formulario de hello, haga clic en **Aceptar**.
