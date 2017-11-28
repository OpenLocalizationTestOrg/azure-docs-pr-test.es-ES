---
title: "aaaTransactions en el almacén de datos de SQL | Documentos de Microsoft"
description: Sugerencias para implementar transacciones en el Almacenamiento de datos SQL Azure para el desarrollo de soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a><span data-ttu-id="670ce-103">Transacciones en el Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="670ce-103">Transactions in SQL Data Warehouse</span></span>
<span data-ttu-id="670ce-104">Como cabría esperar, almacenamiento de datos SQL admite transacciones como parte de la carga de trabajo de almacenamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="670ce-104">As you would expect, SQL Data Warehouse supports transactions as part of hello data warehouse workload.</span></span> <span data-ttu-id="670ce-105">Sin embargo, rendimiento de hello tooensure de almacenamiento de datos de SQL se mantiene a escala que algunas características están limitadas cuando comparado tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="670ce-105">However, tooensure hello performance of SQL Data Warehouse is maintained at scale some features are limited when compared tooSQL Server.</span></span> <span data-ttu-id="670ce-106">Este artículo resalta las diferencias de Hola y Hola listas de otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="670ce-106">This article highlights hello differences and lists hello others.</span></span> 

## <a name="transaction-isolation-levels"></a><span data-ttu-id="670ce-107">Niveles de aislamiento de transacciones</span><span class="sxs-lookup"><span data-stu-id="670ce-107">Transaction isolation levels</span></span>
<span data-ttu-id="670ce-108">El Almacenamiento de datos SQL implementa las transacciones ACID.</span><span class="sxs-lookup"><span data-stu-id="670ce-108">SQL Data Warehouse implements ACID transactions.</span></span> <span data-ttu-id="670ce-109">Sin embargo, aislamiento de compatibilidad transaccional Hola Hola se limita demasiado`READ UNCOMMITTED` y no puede cambiarse.</span><span class="sxs-lookup"><span data-stu-id="670ce-109">However, hello Isolation of hello transactional support is limited too`READ UNCOMMITTED` and this cannot be changed.</span></span> <span data-ttu-id="670ce-110">Puede implementar una serie de métodos de codificación tooprevent desfasada lee de datos si se trata de un problema para usted.</span><span class="sxs-lookup"><span data-stu-id="670ce-110">You can implement a number of coding methods tooprevent dirty reads of data if this is a concern for you.</span></span> <span data-ttu-id="670ce-111">Hello más populares métodos aprovechan CTAS y modificación de particiones de tabla (a menudo conocido como Hola patrón de ventana deslizante) tooprevent a los usuarios de consultar los datos aún se está preparando.</span><span class="sxs-lookup"><span data-stu-id="670ce-111">hello most popular methods leverage both CTAS and table partition switching (often known as hello sliding window pattern) tooprevent users from querying data that is still being prepared.</span></span> <span data-ttu-id="670ce-112">Vistas que filtran previamente los datos de hello también es un enfoque popular.</span><span class="sxs-lookup"><span data-stu-id="670ce-112">Views that pre-filter hello data is also a popular approach.</span></span>  

## <a name="transaction-size"></a><span data-ttu-id="670ce-113">Tamaño de la transacción</span><span class="sxs-lookup"><span data-stu-id="670ce-113">Transaction size</span></span>
<span data-ttu-id="670ce-114">Una transacción de modificación de datos única tiene un tamaño limitado.</span><span class="sxs-lookup"><span data-stu-id="670ce-114">A single data modification transaction is limited in size.</span></span> <span data-ttu-id="670ce-115">Hola hoy en día se aplique el límite "por distribución".</span><span class="sxs-lookup"><span data-stu-id="670ce-115">hello limit today is applied "per distribution".</span></span> <span data-ttu-id="670ce-116">Por lo tanto, se puede calcular la asignación total Hola multiplicando el límite de Hola por recuento de distribución de Hola.</span><span class="sxs-lookup"><span data-stu-id="670ce-116">Therefore, hello total allocation can be calculated by multiplying hello limit by hello distribution count.</span></span> <span data-ttu-id="670ce-117">número máximo de hello tooapproximate de filas de la transacción de hello divide cap de distribución de Hola por tamaño total de Hola de cada fila.</span><span class="sxs-lookup"><span data-stu-id="670ce-117">tooapproximate hello maximum number of rows in hello transaction divide hello distribution cap by hello total size of each row.</span></span> <span data-ttu-id="670ce-118">Columnas de longitud variable considere la posibilidad de tomar una longitud de la columna promedio, en lugar de usar tamaño máximo de Hola.</span><span class="sxs-lookup"><span data-stu-id="670ce-118">For variable length columns consider taking an average column length rather than using hello maximum size.</span></span>

