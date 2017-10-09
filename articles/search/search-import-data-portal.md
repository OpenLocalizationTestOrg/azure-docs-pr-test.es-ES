---
title: "datos de aaaImport en búsqueda de Azure en el portal de hello | Documentos de Microsoft"
description: "Usar hello Asistente para importar datos de Azure búsqueda en el Portal de Azure de hello toocrawl datos de Azure desde la base de datos de SQL Azure Cosmos, almacenamiento de Blob, almacenamiento de tabla, base de datos SQL y SQL Server en máquinas virtuales de Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: Azure Portal
ms.assetid: f40fe07a-0536-485d-8dfa-8226eb72e2cd
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 00b0e59594560c0cdaea748df196518e9fba3834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-tooazure-search-using-hello-portal"></a>Importar datos tooAzure búsqueda mediante el portal de Hola
Hello Azure portal proporciona un **importar datos** asistente en el panel de búsqueda de Azure de Hola para cargar datos en un índice. 

  ![Importar datos en la barra de comandos de Hola][1]

Internamente, el Asistente de hello configura e invoca un *indizador*, automatizar varios pasos del proceso de indización de hello: 

* Conectar origen de datos externo tooan Hola misma suscripción de Azure
* Generar un esquema de índice modificable basado en la estructura de datos de origen de Hola
* Cargar documentos JSON en un índice mediante un conjunto de filas recuperado del origen de datos de Hola

Puede probar este flujo de trabajo con datos de ejemplo en Azure Cosmos DB. Visite [empezar a trabajar con búsqueda de Azure en hello Azure Portal](search-get-started-portal.md) para obtener instrucciones.

> [!NOTE]
> Puede iniciar hello **importar datos** Asistente de toosimplify de panel de base de datos de Azure Cosmos Hola la indización para ese origen de datos. En la navegación de la izquierda, vaya demasiado**colecciones** > **Agregar búsqueda de Azure** tooget iniciado.

## <a name="data-sources-supported-by-hello-import-data-wizard"></a>Orígenes de datos admitidos por el Asistente para importar datos de Hola
Asistente para importar datos de Hello admite Hola siguientes orígenes de datos: 

* Azure SQL Database
* Datos relacionales de SQL Server en una máquina virtual de Azure
* Azure Cosmos DB
* Almacenamiento de blobs de Azure
* Almacenamiento de tablas de Azure

Un conjunto de datos plano es una entrada necesaria. Solo se puede importar desde una única tabla, vista de base de datos o estructura de datos equivalente. Debe crear esta estructura de datos antes de ejecutar el Asistente de Hola.

## <a name="connect-tooyour-data"></a>Conexión de datos de tooyour
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) y panel de servicio de hello abierto. Puede hacer clic en **más servicios** en hello salto barra toosearch existente "para servicios de búsqueda" en la suscripción actual de Hola. 
2. Haga clic en **importar datos** en la hoja de datos de importación de tooslide Hola abrir la barra de comandos de Hola.  
3. Haga clic en **conectar datos tooyour** toospecify una definición de origen de datos utilizada por un indizador. Para orígenes de datos de suscripción dentro de un asistente de hello normalmente puede detectar y leer la información de conexión, minimizar los requisitos de configuración general.

|  |  |
| --- | --- |
| **Origen de datos existente** |Si ya tiene indexadores definidos en el servicio de búsqueda, puede seleccionar una definición de origen de datos existente para otra importación. |
| **Azure SQL Database** |Nombre del servicio, las credenciales de un usuario de base de datos con permiso de lectura y un nombre de base de datos se pueden especificar en la página de Hola o a través de una cadena de conexión de ADO.NET. Elija tooview de opción de cadena de conexión de Hola o personalizar las propiedades. <br/><br/>Hola tabla o vista que proporciona el conjunto de filas de hello debe especificarse en la página de Hola. Esta opción aparece después de hello conexión se realiza correctamente, lo que proporciona una lista desplegable para que pueda realizar una selección. |
| **SQL Server en máquinas virtuales de Azure** |Especifique un nombre de servicio completo, el identificador de usuario y la contraseña, y la base de datos como una cadena de conexión. toouse este origen de datos, debe tener previamente instalado un certificado del almacén local Hola que cifra la conexión de Hola. Para obtener instrucciones, consulte [tooAzure de conexión de VM de SQL búsqueda](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md). <br/><br/>Hola tabla o vista que proporciona el conjunto de filas de hello debe especificarse en la página de Hola. Esta opción aparece después de hello conexión se realiza correctamente, lo que proporciona una lista desplegable para que pueda realizar una selección. |
| **Azure Cosmos DB** |Requisitos incluyen la colección, la base de datos y la cuenta de hello. Todos los documentos de la colección de Hola se incluirán en el índice de Hola. Puede definir una consulta tooflatten o filtrar el conjunto de filas de Hola o toodetect cambiado documentos para las operaciones de actualización de datos subsiguientes. |
| **Azure Blob Storage** |Requisitos incluyen la cuenta de almacenamiento de Hola y un contenedor. Opcionalmente, si los nombres de blob siguen una convención de nomenclatura virtual para fines de agrupación, puede especificar parte del directorio virtual de hello del nombre de hello como una carpeta en el contenedor. Consulte [Indexación de Blob Storage](search-howto-indexing-azure-blob-storage.md) para más información. |
| **Azure Table Storage** |Requisitos incluyen la cuenta de almacenamiento de Hola y un nombre de tabla. Si lo desea, puede especificar un tooretrieve consulta un subconjunto de tablas de Hola. Consulte [Indexación de Table Storage](search-howto-indexing-azure-tables.md) para más información. |

