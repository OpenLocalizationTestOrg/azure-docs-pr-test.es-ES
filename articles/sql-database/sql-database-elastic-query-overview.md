---
title: "información general de consulta flexible de base de datos SQL de aaaAzure | Documentos de Microsoft"
description: "Información general sobre la característica de consulta flexible de Hola"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: a8bf0e2c-bc74-44d0-9b1e-bcc9a6aa2e33
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: mlandzic
ms.openlocfilehash: db17f551882cfcae0da67fdda12708baeb6db81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-elastic-query-overview-preview"></a>Información general sobre las consultas elásticas de Azure SQL Database (versión preliminar)
característica de consulta flexible de Hello (en vista previa) le permite toorun una consulta de Transact-SQL que abarca varias bases de datos en la base de datos de SQL Azure. Permite tablas remotas de tooperform consultas entre bases de datos tooaccess y tooquery de herramientas (Excel, Power BI, Tableau, etc.) de Microsoft y terceros tooconnect uno de los niveles de datos con varias bases de datos. Con esta característica, puede escalar horizontalmente capas de datos de toolarge de las consultas en base de datos SQL y visualizar los resultados de hello en los informes de business intelligence (BI).


## <a name="why-use-elastic-queries"></a>¿Por qué usar consultas elásticas?

**Base de datos SQL de Azure**

Realice consultas entre bases de datos SQL de Azure completamente en T-SQL. lo que permite realizar consultas de solo lectura en bases de datos remotas. Esto proporciona una opción para local actual usando nombres de tres y cuatro partes o base de datos del servidor vinculado tooSQL las aplicaciones de toomigrate de los clientes de SQL Server.

**Disponible en el nivel Estándar**

Consulta elástico se admite en el nivel de rendimiento estándar de hello en el nivel de rendimiento de suma toohello Premium. Vea la sección de hello en vista previa de limitaciones que se indican en las limitaciones de rendimiento para los niveles de rendimiento inferior.

**Bases de datos de inserción tooremote**

Consultas elásticas ahora pueden insertar parámetros toohello remotos bases de datos SQL para su ejecución.

**Ejecución de un procedimiento almacenado**

