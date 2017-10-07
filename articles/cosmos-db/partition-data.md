---
title: aaaPartitioning y escalado horizontal en la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Obtenga información acerca de cómo funciona la creación de particiones en la base de datos de Azure Cosmos, cómo tooconfigure particiones y las claves de partición, y cómo toopick Hola derecha clave de partición para la aplicación."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a>¿Cómo toopartition y la escala en la base de datos de Azure Cosmos

[Base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) es un toohelp de servicio diseñado de base de datos distribuida, varios modelos global, obtendrá rendimiento rápido y predecible y escalabilidad sin problemas junto con la aplicación que se incremente. Este artículo proporciona información general sobre cómo las particiones funcionan para todos los datos de hello los modelos de base de datos de Azure Cosmos y describen cómo puede configurar el escalado de base de datos de Azure Cosmos contenedores tooeffectively sus aplicaciones.

Las particiones y las claves de partición también se explican en este vídeo de Azure Friday con Scott Hanselman y Shireesh Thota, Administrador de ingeniería principal de Azure Cosmos DB.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Creación de particiones en Azure Cosmos DB
Azure Cosmos DB permite almacenar y consultar datos sin esquemas con un tiempo de respuesta de milisegundos y a cualquier escala. Cosmos DB proporciona contenedores para el almacenamiento de datos llamados **colecciones (para el documento), grafos o tablas**. Los contenedores son recursos lógicos y pueden abarcar uno o varios servidores o particiones físicos. número de Hola de particiones viene determinado por la base de datos de Cosmos según el tamaño de almacenamiento de Hola y rendimiento aprovisionado de Hola de contenedor de Hola. Todas las particiones de Cosmos DB tienen una cantidad fija de almacenamiento con respaldo SSD asociado y se replican para ofrecer una alta disponibilidad. Administración de particiones es completamente administrado por base de datos de Azure Cosmos y no tiene un código complejo toowrite o administrar las particiones. Los contenedores de Cosmos DB son ilimitados en términos de almacenamiento y rendimiento. 

![horizontal](./media/introduction/azure-cosmos-db-partitioning.png) 

Creación de particiones es una aplicación tooyour transparente. COSMOS DB admite rápidas lecturas y escrituras, consultas, la lógica transaccional, niveles de coherencia y control de acceso específico a través de recursos de métodos y API tooa único contenedor. identificadores de servicio de Hello, distribuir los datos entre particiones y el enrutamiento de partición correcta de toohello de solicitudes de consulta. 

¿Cómo funciona la creación de particiones? Cada elemento debe tener una clave de partición y una clave de fila que lo identifiquen de forma única. La clave de partición ejerce de partición lógica para sus datos y proporciona a Cosmos DB un límite natural para distribuir datos entre las particiones. En resumen, la creación de particiones funciona en Azure Cosmos DB de la siguiente manera:

* Usted aprovisiona un contenedor de Cosmos DB con el rendimiento de las solicitudes/s `T`
* Entre bastidores de hello, las particiones de las disposiciones de Cosmos DB necesarios tooserve `T` solicitudes/s. Si `T` es mayor que el rendimiento máximo por partición hello `t`, a continuación, las disposiciones de Cosmos DB `N`  =  `T/t` particiones
* COSMOS DB asigna Hola clave espacio de partición hashes claves uniformemente a través de hello `N` particiones. De este modo, cada partición (partición física) hospeda valores de clave de partición 1-N (particiones lógicas)
* Cuando una partición física `p` alcanza su límite de almacenamiento, DB Cosmos perfectamente divide `p` en dos nuevas particiones `p1` y `p2` y distribuye valores correspondientes tooroughly mitad Hola claves tooeach de hello particiones. Esta operación de división es invisible tooyour aplicación.
* De forma similar, cuando se aprovisiona rendimiento superior `t*N` rendimiento, base de datos de Cosmos divide una o varias de su particiones toosupport Hola un rendimiento mayor

semántica de Hola para las claves de partición es la semántica de hello toomatch ligeramente diferente de cada API, como se muestra en hello en la tabla siguiente:

| API | Partition Key | Row Key |
| --- | --- | --- |
| DocumentDB | ruta de acceso de clave de partición personalizada | `id` fija | 
| MongoDB | clave de partición personalizada  | `_id` fija | 
| Grafo | propiedad de clave de partición personalizada | `id` fija | 
| Tabla | `PartitionKey` fija | `RowKey` fija | 

Cosmos DB usa la creación de particiones basada en hash. Cuando se escribe un elemento, Cosmos DB aplica un algoritmo hash de valor de clave de partición de Hola y Hola de uso valor hash resultado toodetermine qué elemento de partición toostore hello en. Hola a todos los elementos con misma clave de partición en los almacenes COSMOS DB Hola misma partición física. elección de Hola de clave de partición de hello es una decisión importante que se están toomake en tiempo de diseño. Debe elegir un nombre de propiedad que tenga una amplia gama de valores e incluso patrones de acceso.

> [!NOTE]
> Es un toohave de práctica recomendada una clave de partición con muchos valores distintos (100s 1000s como mínimo).
>