## <a name="customize-target-index"></a>Personalización del índice de destino
Un índice preliminar normalmente se deduce del conjunto de datos de Hola. Agregar, editar o eliminar campos toocomplete Hola esquema. Además, establecer atributos en toodetermine de nivel de campo de hello sus comportamientos de búsqueda posterior.

1. En **índice de destino de personalizar**, especifique el nombre de Hola y un **clave** toouniquely usado identificar cada documento. Hola clave debe ser una cadena. Si los valores de campo incluyen espacios o guiones estar seguro de que tooset opciones avanzadas en **importar los datos** toosuppress Hola estos caracteres en la comprobación de validación.
2. Revisar y modificar Hola restante. El tipo y el nombre de campo suelen rellenarse automáticamente. Puede cambiar el tipo de datos de Hola hasta que se crea el índice de Hola. Para cambiarlo posteriormente, será necesario recompilar.
3. Establezca los atributos de índice para cada campo:
   
   * Puede recuperar devuelve campo hello en resultados de búsqueda.
   * Filtrables permite hello toobe de campo al que hace referencia en las expresiones de filtro.
   * Que se puede ordenar permite hello toobe de campo utilizado en un criterio de ordenación.
   * Facetable permite campo hello para la navegación por facetas.
   * Searchable permite la búsqueda de texto completo.
4. Haga clic en hello **analizador** pestaña si desea que un analizador de lenguaje en el nivel de campo de hello toospecify. Solo se pueden especificar en este momento los analizadores de lenguaje. Si se usa un analizador personalizado o un analizador que no sea de lenguaje, como palabra clave o patrón, se requerirá código.
   
   * Haga clic en **Searchable** toodesignate texto completo Buscar en el campo de Hola y habilitar la lista de hello analizador de lista desplegable.
   * Elija el analizador de Hola que desee. Para más información, consulte [Creación de un índice para documentos en varios idiomas en Azure Search](search-language-support.md).
5. Haga clic en hello **proveedor de sugerencias** tooenable sugerencias de consulta de escritura en los campos seleccionados.

## <a name="import-your-data"></a>Importar sus datos
1. En **importar los datos**, proporcione un nombre para el indizador de Hola. Recuerde ese producto Hola de hello importar datos asistente es un indizador. Más adelante, si desea que tooview o editarlo, lo seleccionará desde el portal de hello en lugar de volver a ejecutar el Asistente de Hola. 
2. Especifique la programación de hello, que se basa en la zona de horaria regional hello en el que se aprovisiona el servicio Hola.
3. Establecer umbrales de toospecify de opciones avanzadas en si la indización puede continuar si se coloca un documento. Además, puede especificar si **clave** los campos se permiten toocontain espacios y barras diagonales.  
4. Haga clic en **Aceptar** toocreate Hola índice e importar datos de Hola.

Puede supervisar la indización en el portal de Hola. Tal y como se cargan documentos, recuento de documentos de hello crecerá para índice de Hola que ha definido. A veces tarda unos minutos para toopick de página del portal de hello las actualizaciones más recientes de Hola.

índice de Hello es tooquery listo en cuanto se cargan todos los documentos de Hola.

## <a name="query-an-index-using-search-explorer"></a>Realización de consultas en un índice mediante el Explorador de búsqueda

Hola portal incluye **buscar en el explorador** para que pueda consultar un índice sin necesidad de toowrite cualquier código. El [Explorador de búsqueda](search-explorer.md) se puede usar en todos los índices.

Hello experiencia de búsqueda se basa valores predeterminados, como hello [sintaxis simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) y predeterminado [parámetros de consulta searchMode (https://docs.microsoft.com/rest/api/searchservice/search-documents). 

Resultados se devuelven en JSON, en un formato detallado, por lo que le permitirá inspeccionar todo el documento Hola.

## <a name="edit-an-existing-indexer"></a>Edición de un indexador existente
Como se indicó, Asistente para datos de importación de hello crea un **indizador**, que se puede modificar como una construcción independiente en el portal de Hola.

En el panel de servicio de hello, haga doble clic en hello indizador mosaico tooslide una lista de todos los indizadores creado para su suscripción. Haga doble clic en uno de hello indizadores toorun, editarlo o eliminarlo. Puede reemplazar el índice de hello con otro existente, cambiar origen de datos de Hola y establecer las opciones de los umbrales de error durante la indización.

## <a name="edit-an-existing-index"></a>Edición de un índice existente
Asistente de Hello también creado un **índice**. En la búsqueda de Azure, actualizaciones estructural tooan necesitará una regeneración del índice. Una recompilación conlleva Eliminar índice de hello, volver a crear el índice de hello mediante un esquema revisado que tiene cambios de Hola que desee y cargar los datos. Las actualizaciones estructurales incluyen el cambio de un tipo de datos y el cambio de nombre o eliminación de un campo.

Entre las modificaciones que no requieren una recompilación se incluyen la incorporación de un nuevo campo, el cambio los perfiles de puntuación, el cambio de los proveedores de sugerencias o el cambio de los analizadores de lenguaje. Consulte [Actualización de un índice](https://msdn.microsoft.com/library/azure/dn800964.aspx) para más información.


## <a name="next-steps"></a>Pasos siguientes
Revise estos toolearn de vínculos más información acerca de los indizadores:

* [Indexación de Azure SQL Database](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Indexación de Azure Cosmos DB](search-howto-index-documentdb.md)
* [Indexación de Blob Storage](search-howto-indexing-azure-blob-storage.md)
* [Indexación de Table Storage](search-howto-indexing-azure-tables.md)

<!--Image references-->
[1]: ./media/search-import-data-portal/search-import-data-command.png