<span data-ttu-id="670ce-119">En la tabla Hola Hola se realizaron suposiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="670ce-119">In hello table below hello following assumptions have been made:</span></span>

* <span data-ttu-id="670ce-120">Se ha producido una distribución uniforme de los datos</span><span class="sxs-lookup"><span data-stu-id="670ce-120">An even distribution of data has occurred</span></span> 
* <span data-ttu-id="670ce-121">longitud media de fila de Hello es 250 bytes</span><span class="sxs-lookup"><span data-stu-id="670ce-121">hello average row length is 250 bytes</span></span>

| <span data-ttu-id="670ce-122">[DWU][DWU]</span><span class="sxs-lookup"><span data-stu-id="670ce-122">[DWU][DWU]</span></span> | <span data-ttu-id="670ce-123">Extremo por distribución (GiB)</span><span class="sxs-lookup"><span data-stu-id="670ce-123">Cap per distribution (GiB)</span></span> | <span data-ttu-id="670ce-124">Número de distribuciones</span><span class="sxs-lookup"><span data-stu-id="670ce-124">Number of Distributions</span></span> | <span data-ttu-id="670ce-125">Tamaño máximo de la transacción (GiB)</span><span class="sxs-lookup"><span data-stu-id="670ce-125">MAX transaction size (GiB)</span></span> | <span data-ttu-id="670ce-126"># Filas por distribución</span><span class="sxs-lookup"><span data-stu-id="670ce-126"># Rows per distribution</span></span> | <span data-ttu-id="670ce-127">Máximo de filas por transacción</span><span class="sxs-lookup"><span data-stu-id="670ce-127">Max Rows per transaction</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="670ce-128">DW100</span><span class="sxs-lookup"><span data-stu-id="670ce-128">DW100</span></span> |<span data-ttu-id="670ce-129">1</span><span class="sxs-lookup"><span data-stu-id="670ce-129">1</span></span> |<span data-ttu-id="670ce-130">60</span><span class="sxs-lookup"><span data-stu-id="670ce-130">60</span></span> |<span data-ttu-id="670ce-131">60</span><span class="sxs-lookup"><span data-stu-id="670ce-131">60</span></span> |<span data-ttu-id="670ce-132">4 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-132">4,000,000</span></span> |<span data-ttu-id="670ce-133">240 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-133">240,000,000</span></span> |
| <span data-ttu-id="670ce-134">DW200</span><span class="sxs-lookup"><span data-stu-id="670ce-134">DW200</span></span> |<span data-ttu-id="670ce-135">1.5</span><span class="sxs-lookup"><span data-stu-id="670ce-135">1.5</span></span> |<span data-ttu-id="670ce-136">60</span><span class="sxs-lookup"><span data-stu-id="670ce-136">60</span></span> |<span data-ttu-id="670ce-137">90</span><span class="sxs-lookup"><span data-stu-id="670ce-137">90</span></span> |<span data-ttu-id="670ce-138">6.000.000</span><span class="sxs-lookup"><span data-stu-id="670ce-138">6,000,000</span></span> |<span data-ttu-id="670ce-139">360 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-139">360,000,000</span></span> |
| <span data-ttu-id="670ce-140">DW300</span><span class="sxs-lookup"><span data-stu-id="670ce-140">DW300</span></span> |<span data-ttu-id="670ce-141">2.25</span><span class="sxs-lookup"><span data-stu-id="670ce-141">2.25</span></span> |<span data-ttu-id="670ce-142">60</span><span class="sxs-lookup"><span data-stu-id="670ce-142">60</span></span> |<span data-ttu-id="670ce-143">135</span><span class="sxs-lookup"><span data-stu-id="670ce-143">135</span></span> |<span data-ttu-id="670ce-144">9 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-144">9,000,000</span></span> |<span data-ttu-id="670ce-145">540 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-145">540,000,000</span></span> |
| <span data-ttu-id="670ce-146">DW400</span><span class="sxs-lookup"><span data-stu-id="670ce-146">DW400</span></span> |<span data-ttu-id="670ce-147">3</span><span class="sxs-lookup"><span data-stu-id="670ce-147">3</span></span> |<span data-ttu-id="670ce-148">60</span><span class="sxs-lookup"><span data-stu-id="670ce-148">60</span></span> |<span data-ttu-id="670ce-149">180</span><span class="sxs-lookup"><span data-stu-id="670ce-149">180</span></span> |<span data-ttu-id="670ce-150">12 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-150">12,000,000</span></span> |<span data-ttu-id="670ce-151">720 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-151">720,000,000</span></span> |
| <span data-ttu-id="670ce-152">DW500</span><span class="sxs-lookup"><span data-stu-id="670ce-152">DW500</span></span> |<span data-ttu-id="670ce-153">3,75</span><span class="sxs-lookup"><span data-stu-id="670ce-153">3.75</span></span> |<span data-ttu-id="670ce-154">60</span><span class="sxs-lookup"><span data-stu-id="670ce-154">60</span></span> |<span data-ttu-id="670ce-155">225</span><span class="sxs-lookup"><span data-stu-id="670ce-155">225</span></span> |<span data-ttu-id="670ce-156">15 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-156">15,000,000</span></span> |<span data-ttu-id="670ce-157">900 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-157">900,000,000</span></span> |
| <span data-ttu-id="670ce-158">DW600</span><span class="sxs-lookup"><span data-stu-id="670ce-158">DW600</span></span> |<span data-ttu-id="670ce-159">4.5.</span><span class="sxs-lookup"><span data-stu-id="670ce-159">4.5</span></span> |<span data-ttu-id="670ce-160">60</span><span class="sxs-lookup"><span data-stu-id="670ce-160">60</span></span> |<span data-ttu-id="670ce-161">270</span><span class="sxs-lookup"><span data-stu-id="670ce-161">270</span></span> |<span data-ttu-id="670ce-162">18 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-162">18,000,000</span></span> |<span data-ttu-id="670ce-163">1 080 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-163">1,080,000,000</span></span> |
| <span data-ttu-id="670ce-164">DW1000</span><span class="sxs-lookup"><span data-stu-id="670ce-164">DW1000</span></span> |<span data-ttu-id="670ce-165">7.5</span><span class="sxs-lookup"><span data-stu-id="670ce-165">7.5</span></span> |<span data-ttu-id="670ce-166">60</span><span class="sxs-lookup"><span data-stu-id="670ce-166">60</span></span> |<span data-ttu-id="670ce-167">450</span><span class="sxs-lookup"><span data-stu-id="670ce-167">450</span></span> |<span data-ttu-id="670ce-168">30 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-168">30,000,000</span></span> |<span data-ttu-id="670ce-169">1 800 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-169">1,800,000,000</span></span> |
| <span data-ttu-id="670ce-170">DW1200</span><span class="sxs-lookup"><span data-stu-id="670ce-170">DW1200</span></span> |<span data-ttu-id="670ce-171">9</span><span class="sxs-lookup"><span data-stu-id="670ce-171">9</span></span> |<span data-ttu-id="670ce-172">60</span><span class="sxs-lookup"><span data-stu-id="670ce-172">60</span></span> |<span data-ttu-id="670ce-173">540</span><span class="sxs-lookup"><span data-stu-id="670ce-173">540</span></span> |<span data-ttu-id="670ce-174">36 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-174">36,000,000</span></span> |<span data-ttu-id="670ce-175">2 160 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-175">2,160,000,000</span></span> |
| <span data-ttu-id="670ce-176">DW1500</span><span class="sxs-lookup"><span data-stu-id="670ce-176">DW1500</span></span> |<span data-ttu-id="670ce-177">11,25</span><span class="sxs-lookup"><span data-stu-id="670ce-177">11.25</span></span> |<span data-ttu-id="670ce-178">60</span><span class="sxs-lookup"><span data-stu-id="670ce-178">60</span></span> |<span data-ttu-id="670ce-179">675</span><span class="sxs-lookup"><span data-stu-id="670ce-179">675</span></span> |<span data-ttu-id="670ce-180">45 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-180">45,000,000</span></span> |<span data-ttu-id="670ce-181">2 700 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-181">2,700,000,000</span></span> |
| <span data-ttu-id="670ce-182">DW2000</span><span class="sxs-lookup"><span data-stu-id="670ce-182">DW2000</span></span> |<span data-ttu-id="670ce-183">15</span><span class="sxs-lookup"><span data-stu-id="670ce-183">15</span></span> |<span data-ttu-id="670ce-184">60</span><span class="sxs-lookup"><span data-stu-id="670ce-184">60</span></span> |<span data-ttu-id="670ce-185">900</span><span class="sxs-lookup"><span data-stu-id="670ce-185">900</span></span> |<span data-ttu-id="670ce-186">60 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-186">60,000,000</span></span> |<span data-ttu-id="670ce-187">3 600 000 000</span><span class="sxs-lookup"><span data-stu-id="670ce-187">3,600,000,000</span></span> |
| <span data-ttu-id="670ce-188">DW3000</span><span class="sxs-lookup"><span data-stu-id="670ce-188">DW3000</span></span> |<span data-ttu-id="670ce-189">22.5</span><span class="sxs-lookup"><span data-stu-id="670ce-189">22.5</span></span> |<span data-ttu-id="670ce-190">60</span><span class="sxs-lookup"><span data-stu-id="670ce-190">60</span></span> |<span data-ttu-id="670ce-191">1,350</span><span class="sxs-lookup"><span data-stu-id="670ce-191">1,350</span></span> |<span data-ttu-id="670ce-192">90,000,000</span><span class="sxs-lookup"><span data-stu-id="670ce-192">90,000,000</span></span> |<span data-ttu-id="670ce-193">5,400,000,000</span><span class="sxs-lookup"><span data-stu-id="670ce-193">5,400,000,000</span></span> |
| <span data-ttu-id="670ce-194">DW6000</span><span class="sxs-lookup"><span data-stu-id="670ce-194">DW6000</span></span> |<span data-ttu-id="670ce-195">45</span><span class="sxs-lookup"><span data-stu-id="670ce-195">45</span></span> |<span data-ttu-id="670ce-196">60</span><span class="sxs-lookup"><span data-stu-id="670ce-196">60</span></span> |<span data-ttu-id="670ce-197">2,700</span><span class="sxs-lookup"><span data-stu-id="670ce-197">2,700</span></span> |<span data-ttu-id="670ce-198">180,000,000</span><span class="sxs-lookup"><span data-stu-id="670ce-198">180,000,000</span></span> |<span data-ttu-id="670ce-199">10,800,000,000</span><span class="sxs-lookup"><span data-stu-id="670ce-199">10,800,000,000</span></span> |