Ejecute llamadas a procedimientos almacenados remotos o funciones remotas mediante [sp\_execute\_remote](https://msdn.microsoft.com/library/mt703714).

**Flexibilidad**

Tablas externas con consulta elástico ahora pueden hacer referencia a tablas de tooremote con un esquema diferente o un nombre de tabla.

## <a name="elastic-query-scenarios"></a>Escenarios de consulta elástica

objetivo de Hello es toofacilitate consultar escenarios donde varias bases de datos contribuyen filas en un solo resultado total. consulta de Hola o bien puede estar compuesto por usuario de Hola o una aplicación directamente o indirectamente a través de herramientas que están conectados toohello base de datos. Esto resulta especialmente útil cuando se crean informes, mediante herramientas de integración de datos o de BI comerciales, o bien cualquier aplicación que no se pueda cambiar. Con una consulta flexible, puede consultar a través de varias bases de datos con experiencia de conectividad de SQL Server familiar de hello en herramientas como Excel, Power BI, Tableau o Cognos.
Una consulta flexible permite un acceso sencillo tooan completa colección de bases de datos a través de las consultas emitidas por SQL Server Management Studio o Visual Studio y facilita la consulta entre bases de datos de Entity Framework o en otros entornos de ORM. La figura 1 muestra un escenario donde existente en la nube aplicación (que utiliza hello [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md)) se basa en una escala horizontal de datos de nivel y se utiliza una consulta flexible para informes de entre bases de datos.

**Figura 1** Consulta usada en la capa de datos de escala horizontal

![Consulta usada en la capa de datos de escala horizontal][1]

Escenarios de clientes para consulta elástico se caracterizan por hello siguientes topologías:

* **Particionamiento vertical - consultas entre bases de datos** (topología 1): datos de Hola se crea una partición vertical entre un número de bases de datos de una capa de datos. Normalmente, los distintos conjuntos de tablas residen en bases de datos diferentes. Esto significa que el esquema hello es diferente en distintas bases de datos. Por ejemplo, todas las tablas de inventario se encuentran en una base de datos mientras que todas las relacionadas con la contabilidad se encuentran en otra. Casos de uso comunes con esta topología requieren una tooquery a través de o informes de toocompile entre tablas en varias bases de datos.
* **Particiones horizontales - particionamiento** (topología de 2): datos se dividen en sentido horizontal de nivel de filas de toodistribute a través de un repositorio ampliado de datos. Con este enfoque, el esquema de hello es idéntica en todas las bases de datos participantes. Este enfoque también se denomina simplemente "particionamiento". Particionamiento puede realizarse y administra mediante bibliotecas de herramientas de bases de datos elásticas (1) Hola o (2) particionamiento automático. Una consulta flexible es informes tooquery o compilación usados en muchas particiones.

> [!NOTE]
> Consulta flexible funciona mejor para escenarios de informes ocasionales donde se puede realizar la mayor parte del procesamiento de Hola de capa de datos de Hola. Para grandes cargas de trabajo de informes o escenarios de almacenamiento de datos con consultas más complejas, considere también usar [Almacenamiento de datos SQL de Azure](https://azure.microsoft.com/services/sql-data-warehouse/).
>  

## <a name="vertical-partitioning---cross-database-queries"></a>Particionamiento vertical: consultas entre bases de datos

toobegin de codificación, vea [Introducción a la consulta entre bases de datos (creación de particiones verticales)](sql-database-elastic-query-getting-started-vertical.md).

Una consulta flexible puede ser datos de uso toomake ubicados en una bases de datos SQL del tooother disponible de base de datos SQL. Esto permite que las consultas de una base de datos toorefer tootables en cualquier otro remoto base de datos SQL. Hola primer paso es toodefine un origen de datos externo para cada base de datos remota. origen de datos externo de Hola se define en hello base de datos local que se desean toogain acceso tootables ubicado en la base de datos remota Hola. No son necesarios en la base de datos remota de Hola cambios. Para verticales partición escenarios típicos donde diferentes bases de datos tienen esquemas distintos, consultas elásticas pueden ser tooimplement usado casos de uso comunes, como acceder a los datos tooreference y entre bases de datos realizar consultas.

> [!IMPORTANT]
> Se debe poseer el permiso ALTER ANY EXTERNAL DATA SOURCE. Este permiso se incluye con el permiso ALTER DATABASE Hola. Los permisos ALTER ANY EXTERNAL DATA SOURCE son toohello toorefer necesario el origen de datos subyacentes.
>

**Datos de referencia**: topología de Hola se utiliza para la administración de datos de referencia. En la siguiente ilustración de hello, dos tablas (T1 y T2) con datos de referencia se mantienen en una base de datos dedicado. Utilizando una consulta flexible, ahora puede acceder a tablas T1 y T2 remotamente desde otras bases de datos, como se muestra en la figura Hola. Use la topología 1 si las tablas de referencia son pequeñas o si las consultas remotas en la tabla de referencia tienen predicados selectivos.

**Figura 2** partición Vertical: usar datos de referencia de tooquery de consulta flexible

![Creación de particiones: usar datos de referencia de consulta flexible tooquery vertical][3]

**Consulta entre bases de datos**: las consultas elásticas hacen posibles los casos de uso que requieren realizar consultas en varias bases de datos SQL. En la ilustración 3, se muestran cuatro bases de datos diferentes: CRM, Inventory, HR y Products. Las consultas realizadas en una de las bases de datos de hello también necesitan tener acceso a tooone o todos Hola otras bases de datos. Con una consulta flexible, puede configurar la base de datos para este caso mediante la ejecución de algunas instrucciones de DDL simples en cada una de las bases de cuatro datos Hola. Después de esta configuración por única vez, tabla de acceso tooa remota es tan sencillo como referencia tooa de tabla local de las consultas de T-SQL o desde las herramientas de BI. Si las consultas remotas de hello no devuelven resultados grandes, se recomienda este enfoque.

**Figura 3** partición Vertical: con consulta elástico tooquery a través de varias bases de datos

![Particionamiento vertical: con consulta elástico tooquery a través de varias bases de datos][4]

pasos siguientes Hello configuran consultas de bases de datos elásticas para escenarios de partición verticales que requieren la tabla de access tooa ubicados en bases de datos remotas de SQL con hello mismo esquema:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) miClaveMaestra
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) miCredencial
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) miOrigenDeDatos de tipo **RDBMS**
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) miTabla

