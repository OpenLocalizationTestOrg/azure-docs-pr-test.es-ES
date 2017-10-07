---
title: "una base de datos del gráfico de base de datos de Azure Cosmos con Java aaaCreate | Documentos de Microsoft"
description: "Presenta una Java código de ejemplo que puede usar datos de gráfico de consultas de tooconnect tooand en la base de datos de Azure Cosmos con Gremlin."
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB: Crear una base de datos de gráfico con Java y Hola portal de Azure

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente. 

Este tutorial crea un gráfico de base de datos mediante Hola herramientas del portal Azure para la base de datos de Azure Cosmos. Este tutorial rápido muestra también cómo tooquickly crear una aplicación de consola de Java con una base de datos de gráfico con sistemas operativos de hello [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) controlador. instrucciones de Hello en este tutorial rápido se pueden aplicar en cualquier sistema operativo que sea capaz de ejecutar Java. Este inicio rápido le ayudará a familiarizarse con la creación y modificación de los recursos de gráfico en hello interfaz de usuario o mediante programación, lo que sea su preferencia. 

## <a name="prerequisites"></a>Requisitos previos

* [Kit de desarrollo de Java (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * En Ubuntu, ejecute `apt-get install default-jdk` tooinstall Hola JDK.
    * Ser seguro tooset Hola JAVA_HOME entorno variable toopoint toohello carpeta donde está instalado Hola JDK.
* [Descargar](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) un archivo binario de [Maven](http://maven.apache.org/)
    * En Ubuntu, se pueden ejecutar `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * En Ubuntu, se pueden ejecutar `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

Antes de poder crear una base de datos del gráfico, debe toocreate una cuenta de base de datos Gremlin (gráfico) con la base de datos de Azure Cosmos.

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Agregar un grafo

Ahora puede usar la herramienta de exploración de datos de Hola Hola toocreate portal Azure una base de datos del gráfico. 

1. Hola portal de Azure, en el menú de navegación izquierdo de hello, haga clic en **Explorador de datos (vista previa)**. 
2. Hola **Explorador de datos (vista previa)** hoja, haga clic en **nuevo gráfico**, a continuación, rellene la página de hello mediante Hola siguiente información:

    ![Explorador de datos en hello portal de Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    Configuración|Valor sugerido|Descripción
    ---|---|---
    Identificador de base de datos|sample-database|Id. de Hello para la nueva base de datos. Los nombres de bases de datos deben tener entre 1 y 255 caracteres y no pueden contener `/ \ # ?` o un espacio al final.
    Identificador de grafo|sample-graph|Id. de Hello para el nuevo gráfico. Los nombres de gráfico tienen Hola mismo carácter requisitos como identificadores de base de datos.
    Capacidad de almacenamiento| 10 GB|Deje el valor predeterminado de Hola. Se trata de capacidad de almacenamiento de Hola de base de datos de Hola.
    Rendimiento|400 RU|Deje el valor predeterminado de Hola. Se puede escalar el rendimiento de hello más tarde si desea que la latencia tooreduce.
    Clave de partición|Déjelo en blanco|A fin de Hola de este tutorial rápido, deje en blanco clave de partición de Hola.

3. Una vez que se rellena el formulario de hello, haga clic en **Aceptar**.

## <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Ahora vamos a clonar una aplicación de gráfico de github, establezca la cadena de conexión de Hola y ejecútelo. Vea lo fácil que es toowork con datos mediante programación. 

1. Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.  

2. Ejecute hello después de repositorio de ejemplo de comando tooclone Hola. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Revise el código de hello

Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello. Abra hello `Program.java` archivo de hello \src\GetStarted carpeta y busque las siguientes líneas de código. 

* Hola Gremlin `Client` se inicializa desde la configuración de hello en `src/remote.yaml`.

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* Una serie de pasos de Gremlin se ejecutan utilizando hello `client.submit` método.

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

1. Archivo de src/remote.yaml de hello abierto. 

3. Rellene la *hosts*, *nombre de usuario*, y *contraseña* valores en el archivo de hello src/remote.yaml. resto de Hola de configuración de hello no es necesario toobe cambiado.

    Configuración|Valor sugerido|Descripción
    ---|---|---
    Hosts|[***.graphs.azure.com]|Consulte la captura de pantalla de hello sigue a esta tabla. Este valor es el valor de URI Gremlin de hello en la página de información general de Hola de hello portal de Azure, entre corchetes, con hello finales: 443 / quitado.<br><br>Este valor también puede obtenerse de la pestaña de claves de hello, utilizando el valor URI de hello quitar https://, cambiar toographs de documentos y quitando finales Hola: 443 /.
    Nombre de usuario|/dbs/sample-database/colls/sample-graph|Hola recursos de formulario de hello `/dbs/<db>/colls/<coll>` donde `<db>` es el nombre de base de datos existente y `<coll>` es el nombre de la colección existente.
    Password|*Su clave maestra principal*|Vea Hola segunda captura de pantalla sigue a esta tabla. Este valor es la clave principal, que puede recuperar de la página de claves de Hola de portal de Azure, en el cuadro de la clave principal de Hola Hola. Copiar valor de hello usando Hola copia botón Hola derecha del cuadro de Hola.

    Para el valor de Hosts de hello, copie hello **Gremlin URI** valor de hello **Introducción** página. Si está vacía, consulte las instrucciones de Hola de fila de Hosts de Hola Hola tabla sobre la creación de hello Gremlin URI de la hoja de claves de hello anterior.
![Visualizar y copiar valor de URI Gremlin de hello en la página de información general de Hola Hola portal de Azure](./media/create-graph-java/gremlin-uri.png)

    Para el valor de la contraseña de hello, copie hello **clave principal** de hello **claves** hoja: ![visualizar y copiar las claves de la clave principal en hello portal de Azure, página](./media/create-graph-java/keys.png)

## <a name="run-hello-console-app"></a>Ejecutar la aplicación de consola de hello

1. En la ventana de terminal de git hello, `cd` toohello azure-cosmos-db-graph-java-getting-started carpeta.

2. En la ventana de terminal de git hello, escriba `mvn package` tooinstall Hola necesario paquetes de Java.

3. En la ventana de terminal de git hello, ejecute `mvn exec:java -D exec.mainClass=GetStarted.Program` en Hola ventana de terminal toostart la aplicación de Java.

ventana de terminal de Hello muestra vértices Hola añadidos toohello gráfico. Una vez que finalice el programa de hello, cambiar atrás toohello portal de Azure en el Explorador de internet. 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a>Revise y agregue datos de ejemplo

Ahora puede volver atrás tooData explorador y vea vértices Hola agregan toohello gráfico y agregar puntos de datos adicionales.

1. En el Explorador de datos, expanda hello **base de datos de ejemplo**/**gráfico de ejemplo**, haga clic en **gráfico**y, a continuación, haga clic en **aplicar filtro**. 

   ![Crear nuevos documentos en el Explorador de datos en hello portal de Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. Hola **resultados** lista, tenga en cuenta los nuevos usuarios de hello agregan toohello gráfico. Seleccione **ben** y observe que ha conectado toorobin. Puede moverse vértices hello en el Explorador de gráficos de hello, acercar y alejar y expandir el tamaño de la superficie del explorador de gráfico de Hola Hola. 

   ![Nueva vértices en gráfico hello en el Explorador de datos Hola portal de Azure](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. Vamos a agregar unos nuevo gráfico toohello de los usuarios mediante Hola Explorador de datos. Haga clic en hello **nuevo vértice** gráfico de botón tooadd datos tooyour.

   ![Crear nuevos documentos en el Explorador de datos en hello portal de Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. Escriba una etiqueta de *persona* , a continuación, escriba Hola siguiente claves y valores toocreate Hola primer vértice gráfico Hola. Tenga en cuenta que puede crear propiedades únicas para cada persona en el grafo. Solo Hola identificador clave es obligatoria.

    key|value|Notas
    ----|----|----
    id|ashley|Identificador único de Hola de vértice Hola. Si no se especifica un identificador, se genera uno automáticamente.
    gender|mujer| 
    técnico | Java | 

    > [!NOTE]
    > En este tutorial rápido se crea una colección sin particiones. Sin embargo, si crea una colección con particiones mediante la especificación de una clave de partición durante la creación de la colección de hello, necesita clave de partición de hello tooinclude como una clave en cada nuevo vértice. 

5. Haga clic en **Aceptar**. Puede que necesite tooexpand su toosee pantalla **Aceptar** en la parte inferior de Hola de pantalla de bienvenida.

6. Haga clic en **Nuevo vértice** de nuevo y agregue otro usuario. Escriba una etiqueta de *persona* escriba Hola siguiente claves y valores:

    key|value|Notas
    ----|----|----
    id|rakesh|Identificador único de Hola de vértice Hola. Si no se especifica un identificador, se genera uno automáticamente.
    gender|hombre| 
    centro educativo|MIT| 

7. Haga clic en **Aceptar**. 

8. Haga clic en **aplicar filtro** no tiene valor predeterminado de hello `g.V()` filtro. Todos los usuarios de hello muestran ahora en hello **resultados** lista. Si agrega más datos, puede usar filtros toolimit los resultados. De forma predeterminada, usa el Explorador de datos `g.V()` tooretrieve todos los vértices en un gráfico, pero pueden cambiar ese tooa diferentes [consulta graph](tutorial-query-graph.md), como `g.V().count()`, tooreturn un recuento de todos los vértices de hello en el gráfico de hello en formato JSON.

9. Ahora podemos conectar a rakesh y ashley. Asegúrese de **Ana** en seleccionado en hello **resultados** lista, a continuación, haga clic en botón de edición de hello siguiente demasiado**destinos** en la parte inferior derecha. Puede que necesite toowiden su Hola de ventana toosee **propiedades** área.

   ![Cambiar el destino de Hola de un vértice en un gráfico](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. Hola **destino** cuadro, escriba *rakesh*y en hello **etiqueta de borde** cuadro, escriba *sabe*y, a continuación, haga clic en la casilla de verificación de Hola.

   ![Adicion de una conexión entre ashley y rakesh en el Explorador de datos](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. Ahora seleccione **rakesh** desde la lista de resultados de Hola y vea que Ana y rakesh están conectados. 

   ![Dos vértices conectados en el Explorador de datos](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    También puede usar procedimientos de explorador de datos toocreate almacenado, UDF y lógica de negocios de servidor de tooperform de desencadenadores, así como el rendimiento de escala. Explorador de datos expone todo acceso a los datos de mediante programación integrada Hola disponible en las API de hello, pero proporciona un acceso sencillo tooyour datos Hola portal de Azure.



## <a name="review-slas-in-hello-azure-portal"></a>Revise los SLA de hello portal de Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos: 

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo crear un gráfico utilizando Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación. Ahora puede crear consultas más complejas e implementar con Gremlin una lógica eficaz de recorrido del grafo. 

> [!div class="nextstepaction"]
> [Consulta mediante Gremlin](tutorial-query-graph.md)