<span data-ttu-id="670ce-200">límite de tamaño de transacción de Hola se aplica por transacción u operación.</span><span class="sxs-lookup"><span data-stu-id="670ce-200">hello transaction size limit is applied per transaction or operation.</span></span> <span data-ttu-id="670ce-201">No se aplica en todas las transacciones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="670ce-201">It is not applied across all concurrent transactions.</span></span> <span data-ttu-id="670ce-202">Por lo tanto, cada transacción está permitido toowrite esta cantidad de datos toohello registro.</span><span class="sxs-lookup"><span data-stu-id="670ce-202">Therefore each transaction is permitted toowrite this amount of data toohello log.</span></span> 

<span data-ttu-id="670ce-203">toooptimize y minimizar la cantidad de Hola de los datos escritos toohello registro consulte toohello [prácticas recomendadas de las transacciones] [ Transactions best practices] artículo.</span><span class="sxs-lookup"><span data-stu-id="670ce-203">toooptimize and minimize hello amount of data written toohello log please refer toohello [Transactions best practices][Transactions best practices] article.</span></span>

> [!WARNING]
> <span data-ttu-id="670ce-204">Hola máximo tamaño de las transacciones solo se pueden conseguir para HASH o tablas ROUND_ROBIN distribuidas donde propagarse Hola Hola datos es par.</span><span class="sxs-lookup"><span data-stu-id="670ce-204">hello maximum transaction size can only be achieved for HASH or ROUND_ROBIN distributed tables where hello spread of hello data is even.</span></span> <span data-ttu-id="670ce-205">Si transacción Hola está escribiendo datos en un modo sesgado distribuciones toohello, a continuación, hello límite es probable toobe alcanzado el tamaño máximo de la transacción de toohello anteriores.</span><span class="sxs-lookup"><span data-stu-id="670ce-205">If hello transaction is writing data in a skewed fashion toohello distributions then hello limit is likely toobe reached prior toohello maximum transaction size.</span></span>
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a><span data-ttu-id="670ce-206">Estado de las transacciones</span><span class="sxs-lookup"><span data-stu-id="670ce-206">Transaction state</span></span>
<span data-ttu-id="670ce-207">Almacenamiento de datos de SQL utiliza hello xact_state función tooreport una transacción errónea con hello valor -2.</span><span class="sxs-lookup"><span data-stu-id="670ce-207">SQL Data Warehouse uses hello XACT_STATE() function tooreport a failed transaction using hello value -2.</span></span> <span data-ttu-id="670ce-208">Esto significa que transacción Hola ha fallado y se marca para la reversión solo</span><span class="sxs-lookup"><span data-stu-id="670ce-208">This means that hello transaction has failed and is marked for rollback only</span></span>

