---
título: aaa "Tutorial: crear el primer índice de búsqueda de Azure en el portal de hello | Descripción de Microsoft Docs": Hola portal de Azure, utilice predefinidos toogenerate de datos de ejemplo un índice. Explore la búsqueda de texto completo, los filtros, las facetas, la búsqueda aproximada, la búsqueda geográfica y más.
servicios: buscar documentationcenter: '' autor: HeidiSteen manager: jhubbard editor: '' etiquetas: portal de azure

MS.AssetId: 21adc351-69bb-4a39-bc59-598c60c8f958 ms.service: buscar ms.devlang: na ms.workload: buscar ms.topic: artículo héroe ms.tgt_pltfrm: na ms.date: 26/06/2017 ms.author: heidist

---
# <a name="tutorial-create-your-first-azure-search-index-in-hello-portal"></a>Tutorial: Crear el primer índice de búsqueda de Azure en el portal de Hola

Hola portal de Azure, comienzan con un tooquickly de conjunto de datos de ejemplo predefinidos generar un índice mediante hello **importar datos** asistente. Explore la búsqueda de texto completo, los filtros, las facetas, la búsqueda aproximada y la búsqueda geográfica con el **Explorador de búsqueda**.  

Esta introducción sin código le permitirá comenzar a trabajar con datos predefinidos de modo que pueda escribir consultas interesantes de forma inmediata. Si bien las herramientas del portal no sustituyen al código, resultan de utilidad para realizar estas tareas:

+ Aprender de manera práctica con un período de inicialización mínimo
+ Crear un prototipo de un índice antes de escribir código en **Import data** (Importar datos).
+ Probar las consultas y la sintaxis del analizador en el **Explorador de búsqueda**.
+ Ver existente publicado tooyour servicios de index Server y buscar sus atributos

**Tiempo estimado:** unos 15 minutos, o más si también es necesario registrar la cuenta o el servicio. 

Como alternativa, resultará utilizando un [tooprogramming introducción basada en código búsqueda de Azure en .NET](search-howto-dotnet-sdk.md).

## <a name="prerequisites"></a>Requisitos previos

En este tutorial se supone que tiene una [suscripción de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) y un [servicio de Azure Search](search-create-service-portal.md). 

