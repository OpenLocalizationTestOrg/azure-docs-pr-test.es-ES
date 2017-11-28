---
title: "variables de aaaAssign en el almacén de datos de SQL | Documentos de Microsoft"
description: "Sugerencias para la asignación de variables de Transact-SQL en el Almacenamiento de datos SQL Azure para desarrollar soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="3b600-103">Asignación de variables en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3b600-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="3b600-104">Las variables en el almacén de datos de SQL se establecen mediante hello `DECLARE` instrucción o hello `SET` instrucción.</span><span class="sxs-lookup"><span data-stu-id="3b600-104">Variables in SQL Data Warehouse are set using hello `DECLARE` statement or hello `SET` statement.</span></span>

<span data-ttu-id="3b600-105">Todos Hola siguientes son formas perfectamente válidos tooset un valor de variable:</span><span class="sxs-lookup"><span data-stu-id="3b600-105">All of hello following are perfectly valid ways tooset a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="3b600-106">Configuración de variables con DECLARE</span><span class="sxs-lookup"><span data-stu-id="3b600-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="3b600-107">Inicializar variables con DECLARE es uno de hello más flexible formas tooset un valor de la variable en el almacén de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="3b600-107">Initializing variables with DECLARE is one of hello most flexible ways tooset a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="3b600-108">También puede utilizar DECLARE tooset más de una variable a la vez.</span><span class="sxs-lookup"><span data-stu-id="3b600-108">You can also use DECLARE tooset more than one variable at a time.</span></span> <span data-ttu-id="3b600-109">No se puede utilizar `SELECT` o `UPDATE` toodo esto:</span><span class="sxs-lookup"><span data-stu-id="3b600-109">You cannot use `SELECT` or `UPDATE` toodo this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="3b600-110">No se puede inicializar y utilizar una variable en hello misma instrucción DECLARE.</span><span class="sxs-lookup"><span data-stu-id="3b600-110">You cannot initialise and use a variable in hello same DECLARE statement.</span></span> <span data-ttu-id="3b600-111">ejemplo de Hola de tooillustrate Hola punto es **no** permitido como @p1 tanto inicializado y usar en hello misma instrucción DECLARE.</span><span class="sxs-lookup"><span data-stu-id="3b600-111">tooillustrate hello point hello example below is **not** allowed as @p1 is both initialized and used in hello same DECLARE statement.</span></span> <span data-ttu-id="3b600-112">Esto generará un error.</span><span class="sxs-lookup"><span data-stu-id="3b600-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="3b600-113">Configuración de valores con SET</span><span class="sxs-lookup"><span data-stu-id="3b600-113">Setting values with SET</span></span>
<span data-ttu-id="3b600-114">SET es un método muy común para configurar una sola variable.</span><span class="sxs-lookup"><span data-stu-id="3b600-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="3b600-115">Todos ejemplos de hello siguientes son formas válidas de establecer una variable con el conjunto:</span><span class="sxs-lookup"><span data-stu-id="3b600-115">All of hello examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="3b600-116">Solo puede establecer una variable al mismo tiempo con SET.</span><span class="sxs-lookup"><span data-stu-id="3b600-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="3b600-117">Sin embargo, como hemos visto anteriormente, se admiten los operadores compuestos.</span><span class="sxs-lookup"><span data-stu-id="3b600-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="3b600-118">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="3b600-118">Limitations</span></span>
<span data-ttu-id="3b600-119">Puede usar SELECT o UPDATE para la asignación de variables.</span><span class="sxs-lookup"><span data-stu-id="3b600-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b600-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b600-120">Next steps</span></span>
<span data-ttu-id="3b600-121">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="3b600-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