> [!NOTE]
> <span data-ttu-id="670ce-209">Hola el uso de -2 por hello XACT_STATE función toodenote un comportamiento diferente de representa transacción errónea tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="670ce-209">hello use of -2 by hello XACT_STATE function toodenote a failed transaction represents different behavior tooSQL Server.</span></span> <span data-ttu-id="670ce-210">SQL Server utiliza el valor -1 de hello toorepresent una transacción no confirmable.</span><span class="sxs-lookup"><span data-stu-id="670ce-210">SQL Server uses hello value -1 toorepresent an un-committable transaction.</span></span> <span data-ttu-id="670ce-211">SQL Server puede tolerar algunos errores dentro de una transacción sin necesidad de toobe marcado como no confirmable.</span><span class="sxs-lookup"><span data-stu-id="670ce-211">SQL Server can tolerate some errors inside a transaction without it having toobe marked as un-committable.</span></span> <span data-ttu-id="670ce-212">Por ejemplo, `SELECT 1/0` producirá un error pero no fuerza una transacción en un estado no confirmable.</span><span class="sxs-lookup"><span data-stu-id="670ce-212">For example `SELECT 1/0` would cause an error but not force a transaction into an un-committable state.</span></span> <span data-ttu-id="670ce-213">SQL Server también permite a las lecturas de transacción no confirmable Hola.</span><span class="sxs-lookup"><span data-stu-id="670ce-213">SQL Server also permits reads in hello un-committable transaction.</span></span> <span data-ttu-id="670ce-214">Sin embargo, Almacenamiento de datos SQL no permite hacerlo.</span><span class="sxs-lookup"><span data-stu-id="670ce-214">However, SQL Data Warehouse does not let you do this.</span></span> <span data-ttu-id="670ce-215">Si se produce un error dentro de una transacción de almacenamiento de datos SQL se pasará automáticamente al estado de hello -2 y no será capaz de toomake cualquiera más instrucciones select hasta que se ha revertido instrucción Hola.</span><span class="sxs-lookup"><span data-stu-id="670ce-215">If an error occurs inside a SQL Data Warehouse transaction it will automatically enter hello -2 state and you will not be able toomake any further select statements until hello statement has been rolled back.</span></span> <span data-ttu-id="670ce-216">Por lo tanto es toocheck importante que su toosee de código de aplicación si usa xact_state que puede requerir modificaciones en el código toomake.</span><span class="sxs-lookup"><span data-stu-id="670ce-216">It is therefore important toocheck that your application code toosee if it uses  XACT_STATE() as you may need toomake code modifications.</span></span>
> 
> 