Después de ejecutar las instrucciones de DDL de hello, puede tener acceso a tabla remota Hola "mytable" como si fuese una tabla local. La base de datos de SQL Azure automáticamente se abre una base de datos remoto de conexión toohello, procesará la solicitud en la base de datos remota de Hola y devuelve los resultados de Hola.

## <a name="horizontal-partitioning---sharding"></a>Particiones horizontales (particionamiento)
Con tooperform de consulta flexible tareas de notificación sobre particionada, es decir, horizontalmente particiones, capa de datos requiere un [mapa de particiones de bases de datos elásticas](sql-database-elastic-scale-shard-map-management.md) bases de datos de toorepresent Hola de capa de datos de Hola. Normalmente, sólo un mapa de particiones solo se usa en este escenario y una base de datos dedicada con capacidades de consulta flexible (nodo principal) actúa como punto de entrada de Hola para consultas de notificación. Sólo esta base de datos dedicada debe mapa de particiones de acceso toohello. Figura 4 muestra esta topología y su configuración con asignación de base de datos y particiones de consulta flexible de Hola. las bases de datos de Hola Hola nivel de datos pueden ser de cualquier edición o versión de base de datos de SQL Azure. Para obtener más información acerca de la biblioteca de cliente de base de datos elástica hello y la creación de mapas de particiones, vea [administración de mapa de particiones](sql-database-elastic-scale-shard-map-management.md).

**Ilustración 4** Particionamiento horizontal: usar una consulta elástica para informes en capas de datos particionadas

![Particionamiento horizontal: usar una consulta elástica para informes en capas de datos particionadas][5]

> [!NOTE]
> Base de datos de consulta flexible (nodo principal) puede ser independiente de la base de datos, o puede ser Hola mismo dicho mapa de particiones de Hola de hosts de la base de datos. Cualquier configuración que elija, asegúrese de que ese nivel de servicio y el rendimiento de esa base de datos es la cantidad de hello esperado de toohandle lo suficientemente alto de solicitudes de inicio de sesión o consulta.

Hello estos pasos, configure las consultas de bases de datos elásticas para escenarios horizontales de partición que requieren acceso tooa conjunto de tabla y que se encuentran en (normalmente) varios remotos bases de datos SQL:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) miClaveMaestra
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) miCredencial
* Crear un [mapa de particiones](sql-database-elastic-scale-shard-map-management.md) que representa el nivel de datos mediante la biblioteca de cliente de base de datos elástica Hola.   
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) miOrigenDeDatos de tipo **SHARD_MAP_MANAGER**
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) miTabla

Una vez que ha llevado a cabo estos pasos, puede tener acceso a la tabla con particiones horizontales de Hola "mytable" como si fuese una tabla local. La base de datos de SQL Azure automáticamente abre varias conexiones en paralelo toohello bases de datos remotas donde se almacenan físicamente las tablas de hello, procesa las solicitudes de hello en bases de datos remotas de Hola y devuelve los resultados de Hola.
Obtener más información sobre los pasos de hello necesarios para el escenario de particiones horizontales de hello puede encontrarse en [consulta flexible para la partición horizontal](sql-database-elastic-query-horizontal-partitioning.md).

toobegin de codificación, vea [Introducción a la consulta flexible para la partición horizontal (particionamiento)](sql-database-elastic-query-getting-started.md).

## <a name="t-sql-querying"></a>Consultas T-SQL
Una vez haya definido los orígenes de datos externos y las tablas externas, puede usar SQL Server conexión cadenas tooconnect toohello bases de datos normales que definió las tablas externas. A continuación, puede ejecutar instrucciones T-SQL sobre las tablas externas en esa conexión con limitaciones de hello descritas a continuación. Puede encontrar más información y ejemplos de consultas de T-SQL en temas de la documentación de Hola para [particiones horizontales](sql-database-elastic-query-horizontal-partitioning.md) y [particionamiento vertical](sql-database-elastic-query-vertical-partitioning.md).