Los contenedores de Azure Cosmos DB se pueden crear como "fijos" o "ilimitados". Los contenedores de tamaño fijo tienen un límite máximo de 10 GB y un rendimiento de 10 000 RU/s. Algunas API permiten toobe de clave de partición de Hola se omite para los contenedores de tamaño fijo. toocreate un contenedor como ilimitado, debe especificar un rendimiento mínimo de 2500 RU/s.

## <a name="partitioning-and-provisioned-throughput"></a>Creación de particiones y procesamiento aprovisionado
Cosmos DB se ha diseñado para ofrecer un rendimiento predecible. Al crear un contenedor, reserva rendimiento en términos de **[unidades de solicitud](request-units.md) (RU) por segundo con un complemento potencial para RU por minuto**. Cada solicitud se asigna un cargo de unidad de solicitud es proporcional toohello cantidad de recursos del sistema como CPU, memoria y E/S consumidas por operación Hola. Una lectura de un documento de 1 KB con coherencia de sesión consume una unidad de solicitud. Una lectura es 1 RU independientemente del número de Hola de elementos almacenados u Hola número de solicitudes simultáneas que se ejecutan en hello mismo tiempo. Los elementos de mayor requieren mayor unidades de solicitud según el tamaño de Hola. Si conoce el tamaño de Hola de las entidades y Hola número de lecturas deberá toosupport para la aplicación, puede aprovisionar la cantidad exacta de Hola de rendimiento necesario para la aplicación de leer las necesidades. 

> [!NOTE]
> rendimiento total de Hola de tooachieve del contenedor de hello, debe elegir una clave de partición que le permite tooevenly distribuir las solicitudes entre algunos valores de clave de partición distintos.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a>Trabajar con las API de base de datos de Azure Cosmos Hola
Puede usar Hola portal de Azure o contenedores de toocreate de CLI de Azure y escalarlos en cualquier momento. Esta sección se muestra cómo los contenedores toocreate y especifique Hola rendimiento y la partición de definición de clave en cada uno de hello API admitidas.

### <a name="documentdb-api"></a>DocumentDB API
Hola siguiente ejemplo muestra cómo toocreate un contenedor (colección) mediante Hola API de documentos. Puede encontrar más información en [Creación de particiones con API de DocumentDB](partition-data.md).

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Puede leer un elemento (documento) con hello `GET` método hello API de REST o utilizando `ReadDocumentAsync` en uno de hello SDK.

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>MongoDB API
Con API de MongoDB hello, puede crear una colección particionada a través de la herramienta que prefiera, el controlador o el SDK. En este ejemplo, utilizamos Hola Shell de Mongo para la creación de la colección de Hola.

Hola Shell de Mongo:

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
Resultados:

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a>Table API

Con hello API de tabla, debe especificar para tablas de rendimiento de hello en configuración de appSettings de hello para la aplicación:

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

A continuación, crear una tabla mediante el SDK de almacenamiento de tabla de Azure Hola. clave de partición de Hola se crea implícitamente como hello `PartitionKey` valor. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

Puede recuperar una sola entidad con el siguiente fragmento de código de hello:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Vea [desarrollar con hello tabla API](tutorial-develop-table-dotnet.md) para obtener más detalles.

### <a name="graph-api"></a>API Graph

Con hello API Graph, debe usar Hola portal de Azure o contenedores de toocreate CLI. O bien, puesto que la base de datos de Azure Cosmos es varios modelo, puede usar uno de hello otro toocreate de modelos y escalar el contenedor de gráficos.

Puede leer cualquier vértice o borde con clave de partición de Hola y el identificador en Gremlin. Por ejemplo, para un gráfico con la región (EE ".") como clave de partición de Hola y "Seattle" como clave de fila de hello, encontrará un vértice mediante Hola según la sintaxis:

```
g.V(['USA', 'Seattle'])
```

Al igual que con los extremos, puede hacer referencia a un borde con clave de partición de Hola y clave de fila.

```
g.E(['USA', 'I5'])
```

Consulte [Gremlin support for Cosmos DB](gremlin-support.md) (Compatibilidad con Gremlin para Cosmos DB) para obtener más información.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Diseño de la creación de particiones
tooscale eficazmente con base de datos de Azure Cosmos, deberá toopick una buena clave de partición cuando se crea el contenedor. Existen dos consideraciones clave cuando se trata de elegir una clave de partición:

* **Límite para la consulta y las transacciones**: su elección de clave de partición debe equilibrar las entidades de uso de hello necesidad tooenable Hola de transacciones en hello requisito toodistribute a través de varios tooensure de claves de partición una solución escalable. En un extremo, puede establecer Hola misma clave de partición para todos los elementos, pero esto puede limitar la escalabilidad de hello de la solución. En hello otro extremo, puede asignar una clave de partición única para cada elemento, que podría ser muy escalables, pero podría impedir el uso de transacciones de documento cruzada a través de procedimientos almacenados y desencadenadores. Una clave de partición ideal es uno que permite conseguir consultas eficaces toouse y que tiene suficiente cardinalidad tooensure la solución es escalable. 
* **No hay cuellos de botella de rendimiento y almacenamiento**: es importante toopick una propiedad que permite escribe toobe distribuido en varios valores distintos. Las solicitudes toohello misma clave de partición no puede superar el rendimiento de una sola partición hello y están limitados. Por lo que es importante toopick una clave de partición que no da como resultado "zonas activas" dentro de la aplicación. Ya que todos los datos de Hola para una clave de partición solo debe almacenarse en una partición, también se recomienda tooavoid las claves de partición que tienen grandes volúmenes de datos para hello mismo valor. 

