---
title: sqlcmd de almacenamiento de datos SQL de aaaConnect tooAzure | Documentos de Microsoft
description: "Use [sqlcmd] [sqlcmd] Utilidad de línea de comandos tooconnect tooand consulta un almacén de datos de SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="d68b7-103">Conectar tooSQL almacenamiento de datos con sqlcmd</span><span class="sxs-lookup"><span data-stu-id="d68b7-103">Connect tooSQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d68b7-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="d68b7-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="d68b7-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d68b7-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="d68b7-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d68b7-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="d68b7-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="d68b7-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="d68b7-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="d68b7-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="d68b7-109">Use [sqlcmd] [ sqlcmd] tooand tooconnect de utilidad de línea de comandos de consulta un almacén de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d68b7-109">Use [sqlcmd][sqlcmd] command-line utility tooconnect tooand query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="d68b7-110">1. Conectar</span><span class="sxs-lookup"><span data-stu-id="d68b7-110">1. Connect</span></span>
<span data-ttu-id="d68b7-111">partió tooget [sqlcmd][sqlcmd], abra el símbolo del sistema de Hola y escriba **sqlcmd** seguido por la cadena de conexión de hello para la base de datos de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d68b7-111">tooget started with [sqlcmd][sqlcmd], open hello command prompt and enter **sqlcmd** followed by hello connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="d68b7-112">cadena de conexión de Hello requiere Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="d68b7-112">hello connection string requires hello following parameters:</span></span>

* <span data-ttu-id="d68b7-113">**Servidor (-S):** servidor en forma de hello `<`nombre del servidor`>`. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="d68b7-113">**Server (-S):** Server in hello form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="d68b7-114">**Base de datos (-d):** nombre de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="d68b7-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="d68b7-115">**Habilitar los identificadores entre comillas (-I):** identificadores entre comillas deben ser una instancia de almacenamiento de datos SQL de tooa tooconnect habilitado.</span><span class="sxs-lookup"><span data-stu-id="d68b7-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled tooconnect tooa SQL Data Warehouse instance.</span></span>

<span data-ttu-id="d68b7-116">toouse autenticación de SQL Server, necesita parámetros de nombre de usuario/contraseña Hola tooadd:</span><span class="sxs-lookup"><span data-stu-id="d68b7-116">toouse SQL Server Authentication, you need tooadd hello username/password parameters:</span></span>

* <span data-ttu-id="d68b7-117">**Usuario (-U):** usuario de servidor en forma de hello `<`usuario`>`</span><span class="sxs-lookup"><span data-stu-id="d68b7-117">**User (-U):** Server user in hello form `<`User`>`</span></span>
* <span data-ttu-id="d68b7-118">**Contraseña (-P):** contraseña asociada con el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="d68b7-118">**Password (-P):** Password associated with hello user.</span></span>

<span data-ttu-id="d68b7-119">Por ejemplo, la cadena de conexión podría ser similar a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="d68b7-119">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="d68b7-120">autenticación de Azure Active Directory integrado toouse, necesita parámetros de tooadd hello Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="d68b7-120">toouse Azure Active Directory Integrated authentication, you need tooadd hello Azure Active Directory parameters:</span></span>

* <span data-ttu-id="d68b7-121">**Autenticación de Azure Active Directory (-G):** use Azure Active Directory para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="d68b7-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="d68b7-122">Por ejemplo, la cadena de conexión podría ser similar a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="d68b7-122">For example, your connection string might look like hello following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="d68b7-123">Necesita demasiado[Habilitar autenticación de Azure Active Directory](sql-data-warehouse-authentication.md) tooauthenticate mediante Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d68b7-123">You need too[enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) tooauthenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="d68b7-124">2. Consultar</span><span class="sxs-lookup"><span data-stu-id="d68b7-124">2. Query</span></span>
<span data-ttu-id="d68b7-125">Después de la conexión, puede emitir cualquier instrucciones de Transact-SQL compatibles con la instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="d68b7-125">After connection, you can issue any supported Transact-SQL statements against hello instance.</span></span>  <span data-ttu-id="d68b7-126">En este ejemplo, las consultas se envían en modo interactivo.</span><span class="sxs-lookup"><span data-stu-id="d68b7-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="d68b7-127">Estos ejemplos siguientes muestra cómo puede ejecutar las consultas en modo de lote con opción -Q de Hola o canalizando el toosqlcmd SQL.</span><span class="sxs-lookup"><span data-stu-id="d68b7-127">These next examples show how you can run your queries in batch mode using hello -Q option or piping your SQL toosqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="d68b7-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d68b7-128">Next steps</span></span>
<span data-ttu-id="d68b7-129">Vea [documentación de sqlcmd] [ sqlcmd] para obtener más información acerca de los detalles acerca de las opciones de hello disponibles en sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="d68b7-129">See [sqlcmd documentation][sqlcmd] for more about details about hello options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
