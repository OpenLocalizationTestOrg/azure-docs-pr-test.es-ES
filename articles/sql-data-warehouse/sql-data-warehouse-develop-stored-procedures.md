---
title: "procedimientos de aaaStored en el almacén de datos de SQL | Documentos de Microsoft"
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
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="5879c-103">Procedimientos almacenados en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="5879c-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="5879c-104">Almacenamiento de datos SQL es compatible con muchas características de Transact-SQL de Hola que se encuentran en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5879c-104">SQL Data Warehouse supports many of hello Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="5879c-105">Lo más importante es que hay características específicas que deseamos rendimiento de hello tooleverage toomaximize de la solución de escalado horizontal.</span><span class="sxs-lookup"><span data-stu-id="5879c-105">More importantly there are scale out specific features that we will want tooleverage toomaximize hello performance of your solution.</span></span>

<span data-ttu-id="5879c-106">Sin embargo, escala de hello toomaintain y el rendimiento de almacenamiento de datos SQL no existe también son algunas de las características y funcionalidad que tienen diferencias de comportamiento y otros que no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="5879c-106">However, toomaintain hello scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="5879c-107">Este artículo explica cómo tooimplement almacenan los procedimientos de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="5879c-107">This article explains how tooimplement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="5879c-108">Introducción a los procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="5879c-108">Introducing stored procedures</span></span>
<span data-ttu-id="5879c-109">Los procedimientos almacenados son una excelente manera de encapsular el código SQL; almacenarlos tooyour cerrar datos en almacenamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5879c-109">Stored procedures are a great way for encapsulating your SQL code; storing it close tooyour data in hello data warehouse.</span></span> <span data-ttu-id="5879c-110">Encapsular el código de hello en unidades administrables procedimientos almacenados ayudan a los desarrolladores modularizar sus soluciones; facilitación de mayor reutilización del código.</span><span class="sxs-lookup"><span data-stu-id="5879c-110">By encapsulating hello code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="5879c-111">Cada procedimiento almacenado puede aceptar parámetros toomake ellos incluso más flexible.</span><span class="sxs-lookup"><span data-stu-id="5879c-111">Each stored procedure can also accept parameters toomake them even more flexible.</span></span>

<span data-ttu-id="5879c-112">El Almacenamiento de datos SQL proporciona una implementación optimizada y simplificada de procedimientos almacenados.</span><span class="sxs-lookup"><span data-stu-id="5879c-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="5879c-113">Hola mayor diferencia en comparación con tooSQL Server es que Hola procedimiento almacenado no es código previamente compilado.</span><span class="sxs-lookup"><span data-stu-id="5879c-113">hello biggest difference compared tooSQL Server is that hello stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="5879c-114">En los almacenes de datos nos interesan generalmente menos con el tiempo de compilación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5879c-114">In data warehouses we are generally less concerned with hello compilation time.</span></span> <span data-ttu-id="5879c-115">Es más importante que el código del procedimiento almacenado de hello correctamente está optimizado cuando se trabaja con grandes volúmenes de datos.</span><span class="sxs-lookup"><span data-stu-id="5879c-115">It is more important that hello stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="5879c-116">objetivo de Hello es toosave horas, minutos y segundos no milisegundos.</span><span class="sxs-lookup"><span data-stu-id="5879c-116">hello goal is toosave hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="5879c-117">Por lo tanto, es más útil toothink de procedimientos almacenados como contenedores para la lógica SQL.</span><span class="sxs-lookup"><span data-stu-id="5879c-117">It is therefore more helpful toothink of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="5879c-118">Cuando se ejecuta el almacén de datos SQL las instrucciones de procedimiento almacenado Hola SQL son analizar, se traducen y optimizadas en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="5879c-118">When SQL Data Warehouse executes your stored procedure hello SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="5879c-119">Durante este proceso, cada instrucción se convierte en consultas distribuidas.</span><span class="sxs-lookup"><span data-stu-id="5879c-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="5879c-120">Hola código SQL que se ejecuta realmente en datos de hello es consulta toohello diferentes enviada.</span><span class="sxs-lookup"><span data-stu-id="5879c-120">hello SQL code that is actually executed against hello data is different toohello query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="5879c-121">Anidamiento de los procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="5879c-121">Nesting stored procedures</span></span>
<span data-ttu-id="5879c-122">Cuando los procedimientos almacenados llamar a otros procedimientos almacenados o ejecutar sql dinámico, a continuación, interna de hello del procedimiento almacenado o la invocación de código se dice que toobe anidados.</span><span class="sxs-lookup"><span data-stu-id="5879c-122">When stored procedures call other stored procedures or execute dynamic sql then hello inner stored procedure or code invocation is said toobe nested.</span></span>