Echemos un vistazo a algunos escenarios en el mundo real, así como a las buenas claves de partición de cada uno de ellos:
* Si está implementando un back-end de perfil de usuario, Id. de usuario de hello es una buena elección para la clave de partición.
* Si almacena datos IoT, como el estado del dispositivo, un identificador de dispositivo es una buena elección para la clave de partición.
* Si usas la base de datos de Azure Cosmos para registrar datos de serie temporal, Hola, a continuación, nombre de host o Id. de proceso es una buena elección para la clave de partición.
* Si tiene una arquitectura de varios inquilinos, Id. de inquilino de hello es una buena elección para la clave de partición.

En algunos casos como IoT de uso y perfiles de usuario, la clave de partición de hello podría ser Hola mismo como su identificador (clave de documento). En otras como datos de serie temporal de hello, es posible que tenga una clave de partición es diferente del Id. de Hola.

### <a name="partitioning-and-loggingtime-series-data"></a>Creación de particiones, registro y datos de serie temporal
Uno de los casos de uso comunes de Hola de base de datos de Cosmos es para el registro y telemetría. Es importante toopick una buena clave de partición ya que tendrá que tooread/escritura de grandes volúmenes de datos. elección de Hello depende de su lectura y escritura tasas y tipos de consultas que espera toorun. Estas son algunas sugerencias sobre cómo toochoose una buena clave de partición.

* Si el caso de uso implica una pequeña tasa de escribe acumulan durante un largo período de tiempo y la necesidad de tooquery por intervalos de marcas de tiempo y los demás filtros, utilizando un paquete acumulativo de actualizaciones de hello marca de tiempo, por ejemplo, de fecha como una clave de partición es un enfoque adecuado. Esto le permite tooquery sobre todos los datos de Hola para una fecha de una única partición. 
* Si la carga de trabajo tiene muchas operaciones de escritura, lo que es más común, debe usar una clave de partición que no se base en la marca de tiempo para que Cosmos DB pueda distribuir escrituras uniformemente en varias particiones. En este caso, un nombre de host, identificador de proceso, identificador de actividad u otra propiedad con cardinalidad elevada, es una buena elección. 
* Un tercer enfoque es un híbrido uno donde tiene varios contenedores, uno para cada día/mes y clave de partición de hello es una propiedad como nombre de host específica. Esto tiene la ventaja de Hola que se puede establecer rendimiento diferentes en función de ventana de tiempo de hello, por ejemplo, contenedor de Hola para hello mes actual se haya aprovisionado con un mayor rendimiento porque es de lectura y escritura, mientras que los meses anteriores con reducir el rendimiento desde solo sirven lecturas.

### <a name="partitioning-and-multi-tenancy"></a>Creación de particiones y arquitectura multiempresa
Si implementa una aplicación multiinquilino mediante Cosmos DB, hay dos patrones populares: una clave de partición por inquilino y un contenedor por inquilino. Estos son Hola ventajas y desventajas de cada uno:

* Una clave de partición por inquilino: en este modelo, los inquilinos se colocan en un solo contenedor. Por su parte, las consultas e inserciones de elementos dentro de un único inquilino pueden realizarse en una sola partición. También se puede implementar la lógica transaccional en todos los elementos de un inquilino. Puesto que varios inquilinos comparten un contenedor, se pueden ahorrar costos de almacenamiento y rendimiento mediante la agrupación de los recursos para los inquilinos en un solo contenedor, en lugar de aprovisionar capacidad de aumento adicional para cada inquilino. el inconveniente de Hello es que no tienen aislamiento del rendimiento por inquilino. Aumenta el rendimiento/rendimiento aplica toohello todo contenedor vs destinadas aumenta para inquilinos.
* Un contenedor por inquilino: cada inquilino tiene su propio contenedor. En este modelo es posible reservar procesamiento por inquilino. Con el nuevo modelo de precios de aprovisionamiento de Cosmos DB, este modelo es más rentable para las aplicaciones multiempresa con un número pequeño de inquilinos.

También puede utilizar un enfoque de combinación/niveles que coloca a los inquilinos pequeños y migra mayor contenedor propias tootheir de inquilinos.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, hemos proporcionado información general a fin de dar una idea de los conceptos y procedimientos recomendados para crear particiones con cualquier API de Azure Cosmos DB. 

* Información sobre el [procesamiento aprovisionado en Azure Cosmos DB](request-units.md)
* Información sobre la [distribución global en Azure Cosmos DB](distribute-data-globally.md)