<span data-ttu-id="670ce-217">Por ejemplo, puede que vea una transacción con el siguiente aspecto en SQL Server:</span><span class="sxs-lookup"><span data-stu-id="670ce-217">For example, in SQL Server you might see a transaction that looks like this:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="670ce-218">Si deja el código tal cual está por encima obtendrá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="670ce-218">If you leave your code as it is above then you will get hello following error message:</span></span>

<span data-ttu-id="670ce-219">Msg 111233, nivel 16, estado 1, línea 1 111233; Hola actual anuló la transacción y los cambios pendientes se han revertido.</span><span class="sxs-lookup"><span data-stu-id="670ce-219">Msg 111233, Level 16, State 1, Line 1 111233;hello current transaction has aborted, and any pending changes have been rolled back.</span></span> <span data-ttu-id="670ce-220">Causa: una transacción en estado de solo reversión no se ha revertido explícitamente antes de la instrucción DDL, DML o SELECT.</span><span class="sxs-lookup"><span data-stu-id="670ce-220">Cause: A transaction in a rollback-only state was not explicitly rolled back before a DDL, DML or SELECT statement.</span></span>

<span data-ttu-id="670ce-221">También puede obtener no salida Hola de hello error. * funciones.</span><span class="sxs-lookup"><span data-stu-id="670ce-221">You will also not get hello output of hello ERROR_* functions.</span></span>

