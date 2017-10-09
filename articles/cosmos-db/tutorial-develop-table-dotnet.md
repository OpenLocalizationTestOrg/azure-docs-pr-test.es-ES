---
title: 'Azure Cosmos DB: Desarrollar con hello API de tabla en .NET | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toodevelop con API de tabla de Azure Cosmos DB con .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a>Azure Cosmos DB: Desarrollar con hello API de tabla en .NET

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.

Este tutorial trata Hola siguientes tareas: 

> [!div class="checklist"] 
> * Creación de una cuenta de Azure Cosmos DB 
> * Habilitar la funcionalidad en el archivo app.config de hello 
> * Crear una tabla mediante hello [API tabla](table-introduction.md) (versión preliminar)
> * Agregar una tabla de tooa de entidad 
> * Inserción de un lote de entidades 
> * una sola entidad 
> * Consulta de entidades con índices secundarios automáticos 
> * una entidad 
> * Eliminación de una entidad 
> * Eliminación de una tabla
 
## <a name="tables-in-azure-cosmos-db"></a>Tablas en Azure Cosmos DB 

Base de datos de Azure Cosmos proporciona hello [API tabla](table-introduction.md) (vista previa) para las aplicaciones que necesitan un almacén de clave y valor con un diseño sin esquema. [El almacenamiento de tabla](../storage/common/storage-introduction.md) SDK y las API de REST pueden ser toowork utilizado con la base de datos de Azure Cosmos. Puede usar tablas de base de datos de Azure Cosmos toocreate con requisitos de alto rendimiento. Azure Cosmos DB admite tablas optimizadas para el rendimiento (llamadas informalmente "tablas premium"), actualmente en versión preliminar pública. 

Puede continuar toouse almacenamiento de tabla de Azure para las tablas con almacenamiento alta y requisitos de rendimiento inferior. Azure DB Cosmos incorporará la compatibilidad con tablas con optimización para el almacenamiento en una futura actualización y se actualiza la tabla de Azure nuevas y existentes serán las cuentas de almacenamiento sin problemas tooAzure Cosmos DB.

Si actualmente usa almacenamiento de tabla de Azure, obtendrá Hola siguientes ventajas con hello "premium" vista previa:

- [Distribución global](distribute-data-globally.md) llave en mano con hospedaje múltiple y [conmutaciones por error manuales y automáticas](regional-failover.md)
- Compatibilidad con el indexado automático independiente del esquema con respecto a todas las propiedades ("índices secundarios") y consultas rápidas 
- Compatibilidad con el [escalado independiente de proceso y almacenamiento](partition-data.md), en cualquier número de regiones
- Compatibilidad con [rendimiento dedicado por tabla](request-units.md) que se puede escalar de las centenas toomillions de solicitudes por segundo
- Compatibilidad con [cinco niveles de coherencia optimizarse](consistency-levels.md) tootrade disponibilidad, latencia y coherencia según sus necesidades de aplicación
- disponibilidad del 99,99% dentro de una única región y capacidad tooadd más regiones para una mayor disponibilidad y [líderes en la industria completa SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/) en disponibilidad general
- Trabajar con almacenamiento de Azure existente .NET SDK de Hola y no haya ninguna aplicación de tooyour de cambios de código

