---
title: Ejemplos de CLI de base de datos de Azure Cosmos aaaAzure | Documentos de Microsoft
description: "Ejemplos de la CLI de Azure: creación y administración de cuentas, bases de datos, contenedores, regiones y firewalls de Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>Ejemplos de la CLI de Azure para Azure Cosmos DB

Hello tabla siguiente incluye vínculos toosample CLI de Azure secuencias de comandos para la base de datos de Azure Cosmos. Páginas de referencia para todos los comandos de CLI de base de datos de Azure Cosmos están disponibles en hello [Azure CLI 2.0 referencia](https://docs.microsoft.com/cli/azure/cosmosdb).

| |  |
|---|---|
|**Creación de cuentas, bases de datos y contenedores de Azure Cosmos DB**||
|[Creación de una cuenta de API de DocumentDB, API Graph o Table API](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Crea una única cuenta de la API de base de datos de Azure Cosmos, base de datos y contenedor para su uso con hello documentos, gráfico o las API de tabla. |
| [Creación de una cuenta de API de MongoDB](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Creación de una única cuenta, base de datos y colección de API de MongoDB para Azure Cosmos DB. |
|**Escalado de Azure Cosmos DB**||
| [Escalado del rendimiento del contenedor](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Hola cambios aprovisiona througput en un contenedor.|
|[Replicación de la cuenta de base de datos de Azure Cosmos DB en varias regiones y configuración de prioridades de conmutación por error](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Replicación global de datos de la cuenta en varias regiones con una prioridad específica de conmutación por error.|
|**Protección de Azure Cosmos DB**||
| [Obtención de claves de cuenta](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Obtiene las claves de escritura maestro principal y secundaria de Hola y claves primarias y secundarias de solo lectura para la cuenta de hello.|
| [Obtención de la cadena de conexión de MongoDB](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | Obtiene tooconnect de cadena de conexión de hello su tooyour de aplicación de MongoDB cuenta de base de datos de Azure Cosmos.|
|[Regeneración de claves de cuenta](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Vuelve a generar master de Hola o clave de solo lectura para la cuenta de hello.|
|[Creación de un firewall](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| Crea una entrada IP access control directiva toolimit toohello cuenta de acceso de un conjunto de aprobados de máquinas o servicios en la nube.|
|**Alta disponibilidad, recuperación ante desastres, copia de seguridad y restauración**||
|[Configuración de la directiva de conmutación por error](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|Conjuntos de Hola prioridad de conmutación por error de cada región en la que se replica la cuenta de hello.|
|**Conexión de Azure Cosmos DB a los recursos**||
|[Conectar un tooAzure de aplicación web Cosmos DB](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|Creación y conexión a una base de datos de Azure Cosmos DB y creación de una aplicación web de Azure.|
|||