Si no desea tooprovision un servicio inmediatamente, puede ver una demostración de 6 minutos de hello los pasos de este tutorial, a partir de aproximadamente tres minutos en esta [vídeo de información general sobre la búsqueda de Azure](https://channel9.msdn.com/Events/Connect/2016/138).

## <a name="find-your-service"></a>Búsqueda del servicio
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Abra Panel de servicio de Hola de su servicio de búsqueda de Azure. Si no anclar Hola servicio icono tooyour o panel, puede ubicar el servicio de esta forma: 
   
   * Hola Jumpbar, haga clic en **más servicios** final Hola del panel de navegación izquierdo de Hola.
   * En el cuadro de búsqueda de hello, escriba *búsqueda* tooget una lista de búsqueda de servicios para su suscripción. El servicio debe aparecer en la lista de Hola. 

## <a name="check-for-space"></a>Búsqueda de espacio
Muchos clientes que se inicie con el servicio gratuito de Hola. Esta versión es limitado toothree índices, tres orígenes de datos y tres indizadores. Asegúrese de que tiene espacio para elementos adicionales antes de empezar. Este tutorial crea uno de cada objeto. 

> [!TIP] 
> Iconos de panel de servicio de hello muestran cuántos índices, los indizadores y orígenes de datos que ya tiene. icono de indizador de Hello muestra indicadores correctos y erróneos. Haga clic en recuento de indizador de hello mosaico tooview Hola. 
>
> ![Iconos para indexadores y orígenes de datos][1]
>

## <a name="create-index"></a> Creación de un índice y carga de datos
Las consultas de búsqueda recorren en iteración un *índice* que contiene datos de búsqueda, metadatos y construcciones usados para optimizar determinados comportamientos de búsqueda.

tookeep esta tarea basada en el portal, usamos un conjunto de datos de ejemplo integrada que puede volverán a rastrear usando un indizador a través de hello **importar datos** asistente. 

#### <a name="step-1-start-hello-import-data-wizard"></a>Paso 1: Iniciar el Asistente para datos de importación de Hola
1. En el panel de servicio de búsqueda de Azure, haga clic en **importar datos** en toostart de barra de comandos de hello un asistente que crea y rellena un índice.
   
    ![Comando de importación de datos][2]

2. En el Asistente de hello, haga clic en **origen de datos** > **ejemplos** > **realestate-us-sample**. Este origen de datos está preconfigurado con el nombre, el tipo y la información de conexión. Una vez creado, se convierte en un "origen de datos existente" que se puede reutilizar en otras operaciones de importación.

    ![Selección del conjunto de datos de ejemplo][9]

3. Haga clic en **Aceptar** toouse lo.

#### <a name="step-2-define-hello-index"></a>Paso 2: Definir índice Hola
Crear un índice es normalmente manual y basada en código, pero Asistente Hola puede generar un índice con cualquier origen de datos que pueden rastrear. Como mínimo, un índice requiere un nombre y una colección de campos, con un campo marcado como Hola toouniquely clave de documento identifique cada documento.

Los campos tienen tipos de datos y atributos. casillas de verificación de Hola a través de la parte superior de hello están *INDICE atributos* controlar cómo se utiliza el campo de Hola. 

* **Retrievable** significa que se muestra en la lista de resultados de búsqueda. Puede desactivar esta casilla para marcar los campos individuales como fuera de los resultados de búsqueda, por ejemplo, cuando los campos se usan solo en expresiones de filtro. 
* **Filterable**, **Sortable** y **Facetable** determinan si un campo se puede usar en un filtro, una ordenación o una estructura de navegación de facetas. 
* **Searchable** significa que se incluye un campo en la búsqueda de texto completo. Las cadenas permiten realizar búsquedas. Los campos numéricos y los booleanos a menudo se marcan como no utilizables en búsquedas. 

De forma predeterminada, el Asistente de hello examina origen de datos de Hola para identificadores únicos como base de hello para el campo de clave de Hola. Las cadenas se atribuyen como que se pueden recuperar y permiten realizar búsquedas. Los enteros se atribuyen como que se pueden recuperar, filtrar, ordenar y clasificar.

  ![Índice realestate generado][3]

Haga clic en **Aceptar** índice de hello toocreate.

#### <a name="step-3-define-hello-indexer"></a>Paso 3: Definir indizador Hola
Aún en hello **importar datos** asistente, haga clic en **indizador** > **nombre**y escriba un nombre para el indizador de Hola. 

Este objeto define un proceso ejecutable. Puede colocarlo en programación periódica, pero por ahora use Hola opción toorun Hola indizador una vez, inmediatamente, al hacer clic en **Aceptar**.  

  ![indexador realestate][8]

## <a name="check-progress"></a>Comprobación del progreso
toomonitor datos importar, volver al panel de servicio de toohello, desplácese hacia abajo y haga doble clic en hello **indizadores** lista de mosaicos tooopen Hola indizadores. Debería ver indizador Hola recién creado en la lista hello, que indica el estado "en curso" correcta o incorrecta, junto con el número de Hola de documentos indizados.

   ![Mensaje de progreso del indexador][4]

## <a name="query-index"></a>Índice de Hola de consulta
Ahora tiene un índice de búsqueda que está listo tooquery. **Buscar en el explorador** es una herramienta de consulta integrada en el portal de Hola. Proporciona un cuadro de búsqueda para que pueda comprobar si los resultados de búsqueda son los esperados. 

> [!TIP]
> Hola [vídeo de información general sobre la búsqueda de Azure](https://channel9.msdn.com/Events/Connect/2016/138), Hola siguiendo los pasos que se muestra en 6m08s vídeo Hola.
>

1. Haga clic en **buscar en el explorador** en la barra de comandos de Hola.

   ![Comando del explorador de búsqueda][5]

2. Haga clic en **cambios índice** en hello barra de comandos tooswitch demasiado*realestate-us-sample*.

   ![Comandos de índice y API][6]

3. Haga clic en **versión de API establecer** en toosee de barra de comandos de Hola que están disponibles las API de REST. Obtener una vista previa ofrecen a las API que tener acceso a características de toonew todavía no se han generalmente publicadas. Para las consultas de Hola a continuación, usar versión disponible con carácter general de hello (2016-09-01) a menos que indique. 

    > [!NOTE]
    > [API de REST de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/search-documents) hello y [biblioteca .NET](search-howto-dotnet-sdk.md#core-scenarios) son totalmente equivalentes, pero **buscar en el explorador** está equipado toohandle sólo las llamadas de REST. Acepta la sintaxis para ambos [sintaxis de consulta simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) y [completo analizador de consultas de Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), además de Hola a todos los parámetros de búsqueda disponibles en [Buscar documento](https://docs.microsoft.com/rest/api/searchservice/search-documents) operaciones.
    > 

4. En la barra de búsqueda de hello, escriba las cadenas de consulta de Hola a continuación y haga clic en **búsqueda**.

  ![Ejemplo de consulta de búsqueda][7]

**`search=seattle`**

+ Hola `search` parámetro es tooinput usa una búsqueda de palabra clave de búsqueda de texto completo, en este caso, devolver listados en el estado de Washington, Condado de rey, que contiene *Seattle* en cualquier campo de búsqueda en el documento de Hola. 

+ **Buscar en el explorador** devuelve resultados en JSON, que es detallado y son difícil de tooread si documentos tienen una estructura densa. Dependiendo de los documentos, puede que tenga código toowrite que los identificadores de buscan elementos importantes de resultados tooextract. 

+ Documentos se componen de todos los campos marcados como recuperables en el índice de Hola. atributos de índice tooview en el portal de hello, haga clic en *realestate-us-sample* en hello **índices** icono.

**`search=seattle&$count=true&$top=100`**

+ Hola `&` símbolo es parámetros de búsqueda usados tooappend, que pueden especificarse en cualquier orden. 

+  Hola `$count=true` parámetro devuelve un recuento de suma de Hola de todos los documentos devueltos. Puede comprobar las consultas de filtro mediante la supervisión de los cambios notificados por `$count=true`. 

+ Hola `$top=100` devuelve Hola mayor rango 100 documentos fuera Hola total. De forma predeterminada, búsqueda de Azure devuelve Hola primeros 50 mejores coincidencias. Puede aumentar o disminuir la cantidad de Hola a través de `$top`.

**`search=*&facet=city&$top=2`**

+ `search=*` es una búsqueda vacía. Las búsquedas vacías buscan en todo. Una de las razones para enviar una consulta vacía demasiado es filtrar o faceta sobre el conjunto completo de Hola de documentos. Por ejemplo, desea una tooconsist de estructura de navegación de facetas de todas las ciudades de índice de Hola.

+  `facet`Devuelve una exploración de la estructura que puede pasar el control de interfaz de usuario de tooa. Devuelve categorías y un recuento. En este caso, las categorías se basan en número de Hola de ciudades. No hay ninguna agregación en Azure Search, pero puede aproximarla mediante `facet`, que proporciona un recuento de documentos de cada categoría.

+ `$top=2`vuelve a incluir dos documentos, que ilustra que puede usar `top` tooboth reducir o aumentar los resultados.

**`search=seattle&facet=beds`**

+ Esta consulta es una faceta de "beds", en una búsqueda de texto de *Seattle*. `"beds"`se puede especificar como una faceta porque Hola campo está marcado como recuperables, puede filtrar y facetable en el índice de Hola y Hola valores contiene (numérico, 1 a 5), son adecuados para clasificar los anuncios en grupos (anuncios con 3 habitaciones, 4 habitaciones). 

+ Solo los campos que se pueden filtrar se pueden clasificar. Solo puede recuperables campos se pueden devolver en los resultados de Hola.

**`search=seattle&$filter=beds gt 3`**

+ Hola `filter` parámetro devuelve resultados que coincidan con los criterios de hello proporcionada. En este caso, más de 3 dormitorios. 

+ La sintaxis de filtro es una construcción de OData. Para más información, consulte la [sintaxis de filtro de OData](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search).

**`search=granite countertops&highlight=description`**

+ Resultados destacados hace referencia tooformatting en texto de coincidencia de palabra clave de hello, dada coincidencias se encuentran en un campo específico. Si el término de búsqueda profundamente se incrusta en una descripción, puede agregar llamada toomake resaltado sea más fácil toospot. En este caso, el Hola formato frase `"granite countertops"` es más fácil toosee en el campo de descripción de Hola.

**`search=mice&highlight=description`**

+ La búsqueda de texto completo busca formas de palabras con una semántica parecida. En este caso, los resultados de la búsqueda contienen texto resaltado de "mouse", para el hogar que tengan una infección de mouse (ratón) en la búsqueda de palabra clave de respuesta tooa en "mouse". Distintas formas de la misma palabra puede aparecer en los resultados debido a un análisis lingüístico de Hola. 

+ Azure Search admite 56 analizadores de Lucene y Microsoft. valor predeterminado de Hello utilizado por búsqueda de Azure es el analizador de Lucene estándar de Hola. 

**`search=samamish`**

+ Palabras incorrectas, como 'samamish' para el nivel predefinido de Samammish Hola Hola área de Seattle, se producirá un error tooreturn coincidencias de búsqueda típicas. errores de ortografía toohandle, puede usar búsqueda aproximada, que se describe en el siguiente ejemplo de Hola.

**`search=samamish~&queryType=full`**

+ La búsqueda aproximada está habilitada cuando se especifica hello `~` de símbolos y usar el analizador de consultas completa de hello, que se interpreta y analiza correctamente hello `~` sintaxis. 

+ La búsqueda aproximada está disponible cuando se opta por para el analizador de consultas completa de hello, que se produce cuando se establece `queryType=full`. Para obtener más información acerca de los escenarios de consulta habilitadas por el analizador de consultas completa de hello, consulte [Lucene de sintaxis de consulta de búsqueda de Azure](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).

+ Cuando `queryType` es no se especifica, se utiliza el analizador de consulta simple de hello predeterminado. Analizador de consultas sencillas de Hello es más rápido, pero si necesita búsqueda aproximada, las expresiones regulares, búsqueda de proximidad u otros tipos de consultas avanzadas, será necesario sintaxis completa de Hola. 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ Se admite la búsqueda de Geospatial a través de hello [edm. Tipo de datos de GeographyPoint](https://docs.microsoft.com/rest/api/searchservice/supported-data-types) en un campo que contiene coordenadas. La búsqueda geográfica es un tipo de filtro, que se especifica en la [sintaxis de filtro de OData](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search). 

+ consulta de ejemplo de Hola filtra todos los resultados de datos posicionales, donde los resultados son menos de 5 kilómetros desde un punto determinado (especificado como coordenadas de latitud y longitud). Agregando `$count`, puede ver cuántos resultados se devuelven cuando se cambia la distancia de Hola o coordenadas Hola. 

+ La búsqueda geoespacial resulta útil si su aplicación de búsqueda tiene una característica "buscar cerca de mí" o utiliza la navegación mediante mapas. No obstante, no es una búsqueda de texto completo. Si tiene requisitos de usuario para las búsquedas en una ciudad o el país por su nombre, agregar campos que contienen los nombres de ciudad o el país, en toocoordinates de adición.

## <a name="next-steps"></a>Pasos siguientes

+ Modificar cualquiera de los objetos de Hola que acaba de crear. Después de ejecutar el Asistente de hello una vez, se puede volver atrás y ver o modificar los componentes individuales: origen de datos, el indexador o el índice. No se permiten algunas modificaciones, como Hola cambiar el tipo de datos de campo de hello, en el índice de Hola, pero la mayoría de las propiedades y configuraciones son modificables.

  tooview componentes individuales, haga clic en hello **índice**, **indizador**, o **orígenes de datos** iconos en el panel toodisplay una lista de los objetos existentes. toolearn más información acerca de las modificaciones del índice que no requieren una recompilación, vea [Actualizar índice (API de REST de búsqueda de Azure)](https://docs.microsoft.com/rest/api/searchservice/update-index).

+ Intente Hola herramientas y pasos con otros orígenes de datos. conjunto de datos de ejemplo de Hola `realestate-us-sample`, proviene de una base de datos de SQL Azure que puede rastrear la búsqueda de Azure. Además de Azure SQL Database, Azure Search puede rastrear e inferir un índice a partir de estructuras de datos planas en Azure Table Storage, Blob Storage, SQL Server en una máquina virtual de Azure y Azure Cosmos DB. Todos estos orígenes de datos se admiten en el Asistente de Hola. En el código, puede rellenar un índice fácilmente con un *indexador*.

+ Todos los demás orígenes de datos no de indizador se admiten a través de un modelo de inserción, donde el código inserta nuevos y cambia los conjuntos de filas de índice de tooyour JSON. Para más información, consulte [Add, update, or delete documents in Azure Search](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents) (Agregar, actualizar o eliminar documentos en Azure Search).

Para más información sobre otras características mencionadas en este artículo, visite los vínculos siguientes:

* [Introducción a los indexadores](search-indexer-overview.md)
* [Crear índice (incluye una explicación detallada de los atributos de índice de hello)](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [Explorador de búsqueda](search-explorer.md)
* [Buscar documentos (incluye ejemplos de sintaxis de consulta)](https://docs.microsoft.com/rest/api/searchservice/search-documents)


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png