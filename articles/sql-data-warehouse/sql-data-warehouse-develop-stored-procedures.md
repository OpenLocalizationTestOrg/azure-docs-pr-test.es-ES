---
title: Procedimientos almacenados en SQL Data Warehouse | Microsoft Docs
description: Sugerencias para implementar procedimientos almacenados en el Almacenamiento de datos SQL Azure para el desarrollo de soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: e42d80f0ca35f3fbb67389c66d072bc40d8a8d2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="e2fbe-103">Procedimientos almacenados en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="e2fbe-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="e2fbe-104">El Almacenamiento de datos SQL admite muchas de las características de Transact-SQL que se encuentran en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-104">SQL Data Warehouse supports many of the Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="e2fbe-105">Más importante aún, hay características específicas de escalado horizontal que deseamos utilizar para maximizar el rendimiento de la solución.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-105">More importantly there are scale out specific features that we will want to leverage to maximize the performance of your solution.</span></span>

<span data-ttu-id="e2fbe-106">Sin embargo, para mantener la escala y el rendimiento del Almacenamiento de datos SQL también hay algunas características y funcionalidades que tienen diferencias de comportamiento y otras que no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-106">However, to maintain the scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="e2fbe-107">En este artículo se explica cómo implementar procedimientos almacenados en el Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-107">This article explains how to implement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="e2fbe-108">Introducción a los procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="e2fbe-108">Introducing stored procedures</span></span>
<span data-ttu-id="e2fbe-109">Los procedimientos almacenados son una manera excelente para encapsular el código SQL y almacenarlo cerca de los datos en el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-109">Stored procedures are a great way for encapsulating your SQL code; storing it close to your data in the data warehouse.</span></span> <span data-ttu-id="e2fbe-110">Al encapsular el código en unidades administrables, los procedimientos almacenados ayudan a los programadores a modularizar sus soluciones, de tal manera que facilitan una mayor reutilización del código.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-110">By encapsulating the code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="e2fbe-111">Cada procedimiento almacenado también puede aceptar parámetros para que sean todavía más flexibles.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-111">Each stored procedure can also accept parameters to make them even more flexible.</span></span>

<span data-ttu-id="e2fbe-112">El Almacenamiento de datos SQL proporciona una implementación optimizada y simplificada de procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="e2fbe-113">La diferencia más importante en comparación con SQL Server es que el procedimiento almacenado no es código compilado previamente.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-113">The biggest difference compared to SQL Server is that the stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="e2fbe-114">En los almacenamientos de datos, en general, nos preocupa menos el tiempo de compilación.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-114">In data warehouses we are generally less concerned with the compilation time.</span></span> <span data-ttu-id="e2fbe-115">Es más importante que el código del procedimiento almacenado esté bien optimizado al operar con grandes volúmenes de datos.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-115">It is more important that the stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="e2fbe-116">El objetivo es ahorrar horas, minutos y segundos, no milisegundos.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-116">The goal is to save hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="e2fbe-117">Por lo tanto, resulta más útil pensar en los procedimientos almacenados como contenedores para la lógica SQL.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-117">It is therefore more helpful to think of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="e2fbe-118">Si el Almacenamiento de datos SQL ejecuta el procedimiento almacenado, las instrucciones SQL se distribuyen, traducen y optimizan en el momento de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-118">When SQL Data Warehouse executes your stored procedure the SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="e2fbe-119">Durante este proceso, cada instrucción se convierte en consultas distribuidas.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="e2fbe-120">El código SQL que se ejecuta realmente en los datos es diferente de la consulta enviada.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-120">The SQL code that is actually executed against the data is different to the query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="e2fbe-121">Anidamiento de los procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="e2fbe-121">Nesting stored procedures</span></span>
<span data-ttu-id="e2fbe-122">Cuando los procedimientos almacenados llaman a otros procedimientos almacenados o ejecutan SQL dinámico, se dice que la invocación interna de código o de procedimientos almacenados se anida.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-122">When stored procedures call other stored procedures or execute dynamic sql then the inner stored procedure or code invocation is said to be nested.</span></span>

<span data-ttu-id="e2fbe-123">El Almacenamiento de datos SQL admite un máximo de ocho niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="e2fbe-124">Esto difiere ligeramente de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-124">This is slightly different to SQL Server.</span></span> <span data-ttu-id="e2fbe-125">El nivel de anidamiento en SQL Server es 32.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-125">The nest level in SQL Server is 32.</span></span>