<span data-ttu-id="5879c-123">El Almacenamiento de datos SQL admite un máximo de ocho niveles de anidamiento.</span><span class="sxs-lookup"><span data-stu-id="5879c-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="5879c-124">Esto es ligeramente diferente tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="5879c-124">This is slightly different tooSQL Server.</span></span> <span data-ttu-id="5879c-125">nivel de anidamiento de Hello en SQL Server es 32.</span><span class="sxs-lookup"><span data-stu-id="5879c-125">hello nest level in SQL Server is 32.</span></span>

<span data-ttu-id="5879c-126">llamada de procedimiento almacenado de nivel superior de Hello equivale toonest nivel 1</span><span class="sxs-lookup"><span data-stu-id="5879c-126">hello top level stored procedure call equates toonest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="5879c-127">Si almacena Hola procedimiento también realiza EXEC otra llamada, a continuación, Esto aumentará too2 de nivel de anidamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="5879c-127">If hello stored procedure also makes another EXEC call then this will increase hello nest level too2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="5879c-128">Si el segundo procedimiento de hello, a continuación, ejecuta algunos sql dinámico, a continuación, Esto aumentará too3 de nivel de anidamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="5879c-128">If hello second procedure then executes some dynamic sql then this will increase hello nest level too3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="5879c-129">Tenga en cuenta que SQL Data Warehouse no admite actualmente @@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="5879c-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="5879c-130">Deberá tookeep un seguimiento de su nivel de anidamiento usted mismo.</span><span class="sxs-lookup"><span data-stu-id="5879c-130">You will need tookeep a track of your nest level yourself.</span></span> <span data-ttu-id="5879c-131">No es probable alcanzará el límite de niveles de anidamiento de hello 8, pero si lo hace, necesitará toore-trabajo del código y "acoplarla" para que quepa dentro de este límite.</span><span class="sxs-lookup"><span data-stu-id="5879c-131">It is unlikely you will hit hello 8 nest level limit but if you do you will need toore-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="5879c-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="5879c-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="5879c-133">Almacenamiento de datos SQL no le permiten conjunto de resultados de hello tooconsume de un procedimiento almacenado con una instrucción INSERT.</span><span class="sxs-lookup"><span data-stu-id="5879c-133">SQL Data Warehouse does not permit you tooconsume hello result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="5879c-134">Sin embargo, puede utilizar un método alternativo.</span><span class="sxs-lookup"><span data-stu-id="5879c-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="5879c-135">Consulte toohello siguiente artículo de [tablas temporales] para obtener un ejemplo sobre cómo toodo esto.</span><span class="sxs-lookup"><span data-stu-id="5879c-135">Please refer toohello following article on [temporary tables] for an example on how toodo this.</span></span>

## <a name="limitations"></a><span data-ttu-id="5879c-136">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="5879c-136">Limitations</span></span>
<span data-ttu-id="5879c-137">Existen algunos aspectos de los procedimientos almacenados de Transact-SQL que no se implementan en el Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="5879c-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="5879c-138">Son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="5879c-138">They are:</span></span>

* <span data-ttu-id="5879c-139">Procedimientos almacenados temporales</span><span class="sxs-lookup"><span data-stu-id="5879c-139">temporary stored procedures</span></span>
* <span data-ttu-id="5879c-140">Procedimientos almacenados numerados</span><span class="sxs-lookup"><span data-stu-id="5879c-140">numbered stored procedures</span></span>
* <span data-ttu-id="5879c-141">Procedimientos almacenados extendidos</span><span class="sxs-lookup"><span data-stu-id="5879c-141">extended stored procedures</span></span>
* <span data-ttu-id="5879c-142">Procedimientos almacenados CLR</span><span class="sxs-lookup"><span data-stu-id="5879c-142">CLR stored procedures</span></span>
* <span data-ttu-id="5879c-143">Opción de cifrado</span><span class="sxs-lookup"><span data-stu-id="5879c-143">encryption option</span></span>
* <span data-ttu-id="5879c-144">Opción de replicación</span><span class="sxs-lookup"><span data-stu-id="5879c-144">replication option</span></span>
* <span data-ttu-id="5879c-145">Parámetros con valores de tabla</span><span class="sxs-lookup"><span data-stu-id="5879c-145">table-valued parameters</span></span>
* <span data-ttu-id="5879c-146">Parámetros de solo lectura</span><span class="sxs-lookup"><span data-stu-id="5879c-146">read-only parameters</span></span>
* <span data-ttu-id="5879c-147">Parámetros predeterminados</span><span class="sxs-lookup"><span data-stu-id="5879c-147">default parameters</span></span>
* <span data-ttu-id="5879c-148">Contextos de ejecución</span><span class="sxs-lookup"><span data-stu-id="5879c-148">execution contexts</span></span>
* <span data-ttu-id="5879c-149">Instrucción de devolución</span><span class="sxs-lookup"><span data-stu-id="5879c-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="5879c-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5879c-150">Next steps</span></span>
<span data-ttu-id="5879c-151">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="5879c-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[tablas temporales]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
