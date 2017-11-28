---
title: aaaDesign primer Azure base de datos SQL - C# | Documentos de Microsoft
description: "Obtenga información acerca de toodesign la primera base de datos de SQL Azure y conéctese tooit con un programa de C# mediante ADO.NET."
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="19315-103">Diseño de una base de datos de SQL Azure Database y conexión con C&#x23; y ADO.NET</span><span class="sxs-lookup"><span data-stu-id="19315-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="19315-104">La base de datos de SQL Azure es un base de datos como un servicio relacional (DBaaS) Hola Microsoft Cloud ("Azure").</span><span class="sxs-lookup"><span data-stu-id="19315-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="19315-105">En este tutorial, aprenderá cómo toouse Hola portal de Azure y ADO.NET con Visual Studio para:</span><span class="sxs-lookup"><span data-stu-id="19315-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="19315-106">Crear una base de datos en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="19315-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="19315-107">Configurar una regla de firewall de nivel de servidor en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="19315-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="19315-108">Conectar la base de datos de toohello con ADO.NET y Visual Studio</span><span class="sxs-lookup"><span data-stu-id="19315-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="19315-109">Crear tablas con ADO.NET</span><span class="sxs-lookup"><span data-stu-id="19315-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="19315-110">Insertar, actualizar y eliminar datos con ADO.NET</span><span class="sxs-lookup"><span data-stu-id="19315-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="19315-111">Consultar datos con ADO.NET</span><span class="sxs-lookup"><span data-stu-id="19315-111">Query data ADO.NET</span></span>

<span data-ttu-id="19315-112">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="19315-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19315-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="19315-113">Prerequisites</span></span>

<span data-ttu-id="19315-114">Una instalación de [Visual Studio Community 2017, Visual Studio Professional 2017 o Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="19315-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="19315-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19315-115">Next steps</span></span>

<span data-ttu-id="19315-116">En este tutorial, ha aprendido las tareas básicas de la base de datos, como crean una base de datos y tablas, cargar y consultar los datos y restaurar el punto anterior de tooa de base de datos de hello en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="19315-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="19315-117">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="19315-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="19315-118">Crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="19315-118">Create a database</span></span>
> * <span data-ttu-id="19315-119">Configurar una regla de firewall</span><span class="sxs-lookup"><span data-stu-id="19315-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="19315-120">Conectar la base de datos de toohello con [C# y Visual Studio](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="19315-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="19315-121">Cree las tablas.</span><span class="sxs-lookup"><span data-stu-id="19315-121">Create tables</span></span>
> * <span data-ttu-id="19315-122">Insertar, actualizar y eliminar datos</span><span class="sxs-lookup"><span data-stu-id="19315-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="19315-123">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="19315-123">Query data</span></span>

<span data-ttu-id="19315-124">Avanzar toohello toolearn de tutorial siguiente sobre cómo migrar los datos.</span><span class="sxs-lookup"><span data-stu-id="19315-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="19315-125">Migrar su tooAzure de base de datos base de datos SQL de SQL Server</span><span class="sxs-lookup"><span data-stu-id="19315-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