<span data-ttu-id="e2fbe-126">La llamada al procedimiento almacenado de nivel superior es igual al nivel de anidamiento 1.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-126">The top level stored procedure call equates to nest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="e2fbe-127">Si el procedimiento almacenado también realiza otra llamada EXEC, aumentará el nivel de anidación a 2.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-127">If the stored procedure also makes another EXEC call then this will increase the nest level to 2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="e2fbe-128">Si el segundo procedimiento ejecuta luego SQL dinámico, aumentará el nivel de anidación a 3.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-128">If the second procedure then executes some dynamic sql then this will increase the nest level to 3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="e2fbe-129">Tenga en cuenta que SQL Data Warehouse no admite actualmente @@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="e2fbe-130">Debe poder realizar usted mismo un seguimiento de su nivel de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-130">You will need to keep a track of your nest level yourself.</span></span> <span data-ttu-id="e2fbe-131">Es probable que alcance el límite del nivel 8 de anidamiento, pero, en su caso, deberá reprocesar el código y "acoplarlo" para adecuarlo a dicho límite.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-131">It is unlikely you will hit the 8 nest level limit but if you do you will need to re-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="e2fbe-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="e2fbe-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="e2fbe-133">El Almacenamiento de datos SQL no permite utilizar el conjunto de resultados de un procedimiento almacenado con una instrucción INSERT.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-133">SQL Data Warehouse does not permit you to consume the result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="e2fbe-134">Sin embargo, puede utilizar un método alternativo.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="e2fbe-135">Consulte el siguiente artículo sobre las [tablas temporales] para obtener un ejemplo sobre cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-135">Please refer to the following article on [temporary tables] for an example on how to do this.</span></span>

## <a name="limitations"></a><span data-ttu-id="e2fbe-136">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="e2fbe-136">Limitations</span></span>
<span data-ttu-id="e2fbe-137">Existen algunos aspectos de los procedimientos almacenados de Transact-SQL que no se implementan en el Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="e2fbe-138">Son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="e2fbe-138">They are:</span></span>

* <span data-ttu-id="e2fbe-139">Procedimientos almacenados temporales</span><span class="sxs-lookup"><span data-stu-id="e2fbe-139">temporary stored procedures</span></span>
* <span data-ttu-id="e2fbe-140">Procedimientos almacenados numerados</span><span class="sxs-lookup"><span data-stu-id="e2fbe-140">numbered stored procedures</span></span>
* <span data-ttu-id="e2fbe-141">Procedimientos almacenados extendidos</span><span class="sxs-lookup"><span data-stu-id="e2fbe-141">extended stored procedures</span></span>
* <span data-ttu-id="e2fbe-142">Procedimientos almacenados CLR</span><span class="sxs-lookup"><span data-stu-id="e2fbe-142">CLR stored procedures</span></span>
* <span data-ttu-id="e2fbe-143">Opción de cifrado</span><span class="sxs-lookup"><span data-stu-id="e2fbe-143">encryption option</span></span>
* <span data-ttu-id="e2fbe-144">Opción de replicación</span><span class="sxs-lookup"><span data-stu-id="e2fbe-144">replication option</span></span>
* <span data-ttu-id="e2fbe-145">Parámetros con valores de tabla</span><span class="sxs-lookup"><span data-stu-id="e2fbe-145">table-valued parameters</span></span>
* <span data-ttu-id="e2fbe-146">Parámetros de solo lectura</span><span class="sxs-lookup"><span data-stu-id="e2fbe-146">read-only parameters</span></span>
* <span data-ttu-id="e2fbe-147">Parámetros predeterminados</span><span class="sxs-lookup"><span data-stu-id="e2fbe-147">default parameters</span></span>
* <span data-ttu-id="e2fbe-148">Contextos de ejecución</span><span class="sxs-lookup"><span data-stu-id="e2fbe-148">execution contexts</span></span>
* <span data-ttu-id="e2fbe-149">Instrucción de devolución</span><span class="sxs-lookup"><span data-stu-id="e2fbe-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2fbe-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e2fbe-150">Next steps</span></span>
<span data-ttu-id="e2fbe-151">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="e2fbe-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
<span data-ttu-id="e2fbe-152">[tablas temporales]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span><span class="sxs-lookup"><span data-stu-id="e2fbe-152">[temporary tables]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span></span>
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
