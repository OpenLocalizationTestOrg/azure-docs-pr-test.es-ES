---
title: "Guía de diseño de tabla de almacenamiento aaaAzure | Documentos de Microsoft"
description: "Diseño de tablas escalables y eficientes en Azure Table Storage"
services: cosmos-db
documentationcenter: na
author: mimig1
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 059f05a1d20e4d9537034b7ca133c5334bbefa04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a>Guía de diseño de tablas de Azure Storage: diseño de tablas escalables y eficientes
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

toodesign escalable y tablas de rendimiento debe tener en cuenta una serie de factores como el rendimiento, escalabilidad y costo. Si previamente ha diseñado esquemas para bases de datos relacionales, estas consideraciones será tooyou familiar, pero aunque hay algunas similitudes entre el modelo de almacenamiento del servicio de tabla de Azure de Hola y modelos relacionales, también hay muchos importante diferencias. Normalmente, estas diferencias provocan toovery distintos diseños que puede ser contraproducente o incorrecto toosomeone familiarizado con bases de datos relacionales, pero que realizar idea clara si está diseñando para un almacén de clave/valor de NoSQL como Hola servicio tabla de Azure. Muchas de sus diferencias de diseño reflejarán Hola ausencia de servicio de la tabla de hello toosupport diseñado aplicaciones de escala de nube que pueden contener miles de millones de entidades (filas en la terminología de base de datos relacional) de datos o conjuntos de datos que debe admitir muy alto volúmenes de transacciones: por lo tanto, necesita toothink diferente sobre cómo almacenar los datos y comprender el funcionamiento de hello servicio tabla. Un almacén de datos NoSQL bien diseñado puede habilitar su tooscale solución mucho más allá (y a un costo menor) a una solución que usa una base de datos relacional. Esta guía le ayuda con estos temas.  

## <a name="about-hello-azure-table-service"></a>Acerca de hello servicio tabla de Azure
Esta sección resalta algunas de hello características clave de servicio de la tabla de Hola que son especialmente relevante toodesigning de rendimiento y escalabilidad. Si está tooAzure nuevo almacenamiento y Hola servicio tabla, primero lea [Introducción tooMicrosoft almacenamiento de Azure](../storage/common/storage-introduction.md) y [Introducción al almacenamiento de tabla de Azure mediante .NET](table-storage-how-to-use-dotnet.md) antes de leer el resto de Hola de este artículo. Aunque el objetivo de Hola de esta guía se encuentra en hello servicio tabla, se incluyen algunos discusión de hello cola de Azure y servicios de Blob y cómo puede usar junto con hello servicio de tabla en una solución.  

¿Qué es el servicio de la tabla de hello? Como cabría esperar en nombre de hello, Hola servicio tabla utiliza un datos de toostore formato tabular. En la terminología estándar de hello, cada fila de tabla de hello representa una entidad y almacén de columnas de Hola Hola distintas propiedades de esa entidad. Cada entidad tiene un par de claves toouniquely identificarlo y una columna de marca de tiempo que Hola servicio tabla usa tootrack cuando se actualizó por última vez la entidad de hello (Esto ocurre automáticamente y no se puede sobrescribir manualmente Hola marca de tiempo con un valor arbitrario). Hola servicio tabla utiliza esta simultaneidad optimista de toomanage de marca de hora de última modificación (LMT).  

> [!NOTE]
> operaciones de API de REST del servicio de tabla de Hello también devuelven un **ETag** valor que se derive de marca de hora de última modificación de hello (LMT). En este documento se usará Hola términos ETag y LMT indistintamente porque hacen referencia toohello mismos datos subyacentes.  
> 
> 

Hello en el ejemplo siguiente se muestra un toostore de diseño de tabla simple entidades employee y department. Muchos de los ejemplos de hello que se muestra más adelante en esta guía se basan en este diseño simple.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td>Marketing</td>
<td>00001</td>
<td>2014-08-22T00:50:32Z</td>
<td>
<table>
<tr>
<th>Nombre</th>
<th>Apellidos</th>
<th>Edad</th>
<th>Email</th>
</tr>
<tr>
<td>Don</td>
<td>Hall</td>
<td>34</td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>00002</td>
<td>2014-08-22T00:50:34Z</td>
<td>
<table>
<tr>
<th>Nombre</th>
<th>Apellidos</th>
<th>Edad</th>
<th>Email</th>
</tr>
<tr>
<td>Jun</td>
<td>Cao</td>
<td>47</td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>Departamento</td>
<td>2014-08-22T00:50:30Z</td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Marketing</td>
<td>153</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>Ventas</td>
<td>00010</td>
<td>2014-08-22T00:50:44Z</td>
<td>
<table>
<tr>
<th>Nombre</th>
<th>Apellidos</th>
<th>Edad</th>
<th>Email</th>
</tr>
<tr>
<td>Ken</td>
<td>Kwok</td>
<td>23</td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


