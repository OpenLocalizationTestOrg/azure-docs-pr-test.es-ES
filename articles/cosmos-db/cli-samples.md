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
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="6abfd-103">Ejemplos de la CLI de Azure para Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6abfd-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="6abfd-104">Hello tabla siguiente incluye vínculos toosample CLI de Azure secuencias de comandos para la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6abfd-104">hello following table includes links toosample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="6abfd-105">Páginas de referencia para todos los comandos de CLI de base de datos de Azure Cosmos están disponibles en hello [Azure CLI 2.0 referencia](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="6abfd-105">Reference pages for all Azure Cosmos DB CLI commands are available in hello [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="6abfd-106">**Creación de cuentas, bases de datos y contenedores de Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="6abfd-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="6abfd-107">Creación de una cuenta de API de DocumentDB, API Graph o Table API</span><span class="sxs-lookup"><span data-stu-id="6abfd-107">Create a DocumentDB API, Graph, or Table API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="6abfd-108">Crea una única cuenta de la API de base de datos de Azure Cosmos, base de datos y contenedor para su uso con hello documentos, gráfico o las API de tabla.</span><span class="sxs-lookup"><span data-stu-id="6abfd-108">Creates a single Azure Cosmos DB API account, database, and container for use with hello DocumentDB, Graph, or Table APIs.</span></span> |
| [<span data-ttu-id="6abfd-109">Creación de una cuenta de API de MongoDB</span><span class="sxs-lookup"><span data-stu-id="6abfd-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="6abfd-110">Creación de una única cuenta, base de datos y colección de API de MongoDB para Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6abfd-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
|<span data-ttu-id="6abfd-111">**Escalado de Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="6abfd-111">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="6abfd-112">Escalado del rendimiento del contenedor</span><span class="sxs-lookup"><span data-stu-id="6abfd-112">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="6abfd-113">Hola cambios aprovisiona througput en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="6abfd-113">Changes hello provisioned througput on a container.</span></span>|
|[<span data-ttu-id="6abfd-114">Replicación de la cuenta de base de datos de Azure Cosmos DB en varias regiones y configuración de prioridades de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="6abfd-114">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="6abfd-115">Replicación global de datos de la cuenta en varias regiones con una prioridad específica de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="6abfd-115">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="6abfd-116">**Protección de Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="6abfd-116">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="6abfd-117">Obtención de claves de cuenta</span><span class="sxs-lookup"><span data-stu-id="6abfd-117">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="6abfd-118">Obtiene las claves de escritura maestro principal y secundaria de Hola y claves primarias y secundarias de solo lectura para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="6abfd-118">Gets hello primary and secondary master write keys and primary and secondary read-only keys for hello account.</span></span>|
| [<span data-ttu-id="6abfd-119">Obtención de la cadena de conexión de MongoDB</span><span class="sxs-lookup"><span data-stu-id="6abfd-119">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="6abfd-120">Obtiene tooconnect de cadena de conexión de hello su tooyour de aplicación de MongoDB cuenta de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6abfd-120">Gets hello connection string tooconnect your MongoDB app tooyour Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="6abfd-121">Regeneración de claves de cuenta</span><span class="sxs-lookup"><span data-stu-id="6abfd-121">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="6abfd-122">Vuelve a generar master de Hola o clave de solo lectura para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="6abfd-122">Regenerates hello master or read-only key for hello account.</span></span>|
|[<span data-ttu-id="6abfd-123">Creación de un firewall</span><span class="sxs-lookup"><span data-stu-id="6abfd-123">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="6abfd-124">Crea una entrada IP access control directiva toolimit toohello cuenta de acceso de un conjunto de aprobados de máquinas o servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="6abfd-124">Creates an inbound IP access control policy toolimit access toohello account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="6abfd-125">**Alta disponibilidad, recuperación ante desastres, copia de seguridad y restauración**</span><span class="sxs-lookup"><span data-stu-id="6abfd-125">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="6abfd-126">Configuración de la directiva de conmutación por error</span><span class="sxs-lookup"><span data-stu-id="6abfd-126">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="6abfd-127">Conjuntos de Hola prioridad de conmutación por error de cada región en la que se replica la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="6abfd-127">Sets hello failover priority of each region in which hello account is replicated.</span></span>|
|<span data-ttu-id="6abfd-128">**Conexión de Azure Cosmos DB a los recursos**</span><span class="sxs-lookup"><span data-stu-id="6abfd-128">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="6abfd-129">Conectar un tooAzure de aplicación web Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6abfd-129">Connect a web app tooAzure Cosmos DB</span></span>](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="6abfd-130">Creación y conexión a una base de datos de Azure Cosmos DB y creación de una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="6abfd-130">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
