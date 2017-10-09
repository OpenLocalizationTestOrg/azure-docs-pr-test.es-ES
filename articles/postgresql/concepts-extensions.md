---
title: extensiones de PostgreSQL aaaUsing en la base de datos de Azure para PostgreSQL | Documentos de Microsoft
description: Describe la funcionalidad de Hola de hello capacidad tooextend de la base de datos mediante extensiones en la base de datos de PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: af2462d7a923b934bc0329153be7079ba86e8856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>Extensiones de PostgreSQL en Azure Database for PostgreSQL
PostgreSQL proporciona la funcionalidad de Hola de hello capacidad tooextend de la base de datos con las extensiones. Extensiones permiten varias toobe de objetos SQL relacionado agrupado juntos en un único paquete y se pueden cargar o quitadas de la base de datos con un solo comando. Una vez cargadas en la base de datos de hello las extensiones pueden funcionar como características que están integradas en. Para obtener más información acerca de las extensiones de PostgreSQL, consulte la información sobre el [empaquetado de objetos relacionados en una extensión](https://www.postgresql.org/docs/9.6/static/extend-extensions.html).

## <a name="how-toouse-postgresql-extensions"></a>¿Cómo toouse PostgreSQL extensiones?
Las extensiones de PostgreSQL deben toobe instalado para la base de datos antes de utilizarlas. tooinstall una extensión determinada, ejecute el [crear extensión](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) comandos de tooload de herramienta psql Hola empaquetados objetos en la base de datos.

Azure Database for PostgreSQL admite un subconjunto de extensiones de claves, como se enumeran aquí. Más allá de hello mencionados, no se admiten otras extensiones. No puede crear su propia extensión con el servicio Azure Database for PostgreSQL.

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>Extensiones admitidas por Azure Database for PostgreSQL
Hola las tablas siguientes se lista Hola PostgreSQL extensiones estándar que son compatibles actualmente con la base de datos de Azure para PostgreSQL. También puede obtener esta información emitiendo la consulta pg\_available\_extensions. 

### <a name="data-types-extensions"></a>Extensiones de tipos de datos

> [!div class="mx-tableFixed"]
| **Extensión** | **Descripción** |
|---|---|
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | Proporciona un tipo de cadena de caracteres que no distingue entre mayúsculas y minúsculas. |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | Proporciona el tipo de datos para almacenar conjuntos de pares clave/valor. |

### <a name="functions-extensions"></a>Extensiones de funciones

> [!div class="mx-tableFixed"]
| **Extensión** | **Descripción** |
|---|---|
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | Proporciona varias similitudes toodetermine de funciones y la distancia entre las cadenas. |
| [intarray](https://www.postgresql.org/docs/9.6/static/intarray.html) | Proporciona funciones y operadores para manipular matrices de enteros sin valores nulos. |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | Proporciona funciones de cifrado. |
| [pg\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | Administra las tablas con particiones por hora o identificador. |
| [pg\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | Proporciona funciones y operadores para determinar la similitud de hello del texto alfanumérico basada en la coincidencia de Trigrama |
| [uuid-ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | Genera identificadores únicos universales (UUID). |

### <a name="full-text-search-extensions"></a>Extensiones de búsqueda de texto completo

> [!div class="mx-tableFixed"]
| **Extensión** | **Descripción** |
|---|---|
| [unaccent](https://www.postgresql.org/docs/9.6/static/unaccent.html) | Un diccionario de búsqueda de texto que quita los acentos (signos diacríticos) de lexemas. |

### <a name="index-types-extensions"></a>Extensiones de tipos de índices

> [!div class="mx-tableFixed"]
| **Extensión** | **Descripción** |
|---|---|
| [btree\_gin](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | Proporciona clases de operador GIN de ejemplo que implementan el comportamiento similar al del árbol B para determinados tipos de datos. |
| [btree\_gist](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | Proporciona clases de operador de índice de GiST que implementan el árbol B. |

### <a name="language-extensions"></a>Extensiones de lenguaje

> [!div class="mx-tableFixed"]
| **Extensión** | **Descripción** |
|---|---|
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | Lenguaje de procedimientos que puede cargar PL/pgSQL |

### <a name="miscellaneous-extensions"></a>Extensiones variadas

> [!div class="mx-tableFixed"]
| **Extensión** | **Descripción** |
|---|---|
| [pg\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | Proporciona un medio para examinar lo que está sucediendo en memoria caché del búfer Hola compartido en tiempo real. |
| [pg\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | Proporciona una manera tooload relación de datos en memoria caché del búfer Hola. |
| [pg\_stat\_statements](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | Proporciona un medio para realizar el seguimiento de las estadísticas de ejecución de todas las instrucciones SQL ejecutadas por un servidor. |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | Contenedor de datos externo utilizado tooaccess los datos almacenados en los servidores externos de PostgreSQL |

### <a name="postgis"></a>PostGIS

> [!div class="mx-tableFixed"]
| **Extensión** | **Descripción** |
|---|---|
| [PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal | Objetos espaciales y geográficos para PostgreSQL. |
| address\_standardizer, address\_standardizer\_data\_us | Tooparse usa una dirección en los elementos que lo componen. Usa el paso de normalización de dirección de toosupport geocodificación. |
| [pgrouting](http://pgrouting.org/) | Extiende hello PostGIS / PostgreSQL geospatial tooprovide geospatial enrutamiento funcionalidad de base de datos. |

## <a name="next-steps"></a>Pasos siguientes
¿No se ve una extensión que le gustaría toouse? Díganoslo. Vote las solicitudes existentes o cree nuevos comentarios y deseos en nuestro [foro de comentarios de clientes](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).