Hasta ahora, parece muy similar tabla tooa en una base de datos relacional con diferencias clave Hola está Hola columnas obligatorias y hello capacidad toostore varios tipos de entidad en hello misma tabla. Además, cada uno de Hola propiedades definidas por el usuario como **FirstName** o **Age** tiene un tipo de datos, como entero o cadena, simplemente como una columna en una base de datos relacional. Aunque a diferencia de una base de datos relacional, naturaleza sin esquema de Hola de hello significa de servicio de tabla que no necesita tener una propiedad Hola mismo tipo de datos de cada entidad. toostore tipos de datos complejos en una sola propiedad, debe usar un formato serializado como JSON o XML. Para obtener más información acerca de los tipos de datos de servicio como las de tabla de hello, intervalos de fechas admitido, las reglas de nomenclatura y las restricciones de tamaño, vea [Hola de entender el modelo de datos del servicio de tabla](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Como verá, la elección de **PartitionKey** y **RowKey** es el diseño de tabla toogood fundamentales. Todas las entidades almacenadas en una tabla deben tener una combinación única de **PartitionKey** y **RowKey**. Al igual que con las claves en una tabla de base de datos relacional, Hola **PartitionKey** y **RowKey** valores están indizada toocreate un índice agrupado que permite búsquedas rápidas; sin embargo, Hola servicio tabla no crea ninguno índices secundarios, por lo que se trata de hello solo dos propiedades (para algunos de los patrones de Hola que se describe más adelante, muestran cómo puede solucionar esta limitación aparente) indizan.  

Una tabla está formada por una o varias particiones, como verá, muchas de hello decisiones de diseño que realice torno eligiendo un adecuado **PartitionKey** y **RowKey** toooptimize la solución. Una solución puede constar de solo una única tabla que contenga todas las entidades que se organizan en particiones, pero normalmente las soluciones tendrán varias tablas. Ayudarle a tablas toologically organizar las entidades, ayudará a administrar toohello el acceso a datos mediante acceso a las listas de control y puede quitar una tabla completa con una sola operación de almacenamiento.  

### <a name="table-partitions"></a>Particiones de tabla
nombre de la cuenta de Hello, nombre de tabla y **PartitionKey** juntos identifican la partición de hello en el servicio de almacenamiento de Hola donde el servicio de la tabla de Hola almacena entidad Hola. Además de ser parte del esquema para las entidades de direccionamiento de hello, las particiones definen un ámbito para las transacciones (vea [transacciones de grupo de la entidad](#entity-group-transactions) a continuación) y formulario Hola de cómo el servicio de tabla de hello escala. Para obtener más información sobre las particiones, vea [Objetivos de rendimiento y escalabilidad de Azure Storage](../storage/common/storage-scalability-targets.md).  

Hola servicio tabla, un nodo individual de servicios de uno o varios completar las particiones y Hola escalas de servicio mediante Equilibrio de carga de forma dinámica particiones entre nodos. Si un nodo está bajo carga, servicio de la tabla de hello puede *dividir* intervalo Hola de particiones da servicio ese nodo en nodos diferentes; cuando desaparezca el tráfico, puede servicio hello *mezcla* partición Hola comprendido entre nodos silenciosos en un único nodo.  

Para obtener más información acerca de Hola servicio tabla Detalles internos de hello y, en particular cómo servicio hello: administra las particiones, vea papel hello [almacenamiento de Microsoft Azure: A altamente disponible en la nube servicio de almacenamiento seguro coherencia](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).  

### <a name="entity-group-transactions"></a>Transacciones de grupo de entidad
Hola servicio tabla, las transacciones de grupo de entidad (EGTs) son el mecanismo de solo integrados de Hola para llevar a cabo actualizaciones atómicas en varias entidades. EGTs también son que se hace referencia tooas *procesar por lotes las transacciones* en algunos documentos. EGTs sólo pueden funcionar en entidades almacenadas en hello misma partición (Hola de recurso compartido misma clave de partición en una tabla determinada), por lo que siempre que necesite comportamiento transaccional atómica a través de varias entidades necesita tooensure que esas entidades se encuentran en hello misma partición. Por lo general, suele ser una razón para conservar varios tipos de entidad en hello misma tabla (y crear particiones) y no utilizar varias tablas para los tipos de entidad diferente. Una sola EGT puede operar en 100 entidades como máximo.  Si envía varios EGTs simultáneas para procesarlo es importante tooensure esas EGTs no funcionar en entidades que son comunes entre EGTs tal y como se puede retrasar el procesamiento en caso contrario.

EGTs también presentan una solución de compromiso potencial para tooevaluate en el diseño: uso más particiones aumentará la escalabilidad de saludo de la aplicación porque Azure tiene más oportunidades para equilibrar las solicitudes en todos los nodos, pero esto podría limitar Hola capacidad de las transacciones atómicas tooperform de aplicación y mantener la coherencia segura para los datos. Además, hay objetivos de escalabilidad específico en el nivel de Hola de una partición que puede limitar el rendimiento de Hola de las transacciones que se pueden esperar de un solo nodo: para obtener más información acerca de los destinos de escalabilidad de Hola para cuentas de almacenamiento de Azure y tabla de Hola servicio, vea [objetivos de rendimiento y escalabilidad de almacenamiento de Azure](../storage/common/storage-scalability-targets.md). En secciones posteriores de esta guía trata sobre diversas estrategias que le ayudarán a administración ventajas e inconvenientes como éste y comente la mejor toochoose su clave de partición basado en requisitos específicos de saludo de la aplicación de cliente de diseño.  

### <a name="capacity-considerations"></a>Consideraciones de capacidad
Hello tabla siguiente incluyen algunos toobe de valores de clave de hello en cuenta al diseñar una solución de servicio de tabla:  

| Capacidad total de una cuenta de Azure Storage | 500 TB |
| --- | --- |
| Número de tablas en una cuenta de Azure Storage |Limitado solo por la capacidad de Hola de cuenta de almacenamiento de Hola |
| Número de particiones en una tabla |Limitado solo por la capacidad de Hola de cuenta de almacenamiento de Hola |
| Número de entidades de una partición |Limitado solo por la capacidad de Hola de cuenta de almacenamiento de Hola |
| Tamaño de una entidad individual |Una copia de seguridad too1 MB con un máximo de 255 propiedades (incluidos hello **PartitionKey**, **RowKey**, y **Timestamp**) |
| Tamaño de hello **PartitionKey** |Una cadena de seguridad too1 KB de tamaño |
| Tamaño de hello **RowKey** |Una cadena de seguridad too1 KB de tamaño |
| Tamaño de una transacción de un grupo de entidades |Una transacción puede incluir como máximo 100 entidades y carga de hello debe ser inferior a 4 MB de tamaño. Un EGT solo puede actualizar una entidad una vez. |

Para obtener más información, consulte [Hola de entender el modelo de datos del servicio de tabla](http://msdn.microsoft.com/library/azure/dd179338.aspx).  

### <a name="cost-considerations"></a>Consideraciones sobre el coste
Almacenamiento de tabla es relativamente económico, pero debe incluir las estimaciones de costos para ambos cantidad de capacidad de Hola y el uso de transacciones como parte de la evaluación de cualquier solución que utilice el servicio de la tabla de Hola. Sin embargo, en muchos escenarios de almacenamiento de datos duplicados o sin normalizar en hello tooimprove de orden rendimiento o la escalabilidad de la solución es un enfoque válido tootake. Para obtener más información sobre los precios, consulte [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/storage/).  

## <a name="guidelines-for-table-design"></a>Directrices para el diseño de tablas
Estas listas resumen algunas de las instrucciones de clave de hello que debe tener en cuenta al diseñar las tablas y, en esta guía se tratarlas en más detalle más adelante en. Estas instrucciones son muy diferentes de directrices de Hola para ello se usaría normalmente para el diseño de la base de datos relacional.  

Diseñar la toobe de solución de servicio de tabla *leer* eficaz:

* ***Diseño para realizar consultas en aplicaciones con muchas lecturas.*** Al diseñar las tablas, tenga en cuenta las consultas de hello (especialmente Hola latencia de las minúsculas) que va a ejecutar antes de pensar en cómo se actualizarán las entidades. Normalmente esto produce una solución eficiente y de rendimiento.  
* ***Especificar tanto PartitionKey como RowKey en sus consultas.*** *Seleccione las consultas* , como se trata de consultas del servicio de tabla más eficaces de Hola.  
* ***Tenga en cuenta la posibilidad de almacenar copias duplicadas de las entidades.*** Almacenamiento de tabla es barato por lo que puede almacenar Hola misma entidad varias veces (con claves diferentes) tooenable consultas más eficaces.  
* ***Considere la posibilidad de desnormalizar sus datos.*** El almacenamiento en tablas es barato, por tanto, piense en desnormalizar sus datos. Por ejemplo, almacenar entidades de resumen para que las consultas de datos agregados sólo necesitan tooaccess una sola entidad.  
* ***Use valores de clave compuestos.*** Hello solo claves tiene son **PartitionKey** y **RowKey**. Por ejemplo, utilice tooentities de rutas de acceso de valores de clave compuesta tooenable acceso con claves alternativas.  
* ***Use la proyección de consultas.*** Puede reducir la cantidad de Hola de datos que transfieren por red hello mediante el uso de consultas que seleccionan solo los campos de hello que necesarios.  

Diseñar la toobe de solución de servicio de tabla *escribir* eficaz:  

* ***No cree particiones activas.*** Elija las solicitudes de teclas que le permiten toospread en varias particiones en cualquier momento.  
* ***Evite picos de tráfico.*** Suavizar el tráfico de Hola durante un período razonable de tiempo y evitar picos de tráfico.
* ***No es preciso crear necesariamente una tabla independiente para cada tipo de entidad.*** Cuando necesite transacciones atómicas en tipos de entidad, puede almacenar estos varios tipos de entidad en hello igual de partición en hello misma tabla.
* ***Tenga en cuenta que debe lograr el rendimiento máximo Hola.*** Debe tener en cuenta los objetivos de escalabilidad de Hola de hello servicio tabla y asegurarse de que su diseño no hará que tooexceed ellos.  

A medida que lea esta guía, verá ejemplos en los que se ponen en práctica todos estos principios.  

## <a name="design-for-querying"></a>Diseño de consulta
Soluciones de servicio de tabla pueden ser lectura intensiva, escritura intensiva o una combinación de hello dos. En esta sección se centra en hello toobear de cosas en cuenta al diseñar su toosupport de servicio de tabla las operaciones de lectura de forma eficaz. Normalmente, un diseño que admite operaciones de lectura eficazmente también es eficaz para las operaciones de escritura. Sin embargo, hay consideraciones adicionales toobear en cuenta al diseñar toosupport escribir operaciones, descritas en la siguiente sección hello, [diseño para la modificación de datos](#design-for-data-modification).

Un buen punto de partida para diseñar su tooenable de solución de servicio de tabla tooread datos eficazmente están tooask "las consultas que será necesario tooexecute tooretrieve Hola datos de mi aplicación que necesita de hello servicio tabla?"  

> [!NOTE]
> Con hello servicio tabla, es importante tooget Hola correcto de diseño por adelantado porque es difícil y costosa toochange que más adelante. Por ejemplo, en una base de datos relacional a menudo resulta tooaddress posibles problemas de rendimiento mediante la adición de índices de base de datos existente de tooan: no es una opción con hello servicio tabla.  
> 
> 

En esta sección se centra en los problemas clave de Hola que debe tratar al diseñar las tablas para las consultas. Hola los temas tratados en esta sección incluyen:

* [Cómo afecta al rendimiento de las consultas su elección de PartitionKey y RowKey](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [Elegir un PartitionKey apropiado](#choosing-an-appropriate-partitionkey)
* [Optimizar las consultas para hello servicio tabla](#optimizing-queries-for-the-table-service)
* [Ordenar datos en hello servicio tabla](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a>Cómo afecta al rendimiento de las consultas su elección de PartitionKey y RowKey
Hello en los ejemplos siguientes se suponen servicio de la tabla de hello es almacenar entidades employee con hello siguiendo estructura (la mayoría de los ejemplos de hello omite hello **Timestamp** propiedad por motivos de claridad):  

| *Nombre de la columna* | *Tipo de datos* |
| --- | --- |
| **PartitionKey** (nombre de departamento) |String |
| **RowKey** (Identificación de empleado) |String |
| **Nombre** |String |
| **Apellidos** |String |
| **Edad** |Entero |
| **EmailAddress** |String |

Hola sección anterior [Introducción al servicio tabla de Azure](#overview) se describen algunas características clave Hola de hello servicio tabla de Azure que tienen una influencia directa en el diseño de la consulta. Estos dan como resultado de hello siguiendo las directrices generales para diseñar las consultas del servicio tabla. Tenga en cuenta que es sintaxis de filtro de hello usada en ejemplos de hello siguientes desde el servicio de tabla de hello API de REST, para más información, vea [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

* A ***punto consulta*** es toouse de búsqueda más eficaz de Hola y se recomienda toobe utilizada para realizar búsquedas de gran volumen o búsquedas que requieren menor latencia. Este tipo de consulta puede utilizan de manera muy eficaz Hola índices toolocate una entidad individual mediante la especificación de ambos Hola **PartitionKey** y **RowKey** valores. Por ejemplo: $filter=(PartitionKey eq 'Sales') y (RowKey eq '2')  
* En segundo lugar mejor es un ***consulta por rango*** que usa hello **PartitionKey** y filtros en un intervalo de **RowKey** valores tooreturn más de una entidad. Hola **PartitionKey** valor identifica una partición específica y hello **RowKey** valores identifican un subconjunto de las entidades de hello en esa partición. Por ejemplo: $filter=PartitionKey eq 'Sales”, RowKey ge 'S' y RowKey lt 'T'  
* Tercer lo mejor es un ***partición examinar*** que usa hello **PartitionKey** y filtros en otra propiedad de no son de clave y que pueden devolver más de una entidad. Hola **PartitionKey** valor identifica una partición específica, y seleccione un subconjunto de las entidades de hello en esa partición de valores de propiedad de Hola. Por ejemplo: $filter=PartitionKey eq 'Sales' y LastName eq 'Smith'  
* A ***Table Scan*** no incluye hello **PartitionKey** y es muy eficaz ya que busca en todas las particiones de Hola que componen la tabla a su vez para todas las entidades coincidentes. Llevará a cabo un recorrido de tabla, independientemente de si su filtro usa hello **RowKey**. Por ejemplo: $filter=LastName eq 'Jones'  
* Las consultas que devuelven varias entidades las devuelven ordenadas en orden **PartitionKey** y **RowKey**. tooavoid de entidades de hello ordenar de nuevo en el cliente de hello, elija un **RowKey** que define el criterio de ordenación de hello más comunes.  

Tenga en cuenta que cuando se utiliza un "**o**" toospecify un filtro basado en **RowKey** valores da como resultado un examen de la partición y no se trata como una consulta por rango. Por lo tanto, debe evitar las consultas que usan filtros como: $filter=PartitionKey eq 'Sales' y (RowKey eq '121' o RowKey eq '322')  

Para obtener ejemplos de código de cliente que usan consultas eficaces de hello biblioteca cliente de almacenamiento tooexecute, consulte:  

* [Ejecutar una consulta de punto mediante Hola biblioteca cliente de almacenamiento](#executing-a-point-query-using-the-storage-client-library)
* [Recuperar varias entidades con LINQ](#retrieving-multiple-entities-using-linq)
* [Proyección de servidor](#server-side-projection)  

Para obtener ejemplos de código de cliente que puede controlar varios entidad tipos almacenan en hello misma tabla, vea:  

* [Trabajar con tipos de entidad heterogéneos](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a>Elegir un PartitionKey apropiado
La elección de **PartitionKey** debe equilibrar Hola necesidad tooenables Hola utilizar EGTs (tooensure coherencia) contra Hola requisito toodistribute las entidades en varias particiones (tooensure una solución escalable).  

En un extremo, podría almacenar todas las entidades en una sola partición, pero esto puede limitar la escalabilidad de saludo de la solución y evitaría que servicio de la tabla de Hola se pueda tooload-equilibrar las solicitudes. En hello otro extremo, puede almacenar una entidad por partición, lo que sería muy escalable y lo que permite tooload equilibrar las solicitudes del servicio de tabla hello, pero que impiden que se usan transacciones de grupo de entidad.  

Ideal **PartitionKey** es aquel que le permite conseguir consultas eficaces toouse y que tiene suficientes tooensure de particiones, la solución es escalable. Normalmente, encontrará que las entidades tendrán una propiedad adecuada que distribuye las entidades entre particiones suficientes.

> [!NOTE]
> Por ejemplo, en un sistema que almacena información acerca de los usuarios o empleados, el identificador del usuario puede ser un buen PartitionKey. Puede tener varias entidades que utilizan un determinado identificador de usuario como clave de partición de Hola. Cada entidad que almacena los datos de un usuario se agrupa en una sola partición y, de esta manera estas entidades están accesibles a través de las transacciones de grupo de entidad, y continúan siendo altamente escalables.
> 
> 

Existen consideraciones adicionales en su elección de **PartitionKey** que relacionan toohow se insertar, actualizar y eliminar entidades: consulte la sección de hello [diseño para la modificación de datos](#design-for-data-modification) a continuación.  

### <a name="optimizing-queries-for-hello-table-service"></a>Optimizar las consultas para hello servicio tabla
Hola servicio tabla indizará automáticamente las entidades con hello **PartitionKey** y **RowKey** valores en un índice clúster único, por lo tanto, Hola motivo que las consultas de punto se Hola toouse más eficaz . Sin embargo, no hay ningún índice distinto en el índice agrupado de hello en hello **PartitionKey** y **RowKey**.

Muchos diseños deben cumplir con búsqueda de tooenable requisitos de entidades basándose en varios criterios. Por ejemplo, localizar las entidades employee en función de correo electrónico, Id. de empleado o apellido. Hola siguientes patrones en la sección de hello [patrones de diseño de tabla](#table-design-patterns) tratar estos tipos de requisito y se describen las formas de trabajar con los hechos de Hola que el servicio de la tabla de Hola no proporciona índices secundarios:  

* [Patrón de índice secundario intra-partition](#intra-partition-secondary-index-pattern) -almacenar varias copias de cada entidad con diferentes **RowKey** valores (Hola misma partición) tooenable rápidos y eficaces búsquedas y ordenación alternativa se ordena mediante el uso de diferentes **RowKey** valores.  
* [Patrón de índice secundario de partición entre](#inter-partition-secondary-index-pattern) : almacenar varias copias de cada entidad con distintos valores de RowKey en particiones independientes o en tablas independientes tooenable rápida y búsquedas eficaces y ordenación alternativo se ordena mediante el uso de diferentes **RowKey** valores.  
* [Patrón de entidades de índice](#index-entities-pattern) -mantener el índice entidades tooenable búsquedas eficaces que devuelven listas de entidades.  

### <a name="sorting-data-in-hello-table-service"></a>Ordenar datos en hello servicio tabla
Hola servicio tabla devuelve las entidades que se ordenan en orden ascendente según **PartitionKey** y, a continuación, por **RowKey**. Estas claves son valores de cadena y tooensure que los valores numéricos se ordenan correctamente, debe convertirlos tooa fijada de longitud y ellos rellenar con ceros. Por ejemplo, si hello valor de identificador de empleado use como hello **RowKey** es un valor entero, se debe convertir el Id. de empleado **123** demasiado**00000123**.  

Muchas aplicaciones tienen requisitos toouse datos ordenan en un orden diferente: por ejemplo, ordenar los empleados por su nombre, o mediante la combinación de fecha. Hola siguientes patrones en la sección de hello [patrones de diseño de tabla](#table-design-patterns) cómo tooalternate criterios de ordenación para las entidades de direcciones:  

* [Patrón de índice secundario intra-partition](#intra-partition-secondary-index-pattern) -almacenar varias copias de cada entidad con distintos valores de RowKey (Hola misma partición) tooenable rápidos y eficaces búsquedas y ordenación alternativa ordena utilizando diferentes valores de RowKey.  
* [Patrón de índice secundario de partición entre](#inter-partition-secondary-index-pattern) : almacenar varias copias de cada entidad con distintos valores de RowKey en particiones independientes en tablas independientes tooenable rápida y búsquedas eficaces y ordenación alternativo se ordena mediante el uso de diferentes RowKey valores.
* [Patrón de final del registro](#log-tail-pattern) -recuperar hello  *n*  entidades agregan más recientemente tooa partición mediante el uso de un **RowKey** valor que ordena en fecha inversa y orden cronológico.  

## <a name="design-for-data-modification"></a>Diseño para la modificación de datos
En esta sección se centra en las consideraciones de diseño de Hola para optimizar las inserciones, actualizaciones y eliminaciones. En algunos casos, será necesario ventajas y desventajas de tooevaluate Hola entre los diseños que optimizar para realizar una consulta en diseños de optimizar la modificación de datos tal como se hace en diseños de bases de datos relacionales (aunque Hola de técnicas de Hola para administrar el diseño ventajas e inconvenientes son diferentes en una base de datos relacional). Hola sección [patrones de diseño de tabla](#table-design-patterns) se describen algunos modelos de diseño detallado de hello servicio tabla y destaca algunas de estas ventajas e inconvenientes. En la práctica, encontrará que muchos diseños optimizados para consultar entidades también funcionan bien para la modificación de entidades.  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a>Optimizar el rendimiento de Hola de insertar, actualizar y eliminar operaciones
tooupdate o eliminar una entidad, debe ser capaz de tooidentify mediante hello **PartitionKey** y **RowKey** valores. En este sentido, la elección de **PartitionKey** y **RowKey** modificar entidades debe seguir similar criterios tooyour elección toosupport seleccione consultas ya que desea que las entidades de tooidentify como más eficaz posible. No desea toouse una toolocate de examen ineficaz de partición o tabla de una entidad en Hola de orden toodiscover **PartitionKey** y **RowKey** valores necesita tooupdate o eliminarlo.  

Hola siguientes patrones en la sección de hello [patrones de diseño de tabla](#table-design-patterns) dirección de optimizar el rendimiento de Hola o la inserción, actualización y las operaciones de eliminación:  

* [Eliminación del modelo de gran volumen](#high-volume-delete-pattern) -habilitar la eliminación de Hola de un gran volumen de entidades mediante el almacenamiento de todas las entidades de Hola para su eliminación simultánea en su propia tabla independiente; debe eliminar entidades de hello mediante la eliminación de la tabla de Hola.  
* [Modelo de serie de datos](#data-series-pattern) -series de datos completa de almacén en un número de entidad única toominimize Hola de solicitudes que realice.  
* [Patrón de entidades amplia](#wide-entities-pattern) -usar varias entidades lógicas toostore de entidades físicas con más de 252 propiedades.  
* [Patrón de entidades de gran tamaño](#large-entities-pattern) -valores de propiedad grande de toostore de almacenamiento de blob de uso.  

### <a name="ensuring-consistency-in-your-stored-entities"></a>Garantizar la coherencia en las entidades almacenadas
Hola otro factor clave que influye en la elección de las claves para optimizar las modificaciones de datos es cómo tooensure coherencia mediante el uso de transacciones atómicas. Solo puede usar un toooperate EGT en entidades almacenadas en hello misma partición.  

Hola siguientes patrones en la sección de hello [patrones de diseño de tabla](#table-design-patterns) administrar la coherencia de dirección:  

* [Patrón de índice secundario intra-partition](#intra-partition-secondary-index-pattern) -almacenar varias copias de cada entidad con diferentes **RowKey** valores (Hola misma partición) tooenable rápidos y eficaces búsquedas y ordenación alternativa se ordena mediante el uso de diferentes **RowKey** valores.  
* [Patrón de índice secundario de partición entre](#inter-partition-secondary-index-pattern) : almacenar varias copias de cada entidad con distintos valores de RowKey en particiones independientes o en tablas independientes tooenable rápida y búsquedas eficaces y ordenación alternativo se ordena mediante el uso de diferentes **RowKey** valores.  
* [Patrón final coherente de transacciones](#eventually-consistent-transactions-pattern) : habilitar el comportamiento final coherente a través de límites de partición o los límites del sistema de almacenamiento mediante el uso de las colas de Azure.
* [Patrón de entidades de índice](#index-entities-pattern) -mantener el índice entidades tooenable búsquedas eficaces que devuelven listas de entidades.  
* [Patrón de desnormalización](#denormalization-pattern) -combinar los datos relacionados con juntos en una sola entidad tooenable tooretrieve todos los datos que necesita con una consulta de punto único de Hola.  
* [Modelo de serie de datos](#data-series-pattern) -series de datos completa de almacén en un número de entidad única toominimize Hola de solicitudes que realice.  

Para obtener información acerca de las transacciones de grupo de entidad, vea la sección de hello [transacciones de grupo de la entidad](#entity-group-transactions).  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a>Garantizar su diseño para efectuar modificaciones eficientes facilita la realización de consultas eficaces
En muchos casos, un diseño para los resultados de consultas eficaz en modificaciones eficaz, pero siempre debe evaluar si se trata de caso de hello para su escenario concreto. Algunos de los patrones de hello en la sección de hello [patrones de diseño de tabla](#table-design-patterns) explícitamente evaluar ventajas y desventajas de consultar y modificar las entidades, y debe tener siempre en número de Hola de cuenta de cada tipo de operación.  

Hola siguientes patrones en la sección de hello [patrones de diseño de tabla](#table-design-patterns) ventajas y desventajas de diseño para conseguir consultas eficaces y diseño para la modificación de datos eficaz de direcciones:  

* [Patrón de clave compuesta](#compound-key-pattern) -uso compuesta **RowKey** valores tooenable un toolookup de cliente relacionadas con datos con una consulta de punto único.  
* [Patrón de final del registro](#log-tail-pattern) -recuperar hello  *n*  entidades agregan más recientemente tooa partición mediante el uso de un **RowKey** valor que ordena en fecha inversa y orden cronológico.  

## <a name="encrypting-table-data"></a>Cifrado de datos de tablas
Biblioteca de cliente de almacenamiento de Azure .NET admite el cifrado de propiedades de la entidad de cadena para la inserción de Hola y reemplace operaciones. cadenas de Hello cifrado se almacenan en el servicio de hello como propiedades binarias y se convierten toostrings atrás tras la descodificación.    

Para las tablas, además toohello directiva de cifrado, los usuarios deben especificar Hola propiedades toobe cifrado. Para ello, pueden especificar un atributo EncryptProperty (para las entidades POCO que se derivan de TableEntity) o una resolución de cifrado en las opciones de solicitud. Una resolución de cifrado es un delegado que toma una clave de partición, una clave de fila y un nombre de propiedad y devuelve un valor booleano que indica si se debe cifrar dicha propiedad. Durante el cifrado, biblioteca de cliente de hello utilizará esta toodecide información si se debe cifrar una propiedad al escribir el cable toohello. delegado de Hello también proporciona posibilidad de Hola de lógica de alrededor de cómo se cifran las propiedades. (Por ejemplo, si el valor es X, hay que cifrar la propiedad A; en caso contrario, hay que cifrar las propiedades A y B). Tenga en cuenta que TI es tooprovide no es necesario que esta información al leer o consultar entidades.

Tenga en cuenta que actualmente no se admite la combinación. Puesto que un subconjunto de propiedades se puede haber cifrado previamente mediante una clave diferente, simplemente combinar nuevas propiedades de Hola y actualizar metadatos de hello producirá pérdida de datos. Combinar cualquiera requiere servicio adicional de realizar llamadas entidad preexistente de hello tooread del servicio de hello, o mediante una clave nueva por cada propiedad, los cuales no son adecuados por motivos de rendimiento.     

Para información acerca del cifrado de datos de tablas, consulte [Cifrado del lado cliente y Azure Key Vault para Microsoft Azure Storage](../storage/common/storage-client-side-encryption.md).  

## <a name="modelling-relationships"></a>Relaciones de modelos
Creación de modelos de dominio es un paso clave en el diseño de hello sistemas complejos. Por lo general, usa Hola modelización proceso tooidentify entidades y relaciones de hello entre ellos como una manera toounderstand Hola dominio de negocio e informar al diseño de saludo del sistema. En esta sección se centra en cómo puede traducir algunos de los tipos de relación común Hola que se encuentra en toodesigns de modelos de dominio para hello servicio tabla. proceso de Hola de asignación de un lógica tooa de modelo de datos físico NoSQL según modelo de datos es muy diferente del que se utiliza cuando se diseña una base de datos relacional. Diseño de bases de datos relacionales normalmente se da por supuesto un proceso de normalización de datos con optimización para minimizar la redundancia y una capacidad de consulta declarativa que resúmenes Hola la implementación del funcionamiento de la base de datos de Hola.  

### <a name="one-to-many-relationships"></a>Relaciones uno a varios
Las relaciones uno a varios entre los objetos de dominio de negocio se producen con mucha frecuencia: por ejemplo, cuando un departamento tiene muchos empleados. Hay varias relaciones de uno a varios de formas tooimplement en hello servicio tabla cada con ventajas y desventajas que pueden ser relevantes toohello escenario en particular.  

Considere el ejemplo de Hola de una gran empresa multinacional con decenas de miles de departamentos y entidades employee donde cada departamento tiene muchos empleados y cada empleado como asociada a un departamento específico. Un enfoque es toostore independiente departamento y entidades de empleado como los siguientes:  

![][1]

Este ejemplo muestra una relación de uno a varios implícita entre tipos de hello basada en hello **PartitionKey** valor. Cada departamento puede tener muchos empleados.  

En este ejemplo también muestra una entidad de departamento y sus entidades relacionadas empleado en Hola misma partición. Puede elegir toouse distintas particiones, tablas o incluso las cuentas de almacenamiento Hola diferentes tipos de entidad.  

Un enfoque alternativo es toodenormalize las entidades de empleado único almacén y de datos con datos sin normalizar departamento como se muestra en el siguiente ejemplo de Hola. En este escenario en particular, este enfoque sin normalizar no puede Hola recomendada si tiene un requisito toobe toochange capaz de Hola obtener información detallada de un administrador del departamento porque toodo esta operación, necesita tooupdate todos los empleados en el departamento de Hola.  

![][2]

Para obtener más información, vea hello [patrón de desnormalización](#denormalization-pattern) más adelante en esta guía.  

Hello siguiente tabla resume Hola ventajas y desventajas de cada uno de los enfoques de hello descritos anteriormente para almacenar los empleados y las entidades de departamento que tienen una relación uno a varios. También debería considerar la frecuencia con que espera tooperform varias operaciones: puede ser aceptable toohave un diseño que incluye una operación costosa si esa operación solo se produce con poca frecuencia.  

<table>
<tr>
<th>Enfoque</th>
<th>Ventajas</th>
<th>Desventajas</th>
</tr>
<tr>
<td>Tipos de entidad independientes, la misma partición, la misma tabla</td>
<td>
<ul>
<li>Puede actualizar una entidad de departamento con una sola operación.</li>
<li>Puede usar una coherencia de toomaintain EGT si tiene un requisito toomodify una entidad department cada vez que se actualizaciones, inserciones y eliminaciones una entidad empleado. Por ejemplo, si mantiene un recuento de empleado del departamento para cada departamento.</li>
</ul>
</td>
<td>
<ul>
<li>Puede necesitar tooretrieve un empleado y una entidad de departamento para algunas actividades de cliente.</li>
<li>Almacenamiento llevan a cabo operaciones en hello misma partición. Con volúmenes de transacciones elevados, esto puede producir un punto de conflicto.</li>
<li>No se puede mover un empleado tooa nuevo departamento con un EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Tipos de entidad independientes, particiones o tablas distintas o cuentas de almacenamiento</td>
<td>
<ul>
<li>Puede actualizar una entidad de departamento o de empleado con una sola operación.</li>
<li>En los volúmenes de transacciones alta, esto puede ayudar a spread Hola carga entre varias particiones.</li>
</ul>
</td>
<td>
<ul>
<li>Puede necesitar tooretrieve un empleado y una entidad de departamento para algunas actividades de cliente.</li>
<li>No se puede utilizar EGTs toomaintain coherencia cuando se actualizaciones, inserciones y eliminaciones un empleado y un departamento de la actualización. Por ejemplo, actualizando un recuento de empleados en una entidad de departamento.</li>
<li>No se puede mover un empleado tooa nuevo departamento con un EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Desnormalizar en un único tipo de entidad</td>
<td>
<ul>
<li>Puede recuperar toda la información de Hola que necesita con una única solicitud.</li>
</ul>
</td>
<td>
<ul>
<li>Puede ser costoso toomaintain coherencia si necesita información de departamento tooupdate (Esto requeriría tooupdate todos los empleados de Hola de un departamento).</li>
</ul>
</td>
</tr>
</table>

Cómo elegir entre estas opciones y que los profesionales de TI de Hola e inconvenientes son más significativos, depende de los escenarios de aplicación específica. Por ejemplo, ¿con qué frecuencia modificar entidades de departamento; es necesario todas las consultas de empleado Hola departamento una información suplementaria; ¿grado de aproximación son límites de escalabilidad de toohello en las particiones o la cuenta de almacenamiento?  

### <a name="one-to-one-relationships"></a>Relaciones uno a uno
Es posible que los modelos de dominio incluyan relaciones uno a uno entre las entidades. Si necesita tooimplement una relación uno a uno en hello servicio tabla, también debe elegir cómo toolink Hola dos entidades relacionadas cuando necesite tooretrieve ambos. Este vínculo puede ser implícita, en función de una convención de valores de clave de Hola o explícita mediante el almacenamiento de un vínculo en forma de Hola de **PartitionKey** y **RowKey** valores de cada entidad tooits entidades relacionan. Para obtener información sobre si debe almacenar hello las entidades relacionadas en Hola la misma partición, vea la sección de hello [uno a varios relaciones](#one-to-many-relationships).  

Tenga en cuenta que también existen consideraciones de implementación que puedan provocar relaciones uno a uno tooimplement en servicio de la tabla de hello:  

* Administración de entidades de gran tamaño (para obtener más información, consulte [Patrón de entidades de gran tamaño](#large-entities-pattern)).  
* Implementación de controles de acceso (para más información, consulte [Control de acceso con firmas de acceso compartido](#controlling-access-with-shared-access-signatures)).  

### <a name="join-in-hello-client"></a>Combinación en el cliente de Hola
Aunque existen relaciones de formas toomodel Hola servicio tabla, no debe olvidar que Hola dos razones principales para utilizar el servicio de la tabla de hello son escalabilidad y rendimiento. Si encuentra que se modelización muchas relaciones que poner en peligro Hola rendimiento y escalabilidad de la solución, debe pregúntese lo siguiente: si es necesario toobuild todas Hola relaciones de datos al diseño de la tabla. Puede toosimplify capaz de diseño de Hola y mejorar la escalabilidad de Hola y rendimiento de la solución si permite que la aplicación cliente realizar las operaciones de combinación necesarios.  

Por ejemplo, si tiene tablas pequeñas que contienen datos que no cambian con frecuencia, puede recuperar estos datos una vez y almacenarla en la caché de cliente de Hola. Esto puede evitar los repetidos idas y vueltas tooretrieve Hola los mismos datos. En los ejemplos de hello que hemos examinado en esta guía, hello conjunto de departamentos en una organización pequeña es probable toobe pequeño y cambie con poca frecuencia lo que un buen candidato para datos de la aplicación cliente puede descargar una vez y la memoria caché como datos de búsqueda.  

### <a name="inheritance-relationships"></a>Relaciones de herencia
Si la aplicación cliente usa un conjunto de clases que forman parte de una herencia relación toorepresent las entidades empresariales, puede conservar fácilmente las entidades en hello servicio tabla. Por ejemplo, podría tener Hola siguiendo el conjunto de clases definidas en la aplicación cliente donde **persona** es una clase abstracta.

![][3]

Puede conservar las instancias de dos clases concretas Hola Hola servicio tabla utilizando una sola tabla de persona con entidades en ese aspecto similar al siguiente:  

![][4]

Para obtener más información sobre cómo trabajar con varios tipos de entidad en la misma tabla en el código de cliente de hello, vea la sección de hello [trabajar con tipos de entidades heterogéneas](#working-with-heterogeneous-entity-types) más adelante en esta guía. Esto proporciona ejemplos de cómo toorecognize Hola tipo de entidad en el código de cliente.  

## <a name="table-design-patterns"></a>Patrones de diseño de tabla
En las secciones anteriores, ha visto algunas explicaciones detalladas acerca de cómo toooptimize la tabla de diseño para ambos al recuperar datos de la entidad mediante consultas y para insertar, actualizar y eliminar datos de la entidad. En esta sección se describen algunos modelos adecuados para usarse con soluciones de Table service. Además, verá cómo puede prácticamente solucionar algunos problemas de Hola y ventajas e inconvenientes generados anteriormente en esta guía. Hello diagrama siguiente resume Hola relaciones entre los distintos patrones de hello:  

![][5]

mapa de patrón de Hello anteriormente resalta algunas relaciones entre patrones (azules) y antipatrones (naranja) que se documentan en esta guía. Por supuesto, existen muchos otros patrones que merece la pena tener en cuenta. Por ejemplo, uno de los escenarios clave de hello para el servicio tabla es hello toouse [materializar el patrón de vista](https://msdn.microsoft.com/library/azure/dn589782.aspx) de hello [segregación de responsabilidad de consulta de comandos (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) patrón.  

### <a name="intra-partition-secondary-index-pattern"></a>Patrón de índice secundario dentro de la partición
Almacenar varias copias de cada entidad con diferentes **RowKey** valores (Hola misma partición) tooenable rápidos y eficaces búsquedas y ordenación alternativa se ordena mediante diferentes **RowKey** valores. La coherencia de las actualizaciones entre copias se puede mantener mediante EGT.  

#### <a name="context-and-problem"></a>Contexto y problema
Hola servicio tabla indizará automáticamente entidades mediante hello **PartitionKey** y **RowKey** valores. Esto permite a un tooretrieve de aplicación de cliente en una entidad eficazmente con estos valores. Por ejemplo, mediante la estructura de tabla de Hola se muestra a continuación, una aplicación cliente puede utilizar un tooretrieve de consulta de punto de una entidad de empleados individuales utilizando el nombre del departamento de Hola y el Id. de empleado de hello (hello **PartitionKey** y  **RowKey** valores). Un cliente también puede recuperar las entidades ordenadas por identificador de empleado dentro de cada departamento.

![][6]

Si también desea toobe capaz toofind una entidad de empleado según Hola valor de otra propiedad, como la dirección de correo electrónico, debe usar un toofind de examen de partición menos eficaz una coincidencia. Esto es porque el servicio de la tabla de hello no proporciona índices secundarios. Además, no hay ninguna opción toorequest una lista de empleados ordenados en un orden diferente del **RowKey** orden.  

#### <a name="solution"></a>Solución
toowork alrededor de falta de Hola de índices secundarios, puede almacenar varias copias de cada entidad con cada copia con otro **RowKey** valor. Si almacena una entidad con estructuras de Hola que se muestra a continuación, puede recuperar eficazmente entidades de empleado basándose en el identificador de empleado o de dirección de correo electrónico. Hola valores de prefijo para hello **RowKey**, "empid_" y "email_" permiten tooquery en un único empleado o un intervalo de empleados mediante el uso de un intervalo de direcciones de correo electrónico o Id. de empleados.  

![][7]

Hola siguiendo dos criterios de filtro (uno Buscar por Id. de empleado y una búsqueda por dirección de correo electrónico) ambos especifica consultas de punto:  

* $filter=(PartitionKey eq 'Sales') y (RowKey eq 'empid_000223')  
* $filter=(PartitionKey eq 'Sales') y (RowKey eq 'email_jonesj@contoso.com')  

Si se consulta para un intervalo de entidades de empleado, puede especificar un intervalo ordenado en orden de Id. de empleado o un intervalo que se ordenan en orden de la dirección de correo electrónico mediante una consulta para entidades con prefijo adecuado de Hola Hola **RowKey**.  

* usan de todos los empleados de Hola Hola departamento de ventas con un identificador de empleado en hello intervalo 000100 too000199 toofind: $filter = (PartitionKey eq 'Ventas') y (RowKey ge 'empid_000100') y (RowKey le 'empid_000199')  
* toofind todos Hola empleados Hola departamento de ventas con una dirección de correo electrónico a partir de hello letra 'a' uso: $filter = (PartitionKey eq 'Ventas') y (RowKey ge 'email_a') y (RowKey lt 'email_b')  
  
  Observe que la sintaxis de filtro de hello usada en ejemplos de hello anteriores es de servicio de tabla de hello API de REST, para más información, vea [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* Almacenamiento de tabla es relativamente barato toouse para que hello costo sobrecarga de almacenamiento de datos duplicados no debe ser un gran problema. Sin embargo, debe siempre se evalúan costo Hola del diseño según sus requisitos de almacenamiento previstas y solo agregar entidades duplicadas toosupport Hola consultas que se ejecutará la aplicación cliente.  
* Como entidades de índice secundario de Hola se almacenan en hello igual de partición como entidades de hello original, debes asegurarte de que no superen los objetivos de escalabilidad de Hola para una partición individual.  
* Puede mantener las entidades duplicadas sean coherentes entre sí utilizando las dos copias de hello del tooupdate de EGTs de entidad de Hola de forma atómica. Esto implica que debe almacenar todas las copias de una entidad en hello misma partición. Para obtener más información, vea la sección de hello [usando transacciones de grupo de la entidad](#entity-group-transactions).  
* Hola valor utilizado para hello **RowKey** debe ser único para cada entidad. Considere la posibilidad de usar valores de clave compuestos.  
* Relleno de valores numéricos en hello **RowKey** (por ejemplo, Id. de empleado de hello 000223) permite corregir para ordenar y filtrar según superior e inferior.  
* No es necesariamente necesario tooduplicate todas las propiedades de saludo de la entidad. Por ejemplo, si hello las consultas que enviar por correo electrónico en entidades de búsqueda hello mediante Hola dirección en hello **RowKey** nunca tendrá la edad del empleado de hello, estas entidades pudieron tener Hola siguiendo estructura:

![][8]

* Es mejor normalmente toostore los datos duplicados y asegurarse de que puede recuperar todos los datos de Hola que necesita con una sola consulta, que toouse una consulta toolocate requiere datos de una entidad y otro hello toolookup.  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Use este patrón cuando la aplicación cliente necesita entidades tooretrieve mediante una variedad de claves diferentes, cuando el cliente necesita tooretrieve entidades en distintos criterios de ordenación, y donde se puede identificar cada entidad con una variedad de valores únicos. Sin embargo, debe asegurarse de que no superan los límites de escalabilidad de partición de hello al realizar búsquedas de entidad usando Hola diferentes **RowKey** valores.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Patrón de índice secundario entre particiones](#inter-partition-secondary-index-pattern)
* [Patrón de clave compuesta](#compound-key-pattern)
* [Transacciones de grupos de entidades](#entity-group-transactions)
* [Trabajar con tipos de entidad heterogéneos](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a>Patrón de índice secundario entre particiones
Almacenar varias copias de cada entidad con diferentes **RowKey** valores en particiones independientes o en tablas independientes tooenable rápidos y eficaces las búsquedas y ordenación alternativos mediante diferentes **RowKey**valores.  

#### <a name="context-and-problem"></a>Contexto y problema
Hola servicio tabla indizará automáticamente entidades mediante hello **PartitionKey** y **RowKey** valores. Esto permite a un tooretrieve de aplicación de cliente en una entidad eficazmente con estos valores. Por ejemplo, mediante la estructura de tabla de Hola se muestra a continuación, una aplicación cliente puede utilizar un tooretrieve de consulta de punto de una entidad de empleados individuales utilizando el nombre del departamento de Hola y el Id. de empleado de hello (hello **PartitionKey** y  **RowKey** valores). Un cliente también puede recuperar las entidades ordenadas por identificador de empleado dentro de cada departamento.  

![][9]

Si también desea toobe capaz toofind una entidad de empleado según Hola valor de otra propiedad, como la dirección de correo electrónico, debe usar un toofind de examen de partición menos eficaz una coincidencia. Esto es porque el servicio de la tabla de hello no proporciona índices secundarios. Además, no hay ninguna opción toorequest una lista de empleados ordenados en un orden diferente del **RowKey** orden.  

Se anticipan un volumen elevado de transacciones en estas entidades y desea riesgo de hello toominimize de hello limitación del cliente de servicio de tabla.  

#### <a name="solution"></a>Solución
toowork alrededor de falta de Hola de índices secundarios, puede almacenar varias copias de cada entidad con cada copia con diferentes **PartitionKey** y **RowKey** valores. Si almacena una entidad con estructuras de Hola que se muestra a continuación, puede recuperar eficazmente entidades de empleado basándose en el identificador de empleado o de dirección de correo electrónico. Hola valores de prefijo para hello **PartitionKey**, "empid_" y "email_" permiten tooidentify que índice al que desea toouse para una consulta.  

![][10]

Hola siguiendo dos criterios de filtro (uno Buscar por Id. de empleado y una búsqueda por dirección de correo electrónico) ambos especifica consultas de punto:  

* $filter=(PartitionKey eq 'empid_Sales') y (RowKey eq '000223')
* $filter=(PartitionKey eq 'email_Sales') y (RowKey eq 'jonesj@contoso.com')  

Si se consulta para un intervalo de entidades de empleado, puede especificar un intervalo ordenado en orden de Id. de empleado o un intervalo que se ordenan en orden de la dirección de correo electrónico mediante una consulta para entidades con prefijo adecuado de Hola Hola **RowKey**.  

* Hola a toofind Hola a todos los empleados en el departamento de ventas con un identificador de empleado en el intervalo de hello **000100** demasiado**000199** ordenados en uso de orden de Id. de empleado: $filter = (PartitionKey eq ' empid_Sales') y (ge RowKey ' 000100') y (RowKey le '000199')  
* toofind uso de orden de dirección de correo electrónico todos los empleados de Hola Hola departamento de ventas con una dirección de correo electrónico que empieza con 'a' ordenada en: $filter = (PartitionKey eq ' email_Sales') y (ge RowKey 'a') y (RowKey lt 'b')  

Observe que la sintaxis de filtro de hello usada en ejemplos de hello anteriores es de servicio de tabla de hello API de REST, para más información, vea [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* Puede mantener las entidades duplicadas finalmente sean coherentes entre sí mediante el uso de hello [patrón coherente transacciones](#eventually-consistent-transactions-pattern) entidades de toomaintain Hola índice principal y secundaria.  
* Almacenamiento de tabla es relativamente barato toouse para que hello costo sobrecarga de almacenamiento de datos duplicados no debe ser un gran problema. Sin embargo, debe siempre se evalúan costo Hola del diseño según sus requisitos de almacenamiento previstas y solo agregar entidades duplicadas toosupport Hola consultas que se ejecutará la aplicación cliente.  
* Hola valor utilizado para hello **RowKey** debe ser único para cada entidad. Considere la posibilidad de usar valores de clave compuestos.  
* Relleno de valores numéricos en hello **RowKey** (por ejemplo, Id. de empleado de hello 000223) permite corregir para ordenar y filtrar según superior e inferior.  
* No es necesariamente necesario tooduplicate todas las propiedades de saludo de la entidad. Por ejemplo, si hello las consultas que enviar por correo electrónico en entidades de búsqueda hello mediante Hola dirección en hello **RowKey** nunca tendrá la edad del empleado de hello, estas entidades pudieron tener Hola siguiendo estructura:
  
  ![][11]
* Es normalmente mejores datos duplicados toostore y asegúrese de que se pueden recuperar todos los datos de Hola que necesita con una única consulta de toouse una consulta toolocate una entidad con Hola índice secundario y otro toolookup Hola datos necesarios en el índice principal de Hola.  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Use este patrón cuando la aplicación cliente necesita entidades tooretrieve mediante una variedad de claves diferentes, cuando el cliente necesita tooretrieve entidades en distintos criterios de ordenación, y donde se puede identificar cada entidad con una variedad de valores únicos. Utilice este patrón cuando desee tooavoid exceder el límite de escalabilidad de partición de hello al realizar búsquedas de entidad usando Hola diferentes **RowKey** valores.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Patrón final coherente de transacciones](#eventually-consistent-transactions-pattern)  
* [Patrón de índice secundario dentro de la partición](#intra-partition-secondary-index-pattern)  
* [Patrón de clave compuesta](#compound-key-pattern)  
* [Transacciones de grupos de entidades](#entity-group-transactions)  
* [Trabajar con tipos de entidad heterogéneos](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a>Patrón final coherente de transacciones
Habilitar el comportamiento final coherente a través de límites de partición o los límites del sistema de almacenamiento mediante el uso de las colas de Azure.  

#### <a name="context-and-problem"></a>Contexto y problema
EGTs Habilitar transacciones atómicas en varias entidades que comparten Hola misma clave de partición. Por motivos de escalabilidad y rendimiento, podría decidir toostore entidades que tienen requisitos de coherencia en particiones independientes o en un sistema de almacenamiento independiente: en este escenario, no puede usar EGTs toomaintain coherencia. Por ejemplo, podría tener una coherencia definitiva de requisito toomaintain entre:  

* Entidades almacenadas en dos particiones diferentes en la misma tabla, en tablas diferentes, en diferentes cuentas de almacenamiento de Hola.  
* Una entidad que se almacenan en hello servicio tabla y un blob almacenado en hello servicio Blob.  
* Una entidad que se almacenan en el servicio de la tabla de Hola y un archivo en un sistema de archivos.  
* Una entidad almacenar en hello servicio tabla aún indizarse utilizando el servicio de búsqueda de Azure Hola.  

#### <a name="solution"></a>Solución
Mediante el uso de las colas de Azure, puede implementar una solución que ofrece coherencia final entre dos o más particiones o sistemas de almacenamiento.
tooillustrate este enfoque, suponga que tiene un requisito toobe tooarchive pueda antiguo empleado las entidades. Las entidades de empleado antiguas rara vez se consultan y deben excluirse de las actividades relacionadas con los empleados actuales. tooimplement este requisito almacenar empleados activos en hello **actual** tabla y antiguos empleados en hello **archivo** tabla. Archivar un empleado requiere toodelete entidad Hola Hola **actual** de tabla y agregue Hola entidad toohello **archivo** tabla, pero no se puede usar un tooperform EGT estas dos operaciones. riesgo de hello tooavoid que un error provoca una entidad tooappear de tablas de ambos o ninguno, operación de almacenamiento de hello debe ser coherente. Hello diagrama de secuencia siguiente describe los pasos de hello en esta operación. Para las rutas de acceso de excepción en el texto que siga Hola se proporcionan más detalles.  

![][12]

Un cliente inicia la operación de almacenamiento de hello colocando un mensaje en una cola de Azure, en este empleado de ejemplo tooarchive #456. Un rol de trabajo sondea la cola de hello si hay mensajes nuevos; Cuando encuentra uno, lee el mensaje de bienvenida y deja una copia oculta en la cola de Hola. rol de trabajo de Hola a continuación recupera una copia de entidad de Hola de hello **actual** de tabla, se inserta una copia en hello **archivo** tabla y, a continuación, elimina Hola original de Hola **actual**tabla. Por último, si no hubiera ningún error de los pasos anteriores de hello, rol de trabajo de hello elimina mensajes de bienvenida del oculto de cola de Hola.  

En este ejemplo, el paso 4 inserta empleado Hola Hola **archivo** tabla. Podría agregar tooa blob de empleado de Hola Hola servicio Blob o un archivo en un sistema de archivos.  

#### <a name="recovering-from-failures"></a>Recuperación de errores
Es importante que las operaciones en los pasos de Hola **4** y **5** debe ser *idempotente* en caso de rol de trabajo de hello necesita operación de almacenamiento de toorestart Hola. Si está utilizando el servicio de tabla de hello, para el paso **4** debe usar una operación "Insertar o reemplazar"; para el paso **5** debe usar un "eliminar si existe" operación en la biblioteca de cliente de Hola que usa. Si está utilizando otro sistema de almacenamiento, debe utilizar una operación idempotente adecuada.  

Si el rol de trabajo de hello nunca completa el paso **6**, a continuación, después vuelve a aparecer un mensaje de saludo de tiempo de espera en cola Hola prepararla para hello trabajo rol tootry tooreprocess. rol de trabajo de Hello puede comprobar cuántas veces se ha leído un mensaje en cola de hello y, si es necesario, marca es un mensaje "dudoso" con fines de investigación enviando tooa separa la cola. Para obtener más información acerca de la lectura de cola de mensajes y la comprobación Hola recuento de eliminación de cola, vea [Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx).  

Algunos errores de los servicios de tabla y cola de hello son errores transitorios y la aplicación cliente debe incluir toohandle de lógica de reintento adecuado ellos.  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* Esta solución no permite el aislamiento de las transacciones. Por ejemplo, un cliente podría leer hello **actual** y **archivo** tablas al rol de trabajo de hello estuvo entre pasos **4** y **5**así como un vista incoherente de los datos de Hola. Tenga en cuenta que los datos de hello será coherentes al final.  
* Asegúrese de que los pasos 4 y 5 son idempotentes en coherencia definitiva de orden tooensure.  
* Puede escalar la solución de hello mediante el uso de varias colas e instancias de rol de trabajo.  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Utilice este patrón cuando desee tooguarantee coherencia definitiva entre las entidades que existen en las distintas particiones o tablas. Puede extender esta coherencia definitiva tooensure de patrón para las operaciones en el servicio de tabla de Hola y servicio de Blob de Hola y otros orígenes de datos de almacenamiento que no sea de Azure como sistema de archivos de base de datos o hello.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Transacciones de grupos de entidades](#entity-group-transactions)  
* [Combinar o reemplazar](#merge-or-replace)  

> [!NOTE]
> Si el aislamiento de transacciones es importante tooyour solución, considere la posibilidad de volver a diseñar la tooenable de tablas le toouse EGTs.  
> 
> 

### <a name="index-entities-pattern"></a>Patrón de entidades de índice
Mantener el índice entidades tooenable búsquedas eficaces que devuelven listas de entidades.  

#### <a name="context-and-problem"></a>Contexto y problema
Hola servicio tabla indizará automáticamente entidades mediante hello **PartitionKey** y **RowKey** valores. Esto permite un tooretrieve de aplicación cliente una entidad de forma eficaz con una consulta de punto. Por ejemplo, mediante la estructura de tabla de Hola se muestra a continuación, una aplicación cliente puede eficazmente recuperar una entidad empleado individual mediante el nombre del departamento de Hola y el Id. de empleado de hello (hello **PartitionKey** y **RowKey** ).  

![][13]

Si también desea toobe tooretrieve capaz de obtener una lista de entidades de empleado según Hola valor de otra propiedad no es único, como su apellido, debe usar una partición menos eficiente examinar toofind coincidencias, en lugar de utilizar un índice toolook ellos una copia de seguridad directamente. Esto es porque el servicio de la tabla de hello no proporciona índices secundarios.  

#### <a name="solution"></a>Solución
búsqueda de tooenable por apellido con estructura de la entidad de hello mostrado anteriormente, debe mantener listas de identificadores de empleado. Si desea que las entidades de tooretrieve Hola empleado con un apellido determinado, como Jones, debe encontrar primero lista Hola de identificadores de empleado para los empleados con Jones como su apellido y, a continuación, recuperar las entidades del empleado. Hay tres opciones principales para almacenar listas de Hola de Id. de empleados:  

* Utilice Blob Storage.  
* Crear entidades de índice en hello igual de partición como entidades de empleado de Hola.  
* Cree entidades de índice en una tabla o una partición independiente.  

<u>Opción n.º 1: Usar el almacenamiento de blobs</u>  

Para la primera opción hello, crear un blob para cada nombre único de la última y, en cada almacén de blobs una lista de hello **PartitionKey** (departamento) y **RowKey** valores (Id. de empleado) para los empleados que tienen que última nombre. Cuando agrega o elimina a un empleado debe asegurarse de que el contenido de Hola del blob relevantes de Hola es coherente con las entidades de empleado de Hola.  

<u>Opción #2:</u> crear entidades de índice en Hola misma partición  

Para la segunda opción hello, utilice entidades de índice que almacenan Hola datos siguientes:  

![][14]

Hola **EmployeeIDs** propiedad contiene una lista de identificadores de empleado para los empleados con apellidos de hello almacenados en hello **RowKey**.  

Hello pasos siguientes describen proceso Hola que deben seguir al agregar un nuevo empleado si usas la segunda opción de Hola. En este ejemplo, vamos a agregar a un empleado cuyo Id. de 000152 y un apellido Jones Hola departamento de ventas:  

1. Recuperar Hola índice entidad con un **PartitionKey** valor hello y "Ventas" **RowKey** valor "Jones". Guardar Hola ETag de este toouse de entidad en el paso 2.  
2. Crear una transacción de grupo de entidad (es decir, una operación por lotes) que inserta la nueva entidad de empleado hello (**PartitionKey** valor "Ventas" y **RowKey** valor "000152"), y las actualizaciones de Hola entidad índice ( **PartitionKey** valor "Ventas" y **RowKey** valor "Jones") mediante la adición de hello nueva employee id toohello lista en el campo de EmployeeIDs Hola. Para obtener información sobre EGT, consulte la sección [Transacciones de grupo de entidad (EGT)](#entity-group-transactions).  
3. Si se produce un error en la transacción de grupo de entidades de hello debido a un error de simultaneidad optimista (otra persona se acaba de modificar entidad del índice de hello), a continuación, necesitará toostart sobre en el paso 1 nuevo.  

Puede usar un toodeleting enfoque similar un empleado si usas la segunda opción de Hola. Cambiar el apellido de un empleado es ligeramente más complejo, ya que necesitará tooexecute una transacción de grupo de entidades que actualiza tres entidades: Hola entidad employee, la entidad de índice de Hola para apellido anterior hello y la entidad de índice de Hola para apellido nuevo Hola. Se debe recuperar cada entidad antes de realizar cambios en el orden de valores de ETag de hello tooretrieve que, a continuación, puede usar tooperform Hola actualizaciones mediante el uso de simultaneidad optimista.  

Hello pasos siguientes describen proceso Hola que deben seguir cuando necesite toolook todos los empleados de hello con un apellido determinado de un departamento si usas la segunda opción de Hola. En este ejemplo, estamos buscando todos los empleados de hello con apellido Jones Hola departamento de ventas:  

1. Recuperar Hola índice entidad con un **PartitionKey** valor hello y "Ventas" **RowKey** valor "Jones".  
2. Analizar la lista de Hola de identificadores de campo de EmployeeIDs Hola de empleado.  
3. Si necesita información adicional sobre cada uno de estos empleados (por ejemplo, sus direcciones de correo electrónico), recuperar cada una de las entidades de empleado de hello mediante **PartitionKey** valor "Ventas" y **RowKey** los valores de lista de Hola de empleados que obtuvo en el paso 2.  

<u>Opción n.º 3:</u> crear entidades de índice en una tabla o partición independientes  

Para la tercera opción hello, utilice entidades de índice que almacenan Hola datos siguientes:  

![][15]

Hola **EmployeeIDs** propiedad contiene una lista de identificadores de empleado para los empleados con apellidos de hello almacenados en hello **RowKey**.  

Con la tercera opción hello, no puede usar EGTs toomaintain coherencia porque entidades de índice de Hola se encuentran en una partición independiente de las entidades de empleado de Hola. Debe asegurarse de que las entidades de índice de hello son coherentes con las entidades de employee Hola.  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* Esta solución requiere entidades de búsqueda de coincidencias de tooretrieve de al menos dos consultas: una tooquery Hola índice tooobtain Hola lista de entidades de **RowKey** valores y, a continuación, consulta tooretrieve cada entidad en la lista de Hola.  
* Dado que una entidad individual tiene un tamaño máximo de 1 MB, opción #2 y opción #3 en soluciones de hello asumir esa lista Hola de identificadores de empleado para cualquier apellido determinado nunca es mayor que 1 MB. Si lista Hola de Id. de empleados es probable toobe mayor que 1 MB de tamaño, utilice la opción #1 y almacenar datos de índice de hello en almacenamiento de blobs.  
* Si utiliza la opción #2 (mediante EGTs toohandle agregando y eliminando a los empleados y cambiando el apellido de un empleado), debe evaluar si el volumen de Hola de transacciones aproximan a los límites de escalabilidad de hello en una partición determinada. Si éste es el caso de hello, debería considerar una solución coherente (opción #1 o #3) que utiliza colas toohandle Hola actualización las solicitudes y permite toostore las entidades de índice en una partición independiente de las entidades de empleado de Hola.  
* Opción #2 en esta solución se da por supuesto que desea toolook por apellido dentro de un departamento: por ejemplo, desea tooretrieve una lista de empleados que tienen un apellido Jones Hola departamento de ventas. Si desea que toobe toolook capaz de seguridad de todos los empleados de hello cuyo apellido Jones en toda organización de hello, use la opción #1 u opción #3.
* Puede implementar una solución basada en cola que ofrece la coherencia definitiva (vea hello [patrón coherente transacciones](#eventually-consistent-transactions-pattern) para obtener más detalles).  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Utilice este patrón cuando desee toolookup un conjunto de entidades que comparten un valor de propiedad común, como todos los empleados con apellidos Hola Jones.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Patrón de clave compuesta](#compound-key-pattern)  
* [Patrón final coherente de transacciones](#eventually-consistent-transactions-pattern)  
* [Transacciones de grupos de entidades](#entity-group-transactions)  
* [Trabajar con tipos de entidad heterogéneos](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a>Patrón de desnormalización
Combinar datos relacionados entre sí en una sola entidad tooenable tooretrieve todos los datos que necesita con una consulta de punto único de Hola.  

#### <a name="context-and-problem"></a>Contexto y problema
En una base de datos relacional, normalmente se normalizan desduplicación de datos tooremove resultante en las consultas que recuperan datos de varias tablas. Si normalizar los datos en tablas de Azure, debe realizar varias acciones de ida y vuelta de hello cliente toohello server tooretrieve los datos relacionados. Por ejemplo, con estructura de tabla de Hola se muestra a continuación necesitan dos redondear detalles de hello tooretrieve de viajes de un departamento: entidad de departamento de hello uno toofetch que incluye el identificador del Administrador de hello y, a continuación, otra solicitud toofetch Hola de detalles del Administrador de un empleado entidad.  

![][16]

#### <a name="solution"></a>Solución
En lugar de almacenar datos de hello en dos entidades independientes, reducir la normalización de datos de Hola y conservar una copia de los detalles del Administrador de hello en entidad department de Hola. Por ejemplo:  

![][17]

Con las entidades de departamento almacenadas con estas propiedades, ahora puede recuperar todos los detalles de Hola que necesite acerca de un departamento mediante una consulta de punto.  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* Hay algunos costes de sobrecarga asociados al almacenamiento de datos dos veces. ventajas de rendimiento (resultantes de los servicios de almacenamiento de menos solicitudes toohello) normalmente Hello compensan aumento marginal de hello en los costos de almacenamiento (y parcialmente se compensa este costo por una reducción del número de Hola de transacciones requieren detalles de hello toofetch de un departamento).  
* Debe mantener la coherencia de Hola de entidades de dos de Hola que almacenan información acerca de los administradores. Puede controlar el problema de coherencia de hello mediante EGTs tooupdate varias entidades en una única transacción atómica: en este caso, se almacenan entidad department de Hola y entidad de empleado de hello para el administrador del departamento de Hola Hola misma partición.  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Utilice este patrón cuando sea necesario con frecuencia toolook información relacionada. Este patrón reduce la cantidad de Hola de las consultas que el cliente debe realizar datos de hello tooretrieve requiere.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Patrón de clave compuesta](#compound-key-pattern)  
* [Transacciones de grupos de entidades](#entity-group-transactions)  
* [Trabajar con tipos de entidad heterogéneos](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a>Patrón de clave compuesta
Use compuesta **RowKey** valores tooenable un toolookup de cliente relacionadas con datos con una consulta de punto único.  

#### <a name="context-and-problem"></a>Contexto y problema
En una base de datos relacional, resulta bastante natural toouse combinaciones en las consultas tooreturn relacionadas con elementos de cliente de toohello de datos en una única consulta. Por ejemplo, podría usar toolook de Id. de empleado de hello una lista de entidades relacionadas que contienen el rendimiento y revisar los datos para ese empleado.  

Supongamos que está almacenando las entidades employee en servicio de la tabla de hello utilizando Hola siguiendo la estructura:  

![][18]

También necesita toostore datos históricos relacionados con tooreviews y rendimiento para cada empleado de hello año ha funcionado para su organización y necesita toobe pueda tooaccess esta información por año. Una opción es toocreate otra tabla que almacena las entidades con hello siguiente estructura:  

![][19]

Tenga en cuenta que con este enfoque, puede decidir tooduplicate cierta información (por ejemplo, nombre y apellidos) en hello nueva entidad tooenable tooretrieve los datos con una sola solicitud. Sin embargo, no se puede mantener la coherencia segura porque no puede usar un dos entidades EGT tooupdate Hola de forma atómica.  

#### <a name="solution"></a>Solución
Almacenar un nuevo tipo de entidad en la tabla original con entidades Hola siguiente estructura:  

![][20]

Tenga en cuenta cómo Hola **RowKey** es ahora una clave compuesta formada por Id. de empleado de Hola y Hola año con datos de la revisión de Hola que le permite tooretrieve Hola rendimiento del empleado y revisar los datos con una única solicitud para una sola entidad.  

Hola de ejemplo siguiente describe cómo se pueden recuperar todos los datos de revisión de Hola para un empleado concreto (por ejemplo, employee 000123 Hola departamento de ventas):  

$filter=(PartitionKey eq 'Ventas') y (RowKey ge 'empid_000123') y (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* Debe usar un carácter de separador adecuado que hace más fácil tooparse hello **RowKey** valor: por ejemplo, **000123_2012**.  
* También almacena esta entidad en hello igual de partición como otras entidades que contienen datos relacionados para hello mismo empleado, lo que significa que puede usar EGTs toomaintain homogeneidad.
* Considere la posibilidad de la frecuencia con consultará Hola datos toodetermine si este patrón es adecuado.  Por ejemplo, si se tiene acceso a Hola revisión datos con poca frecuencia y Hola principal datos de los empleados a menudo que debe mantener como entidades independientes.  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Utilice este patrón cuando necesite toostore uno o más entidades relacionadas que se consulta con frecuencia.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Transacciones de grupos de entidades](#entity-group-transactions)  
* [Trabajar con tipos de entidad heterogéneos](#working-with-heterogeneous-entity-types)  
* [Patrón final coherente de transacciones](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a>Patrón final del registro
Recuperar hello  *n*  entidades agregan más recientemente tooa partición mediante el uso de un **RowKey** valor que ordena en fecha inversa y orden cronológico.  

#### <a name="context-and-problem"></a>Contexto y problema
Un requisito común es ser capaz de tooretrieve entidades de Hola creado más recientemente, por ejemplo Hola diez más reciente gastos notificaciones enviadas por un empleado. Consulta de tabla de compatibilidad con un **$top** hello tooreturn de operación de consulta primero  *n*  entidades de un conjunto de: no hay ninguna consulta equivalente operación tooreturn Hola últimos n entidades en un conjunto.  

#### <a name="solution"></a>Solución
Almacén Hola entidades mediante un **RowKey** que naturalmente ordena en orden inverso fecha/hora orden mediante el uso de para entrada más reciente de hello siempre es hello primera de ellas en la tabla de Hola.  

Por ejemplo, toobe puede tooretrieve Hola diez notificaciones más recientes de gastos enviados por un empleado, puede usar un valor de graduación inversa derivan Hola de fecha y hora actuales. Hello siguiente ejemplo de código de C# muestra una manera de toocreate un valor de "invertido tics" adecuado para un **RowKey** que ordena de hello más reciente toohello más antigua:  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

Puede obtener nuevo valor de tiempo de fecha toohello mediante el siguiente código de hello:  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

consulta de tabla de Hello tiene el siguiente aspecto:  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* Debe rellenar valor de graduación inversa de hello con ceros iniciales valor de cadena de hello tooensure ordena según lo previsto.  
* Debe ser consciente de los objetivos de escalabilidad de hello en el nivel de Hola de una partición. Tenga cuidado de no crear particiones en la zona activa.  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Utilice este patrón cuando necesite tooaccess entidades en orden inverso de fecha y hora o cuando necesite tooaccess hello más recientemente agregado entidades.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Anteponer/anexar antipatrón](#prepend-append-anti-pattern)  
* [Recuperación de entidades](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a>Patrón de eliminación de gran volumen
Permitir la eliminación de Hola de un gran volumen de entidades mediante el almacenamiento de todas las entidades de Hola para su eliminación simultánea en su propia tabla independiente; eliminar entidades de hello mediante la eliminación de la tabla de Hola.  

#### <a name="context-and-problem"></a>Contexto y problema
Muchas aplicaciones eliminan datos antiguos que ya no necesita la aplicación de cliente de toobe tooa disponibles o esa aplicación Hola archivado tooanother medio de almacenamiento. Normalmente se identifican estos datos en una fecha: por ejemplo, tendrá registros toodelete requisito de todas las solicitudes de inicio de sesión que tienen más de 60 días de antigüedad.  

Un diseño posible es toouse Hola fecha y hora en de solicitud de inicio de sesión de Hola Hola **RowKey**:  

![][21]

Este enfoque evita zonas activas de partición porque la aplicación hello puede insertar y eliminar entidades de inicio de sesión para cada usuario en una partición independiente. Sin embargo, este enfoque puede resultar costoso mucho tiempo si tiene un gran número de entidades porque primero debe tooperform un recorrido de tabla en orden tooidentify todos los toodelete de entidades de hello y, a continuación, debe eliminar cada entidad antiguo. Tenga en cuenta que puede reducir Hola número de viajes de ida y toohello toodelete servidor necesario Hola entidades antiguo por lotes varias solicitudes de eliminación en EGTs.  

#### <a name="solution"></a>Solución
Utilice una tabla independiente para cada día de intentos de inicio de sesión. Puede usar el diseño de la entidad de Hola por encima de los puntos de conexión tooavoid cuando se insertan entidades, y eliminar entidades anteriores ahora es simplemente una pregunta de la eliminación de una tabla cada día (una operación de almacenamiento único) en lugar de buscar y eliminar cientos y miles de entidades de inicio de sesión individual cada día.  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* ¿Admite el diseño de otras formas de la aplicación va a utilizar datos de hello como búsqueda de entidades específicas, vincular con otros datos, o generar información de agregado?  
* ¿Evita el diseño problemas cuando se insertan nuevas entidades?  
* Esperar un retraso si desea tooreuse Hola mismo nombre de la tabla después de eliminarlo. Es mejor tooalways utilizar nombres de tabla única.  
* Esperar algunos limitación cuando realice primero una nueva tabla mientras Hola servicio tabla aprende los patrones de acceso de Hola y distribuye las particiones de hello entre nodos. Considere la posibilidad de la frecuencia con necesita toocreate nuevas tablas.  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Utilice este patrón cuando tenga un gran volumen de entidades que se deben eliminar en hello mismo tiempo.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Transacciones de grupos de entidades](#entity-group-transactions)
* [Modificación de entidades](#modifying-entities)  

### <a name="data-series-pattern"></a>Patrón de serie de datos
Serie completa de los datos de almacén única entidad toominimize Hola de varias solicitudes que realice.  

#### <a name="context-and-problem"></a>Contexto y problema
Un escenario común es para una aplicación toostore una serie de datos que normalmente se necesita tooretrieve a la vez. Por ejemplo, la aplicación podría grabar cuántos mensajes de mensajería instantánea cada empleado envía cada hora y, a continuación, use este tooplot información cuántos mensajes enviado a través de cada usuario Hola 24 horas anteriores. Un diseño puede ser toostore 24 entidades para cada empleado:  

![][22]

Con este diseño, fácilmente puede buscar y actualizar Hola entidad tooupdate para cada empleado de cada vez que la aplicación hello necesita el valor de número de mensajes de Hola tooupdate. Sin embargo, tooretrieve Hola información tooplot un gráfico de actividad de hello para hello 24 horas anteriores, debe recuperar 24 entidades.  

#### <a name="solution"></a>Solución
Usar hello sigue diseño con un número de mensajes de Hola de toostore de propiedades independientes para cada hora:  

![][23]

Con este diseño, puede usar un número de mensajes de Hola de mezcla operación tooupdate para un empleado de una hora concreta. Ahora, puede recuperar toda la información de hello necesita gráfico de hello tooplot mediante una solicitud para una sola entidad.  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* Si la serie de datos completa no cabe en una única entidad (una entidad puede tener propiedades too252), use un almacén de datos alternativo, como un blob.  
* Si tiene varios clientes simultáneamente, la actualización de una entidad, deberá hello toouse **ETag** tooimplement de simultaneidad optimista. Si tiene muchos clientes, puede experimentar un alto nivel de contención.  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Utilice este patrón cuando necesite tooupdate y recuperar una serie de datos asociada a una entidad individual.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Patrón de entidades de gran tamaño](#large-entities-pattern)  
* [Combinar o reemplazar](#merge-or-replace)  
* [Patrón de transacciones coherente](#eventually-consistent-transactions-pattern) (si está almacenando series de datos de hello en un blob)  

### <a name="wide-entities-pattern"></a>Patrón de entidades amplio
Usar varias entidades lógicas toostore de entidades físicas con más de 252 propiedades.  

#### <a name="context-and-problem"></a>Contexto y problema
Una entidad individual puede tener no más de 252 propiedades (excepto las propiedades del sistema obligatorio de hello) y no puede almacenar más de 1 MB de datos en total. En una base de datos relacional, normalmente, obtendría los límites de tamaño de Hola de una fila de ida y vuelta al agregar una nueva tabla e imponer una relación de 1 a 1 entre ellos.  

#### <a name="solution"></a>Solución
Con el servicio de la tabla de Hola, puede almacenar varias entidades toorepresent un objeto único de grandes empresas con más de 252 propiedades. Por ejemplo, si desea que toostore un recuento del número de Hola de mensajes de mensajería instantánea enviados por cada empleado para hello últimos 365 días, podría utilizar Hola después de diseño que utiliza dos entidades con distintos esquemas:  

![][24]

Si necesita toomake un cambio que es necesario actualizar ambos tookeep entidades ellos sincronizadas entre sí puede utilizar un EGT. En caso contrario, puede usar un número de mensajes de Hola de combinación única operación tooupdate para un día determinado. tooretrieve Hola a todos los datos para un empleado individual que se debe recuperar ambas entidades, lo que puede realizar con dos solicitudes eficaz que se usan un **PartitionKey** y un **RowKey** valor.  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* Recuperar una entidad lógica completa implica al menos dos de las transacciones de almacenamiento: entidad física de un tooretrieve.  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Utilice este patrón cuando necesidad toostore entidades cuyo tamaño o número de propiedades superan el límite de Hola de una entidad individual en hello servicio tabla.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Transacciones de grupos de entidades](#entity-group-transactions)
* [Combinar o reemplazar](#merge-or-replace)

### <a name="large-entities-pattern"></a>Patrón de entidades de gran tamaño
Usar valores de propiedad grande de toostore de almacenamiento de blobs.  

#### <a name="context-and-problem"></a>Contexto y problema
Una entidad individual no puede almacenar más de 1 MB de datos en total. Si una o varias de las propiedades del almacén de valores que hacen el tamaño total de hello de la entidad tooexceed este valor, no se puede almacenar toda la entidad Hola Hola servicio tabla.  

#### <a name="solution"></a>Solución
Si la entidad supera 1 MB de tamaño porque una o varias propiedades contienen una gran cantidad de datos, puede almacenar datos en hello servicio Blob y, a continuación, almacenar direcciones Hola de blob de hello en una propiedad de entidad de Hola. Por ejemplo, puede almacenar fotos Hola de un empleado en el almacenamiento de blobs y almacenar una foto de toohello vínculo Hola **fotográfica** propiedad de la entidad de empleados:  

![][25]

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* toomaintain coherencia definitiva entre entidad Hola Hola servicio tabla y datos de Hola Hola servicio Blob, use hello [patrón coherente transacciones](#eventually-consistent-transactions-pattern) toomaintain las entidades.
* Recuperar una entidad completa implica al menos dos de las transacciones de almacenamiento: una entidad de hello tooretrieve y uno tooretrieve Hola de blobs de datos.  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Utilice este patrón cuando sea necesario entidades toostore cuyo tamaño supera el límite de Hola de una entidad individual en el servicio de la tabla de Hola.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Patrón final coherente de transacciones](#eventually-consistent-transactions-pattern)  
* [Patrón de entidades amplio](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a>Antipatrón de anteponer/anexar
Aumentar la escalabilidad cuando tenga un gran volumen de inserciones extendiendo Hola inserciones en varias particiones.  

#### <a name="context-and-problem"></a>Contexto y problema
Antepone o anexar entidades de entidades tooyour almacena normalmente da lugar a aplicación hello agregar nueva toohello entidades primero o último partición de una secuencia de particiones. En este caso, todos de inserciones de hello en un momento dado se tienen lugar en la misma partición, crear una zona activa que impide que el servicio de la tabla de hello equilibrio de carga se inserta en varios nodos de Hola y lo que podría provocar la escalabilidad de la aplicación toohit Hola destinos de partición. Por ejemplo, si tiene una aplicación que tienen acceso recursos y la red de los registros de los empleados, a continuación, podría dar lugar a una estructura de entidad tal y como se muestra a continuación Hola partición de la hora actual se convierta en una zona activa si volumen Hola de transacciones alcanza el objetivo de escalabilidad de Hola para una partición individual:  

![][26]

#### <a name="solution"></a>Solución
Hello estructura de una entidad alternativa siguiente evita una zona activa en cualquier partición determinada como aplicación Hola registra los eventos:  

![][27]

Tenga en cuenta con este ejemplo cómo ambos Hola **PartitionKey** y **RowKey** son claves compuestas. Hola **PartitionKey** usa el departamento de Hola y el registro de hello de toodistribute de Id. de empleado en varias particiones.  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguientes puntos cuando decida cómo tooimplement este patrón:  

* ¿Hace que la aplicación cliente hace Hola clave estructura alternativa que evita la creación de particiones activas en inserciones eficazmente las consultas de Hola de soporte técnico?  
* ¿Significa el volumen previsto de las transacciones que son probable tooreach objetivos de escalabilidad de Hola para una partición individual y limitarán por servicio de almacenamiento de Hola?  

#### <a name="when-toouse-this-pattern"></a>Cuando toouse este patrón
Evite la antipatrón anteponer/anexar de hello cuando el volumen de transacciones es probable que tooresult en limitación por servicio de almacenamiento de hello cuando tiene acceso a una partición activa.  

#### <a name="related-patterns-and-guidance"></a>Orientación y patrones relacionados
Hello patrones y las directrices siguientes también pueden ser importantes al implementar este patrón:  

* [Patrón de clave compuesta](#compound-key-pattern)  
* [Patrón de cola de registro](#log-tail-pattern)  
* [Modificación de entidades](#modifying-entities)  

### <a name="log-data-anti-pattern"></a>Antipatrón de datos de registro
Normalmente, debe utilizar Hola servicio Blob en lugar de hello datos de registro de toostore de servicio de tabla.  

#### <a name="context-and-problem"></a>Contexto y problema
Caso de uso común para los datos de registro están tooretrieve una selección de entradas del registro para un intervalo de fecha y hora específicas: por ejemplo, desea toofind todos Hola mensajes de error y críticos que registra la aplicación entre 15:04 y 15:06 en una fecha concreta. No desea toouse Hola fecha y hora de partición Hola registro mensaje toodetermine Hola guardar entidades de registro a: que resultados en una partición activa porque en cualquier momento, todas las entidades de registro de hello compartirán Hola mismo **PartitionKey** valor (vea la sección de hello [antipatrón Prepend/anexar](#prepend-append-anti-pattern)). Por ejemplo, hello después de esquema de la entidad para un mensaje de registro se produce en una partición activa porque aplicación hello escribe todos los mensajes de registro toohello partición para hello actual fecha y hora:  

![][28]

En este ejemplo, Hola **RowKey** incluye Hola fecha y hora de tooensure de mensaje de registro de hello que los mensajes de registro se almacenan en orden de fecha y hora e incluye un identificador de mensaje en caso de varios mensajes de registro compartan Hola igual de fecha y hora.  

Otro enfoque es toouse una **PartitionKey** que garantiza que la aplicación hello escribe mensajes a través de un intervalo de particiones. Por ejemplo, si origen Hola de mensaje de registro de hello proporciona un toodistribute de manera mensajes entre ellas, podría utilizar Hola siguiendo los esquemas de la entidad:  

![][29]

Sin embargo, problema de hello con este esquema es que tooretrieve todos Hola mensajes de registro para un intervalo de tiempo específico debe buscar cada partición de tabla de Hola.

#### <a name="solution"></a>Solución
problema de hello resaltado de sección anterior de Hola de intentar toouse Hola entradas del registro de toostore de servicio de tabla y sugiere dos, satisfactorios, diseños. Partición activa de una solución que ha provocado tooa con el riesgo de Hola de un mal rendimiento escribir mensajes de registro; Hello otra solución había ocasionado bajo rendimiento de consultas debido a Hola requisito tooscan cada partición en los mensajes de registro de hello tabla tooretrieve para un intervalo de tiempo específico. Almacenamiento de blobs ofrece una mejor solución para este tipo de escenario y se trata cómo Azure análisis de almacenamiento almacena Hola registro los datos recopila.  

En esta sección se describe cómo el análisis de almacenamiento almacena los datos de registro en el almacenamiento de blobs para ilustrar estos datos de toostoring de enfoque que se suele consultan por intervalo.  

Storage Analytics almacena los mensajes de registro en un formato delimitado en varios blobs. el formato delimitado Hola facilita para un cliente datos de aplicación tooparse hello en el mensaje del registro de hello.  

Análisis de almacenamiento usa una convención de nomenclatura para los blobs que le permite toolocate Hola blob (o blobs) que contienen mensajes de registro de hello para el que está buscando. Por ejemplo, un blob denominado "queue/2014/07/31/1800/000001.log" contiene mensajes de registro relacionados con el servicio de cola de toohello de la hora de Hola a partir de 18:00 del 31 de julio de 2014. Hola "000001" indica que se trata primer archivo de registro de Hola durante este período. Análisis de almacenamiento también registra las marcas de tiempo de Hola de hello primero y último registro mensajes almacenados en el archivo hello como parte de metadatos del blob de Hola. Hola API para habilita el almacenamiento blob buscar blobs en un contenedor en función de un prefijo de nombre: toolocate todos los blobs de Hola que contienen cola registrar los datos de la hora de Hola a partir de 18:00, puede usar Hola prefijo "cola/2014/07/31/1800."  

Análisis de almacenamiento almacena internamente en búfer de mensajes de registro y, a continuación, actualiza periódicamente blob adecuado de Hola o crea uno nuevo con el lote más reciente de Hola de entradas de registro. Esto reduce el número de Hola de escrituras que debe realizar toohello servicio de blob.  

Si está implementando una solución similar en su propia aplicación, debe tener en cuenta cómo toomanage Hola equilibrio entre la confiabilidad (escribir cada almacenamiento de tooblob de entrada de registro en este caso) y el costo y la escalabilidad (en búfer las actualizaciones en la aplicación y escribirlos tooblob almacenamiento por lotes).  

#### <a name="issues-and-considerations"></a>Problemas y consideraciones
Considere la posibilidad de hello siguiendo los puntos de la hora de decidir cómo toostore registrar los datos:  

* Si crea un diseño de tabla que evite posibles particiones activas, observará que no tiene acceso a los datos del registro de forma eficaz.  
* tooprocess registrar los datos, un cliente necesita a menudo tooload muchos registros.  
* Aunque a menudo se estructuran de datos del registro, Blob Storage puede ser una solución mejor.  

### <a name="implementation-considerations"></a>Consideraciones de implementación
En esta sección se describe algunas de hello toobear de consideraciones en cuenta al implementar patrones de Hola se describen en las secciones anteriores Hola. La mayor parte de esta sección se utilizan ejemplos escritos en C# que usan Hola biblioteca de cliente de almacenamiento (versión 4.3.0 en tiempo de Hola de escritura).  

### <a name="retrieving-entities"></a>Recuperación de entidades
Como se describe en la sección de hello [diseño para consultar](#design-for-querying), hello más eficiente de las consultas es una consulta de punto. Sin embargo, en algunos casos deberá tooretrieve varias entidades. Esta sección describen algunas entidades de tooretrieving enfoques comunes mediante Hola biblioteca cliente de almacenamiento.  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a>Ejecutar una consulta de punto mediante Hola biblioteca cliente de almacenamiento
tooexecute de manera más fácil de Hello una consulta de punto es hello de toouse **recuperar** tabla operación tal y como se muestra en hello siguiente fragmento de código de C# que recupera una entidad con un **PartitionKey** de valor "ventas" y un  **RowKey** del valor "212":  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

Observe cómo este ejemplo espera que la entidad de hello recupera toobe de tipo **EmployeeEntity**.  

#### <a name="retrieving-multiple-entities-using-linq"></a>Recuperar varias entidades con LINQ
Puede recuperar varias entidades mediante LINQ con la biblioteca de clientes de Storage y especificar una consulta con una cláusula **where** . tooavoid un recorrido de tabla, debe incluir siempre hello **PartitionKey** valor Hola donde cláusula y si es posible Hola **RowKey** valor recorridos de tabla y de la partición de tooavoid. Hello servicio tabla admite un conjunto limitado de toouse de (mayor que, mayor o igual que, menor que, menor que o igual, igual y no es igual a) de los operadores de comparación en Hola donde cláusula. Hello siguiente fragmento de código de C# busca todos los empleados de hello cuyo último nombre empieza por "B" (suponiendo que esa hello **RowKey** almacenes Hola apellido) en el departamento de ventas de hello (suponiendo que hello **PartitionKey** almacena el nombre del departamento de hello):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

Tenga en cuenta cómo consulta Hola especifica tanto un **RowKey** y un **PartitionKey** tooensure un mejor rendimiento.  

Hello ejemplo de código siguiente muestra una funcionalidad equivalente mediante la API fluida de hello (para obtener más información acerca de la API fluidas en general, vea [prácticas recomendadas para diseñar una API fluida](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> ejemplo Hello anida varios **CombineFilters** tooinclude métodos Hola tres condiciones de filtro.  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a>Recuperar una gran cantidad de entidades de una consulta
Una consulta óptima devuelve una entidad individual basada en un valor **PartitionKey** y un valor **RowKey**. Sin embargo, en algunos casos, habrá un requisito tooreturn muchas entidades de hello misma partición o incluso del número de particiones.  

Siempre por completo debe probar el rendimiento de saludo de la aplicación en tales escenarios.  

Una consulta en el servicio de la tabla de hello puede devolver un máximo de 1.000 entidades al mismo tiempo y se puede ejecutar durante un máximo de cinco segundos. Si el conjunto de resultados hello contiene más de 1.000 entidades, si no se completó la consulta de hello en cinco segundos, o si consulta Hola cruza el límite de la partición de hello, Hola servicio tabla devuelve un tooenable de token de continuación Hola Hola de toorequest de aplicación de cliente siguiente conjunto de entidades. Para más información sobre el funcionamiento de los tokens de continuación, consulte [Tiempo de espera de consulta y paginación](http://msdn.microsoft.com/library/azure/dd135718.aspx).  

Si usas Hola biblioteca cliente de almacenamiento, puede controlar automáticamente tokens de continuación para usted que devuelva las entidades de hello servicio tabla. Hello C# ejemplo de código siguiente utiliza Hola biblioteca cliente de almacenamiento automáticamente controla los tokens de continuación si el servicio de la tabla de hello devuelve en una respuesta:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

Hola siguiente código de C# administra tokens de continuación explícitamente:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

Mediante el uso de tokens de continuación explícitamente, puede controlar cuando la aplicación recupera el siguiente segmento de Hola de datos. Por ejemplo, si la aplicación cliente permite a los usuarios toopage a través de las entidades de hello almacenadas en una tabla, un usuario puede decidir no toopage a través de todas las entidades de hello recuperados por consulta de hello, por lo que la aplicación sólo utilizaría un hello tooretrieve token de continuación a continuación segmento de usuario de hello había finalizado paginación a través de todas las entidades de hello en el segmento actual Hola. Este enfoque tiene varias ventajas:  

* Le permite toolimit cantidad de Hola de tooretrieve de datos de hello servicio tabla y que se mueve sobre red Hola.  
* Permite tooperform E/S asincrónica en. NET.  
* Permite el almacenamiento de información de tooserialize Hola continuación toopersistent token para que pueda continuar en caso de hello de bloqueo de una aplicación.  

> [!NOTE]
> Normalmente, un token de continuación devuelve un segmento que contiene 1.000 entidades, aunque pueden ser menos. Este también es el caso de hello si limita Hola número de entradas que se devuelve de una consulta mediante **tomar** tooreturn Hola primer n entidades que coinciden con los criterios de búsqueda: servicio de la tabla de hello puede devolver un segmento que contiene menos de n entidades a lo largo de con un tooenable de token de continuación tooretrieve Hola entidades restantes.  
> 
> 

Hello código C# siguiente muestra cómo toomodify número de Hola de entidades devuelve dentro de un segmento:  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a>Proyección de servidor
Una sola entidad puede tener propiedades too255 y debe too1 MB de tamaño. Al consultar la tabla de Hola y recuperar entidades, no es necesario todas las propiedades de Hola y puede evitar la transferencia de datos innecesariamente (toohelp reducir la latencia y el costo). Puede usar propiedades de servidor proyección tootransfer Hola solo que necesita. Hello en el ejemplo siguiente se es recupera solo Hola **correo electrónico** propiedad (junto con **PartitionKey**, **RowKey**, **marca de tiempo**y  **ETag**) desde las entidades de hello seleccionadas por consulta Hola.  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

Tenga en cuenta cómo Hola **RowKey** valor está disponible, aunque no se incluyó en lista de Hola de tooretrieve de propiedades.  

### <a name="modifying-entities"></a>Modificación de entidades
Hola biblioteca cliente de almacenamiento permite toomodify las entidades se almacenan en el servicio de la tabla de hello mediante inserción, eliminación y actualización de entidades. Puede usar EGTs toobatch varias operaciones de inserción, actualización y eliminación número de hello tooreduce juntos de ida y vuelta necesarios y mejora el rendimiento de hello de la solución.  

Tenga en cuenta que las excepciones producidas cuando Hola biblioteca cliente de almacenamiento se ejecuta un EGT normalmente incluyen el índice de Hola de entidad de Hola que causó Hola lote toofail. Esto resulta útil cuando se depura código que usa EGT.  

También debe considerar cómo afecta su diseño a la forma en que la aplicación cliente trata las operaciones de simultaneidad y actualización.  

#### <a name="managing-concurrency"></a>Administrar la simultaneidad
De forma predeterminada, el servicio de tabla de hello implementa optimista de simultaneidad realiza comprobaciones en nivel de Hola de entidades individuales para **insertar**, **mezcla**, y **eliminar** operaciones, Aunque es posible para un hello tooforce de cliente de servicio toobypass las tablas estas comprobaciones. Para obtener más información acerca de cómo el servicio de la tabla de hello administra simultaneidad, vea [administrar la simultaneidad en el almacenamiento de Azure de Microsoft](../storage/common/storage-concurrency.md).  

#### <a name="merge-or-replace"></a>Combinar o reemplazar
Hola **reemplazar** método de hello **TableOperation** clase siempre reemplaza la entidad completa de Hola Hola servicio tabla. Si no incluye una propiedad en la solicitud de hello cuando existe esa propiedad de entidad de hello almacenado, solicitud de hello quita que la propiedad de hello almacena entidad. A menos que desee tooremove una propiedad explícitamente desde una entidad almacenada, debe incluir todas las propiedades de solicitud de Hola.  

Puede usar hello **mezcla** método de hello **TableOperation** cantidad de hello tooreduce de clase de datos que se envíe toohello servicio de tabla cuando desee tooupdate una entidad. Hola **mezcla** método reemplaza cualquier propiedad de entidad de hello almacenado con valores de propiedad de entidad de hello incluido en la solicitud de hello, pero deja intacta cualquier propiedad de hello almacena entidad que no se incluyen en la solicitud de saludo. Esto es útil si tiene entidades de gran tamaño y solo necesita tooupdate un pequeño número de propiedades en una solicitud.  

> [!NOTE]
> Hola **reemplazar** y **mezcla** métodos producirá un error si la entidad de hello no existe. Como alternativa, puede usar hello **InsertOrReplace** y **InsertOrMerge** métodos que crean una nueva entidad si no existe.  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a>Trabajar con tipos de entidad heterogéneos
Hola servicio tabla es una *sin esquema* almacén de tablas que significa que una sola tabla puede almacenar entidades de varios tipos que proporciona gran flexibilidad en el diseño. Hello en el ejemplo siguiente se muestra una tabla que almacena empleado y entidades de departamento:  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Nombre</th>
<th>Apellidos</th>
<th>Edad</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Nombre</th>
<th>Apellidos</th>
<th>Edad</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Nombre</th>
<th>Apellidos</th>
<th>Edad</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Tenga en cuenta que cada entidad aún debe tener valores **PartitionKey**, **RowKey** y **Timestamp**, pero puede tener cualquier conjunto de propiedades. Además, no hay nada tooindicate Hola tipo de una entidad a menos que elija toostore esa información en algún lugar. Hay dos opciones para identificar el tipo de entidad de hello:  

* Anteponer toohello de tipo de entidad de hello **RowKey** (o posiblemente Hola **PartitionKey**). Por ejemplo, **EMPLOYEE_000123** o **DEPARTMENT_SALES** como valores **RowKey**.  
* Utilice un tipo de entidad de propiedad independiente toorecord Hola tal y como se muestra en la siguiente tabla se Hola.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Nombre</th>
<th>Apellidos</th>
<th>Edad</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Nombre</th>
<th>Apellidos</th>
<th>Edad</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>department</td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>Nombre</th>
<th>Apellidos</th>
<th>Edad</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

primera opción Hello, anteponiéndole toohello de tipo de entidad de hello **RowKey**, es útil si hay una posibilidad de que dos entidades de tipos diferentes podrían tener Hola mismo valor de clave. También agrupa las entidades del programa Hola a mismo tipo juntos en la partición de Hola.  

Hello técnicas descritas en esta sección son especialmente relevante toohello discusión [las relaciones de herencia](#inheritance-relationships) anteriormente en esta guía en la sección de hello [modelización relaciones](#modelling-relationships).  

> [!NOTE]
> Considere la posibilidad de incluir un número de versión en hello entidad tipo valor tooenable aplicaciones tooevolve POCO objetos de cliente y trabajar con versiones diferentes.  
> 
> 

Hello restantes de esta sección describen algunas de las características de Hola Hola biblioteca cliente de almacenamiento que facilitan el trabajo con varios tipos de entidad en hello mismo tabla.  

#### <a name="retrieving-heterogeneous-entity-types"></a>Recuperar tipos de entidad heterogéneos
Si usas Hola biblioteca cliente de almacenamiento, tiene tres opciones para trabajar con varios tipos de entidad.  

Si sabe Hola tipo de entidad de hello almacenado con un valor concreto **RowKey** y **PartitionKey** valores, a continuación, puede especificar tipo de entidad de hello al recuperar entidad Hola tal y como se muestra en los ejemplos de hello dos anteriores que recuperan entidades de tipo **EmployeeEntity**: [ejecutar una consulta de punto mediante Hola biblioteca cliente de almacenamiento](#executing-a-point-query-using-the-storage-client-library) y [recuperar varias entidades usando LINQ](#retrieving-multiple-entities-using-linq).  

Hola segunda opción es hello toouse **DynamicTableEntity** tipo (una bolsa de propiedades) en lugar de un tipo concreto de entidad POCO (esta opción también puede mejorar el rendimiento porque no hay ninguna necesidad de tooserialize y deserializar entidad Hola demasiado. Tipos de red). Hola siguiente código de C# potencialmente recupera varias entidades de distintos tipos de tabla de hello, pero devuelve todas las entidades como **DynamicTableEntity** instancias. A continuación, utiliza hello **EntityType** tipo de propiedad toodetermine Hola de cada entidad:  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

Tenga en cuenta que tooretrieve otras propiedades que se debe utilizar hello **TryGetValue** método en hello **propiedades** propiedad de hello **DynamicTableEntity** clase.  

Una tercera opción es toocombine con hello **DynamicTableEntity** tipo y un **EntityResolver** instancia. Esto le permite tooresolve toomultiple POCO tipos Hola misma consulta. En este ejemplo, Hola **EntityResolver** delegado está usando hello **EntityType** toodistinguish de propiedad entre los tipos de hello dos de entidad que Hola consulta devuelve. Hola **resolver** método usa hello **resolución** delegar tooresolve **DynamicTableEntity** instancias demasiado**TableEntity** instancias.  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a>Modificar tipos de entidad heterogéneos
No es necesario tooknow tipo de Hola de una entidad toodelete y conozca tipo hello de una entidad al insertarlo. Sin embargo, puede usar **DynamicTableEntity** escriba tooupdate una entidad sin conocer su tipo y sin utilizar una clase de entidad POCO. Hello ejemplo de código siguiente recupera una entidad única y comprueba hello **EmployeeCount** propiedad existe antes de actualizarlo.  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a>Control de acceso con firmas de acceso compartido
Puede usar toomodify de las aplicaciones de cliente de firma de acceso compartido (SAS) tokens tooenable (y consultar) las entidades de tabla directamente sin Hola necesidad tooauthenticate directamente con el servicio de la tabla de Hola. Normalmente, hay tres ventajas principales toousing SAS en la aplicación:  

* No es necesario toodistribute su almacenamiento cuenta tooan clave insegura plataforma (por ejemplo, un dispositivo móvil) en orden tooallow tooaccess de ese dispositivo y modificar las entidades de hello servicio tabla.  
* Puede descargar algunas de las tareas de hello ese sitio web y roles de trabajo realizar para administrar los dispositivos de tooclient de entidades, como los equipos y dispositivos móviles.  
* Puede asignar un restringida y conjunto de cliente de tooa de permisos (por ejemplo, para permitir el acceso de solo lectura toospecific recursos) limitado de tiempo.  

Para obtener más información acerca del uso de tokens de SAS con hello servicio tabla, vea [utilizando firmas de acceso compartido (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md).  

Sin embargo, todavía debe generar tokens SAS de Hola que conceda a un cliente las entidades de toohello de aplicación de servicio de la tabla de Hola: debería hacerlo en un entorno que se protegen acceso tooyour claves de cuenta de almacenamiento. Normalmente, se utiliza un Hola de toogenerate de rol web o de trabajo SAS tokens y entregarlos toohello las aplicaciones de cliente que necesitan tener acceso a entidades de tooyour. Dado que todavía hay una sobrecarga implicada en la generación y entrega tooclients de tokens SAS, debe considerar la mejor manera de tooreduce esta sobrecarga, especialmente en escenarios de alto volumen.  

Es posible toogenerate un token SAS que concede acceso tooa subconjunto de entidades de hello en una tabla. De forma predeterminada, se crea un token SAS para una tabla completa, pero también es posible toospecify ese tooeither de acceso de hello SAS token conceder un intervalo de **PartitionKey** valores o un intervalo de **PartitionKey** y  **RowKey** valores. Puede elegir a toogenerate tokens SAS para usuarios individuales del sistema de forma que el token de SAS de cada usuario solo les permite el acceso tootheir propio entidades Hola servicio tabla.  

### <a name="asynchronous-and-parallel-operations"></a>Operaciones asincrónicas y paralelas
En caso de que reparta las solicitudes entre varias particiones, puede mejorar el rendimiento y la capacidad de respuesta del cliente mediante consultas asincrónicas o paralelas.
Por ejemplo, podría tener dos o más instancias de rol de trabajo con acceso a las tablas en paralelo. Se puede tener roles de trabajo individuales responsables determinados conjuntos de particiones, o simplemente tiene varias instancias de rol de trabajo, cada tooaccess capaz de todas las particiones en una tabla de Hola.  

Dentro de una instancia de cliente, puede mejorar el rendimiento mediante la ejecución de operaciones de almacenamiento de forma asincrónica. Hola biblioteca cliente de almacenamiento permite modificaciones y consultas asincrónicas de toowrite fácil. Por ejemplo, puede comenzar con el método sincrónico de Hola que recupera todas las entidades de hello en una partición como se muestra en hello siguiente código de C#:  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

Puede modificar fácilmente este código para que esa consulta Hola se ejecuta de forma asincrónica como sigue:  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

En este ejemplo asincrónica, puede ver la siguiente Hola cambia de la versión sincrónica de hello:  

* firma del método Hello ahora incluye hello **async** modificador y devuelve un **tarea** instancia.  
* En lugar de Hola que realiza la llamada **ExecuteSegmented** resultados del método tooretrieve, Hola método ahora llamadas Hola **ExecuteSegmentedAsync** Hola de método y se utiliza **await** modificador tooretrieve resultados de forma asincrónica.  

aplicación de cliente de Hello puede llamar a este método varias veces (con valores diferentes para hello **departamento** parámetro), y cada consulta se ejecutará en un subproceso independiente.  

Tenga en cuenta que no hay ninguna versión asincrónica de hello **Execute** método Hola **TableQuery** clase porque hello **IEnumerable** interfaz no admite asincrónica enumeración.  

También puede insertar, actualizar y eliminar entidades de forma asincrónica. Hola el ejemplo de C# siguiente muestra un método sencillo y sincrónico tooinsert o reemplaza una entidad empleado:  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Puede modificar fácilmente este código para que la actualización de Hola se ejecuta de forma asincrónica como se indica a continuación:  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

En este ejemplo asincrónica, puede ver la siguiente Hola cambia de la versión sincrónica de hello:  

* firma del método Hello ahora incluye hello **async** modificador y devuelve un **tarea** instancia.  
* En lugar de Hola que realiza la llamada **Execute** entidad de método tooupdate hello, Hola método ahora llamadas Hola **ExecuteAsync** Hola de método y se utiliza **await** tooretrieve de modificador Si se produce de forma asincrónica.  

aplicación de cliente de Hello puede llamar a varios métodos asincrónicos como este, y cada invocación del método se ejecutará en un subproceso independiente.  

### <a name="credits"></a>Créditos
Nos gustaría hello toothank después de los miembros de equipo de Azure para sus contribuciones hello: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Shah Vinay y Serdar Ozler, así como Tom Hollander de DX de Microsoft. 

También nos gustaría hello toothank sigue MVP de Microsoft para sus valiosos comentarios durante los ciclos de revisión: Igor Papirov y Edward Bakker.

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

