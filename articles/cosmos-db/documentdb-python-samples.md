---
title: ejemplos de Python aaaDocumentDB API de base de datos de Azure Cosmos | Documentos de Microsoft
description: Busque ejemplos de Python en GitHub para tareas comunes en Azure Cosmos DB, incluidas las operaciones CRUD.
keywords: Ejemplos de Python
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2016
ms.author: moderakh
ms.openlocfilehash: d8f240782b0997f2d32b68d310dc6f4ff6cb36d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-examples"></a>Ejemplos de Python para Azure Cosmos DB
> [!div class="op_single_selector"]
> * [Ejemplos de .NET](documentdb-dotnet-samples.md)
> * [Ejemplos de Node.js](documentdb-nodejs-samples.md)
> * [Ejemplos de Python](documentdb-python-samples.md)
> * [Galería de ejemplos de código de Azure](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

Soluciones de ejemplo que realizan operaciones CRUD y otras operaciones comunes en los recursos de base de datos de Azure Cosmos se incluyen en hello [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) repositorio de GitHub. Este artículo ofrece:

* Tareas de toohello de vínculos en cada uno de los archivos de proyecto de ejemplo de Hola Python. 
* Toohello de vínculos relacionados con contenido de referencia de API.

**Requisitos previos**

1. Necesita una cuenta de Azure toouse estos ejemplos de Python:
   * También puede [abrir una cuenta de Azure de forma gratuita](https://azure.microsoft.com/pricing/free-trial/): obtenga créditos puede usar tootry los servicios de Azure de pago e incluso después de que se utilizan hasta puede mantener la cuenta de hello y libre de usar servicios de Azure, como sitios Web. Nunca se cargará su tarjeta de crédito a menos que cambiar la configuración y pida toobe cobrado explícitamente.
     * Puede [activar los beneficios de suscriptor de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/): su suscripción a Visual Studio le proporciona crédito todos los meses que puede usar con servicios de Azure de pago.
2. También necesita hello [SDK de Python](documentdb-sdk-python.md). 
   
   > [!NOTE]
   > Cada ejemplo es independiente, es decir, se configura a sí mismo y posteriormente se limpia solo. Por lo tanto, los ejemplos de hello emiten varias llamadas demasiado[document_client. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html). Cada vez que esto se realiza la suscripción le facturará una hora de uso por nivel de rendimiento de Hola de colección de Hola que se está creando. 
   > 
   > 

## <a name="database-examples"></a>Ejemplos de base de datos
Hola [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) archivo de hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) proyecto muestra cómo hello tooperform después de las tareas.

| Tarea | Referencia de API |
| --- | --- |
| [Creación de una base de datos](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[document_client.CreateDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Consultar una base de datos de una cuenta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[document_client.QueryDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Leer una base de datos por identificador](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[document_client.ReadDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Enumerar bases de datos de una cuenta](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[document_client.ReadDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [Eliminar una base de datos](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[document_client.DeleteDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a>Ejemplos de colección
Hola [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) archivo de hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) proyecto muestra cómo hello tooperform después de las tareas.

| Tarea | Referencia de API |
| --- | --- |
| [Creación de una colección](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Leer una lista de todas las colecciones en una base de datos](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[document_client.ListCollections](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Obtención de una colección por identificador](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[document_client.ReadCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Obtención del nivel de rendimiento de una colección](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[DocumentQueryable.QueryOffers](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Cambio del nivel de rendimiento de una colección](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[document_client.ReplaceOffer](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [Eliminación de un colección](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[document_client.DeleteCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