<span data-ttu-id="670ce-222">En el almacén de datos de SQL código de hello necesita toobe ligeramente modificado:</span><span class="sxs-lookup"><span data-stu-id="670ce-222">In SQL Data Warehouse hello code needs toobe slightly altered:</span></span>

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

<span data-ttu-id="670ce-223">Hola espera ahora se observa el comportamiento.</span><span class="sxs-lookup"><span data-stu-id="670ce-223">hello expected behavior is now observed.</span></span> <span data-ttu-id="670ce-224">se administra el error de Hello en transacciones de Hola y Hola error. * funciones que proporcionan valores según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="670ce-224">hello error in hello transaction is managed and hello ERROR_* functions provide values as expected.</span></span>

<span data-ttu-id="670ce-225">Todo lo que ha cambiado es ese hello `ROLLBACK` de hello transacción tenía toohappen antes de que Hola de lectura de la información de error de Hola Hola `CATCH` bloque.</span><span class="sxs-lookup"><span data-stu-id="670ce-225">All that has changed is that hello `ROLLBACK` of hello transaction had toohappen before hello read of hello error information in hello `CATCH` block.</span></span>

## <a name="errorline-function"></a><span data-ttu-id="670ce-226">Función Error_Line()</span><span class="sxs-lookup"><span data-stu-id="670ce-226">Error_Line() function</span></span>
<span data-ttu-id="670ce-227">También merece la pena destacar que almacenamiento de datos SQL no implementar admitir o función de hello error_line ().</span><span class="sxs-lookup"><span data-stu-id="670ce-227">It is also worth noting that SQL Data Warehouse does not implement or support hello ERROR_LINE() function.</span></span> <span data-ttu-id="670ce-228">Si tiene esto en el código debe tooremove toobe compatible con el almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="670ce-228">If you have this in your code you will need tooremove it toobe compliant with SQL Data Warehouse.</span></span> <span data-ttu-id="670ce-229">Usar etiquetas de consulta en el código en su lugar tooimplement una funcionalidad equivalente.</span><span class="sxs-lookup"><span data-stu-id="670ce-229">Use query labels in your code instead tooimplement equivalent functionality.</span></span> <span data-ttu-id="670ce-230">Consulte toohello [etiqueta] [ LABEL] artículo para obtener más información acerca de esta característica.</span><span class="sxs-lookup"><span data-stu-id="670ce-230">Please refer toohello [LABEL][LABEL] article for more details on this feature.</span></span>