## <a name="connectivity-for-tools"></a>Conectividad para herramientas
Puede usar regular tooconnect de cadenas de conexión de SQL Server de las aplicaciones y toodatabases herramientas de integración de inteligencia empresarial o datos que tienen tablas externas. Asegúrese de que SQL Server se admite como origen de datos para la herramienta. Una vez conectado, consulte toohello consulta elástico hello y base de datos de tablas externas en esa base de datos tal como lo haría con cualquier otra base de datos de SQL Server se conecta a toowith la herramienta.

> [!IMPORTANT]
> Actualmente no se admite la autenticación usando Azure Active Directory con consultas elásticas.
> 
> 

## <a name="cost"></a>Coste
Consulta elástico se incluye en el costo de Hola de las bases de datos de la base de datos de SQL Azure. Tenga en cuenta que se admiten topologías donde las bases de datos remotos están en otro centro de datos de punto de conexión de consulta flexible de Hola, pero la salida de datos de bases de datos remotas se encargan de regular [tasas Azure](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="preview-limitations"></a>Limitaciones de vista previa
* Ejecuta la primera consulta elástica puede tardar hasta tooa varios minutos en el nivel de rendimiento estándar de Hola. Este tiempo es una funcionalidad de consulta flexible de hello tooload necesarios; mejora el rendimiento de carga con niveles de rendimiento superiores.
* Aún no se admite el scripting de orígenes de datos externos o tablas externas desde SSMS o SSDT.
* La función Importación/Exportación para bases de datos SQL aún no admite orígenes de datos externos ni tablas externas. Si necesita toouse importación/exportación, quitar estos objetos antes de exportar y, a continuación, volver a crearlos después de importar.
* Consulta flexible actualmente solo admite tablas de tooexternal de acceso de solo lectura. Sin embargo, puede utilizar toda la funcionalidad de T-SQL en la base de datos de Hola donde se define la tabla externa de Hola. Esto puede ser útil para, por ejemplo, conservar los resultados temporales con, por ejemplo, seleccione < column_list > en < local_table > o toodefine procedimientos almacenados en la base de datos de consulta flexible de Hola que hacen referencia a tablas de tooexternal.
* A excepción de nvarchar(max), los tipos LOB no se admiten en las definiciones de tabla externa. Como alternativa, puede crear una vista en hello base de datos remota que convierte el tipo LOB de Hola a nvarchar (max), defina la tabla externa a través de la vista de hello en lugar de la tabla de base de Hola y, a continuación, se convierte en tipo LOB original de hello en las consultas.
* Actualmente no se admiten estadísticas de columna con tablas externas. Las estadísticas de tablas se admiten, pero necesitan toobe creado manualmente.

## <a name="feedback"></a>Comentarios
Por favor, compartir comentarios sobre su experiencia con consultas elásticas con nosotros Disqus siguiente, foros de MSDN de hello, o en Stackoverflow. Estamos interesados en todos los tipos de comentarios sobre el servicio de hello (defectos, bordes desparejos, espacios de característica).

## <a name="next-steps"></a>Pasos siguientes

* Para obtener un tutorial sobre la creación de particiones verticales, consulte [Introducción a las consultas entre bases de datos (particiones verticales)](sql-database-elastic-query-getting-started-vertical.md).
* Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento vertical, consulte [Consulta de datos particionados verticalmente](sql-database-elastic-query-vertical-partitioning.md)
* Para obtener un tutorial sobre la creación de particiones horizontales (particionamiento), consulte [Introducción a las consultas elásticas para las particiones horizontales (particionamiento)](sql-database-elastic-query-getting-started.md).
* Para ver la sintaxis y consultas de ejemplo para los datos con particionamiento horizontal, consulte [Consulta de datos particionados horizontalmente.](sql-database-elastic-query-horizontal-partitioning.md)
* Consulte [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) para ver un procedimiento almacenado que ejecuta una instrucción de Transact-SQL en una sola instancia remota de Azure SQL Database o un conjunto de bases de datos que actúan como particiones en un esquema de particiones horizontales.

<!--Image references-->
[1]: ./media/sql-database-elastic-query-overview/overview.png
[2]: ./media/sql-database-elastic-query-overview/topology1.png
[3]: ./media/sql-database-elastic-query-overview/vertpartrrefdata.png
[4]: ./media/sql-database-elastic-query-overview/verticalpartitioning.png
[5]: ./media/sql-database-elastic-query-overview/horizontalpartitioning.png

<!--anchors-->
