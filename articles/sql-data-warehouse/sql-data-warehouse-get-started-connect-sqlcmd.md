---
title: "Conexión a Azure SQL Data Warehouse sqlcmd | Microsoft Docs"
description: "Use la utilidad de línea de comandos [sqlcmd][sqlcmd] para conectar y consultar una instancia de Azure SQL Data Warehouse."
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
ms.openlocfilehash: 5a3fe1046c3417070ba8ff5bd18a0485e2152eff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="c9051-103">Conexión a Almacenamiento de datos SQL con sqlcmd</span><span class="sxs-lookup"><span data-stu-id="c9051-103">Connect to SQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9051-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="c9051-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="c9051-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c9051-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="c9051-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c9051-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="c9051-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="c9051-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="c9051-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="c9051-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="c9051-109">Use la utilidad de línea de comandos [sqlcmd][sqlcmd] para conectarse a Azure SQL Data Warehouse y realizar consultas.</span><span class="sxs-lookup"><span data-stu-id="c9051-109">Use [sqlcmd][sqlcmd] command-line utility to connect to and query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="c9051-110">1. Conectar</span><span class="sxs-lookup"><span data-stu-id="c9051-110">1. Connect</span></span>
<span data-ttu-id="c9051-111">Para empezar a trabajar con [sqlcmd][sqlcmd], abra el símbolo del sistema y escriba **sqlcmd**, seguido de la cadena de conexión de la base de datos de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c9051-111">To get started with [sqlcmd][sqlcmd], open the command prompt and enter **sqlcmd** followed by the connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="c9051-112">La cadena de conexión requiere los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="c9051-112">The connection string requires the following parameters:</span></span>

* <span data-ttu-id="c9051-113">**Server (-S):** servidor con el formato `<`Nombre del servidor`>`.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="c9051-113">**Server (-S):** Server in the form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="c9051-114">**Base de datos (-d):** nombre de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="c9051-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="c9051-115">**Habilitar identificadores entre comillas (-I):** los identificadores entre comillas deben estar habilitados para poder conectarse a una instancia de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c9051-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled to connect to a SQL Data Warehouse instance.</span></span>

<span data-ttu-id="c9051-116">Para utilizar la autenticación de SQL Server, debe agregar los parámetros de nombre de usuario y contraseña:</span><span class="sxs-lookup"><span data-stu-id="c9051-116">To use SQL Server Authentication, you need to add the username/password parameters:</span></span>

* <span data-ttu-id="c9051-117">**Usuario (-U):** usuario de servidor con el formato `<`usuario`>`</span><span class="sxs-lookup"><span data-stu-id="c9051-117">**User (-U):** Server user in the form `<`User`>`</span></span>
* <span data-ttu-id="c9051-118">**Contraseña (-P):** la contraseña asociada con el usuario.</span><span class="sxs-lookup"><span data-stu-id="c9051-118">**Password (-P):** Password associated with the user.</span></span>

<span data-ttu-id="c9051-119">Por ejemplo, la cadena de conexión podría ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="c9051-119">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="c9051-120">Para usar la autenticación integrada de Azure Active Directory, debe agregar los parámetros de Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="c9051-120">To use Azure Active Directory Integrated authentication, you need to add the Azure Active Directory parameters:</span></span>

* <span data-ttu-id="c9051-121">**Autenticación de Azure Active Directory (-G):** use Azure Active Directory para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="c9051-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="c9051-122">Por ejemplo, la cadena de conexión podría ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="c9051-122">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> <span data-ttu-id="c9051-123">Necesita [habilitar la autenticación de Azure Active Directory](sql-data-warehouse-authentication.md) para autenticarse con Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c9051-123">You need to [enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) to authenticate using Active Directory.</span></span>
> 
> 

## <a name="2-query"></a><span data-ttu-id="c9051-124">2. Consultar</span><span class="sxs-lookup"><span data-stu-id="c9051-124">2. Query</span></span>
<span data-ttu-id="c9051-125">Después de la conexión, puede emitir cualquier instrucción Transact-SQL en la instancia.</span><span class="sxs-lookup"><span data-stu-id="c9051-125">After connection, you can issue any supported Transact-SQL statements against the instance.</span></span>  <span data-ttu-id="c9051-126">En este ejemplo, las consultas se envían en modo interactivo.</span><span class="sxs-lookup"><span data-stu-id="c9051-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="c9051-127">Los siguientes ejemplos muestran cómo se pueden ejecutar las consultas en el modo por lotes con la opción -Q o mediante la canalización de su SQL a sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="c9051-127">These next examples show how you can run your queries in batch mode using the -Q option or piping your SQL to sqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="c9051-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9051-128">Next steps</span></span>
<span data-ttu-id="c9051-129">Para más información sobre las opciones disponibles en sqlcmd, consulte la [documentación de sqlcmd][sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="c9051-129">See [sqlcmd documentation][sqlcmd] for more about details about the options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