## <a name="using-throw-and-raiserror"></a><span data-ttu-id="670ce-231">Uso de THROW y RAISERROR</span><span class="sxs-lookup"><span data-stu-id="670ce-231">Using THROW and RAISERROR</span></span>
<span data-ttu-id="670ce-232">THROW es Hola implementación más moderno para generar excepciones en el almacén de datos de SQL pero RAISERROR también se admite.</span><span class="sxs-lookup"><span data-stu-id="670ce-232">THROW is hello more modern implementation for raising exceptions in SQL Data Warehouse but RAISERROR is also supported.</span></span> <span data-ttu-id="670ce-233">Hay algunas diferencias que son vale la pena prestar atención toohowever.</span><span class="sxs-lookup"><span data-stu-id="670ce-233">There are a few differences that are worth paying attention toohowever.</span></span>

* <span data-ttu-id="670ce-234">Números no pueden estar en hello 100.000 150.000 intervalo para THROW de mensajes de error definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="670ce-234">User defined error messages numbers cannot be in hello 100,000 - 150,000 range for THROW</span></span>
* <span data-ttu-id="670ce-235">Los mensajes de error RAISERROR se fijan en 50.000.</span><span class="sxs-lookup"><span data-stu-id="670ce-235">RAISERROR error messages are fixed at 50,000</span></span>
* <span data-ttu-id="670ce-236">No se admite el uso de sys.messages.</span><span class="sxs-lookup"><span data-stu-id="670ce-236">Use of sys.messages is not supported</span></span>

## <a name="limitiations"></a><span data-ttu-id="670ce-237">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="670ce-237">Limitiations</span></span>
<span data-ttu-id="670ce-238">Almacenamiento de datos de SQL tiene algunas otras restricciones que se relacionan tootransactions.</span><span class="sxs-lookup"><span data-stu-id="670ce-238">SQL Data Warehouse does have a few other restrictions that relate tootransactions.</span></span>

<span data-ttu-id="670ce-239">Los pasos son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="670ce-239">They are as follows:</span></span>

* <span data-ttu-id="670ce-240">Transacciones no distribuidas</span><span class="sxs-lookup"><span data-stu-id="670ce-240">No distributed transactions</span></span>
* <span data-ttu-id="670ce-241">Transacciones anidadas no permitidas</span><span class="sxs-lookup"><span data-stu-id="670ce-241">No nested transactions permitted</span></span>
* <span data-ttu-id="670ce-242">Puntos de almacenamiento no admitidos</span><span class="sxs-lookup"><span data-stu-id="670ce-242">No save points allowed</span></span>
* <span data-ttu-id="670ce-243">Sin transacciones con nombre</span><span class="sxs-lookup"><span data-stu-id="670ce-243">No named transactions</span></span>
* <span data-ttu-id="670ce-244">Sin transacciones marcadas</span><span class="sxs-lookup"><span data-stu-id="670ce-244">No marked transactions</span></span>
* <span data-ttu-id="670ce-245">No existe compatibilidad con DDL como el elemento `CREATE TABLE` de una transacción definida por el usuario</span><span class="sxs-lookup"><span data-stu-id="670ce-245">No support for DDL such as `CREATE TABLE` inside a user defined transaction</span></span>

## <a name="next-steps"></a><span data-ttu-id="670ce-246">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="670ce-246">Next steps</span></span>
<span data-ttu-id="670ce-247">toolearn más acerca de cómo optimizar las transacciones, vea [prácticas recomendadas de las transacciones][Transactions best practices].</span><span class="sxs-lookup"><span data-stu-id="670ce-247">toolearn more about optimizing transactions, see [Transactions best practices][Transactions best practices].</span></span>  <span data-ttu-id="670ce-248">toolearn sobre otras prácticas recomendadas de almacenamiento de datos SQL, consulte [prácticas recomendadas de almacenamiento de datos SQL][SQL Data Warehouse best practices].</span><span class="sxs-lookup"><span data-stu-id="670ce-248">toolearn about other SQL Data Warehouse best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse best practices].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