Durante la vista previa de hello, admite la base de datos de Azure Cosmos Hola mediante Hola .NET SDK de API de tabla. Puede descargar hello [SDK de vista previa del almacenamiento de Azure](https://aka.ms/premiumtablenuget) de NuGet, que tiene Hola mismas clases y las firmas de método como hello [SDK de almacenamiento de Azure](https://www.nuget.org/packages/WindowsAzure.Storage), pero también puede conectarse tooAzure Cosmos DB cuentas con hello API de la tabla.

toolearn más información acerca de tareas complejas de almacenamiento de tabla de Azure, vea:

* [Introducción tooAzure DB Cosmos: API de tabla](table-introduction.md)
* Hola documentación de referencia de servicio de tabla para obtener información detallada acerca de las API disponibles [biblioteca de cliente de almacenamiento para la referencia de .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

### <a name="about-this-tutorial"></a>Acerca de este tutorial
Este tutorial está usando para los desarrolladores que están familiarizados con hello almacenamiento de tabla de Azure SDK y desearía disponibles las características toouse Hola premium de base de datos de Azure Cosmos. Se basa en [Introducción al almacenamiento de tabla de Azure mediante .NET](table-storage-how-to-use-dotnet.md) y muestra cómo tootake aprovechar capacidades adicionales como los índices secundarios, rendimiento aprovisionado y la conexión. Trataremos cómo toouse Hola toocreate portal Azure una cuenta de base de datos de Azure Cosmos y, a continuación, generar e implementar una aplicación de la tabla. También analizaremos ejemplos de .NET para crear y eliminar una tabla, además de insertar, actualizar, eliminar y consultar datos de tabla. 

Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/). Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

Empecemos creando una cuenta de base de datos de Azure Cosmos Hola portal de Azure.  

> [!TIP]
> * ¿Ya tiene una cuenta de Azure Cosmos DB? Si es así, pasar demasiado[configure su solución de Visual Studio](#SetupVS).
> * ¿Ya tenía una cuenta de Azure DocumentDB? En caso afirmativo, la cuenta es ahora una cuenta de base de datos de Azure Cosmos y puede saltarse lecciones demasiado[configure su solución de Visual Studio](#SetupVS).  
> * Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[configurar la solución de Visual Studio](#SetupVS).
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Ahora vamos a clonar una aplicación de la tabla de github, establezca la cadena de conexión de Hola y ejecútelo.

1. Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.  

2. Ejecute hello después de repositorio de ejemplo de comando tooclone Hola. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. A continuación, abra el archivo de solución de hello en Visual Studio.

## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.

1. Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**. Deberá usar botones de copia de hello en hello derecha de la cadena de conexión de hello pantalla toocopy Hola en el archivo app.config de hello en el paso siguiente Hola.

2. En Visual Studio, abra el archivo app.config de hello. 

3. Copie el valor URI de portal hello (mediante el botón Copiar de Hola) y hacerla Hola valor de clave de cuenta de hello en el archivo app.config. Utilice el nombre de cuenta de hello creado anteriormente para el nombre de cuenta en el archivo app.config.
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> toouse esta aplicación con almacenamiento de tabla de Azure estándar, se necesita la cadena de conexión de Hola de toochange en `app.config file`. Utilice el nombre de cuenta de hello como nombre de la cuenta de la tabla y la clave como clave principal de almacenamiento de Azure. <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a>Compilar e implementar la aplicación hello
1. En Visual Studio, haga doble clic en el proyecto de hello en **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**. 

2. Hola NuGet **examinar** , escriba ***WindowsAzure.Storage PremiumTable***. Active **Incluir versiones preliminares**.

3. Desde los resultados de hello, instalar hello **WindowsAzure.Storage PremiumTable** y elija la versión preliminar de hello `0.0.1-preview`. Esta acción instala el paquete de almacenamiento de tabla de Azure de Hola y todas las dependencias.

4. Haga clic en CTRL + F5 aplicación hello de toorun. 

Ahora puede volver atrás tooData explorador y vea la consulta, modificar y trabajar con estos datos de tabla. 

> [!NOTE]
> toouse esta aplicación con un emulador de base de datos de Cosmos de Azure, que necesita toochange cadena de conexión de hello en `app.config file`. Usar hello por debajo del valor para el emulador. <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a>Funcionalidades de Azure Cosmos DB
Base de datos de Azure Cosmos admite una serie de funcionalidades que no están disponibles en hello API de almacenamiento de tabla de Azure. Hello nueva funcionalidad puede habilitarse a través siguiente hello `appSettings` valores de configuración. No se ha introducido cualquier nueva firmas o sobrecargas toohello vista previa del SDK de almacenamiento de Azure. Esto le permite tooconnect tooboth standard y premium tablas y trabajar con otros servicios de almacenamiento de Azure como Blobs y colas. 


| Clave | Descripción |
| --- | --- |
| TableConnectionMode  | Azure Cosmos DB admite dos modos de conectividad. En `Gateway` modo, las solicitudes se realizan siempre toohello base de datos de Azure Cosmos puerta de enlace, que lo reenvía toohello particiones de datos correspondiente. En `Direct` modo de conectividad, cliente hello captura asignación Hola de toopartitions de tablas y las solicitudes se realizan directamente en particiones de datos. Se recomienda `Direct`, Hola de forma predeterminada.  |
| TableConnectionProtocol | Azure Cosmos DB admite dos protocolos de conexión: `Https` y `Tcp`. `Tcp`es el valor predeterminado de Hola y recomienda porque es más ligera. |
| TablePreferredLocations | Lista separada por comas de las ubicaciones preferidas (hospedaje múltiple) para las lecturas. Cada cuenta de Azure Cosmos DB se puede asociar con entre 1 y 30 regiones más. Cada instancia del cliente puede especificar un subconjunto de estas regiones en orden de hello preferido para las lecturas de latencia baja. regiones de Hello deben denominarse mediante sus [nombres para mostrar](https://msdn.microsoft.com/library/azure/gg441293.aspx), por ejemplo, `West US`. Consulte también las [API de hospedaje múltiple](tutorial-global-distribution-table.md).
| TableConsistencyLevel | Puede compensar entre la latencia, la coherencia y la disponibilidad si elige entre cinco niveles de coherencia bien definidos: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` y `Eventual`. El valor predeterminado es `Session`. elección de Hola de nivel de coherencia realiza una diferencia significativa del rendimiento en configuraciones de varias regiones. Consulte [Niveles de coherencia](consistency-levels.md) para obtener detalles. |
| TableThroughput | Rendimiento reservados para la tabla de hello expresado en unidades de solicitud (RU) por segundo. Las tablas únicas puede admitir cientos de millones de RU/s. Consulte [Unidades de solicitud](request-units.md). El valor predeterminado es `400` |
| TableIndexingPolicy | Indexado secundario coherente y automático de todas las columnas dentro de las tablas | Toohello que cumplan con la indización de especificación de la directiva de cadena JSON. Vea [directiva de indización](indexing-policies.md) toosee cómo puede cambiar columnas específicas de indización directiva tooinclude/exclude. | Indexado automático de todas las propiedades (hash para cadenas e intervalo para números) |
| TableQueryMaxItemCount | Configurar Hola número máximo de elementos devueltos por la consulta de tabla en un viaje de ida y. Valor predeterminado es `-1`, que permite que base de datos de Azure Cosmos determinar dinámicamente el valor de hello en tiempo de ejecución. |
| TableQueryEnableScan | Si consulta hello no puede utilizar el índice de Hola para cualquier filtro, a continuación, ejecutarlo todos modos a través de un examen. El valor predeterminado es `false`.|
| TableQueryMaxDegreeOfParallelism | grado de Hola de paralelismo para la ejecución de una consulta entre particiones. `0`es en serie con ninguna captura previa, `1` es en serie con captura previa y los valores altos aumento de velocidad de Hola de paralelismo. Valor predeterminado es `-1`, que permite que base de datos de Azure Cosmos determinar dinámicamente el valor de hello en tiempo de ejecución. |

toochange Hola valor, abra hello `app.config` archivo desde el Explorador de soluciones en Visual Studio. Agregar contenido de Hola de hello `<appSettings>` elemento se muestra a continuación. Reemplace `account-name` con el nombre de saludo de la cuenta de almacenamiento y `account-key` con su clave de acceso de cuenta. 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello. Abra hello `Program.cs` archivo y descubre que estas líneas de código crean Hola recursos de la tabla. 

## <a name="create-hello-table-client"></a>Crear el cliente de la tabla de Hola
Inicializar un `CloudTableClient` cuenta de tabla de tooconnect toohello.

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
Este cliente se inicializa con hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, y `TablePreferredLocations` si se especifica en configuración de la aplicación hello de los valores de configuración.
    
## <a name="create-a-table"></a>Creación de una tabla
Luego, se crea una tabla con `CloudTable`. Tablas de base de datos de Azure Cosmos pueden escalar de forma independiente en cuanto a almacenamiento y rendimiento, y el servicio Hola particiones administra automáticamente. Azure Cosmos DB admite tanto tablas ilimitadas como de tamaño fijo. Consulte [Creación de particiones en Azure Cosmos DB](partition-data.md) para obtener detalles. 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

Existe una diferencia importante en la manera de crear las tablas. Azure Cosmos DB reserva rendimiento, a diferencia del modelo basado en consumo de Azure Storage para las transacciones. modelo de reserva de Hello tiene dos ventajas clave:

* El rendimiento es dedicado/reservado, por lo que nunca se verá limitado si la velocidad de solicitudes se encuentra en el rendimiento aprovisionado o está por debajo de este
* modelo de reserva de Hello es más [rentable para cargas de trabajo de uso intensivo de rendimiento](key-value-store-cost.md)

Puede configurar el rendimiento de hello predeterminado mediante la configuración de Hola para `TableThroughput` en cuanto a RU (unidades de solicitud) por segundo. 

Una lectura de una entidad de 1 KB se normaliza como 1 RU y otras operaciones son tooa normalizado fijo valor RU según su consumo de CPU, memoria y e/s por segundo. Más información sobre [Unidades de solicitud en Azure Cosmos DB](request-units.md).

> [!NOTE]
> Aunque SDK de almacenamiento de tabla no admite actualmente la modificación de rendimiento, puede cambiar el rendimiento de hello al instante en cualquier momento mediante el portal de Azure de Hola o CLI de Azure.

A continuación, se recorra lectura simple hello y operaciones de escritura (CRUD) mediante almacenamiento de tabla de Azure Hola SDK. En este tutorial se muestran las consultas rápidas y las latencias bajas predecibles de milisegundos de un solo dígito que proporciona Azure Cosmos DB.

## <a name="add-an-entity-tooa-table"></a>Agregar una tabla de tooa de entidad
Las entidades de almacenamiento de tabla de Azure se extienden desde hello `TableEntity` clase y debe tener `PartitionKey` y `RowKey` propiedades. La siguiente es una definición de ejemplo de una entidad de cliente.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

Hola siguiente fragmento de código muestra cómo tooinsert una entidad con Hola almacenamiento de Azure SDK. Base de datos de Azure Cosmos está diseñado para garantiza una latencia baja a cualquier escala, a través de Hola a todos.

Completar escrituras < 15 ms en p99 y ~ 6 ms en p50 para aplicaciones que se ejecutan Hola misma región que la cuenta de base de datos de Azure Cosmos Hola. Y esta duración cuentas para hechos de Hola que escribe se confirmen cliente toohello espera una vez que se replican de forma sincrónica, confirma de forma duradera, y se indiza todo el contenido.

Hola API de tabla de base de datos de Azure Cosmos está en vista previa. En disponibilidad general, garantías de latencia de hello p99 respaldados por el SLA al igual que otras API de base de datos de Azure Cosmos. 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Inserción de un lote de entidades
Azure tabla almacenamiento es compatible con una API de operación por lotes, que le permite combinar las actualizaciones, eliminaciones e inserciones en Hola misma operación por lotes. Base de datos de Azure Cosmos no tiene algunas de las limitaciones de hello en API de lote de hello como almacenamiento de tabla de Azure. Por ejemplo, puede realizar varias lecturas dentro de un lote, puede realizar varias toohello escrituras misma entidad dentro de un lote, y no hay ningún límite en 100 operaciones por lote. 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a>una sola entidad
Recupera (obtiene) en la base de datos de Cosmos a Azure completo < 10 ms en p99 y ~ 1 ms en p50 en Hola la misma región de Azure. Puede agregar tantos cuenta tooyour de regiones para lecturas de latencia baja e implementar aplicaciones tooread de su región local ("host múltiple") estableciendo `TablePreferredLocations`. 

Puede recuperar una sola entidad con el siguiente fragmento de código de hello:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> Obtenga información sobre las API de hospedaje múltiple en [Desarrollo con varias regiones](tutorial-global-distribution-table.md)
>

## <a name="query-entities-using-automatic-secondary-indexes"></a>Consulta de entidades con índices secundarios automáticos
Las tablas se pueden consultar mediante hello `TableQuery` clase. Azure Cosmos DB tiene un motor de base de datos optimizado para escritura que indexa automáticamente todas las columnas dentro de la tabla. La indización de base de datos de Azure Cosmos es tooschema independiente. Por lo tanto, incluso si el esquema es diferente entre las filas, o si el esquema de hello evoluciona con el tiempo, se indizan automáticamente. Puesto que la base de datos de Azure Cosmos admite índices secundarios automática, las consultas con respecto a cualquier propiedad pueden usar el índice de Hola y servidas eficazmente.

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

En la vista previa, base de datos de Azure Cosmos admite Hola igual funcionalidad como almacenamiento de tabla de Azure para hello API de tabla de consulta. Azure Cosmos DB también admite ordenación, agregados, consulta geoespacial, jerarquía y una amplia variedad de funciones integradas. se proporciona funcionalidad adicional de Hello en hello API de tabla en una actualización de servicio futura. En [Consulta de Azure Cosmos DB](documentdb-sql-query.md) puede encontrar información general sobre esas funcionalidades. 

## <a name="replace-an-entity"></a>una entidad
tooupdate una entidad, recuperar del servicio de tabla de hello, modificar el objeto de entidad de hello y, a continuación, guardar los cambios de hello hacer copia de servicio de la tabla de toohello. Hello código siguiente cambia número de teléfono de un cliente existente. 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
Del mismo modo, puede realizar las operaciones `InsertOrMerge` o `Merge`.  

## <a name="delete-an-entity"></a>Eliminación de una entidad
Puede eliminar fácilmente una entidad después de que se han recuperado mediante el uso de hello mismo patrón que se muestra para la actualización de una entidad. Hola siguiente código recupera y elimina una entidad customer.

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a>Eliminación de una tabla
Por último, Hola ejemplo de código siguiente elimina una tabla de una cuenta de almacenamiento. Puede eliminar una tabla y volver a crearla de inmediato con Azure Cosmos DB.

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a>Limpieza de recursos 

Si no va toocontinue toouse esta aplicación, utilice Hola después toodelete pasos todos los recursos creados por este tutorial Hola portal de Azure.   

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.  
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**. 

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, hemos aprendido cómo tooget a usar base de datos de Azure Cosmos con hello API de tabla y ha hecho siguiente hello: 

> [!div class="checklist"] 
> * Se creó una cuenta de Azure Cosmos DB 
> * Funcionalidad activada en el archivo app.config de hello 
> * Se creó una tabla 
> * Se ha agregado una tabla de tooa de entidad 
> * Se insertó un lote de entidades 
> * Se recuperó una sola entidad 
> * Se consultaron las entidades con índices secundarios automáticos 
> * Se reemplazó una entidad 
> * Se eliminó una entidad 
> * Se eliminó una tabla  

Ahora puede continuar el tutorial siguiente toohello y más información sobre cómo consultar los datos de la tabla. 

> [!div class="nextstepaction"]
> [Consultar con hello API de tabla](tutorial-query-table.md)
