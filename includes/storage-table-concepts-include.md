## <a name="what-is-table-storage"></a>¿Qué es Table Storage?
Azure Table Storage permite almacenar una gran cantidad de datos estructurados. servicio de Hello es autenticado de un almacén de datos NoSQL que acepta llamadas de dentro y fuera de hello nube de Azure. Las tablas de Azure son ideales para el almacenamiento de datos estructurados no relacionales. Table Storage suele usarse para realizar las siguientes tareas:

* Almacenamiento de TB de datos estructurados capaces de ofrecer servicio a aplicaciones de escalado web
* Almacenamiento de conjuntos de datos que no requieren uniones complejas, claves externas o procedimientos almacenados y que pueden desnormalizarse para obtener un acceso rápido
* Consulta rápida de datos mediante un índice agrupado
* Acceso a datos con el protocolo de OData de Hola y las consultas LINQ con bibliotecas de .NET de servicios de datos de WCF

Puede usar la tabla almacenamiento toostore y consulta muy grandes conjuntos de datos estructurados no relacionales y las tablas se escalará que aumenta la demanda.

## <a name="table-storage-concepts"></a>Descripción de Table Storage
Almacenamiento de tabla contiene Hola de los componentes siguientes:

![Diagrama de componentes de Table Storage][Table1]

* **Formato de dirección URL:** el código trata las tablas en una cuenta con este formato de dirección:   
  http://`<storage account>`.table.core.windows.net/`<table>`  
  
  También puede resolver tablas de Azure directamente mediante esta dirección con hello Protocolo OData. Para más información, consulte [OData.org][OData.org].
* **Cuenta de almacenamiento:** todos los accesos tooAzure almacenamiento se realiza a través de una cuenta de almacenamiento. Consulte [Objetivos de escalabilidad y rendimiento del almacenamiento de Azure](../articles/storage/common/storage-scalability-targets.md) para obtener información sobre la capacidad de la cuenta de almacenamiento.
* **Tabla**: una tabla es una colección de entidades. Las tablas no exigen un esquema sobre entidades, lo que significa que una única tabla puede contener entidades que dispongan de diferentes conjuntos de propiedades. número de Hola de tablas que puede contener una cuenta de almacenamiento está limitado únicamente por límite de capacidad de cuenta de almacenamiento de Hola.
* **Entidad**: una entidad es un conjunto de propiedades de la fila de base de datos de tooa similar. Una entidad puede estar too1MB de tamaño.
* **Propiedades**: una propiedad es un par nombre-valor. Cada entidad puede incluir los datos de toostore de too252 propiedades. Cada entidad dispone también de tres propiedades del sistema que especifican una clave de partición, una clave de fila y una marca de tiempo. Entidades con la misma clave de partición se puede consultar más rápidamente e insertados o actualizados en las operaciones atómicas de Hola. Una clave de fila de la entidad es el identificador exclusivo en una partición.

Para obtener más información sobre la nomenclatura de tablas y propiedades, vea [Hola de entender el modelo de datos del servicio de tabla](/rest/api/storageservices/Understanding-the-Table-Service-Data-Model).

[Table1]: ./media/storage-table-concepts-include/table1.png
[OData.org]: http://www.odata.org/
